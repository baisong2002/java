# 核心类
## 一、字符串和编码
>> 1、String类代表字符串，是final类，代表不可变字符序列（不可变性）。
>> 2、String类实现类Serializable接口，表示字符串是支持序列化的。
>>>> 实现Compaable接口，表示String可以比较大小。
>>>> 我们通过字面量的方式给一个字符串赋值，此时的字符串值声明在字符串常量池中，
>> 3、字符串比较用 equals(),忽略大小写比较用equalsIgnoreCase，== 比较地址值。
>> 4、查看字符串是否包含字符："字符串".contains="字符"；
>> 5、erplace()修改指定字符或字符串
>> 6、String实例化：
>>>> （1）通过字面量定义的方式：
>>>> （2）通过new+构造器的方式。
```
     //通过字面量的方式，a的地址值，是常量池中
        String a="你好";
      //通过new+构造器的方式，b的地址值，是数据在堆空间中开辟空间以后对应的地址值。
        String b=new String("shi");
     //运用==来比较a和b的地址值是否相同。    
        System.out.println(a==b);
```
>> 7、String和char的转换
```
      （1）String转换为char                    
            String a="abcd";
    char[] charArray=a.toCharArray();
    for (int i=0;i<charArray.length;i++){
        System.out.println(charArray[i]);
    }  
     (2)cahr转换为String
        char[] a=new char[]{'a','b','c'};
        String b=new String(a);
        System.out.println(b);
```
>> 8、String和byte的转换
```
  （1）String转换为byte（编码）
     String a="nihao";
     byte[] b=a.getBytes();
     System.out.println(Arrays.toString(b));
```
>>>> （2）byte转换为String(解码)
>>>>>>- 编码：字符串--字节（看的懂转换为看不懂的二进制）    调用String的getBytes方法
>>>>>>- 解码：字节--字符串（看不懂二进制转换为看得懂）
>>>>>>- 说明：我们在解码时使用的字符集必须与编码时使用的字符集一致，否则会出现乱码
>> 9、拼接
>>>>- （1）常量与常量拼接实在常量池
>>>>- （2）常量与变量/变量与变量 拼接就是在堆
>>>>- （3）如果拼接的结构调用intern方法则返回值就在常量池中
>>>>>>- final修饰则是常量
## 二、StringBuilder(可变的String)、StringBuffer(String可变)
>>- 1、String、StringBuffer、StringBuilder的区别
```
String：不可变的字符序列
StringBuffer：可变的字符序列，线程安全。效率低（多线程选用）
StringBuilder:可变的字符序列，线程不安全。效率高
底层都使用char[]进行存储,会自动
StringBuffer append   :用于字符串链接
StringBuffer delete（int start,int end）  :删除指定位置的内容
StringBuffer replace(int start,int end,String str)  :把[start,end]内容更换为str
StringBuffer insert(int offset,xxx) :把指定位置插入xxx
StringBuffer reverser()  :把当前字符序列逆转
String 变量2=变量1.substring(int start,int end)  :返回一个从start开始到end结束的左闭右开的子字符串
```
## 三、StringJoiner
>> 可以将字符用符号隔开，并提供前后缀。
```
     StringJoiner a=new StringJoiner(",","[","]");       //创建一个StrinJoiner,用，将字符隔开,前缀是[,后缀是]。
          a.add("ni").add("hao");                       //在字符nihao中间添加，
          System.out.println(a);                        //输出a
    ***输出结果[ni,hao]***
StringJoiner提供了一个静态方法join可以不添加前后缀。
         String[] a = {"ni", "hao"};                //创建String类型数组
         var s = String.join(",", a);                //调用StringJoiner
         System.out.println(s);
    ***输出结果ni,hao***
```
>>- var定义变量：var 变量名=初始值；
>>>>- 注意：
>>>>>>- var只能在方法内定义局部变量，不能定义类的成员变量
>>>>>>- var定义变量必须赋初始值
>>>>>>- var只能一个变量，不能复合声明变量
>>>>>>- var可以不生命变量类型
## 四、包装类
>>- 基本数据类型：int、short、long、double、char、float、byte、boolean
>>- 引用数据类型：class、interface
```
基本数据类型       包装类型
byte               Byte              
short              Short 
long               Long 
float              Float 
double             Double 
int                Integer                 父类都是Number
--------------------------------------------------------
char               Character 
boolean            Boolean 
```                  
>>- 装箱：基本数据类型---->包装类
```
             int a=1;
            Integer b=new Integer(a);
            System.out.println(b.toString());
        ***输出结果：1***
```
>>- 拆箱：包装类--->基本数据类型（调用包装类的xxxValue（））
```
        Integer a=new Integer(10);
          int b=  a.intValue();
        System.out.println(b+1);
       ***输出结果：11***
```
>>- 包装类不可以进行加减，可以调用方法，也可以将包装类当做方法调用
>>- 基本数据类型可以进行加减，不可以当做方法调用
>>- 自动拆箱和自动封箱：
```
自动封箱： int a=1;                         自动拆箱：Integer a=1;
          Integer b=a;                               int b=a;
   System.out.println(b.toString());         System.out.println(a+1);
   ***输出结果：1 ***                       ***输出结果：2 ***
```
>>>>- 所有包装类型都是不可变类；
>>- 基本数据类型、包装类----->创建String类型
```
  1、连接运算：                       2、调用String的方法：valueof()
    int a=1;                                int a=1;
  String b=a+"";                          String b=String.valueOf(a);
 System.out.println(b);                   System.out.println(b);
                        ***输出结果：1 *** 
```
## 五、JAVABean
>>- 读方法：
```
public 数据类型 get变量名（）{return 变量名;}                public 数据类型 is变量名（）{return 变量名;}  
```
>>- 写方法：
```
public void  set变量名（形参）{this.变量名=形参;}
```
>>- 读和写方法称为属性，也是一种封装数据的方法
## 六、枚举类
>>- 前提条件：类的对象是有限个，确定的，数据类型必须一致
>>- 如果只有一个对象，称之为单例模式的实现方式
>>- 枚举类不可以继承其他类也不能被其他类继承，不能扩展，但可以实现接口
>>- 枚举类的对象修饰符：public static final...
>>- 定义枚举类：
>>>>- 方式一：
```
    public static void main(String[] args) {	
         Person p1=new Person("xaio","男");
         System.out.println(Person.Student2);
        System.out.println(p1);
    }
}
class Person{
    //声明对象的属性：private final修饰
    private final String name;
    private final String xb;
    //构造器，并给对象赋值                                       
    public Person(String name,String xb){                                如果私有化构造器则上面无法用new创建
     this.name=name;
     this.xb=xb;
    }
    //提供枚举类的多个对象：public static final修饰
    public static final Person Student=new Person("小米","女");
    public static final Person Student1=new Person("小红","女");
    public static final Person Student2=new Person("小刚","男");
   //获取枚举对象的属性，并提供赋值器
    public String getName() {
        return name;
    }
    public String getXb() {
        return xb;
    }
    //调用toString方法打印枚举属性
    @Override                                                                 如果不调用toString方法则打印出来是地址值
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", xb='" + xb + '\'' +
                '}';
    }
}
***输出结果：Person{name='小刚', xb='男'}***
            Person{name='xaio', xb='男'} 
```
>>>>- 方式二：
```
public static void main(String[] args) {
        Person student2 = Person.Student2;
        System.out.println(Person.Student2);
    }
}
enum Person{
    //提供枚举类的多个对象：public static final修饰可以省略
     Student("小米","女"),
     Student1("小红","女"),
     Student2("小刚","男");
    //声明对象的属性：private final修饰
    private final String name;
    private final String xb;
    //私有化构造器，并给对象赋值
    private Person(String name,String xb){                    此处必须私有化构造器，即enum类无法用new调用方法
     this.name=name;
     this.xb=xb;
    }
   //获取枚举对象的属性，并提供赋值器
    public String getName() {
        return name;
    }
    public String getXb() {
        return xb;
    }
    //调用toString方法打印枚举属性                                   如果没有调用toString方法则打印出对象名
    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", xb='" + xb + '\'' +
                '}';
    }
}
***输出结果：Person{name='小刚', xb='男'}***
```
>>- enum类继承java.lang.Enum，即enum类的父类是java.lang.Enum并不是object
>>- 常用方法：toString、values、valuesof(String name )
## 六、记录类
>>- 不变类：String、包装类
>>- 不变类特点：
>>>>- 1、定义class时使用final修饰，无法派生子类
>>>>- 2、每个字段使用final修饰，保证创建实例后无法修改任何字段
>>>>- 用record可以快速创建一个不可变类
```
record Person(int a,int b){}     
        | |
final class Person {
    private final int a;
    private final int b;

    Person(int a, int b) {
        this.a = a;
        this.b = b;
    }
    public int a() {
        return a;
    }
    public int b() {
        return b;
    }
    @Override
    public boolean equals(Object obj) {
        if (obj == this) return true;
        if (obj == null || obj.getClass() != this.getClass()) return false;
        var that = (Person) obj;
        return this.a == that.a &&
                this.b == that.b;
    }
    @Override
    public int hashCode() {
        return Objects.hash(a, b);
    }
    @Override
    public String toString() {
        return "Person[" +
                "a=" + a + ", " +
                "b=" + b + ']';
    }
}
```
>>- 我们仍可以在record中定义静态方法,经常是静态方法里的(of（）)
## 七、常用工具类
>>- 1、math类用于计算
>>- 2、random用于获取随机数