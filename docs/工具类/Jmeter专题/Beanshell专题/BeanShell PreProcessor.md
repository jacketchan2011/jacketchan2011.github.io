# BeanShell PreProcessor
BeanShell PreProcessor：通常在发送请求前，需要构造输入报文。可用此组件达到目的。

这个我不常用，但是要用的时候又不怎么会用。  
简单的玩法：
## 读写变量
### vars
提供了对**当前线程**变量的读写能力。
* vars.get(String key)：从jmeter中获得变量值  
* vars.put(String key，String value)：数据存到jmeter变量中  

总结一下：哪里的变量可以被vars读写呢？
* 测试计划中的用户自定义变量
* 用户定义的变量
* 随机变量
* 计数器
* ……
只要是全局变量或本线程的局部变量都可以(csv数据文件设置中的变量貌似无法读取)

另外还发现一个，vars.put("A", "a")，相当于创建且赋值了变量A。

### props
读写jmeter属性，可读写其他线程的变量

props.put("属性名","属性值")：创建一个属性并赋值
props.get("属性名")：使用BeanShell内置对象获取属性值;

## jmeter属性相关的内置函数
三个jmeter内置函数（可在jmeter任何地方用，当然包括beanshell），用法详见**Jmeter常见内置函数**篇

**${__setProperty(property name, property value, True/False)}**  
该函数用来给JMeter属性设置值，默认返回值为空字符串，所以在函数在任何地方被调用是有效的

**${__property(property name , variable name, default value)}**  
函数返回JMeter的属性值。如果找不到到属性值而且没有提供默认值，将返回属性名。在有提供默认值时，可以选择不用提供引用名(可选的)。

**${__P(property name, default value)}**
__P是__property函数的简化版，用来返回jmeter属性的值，可以在命令行中使用也可以在beanshell中用，

举个例子：

${__P(prop1)} 会返回属性prop1的值；  
${__P(prop1,www.bidu.com)} 会返回属性prop1的值，如果prop1未定义值，则返回www.baidu.com；

用法上__property函数仅仅是比__P函数多了一个可以存值的变量，举例：  
${__property(prop1,var1,shanghai)}会返回prop1的值，如果prop1未定义值则会返回shanghai，同时会将prop1的值存到变量var1中

总结：

${__setProperty()}与${__property()}/${__P()}一起配合使用，setProptety等于把值拿出来，
__property/__P   
1.可以把setProperty 的值直接拿出来  
2.可以对已存在的变量重新赋值


## 引入外部文件
### 引入java文件
在beanshell组件中引入：

    source("D://xxx.java");
然后就能用该java文件的类和函数了。
### addClassPath
一个java文件不够用？那就引入整个项目，再通过import引用该目录下的类。
 
    addClassPath("D://xxx/src")
    //引入
    import mutest.Md5Encryption;

    String passwordIni = "123456";
    // 调用加密方法
    String passwordEncryp = new Md5Encryption().md5Encryption(passwordIni);
    vars.put("passwordEncryp",passwordEncryp);
### 引入jar包
将项目打成jar包，导入JMeter安装目录\lib\etc中，并重启JMeter。然后直接在beanshell组件中import。