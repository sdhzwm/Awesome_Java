
# Readme
  
本文包含tomcat和tomcat web的基础部署以及部分的Servlet的用法
- [Readme](#readme)
- [Tomcat](#tomcat)
  - [Tomcat是什么](#tomcat%e6%98%af%e4%bb%80%e4%b9%88)
  - [Tomcat与Java技术](#tomcat%e4%b8%8ejava%e6%8a%80%e6%9c%af)
  - [Tomcat基于Mac安装及部署](#tomcat%e5%9f%ba%e4%ba%8emac%e5%ae%89%e8%a3%85%e5%8f%8a%e9%83%a8%e7%bd%b2)
    - [下载](#%e4%b8%8b%e8%bd%bd)
    - [设置本地放置路径](#%e8%ae%be%e7%bd%ae%e6%9c%ac%e5%9c%b0%e6%94%be%e7%bd%ae%e8%b7%af%e5%be%84)
    - [启动Tomcat](#%e5%90%af%e5%8a%a8tomcat)
    - [关闭tomcat](#%e5%85%b3%e9%97%adtomcat)
    - [Tomcat的目录结构及作用](#tomcat%e7%9a%84%e7%9b%ae%e5%bd%95%e7%bb%93%e6%9e%84%e5%8f%8a%e4%bd%9c%e7%94%a8)
    - [注意事项：](#%e6%b3%a8%e6%84%8f%e4%ba%8b%e9%a1%b9)
    - [配置java web服务器](#%e9%85%8d%e7%bd%aejava-web%e6%9c%8d%e5%8a%a1%e5%99%a8)
- [Tomcat Web部署](#tomcat-web%e9%83%a8%e7%bd%b2)
  - [WEB应用部署目录结构](#web%e5%ba%94%e7%94%a8%e9%83%a8%e7%bd%b2%e7%9b%ae%e5%bd%95%e7%bb%93%e6%9e%84)
  - [Tomcat基本框架及相关配置](#tomcat%e5%9f%ba%e6%9c%ac%e6%a1%86%e6%9e%b6%e5%8f%8a%e7%9b%b8%e5%85%b3%e9%85%8d%e7%bd%ae)
    - [Server组件](#server%e7%bb%84%e4%bb%b6)
    - [Service组件](#service%e7%bb%84%e4%bb%b6)
    - [Connector组件](#connector%e7%bb%84%e4%bb%b6)
    - [Engine组件](#engine%e7%bb%84%e4%bb%b6)
    - [Host组件](#host%e7%bb%84%e4%bb%b6)
    - [Context组件](#context%e7%bb%84%e4%bb%b6)
    - [Realm组件](#realm%e7%bb%84%e4%bb%b6)
    - [Valve组件](#valve%e7%bb%84%e4%bb%b6)
    - [其他组件](#%e5%85%b6%e4%bb%96%e7%bb%84%e4%bb%b6)
- [Servlet](#servlet)
  - [什么是Servlet](#%e4%bb%80%e4%b9%88%e6%98%afservlet)
  - [Servlet工作模式](#servlet%e5%b7%a5%e4%bd%9c%e6%a8%a1%e5%bc%8f)
  - [Servlet的API概览](#servlet%e7%9a%84api%e6%a6%82%e8%a7%88)
  - [Servlet 的主要类型](#servlet-%e7%9a%84%e4%b8%bb%e8%a6%81%e7%b1%bb%e5%9e%8b)
  - [Servlet 的使用方法](#servlet-%e7%9a%84%e4%bd%bf%e7%94%a8%e6%96%b9%e6%b3%95)
  - [Servlet 的工作原理](#servlet-%e7%9a%84%e5%b7%a5%e4%bd%9c%e5%8e%9f%e7%90%86)
  


#  Tomcat
  
  
##  Tomcat是什么
  
Apache Tomcat是由Apache Software Foundation（ASF）开发的一个开源Java WEB应用服务器。
  
类似功能的还有：Jetty、Resin、Websphere、weblogic、JBoss、Glassfish、GonAS等，它们的市场占有率如下，可以看到Tomcat是最受欢迎的Java WEB应用服务器.Tomcat在技术实现上所处的位置如下：
  
![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20191023101318.png )
  
  
  
##  Tomcat与Java技术 
  
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
  
![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20191023101830.png )
  
##  Tomcat基于Mac安装及部署
  
  
###  下载
  
  
登录Apache Tomcat官网，地址 http://tomcat.apache.org ，点击左边的Download，选择需要下载的版本。
  
![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20191023102100.png )
  
###  设置本地放置路径
  
  
把下载下来的包解压到 /Users/你的用户名/目录下
  
###  启动Tomcat
  
  
打开终端
  
```
  
cd /Users/你的用户名/apache-tomcat-9.0.27/bin
  
打开终端输入 “cd”+”空格”，然后把bin文件夹拖到终端里，快速输入，点击回车
  
赋予超级管理员权限sudo chmod 755 *.sh
  
再次./startup.sh
  
打开我们的浏览器，然后网址输入 http://localhost:8080/，如果出现一只猫，则证明配置成功~
  
```
![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20191023103754.png )
  
###  关闭tomcat
  
  
同样是在bin 目录下，在终端输入：./shutdown.sh + 回车，就可以了。
  
  
###  Tomcat的目录结构及作用
  
  
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
  
  
###  注意事项：
  
如果服务器启动后信息提示Tomcat started，但是在浏览器中输入http://localhost:8080/后提示”无法连接至服务器“，则有可能是因为tomcat使用的jdk版本过低，不符合tomcat 9.0对jdk的最低要求，解决方法如下：
  
  
1. 去官网http://www.Oracle.com/technetwork/Java/javase/downloads/index-jsp-138363.html下载最新的jdk；
  
2. 在mac上根据提示安装jdk；
  
3. 在控制台输入命令：/usr/libexec/java_home得到目前mac中jdk的位置，如本人机器的jdk位置为：/Library/Java/JavaVirtualMachines/jdk1.8.0_73.jdk/Contents/Home
  
4. cd至~/ 目录下，执行vim .bash_profile，打开该文件；
  
5. 加入或者修改：export JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk1.8.0_73.jdk/Contents/Home"
  
6. 保存退出，在控制台输入 source .bash_profile
  
7. 重新启动tomcat，登陆浏览器输入网址后应该会产生正确的提示。
  
###  配置java web服务器
  
  
 如果你手里有一套java web源码，那么就把这个文件夹（假设文件夹名字叫做javaJar）放到tomcat9目录下的webapps目录下，在终端下执行
  
```
       sudo sh shutdown.sh 关闭服务器，然后再输入
  
       sudo sh startup.sh 打开服务器，表示服务器重启（会自动导入这个web）。
```
  
       （开启服务器的时候，dock上会有java的Bootstrap运行图标显示，当关闭服务器时，这个Bootstrap运行图标消失）
  
       打开浏览器，在浏览器输入“localhost:8080/javaJar”，回车，如果看到预期的网页，那么表示你的web部署成功。
  
  
  
  
#  Tomcat Web部署
  
  
##  WEB应用部署目录结构
  
  
我们的应用程序一般会打包成归档格式（.war），然后放到Tomcat的应用程序部署目录。而webapp有特定的组织格式，是一种层次型目录结构，通常包含了servlet代码文件、HTML/jsp页面文件、类文件、部署描述符文件等等，相关说明如下：
  
```
 /：web应用程序的根目录，可以存放HTML/JSP页面以及其他客户端浏览器必须可见的其他文件（如js/css/图像文件）。在较大的应用程序中，还可以选择将这些文件划分为子目录层次结构。
  
/WEB-INF：此webapp的所有私有资源目录，用户浏览器不可能访问到的，通常web.xml和context.xml均放置于此目录。
  
/WEB-INF/web.xml：此webapp的私有的部署描述符，描述组成应用程序的servlet和其他组件（如filter），以及相关初始化参数和容器管理的安全性约束。
  
/WEB-INF/classes：此webapp自有的Java程序类文件（.class）及相关资源存放目录。
  
/WEB-INF/lib：此目录存放webapp自有的JAR文件，其中包含应用程序所需的Java类文件（及相关资源），例如第三方类库或JDBC驱动程序。
  
  
```
  
##  Tomcat基本框架及相关配置
  
  
Tomcat可以按功能划分许多不同的组件，这些组件都可以通过`/conf/server.xml`文件中可定义和配置，包括`Server, Service, Connector, Engine, Cluster, Host, Alias, Context, Realm, Valve, Manager, Listener, Resources, ResourceEnvRef, WatchedResource, Store, Transaction, Channel, Membership, Transport, Member, ClusterListener等`，一般可分为以下四类：
  
- 1、顶级组件：位于配置层次的顶级，并且彼此间有着严格的对应关系，有Server组件、Service组件；
  
- 2、连接器：连接客户端（可以是浏览器或Web服务器）请求至Servlet容器，只有Connector组件，
  
- 3、容器：表示其功能是处理传入请求的组件，并创建相应的响应。如Engine处理对一个Service的所有请求，Host处理对特定虚拟主机的所有请求，并且Context处理对特定web应用的所有请求；
  
- 4、被嵌套的组件：位于一个容器当中，但不能包含其它组件；一些组件可以嵌套在任何Container中，而另一些只能嵌套在Context中。
  
  
![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20191023105406.png )
  
  
  
  
###  Server组件
  
  
Server（服务器）表示Tomcat的一个实例，因此，它必须是/conf / server.xml配置文件中的单个最外层元素，它的属性表示servlet容器的整体特性。通常一个JVM只能包含一个Tomcat实例。
  
默认配置表示监听在8005端口以接收shutdown命令，默认仅允许通过本机访问。
  
  
  
###  Service组件
  
  
Service（服务）主要用于关联一个Engine和与此Engine相关的Connector，每个Connector通过一个特定的端口和协议接收请求，并将其转发至关联的Engine进行处理。
  
因此，Service可以包含一个Engine、以有一个或多个Connector；而一个Server可以包含多个Service组件，但通常情下只为一个Server指派一个Service。通常需要给Service命名，可以方便管理员在日志文件中识别不同Service产生的日志。
  
如默认配置中server只包含一个名为"Catalina"的service，而service里包含两个Connector，其中一个监听8080端口接收HTTP请求，另一个监听8009端口接收AJP协议的请求。
  
  
  
###  Connector组件
  
  
如上面所述，Connector（连接器）通过一个特定的端口接收特定协议的客户端请求，并将其转发至关联的Engine进行处理。一个Engine可以配置多个连接器，但这些连接器必须使用不同的端口。
  
定义连接器可以使用多种属性，有些属性也只适用于某特定的连接器类型。一般说来，连接器类型可以分为两种：
  
（1）、HTTP连接器
  
HTTP连接器元素表示支持HTTP / 1.1协议的连接器组件，它能使Tomcat能够作为独立的Web服务器。此组件的特定实例侦听服务器上特定TCP端口号上的连接，每个转发到相关联的Engine以执行请求处理并创建响应。
  
HTTP连接器又有三种不同的实现：`Java Nio Connector、Java Nio2 Connector、APR/native Connector`，它们的对比如下：
  
![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20191023105658.png )
  
  
默认配置文件，定义了一个连接器为`protocol="HTTP/1.1` 表示的是使用自动切换机制来选择基于`Java NIOConnector`或基于`APR /Native Connector`（需要设置），也可以手动指定，
  
  
（2）、AJP 1.3连接器
  
AJP连接器元素表示通过AJP(Apache JServ Protocol)协议与Web连接器通信的连接器组件。
  
AJP协议是基于二进制的格式在Web服务器和Tomcat之间传输数据，这比HTTPP获得更好的效率，但比较复杂不通用。
  
通常用于将Tomcat集成到现有Apache服务器中，并且希望Apache处理Web应用程序中包含的静态内容或SSL连接处理的情况，即Apache服务器作为代理服务器。Apache与Tomcat结合可以由mod_jk或mod_proxy模块来实现，但它们的使用范围不同：mod_jk支持`apache/1.3,apache/2.0，mod_proxy支持apache/2.2+`。
  
默认配置文件中定义了一个监听8009端口的AJP连接器，其实官方文档说明这种连接器不久后不再支持，一般用得不多，就不再多介绍了。
  
定义连接器时可以配置的属性非常多，但通常定义HTTP连接器时必须定义的属性只有"port"，定义AJP连接器时必须定义的属性只有"protocol"，因为默认的协议为HTTP。以下为常用属性的说明（更多请参考前面给出的文档）：
  
  
1. address：指定连接器监听的地址，默认为所有地址，即0.0.0.0；
  
2. maxThreads：支持的最大并发连接数，默认为200；
3. port：监听的端口，默认为0；
  
4. protocol：连接器使用的协议，默认为HTTP/1.1，定义AJP协议时通常为AJP/1.3；
  
5. redirectPort：如果某连接器支持的协议是HTTP，当接收客户端发来的HTTPS请求时，则转发至此属性定义的端口；
  
6. connectionTimeout：等待客户端发送请求的超时时间，单位为毫秒，默认为60000，即1分钟；
  
7. enableLookups：是否通过request.getRemoteHost()进行DNS查询以获取客户端的主机名；默认为true；
  
8. acceptCount：设置等待队列的最大长度；通常在tomcat所有处理线程均处于繁忙状态时，新发来的请求将被放置于等待队列中；
  
###  Engine组件
  
  
Engine（引擎）表示与特定Service相关联的整个请求处理机制，即Servlet容器引擎。它接收和处理来自一个或多个连接器的所有请求，并检查每一个请求的HTTP首部信息以辨别此请求应该发往哪个Host或Context，并将完成的响应返回到连接器，以便最终传输回客户端。
  
一个Engine元素必须嵌套在Service元素内，它可以包含多个host组件，还可以包含Realm、Listener和Valve等子容器。
  
  
**常用的属性定义**
  
- 1、defaultHost：Tomcat支持基于FQDN的虚拟主机，这些虚拟主机可以通过在Engine容器中定义多个不同的Host组件来实现；但如果此引擎的连接器收到一个发往非非明确定义虚拟主机的请求时则需要将此请求发往一个默认的虚拟主机进行处理，因此，在Engine中定义的多个虚拟主机的主机名称中至少要有一个跟defaultHost定义的主机名称同名。
  
- 2、name：Engine组件的名称，用于日志和错误信息记录时区别不同的引擎。
- 3、 如默认配置中定义了一个名为"Catalina"的Engine，而Engine里包含一个Hots，并被配置为默认的虚拟主机。
  
  
  
###  Host组件
  
  
Host（虚拟主机）类似于Apache中的虚拟主机，但在Tomcat中只支持基于FQDN的"虚拟主机"。Host位于Engine容器中用于接收请求并进行相应处理，它是服务器（例如`www.mycompany.com`）的网络名称与运行Tomcat的特定服务器的关联。
  
客户端通常使用主机名来标识他们希望连接的服务器，但要使客户端能够使用其网络名称连接到Tomcat服务器，此名称必须在管理所属的Internet域的域名服务（DNS）服务器中注册。此主机名也包含在HTTP请求标头中，Tomcat从HTTP头中提取主机名，并查找具有匹配名称的主机；如果未找到匹配项，请求将路由到默认主机。
  
一个Engine至少要包含一个Host组件，而在Host元素内可以嵌入与此虚拟主机关联的Web应用程序的Context等元素。
  
  
**常用属性说明**
  
1. name：此Host的FQDN虚拟主机名称；
  
2. appBase：此Host的webapps目录，即存放非归档的web应用程序的目录或归档后的WAR文件的目录路径；可以使用基于<img src="https://latex.codecogs.com/gif.latex?CATALINA_HOME的相对路径；3.%20autoDeploy：在Tomcat处于运行状态时放置于appBase目录中的应用程序文件是否自动进行deploy；默认为true；4.%20unpackWars：在启用此webapps时是否对WAR格式的归档文件先进行展开；默认为true。如默认配置中定义了一个主机名为&quot;localhost&quot;的Host，而webapps目录为"/> CATALINA_BASE相对的"webapps"，即前面说到的默认目录，也可用绝对路径来配置其他目录。
  
  
###  Context组件
  
  
Context（上下文）表示在特定虚拟主机中运行的Web应用程序，一个Context对应一个Web应用程序，而里面的Wrapper可以理解为一个个Servlet程序。
  
Context需要根据其定义的上下文路径（path）匹配请求URI的最长前缀（除主机名外）来选择。一旦选择，可以由docBase来找到该上下文将对应的web应用程序部署目录，由目录中web.xml定义的servlet映射选择一个合适的servlet来处理传入的请求。
  
一个Host可以有多个Context，通常不建议定义在server.xml文件中，而是每一个context定义使用一个单独的XML文件进行，其文件的目录为`$CATALINA_HOME/conf/<engine name>/<host name>`。
  
可以看到server.xml中默认没有定义Context，但存在/conf/context.xml，在前面说Tomcat配置文件时曾介绍过，context.xml为部署与此Tomcat实例上所有的web应用程序提供的默认配置文件，删除注释后其内容如下：
  
通过它可以找到默认的和各web应用程序提供部署描述符文件web.xml，/conf/web.xml定义了Tomcat提供的默认Servlet处理程序，主要用来处理静态资源请求；而各webapp的web.xml可以定义其他的动态请求url映射到不同Servlet程序处理。
  
**常用的属性定义有**
  
- docBase：相应的Web应用程序的存放位置；也可以使用相对路径，起始路径为此Context所属Host中appBase定义的路径；切记，docBase的路径名不能与相应的Host中appBase中定义的路径名有包含关系，比如，如果appBase为deploy，而docBase绝不能为deploy-bbs类的名字；
  
- path：相对于Web服务器根路径而言的URI；如果为空""，则表示为此webapp的根路径；如果context定义在一个单独的xml文件中，此属性不需要定义；
  
- reloadable：是否允许重新加载此context相关的Web应用程序的类；默认为false；
  
  
  
###  Realm组件
  
  
Realm（领域）表示分配给这些用户的用户名，密码和角色（类似于Unix组）的"数据库"。一个Realm（领域）表示一个安全上下文，它是一个授权访问某个给定Context的用户列表和某用户所允许切换的角色相关定义的列表。
  
Catalina容器（Engine，Host或Context）可以包含不超过一个Realm元素（但自身可以嵌套）。此外，与引擎或主机关联的领域由低级容器自动继承，除非下级容器显式定义了自己的领域。如果没有为引擎配置领域，将自动为引擎配置空领域的实例。
  
定义Realm时惟一必须要提供的属性是classname，它是Realm的多个不同实现，用于表示此Realm认证的用户及角色等认证信息的存放位置，Tomcat中实现了多种不同的Realm，如下：
  
- UserDatabaseRealm：基于UserDatabase文件(通常是tomcat-user.xml)实现用户认证，它实现是一个完全可更新和持久有效的MemoryRealm，因此能够跟标准的MemoryRealm兼容；它通过JNDI实现；
  
- LockOutRealm：提供锁定功能，以便在给定时间段内出现过多的失败认证尝试时提供用户锁定机制；
  
- JAASRealm：基于Java Authintication and Authorization Service实现用户认证；
  
- JDBCRealm：通过JDBC访问某关系型数据库表实现用户认证；
  
- JNDIRealm：基于JNDI使用目录服务实现认证信息的获取；
  
- MemoryRealm：查找tomcat-user.xml文件实现用户信息的获取。
  
  
可以看到默认配置文件中定义了一个LockOutRealm并嵌套一个UserDatabaseRealm的Realm来通过tomcat-user.xml文件实现用户认证。
  
  
###  Valve组件
  
  
Valve（阀门）类似于过滤器，用来拦截请求并在将其转至目标之前进行某种处理操作；它可以工作于Engine和Host/Context之间、Host和Context之间以及Context和Web应用程序的某资源之间。
  
Valve常被用来记录客户端请求、客户端IP地址和服务器等信息，这种处理技术通常被称作请求转储(request dumping)。请求转储valve记录请求客户端请求数据包中的HTTP首部信息和cookie信息文件中，响应转储valve则记录响应数据包首部信息和cookie信息至文件中。
  
一个容器内可以建立多个Valve，而且Valve定义的次序也决定了它们生效的次序。不同类型的Value具有不同的处理能力，Tomcat中实现了多种不同的Valve：
  
- AccessLogValve：访问日志Valve
  
- ExtendedAccessValve：扩展功能的访问日志Valve
  
- RequestDumperValve：请求转储Valve；
- RemoteAddrValve：基于远程地址的访问控制；
  
- RemoteHostValve：基于远程主机名称的访问控制；
  
- SemaphoreValve：用于控制Tomcat主机上任何容器上的并发访问数量；
  
- ReplicationValve：专用于Tomcat集群架构中，可以在某个请求的session信息发生更改时触发session数据在各节点间进行复制；
  
- SingleSignOn：将两个或多个需要对用户进行认证webapp在认证用户时连接在一起，即一次认证即可访问所有连接在一起的webapp；
  
- ClusterSingleSingOn：对SingleSignOn的扩展，专用于Tomcat集群当中，需要结合ClusterSingleSignOnListener进行工作。
  
- 通过属性className定义相关的java实现的类名来选择Value。如默认配置文件中定义了一个AccessLogValve的Value来记录访问日志到文件中。
  
  
  
###   其他组件
  
  
**1、Logger**
  
日志记录器(Logger)：用于记录组件内部的状态信息，可被用于除Context之外的任何容器中。日志记录的功能可被继承，因此，一个引擎级别的Logger将会记录引擎内部所有组件相关的信息，除非某内部组件定义了自己的Logger组件（前面介绍的AccessLogValve使用自包含的逻辑来写它的日志文件，以获得更好的效率）。
  
**2、Listener**
  
Listener用于创建和配置LifecycleListener对象，而LifecycleListener通常被开发人员用来创建和删除容器。
  
**3、Loader**
  
Java的动态装载功能是其语言功能强大表现之一，Servlet容器使用此功能在运行时动态装载servlet和它们所依赖的类。Loader可以用于Context中控制java类的加载，即WebApp类加载器。
  
**4、Resources**
  
经常用于实现在Context中指定需要装载的但不在Tomcat本地磁盘上的应用资源，如Java类，HTML页面，JSP文件等。
  
**5、GlobalNamingResources**
  
应用于整个服务器的JNDI映射，此可以避免每个Web应用程序都需要在各自的web.xml创建，这在web应用程序以WAR的形式存在时尤为有用。它通常可以包含三个子元素：Environment、Resource和ResourceEnvRef。
  
**6、WatchedResource**
  
WatchedResource可以用于Context中监视指定的webapp程序文件的改变，并且能够在监视到文件内容发生改变时重新装载此文件。
  
**7、Manager**
  
  
Manger对象用于实现HTTP会话管理的功能，Tomcat中有5种Manger的实现：
  
- StandardManager,Tomcat6的默认会话管理器，用于非集群环境中对单个处于运行状态的Tomcat实例会话进行管理。当Tomcat关闭时，这些会话相关的数据会被写入磁盘上的一个名叫SESSION.ser的文件，并在Tomcat下次启动时读取此文件。
- PersistentManager,当一个会话长时间处于空闲状态时会被写入到swap会话对象，这对于内存资源比较吃紧的应用环境来说比较有用。
  
- DeltaManager,属于ClusterManager，用于Tomcat集群的会话管理器，它通过将改变了会话数据同步给集群中的其它节点实现会话复制。这种实现会将所有会话的改变同步给集群中的每一个节点，也是在集群环境中用得最多的一种实现方式。但集群节点较多时，会消耗大量的网络资源，一般适用于3、4个节点的集群。
  
- BackupManager,属于ClusterManager，用于Tomcat集群的会话管理器，与DeltaManager不同的是，某节点会话的改变只会同步给集群中的另一个而非所有节点。
  
- SimpleTcpReplicationManager,Tomcat4时用到的版本，过于老旧了。
  
**8、Stores**
  
PersistentManager必须包含一个Store元素以指定将会话数据存储至何处。这通常有两种实现方式：FileStore和JDBCStore。
  
**9、Cluster**
  
专用于配置Tomcat集群的元素，可用于Engine和Host容器中。在用于Engine容器中时，Engine中的所有Host均支持集群功能。在Cluster元素中，需要直接定义一个Manager元素，这个Manager元素有一个其值为org.apache.catalina.ha.session.DeltaManager或org.apache.catalina.ha.session.BackupManager的className属性。同时，Cluster中还需要分别定义一个Channel和ClusterListener元素。
  
**10、Channel**
  
用于Cluster中给集群中同一组中的节点定义通信"信道"。Channel中需要至少定义Membership、Receiver和Sender三个元素，此外还有一个可选元素Interceptor。
  
**11、Membership**
  
用于Channel中配置同一通信信道上节点集群组中的成员情况，即监控加入当前集群组中的节点并在各节点间传递心跳信息，而且可以在接收不到某成员的心跳信息时将其从集群节点中移除。Tomcat6中Membership的实现是org.apache.catalina.tribes.membership.McastService。
  
**12、Sender**
  
用于Channel中配置"复制信息"的发送器，实现发送需要同步给其它节点的数据至集群中的其它节点。发送器不需要属性的定义，但可以在其内部定义一个Transport元素。
  
**13、Transport**
  
用于Sender内部，配置数据如何发送至集群中的其它节点。Tomcat有两种Transport的实现：
  
- PooledMultiSender 基于Java阻塞式IO，可以将一次将多个信息并发发送至其它节点，但一次只能传送给一个节点。
  
- PooledParallelSener,基于Java非阻塞式IO，即NIO，可以一次发送多个信息至一个或多个节点。
  
**14、Receiver**
  
用于Channel定义某节点如何从其它节点的Sender接收复制数据，Tomcat中实现的接收方式有两种BioReceiver和NioReceiver。 
  
  
  
————————————————
  
本文为CSDN博主「尐譽」的原创文章：https://blog.csdn.net/tjiyu/article/details/54590258
  
  
#  Servlet
  
  
##  什么是Servlet
  
  
  
Servlet（Server Applet），全称Java Servlet，未有中文译文。是用Java编写的服务器端程序。其主要功能在于交互式地浏览和修改数据，生成动态Web内容。狭义的Servlet是指Java语言实现的一个接口，广义的Servlet是指任何实现了这个Servlet接口的类，一般情况下，人们将Servlet理解为后者。
  
Servlet运行于支持Java的应用服务器中。从实现上讲，Servlet可以响应任何类型的请求，但绝大多数情况下Servlet只用来扩展基于HTTP协议的Web服务器。
  
##  Servlet工作模式
  
  
- 客户端发送请求至服务器
- 服务器启动并调用Servlet，Servlet根据客户端请求生成响应内容并将其传给服务器
- 服务器将响应返回客户端
  
##  Servlet的API概览
  
  
Servlet API 包含以下4个Java包：
  
1. `javax.servlet`其中包含定义servlet和servlet容器之间契约的类和接口。
  
2. `javax.servlet.http`其中包含定义HTTP Servlet 和Servlet容器之间的关系。
  
3. `javax.servlet.annotation`其中包含标注servlet，Filter,Listener的标注。它还为被标注元件定义元数据。
  
4. `javax.servlet.descriptor`，其中包含提供程序化登录Web应用程序的配置信息的类型。
  
  
##  Servlet 的主要类型
  
  
![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20191025111742.png )
  
##  Servlet 的使用方法
  
  
Servlet技术的核心是Servlet，它是所有Servlet类必须直接或者间接实现的一个接口。在编写实现Servlet的Servlet类时，直接实现它。在扩展实现这个这个接口的类时，间接实现它。
  
##  Servlet 的工作原理
  
  
Servlet接口定义了Servlet与servlet容器之间的契约。这个契约是：Servlet容器将Servlet类载入内存，并产生Servlet实例和调用它具体的方法。但是要注意的是，在一个应用程序中，每种Servlet类型只能有一个实例。
  
  
  
用户请求致使Servlet容器调用Servlet的Service（）方法，并传入一个ServletRequest对象和一个ServletResponse对象。ServletRequest对象和ServletResponse对象都是由Servlet容器（例如TomCat）封装好的，并不需要程序员去实现，程序员可以直接使用这两个对象。
  
ServletRequest中封装了当前的Http请求，因此，开发人员不必解析和操作原始的Http数据。ServletResponse表示当前用户的Http响应，程序员只需直接操作ServletResponse对象就能把响应轻松的发回给用户。
  
对于每一个应用程序，Servlet容器还会创建一个ServletContext对象。这个对象中封装了上下文（应用程序）的环境详情。每个应用程序只有一个ServletContext。每个Servlet对象也都有一个封装Servlet配置的ServletConfig对象。
  
  
  