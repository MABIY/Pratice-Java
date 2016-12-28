```java
/**
* ReplaceIntegerToBinaryStringMethod toBinaryString
**/
public class ReplaceIntegerToBinaryStringMethod {
  //binaryInteger 代替 toBinaryString
  static void binaryInteger(int q) {
    if(q ==0) System.out.println(0);
    else {
      //numberOfLeadingZeros 显示 Integer 的补码 从最高位开始连续0的个数 不是0开头为0
      int nlz = Integer.numberOfLeadingZeros(q);
      q<<=nlz;
      for(int p =0;p<32 -nlz;p++){
        int n =(Integer.numberOfLeadingZeros(q) == 0)?1:0;
        System.out.print(n);
        q<<=1;
      }
        System.out.println();
    }

  }
  //binaryInteger() instead of Integer.toBinaryString()
  public static void main(String[] args) {
     //toBinaryString 显示Integer 的二进制补码
     System.out.println(Integer.toBinaryString(0x0));
     System.out.println(Integer.toBinaryString(-0x1f));
     System.out.println(Integer.toBinaryString(0x1f));
     binaryInteger(0x0);
     binaryInteger(-0x1f);
     binaryInteger(0x1f);
  }
}

```
