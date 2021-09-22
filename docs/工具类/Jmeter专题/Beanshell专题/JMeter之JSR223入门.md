# JSR223 介绍
* JMeter 支持使用编程语言来开发测试，最常用的莫过于 BeanShell
* 但是 BeanShell 脚本的效率却不高
* 针对此种情况，JMeter 给了测试开发人员更多的选择，引入了 JSR223 组件元素，提供了使用多种编程语言开发测试的可能性，其中包括了性能较高的Groovy语言
* 在使用 JSR223 组件元素开发测试时，可以使用其内置的变量，有助于精简脚本，提高开发测试的效率
* JSR223 定义了可集成在Java平台上运行的一系列脚本语言，比如 Groovy，JavaScript 等
 

# Jmeter  有哪些 JSR223
* 定时器：　　JSR223 Timer
* 前置处理器：JSR223 PreProcessor
* 采样器：　　JSR223 Sampler
* 后置处理器：JSR223 PostProcessor
* 断言：　　　JSR223 断言
* 监听器：　　JSR223 Listener
 

# 总结
如果要写 BeanShell 脚本的话，建议使用 JSR223 组件，因为基本都一样，效率也高很多