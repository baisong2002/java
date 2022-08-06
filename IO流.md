# IO流
###一、IO流原理及流的分类
 - 作用：处理设备之间的输入输出，以“流”的方式，通过标准的方法输入输出
    - 输入：input读取外部数据，到程序中
    - 输出：output将程序输出到储存设备中 
 - 分类：
    - 按照操作数据单位不同：
      - 字节流（图片、视频等非文本）、字符流（文本文件） 
    - 按流的流向不同：
      - 输入流、输出流
 - 按角色不同：
    - 节点流（直接作用在程序上）、处理流（在已有流的基础上再包一层）
 - 抽象基础类：
  ```
  字节流          字符流
输入流：     InpuStream      Reader
输出流：     OutputStream    Writer 
  ``` 
  **其他子类都以上述四个抽象基础类为后缀**
 - 基本用法：
   - 1、创造文件
   - 2、创造流（根据自身需求选择流） 
   - 3、输出和输入操作
   - 4、关流
   - 5、使用try-cath-finally异常处理
### 二、File流（文件流）节点流
 - 1、FileReader(字符流)
```
         FileReader fr=null;
        try {
         /*
        将hello.txt文件内容读入程序，并控制输出到控制台
         */
            //实例化File类的对象，指明要操作的文件
            File file = new File("hello.txt");
            System.out.println(file.getPath());
            //提供具体的流
           fr = new FileReader(file);
            //数据的读入过程
            //read():返回一个字符，如果达到末尾，返回-1
            int date = fr.read();
            while (date != -1) {
                System.out.print((char) date);
                date = fr.read();
            }
        }catch (IOException e){
            e.printStackTrace();
        }finally {
            try{
                if (fr!=null)
                //4、流的关闭操作
                fr.close();
            }catch (IOException e){
                e.printStackTrace();
            }
        }
```
 >>**read()的理解：返回读入的一个字符。如果达到文件末尾，返回-1**   
 >>**异常的处理：为了保证流的资源一定可以执行关闭操作。需要使用try-catch-finally处理**    
 >>**读入的文件一定要存在否则就会报异常**    
```
//1、File类的实例化
File a = new File("hello.txt");
//2、FileRead流的实例化
FileReader b = null;
try {
b = new FileReader(a);
//3、读入操作
//read(read[] cbuf):返回每次读入cbuf数组中的字符的个数。如果达到文件末尾，返回-1
char[] c = new char[5];
int d;
while ((d = b.read(c)) != -1) {
//方式一：
for (int i = 0; i < d; i++) {
System.out.println(c[i]);
}

                String str=new String(c,0,d);
                System.out.print(str);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (b != null) {
                //4、资源的关闭
                try {
                    b.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```
- 2、FileWrite输入
  - 注意：
    - 1、输出对应的File可以不存在。并不会报异常
      - 如果不存在，在输出会自动创建
      - 如果存在:  
      如果流使用的构造器是：FileWrite(file,false)/FileWrite(file):对原有文件覆盖  
      如果流使用的构造器是：FileWrite(file,true)/FileWrite(file):不会对与哪有文件覆盖，而是在原有文件基础上追加内容  
```
           FileWriter b=null;
        try  {
            //1、提供File类的文件：指明写出到的文件
           File  a = new File("hello1.txt");
            //2、提供FileWriter的对象，用于数据写入
            b = new FileWriter(a, false);
            //3、写入操作
            b.write("I have a dream!\n");
            b.write("You need to have a dream!");

        }catch (IOException e){
            e.printStackTrace();
        }finally {
            //4、流资源的关闭
            if (b!=null) {

                try {
                    b.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```
- 3、文件复制
```
FileReader a1 = null;
FileWriter b1 =null;
try {
//1、创建File类对象，指明读入和写出文件
File a = new File("hello.txt");
File b = new File("hello2.txt");
//2、创建输入和输出流的对象
a1 = new FileReader(a);
b1 = new FileWriter(b);
//3、数据的读入和写出操作
char[]c =new char[5];
int len;
while ((len=a1.read(c))!=-1){
b1.write(c,0,len);
}
}catch (IOException e) {
e.printStackTrace();
}finally {
//4、关闭资源
try {
a1.close();
} catch (IOException e) {
e.printStackTrace();
}
try {
b1.close();
} catch (IOException e) {
e.printStackTrace();
}
}
```
   文本文件（.txt，.java等 ）使用字符流   
   非文本文件（.jpg,.mp3等），使用字节流处理   
   不能使用字符流来处理图片等数据，要想处理图片片要用字节流    
   不能使用字节流来处理字符等数据，否则会出现乱码    
- 4、FileInputeStream和FileOutputeStream
```
复制图片（输入、输出图片）
FileInputStream a1 = null;
FileOutputStream b1 = null;
try {
//创建文件
File a = new File("R-C.jfif");
File b = new File("R1.jfif");
//创建流
a1=new FileInputStream(a);
b1 = new FileOutputStream(b);
//复制
byte[]c=new byte[5];
int len;
while ((len=a1.read(c))!=-1){
b1.write(c,0,len);
}
} catch (IOException e) {
e.printStackTrace();
} finally {
//关流
if (a1!=null) {
try {
a1.close();
} catch (IOException e) {
e.printStackTrace();
}
}
if (b1!=null) {
try {
b1.close();
} catch (IOException e) {
e.printStackTrace();
}
}
}
```  
### 三、缓冲流（处理流的一种）
- （一）Buffered  
     BufferedInput  
     BuffrerdOutput  
     BufferedRead  
     BufferedWrite  
  >> 作用：提高流的读取和写入的速度  
  >> 提高读写速度的原因：内部提供了一个缓冲区  
 **flush():刷新缓冲区**
 **“套接”在已有的流之上**
```
1、非文本文件复制
//造文件
File file = new File("R-C.jfif");
File file1 = new File("R-C1.jfif");
//造流
FileInputStream fis = null;
FileOutputStream fis1 = null;
BufferedInputStream a = null;
BufferedOutputStream a1 = null;
try {
fis = new FileInputStream(file);
fis1 = new FileOutputStream(file1);
//造处理流（缓冲流）
a = new BufferedInputStream(fis);
a1 = new BufferedOutputStream(fis1);
//复制的细节：读取和写入的过程
byte[] b = new byte[5];
int len;
while ((len = a.read(b)) != -1) {
a1.write(b, 0, len);
}
} catch (IOException e) {
e.printStackTrace();
} finally {
if (a != null) {
//关流:要求：先关闭外层的流，再关内层
try {
a.close();
} catch (IOException e) {
e.printStackTrace();
}
//说明：关闭外层流的同时，内层流也进行关闭，内层流的关闭可以不用管
}
if (a1 != null) {
try {
a1.close();
} catch (IOException e) {
e.printStackTrace();
}
}
```
```
        BufferedReader a = null;
        BufferedWriter a1 = null;
        try {
            a = new BufferedReader(new FileReader(new File("hello.txt")));
            a1 = new BufferedWriter(new FileWriter(new File("hello3.txt")));
            /*方式一
            char[]b=new char[1024];
            int len;
            while ((len=a.read(b))!=-1){
                a1.write(b,0,len);
            }
             */
            //方式二
           String b;
           while ((b=a.readLine())!=null){
               //方法一;
               a1.write(b+"\n");//b不包含换行符
               //方法二
               a1.write(b);
               a1.newLine();//提供换行的服务
           }
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (a!=null) {
                a.close();
            }
            if (a1!=null) {
                a1.close();
            }
        }
```
### 四、转换流（处理流的一种）
- 字节流和字符流之间的转换  
>> InputStreamReader(字符流)：将一个字节的输入流转换为字符的输入流/解码  
>> OutputStreamWrite(字符流)：将一个字符的输出流转换为字节的输出流/编码  
**字符集：具体使用哪个字符集，取决于文件存储时使用的字符集**
```
FileInputStream a = new FileInputStream("hello.txt");
InputStreamReader a1 = new InputStreamReader(a);
char[]b=new char[20];
int len;
while ((len=a1.read(b))!=-1){
String s = new String(b, 0, len);
System.out.println(s);
}
a1.close();
```
```
FileInputStream b = new FileInputStream("hello.txt");
FileOutputStream b1 = new FileOutputStream("hello-gbk.txt");
InputStreamReader c = new InputStreamReader(b);
OutputStreamWriter c1 = new OutputStreamWriter(b1,"gbk");
char[]d=new char[10];
int len;
while ((len=c.read(d))!=-1){
c1.write(d,0,len);
}
c.close();
c1.close();
```
###五、其他流
- 输入输出流
 >>System.in:标准的输入流，从键盘输入
 >>System.out:标准的输出流,从控制台输出
**System类的setIn(InputStream is )/SetOut(OutputStream is)方式重新指定输入输出流**
```
InputStreamReader a = new InputStreamReader(System.in);
BufferedReader a1 = new BufferedReader(a);

            while (true) {
                System.out.println("请输入字符串：");
                String b = a1.readLine();
                if (b.equalsIgnoreCase("e") || b.equalsIgnoreCase("exit")) {
                    System.out.println("程序结束！！");
                    break;
                }
                String c = b.toUpperCase();
                System.out.println(c);
                a1.close();
        }
```
- 打印流：
>> PrintStream  PintWriter
>> 基本数据类型---->字符串 
- 数据流：
>> DateInputStream DateOutputStream
操作java语言的基本数据类型和String  
将数据持久化到文件中/将文件写出到内存中  
读取顺序要和写入顺序一致  
```
@Test
public void A() throws IOException {
DataOutputStream a = new DataOutputStream(new FileOutputStream("data.txt"));
a.writeUTF("薛浩然");
a.flush();
a.write(20);
a.flush();
a.close();
}
@Test
public void B() throws IOException {
DataInputStream a = new DataInputStream(new FileInputStream("data.txt"));
String b = a.readUTF();
int b1=a.read();
System.out.println(b+b1);
a.close();

    }
```
### 六、对象流
>>用于存储和读取基本数据类型或对象的处理流，可以把对象写入到数据源中  
**序列化：ObjectOutputStream类保存基本数据类型** 
**反序列化：ObjectInputStream类来读取**  
>>对象的序列化机制：允许把内存中的java对象转换为平台无关的二进制流，从而允许把这种二进制流持久保存在磁盘上
或通过网络将二进制流传输到另一个网络节点//（序列化）当其他程序获取这种二进制，就可以恢复成原来的java对象
```
@Test
public void A() throws IOException {
/*
对象流的使用
*/
//序列化：将内存中的java对象保存到磁盘中或通过网络传输出去
//使用：ObjectInputStream
ObjectOutputStream a = new ObjectOutputStream(new FileOutputStream("hello5.txt"));
a.writeObject(new String("沈晨晨"));
a.flush();
a.close();
}
@Test
public void B(){
/*
反序列化：将磁盘中的对象还原为内存中的对象
使用：ObjectInputStream
*/
ObjectInputStream b = null;
try {
b = new ObjectInputStream(new FileInputStream("hello5.txt"));
Object o = b.readObject();
String s=(String) o;
System.out.println(s);
} catch (IOException e) {
e.printStackTrace();
} catch (ClassNotFoundException e) {
e.printStackTrace();
} finally {
try {
b.close();
} catch (IOException e) {
e.printStackTrace();
}
}
```
- 自定义类的序列化和反序列化
  - 要想一个java对象可序列化，满足那些要求：
    - 1、实现接口：Serializable(标识接口)
     **serialVersionUI：用来表示类的不同版本之间的兼容性**
    - 2、当前类提供的全局常量：public static final long serialVersionUTD =47546353452L;
    - 3、除了当前类需要实现Serializable接口外，还要保证其内部所有属性也必须可序列化（默认情况下，基本数据类型可序列化）
**补充： 不能序列化：static/transient修饰的常量**
```
@Test
public void A() throws IOException {
/*
对象流的使用
*/
//序列化：将内存中的java对象保存到磁盘中或通过网络传输出去
//使用：ObjectInputStream
ObjectOutputStream a = new ObjectOutputStream(new FileOutputStream("hello5.txt"));
a.writeObject(new String("沈晨晨"));
a.flush();
a.writeObject(new Person("邓浩",20));
a.close();
}
@Test
public void B(){
/*
反序列化
使用：ObjectInputStream
*/
ObjectInputStream b = null;
try {
b = new ObjectInputStream(new FileInputStream("hello5.txt"));
Object o = b.readObject();
String s=(String) o;
Person o1 =(Person) b.readObject();
System.out.println(o1);

            System.out.println(s);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } finally {
            try {
                b.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
```
### 七、随机存储文件流   
>>直接继承object  即可输入又可输出    实现了DataInput DataOutput接口
- **mode参数：**  
r:只读文件  
rw：打开以便读取和写入  
rwd：打开以便读取和写入，同步更新文件的内容  
rws：打开以便读取和写入，同步更新文件内容和元数据内容  
>>如果RandomAccessFile作为输出流出时，写出到的文件如果不存在，则在执行过程中自动创建  
>>如果文件存在， 则会对原有文件内容进行覆盖。(默认从头覆盖)
```
@Test
public void A() {
RandomAccessFile a = null;
RandomAccessFile a1 = null;
try {
a = new RandomAccessFile(new File("hello.txt"), "r");
a1 = new RandomAccessFile(new File("hello1.txt"), "rw");
byte[] b = new byte[1024];
int len;
while ((len = a.read(b)) != -1) {
a1.write(b, 0, len);
}
} catch (IOException e) {
e.printStackTrace();
} finally {
if (a != null) {
try {
a.close();
} catch (IOException e) {
e.printStackTrace();
}
}
if (a1 != null) {
try {
a1.close();
} catch (IOException e) {
e.printStackTrace();
}
}
}
}
@Test
public void B() throws IOException {
RandomAccessFile a = new RandomAccessFile("hello.txt", "rw");
a.write("xyz".getBytes());
a.close();
}
}
/*
使用RandomAccessFile实现数据插入效果
*/
@Test
public void C() throws IOException {
RandomAccessFile a = new RandomAccessFile("hello1.txt", "rw");
a.seek(2);//将指针调到角标为2的位置
//保存指针2后面的所有数据到StringBuffder中
StringBuilder c = new StringBuilder((int) new File("hello1.txt").length());
byte[] b = new byte[20];
int len;
while ((len = a.read(b)) != -1) {
c.append(new String(b, 0, len));
}
//调回指针，写入数据
a.seek(2);
a.write("xyz".getBytes());
//将StringBuffer文件中的数据写入到文件中
a.write(c.toString().getBytes());
}
```
