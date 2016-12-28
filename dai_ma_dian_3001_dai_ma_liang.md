# 代码点、代码量
码点(Unicode code point) 代码单元 (Unicode code units))  
 * char：java中，char类型为16位，原本用于表示一个字符。但是后来发现，16位已经不够表示所有的字符，所以后来发展出了用代码点表示字符的方法。
 * 
代码点：是指编码字符集中，字符所对应的数字。有效范围从U+0000到U+10FFFF。其中U+0000到U+FFFF为基本字符，U+10000到U+10FFFF为增补字符。
 * 
代码单元：为代码点进行编码得到的1或2个16位序列（UTF-16）。
 其中基本字符的代码点直接用一个相同值的代码单元表示，增补字符的代码点用两个代码单元进行编码,组成的格式是 编码值来自U+D800到U+DBFF、U+DC00~U+DFFF
 这个范围内没有数字用于表示字符，
 因此程序可以识别出当前字符是单元的基本字符，还是双单元的增补字符
```java
public class test {

    public static void main(String[] args) {
        String sentence = "\u03C0 \uD835\uDD6B \uD835\uDF61";
        int lengthU = sentence.length();
        int lengthP = sentence.codePointCount(0, lengthU);
        System.out.println(lengthU);        // 4个code units
        System.out.println(lengthP);        // 3个code points

        int i = sentence.codePointAt(5); //返回增补字符的int
        int ii = sentence.codePointAt(5); //返回DF61
        System.out.println("整部点"+i);
        //验证是够是增补字符
        boolean b = Character.isSupplementaryCodePoint(i);
        System.out.println(b);
    }
}
```