## Tomcat是什么
Apache Tomcat是由Apache Software Foundation（ASF）开发的一个开源Java WEB应用服务器。

类似功能的还有：Jetty、Resin、Websphere、weblogic、JBoss、Glassfish、GonAS等，它们的市场占有率如下，可以看到Tomcat是最受欢迎的Java WEB应用服务器.Tomcat在技术实现上所处的位置如下：

![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20191023101318.png)



## Tomcat与Java技术 
1. Tomcat与Java SE

Tomcat是用Java语言编写的，需要运行在Java虚拟机上，所以一般需要先安装JDK，以提供运行环境。

2. Tomcat与Java EE

Tomcat实现了几个Java EE规范，包括Java Servlet、Java Server Pages（JSP），Java Expression Language和Java WebSocket等，这些是都下载Tomcat安装包默认提供的，可以在源码中看到相关Java EE 规范API源码引用.

3. Tomcat与Servlet/编程开发

 Tomcat实现的几个Java EE规范最重的是Servlet，因为实现了Servlet规范，所以Tomcat也是一个Servlet容器，可以运行我们自己编写的Servlet应用程序处理动态请求。

平时用的Struts2、SpringMVC框架就是基于Servlet，所以我们可以在这些框架的基础上进行快速开发，然后部署到Tomcat中运行。

另外对于JSP规范实现：可以混合HTML与Java开发在一个文件中（.jsp），这种文件在第一次调用之后会被Tomcat的Jasper组件编译成一个servlet类，在后续的操作中则可以直接使用此类。这种开发方式不灵活，一般少用。

4. Tomcat与Web应用 

Tomcat的（HTTP类型）Connector组件实现了HTTP请求的解析，Tomcat通过Connector组件接收HTTP请求并解析，然后把解析后的信息交给Servlet处理：

对于静态资源（html/js/jpg等）请求，Tomcat提供默认的Servlet来处理并响应；

对于动态请求，可以映射到自己编写的Servlet应用程序来处理。

5. Tomcat与Nginx/Apache的应用架构

Nginx、Apache都是目前主流的Web服务器，也可以作为反向代理服务器；它们在处理大量并发的请求连接、连接会话管理和静态内容请求等方面相比Tomcat更具优势。

所以一般在实际应用中，先是通过Nginx（或Apache）反向代理服务器接收请求，匹配分离动态/静态请求（动静分离）;

如果是静态请求，则转发到另外的Nginx WEB服务器上，返回静态内容；如果是动态请求，则转发到后面的Tomcat应用服务器，处理动态请求的业务逻辑。

简单的架构如下：

![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20191023101830.png)

## Tomcat基于Mac安装及部署

### 下载

登录Apache Tomcat官网，地址 http://tomcat.apache.org ，点击左边的Download，选择需要下载的版本。

![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20191023102100.png)

### 设置本地放置路径

把下载下来的包解压到 /Users/你的用户名/目录下

### 启动Tomcat

打开终端

```

cd /Users/你的用户名/apache-tomcat-9.0.27/bin

打开终端输入 “cd”+”空格”，然后把bin文件夹拖到终端里，快速输入，点击回车

赋予超级管理员权限sudo chmod 755 *.sh

再次./startup.sh

打开我们的浏览器，然后网址输入 http://localhost:8080/，如果出现一只猫，则证明配置成功~

```
![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20191023103754.png)

### 关闭tomcat

同样是在bin 目录下，在终端输入：./shutdown.sh + 回车，就可以了。


### Tomcat的目录结构及作用

|- bin:存放tomcat的命令。

```java
    catalina.bat命令：

    startup.bat-> catalina.bat start

    shutdown.bat- > catalina.bat stop
```
|- conf:存放tomcat的配置信息。其中server.xml文件是核心的配置文件。

|-lib：支持tomcat软件运行的jar包。其中还有技术支持包，如servlet，jsp

|-logs：运行过程的日志信息

|-temp:临时目录

|-webapps：共享资源目录。web应用目录。（注意不能以单独的文件进行共享）

|-work：tomcat的运行目录。jsp运行时产生的临时文件就存放在这里

|- WebRoot :web应用的根目录

|-静态资源（html+css+js+image+vedio）

|-WEB-INF：固定写法。

|-classes：（可选）固定写法。存放class字节码文件

|-lib：（可选）固定写法。存放jar包文件。

|-web.xml

**注意：**

1）WEB-INF目录里面的资源不能通过浏览器直接访问

2）如果希望访问到WEB-INF里面的资源，就必须把资源配置到一个叫web.xml的文件中


### 注意事项：
如果服务器启动后信息提示Tomcat started，但是在浏览器中输入http://localhost:8080/后提示”无法连接至服务器“，则有可能是因为tomcat使用的jdk版本过低，不符合tomcat 9.0对jdk的最低要求，解决方法如下：


1. 去官网http://www.Oracle.com/technetwork/Java/javase/downloads/index-jsp-138363.html下载最新的jdk；

2. 在mac上根据提示安装jdk；

3. 在控制台输入命令：/usr/libexec/java_home得到目前mac中jdk的位置，如本人机器的jdk位置为：/Library/Java/JavaVirtualMachines/jdk1.8.0_73.jdk/Contents/Home

4. cd至~/ 目录下，执行vim .bash_profile，打开该文件；

5. 加入或者修改：export JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk1.8.0_73.jdk/Contents/Home"

6. 保存退出，在控制台输入 source .bash_profile

7. 重新启动tomcat，登陆浏览器输入网址后应该会产生正确的提示。

### 配置java web服务器

 如果你手里有一套java web源码，那么就把这个文件夹（假设文件夹名字叫做javaJar）放到tomcat9目录下的webapps目录下，在终端下执行

```
       sudo sh shutdown.sh 关闭服务器，然后再输入

       sudo sh startup.sh 打开服务器，表示服务器重启（会自动导入这个web）。
```

       （开启服务器的时候，dock上会有java的Bootstrap运行图标显示，当关闭服务器时，这个Bootstrap运行图标消失）

       打开浏览器，在浏览器输入“localhost:8080/javaJar”，回车，如果看到预期的网页，那么表示你的web部署成功。


