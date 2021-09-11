# Redis高可靠之AOF篇
Redis为解决宕机数据丢失问题，提供了AOF日志机制，实现数据持久化，用于数据恢复。

## 一. AOF基本知识
### AOF定义
AOF是以文本形式，记录了每个键值对的操作命令，以便在需要时恢复数据。  

![](Redis图/AOF日志内容.png)
以“set testkey testvalue”为例。AOF文件
内容如图所示，其中：  
* “*3”：当前命令有三个部分，每部分都是由 “$+数字”开头，后面紧跟着具体
的命令、键或值。  
* “$+数字”：表示这部分中的 命令、键或值一共有多少字节。

### AOF是写后日志
![](Redis图/AOF后写.png)
Redis先执行命令，再写日志
好处：
1. Redis没有做语法检查，可避免记录到错误的命令
2. 不会阻塞当前写操作  

风险：
1. 刚执行完命令就宕机，来不及写入日志
2. 可能会给下一个操作带来阻塞风险  

### AOF缓冲区
文件IO是操作系统的性能短板，Redis的追加操作只是把数据写入缓冲区（aof_buf）,从缓冲区
写入磁盘有几种策略选择。

## 持久化流程
![img_3.png](Redis图/AOF流程.png)
主要有几个过程：命令追加、文件写入和同步、AOF重写、数据重新加载

### 命令追加
追加的命令先写道缓存区aof_buf，如果此时正在AOF重写，这些命令还会追加到重写缓冲区aof_rewrite_buffer。

### 文件写入和同步
从流程图可看出，redis在将aof_buf写入内核缓存区后，会有三种策略来决定何时将内核缓冲区的数据
写入磁盘：
**Always**，同步写回：每个写命令执行完，立马同步地将日志写回磁盘；  
**Everysec**，每秒写回：每个写命令执行完，只是先把日志写到 AOF 文件的内存缓冲区，每隔一秒把缓冲区中的内容写入磁盘；  
**No**，操作系统控制的写回：每个写命令执行完，只是先把日志写到 AOF 文件的内存缓冲区，由操作系统决定何时将缓冲区内容写回磁盘。  

下图总结了三种策略的优劣

![img.png](Redis图/AOF写回策略.png)

### AOF重写
AOF文件太大的话会影响性能。

    1.文件太大，往里面追加命令，效率会降低
    2.日志里的命令太多，影响恢复速度
![img_2.png](Redis图/AOF重写含义.png)
AOF重写就是，当一个键值对被反复修改，重写只记录最新状态对应的写操作。

### 重写过程
AOF重写毕竟是要将整个数据库的最新数据的操作日志都写回磁盘，很耗时。所以用子进程完成重写

    AOF日志由主线程写回，而重写过程是由后台子进程bgrewriteaof完成。

#### AOF重写触发条件
1. 手动触发  
   直接调用bgrewriteaof命令
2. 自动触发
   由Redis的周期性方法serverCron检查在满足一定条件时触发。  
   先介绍几个参数含义：  
   * aof_current_size：serverCron执行时AOF文件的实时大小  
   * aof_base_size：上一次重写后AOF文件大小  
   两个配置项：
   * auto-aof-rewrite-percentage：代表当前AOF文件大小（aof_current_size）和上一次重写后AOF文件大小（aof_base_size）相比，增长的比例。
   * auto-aof-rewrite-min-size：表示运行BGREWRITEAOF时AOF文件占用空间最小值，默认为64MB；
   
   当满足以下两个条件时，AOF文件重写就会触发：

       增长比例：(aof_current_size - aof_base_size) / aof_base_size > auto-aof-rewrite-percentage
       文件大小：aof_current_size > auto-aof-rewrite-min-size
3. 重写流程
![img_5.png](Redis图/AOF重写流程.png)

### 数据加载流程
![img_4.png](Redis图/AOF数据加载流程.png)



