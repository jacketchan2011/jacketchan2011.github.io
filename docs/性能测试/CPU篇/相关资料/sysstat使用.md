## mpstat
查看每个 CPU 的使用情况。

### 语法
    mpstat [-P {|ALL}] [internal [count]]
    参数 解释
    -P {|ALL} 表示监控哪个CPU， cpu在[0,cpu个数-1]中取值
    internal 相邻的两次采样的间隔时间、
    count 采样的次数，count只能和delay一起使用
    当没有参数时，mpstat则显示系统启动以后所有信息的平均值。有interval时，第一行的信息自系统启动以来的平均信息。从第二行开始，输出为前一个interval时间段的平均信息。

例子：mpstat  -P ALL 2
### 返回字段含义
* %user      在internal时间段里，用户态的CPU时间(%)，不包含nice值为负进程  (usr/total)*100
* %nice      在internal时间段里，nice值为负进程的CPU时间(%)   (nice/total)*100
* %sys       在internal时间段里，内核时间(%)       (system/total)*100
* %iowait    在internal时间段里，硬盘IO等待时间(%) (iowait/total)*100
* %irq       在internal时间段里，硬中断时间(%)     (irq/total)*100
* %soft      在internal时间段里，软中断时间(%)     (softirq/total)*100
* %idle      在internal时间段里，CPU除去等待磁盘IO操作外的因为任何原因而空闲的时间闲置时间(%) (idle/total)*100

## pidstat
用于监控全部或指定进程的cpu、内存、线程、设备IO等系统资源的占用情况。
### 语法
    pidstat [ 选项 ] [ <时间间隔> ] [ <次数> ]
常用参数：
* -u：默认的参数，显示各个进程的cpu使用统计
* -r：显示各个进程的内存使用统计
* -d：显示各个进程的IO使用情况
* -p：指定进程号
* -w：显示每个进程的上下文切换情况
* -t：显示选择任务的线程的统计信息外的额外信息
* -T { TASK | CHILD | ALL }   
这个选项指定了pidstat监控的。TASK表示报告独立的task，CHILD关键字表示报告进程下所有线程统计信息。ALL表示报告独立的task和task下面的所有线程。  
注意：task和子线程的全局的统计信息和pidstat选项无关。这些统计信息不会对应到当前的统计间隔，这些统计信息只有在子线程kill或者完成的时候才会被收集。
* -V：版本号
* -h：在一行上显示了所有活动，这样其他程序可以容易解析。
* -I：在SMP环境，表示任务的CPU使用率/内核数量
* -l：显示命令名和所有参数

