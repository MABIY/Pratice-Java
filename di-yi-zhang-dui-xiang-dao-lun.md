## 对象导论

### 1.6 继承

#### 问题:

1. final 修饰的 class 无法集成. 对象里的final 元素 在子类中可以引用到吗?  

```java
package 思考;

/**
 * Created by lh on 17-4-5.
 */
class Father {
    public static final String name = "a";
    public int age = 23;
    private String sex = "男"; // 子类中无法调用 private
}
public class ExtendsPractice extends Father{
    public static final String name ="2";
    public int age =21;
    public static void main(String[] args) {
        System.out.println(ExtendsPractice.name);
        System.out.println(Father.name);

        ExtendsPractice extendsPractice = new ExtendsPractice();
        System.out.println(extendsPractice.age);
    }
}
```

#### 领悟:

[CGI ](https://en.wikipedia.org/wiki/Common_Gateway_Interface):

```shel
In computing, Common Gateway Interface (CGI) offers a standard protocol for web servers to execute programs that execute like Console applications (also called Command-line interface programs) running on a server that generates web pages dynamically. Such programs are known as CGI scripts or simply as CGIs. 
The specifics of how the script is executed by the server are determined by the server. In the common case, a CGI script executes at the time a request is made and generates HTML.
```



