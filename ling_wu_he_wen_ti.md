### 领悟

* [Fork\/Join   并把 The Java Tutorials研习下\(javaThead 看完后\)](https://docs.oracle.com/javase/tutorial/essential/concurrency/forkjoin.html)


### 问题

* 这看起来似乎时起作用的，因为Interger继承自Number,但是它无法工作，因为Inter Class 对象不是 Number Class 对象的子类\(这种差异看起来可能有些诡异，我们将在第15章中深入讨论它\) --&gt;第十四章

* 自动封包机制 在对未封包和封包的对象进行比较时,会相等吗(疑问处于 String "test" 和 new String("")).
  答案: 比较时Autoboxing and Unboxing 

```java
import net.mindview.util.CountingGenerator;

/**
 * Created by lh on 16-12-28.
 */
public class Test1 {
    public static void main(String[] args) {

        System.out.println(new Boolean(true) == true);
        System.out.println(new Byte((byte)1) == (byte)1);
        System.out.println(new Character((char) 1) == (char)1);
        System.out.println(new Float(1.1f) == 1.1f);
        System.out.println(new Integer(1) == 1);
        System.out.println(new Long(1L)==1L);
        System.out.println(new Short((short) 1) ==(short)1);
        System.out.println(new Double(1.11d) == 1.11d);
    }
}

```


* 容器的16 和0.75的理解

* 对已经编译过变为class的二进制文件class会检查该class里的以来关系吗(疑问来自Maven实战 传递性依赖一级直接依赖 test 二级直接依赖provide)   
**  <font color=#E9967A>答案: 检查已经编译过的class类里的依赖关系如果不存在需要的class文件报错</>**
![](/assets/Screenshot from 2016-12-28 10-29-54.png)
A项目对B项目是compile,B项目对C项目是provided那么最终的结果是A项目不对C项目进行依赖~
解答，A项目对B项目有依赖，说明B项目必须要在A项目的编译路径下，B项目对C项目是provided说明该依赖是由容器来提供的，在正式的发布包中B项目是不包含C项目的Jar包，因此A项目对B项目依赖后，会认为C项目是由容器提供，因此会忽略该依赖，默认认为容器中有，此时也不会报错，因为B项目已经编译打包了~


* java代码获取runtime时的classpath(疑问来自Maven实战 maven有3种不同的classpaht: 编译,测试,运行时) 

答案:

```java
import java.io.File;

/**
 * Created by lh on 16-12-28.
 */
public class Test {
    public static void main(String[] args) {
        //文件所在路径
        final File f = new File(Test.class.getProtectionDomain().getCodeSource().getLocation().getPath());
        System.out.println(f);

        System.out.println("blow runtime classPath");
        String classpath = System.getProperty("java.class.path");
        String[] classpathEntries = classpath.split(File.pathSeparator);
        for (String s :classpathEntries) {
            System.out.println(s);
        }
    }
}

```
  迎生问题: placeholder 工具类解析的/src/main/resources 里的propertis 属性文件,看其classpath包含/src/main/resources
  
  - 编译检查
    编译时检查没有指定LinkedList的泛型 赋值是对对象的赋值,相对与容器来说 应该不会对容器里面的属性做类型检查,所以可以成功
  ```java
   private LinkedList<Integer> eventList = new LinkedList(Arrays.asList("1","3"));
  ```


