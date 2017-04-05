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



