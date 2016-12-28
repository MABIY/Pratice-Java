# 在String 中引用变量的另一种形式

2016年 05月 31日 星期二 11:18:03 CST
看到一种一直以为应该有的写法
```java
public class Test{
  public static void main(String[] args) {
    int userId =1;
    System.out.print("my test '"+userId+"'.");
  }
}
```
通过 “” 和‘’ 搭配使用， 感觉很cool  
以前的写法
```java
public class Test{
  public static void main(String[] args) {
    int userId =1;
    System.out.print("my test" + userId + ".");
  }
}
```



