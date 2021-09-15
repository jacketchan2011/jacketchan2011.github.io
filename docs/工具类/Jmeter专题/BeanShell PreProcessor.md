# BeanShell PreProcessor
BeanShell PreProcessor：通常在发送请求前，需要构造输入报文。可用此组件达到目的。

这个我不常用，但是要用的时候又不怎么会用。  
简单的玩法：
1. 内置变量vars：提供了对**当前线程**变量的读写能力。
* vars.get(String key)：从jmeter中获得变量值  
* vars.put(String key，String value)：数据存到jmeter变量中  

总结一下：哪里的变量可以被vars读写呢？
* 测试计划中的用户自定义变量
* 用户定义的变量啊
* 啊，太多了，不写了，只要是全局变量或本线程的局部变量都可以(csv数据文件设置中的变量貌似无法读取)

另外还发现一个，不定义变量直接vars.put("A", "a")，相当于声明且赋值了变量A。

2. props：读写jmeter属性，用这个可以读写其他线程的变量

props可读写其他线程的变量，可以在不同线程之间传递变量了。

用法一：将JMeter变量转换为JMeter属性  
给定一个变量“some_variable”，您必须使用相同的名称强制转换JMeter属性以使用（例如在另一个线程组中）。
        
    props.put("some_variable",vars.get("some_variable"));
用法二：设置jmeter属性
${__setProperty(var-name, ${var-name},)}