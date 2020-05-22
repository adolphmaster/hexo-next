---
title: Java中对象、json、list、map等互转专题-网络整理
comments: true
share: true
toc: true
categories:
  - java
tags:
  - [java,java基础]
date: 2019-12-07 09:56:47
---



# Java中对象、json、list、map等互转专题-网络整理

## fastjson方式

### 1.对象与字符串之间的互转

```java
将对象转换成为字符串
String str = JSON.toJSONString(oneObject);
字符串转换成为对象
OneObject oneObject = JSON.parseObject(str, OneObject.class);
```

### 2.对象集合与字符串之间的互转

```java
将对象集合转换成为字符串
String strList = JSON.toJSONString(oneObjectList);
将字符串转换成为对象集合
List<User> oneObjectList = JSON.parseArray(strList, OneObject.class);  
```

### 3.字符串互转JSONObject

```java
//String 转 Json对象
JSONObject jsonObject = JSONObject.parseObject(str);
//json对象转字符串 
String jsonString = jsonObject.toJSONString();
```

### 4.map与字符串之间互转

```java
  //map转字符串
  String jsonString = JSON.toJSONString(map); 

  //字符串转map的几种方式   
 
  //第一种方式  
  Map maps = (Map)JSON.parse(str);  
  System.out.println("这个是用JSON类来解析JSON字符串!!!");  
  for (Object map : maps.entrySet()){  
     System.out.println(((Map.Entry)map).getKey()+"-" + ((Map.Entry)map).getValue());  
  }  
  //第二种方式  
  Map mapTypes = JSON.parseObject(str);  
  System.out.println("这个是用JSON类的parseObject来解析JSON字符串!!!");  
  for (Object obj : mapTypes.keySet()){  
      System.out.println("key为："+obj+"值为："+mapTypes.get(obj));  
  }  
  //第三种方式  
  Map mapType = JSON.parseObject(str,Map.class);  
  System.out.println("这个是用JSON类,指定解析类型，来解析JSON字符串!!!");  
  for (Object obj : mapType.keySet()){  
       System.out.println("key为："+obj+"值为："+mapType.get(obj));  
  }  
  //第四种
  Map<String, Object> map = JSON.parseObject(result,
                                           new TypeReference<Map<String, Object>>(){});
  //第五种方式
  JSONArray listObjectSeven = JSON.parseArray(strArr);
  System.out.println("利用JSON中的parseArray方法来解析json数组字符串");
  for(Object mapList : listObjectSeven){
      for (Object entry : ((Map)mapList).entrySet()){
          System.out.println(((Map.Entry)entry).getKey()  + "  " +
                             			((Map.Entry)entry).getValue());
      }
  }
  //第六种方式  
  /** 
    * JSONObject是Map接口的一个实现类 
    */  
  Map json = (Map) JSONObject.parse(str);  
  System.out.println("这个是用JSONObject类的parse方法来解析JSON字符串!!!");  
  for (Object map : json.entrySet()){  
     System.out.println(((Map.Entry)map).getKey()+"  "+((Map.Entry)map).getValue());  
  }  
  //第七种方式  
  /** 
    * JSONObject是Map接口的一个实现类 
    */  
  JSONObject jsonObject = JSONObject.parseObject(str);
  //json对象转Map
  //Map<String,Object> map = (Map<String,Object>)jsonObject;
  System.out.println("这个是用JSONObject的parseObject方法来解析JSON字符串!!!");  
  for (Object map : json.entrySet()){  
      System.out.println(((Map.Entry)map).getKey()+"  "+((Map.Entry)map).getValue());  
  }  

  //第八种方式  
  /** 
    * JSONObject是Map接口的一个实现类 
    */  
  Map mapObj = JSONObject.parseObject(str,Map.class);  
  System.out.println("这个是用JSONObject的parseObject方法并执行返回类型来解析JSON字符串!!!");  
  for (Object map: json.entrySet()){  
     System.out.println(((Map.Entry)map).getKey()+"  "+((Map.Entry)map).getValue());  
  }  
  //第九种方式
  JSONArray listObjectFifth = JSONObject.parseArray(strArr);
  System.out.println("利用JSONObject中的parseArray方法来解析json数组字符串");
  for(Object mapList : listObjectFifth){
      for (Object entry : ((Map)mapList).entrySet()){
          System.out.println(((Map.Entry)entry).getKey()  + "  " +
                             				((Map.Entry)entry).getValue());
      }
  }
  //第十种方式
  List listObjectSix = JSONObject.parseArray(strArr,Map.class);
  System.out.println("利用JSONObject中的parseArray方法并指定返回类型来解析json数组字符串");
  for(Object mapList : listObjectSix){
       for (Object entry : ((Map)mapList).entrySet()){
            System.out.println(((Map.Entry)entry).getKey()  + "  " +
                               						((Map.Entry)entry).getValue());
       }
  }

 //第十一种方式
 List<Map<String,String>> listObjectFir = 
     						(List<Map<String,String>>) JSONArray.parse(strArr);
 System.out.println("利用JSONArray中的parse方法来解析json数组字符串");
 for(Map<String,String> mapList : listObjectFir){
      for (Map.Entry entry : mapList.entrySet()){
          System.out.println( entry.getKey()  + "  " +entry.getValue());
      }
 }
 //第十二种方式
  List<Map<String,String>> listObjectSec = JSONArray.parseObject(strArr,List.class);
  System.out.println("利用JSONArray中的parseObject方法并指定返回类型来解析json数组字符串");
  for(Map<String,String> mapList : listObjectSec){
       for (Map.Entry entry : mapList.entrySet()){
           System.out.println( entry.getKey()  + "  " +entry.getValue());
       }
  }
  //第十三种方式
  JSONArray listObjectThir = JSONArray.parseArray(strArr);
  System.out.println("利用JSONArray中的parseArray方法来解析json数组字符串");
  for(Object mapList : listObjectThir){
       for (Object entry : ((Map)mapList).entrySet()){
    		System.out.println(((Map.Entry)entry).getKey()+ ""+
                           					((Map.Entry)entry).getValue());
        }
  }
  //第十四种方式
  List listObjectFour = JSONArray.parseArray(strArr,Map.class);
  System.out.println("利用JSONArray中的parseArray方法并指定返回类型来解析json数组字符串");
  for(Object mapList : listObjectFour){
       for (Object entry : ((Map)mapList).entrySet()){
           System.out.println(((Map.Entry)entry).getKey()  + "  " +
                              				((Map.Entry)entry).getValue());
       }
  }

```

### 5.Map 转 Json对象

```java
    //map转json对象    
	Map<String,Object> map = new HashMap<>();
    map.put("column", "abc");
    map.put("length", "89");
    JSONObject json = new JSONObject(map);　　
    //json对象转Map
	Map<String,Object> map = (Map<String,Object>)jsonObject; 
```









































