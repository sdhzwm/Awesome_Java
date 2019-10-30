---
toc: 'depth_from:2 depth_to:4 ordered:false'
ebook:
    theme: github-light.css
    title: tomcat
    author: wm
    epub: {no-default-epub-cover: true}
---  
  
- [Tomcat](#tomcat )
  - [Tomcat是什么](#tomcat是什么 )
  - [Tomcat与Java技术](#tomcat与java技术 )
  - [Tomcat基于Mac安装及部署](#tomcat基于mac安装及部署 )
    - [下载](#下载 )
    - [设置本地放置路径](#设置本地放置路径 )
    - [启动Tomcat](#启动tomcat )
    - [关闭tomcat](#关闭tomcat )
    - [Tomcat的目录结构及作用](#tomcat的目录结构及作用 )
    - [注意事项：](#注意事项 )
    - [配置java web服务器](#配置java-web服务器 )
- [Tomcat Web部署](#tomcat-web部署 )
  - [WEB应用部署目录结构](#web应用部署目录结构 )
  - [Tomcat基本框架及相关配置](#tomcat基本框架及相关配置 )
    - [Server组件](#server组件 )
    - [Service组件](#service组件 )
    - [Connector组件](#connector组件 )
    - [Engine组件](#engine组件 )
    - [Host组件](#host组件 )
    - [Context组件](#context组件 )
    - [Realm组件](#realm组件 )
    - [Valve组件](#valve组件 )
    - [其他组件](#其他组件 )
- [Servlet](#servlet )
  - [什么是Servlet](#什么是servlet )
  - [Servlet工作模式](#servlet工作模式 )
  - [Servlet的API概览](#servlet的api概览 )
  - [Servlet 的主要类型](#servlet-的主要类型 )
  - [Servlet 的使用方法](#servlet-的使用方法 )
  - [Servlet 的工作原理](#servlet-的工作原理 )
  - [Servlet的体系结构](#servlet的体系结构 )
  - [Servlet相关配置](#servlet相关配置 )
- [HTTP 和 HTTPS](#http-和-https )
  - [HTTP](#http )
    - [什么是HTTP?](#什么是http )
    - [什么是HTTPS？](#什么是https )
  - [HTTP VS HTTPS](#http-vs-https )
    - [HTTP特点](#http特点 )
    - [HTTPS特点](#https特点 )
  - [HTTP通信传输](#http通信传输 )
  - [HTTPS实现原理](#https实现原理 )
    - [SSL建立连接过程](#ssl建立连接过程 )
  - [运用与总结](#运用与总结 )
    - [安全性考虑](#安全性考虑 )
    - [成本考虑](#成本考虑 )
- [Request](#request )
  - [什么是request](#什么是request )
  - [request域方法](#request域方法 )
  - [request获取请求头数据](#request获取请求头数据 )
  - [request获取请求相关的其它方法](#request获取请求相关的其它方法 )
  - [request获取请求参数](#request获取请求参数 )
    - [GET请求和POST请求的区别](#get请求和post请求的区别 )
    - [请求转发和请求包含](#请求转发和请求包含 )
    - [请求转发与请求包含比较](#请求转发与请求包含比较 )
    - [请求转发与重定向比较](#请求转发与重定向比较 )
- [response](#response )
  - [什么是response？](#什么是response )
  - [response响应正文](#response响应正文 )
    - [字符响应流](#字符响应流 )
      - [字符编码](#字符编码 )
      - [缓冲区](#缓冲区 )
  - [设置响应头信息](#设置响应头信息 )
  - [设置状态码及其他方法](#设置状态码及其他方法 )
  - [5、重定向](#5-重定向 )
    - [什么是重定向（两次请求）](#什么是重定向两次请求 )
    - [如何完成重定向？](#如何完成重定向 )
- [案例](#案例 )
  - [用户登录案例需求](#用户登录案例需求 )
  - [开发步骤](#开发步骤 )
  
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
  
  
  
##  Servlet的体系结构	
  
  
Servlet -- 接口
			|
GenericServlet -- 抽象类
  
将Servlet接口中其他的方法做了默认空实现，只将service()方法作为抽象
  
* 将来定义Servlet类时，可以继承GenericServlet，实现service()方法即可
  
  
HttpServlet  -- 抽象类 对http协议的一种封装，简化操作
  
1. 定义类继承HttpServlet
2. 复写doGet/doPost方法
  
##  Servlet相关配置
  
  
1. urlpartten:Servlet访问路径
2. 一个Servlet可以定义多个访问路径 ： @WebServlet({"/d4","/dd4","/ddd4"})
3. 路径定义规则：
	1. /xxx：路径匹配
	2. /xxx/xxx:多层路径，目录结构
	3. *.do：扩展名匹配
  
---
#  HTTP 和 HTTPS
  
  
##  HTTP
  
  
###  什么是HTTP?
  
  
> 超文本传输协议，是一个基于请求与响应，无状态的，应用层的协议，常基于TCP/IP协议传输数据，互联网上应用最为广泛的一种网络协议,所有的WWW文件都必须遵守这个标准。设计HTTP的初衷是为了提供一种发布和接收HTML页面的方法。
  
![发展历史](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/WX20191029-102756@2x.png )
  
使用HTTP/1.1和HTTP/2同时请求379张图片，观察请求的时间，明显看出HTTP/2性能占优势。
  
![对比](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/WX20191029-102930@2x.png )
  
**多路复用：** 通过单一的HTTP/2连接请求发起多重的请求-响应消息，多个请求stream共享一个TCP连接，实现多留并行而不是依赖建立多个TCP连接。
  
![报文格式](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/WX20191029-103238@2x.png )
  
  
###  什么是HTTPS？
  
  
> 《图解HTTP》这本书中曾提过HTTPS是身披SSL外壳的HTTP。HTTPS是一种通过计算机网络进行安全通信的传输协议，经由HTTP进行通信，利用SSL/TLS建立全信道，加密数据包。HTTPS使用的主要目的是提供对网站服务器的身份认证，同时保护交换数据的隐私与完整性。
> PS:TLS是传输层加密协议，前身是SSL协议，由网景公司1995年发布，有时候两者不区分。
  
  
  
##  HTTP VS HTTPS
  
  
###  HTTP特点
  
  
- 无状态：协议对客户端没有状态存储，对事物处理没有“记忆”能力，比如访问一个网站需要反复进行登录操作
- 无连接：HTTP/1.1之前，由于无状态特点，每次请求需要通过TCP三次握手四次挥手，和服务器重新建立连接。比如某个客户机在短时间多次请求同一个资源，服务器并不能区别是否已经响应过用户的请求，所以每次需要重新响应请求，需要耗费不必要的时间和流量。
- 基于请求和响应：基本的特性，由客户端发起请求，服务端响应
- 简单快速、灵活
- 通信使用明文、请求和响应不会对通信方进行确认、无法保护数据的完整性
  
下面通过一个简单的抓包实验观察使用HTTP请求传输的数据：
  
![抓包实验](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/WX20191029-103707@2x.png )
  
![12306结果](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/WX20191029-103913@2x.png )
  
**结果分析： HTTP协议传输数据以明文形式显示**
  
针对无状态的一些解决策略：
  
场景：逛电商商场用户需要使用的时间比较长，需要对用户一段时间的HTTP通信状态进行保存，比如执行一次登陆操作，在30分钟内所有的请求都不需要再次登陆。
- 通过Cookie/Session技术
- HTTP/1.1持久连接（HTTP keep-alive）方法，只要任意一端没有明确提出断开连接，则保持TCP连接状态，在请求首部字段中的Connection: keep-alive即为表明使用了持久连接
  
###  HTTPS特点
  
  
基于HTTP协议，通过SSL或TLS提供加密处理数据、验证对方身份以及数据完整性保护
  
![https的特点](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/WX20191029-104403@2x.png )
  
  
通过抓包可以看到数据不是明文传输，而且HTTPS有如下特点：
  
- 内容加密：采用混合加密技术，中间者无法直接查看明文内容
- 验证身份：通过证书认证客户端访问的是自己的服务器
- 保护数据完整性：防止传输的内容被中间人冒充或者篡改
  
> **混合加密:** 结合非对称加密和对称加密技术。客户端使用对称加密生成密钥对传输数据进行加密，然后使用非对称加密的公钥再对秘钥进行加密，所以网络上传输的数据是被秘钥加密的密文和用公钥加密后的秘密秘钥，因此即使被黑客截取，由于没有私钥，无法获取到加密明文的秘钥，便无法获取到明文数据。
>
> **数字摘要:** 通过单向hash函数对原文进行哈希，将需加密的明文“摘要”成一串固定长度(如128bit)的密文，不同的明文摘要成的密文其结果总是不相同，同样的明文其摘要必定一致，并且即使知道了摘要也不能反推出明文。
>
> **数字签名技术:** 数字签名建立在公钥加密体制基础上，是公钥加密技术的另一类应用。它把公钥加密技术和数字摘要结合起来，形成了实用的数字签名技术。
  
- 收方能够证实发送方的真实身份；
- 发送方事后不能否认所发送过的报文；
- 收方或非法者不能伪造、篡改报文。
  
![https流程](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/WX20191029-105132@2x.png )
  
非对称加密过程需要用到公钥进行加密，那么公钥从何而来？其实公钥就被包含在数字证书中，数字证书通常来说是由受信任的数字证书颁发机构CA，在验证服务器身份后颁发，证书中包含了一个密钥对（公钥和私钥）和所有者识别信息。数字证书被放到服务端，具有服务器身份验证和数据传输加密功能。
  
##  HTTP通信传输
  
  
![HTTP通信传输](https://img-blog.csdn.net/20180719094739178?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70 )
  
客户端输入URL回车，DNS解析域名得到服务器的IP地址，服务器在80端口监听客户端请求，端口通过TCP/IP协议（可以通过Socket实现）建立连接。HTTP属于TCP/IP模型中的运用层协议，所以通信的过程其实是对应数据的入栈和出栈。
  
![流程](https://img-blog.csdn.net/20180719094756330?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70 )
  
报文从运用层传送到运输层，运输层通过TCP三次握手和服务器建立连接，四次挥手释放连接。
  
![三次握手](https://img-blog.csdn.net/20180719110828114?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70 )
  
为什么需要三次握手呢？
  
> 为了防止已失效的连接请求报文段突然又传送到了服务端，因而产生错误。
  
比如：client发出的第一个连接请求报文段并没有丢失，而是在某个网络结点长时间的滞留了，以致延误到连接释放以后的某个时间才到达server。本来这是一个早已失效的报文段，但是server收到此失效的连接请求报文段后，就误认为是client再次发出的一个新的连接请求，于是就向client发出确认报文段，同意建立连接。
  
假设不采用“三次握手”，那么只要server发出确认，新的连接就建立了，由于client并没有发出建立连接的请求，因此不会理睬server的确认，也不会向server发送数据，但server却以为新的运输连接已经建立，并一直等待client发来数据。所以没有采用“三次握手”，这种情况下server的很多资源就白白浪费掉了。
  
  
![四次握手](https://img-blog.csdn.net/20180719110841774?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70 )
  
为什么需要四次挥手呢？
  
> TCP是全双工模式，当client发出FIN报文段时，只是表示client已经没有数据要发送了，client告诉server，它的数据已经全部发送完毕了；但是，这个时候client还是可以接受来server的数据；当server返回ACK报文段时，表示它已经知道client没有数据发送了，但是server还是可以发送数据到client的；当server也发送了FIN报文段时，这个时候就表示server也没有数据要发送了，就会告诉client，我也没有数据要发送了，如果收到client确认报文段，之后彼此就会愉快的中断这次TCP连接。
  
##  HTTPS实现原理
  
  
###  SSL建立连接过程
  
![SSL建立连接过程](https://img-blog.csdnimg.cn/20190803111825690.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx,size_16,color_FFFFFF,t_70 )
  
1. client向server发送请求https://baidu.com，然后连接到server的443端口，发送的信息主要是随机值1和客户端支持的加密算法。
2. server接收到信息之后给予client响应握手信息，包括随机值2和匹配好的协商加密算法，这个加密算法一定是client发送给server加密算法的子集。
3. 随即server给client发送第二个响应报文是数字证书。服务端必须要有一套数字证书，可以自己制作，也可以向组织申请。区别就是自己颁发的证书需要客户端验证通过，才可以继续访问，而使用受信任的公司申请的证书则不会弹出提示页面，这套证书其实就是一对公钥和私钥。传送证书，这个证书其实就是公钥，只是包含了很多信息，如证书的颁发机构，过期时间、服务端的公钥，第三方证书认证机构(CA)的签名，服务端的域名信息等内容。
4. 客户端解析证书，这部分工作是由客户端的TLS来完成的，首先会验证公钥是否有效，比如颁发机构，过期时间等等，如果发现异常，则会弹出一个警告框，提示证书存在问题。如果证书没有问题，那么就生成一个随即值（预主秘钥）。
5. 客户端认证证书通过之后，接下来是通过随机值1、随机值2和预主秘钥组装会话秘钥。然后通过证书的公钥加密会话秘钥。
6. 传送加密信息，这部分传送的是用证书加密后的会话秘钥，目的就是让服务端使用秘钥解密得到随机值1、随机值2和预主秘钥。
7. 服务端解密得到随机值1、随机值2和预主秘钥，然后组装会话秘钥，跟客户端会话秘钥相同。
8. 客户端通过会话秘钥加密一条消息发送给服务端，主要验证服务端是否正常接受客户端加密的消息。
9. 同样服务端也会通过会话秘钥加密一条消息回传给客户端，如果客户端能够正常接受的话表明SSL层连接建立完成了。
  
> 怎么保证保证服务器给客户端下发的公钥是真正的公钥，而不是中间人伪造的公钥呢？
  
![流程](https://img-blog.csdn.net/20180724090424143?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70 )
  
> 证书如何安全传输，被掉包了怎么办？
  
![签名是否真实](https://img-blog.csdn.net/20180719095555854?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70 )
  
**数字证书内容**
  
包括了加密后服务器的公钥、权威机构的信息、服务器域名，还有经过CA私钥签名之后的证书内容（经过先通过Hash函数计算得到证书数字摘要，然后用权威机构私钥加密数字摘要得到数字签名)，签名计算方法以及证书对应的域名。
  
**验证证书安全性过程**
  
- 当客户端收到这个证书之后，使用本地配置的权威机构的公钥对证书进行解密得到服务端的公钥和证书的数字签名，数字签名经过CA公钥解密得到证书信息摘要。
- 然后证书签名的方法计算一下当前证书的信息摘要，与收到的信息摘要作对比，如果一样，表示证书一定是服务器下发的，没有被中间人篡改过。因为中间人虽然有权威机构的公钥，能够解析证书内容并篡改，但是篡改完成之后中间人需要将证书重新加密，但是中间人没有权威机构的私钥，无法加密，强行加密只会导致客户端无法解密，如果中间人强行乱修改证书，就会导致证书内容和证书签名不匹配。
  
那第三方攻击者能否让自己的证书显示出来的信息也是服务端呢？（伪装服务端一样的配置）显然这个是不行的，因为当第三方攻击者去CA那边寻求认证的时候CA会要求其提供例如域名的whois信息、域名管理邮箱等证明你是服务端域名的拥有者，而第三方攻击者是无法提供这些信息所以他就是无法骗CA他拥有属于服务端的域名
  
  
##  运用与总结
  
  
###  安全性考虑
  
  
- TTPS协议的加密范围也比较有限，在黑客攻击、拒绝服务攻击、服务器劫持等方面几乎起不到什么作用
- SSL证书的信用链体系并不安全，特别是在某些国家可以控制CA根证书的情况下，中间人攻击一样可行
  
中间人攻击（MITM攻击）是指，黑客拦截并篡改网络中的通信数据。又分为被动MITM和主动MITM，被动MITM只窃取通信数据而不修改，而主动MITM不但能窃取数据，还会篡改通信数据。最常见的中间人攻击常常发生在公共wifi或者公共路由上。
  
###  成本考虑
  
- SSL证书需要购买申请，功能越强大的证书费用越高
- SSL证书通常需要绑定IP，不能在同一IP上绑定多个域名，IPv4资源不可能支撑这个消耗（SSL有扩展可以部分解决这个问题，但是比较麻烦，而且要求浏览器、操作系统支持，Windows XP就不支持这个扩展，考虑到XP的装机量，这个特性几乎没用）。
- 根据ACM CoNEXT数据显示，使用HTTPS协议会使页面的加载时间延长近50%，增加10%到20%的耗电。
- HTTPS连接缓存不如HTTP高效，流量成本高。
- HTTPS连接服务器端资源占用高很多，支持访客多的网站需要投入更大的成本。
- HTTPS协议握手阶段比较费时，对网站的响应速度有影响，影响用户体验。比较好的方式是采用分而治之，类似12306网站的主页使用HTTP协议，有关于用户信息等方面使用HTTPS。
  
————————————————
版权声明：本文为CSDN博主「会飞的狗~」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/xiaoming100001/article/details/81109617
  
---
  
#  Request
  
  
##  什么是request
  
  
`request`是`Servlet.service()`方法的一个参数，类型为`javax.servlet.http.HttpServletRequest`。在客户端发出每个请求时，服务器都会创建一个request对象，并把请求数据封装到request中，然后在调用`Servlet.service()`方法时传递给`service()`方法，这说明在`service()`方法中可以通过`request`对象来获取请求数据。
  
![图例](https://img-blog.csdn.net/20160816101242457?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center )
  
request的功能可以分为以下几种：
  
- 封装了请求头数据；
  
- 封装了请求正文数据，如果是GET请求，那么就没有正文；
  
- request是一个域对象，可以把它当成Map来添加获取数据；
  
- request提供了请求转发和请求包含功能。
  
##  request域方法
  
  
request是域对象！在JavaWeb中一共四个域对象，其中ServletContext就是域对象，它在整个应用中只创建一个ServletContext对象。request其中一个，request可以在一个请求中共享数据。
  
一个请求会创建一个request对象，如果在一个请求中经历了多个Servlet，那么多个Servlet就可以使用request来共享数据。现在我们还不知道如何在一个请求中经历几个Servlet。
  
- （1）`void setAttribute(String name, Object value)：`用来存储一个对象，也可以称之为存储一个域属性，例如：`servletContext.setAttribute(“xxx”, “XXX”)`，在request中保存了一个域属性，域属性名称为xxx，域属性的值为XXX。请注意，如果多次调用该方法，并且使用相同的name，那么会覆盖上一次的值，这一特性与Map相同；
  
- （2）`Object getAttribute(String name)：`用来获取request中的数据，当前在获取之前需要先去存储才行，例如：`String value = (String)request.getAttribute(“xxx”);`，获取名为xxx的域属性；
  
- （3）`void removeAttribute(String name)：`用来移除request中的域属性，如果参数name指定的域属性不存在，那么本方法什么都不做；
  
- （4）`Enumeration getAttributeNames()：`获取所有域属性的名称；
  
##  request获取请求头数据
  
  
request与请求头相关的方法有：
  
- `String getHeader(String name)：`获取指定名称的请求头；
  
- `Enumeration getHeaderNames()：`获取所有请求头名称；
  
- `int getIntHeader(String name)：`获取值为int类型的请求头。
  
  
##  request获取请求相关的其它方法
  
request中还提供了与请求相关的其他方法，有些方法是为了我们更加便捷的方法请求头数据而设计，有些是与请求URL相关的方法。
- `int getContentLength()：`获取请求体的字节数，GET请求没有请求体，没有请求体返回-1；
- `String getContentType()：`获取请求类型，如果请求是GET，那么这个方法返回null；如果是POST请求，那么默认为`application/x- www-form-urlencoded`，表示请求体内容使用了URL编码；
- `String getMethod()：`返回请求方法，例如：GET
- `Locale getLocale()：`返回当前客户端浏览器的Locale。`java.util.Locale`表示国家和言语，这个东西在国际化中很有用；
- `String getCharacterEncoding()：`获取请求编码，如果没有`setCharacterEncoding()`，那么返回null，表示使用ISO-8859-1编码；
- `void setCharacterEncoding(String code)：`设置请求编码，只对请求体有效！注意，对于GET而言，没有请求体！！！所以此方法只能对POST请求中的参数有效！
- `String getContextPath()：`返回上下文路径，例如：/hello
- `String getQueryString()：`返回请求URL中的参数，例如：name=zhangSan
- `String getRequestURI()：`返回请求URI路径，例如：/hello/oneServlet
- `StringBuffer getRequestURL()：`返回请求URL路径，例如：`http://localhost/hello/oneServlet`，即返回除了参数以外的路径信息；
- `String getServletPath()：`返回Servlet路径，例如：/oneServlet
- `String getRemoteAddr()：`返回当前客户端的IP地址；
- `String getRemoteHost()：`返回当前客户端的主机名，但这个方法的实现还是获取IP地址；
- `String getScheme()：`返回请求协议，例如：http；
- `String getServerName()：`返回主机名，例如：localhost
- `int getServerPort()：`返回服务器端口号，例如：8080
  
##  request获取请求参数
  
  
最为常见的客户端传递参数方式有两种：
  
- 浏览器地址栏直接输入：一定是GET请求；
  
- 超链接：一定是GET请求；
  
- 表单：可以是GET，也可以是POST，这取决与<form>的method属性值；
  
  
  
###  GET请求和POST请求的区别
  
  
**GET请求**
  
- 请求参数会在浏览器的地址栏中显示，所以不安全；
  
- 请求参数长度限制长度在1K之内；
  
- GET请求没有请求体，无法通过request.setCharacterEncoding()来设置参数的编码；
  
**POST请求**
  
- 请求参数不会显示浏览器的地址栏，相对安全；
  
- 请求参数长度没有限制；
  
  
  
下面是使用request获取请求参数的API：
  
- `String getParameter(String name)：`通过指定名称获取参数值；
  
- `String[] getParameterValues(String name)：`当多个参数名称相同时，可以使用方法来获取；
  
- `Enumeration getParameterNames()：`获取所有参数的名字；
  
- `Map getParameterMap()：`获取所有参数封装到Map中，其中key为参数名，value为参数值，因为一个参数名称可能有多个值，所以参数值是String[]，而不是String。
  
###  请求转发和请求包含
  
  
无论是请求转发还是请求包含，都表示由多个Servlet共同来处理一个请求。例如Servlet1来处理请求，然后Servlet1又转发给Servlet2来继续处理这个请求。
  
  
请求转发和请求包含`RequestDispatcher rd = request.getRequestDispatcher("/MyServlet");` 使用`request`获取`RequestDispatcher`对象，方法的参数是被转发或包含的`Servlet`的`Servlet`路径
  
- 请求转发：`rd.forward(request,response)`;
- 请求包含：`rd.include(request,response)`;
  
有时一个请求需要多个`Servlet`协作才能完成，所以需要在一个`Servlet`跳到另一个`Servlet`！
  
- 一个请求跨多个`Servlet`，需要使用转发和包含。
- 请求转发：由下一个`Servlet`完成响应体！当前`Servlet`可以设置响应头！（留头不留体）即当前`Servlet`设置的相应头有效，相应体无效。
- 请求包含：由两个`Servlet`共同未完成响应体！（留头又留体）都有效。 
- 无论是请求转发还是请求包含，都在一个请求范围内！使用同一个`request`和`response`！
  
  
###  请求转发与请求包含比较
  
  
1. 如果在`AServlet`中请求转发到`BServlet`，那么在`AServlet`中就不允许再输出响应体，即不能再使用`response.getWriter()`和`response.getOutputStream()`向客户端输出，这一工作应该由`BServlet`来完成；如果是使用请求包含，那么没有这个限制；
  
2. 请求转发虽然不能输出响应体，但还是可以设置响应头的，例如：`response.setContentType(”text/html;charset=utf-8”)`;
  
3. 请求包含大多是应用在JSP页面中，完成多页面的合并；
  
4. 请求转发大多是应用在`Servlet`中，转发目标大多是JSP页面；
  
![图例](https://img-blog.csdn.net/20160816102052342?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center )
  
###  请求转发与重定向比较
  
  
- 请求转发是一个请求，而重定向是两个请求；
  
- 请求转发后浏览器地址栏不会有变化，而重定向会有变化，因为重定向是两个请求；
  
- 请求转发的目标只能是本应用中的资源，重定向的目标可以是其他应用；
  
- 请求转发对`AServlet`和`BServlet`的请求方法是相同的，即要么都是GET，要么都是POST，因为请求转发是一个请求；
  
- 重定向的第二个请求一定是GET；
  
#  response
  
  
##  什么是response？
  
  
`response`是`Servlet.service`方法的一个参数，类型为`javax.servlet.http.HttpServletResponse`。在客户端发出每个请求时，服务器都会创建一个response对象，并传入给`Servlet.service()`方法。`response`对象是用来对客户端进行响应的，这说明在`service()`方法中使用`response`对象可以完成对客户端的响应工作。
  
`response`对象的功能分为以下四种：
  
（1）设置响应头信息
  
（2）发送状态码
  
（3）设置响应正文
  
（4）重定向
  
  
##  response响应正文
  
  
`response`是响应对象，向客户端输出响应正文（响应体）可以使用response的响应流，repsonse一共提供了两个响应流对象：
  
- `PrintWriter out = response.getWriter()`：获取字符流；
  
- `ServletOutputStreamout = response.getOutputStream()`：获取字节流；
  
  
当然，如果响应正文内容为字符，那么使用`response.getWriter()`，如果响应内容是字节，例如下载时，那么可以使用`response.getOutputStream()`。
  
注意，在一个请求中，不能同时使用这两个流！也就是说，要么你使用`repsonse.getWriter()`，要么使用`response.getOutputStream()`，但不能同时使用这两个流。不然会抛出`illegalStateException`异常。
  
###  字符响应流
  
  
####  字符编码
  
  
在使用`response.getWriter()`时需要注意默认字符编码为`ISO-8859-1`，如果希望设置字符流的字符编码为`utf-8`，可以使用`response.setCharaceterEncoding("utf-8")`来设置。这样可以保证输出给客户端的字符都是使用`UTF-8`编码的！
  
但客户端浏览器并不知道响应数据是什么编码的！如果希望通知客户端使用`UTF-8`来解读响应数据，那么还是使用`response.setContentType("text/html;charset=utf-8")`方法比较好，因为这个方法不只会调用`response.setCharaceterEncoding("utf-8")`，还会设置`content-type`响应头，客户端浏览器会使用`content-type`头来解读响应数据。
  
  
  
####  缓冲区
  
  
`response.getWriter()`是`PrintWriter`类型，所以它有缓冲区，缓冲区的默认大小为8KB。也就是说，在响应数据没有输出8KB之前，数据都是存放在缓冲区中，而不会立刻发送到客户端。当`Servlet`执行结束后，服务器才会去刷新流，使缓冲区中的数据发送到客户端。
  
如果希望响应数据马上发送给客户端：
  
向流中写入大于8KB的数据；
  
调用response.flushBuffer()方法来手动刷新缓冲区；
  
##  设置响应头信息
  
  
可以使用`response`对象的`setHeader()`方法来设置响应头！
  
使用该方法设置的响应头最终会发送给客户端浏览器！
  
（1）`response.setHeader("content-type", "text/html;charset=utf-8")`：设置`content-type`响应头，该头的作用是告诉浏览器响应内容为html类型，编码为`utf-8`。而且同时会设置`response`的字符流编码为`utf-8`，即`response.setCharaceterEncoding("utf-8")`；
  
（2）`response.setHeader("Refresh","5; URL=http://www.baidu.com")`：5秒后自动跳转到百度主页。
  
  
  
##  设置状态码及其他方法
  
  
（1）`response.setContentType("text/html;charset=utf-8")`：等同与调用`response.setHeader("content-type", "text/html;charset=utf-8")`；
（2）`response.setCharacterEncoding("utf-8")`：设置字符响应流的字符编码为`utf-8`；
（3）`response.setStatus(200)`：设置状态码；
（4）`response.sendError(404,"您要查找的资源不存在”)`：当发送错误状态码时，`Tomcat`会跳转到固定的错误页面去，但可以显示错误信息。
  
##  5、重定向
  
  
###  什么是重定向（两次请求）
  
  
当你访问`http://www.sun.com`时，你会发现浏览器地址栏中的URL会变成`http://www.Oracle.com/us/sun/index.htm`，这就是重定向了。重定向是服务器通知浏览器去访问另一个地址，即再发出另一个请求。
  
![重定向](https://img-blog.csdn.net/20160816095908794?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center )
  
  
###  如何完成重定向？
  
  
重定向的状态码为302，我们首先使用response对象向浏览器发送302的状态码，之后再设置一个Location，即给出一个可用的URL，由浏览器去访问新的URL，实现重定向。
  
举例：
  
```java
  
public class AServlet extends HttpServlet {  
    public void doGet(HttpServletRequest request, HttpServletResponse response)  
            throws ServletException, IOException {  
        response.setStatus(302);   
        response.setHeader("Location", "http://www.baidu.com");   
    }  
}  
```
  
上面代码的作用是：当访问`AServlet`后，会通知浏览器重定向到百度主页。客户端浏览器解析到响应码为302后，就知道服务器让它重定向，所以它会马上获取响应头Location，然发出第二个请求。
  
还有一种快捷的重定向方法，即使用`response.sendRedirect()`方法。比如上面例子中的两句可以使用`response.sendRedirect("http://www.baidu.com")`代替。
  
#  案例
  
  
##  用户登录案例需求
  
  
1. 编写login.html登录页面，包含username & password 两个输入框
2. 使用Druid数据库连接池技术,操作mysql，day14数据库中user表
3. 使用JdbcTemplate技术封装JDBC
4. 登录成功跳转到SuccessServlet展示：登录成功！用户名,欢迎您
5. 登录失败跳转到FailServlet展示：登录失败，用户名或密码错误
  
##  开发步骤
  
1. 创建项目，导入html页面，配置文件，jar包
2. 创建数据库环境
```sql
  CREATE DATABASE userLogin;
  USE userLogin;
  CREATE TABLE USER(		
	id INT PRIMARY KEY AUTO_INCREMENT,
	username VARCHAR(32) UNIQUE NOT NULL,
	PASSWORD VARCHAR(32) NOT NULL
	);
  
  ```
  
3. 创建包cn.domain,创建类User
```java
package cn.domain;
/**
 * 用户的实体类
 */
public class User {
  
    private int id;
    private String username;
    private String password;
  
  
    public int getId() {
        return id;
    }
  
    public void setId(int id) {
        this.id = id;
    }
  
    public String getUsername() {
        return username;
    }
  
    public void setUsername(String username) {
        this.username = username;
    }
  
    public String getPassword() {
        return password;
    }
  
    public void setPassword(String password) {
        this.password = password;
    }
  
    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                '}';
    }
}
  
```
4. 创建包cn.util,编写工具类JDBCUtils
  
```java
  
package cn.util;
  
import com.alibaba.druid.pool.DruidDataSourceFactory;
  
import javax.sql.DataSource;
import javax.xml.crypto.Data;
import java.io.IOException;
import java.io.InputStream;
import java.sql.Connection;
import java.sql.SQLException;
import java.util.Properties;
  
/**
 * JDBC工具类 使用Durid连接池
 */
public class JDBCUtils {
  
    private static DataSource ds ;
  
    static {
  
        try {
            //1.加载配置文件
            Properties pro = new Properties();
            //使用ClassLoader加载配置文件，获取字节输入流
            InputStream is = JDBCUtils.class.getClassLoader().getResourceAsStream("druid.properties");
            pro.load(is);
  
            //2.初始化连接池对象
            ds = DruidDataSourceFactory.createDataSource(pro);
  
        } catch (IOException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
  
    /**
     * 获取连接池对象
     */
    public static DataSource getDataSource(){
        return ds;
    }
  
  
    /**
     * 获取连接Connection对象
     */
    public static Connection getConnection() throws SQLException {
        return  ds.getConnection();
    }
}
```
5. 创建包cn.dao,创建类UserDao,提供login方法
  
```java
  
package cn.dao;
  
import cn.domain.User;
import cn.util.JDBCUtils;
import org.springframework.dao.DataAccessException;
import org.springframework.jdbc.core.BeanPropertyRowMapper;
import org.springframework.jdbc.core.JdbcTemplate;
  
/**
 * 操作数据库中User表的类
 */
public class UserDao {
  
    //声明JDBCTemplate对象共用
    private JdbcTemplate template = new JdbcTemplate(JDBCUtils.getDataSource());
  
    /**
     * 登录方法
     * @param loginUser 只有用户名和密码
     * @return user包含用户全部数据,没有查询到，返回null
     */
    public User login(User loginUser){
        try {
            //1.编写sql
            String sql = "select * from user where username = ? and password = ?";
            //2.调用query方法
            User user = template.queryForObject(sql,
                    new BeanPropertyRowMapper<User>(User.class),
                    loginUser.getUsername(), loginUser.getPassword());
  
  
            return user;
        } catch (DataAccessException e) {
            e.printStackTrace();//记录日志
            return null;
        }
    }
}
```
6. 编写cn.web.servlet.LoginServlet类
  
```java
  
package cn.web.servlet;
  
import cn.dao.UserDao;
import cn.domain.User;
  
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
  
  
@WebServlet("/loginServlet")
public class LoginServlet extends HttpServlet {
  
  
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1.设置编码
        req.setCharacterEncoding("utf-8");
        //2.获取请求参数
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        //3.封装user对象
        User loginUser = new User();
        loginUser.setUsername(username);
        loginUser.setPassword(password);
  
        //4.调用UserDao的login方法
        UserDao dao = new UserDao();
        User user = dao.login(loginUser);
  
        //5.判断user
        if(user == null){
            //登录失败
            req.getRequestDispatcher("/failServlet").forward(req,resp);
        }else{
            //登录成功
            //存储数据
            req.setAttribute("user",user);
            //转发
            req.getRequestDispatcher("/successServlet").forward(req,resp);
        }
  
    }
  
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doGet(req,resp);
    }
}
```
7. 编写FailServlet和SuccessServlet类
  
```java
  
@WebServlet("/successServlet")
public class SuccessServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //获取request域中共享的user对象
        User user = (User) request.getAttribute("user");
  
        if(user != null){
            //给页面写一句话
  
            //设置编码
            response.setContentType("text/html;charset=utf-8");
            //输出
            response.getWriter().write("登录成功！"+user.getUsername()+",欢迎您");
        }
  
  
    }		
  
  
@WebServlet("/failServlet")
public class FailServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //给页面写一句话
  
        //设置编码
        response.setContentType("text/html;charset=utf-8");
        //输出
        response.getWriter().write("登录失败，用户名或密码错误");
  
    }
  
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request,response);
    }
}
```
  
  
注意：BeanUtils工具类，用于封装JavaBean的简化数据封装
  
1. 类必须被public修饰
2. 必须提供空参的构造器
3. 成员变量必须使用private修饰
4. 提供公共setter和getter方法
  
  
  
@import '/doc/07:javaWeb/04-cookie和Session.md'
  