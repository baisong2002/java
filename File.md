# File类
 - 称呼：输入、输出流
### 一、File类的使用
- 1、File类的一个对象，代表一个文件或者一个文目录（俗称文件夹）
**File类声明在java,io包下**
  - 如何创建File类的实例  
    - File（String filePath）
    - File(String parentPath ,String childPath)
    - File(File parentFile,String childPath)
- 2、**相对路径：相对于某个路径下，指明的路径**  
   **绝对路径：包含盘符在内的文件或文件目录的路径**
- 3、路径分隔符
**windows:\\**  
**unix:/**
```
例子：
//创建File类的实例
//构造器一
File a = new File("hello.txt");//相对于当前路径
File b = new File("D:\\java项目\\Lianxi\\src\\IO\\he.txt");//绝对路径
System.out.println(a);
System.out.println(b);
//构造器二
File c = new File("D:\\java项目","Lianxi");
System.out.println(c);
//构造器三
File d = new File(c,"hi.txt");
System.out.println(d);
```
### 二、File常用方法
```
1、File a = new File("hello.txt");
System.out.println(a.getAbsolutePath());//获取绝对路径
System.out.println(a.getPath());//获取路径
System.out.println(a.getName());//获取名称
System.out.println(a.getParent());//获取上层文件目录路径。若无，返回Null
System.out.println(a.length());//获取文件长度（即：字节数）。不能获取目录长度
System.out.println(a.lastModified());//获取最后一次修改时间，毫秒值
//适用于文件目录
File c = new File("D:\\java项目\\idea");
String[] list = c.list();//获取指定目录下下十五所有文件或者文件目录的名称数组
for (String s:list){
System.out.println(s);
}
System.out.println();
File[] files = c.listFiles();//获取指定目录下的所有文件或者文件目录的File数组
for (File f:files){
System.out.println(f);
}
```
- 2、File重命名
```
File file1 = new File("hello.txt");
File file2 = new File("D:\\IO\\hi.txt");
boolean a = file1.renameTo(file2);
System.out.println(a);
```
**注意：要想保证返回true,则需保证file1存在，file2不存在**  
- 3、File的判断功能：
```
File a = new File("hello.txt");
System.out.println(a.isDirectory());//是否是文件目录
System.out.println(a.isFile());//是否是文件
System.out.println(a.exists());//是否存在
System.out.println(a.canWrite());//是否可写
System.out.println(a.canRead());//是否可读
System.out.println(a.isHidden());//是否是隐藏
```
- 4、File类的创建功能/删除功能
```
File file = new File("hi.txt");
if (!file.exists()){
file.createNewFile();    //文件创建
System.out.println("创建成功！！");
}else {
file.delete(); //文件删除
System.out.println("删除成功！！！");
}
```
```
      File file = new File("D:\\IO\\io1");
        File file1 = new File(file.getParent(), "haha.txt");
        boolean a = file1.createNewFile();
        if (a) {
            System.out.println("创建成功");
        }
        File file2 = new File("D:\\IO\\io1\\io4");
        System.out.println(file2.delete());//删除文目录
    }
```
**要想删除成功，文件目录下不能有文件**
file类涉及到关于文件或文件目录的创建、删除、重命名、修改时间、文件大小等  
并未涉及到写入或读取文件内容的操作。如果需要读取或写入文件内容，必须使用IO流来完成  
后续File类的对象常会作为参数传递到流的构造器中，指明读取或写入的“终点”  
