CLI模式，即命令行模式。

# CLI 模式可选参数
| 字段 | 含义 | 
| ------| ------ | 
| -n | 指定jmeter在cli模式运行 | 
| -t | 指定执行的jmx文件 | 
| -l | 指定记录测试结果的jtl文件名 | 
| -e | 生成html格式的测试报表 | 
| -o | 生成测试报表的文件夹，文件夹必须不存在或为空 | 
| -g | 输出报告文件 | 
| -j | 记录jmeter运行日志的文件名和文件路径 | 

栗子（-n,-t,-l,-e,-o）：

      //执行jmx脚本，并在result目录下生成 report.jtl 报告
      //report.jtl存在也没关系，可以自动覆盖
      jmeter -n -t FlaskDemo.jmx -l result/report.jtl

      //执行jmx脚本,生成jtl报告，最后在report目录下生成测试报表
      //切记：report.jtl必须不存在，report目录必须不存在或者为空
      jmeter -n -t FlaskDemo.jmx -l result/report.jtl -e -o report

栗子（-g）：

      //jtl文件转html测试报告
      jmeter -g report.jtl -o report

# 服务器相关参数
| 字段 | 含义 |
| ----- | ----- |
| -r | 所有远程服务器中运行测试 |
| -R | 在指定的远程服务器中运行测试 |
| -X | 服务器运行完脚本后自动停止 jmeter-server |
| -H | 代理服务器的host或ip |
| -P | 代理服务器的port |
|  |  |

栗子（-r）：

    //会执行 jmeter.properties 的 remote_hosts 填的所有远程slave机
    jmeter -n -t FlaskDemo.jmx -r -l result/report.jtl

   1.设置jmeter属性
    ![img_2.png](imgs/img_2.png)
   2.master机执行命令
    ![img_3.png](imgs/img_3.png)
   3.slave机
    ![img_4.png](imgs/img_4.png)
   4.本地slave机
    ![img_5.png](imgs/img_5.png)

栗子（-R）：

    //启动指定的远程slave机执行jmx，并在result目录下生成report.jtl  
    jmeter -n -t FlaskDemo.jmx -l result/report.jtl  -R 172.20.72:38:1234
  
栗子（-X）：

    jmeter -n -t FlaskDemo.jmx -l result/report.jtl  -R 172.20.72:38:1234 -X

   1.master 机，跑了两次，第一次没有 -X，第二次加了 -X
    ![img_6.png](imgs/img_6.png)
   2.slave 机
    ![img_7.png](imgs/img_7.png)


# 属性参数
Java 系统属性和 JMeter 属性可以直接通过以下命令进行覆盖，而不用手动修改 jmeter.properties

| 格式 | 含义 |
| ----- | ----- |
| -D[prop_name]=[value]|	定义一个 Java 系统属性值|
|-J[prop_name]=[value]	|定义本地 JMeter 属性|
|-G[prop_name]=[value]	|定义要发送到所有远程服务器的 JMeter 属性|
|-G[propertyfile]	|定义一个包含 JMeter 属性的文件，该文件将发送到所有远程服务器|
|-L[category]=[priority]|覆盖日志记录设置，将特定类别设置为给定的优先级；设置根日志记录级别 |

    jmeter -n -t xxx.jmx -l xxx.jtl -JclientId 8C3wdasdqd