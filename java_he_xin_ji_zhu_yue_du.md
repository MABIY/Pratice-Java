# java 核心技术阅读

###面向对象程序设计（Object-Oriented Programming,OOP）

###3.3.1 整型
  长整型数值有一个后缀L(如4000000000L). 十六进制数值有一个前缀0x(如OxCAFE).八进制有一个前缀0.例如，010对应八进制中的8.很显然，八进制表示法比较容易混淆，所以建议最好不要使用八进制常数。
   从Java7开始，加上前缀0b就可以写二进制数。例如，0b1001就是9.另外，同样是从java 7 开始，海可以未数字字面量加上下划线，如用1_000_000(或ob1111_0010_0100_0100_0000)表示一百万。这些下划线只是未了让人更易读。Java编译器会去除这些下划线。
   
   <h3 style="color:red">Double 表示这种类型的数值精度是float类型的两倍（有人称之为双精度数值）。</h3>
   <h3 style="color:red">精度表示什么。</h3>
   
   3.14 默认双精度，3.14F单精度。


所有浮点数计算都遵循IEEE754规范，下面是用于表示溢出情况的三种特殊的浮点数值：
* 正无穷大
* 负无穷大
* NaN（不是一个数字）
常量Double.POSITIVE_INFINITY、Double.NEGATIVE_INFINITY和Double.NaN(与相应的Float类型常亮一样)分别表示这三个特殊的值，但在实际引用中很少遇到。

特表说明的是，不能这样检测一个特定值是否等于Double.NaN:
if(x == Double.NaN) //is never true
所有“非数值”的值都认为是不相同的。然而，可以使用Double.isNaN方法:
if(Double.isNaN(x)) //check whether x is "not a number"

<h3 style="color:red">浮点数值不适合用于禁止出现舍入误差的金融计算中心。例如，命令System.out.println(2.0-1.1)将打印出0.899999999999，而不是人们想象的0.9。其主要原因是浮点数值采用二进制系统表示，而在二进制系统中无法精确的表示分数1/10.这就好像十进制无法精确的表示1/3一样。如果需要在数值计算中不含有任何舍入误差，就应该使用BigDecimal累。</h3>


<h3 style="color:red">其范围从\u0000到\Uffff</h3>。

###3.4.2 常量
  在Java中，利用关键字final 指示常量。例如：
  ```java
  public class Constants {
      public static void main(String[] args) {
        final double CM_PER_INCH = 2.54;
        double paperWidht = 8.5;
        double paperHeight =11;
        System.out.println("Paper size centimeters:" +paperWidth * CM_PER_INCH + "by"+paperHeight * CM_PER_INCH);
      }
  }
  ```
  关键字final表示这个变量只能被赋值一次。一旦被赋值之后，就不能够再更改了，习惯上，常量使用全大写。
  在Java 中，经常希望某个常量可以在一个类中的多个方法中使用，通常将这些常量称为类常量。可以使用关键字static final 设置类常量。下面使用类常量的示例：
```java
public class Constants2 {
    public static final double CM_PER_INCH =2.54;
    
    public static void main(String[] args) {
        double paperWidth =8.5;
        double paperHeight =11;
        System.out.println("Paper size in centimeters:"+paperWidth *
        CM_PER_INCH + "by" + paperHeight * CM_PER_INCH);
    }
}
```
###3.5 运算符
例如，15/2 等于7,15%2 等于1,15.0/2 等于7.5
可以在赋值语句中采用一种简化的格式书写二元算术运算符。
例如
x+= 4；
等价于
x = x +4;
通常，将运算符放在赋值号的左侧，如×=或%=。

###3.5.6强制类型转换
强制类型转换通过截断小数点部分将浮点值转换未整型。
```java
double x = 9.997;
int nx = (int) x;
System.out.print(nx)\\ 9

double x = 9.997;
int nx = (int)Math.round(x);
System.out.print(nx)\\ 10
```
如果试图将一个数值从一种类型强制转换为一种类型，而又超出了目标类型的表示范围，结果就会截断成一个完全不同的值。例如(byte)300 的实际值44.

右结合性
a +=b+=c
等价于
 a+=(b+=c)
 
```java
   String greeting = "Hello";
        if(greeting == "Hello"){
            System.out.println("mm");
        }

     if(greeting.substring(0,3 )== "Hel") {
                System.out.println("ttt");
            }

    }
``` 
    
 <h3 style="color:blue">String
 substring 等操作产生的结果并不是共享的。</h3>
