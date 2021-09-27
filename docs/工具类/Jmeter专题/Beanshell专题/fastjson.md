# Fastjson简介
fastjson是阿里巴巴的开源JSON解析库，它可以解析JSON格式的字符串，支持将Java Bean序列化为JSON字符串，也可以从JSON字符串反序列化到JavaBean。

Fastjson这个开源jar包经常用，主要是构造入参时，需要对string转json对象，做一些入参值的替换

Fastjson 源码地址：https://github.com/alibaba/fastjson

引入jar包，然后import

    import com.alibaba.fastjson.JSON;
    import com.alibaba.fastjson.JSONArray;
    import com.alibaba.fastjson.JSONObject;

## string转jsonObject
    
       private static final String  JSON_OBJ_STR = "{\"studentName\":\"lily\",\"studentAge\":12}";
       JSONObject jsonObject = JSONObject.parseObject(JSON_OBJ_STR);  
转为json格对象后，就可用jsonObject.replace()来修改其中的key-value

## JsonObject转String

       //已知JSONObject,目标要转换为json字符串
       JSONObject jsonObject = JSONObject.parseObject(JSON_OBJ_STR);
       //第一种方法
       String jsonOutput= JSON.toJSONString(listOfPersons);
       //第二种方法
       String jsonString = jsonObject.toJSONString();

## 字符串(数组类型)转JSONArray

       private static final String  JSON_ARRAY_STR = "[{\"studentName\":\"lily\",\"studentAge\":12},{\"studentName\":\"lucy\",\"studentAge\":15}]";
       JSONArray jsonArray = JSONArray.parseArray(JSON_ARRAY_STR);

## JSONArray转String
    
       //第一种方式
       String jsonString = JSONArray.toJSONString(jsonArray);
       // 第二种方式
       String jsonString = jsonArray.toJSONString(jsonArray);