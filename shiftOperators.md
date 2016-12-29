结论: 根据数据类型返回左右移动无符号移动就是不更具符号位补齐移动处的空缺,有符号移动就是根据符号位填补空缺,最终移除数据类的位数就相当于循环移动了还是原来的二进制显示.
```java

pckage com.liuhua.practice;

/**
 * Created by lh on 16-12-29.
 */
public class ShiftOperators {
    public static void main(String[] args) {
        // ShiftOperator of  <<
        System.out.println(Integer.toBinaryString(5<<2));
        System.out.println(Integer.toBinaryString(5 << 29));
        System.out.println(5<<29);
        System.out.println(Integer.toBinaryString(5 << 30));
        System.out.println(5<<30);
        System.out.println(Integer.toBinaryString(5 << 31));
        System.out.println(5<<31);
        System.out.println(Integer.toBinaryString(5 << 32));
        System.out.println(5<<32);

        // ShiftOperator of  <<
        System.out.println(Integer.toBinaryString(5>>2));
        System.out.println(Integer.toBinaryString(5 >> 29));
        System.out.println(5>>29);
        System.out.println(Integer.toBinaryString(5 >> 30));
        System.out.println(5>>30);
        System.out.println(Integer.toBinaryString(5 >> 31));
        System.out.println(5>>31);
        System.out.println(Integer.toBinaryString(5 >> 32));
        System.out.println(5>>32);

        // ShiftOperator of  >>>
        System.out.println(Integer.toBinaryString(-5));
        System.out.println((5));
        System.out.println(Integer.toBinaryString(-5>>>3));
        System.out.println((-5 >>> 3));
        System.out.println(Integer.toBinaryString(-5>>>30));
        System.out.println(-5>>>30);
        System.out.println(Integer.toBinaryString(-5>>>31));
        System.out.println((-5>>31));
        System.out.println(Integer.toBinaryString(-5>>>32));
        System.out.println((-5>>32));

    }
}ackage com.liuhua.practice;

/**
 * Created by lh on 16-12-29.
 */
public class ShiftOperators {
    public static void main(String[] args) {
        System.out.println(Integer.toBinaryString(5<<2));
        System.out.println(Integer.toBinaryString(5 << 29));
        System.out.println(5<<29);
        System.out.println(Integer.toBinaryString(5 << 30));
        System.out.println(5<<30);
        System.out.println(Integer.toBinaryString(5 << 31));
        System.out.println(5<<31);
        System.out.println(Integer.toBinaryString(5 << 32));
        System.out.println(5<<32);
    }
}

```



