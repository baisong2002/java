# Maven
>>- 是什么？
>>>>- 是一款服务与java平台的自动化构建工具
>>>>- 构建工具：Make-->Ant-->Maven-->Gradle
>>- 构建:
>>>>- (1)概念：以"java源文件" "框架配置文件" "JSP" "HTML" "图片"等资源为"原材料"，去"生产"一个可以运行项目的过程
>>>>- 编译、部署、搭建
>>>>>>- 编译：java源文件[User.java]-->编译-->Class字节码文件[User.class]-->交给JVM执行
>>>>>>- 部署：一个BS项目并不是动态web工程本身，而是这个动态web工程"编译的结果"
>>>>- 依赖：如果A工程里用到了B工程的类、接口、配置文件等资源，A依赖B
>>- maven的作用：
>>>>- 是专门用于管理和构建java项目的工具
>>- 功能：
>>>>- 提供了一套标准化的项目结构                        
>>>>>>- 所有的IDE使用maven构建的项目结构完全一样，所有IDE项目创建的maven项目可以通用
>>>>- 提供了一套标准化的构建流程(编译、测试、打包、发布...)
>>>>- 提供了一套依赖管理机制
## 一、使用maven：命令环境
>>- 1、根据坐标创建maven工程
>>>>- (1)maven坐标(资源的唯一标识)
>>>>>>- 作用:使用坐标来定义项目或引入项目所需要的依赖
>>>>- 向量：
>>>>>>- groupld:公司或组织的id(公司或组织域名的倒叙，通常也加上项目名称   
>>>>>>>>- 例子：com.atguigu,maven)                   
>>>>>>- artifactld:一个项目或项目中模块的id(模块的名称，将来作为maven工程的工程名)
>>>>>>- version:版本号(模块版本号，自己设定)
>>>>- 三个向量可以在maven仓库中唯一的定位到一个jar包
>>>>- (2)坐标和仓库中jar包的存储路径之间的对应关系
>>- maven命令：
>>>>- mvn是主命令(其他的是子命令)   archetype (插件): generate(目标)
>>- 生成maven工程: mvn archetype:generate   
>>- 项目和工程区别:
>>>>- 项目包含很多工程
>>- 2、POM
>>>>- 含义：项目对象模型
>>>>>>- mvn -v 命令和构建无关，而构建的相关命令要在pom.xml所在目录运行----操作那个工程就进入这个工程的pom.xml目录
>>>>- 清理操作：
>>>>>>- mvn clean  删除target目录
>>- 编译操作：
>>>>- 主编译：mvn compile
>>>>- 测试程序编译：mvn test-compile
>>>>- 主体程序编译结果存放目录：target/classes
>>>>- 测试程序编译结果存放的目录：target/test-classes
>>- 测试操作：
>>>>- mvn test
>>- 打包：
>>>>- mvn package
>>- 安装:
>>>>- mvn install