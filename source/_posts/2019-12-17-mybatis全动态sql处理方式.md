---
title: mybatis全动态sql处理方式
comments: true
share: true
toc: true
categories:
  - mybatis
tags:
  - mybatis
date: 2019-12-17 19:45:45
---



# mybatis全动态sql处理方式

> 对于项目中需要用到全动态拼接sql的场景时，可以用到mybatis的statementType属性

![](https://raw.githubusercontent.com/adolphmaster/hexo-next/master/blogPicture/1811991-20190920142529656-1591028426.png)

Demo(如果是非预编译的话，最好使用${}而不是#{})：

```sql
<select id="query" resultType="Map" statementType="STATEMENT">  
        select * from ${tableName} t where  
        <foreach item="item" index="index" collection="field" open=" "  
            separator="and" close=" ">  
            <choose>  
                <when test="item.fieldType == 'DATE' and item.dateQueryFlag == 0">  
                    ${item.fieldCode} between  
                    to_date('${item.fieldValue}','yyyy-mm-dd  
                    hh24:mi:ss')   
                </when>  
                <when test="item.fieldType == 'DATE' and item.dateQueryFlag == 1">  
                    to_date('${item.fieldValue}','yyyy-mm-dd  
                    hh24:mi:ss')   
                </when>  
                <when test="item.fieldItemCode != null and item.fieldItemCode != ''">  
                    ${item.fieldCode} =  
                    '${item.fieldItemCode}'  
                </when>  
                <otherwise>  
                    ${item.fieldCode} =  
                    '${item.fieldValue}'  
                </otherwise>  
            </choose>  
        </foreach>  
  
</select> 
```

