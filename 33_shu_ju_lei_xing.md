# 3.3 数据类型
java 是一种强类型的语言。这意味着必须为每个变量声明一种类型。在java 中，一共有8种基本类型（primitive type)，其中有4种整形、2种浮点类型、一种用于表示Unicode编码的字符单元的字符类型char和一种用于表示真值的boolean类型.

长整形数值有一个后缀L(如400000L).十六进制数值有一个前缀0x(如0xCAFE)。八进制有一个前缀0，例如，010对应八进制中的8.很显然，八进制表示法比较容易混乱，所以建议最好不要用8进制常量。
<div style="color:red">？？？什么是常量</div>
常量就是用 final 修饰的变量 只能初始化一次。


从Java7开始，加上前缀0b 就可以写二进制数。例如Ob1001就是9.另外，同样的是从java7开始，还可以为数字字面量加下划线，如用1_1000_000(或0b1111_1011_0000),这些下划线只是为了让人更易读。Java 编译器会去除这些下划线。

##浮点类型
float :7位有效的数值  (小数部分)  3.14F
double:16位的有效数值.   3.14D (3.14 默认double)
**0.124 在jdk 5.0 中可以使用 十六进制表示浮点数值。例如，0.125可以表示成0x1.0p-3。在十六进制表示法中，使用p表示指数，而不是e，注意，尾数采用十六进制，指数采用十进制。指数的基数是2，而不是10.****

**<div style="color:red">之后看浮点数进制如何在内存中表示的</div>**

所有浮点数值多遵循IEEE 754规范.下面表示溢出和出错情况的三个特殊的浮点数值
* 正无穷大
* 负无穷大
* NAN（非数值）
例如，一个正数除以0的结果为正无穷大。计算0/0或负数的平方根结果为NaN.
x == Double.Nan //is Never true

##3.3.3 char 类型
可以采用转义序列符\u表示Unicode代码单元的编码之外。还有一些用于表示特殊字符的转义序列符。所有这些转义序列都可以出现再字符常量或字符串的引号内。例如，'\u2122'或"Hello\n".转义序列符\u还可以出现在<div style="color:red">字符常量</div> --》字符常量是用单引号括起来的单个普通字符或转义字符，属于编程语言。
  
或字符串的引号之外(二其他所有转义序列不可以)。例如：

```java
  public class FirestSample {
  public static void main(String\u005B\u005D args){
    System.out.println("We will not use 'Hello,World!' \uD835\uDD6B ");
  }

}

```
[代码点 代码单元](https://en.wikipedia.org/wiki/UTF-16) :
U+D800 to U+DFFF 不代表任何字符，通过这个范围的16bit 组合成 16bit 表示不了的unicode 编码。
U+0000 to U+D7FF and U+E000 to U+FFFF 指定原有的一些编码。

##3.4变量
int i,j; //both are integers.

###变量初始化
声明一个变量之后如果属于方法的必须初始化，属于对象或类的默认初始化。

**在java 中，变量声明尽可能靠近变量第一次使用的地方，这是一种良好的程序编写风格。**

###3.4.2 常量
  在java 代码中利用final 指示常量 ，class 的static final  常量 是类的常量。
  const 是 Java 保留的关键字，但目前并没有使用。在java 中，必须使用final 定义常量。

##3.5 运算符
   在java 中，使用算术运算符+、-、×、/表示加、减、乘、除运算。当参加与/运算的两个操作数多是整数的时候，表示整数的除法；否则，表示浮点除法。整数的求余操作（有时称为取模）用%表示。例如，15/2 等于 7 ，15%2等于1,15.0/2 等于7.5。
   需要注意整数被0除将会产生一个异常，而浮点数被0除将会得到无穷大（-1.0/0负无穷、1.0/0正无穷）或NaN（0.0/0）结果。
   可以使用：
   x +=4;
 ##3.5.7括号于运算符级别
    += 是右结合运算符，所以表达式 
      a+=b+=c
    等价于
      a += (b+=c) 
  ##3.5.8
 ```java
      enum Size {SMALL,MEDIUYM,LARGE,EXTRA_LARGE}
      Size s = Size.MEDIUYM
 ```
 
 ```java
  //java 源码 "like".equal(new String("like")) Stirng.equal 比较的字符值
  public boolean equals(Object anObject) {
        if (this == anObject) {
            return true;
        }
        if (anObject instanceof String) {
            String anotherString = (String)anObject;
            int n = value.length;
            if (n == anotherString.value.length) {
                char v1[] = value;
                char v2[] = anotherString.value;
                int i = 0;
                //有意思的地方
                while (n-- != 0) {
                    if (v1[i] != v2[i])
                        return false;
                    i++;
                }
                return true;
            }
        }
        return false;
    }

 ```
 
 遍历Stirng = "\uD835\uDD6B is the set of integers" 代码点
 ```java
     public static void main(String[] args) {
       String greeting ="Hellof\uD835\uDD6B\uD835\uDD6B";
        System.out.println(greeting);
        System.out.println(greeting.length());
        System.out.println(greeting.codePointCount(0,greeting.length()));
        System.out.println(greeting.charAt(5));
        System.out.println(greeting.offsetByCodePoints(8,1));
        String test = "\uD835\uDD6B is the set of integers";
        for (int i = 0; i <test.length() ; ) {
            int cp = test.codePointAt(i);
            if (Character.isSupplementaryCodePoint(cp)) {  //判断是否是辅助代码单元是
                System.out.print(test.substring(i,i+2));
                i +=2;
            } else {
                System.out.print(test.charAt(i));
                i++;
            }
        }

    }
 ```
   
   

