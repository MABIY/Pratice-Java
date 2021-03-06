是变量的作用域的问题，因为匿名内部类是出现在一个方法的内部的，如果它要访问这个方法的参数或者方法中定义的变量，则这些参数和变量必须被修饰为final。因为虽然匿名内部类在方法的内部，但实际编译的时候，内部类编译成Outer.Inner,这说明内部类所处的位置和外部类中的方法处在同一个等级上，外部类中的方法中的变量或参数只是方法的局部变量，这些变量或参数的作用域只在这个方法内部有效。因为编译的时候内部类和方法在同一级别上，所以方法中的变量或参数只有为final，内部类才可以引用。

Java代码:  
package com.cxz.j2se;    
  
public class MyClass {    
    public MyClass\(\) {    
        final int finalValue = 10;    
        int not$Final = 20;    
        MyInterface myInterface = new MyInterface\(\) {    
            public void functionWithoutPara\(\) {    
                //compile Error    
                //System.out.println\(noFinal\);     
                System.out.println\(finalValue\);    
            }    
  
            public void functionWithPara\(int num\) {    
                System.out.println\("The parameter " + num    
                        + " has been passed by the method"\);    
            }    
  
        };    
        myInterface.functionWithoutPara\(\);    
        myInterface.functionWithPara\(not$Final\);    
        System.out.println\(myInterface.getClass\(\).getName\(\)\);    
    }    
  
    public static void main\(String\[\] args\) {    
        new MyClass\(\);    
  
    }    
  
} 

二、为什么局部内部类只能访问final变量  
简单的来说是作用域的问题。就好像方法外面做的事情并不能改变方法内才定义的变量，因为你并不知道方法里面这个时候已经存在了这个局部变量了没有。在这个内部类中方法里面的本地变量是失效的，也就是不在作用域内，所以是不能够访问的

但是为什么这里用final却又可以访问呢？  
因为Java采用了一种copy   local   variable的方式来实现，也就是说把定义为final的局部变量拷贝过来用，而引用的也可以拿过来用，只是不能重新赋值。从而造成了可以access   local   variable的假象，而这个时候由于不能重新赋值，所以一般不会造成不可预料的事情发生

三、如果定义一个局部内部类，并且局部内部类使用了一个在其外部定义的对象，为什么编译器会要求其参数引用是final呢？  
注意：局部内部类，包括匿名内部类。

原因如下：

abstract class ABSClass{  
public abstract void print\(\);  
}

public class Test2{  
public static void test\(final String s\){//一旦参数在匿名类内部使用,则必须是final  
ABSClass c=new ABSClass\(\){  
public void print\(\){  
System.out.println\(s\);  
}  
};  
c.print\(\);  
}  
public static void main\(String\[\] args\){  
test\("Hello World!"\);  
}  
}

JVM中每个进程都会有多个根,每个static变量,方法参数,局部变量,当然这都是指引用类型.基础类型是不能作为根的,根其实就是一个存储地址.垃圾回收器在工作时先从根开始遍历它引用的对象并标记它们,如此递归到最末梢,所有根都遍历后,没有被标记到的对象说明没有被引用,那么就是可以被回收的对象\(有些对象有finalized方法,虽然没有引用,但JVM中有一个专门的队列引用它们直到finalized方法被执行后才从该队列中移除成为真正没有引用的对象,可以回收,这个与本主题讨论的无关,包括代的划分等以后再说明\).这看起来很好.

但是在内部类的回调方法中,s既不可能是静态变量,也不是方法中的临时变量,也不是方法参数,它不可能作为根,在内部类中也没有变量引用它,它的根在内部类外部的那个方法中,如果这时外面变量s重指向其它对象,则回调方法中的这个对象s就失去了引用,可能被回收,而由于内部类回调方法大多数在其它线程中执行,可能还要在回收后还会继续访问它.这将是什么结果?

而使用final修饰符不仅会保持对象的引用不会改变,而且编译器还会持续维护这个对象在回调方法中的生命周期.所以这才是final变量和final参数的根本意义.  
文章出处：飞诺网\([www.firnow.com\):http://dev.firnow.com/course/3\_program/java/javajs/20100719/460085.html](http://www.firnow.com%29:http//dev.firnow.com/course/3_program/java/javajs/20100719/460085.html)

