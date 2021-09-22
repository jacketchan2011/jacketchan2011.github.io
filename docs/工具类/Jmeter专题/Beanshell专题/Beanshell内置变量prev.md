# 简单介绍
* prev 提供对当前取样器结果的访问能力
* prev 映射 org.apache.jmeter.samplers 的 SampleResult 类
* 官方文档： https://jmeter.apache.org/api/org/apache/jmeter/samplers/SampleResult.html
 

# 常用方法
## getResponseCode
*方法声明  
public String getResponseCode()

* 功能  
获取响应状态码

* 栗子代码

      sc = prev.getResponseCode() ;
      log.info('status code is: ' + sc)
 

## isResponseCodeOK
* 方法声明  
public boolean isResponseCodeOK()

* 功能  
判断响应状态码是否为OK对应的状态码（200）

* 栗子代码

      yn = prev.isResponseCodeOK()
      log.info('yn is: ' + yn)
  返回 true 或 false

 

## getThreadName
* 方法声明  
public String getThreadName()

* 功能  
获取线程名

* 栗子代码

      tname = prev.getThreadName()
      log.info('tname is: ' + tname)
 

## getAssertionResults
* 方法声明  
public AssertionResult[] getAssertionResults()

* 功能  
获取取样器断言结果

* 栗子代码

      ars = prev.getAssertionResults()
      ars.each{
          log.info(it.getName() + ': ' + it.getFailureMessage())
      }
 

## getContentType
* 方法声明  
public String getContentType()

* 功能  
获取取样器响应Content-Type首部字段的值域（包含参数）

* 栗子代码

      ct = prev.getContentType()
      log.info('ct is: ' + ct)
 
## getMediaType
* 方法声明  
public String getMediaType()

* 功能  
获取取样器响应Media-Type首部字段的值域（不包含参数）

* 栗子代码

      ct = prev.getMediaType()
      log.info('ct is: ' + ct)
 

## getSentBytes
* 方法声明  
public long getSentBytes()

* 功能  
获取取样器请求报文的大小

* 栗子代码
  
      sb = prev.getSentBytes()
      log.info('sb is: ' + sb)
 

## getBytesAsLong
* 方法声明  
public long getBytesAsLong()

* 功能  
获取取样器响应报文的大小

* 栗子代码
       
      rb = prev.getBytesAsLong()
      log.info('rb is: ' + rb)
 

## getLatency
* 方法声明  
public long getLatency()

* 功能  
获取延迟时间

## getConnectTime
* 方法声明  
public long getConnectTime()

* 功能  
获取连接时间

## getURL
* 方法声明  
public URL getURL()

* 功能
获取取样器请求URL

* 栗子代码
    
      url = prev.getURL()
      log.info('url is: ' + url)
 
## getUrlAsString
* 方法声明  
public String getUrlAsString()

* 功能  
获取取样器请求URL字符串

## getGroupThreads
* 方法声明  
public int getGroupThreads()

* 功能  
获取线程组下正在运行的线程数

* 栗子代码

      gtnum = prev.getGroupThreads()
      log.info('gtnum is: ' + gtnum)
 

## getHeadersSize
* 方法声明
public int getHeadersSize()

* 功能  
获取取样器响应首部字段大小

* 栗子代码

      hs = prev.getHeadersSize()
      log.info('hs is: ' + hs)
 

## getBodySizeAsLong
* 方法声明  
public long getBodySizeAsLong()

* 功能  
获取取样器响应正文大小

* 栗子代码

      bs = prev.getBodySizeAsLong()
      log.info('bs is: ' + bs)