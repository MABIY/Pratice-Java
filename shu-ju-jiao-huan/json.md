### [json](http://www.json.org/json-zh.html)

\(JavaScript Object Notation\) 是一种轻量级的数据交换格式。 易于人阅读和编写。同时也易于机器解析和生成。 它基于JavaScript Programming Language, Standard ECMA-262 3rd Edition - December 1999的一个子集。 JSON采用完全独立于语言的文本格式，但是也使用了类似于C语言家族的习惯（包括C, C++, C\#, Java, JavaScript, Perl, Python等）。 这些特性使JSON成为理想的数据交换语言。

```java
        //json-lib-2.4-jdk15.jar
        Map classMap = new HashMap();
        classMap.put("messages",EmailVo.class);
        EmailMessagePojo dataVO  = (EmailMessagePojo)JSONObject.toBean(JSONObject.fromObject(result), EmailMessagePojo.class, classMap);
        List<EmailVo> folderMessage =dataVO.getData().getMessages();
```



