１．序列化是为了生成i\/o流用于在设备中传输以此来存储等等。

 序列化的什么特点： 如果某个类能够被序列化，其子类也可以被序列化。

声明为static和transient类型的成员数据不能被序列化。

因为static代表类的状态， transient代表对象的临时数据。 

什么时候使用序列化： 一：对象序列化可以实现分布式对象。主要应用例如：RMI要利用对象序列化运行远程主机上的服务，就像在本地机上运行对象时一样。 

二：java对象序列化不仅保留一个对象的数据，而且递归保存对象引用的每个对象的数据。可以将整个对象层次写入字节流中，可以保存在文件中或在网络连接上传递。利用对象序列化可以进行对象的"深复制"，即复制对象本身及引用的对象本身。序列化一个对象可能得到整个对象序列。 
```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Student {
    int id;
    String num;
}
@Data
class NanStudent extends Student implements Serializable{
    String name;
    String age;

    public NanStudent(String name, String age) {
        super(1, "世界");
        this.name = name;
        this.age = age;
    }
    private void writeObject(java.io.ObjectOutputStream out) throws IOException {
        out.defaultWriteObject();//先序列化对象
       out.writeInt(id);//再序列化父类的域
        out.writeObject(num);
    }

    private void readObject(java.io.ObjectInputStream in) throws IOException, ClassNotFoundException {
       in.defaultReadObject();//先反序列化对象
        id=in.readInt();//再反序列化父类的域
        num = (String) in.readObject();
  }

}

class Persist {
    public static void main(String[] args) throws IOException {
        Student student = new NanStudent("刘华","2");
        FileOutputStream fout = new FileOutputStream("f.txt");
        ObjectOutputStream out = new ObjectOutputStream(fout);
        out.writeObject(student);
        out.flush();
        out.close();
        System.out.println("success");

    }
}

class Depersist {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        ObjectInputStream in = new ObjectInputStream(new FileInputStream("f.txt"));
        Student s = (Student) in.readObject();
        System.out.println(s.toString());
        in.close();
    }
}
```

