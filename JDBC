# JDBC
>> 是一个独立于特定数据库管理系统，通用的SQL数据库存取和操作的公共接口
## 一、获取数据库连接
>>- 1、Driver接口：
```
        url:http://localhost:8080/gmall/keyboard.jpg
        jdbc:mysql协议
        localhost:ip地址
        3306:端口号
        test:test数据库
```
>>>>- 1、提供三个连接的基本信息
```
    String url="jdbc:mysql://localhost:3306/sys";
    String user="root";
    String password="root";
```   
>>>>- 2、获取Driver实现类对象
```
    Class.forName("com.mysql.cj.jdbc.Driver");
```
>>>>- 3、获取连接
```
    Connection a = DriverManager.getConnection(url, user, password);
```
>>>>- 相较于方式三可以省略注册驱动
>>>>>>- 原因：在mysql的Driver实现类中，声明了静态方法，而静态方法随着类的加载而加载,第二步可以省略，连接MySQL数据库可以省略，其他数据库则不行
```
  @Test//(final)将数据库连接需要的4个基本信息声明在配置文件中，通过读取配置文件的方式获取连接
    public void A() throws Exception {
        //读取配置文件的基本信息
        InputStream i = test5.class.getClassLoader().getResourceAsStream("jdbc.properties");
        Properties p = new Properties();
        p.load(i);
        String user = p.getProperty("user");
        String password = p.getProperty("password");
        String url= p.getProperty("url");
        String driverClass = p.getProperty("driverClass");
        //2、加载驱动
        Class.forName(driverClass);
        //3、获取连接
        Connection c = DriverManager.getConnection(url, user, password);
        System.out.println(c);
    }
```
>>>>- 好处：实现了数据和代码的分离。实现了解耦
>>>>- 如果需要修改配置文件信息，可以避免程序重新打包
>>>>- ORM编程思想：
>>>>>>- 一个数据表对应一个java类
>>>>>>- 表中的一条记录对应java类的一个对象
>>>>>>- 表中的一个字段对应java类中的一个属性
>>- 数据库事务：
>>>>- 事务：一组逻辑操作单元(一行或多行DML操作(一个或多个数据库操作语句))，使数据从一种状态换到另一种状态(数据的变换)
>>- 事务处理(事务操作)的原则：
>>>>- 保证事务都要作为一个工作单元来执行，即使出现了故障，都不改变这种执行方式。当在一个事务中执行多个操作时，要么所有事务都被提交，要么这些
>>>>- 修改就永久的保存下来，要么数据库管理系统将放弃所作的所有修改，整个事务回滚
>>>>- 为确保数据库的一致性，数据的操作应当时离散的成组的逻辑单元：当它全部完成时，数据的一致性可以保持，而当这个单元中的一部分操作失败，整个事
>>>>- 务应全部视为错误，所有从起始点以后的操作全部退回到开始状态
>>>>- 数据一旦提交不可回滚
>>- 那些操作会导致数据的自动提交？
>>>>- DDL操作一旦执行，都会自动提交
>>>>- set autocommot=false对DDL失效
>>>>- DML默认情况下一旦执行，都会自动提交
>>>>- 可以通过set autocommot=false的方式取消DML操作的自动提交
>>>>- 默认关闭连接时，会将尚未提交的操作自动提交
>>- 事务的ACID属性及4种隔离级别
>>>>- ACID属性：
>>>>>>- 原子性：事务时一个不可分割的单位，事务要么不发生，要么都发生
>>>>>>- 一致性：事务必须使数据库从一个一致性状态换到另一个一致性状态
>>>>>>- 隔离性:一个事务的执行不能被其他事务干扰，即一个事务内部的操作及使用的数据对并发的其他事务是隔离的，并发执行的各个事务之间不能互相干扰
>>>>>>- 持久性：一个事务一旦被提交，它对数据库的改变时永久的，接下来的其他操作和数据库故障不应对其有任何影响
>>- 数据库并发问题：
>>>>- 对运行的多个事务，当这些事务访问数据库中相同的数据时，如果没有采取必要的隔离机制，就会导致并发问题：
>>>>>>- 脏读:对于两个事务A B，A读取了已经被B更新但还没有提交的字段，若B回滚，A读取的内容是临时且无效的
>>>>>>- 不可重复读:事务A B，A读取了一个字段。B更新(提交)了该字段，A再去读该字段，该字段值不一样了
>>>>>>- 幻读:事务A B，A从一个表中读取了一个字段，B在改表中插入了新的行，A再读该表，就会多几行
>>>>- 事务的隔离性:数据库系统必须具有隔离并发运行各个事务的能力，使它们不会互相影响，避免各种并发问题
>>>>- 事务间隔离的程度成为:隔离级别。隔离级别越高，数据一致性越好，并发性越弱
>>- 隔离的级别：
```
     READ UNCOMMITTED(读未提交)
        >都没解决
     READ COMMITED(读已提交)
        >脏读 解决
     REPEATABLE READ(可重复读)
        >脏读、不可重复读 解决
     SERIALIZABLE(串行化)               性能低下，一致性好
        >脏读、不可重复读、幻读 都解决
    Oracle支持2种事务隔离级别：READ COMMITED(读已提交/解决脏读)、SERIAZABLE(串行化);默认为READ COMMITED(读已提交/解决脏读)
    Mysql支持4中隔离级别;默认为:REPEATABLE READ(可重复读/脏读、不可重复读 解决)
```
>>- 查看隔离级别：
```
      SELECT @@tx_isolation;
    设置Mysql隔离级别:
       set transaction isolation level read committed;
     设置数据库的全局隔离级别
       set global transaction isolation level read committed;
```