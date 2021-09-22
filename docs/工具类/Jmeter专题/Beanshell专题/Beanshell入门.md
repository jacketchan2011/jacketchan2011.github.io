# Bean Shell 官方介绍
BeanShell 是一种完全符合Java语法规范的脚本语言，并且又拥有自己的一些语法和方法
BeanShell 执行标准 Java 语句和表达式，另外包括一些脚本命令和语法。

官网:http://www.BeanShell.org/

 

# Jmeter有哪些Bean Shell
* 定时器：　　BeanShell Timer
* 前置处理器：BeanShell PreProcessor
* 采样器：　　BeanShell Sampler
* 后置处理器：BeanShell PostProcessor
* 断言：　　　BeanShell 断言
* 监听器：　　BeanShell Listener
 

# Bean Shell常用内置变量
JMeter 在 BeanShell 中内置了很多变量，我们可以通过这些变量与 JMeter 进行交互

## log
打印日志，并写入信息到 jmeber.log 文件

## ctx
该变量引用了当前线程的上下文，使用方法可参考：org.apache.jmeter.threads.JMeterContext


## vars
操作 JMeter 变量，这个变量实际引用了 JMeter 线程中的局部变量容器（本质上是Map），它是测试用例与 BeanShell 交互的桥梁，更多方法可参考：org.apache.jmeter.threads.JMeterVariables

## props
操作 JMeter 属性，该变量引用了 JMeter 的配置信息，可以获取 JMeter 的属性，它的使用方法与 vars 类似，但是只能 put 进去 String 类型的值，而不能是一个对象，对应于 java.util.Properties 

## prev
获取前面的 Sampler 返回的信息，更多方法可参考：org.apache.jmeter.samplers.SampleResult

