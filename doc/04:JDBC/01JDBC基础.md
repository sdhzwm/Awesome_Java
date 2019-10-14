### 1. 什么是JDBC

#### 1.1 定义

JDBC规范定义接口，具体的实现由各大数据库厂商来实现。

JDBC是Java访问数据库的标准规范，真正怎么操作数据库还需要具体的实现类，也就是数据库驱动。每个 数据库厂商根据自家数据库的通信格式编写好自己数据库的驱动。所以我们只需要会调用JDBC接口中的方法即可，数据库驱动由数据库厂商提供。

#### 1.2 好处

![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20191009154533.png)

- 程序员如果要开发访问数据库的程序，只需要会调用 JDBC 接口中的方法即可，不用关注类是如何实现的
- 使用同一套 Java 代码，进行少量的修改就可以访问其他 JDBC 支持的数据库



#### 1.3  JDBC开发使用到的包

 
| 会使用的包 | 说明|
| ---- | ---- | 
| java.sql | 所有与JDBC访问数据库相关的接口和类 | 
| javax.sql | 数据库拓展包，提供数据库额外的功能，如连接池 | 
| 数据库的驱动| 由各大数据库厂商提供，需要额外去下载，是对 JDBC 接口实现的类 | 

### 2  JDBC核心API

| 接口或类 | 作用|
| ---- | ---- | 
| DriverManager 类 | 1) 管理和注册数据库驱动 2) 得到数据库连接对象 | 
| Connection 接口 | 一个连接对象，可用于创建 Statement 和 PreparedStatement 对象 | 
| Statement 接口| 一个 SQL 语句对象，用于将 SQL 语句发送给数据库服务器 | 
| PreparedStatemen 接口| 一个 SQL 语句对象，是 Statement 的子接口 | 
| ResultSet 接口| 用于封装数据库查询的结果集，返回给客户端 Java 程序 | 

### 3 JDBC使用

1. 导入驱动jar包 mysql-connector-java-5.1.37-bin.jar
	1.复制mysql-connector-java-5.1.37-bin.jar到项目的libs目录下
	2.右键-->Add As Library
2. 注册驱动
3. 获取数据库连接对象 Connection
4. 定义sql
5. 获取执行sql语句的对象 Statement
6. 执行sql，接受返回结果
7. 处理结果
8. 释放资源

**代码实现**

```java
	//1. 导入驱动jar包
    //2.注册驱动: 从JDBC3开始，目前已经普遍使用的版本。可以不用注册驱动而直接使用。Class.forName 这句话可以省略
    Class.forName("com.mysql.jdbc.Driver");
    //3.获取数据库连接对象
    Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/db3", "root", "root");
    //4.定义sql语句
    String sql = "update account set balance = 500 where id = 1";
    //5.获取执行sql的对象 Statement
    Statement stmt = conn.createStatement();
    //6.执行sql
    int count = stmt.executeUpdate(sql);
    //7.处理结果
    System.out.println(count);
    //8.释放资源
    stmt.close();
    conn.close();

```

### 4 JDBC使用详解

#### 4.1 DriverManager

DriverManager主要作用：管理和注册驱动，创建数据库的连接

DriverManager的类中的方法

| DriverManager类中的静态方法 | 描述|
| ---- | ---- | 
| Connection getConnection (String url, String user, String password) | 通过连接字符串，用户名，密码来得到数据 库的连接对象| 
| Connection getConnection (String url, Properties info) | 通过连接字符串，属性对象来得到连接对象 | 

DriverManager使用JDBC连接数据库的四个参数

| 连接数据库的四个参数 | 描述|
| ---- | ---- | 
| 用户名 | 登录的用户名| 
| 密码 | 登录的密码 | 
| 连接字符串 URL | 不同的数据库 URL 是不同的，mysql 的写法jdbc:mysql://localhost:3306/数据库[?参数名=参数值]| 
| 驱动类的字符串名 | com.mysql.jdbc.Driver | 

**连接数据库的 URL 地址格式**

```java
协议名:子协议://服务器名或 IP 地址:端口号/数据库名?参数=参数值

```

如果数据库出现乱码，可以指定参数: ?characterEncoding=utf8，表示让数据库以 UTF-8 编码来处理数据。

```java
jdbc:mysql://localhost:3306/数据库?characterEncoding=utf8
```
