  
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
- [Cookie和Session](#cookie和session )
  - [Cookie](#cookie )
    - [什么是Cookie](#什么是cookie )
    - [记录用户访问次数](#记录用户访问次数 )
    - [Cookie的不可跨域名性](#cookie的不可跨域名性 )
    - [Unicode编码：保存中文](#unicode编码保存中文 )
    - [BASE64编码：保存二进制图片](#base64编码保存二进制图片 )
    - [设置Cookie的所有属性](#设置cookie的所有属性 )
    - [Cookie的有效期](#cookie的有效期 )
    - [Cookie的修改、删除](#cookie的修改-删除 )
    - [Cookie的域名](#cookie的域名 )
    - [Cookie的路径](#cookie的路径 )
    - [Cookie的安全属性](#cookie的安全属性 )
    - [avaScript操作Cookie](#avascript操作cookie )
    - [案例：永久登录](#案例永久登录 )
  - [Session](#session )
    - [什么是Session](#什么是session )
    - [实现用户登录](#实现用户登录 )
    - [Session的生命周期](#session的生命周期 )
    - [Session的有效期](#session的有效期 )
    - [Session的常用方法](#session的常用方法 )
    - [Session对浏览器的要求](#session对浏览器的要求 )
    - [URL地址重写](#url地址重写 )
    - [Session中禁止使用Cookie](#session中禁止使用cookie )
  
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
  
一个Host可以有多个Context，通常不建议定义在server.xml文件中，而是每一个context定义使用一个单独的XML文件进行，其文件的目录为`<img src="https://latex.codecogs.com/gif.latex?CATALINA_HOME&#x2F;conf&#x2F;&lt;engine%20name&gt;&#x2F;&lt;host%20name&gt;`。可以看到server.xml中默认没有定义Context，但存在&#x2F;conf&#x2F;context.xml，在前面说Tomcat配置文件时曾介绍过，context.xml为部署与此Tomcat实例上所有的web应用程序提供的默认配置文件，删除注释后其内容如下：通过它可以找到默认的和各web应用程序提供部署描述符文件web.xml，&#x2F;conf&#x2F;web.xml定义了Tomcat提供的默认Servlet处理程序，主要用来处理静态资源请求；而各webapp的web.xml可以定义其他的动态请求url映射到不同Servlet程序处理。**常用的属性定义有**-%20docBase：相应的Web应用程序的存放位置；也可以使用相对路径，起始路径为此Context所属Host中appBase定义的路径；切记，docBase的路径名不能与相应的Host中appBase中定义的路径名有包含关系，比如，如果appBase为deploy，而docBase绝不能为deploy-bbs类的名字；-%20path：相对于Web服务器根路径而言的URI；如果为空&quot;&quot;，则表示为此webapp的根路径；如果context定义在一个单独的xml文件中，此属性不需要定义；-%20reloadable：是否允许重新加载此context相关的Web应用程序的类；默认为false；     ###%20%20Realm组件Realm（领域）表示分配给这些用户的用户名，密码和角色（类似于Unix组）的&quot;数据库&quot;。一个Realm（领域）表示一个安全上下文，它是一个授权访问某个给定Context的用户列表和某用户所允许切换的角色相关定义的列表。Catalina容器（Engine，Host或Context）可以包含不超过一个Realm元素（但自身可以嵌套）。此外，与引擎或主机关联的领域由低级容器自动继承，除非下级容器显式定义了自己的领域。如果没有为引擎配置领域，将自动为引擎配置空领域的实例。定义Realm时惟一必须要提供的属性是classname，它是Realm的多个不同实现，用于表示此Realm认证的用户及角色等认证信息的存放位置，Tomcat中实现了多种不同的Realm，如下：-%20UserDatabaseRealm：基于UserDatabase文件(通常是tomcat-user.xml)实现用户认证，它实现是一个完全可更新和持久有效的MemoryRealm，因此能够跟标准的MemoryRealm兼容；它通过JNDI实现；-%20LockOutRealm：提供锁定功能，以便在给定时间段内出现过多的失败认证尝试时提供用户锁定机制；-%20JAASRealm：基于Java%20Authintication%20and%20Authorization%20Service实现用户认证；-%20JDBCRealm：通过JDBC访问某关系型数据库表实现用户认证；-%20JNDIRealm：基于JNDI使用目录服务实现认证信息的获取；-%20MemoryRealm：查找tomcat-user.xml文件实现用户信息的获取。可以看到默认配置文件中定义了一个LockOutRealm并嵌套一个UserDatabaseRealm的Realm来通过tomcat-user.xml文件实现用户认证。###%20%20Valve组件Valve（阀门）类似于过滤器，用来拦截请求并在将其转至目标之前进行某种处理操作；它可以工作于Engine和Host&#x2F;Context之间、Host和Context之间以及Context和Web应用程序的某资源之间。Valve常被用来记录客户端请求、客户端IP地址和服务器等信息，这种处理技术通常被称作请求转储(request%20dumping)。请求转储valve记录请求客户端请求数据包中的HTTP首部信息和cookie信息文件中，响应转储valve则记录响应数据包首部信息和cookie信息至文件中。一个容器内可以建立多个Valve，而且Valve定义的次序也决定了它们生效的次序。不同类型的Value具有不同的处理能力，Tomcat中实现了多种不同的Valve：-%20AccessLogValve：访问日志Valve-%20ExtendedAccessValve：扩展功能的访问日志Valve-%20RequestDumperValve：请求转储Valve；-%20RemoteAddrValve：基于远程地址的访问控制；-%20RemoteHostValve：基于远程主机名称的访问控制；-%20SemaphoreValve：用于控制Tomcat主机上任何容器上的并发访问数量；-%20ReplicationValve：专用于Tomcat集群架构中，可以在某个请求的session信息发生更改时触发session数据在各节点间进行复制；-%20SingleSignOn：将两个或多个需要对用户进行认证webapp在认证用户时连接在一起，即一次认证即可访问所有连接在一起的webapp；-%20ClusterSingleSingOn：对SingleSignOn的扩展，专用于Tomcat集群当中，需要结合ClusterSingleSignOnListener进行工作。-%20通过属性className定义相关的java实现的类名来选择Value。如默认配置文件中定义了一个AccessLogValve的Value来记录访问日志到文件中。      ###%20%20%20其他组件**1、Logger**日志记录器(Logger)：用于记录组件内部的状态信息，可被用于除Context之外的任何容器中。日志记录的功能可被继承，因此，一个引擎级别的Logger将会记录引擎内部所有组件相关的信息，除非某内部组件定义了自己的Logger组件（前面介绍的AccessLogValve使用自包含的逻辑来写它的日志文件，以获得更好的效率）。**2、Listener**Listener用于创建和配置LifecycleListener对象，而LifecycleListener通常被开发人员用来创建和删除容器。**3、Loader**Java的动态装载功能是其语言功能强大表现之一，Servlet容器使用此功能在运行时动态装载servlet和它们所依赖的类。Loader可以用于Context中控制java类的加载，即WebApp类加载器。**4、Resources**经常用于实现在Context中指定需要装载的但不在Tomcat本地磁盘上的应用资源，如Java类，HTML页面，JSP文件等。**5、GlobalNamingResources**应用于整个服务器的JNDI映射，此可以避免每个Web应用程序都需要在各自的web.xml创建，这在web应用程序以WAR的形式存在时尤为有用。它通常可以包含三个子元素：Environment、Resource和ResourceEnvRef。**6、WatchedResource**WatchedResource可以用于Context中监视指定的webapp程序文件的改变，并且能够在监视到文件内容发生改变时重新装载此文件。**7、Manager**Manger对象用于实现HTTP会话管理的功能，Tomcat中有5种Manger的实现：-%20StandardManager,Tomcat6的默认会话管理器，用于非集群环境中对单个处于运行状态的Tomcat实例会话进行管理。当Tomcat关闭时，这些会话相关的数据会被写入磁盘上的一个名叫SESSION.ser的文件，并在Tomcat下次启动时读取此文件。-%20PersistentManager,当一个会话长时间处于空闲状态时会被写入到swap会话对象，这对于内存资源比较吃紧的应用环境来说比较有用。-%20DeltaManager,属于ClusterManager，用于Tomcat集群的会话管理器，它通过将改变了会话数据同步给集群中的其它节点实现会话复制。这种实现会将所有会话的改变同步给集群中的每一个节点，也是在集群环境中用得最多的一种实现方式。但集群节点较多时，会消耗大量的网络资源，一般适用于3、4个节点的集群。-%20BackupManager,属于ClusterManager，用于Tomcat集群的会话管理器，与DeltaManager不同的是，某节点会话的改变只会同步给集群中的另一个而非所有节点。-%20SimpleTcpReplicationManager,Tomcat4时用到的版本，过于老旧了。**8、Stores**PersistentManager必须包含一个Store元素以指定将会话数据存储至何处。这通常有两种实现方式：FileStore和JDBCStore。**9、Cluster**专用于配置Tomcat集群的元素，可用于Engine和Host容器中。在用于Engine容器中时，Engine中的所有Host均支持集群功能。在Cluster元素中，需要直接定义一个Manager元素，这个Manager元素有一个其值为org.apache.catalina.ha.session.DeltaManager或org.apache.catalina.ha.session.BackupManager的className属性。同时，Cluster中还需要分别定义一个Channel和ClusterListener元素。**10、Channel**用于Cluster中给集群中同一组中的节点定义通信&quot;信道&quot;。Channel中需要至少定义Membership、Receiver和Sender三个元素，此外还有一个可选元素Interceptor。**11、Membership**用于Channel中配置同一通信信道上节点集群组中的成员情况，即监控加入当前集群组中的节点并在各节点间传递心跳信息，而且可以在接收不到某成员的心跳信息时将其从集群节点中移除。Tomcat6中Membership的实现是org.apache.catalina.tribes.membership.McastService。**12、Sender**用于Channel中配置&quot;复制信息&quot;的发送器，实现发送需要同步给其它节点的数据至集群中的其它节点。发送器不需要属性的定义，但可以在其内部定义一个Transport元素。**13、Transport**用于Sender内部，配置数据如何发送至集群中的其它节点。Tomcat有两种Transport的实现：-%20PooledMultiSender%20基于Java阻塞式IO，可以将一次将多个信息并发发送至其它节点，但一次只能传送给一个节点。-%20PooledParallelSener,基于Java非阻塞式IO，即NIO，可以一次发送多个信息至一个或多个节点。**14、Receiver**用于Channel定义某节点如何从其它节点的Sender接收复制数据，Tomcat中实现的接收方式有两种BioReceiver和NioReceiver。 ————————————————本文为CSDN博主「尐譽」的原创文章：https:&#x2F;&#x2F;blog.csdn.net&#x2F;tjiyu&#x2F;article&#x2F;details&#x2F;54590258%20%20#%20%20Servlet##%20%20什么是Servlet %20  Servlet（Server%20Applet），全称Java%20Servlet，未有中文译文。是用Java编写的服务器端程序。其主要功能在于交互式地浏览和修改数据，生成动态Web内容。狭义的Servlet是指Java语言实现的一个接口，广义的Servlet是指任何实现了这个Servlet接口的类，一般情况下，人们将Servlet理解为后者。Servlet运行于支持Java的应用服务器中。从实现上讲，Servlet可以响应任何类型的请求，但绝大多数情况下Servlet只用来扩展基于HTTP协议的Web服务器。##%20%20Servlet工作模式-%20客户端发送请求至服务器-%20服务器启动并调用Servlet，Servlet根据客户端请求生成响应内容并将其传给服务器-%20服务器将响应返回客户端##%20%20Servlet的API概览Servlet%20API%20包含以下4个Java包：1.%20`javax.servlet`其中包含定义servlet和servlet容器之间契约的类和接口。2.%20`javax.servlet.http`其中包含定义HTTP%20Servlet%20和Servlet容器之间的关系。3.%20`javax.servlet.annotation`其中包含标注servlet，Filter,Listener的标注。它还为被标注元件定义元数据。4.%20`javax.servlet.descriptor`，其中包含提供程序化登录Web应用程序的配置信息的类型。##%20%20Servlet%20的主要类型![](https:&#x2F;&#x2F;imagerepos.oss-cn-beijing.aliyuncs.com&#x2F;images&#x2F;20191025111742.png%20)##%20%20Servlet%20的使用方法Servlet技术的核心是Servlet，它是所有Servlet类必须直接或者间接实现的一个接口。在编写实现Servlet的Servlet类时，直接实现它。在扩展实现这个这个接口的类时，间接实现它。##%20%20Servlet%20的工作原理Servlet接口定义了Servlet与servlet容器之间的契约。这个契约是：Servlet容器将Servlet类载入内存，并产生Servlet实例和调用它具体的方法。但是要注意的是，在一个应用程序中，每种Servlet类型只能有一个实例。 用户请求致使Servlet容器调用Servlet的Service（）方法，并传入一个ServletRequest对象和一个ServletResponse对象。ServletRequest对象和ServletResponse对象都是由Servlet容器（例如TomCat）封装好的，并不需要程序员去实现，程序员可以直接使用这两个对象。ServletRequest中封装了当前的Http请求，因此，开发人员不必解析和操作原始的Http数据。ServletResponse表示当前用户的Http响应，程序员只需直接操作ServletResponse对象就能把响应轻松的发回给用户。对于每一个应用程序，Servlet容器还会创建一个ServletContext对象。这个对象中封装了上下文（应用程序）的环境详情。每个应用程序只有一个ServletContext。每个Servlet对象也都有一个封装Servlet配置的ServletConfig对象。##%20%20Servlet的体系结构	Servlet%20--%20接口			|GenericServlet%20--%20抽象类将Servlet接口中其他的方法做了默认空实现，只将service()方法作为抽象*%20将来定义Servlet类时，可以继承GenericServlet，实现service()方法即可			HttpServlet%20%20--%20抽象类%20对http协议的一种封装，简化操作1.%20定义类继承HttpServlet2.%20复写doGet&#x2F;doPost方法	##%20%20Servlet相关配置1.%20urlpartten:Servlet访问路径2.%20一个Servlet可以定义多个访问路径%20：%20@WebServlet({&quot;&#x2F;d4&quot;,&quot;&#x2F;dd4&quot;,&quot;&#x2F;ddd4&quot;})3.%20路径定义规则：	1.%20&#x2F;xxx：路径匹配	2.%20&#x2F;xxx&#x2F;xxx:多层路径，目录结构	3.%20*.do：扩展名匹配---#%20%20HTTP%20和%20HTTPS##%20%20HTTP###%20%20什么是HTTP?&gt;%20超文本传输协议，是一个基于请求与响应，无状态的，应用层的协议，常基于TCP&#x2F;IP协议传输数据，互联网上应用最为广泛的一种网络协议,所有的WWW文件都必须遵守这个标准。设计HTTP的初衷是为了提供一种发布和接收HTML页面的方法。![发展历史](https:&#x2F;&#x2F;imagerepos.oss-cn-beijing.aliyuncs.com&#x2F;images&#x2F;WX20191029-102756@2x.png%20)使用HTTP&#x2F;1.1和HTTP&#x2F;2同时请求379张图片，观察请求的时间，明显看出HTTP&#x2F;2性能占优势。![对比](https:&#x2F;&#x2F;imagerepos.oss-cn-beijing.aliyuncs.com&#x2F;images&#x2F;WX20191029-102930@2x.png%20)**多路复用：**%20通过单一的HTTP&#x2F;2连接请求发起多重的请求-响应消息，多个请求stream共享一个TCP连接，实现多留并行而不是依赖建立多个TCP连接。![报文格式](https:&#x2F;&#x2F;imagerepos.oss-cn-beijing.aliyuncs.com&#x2F;images&#x2F;WX20191029-103238@2x.png%20)###%20%20什么是HTTPS？&gt;%20《图解HTTP》这本书中曾提过HTTPS是身披SSL外壳的HTTP。HTTPS是一种通过计算机网络进行安全通信的传输协议，经由HTTP进行通信，利用SSL&#x2F;TLS建立全信道，加密数据包。HTTPS使用的主要目的是提供对网站服务器的身份认证，同时保护交换数据的隐私与完整性。&gt;%20PS:TLS是传输层加密协议，前身是SSL协议，由网景公司1995年发布，有时候两者不区分。##%20%20HTTP%20VS%20HTTPS###%20%20HTTP特点-%20无状态：协议对客户端没有状态存储，对事物处理没有“记忆”能力，比如访问一个网站需要反复进行登录操作-%20无连接：HTTP&#x2F;1.1之前，由于无状态特点，每次请求需要通过TCP三次握手四次挥手，和服务器重新建立连接。比如某个客户机在短时间多次请求同一个资源，服务器并不能区别是否已经响应过用户的请求，所以每次需要重新响应请求，需要耗费不必要的时间和流量。-%20基于请求和响应：基本的特性，由客户端发起请求，服务端响应-%20简单快速、灵活-%20通信使用明文、请求和响应不会对通信方进行确认、无法保护数据的完整性下面通过一个简单的抓包实验观察使用HTTP请求传输的数据：![抓包实验](https:&#x2F;&#x2F;imagerepos.oss-cn-beijing.aliyuncs.com&#x2F;images&#x2F;WX20191029-103707@2x.png%20)![12306结果](https:&#x2F;&#x2F;imagerepos.oss-cn-beijing.aliyuncs.com&#x2F;images&#x2F;WX20191029-103913@2x.png%20)**结果分析：%20HTTP协议传输数据以明文形式显示**针对无状态的一些解决策略：场景：逛电商商场用户需要使用的时间比较长，需要对用户一段时间的HTTP通信状态进行保存，比如执行一次登陆操作，在30分钟内所有的请求都不需要再次登陆。-%20通过Cookie&#x2F;Session技术-%20HTTP&#x2F;1.1持久连接（HTTP%20keep-alive）方法，只要任意一端没有明确提出断开连接，则保持TCP连接状态，在请求首部字段中的Connection:%20keep-alive即为表明使用了持久连接###%20%20HTTPS特点基于HTTP协议，通过SSL或TLS提供加密处理数据、验证对方身份以及数据完整性保护![https的特点](https:&#x2F;&#x2F;imagerepos.oss-cn-beijing.aliyuncs.com&#x2F;images&#x2F;WX20191029-104403@2x.png%20)通过抓包可以看到数据不是明文传输，而且HTTPS有如下特点：-%20内容加密：采用混合加密技术，中间者无法直接查看明文内容-%20验证身份：通过证书认证客户端访问的是自己的服务器-%20保护数据完整性：防止传输的内容被中间人冒充或者篡改&gt;%20**混合加密:**%20结合非对称加密和对称加密技术。客户端使用对称加密生成密钥对传输数据进行加密，然后使用非对称加密的公钥再对秘钥进行加密，所以网络上传输的数据是被秘钥加密的密文和用公钥加密后的秘密秘钥，因此即使被黑客截取，由于没有私钥，无法获取到加密明文的秘钥，便无法获取到明文数据。&gt;&gt;%20**数字摘要:**%20通过单向hash函数对原文进行哈希，将需加密的明文“摘要”成一串固定长度(如128bit)的密文，不同的明文摘要成的密文其结果总是不相同，同样的明文其摘要必定一致，并且即使知道了摘要也不能反推出明文。&gt;&gt;%20**数字签名技术:**%20数字签名建立在公钥加密体制基础上，是公钥加密技术的另一类应用。它把公钥加密技术和数字摘要结合起来，形成了实用的数字签名技术。-%20收方能够证实发送方的真实身份；-%20发送方事后不能否认所发送过的报文；-%20收方或非法者不能伪造、篡改报文。![https流程](https:&#x2F;&#x2F;imagerepos.oss-cn-beijing.aliyuncs.com&#x2F;images&#x2F;WX20191029-105132@2x.png%20)非对称加密过程需要用到公钥进行加密，那么公钥从何而来？其实公钥就被包含在数字证书中，数字证书通常来说是由受信任的数字证书颁发机构CA，在验证服务器身份后颁发，证书中包含了一个密钥对（公钥和私钥）和所有者识别信息。数字证书被放到服务端，具有服务器身份验证和数据传输加密功能。##%20%20HTTP通信传输![HTTP通信传输](https:&#x2F;&#x2F;img-blog.csdn.net&#x2F;20180719094739178?watermark&#x2F;2&#x2F;text&#x2F;aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx&#x2F;font&#x2F;5a6L5L2T&#x2F;fontsize&#x2F;400&#x2F;fill&#x2F;I0JBQkFCMA==&#x2F;dissolve&#x2F;70%20)客户端输入URL回车，DNS解析域名得到服务器的IP地址，服务器在80端口监听客户端请求，端口通过TCP&#x2F;IP协议（可以通过Socket实现）建立连接。HTTP属于TCP&#x2F;IP模型中的运用层协议，所以通信的过程其实是对应数据的入栈和出栈。![流程](https:&#x2F;&#x2F;img-blog.csdn.net&#x2F;20180719094756330?watermark&#x2F;2&#x2F;text&#x2F;aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx&#x2F;font&#x2F;5a6L5L2T&#x2F;fontsize&#x2F;400&#x2F;fill&#x2F;I0JBQkFCMA==&#x2F;dissolve&#x2F;70%20)报文从运用层传送到运输层，运输层通过TCP三次握手和服务器建立连接，四次挥手释放连接。![三次握手](https:&#x2F;&#x2F;img-blog.csdn.net&#x2F;20180719110828114?watermark&#x2F;2&#x2F;text&#x2F;aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx&#x2F;font&#x2F;5a6L5L2T&#x2F;fontsize&#x2F;400&#x2F;fill&#x2F;I0JBQkFCMA==&#x2F;dissolve&#x2F;70%20)为什么需要三次握手呢？&gt;%20为了防止已失效的连接请求报文段突然又传送到了服务端，因而产生错误。比如：client发出的第一个连接请求报文段并没有丢失，而是在某个网络结点长时间的滞留了，以致延误到连接释放以后的某个时间才到达server。本来这是一个早已失效的报文段，但是server收到此失效的连接请求报文段后，就误认为是client再次发出的一个新的连接请求，于是就向client发出确认报文段，同意建立连接。假设不采用“三次握手”，那么只要server发出确认，新的连接就建立了，由于client并没有发出建立连接的请求，因此不会理睬server的确认，也不会向server发送数据，但server却以为新的运输连接已经建立，并一直等待client发来数据。所以没有采用“三次握手”，这种情况下server的很多资源就白白浪费掉了。![四次握手](https:&#x2F;&#x2F;img-blog.csdn.net&#x2F;20180719110841774?watermark&#x2F;2&#x2F;text&#x2F;aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx&#x2F;font&#x2F;5a6L5L2T&#x2F;fontsize&#x2F;400&#x2F;fill&#x2F;I0JBQkFCMA==&#x2F;dissolve&#x2F;70%20)为什么需要四次挥手呢？&gt;%20TCP是全双工模式，当client发出FIN报文段时，只是表示client已经没有数据要发送了，client告诉server，它的数据已经全部发送完毕了；但是，这个时候client还是可以接受来server的数据；当server返回ACK报文段时，表示它已经知道client没有数据发送了，但是server还是可以发送数据到client的；当server也发送了FIN报文段时，这个时候就表示server也没有数据要发送了，就会告诉client，我也没有数据要发送了，如果收到client确认报文段，之后彼此就会愉快的中断这次TCP连接。##%20%20HTTPS实现原理###%20%20SSL建立连接过程![SSL建立连接过程](https:&#x2F;&#x2F;img-blog.csdnimg.cn&#x2F;20190803111825690.png?x-oss-process=image&#x2F;watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx,size_16,color_FFFFFF,t_70%20)1.%20client向server发送请求https:&#x2F;&#x2F;baidu.com，然后连接到server的443端口，发送的信息主要是随机值1和客户端支持的加密算法。2.%20server接收到信息之后给予client响应握手信息，包括随机值2和匹配好的协商加密算法，这个加密算法一定是client发送给server加密算法的子集。3.%20随即server给client发送第二个响应报文是数字证书。服务端必须要有一套数字证书，可以自己制作，也可以向组织申请。区别就是自己颁发的证书需要客户端验证通过，才可以继续访问，而使用受信任的公司申请的证书则不会弹出提示页面，这套证书其实就是一对公钥和私钥。传送证书，这个证书其实就是公钥，只是包含了很多信息，如证书的颁发机构，过期时间、服务端的公钥，第三方证书认证机构(CA)的签名，服务端的域名信息等内容。4.%20客户端解析证书，这部分工作是由客户端的TLS来完成的，首先会验证公钥是否有效，比如颁发机构，过期时间等等，如果发现异常，则会弹出一个警告框，提示证书存在问题。如果证书没有问题，那么就生成一个随即值（预主秘钥）。5.%20客户端认证证书通过之后，接下来是通过随机值1、随机值2和预主秘钥组装会话秘钥。然后通过证书的公钥加密会话秘钥。6.%20传送加密信息，这部分传送的是用证书加密后的会话秘钥，目的就是让服务端使用秘钥解密得到随机值1、随机值2和预主秘钥。7.%20服务端解密得到随机值1、随机值2和预主秘钥，然后组装会话秘钥，跟客户端会话秘钥相同。8.%20客户端通过会话秘钥加密一条消息发送给服务端，主要验证服务端是否正常接受客户端加密的消息。9.%20同样服务端也会通过会话秘钥加密一条消息回传给客户端，如果客户端能够正常接受的话表明SSL层连接建立完成了。&gt;%20怎么保证保证服务器给客户端下发的公钥是真正的公钥，而不是中间人伪造的公钥呢？![流程](https:&#x2F;&#x2F;img-blog.csdn.net&#x2F;20180724090424143?watermark&#x2F;2&#x2F;text&#x2F;aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx&#x2F;font&#x2F;5a6L5L2T&#x2F;fontsize&#x2F;400&#x2F;fill&#x2F;I0JBQkFCMA==&#x2F;dissolve&#x2F;70%20)&gt;%20证书如何安全传输，被掉包了怎么办？![签名是否真实](https:&#x2F;&#x2F;img-blog.csdn.net&#x2F;20180719095555854?watermark&#x2F;2&#x2F;text&#x2F;aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx&#x2F;font&#x2F;5a6L5L2T&#x2F;fontsize&#x2F;400&#x2F;fill&#x2F;I0JBQkFCMA==&#x2F;dissolve&#x2F;70%20)**数字证书内容**包括了加密后服务器的公钥、权威机构的信息、服务器域名，还有经过CA私钥签名之后的证书内容（经过先通过Hash函数计算得到证书数字摘要，然后用权威机构私钥加密数字摘要得到数字签名)，签名计算方法以及证书对应的域名。**验证证书安全性过程**-%20当客户端收到这个证书之后，使用本地配置的权威机构的公钥对证书进行解密得到服务端的公钥和证书的数字签名，数字签名经过CA公钥解密得到证书信息摘要。-%20然后证书签名的方法计算一下当前证书的信息摘要，与收到的信息摘要作对比，如果一样，表示证书一定是服务器下发的，没有被中间人篡改过。因为中间人虽然有权威机构的公钥，能够解析证书内容并篡改，但是篡改完成之后中间人需要将证书重新加密，但是中间人没有权威机构的私钥，无法加密，强行加密只会导致客户端无法解密，如果中间人强行乱修改证书，就会导致证书内容和证书签名不匹配。%20%20那第三方攻击者能否让自己的证书显示出来的信息也是服务端呢？（伪装服务端一样的配置）显然这个是不行的，因为当第三方攻击者去CA那边寻求认证的时候CA会要求其提供例如域名的whois信息、域名管理邮箱等证明你是服务端域名的拥有者，而第三方攻击者是无法提供这些信息所以他就是无法骗CA他拥有属于服务端的域名##%20%20运用与总结###%20%20安全性考虑-%20TTPS协议的加密范围也比较有限，在黑客攻击、拒绝服务攻击、服务器劫持等方面几乎起不到什么作用-%20SSL证书的信用链体系并不安全，特别是在某些国家可以控制CA根证书的情况下，中间人攻击一样可行%20%20中间人攻击（MITM攻击）是指，黑客拦截并篡改网络中的通信数据。又分为被动MITM和主动MITM，被动MITM只窃取通信数据而不修改，而主动MITM不但能窃取数据，还会篡改通信数据。最常见的中间人攻击常常发生在公共wifi或者公共路由上。###%20%20成本考虑-%20SSL证书需要购买申请，功能越强大的证书费用越高-%20SSL证书通常需要绑定IP，不能在同一IP上绑定多个域名，IPv4资源不可能支撑这个消耗（SSL有扩展可以部分解决这个问题，但是比较麻烦，而且要求浏览器、操作系统支持，Windows%20XP就不支持这个扩展，考虑到XP的装机量，这个特性几乎没用）。-%20根据ACM%20CoNEXT数据显示，使用HTTPS协议会使页面的加载时间延长近50%，增加10%到20%的耗电。-%20HTTPS连接缓存不如HTTP高效，流量成本高。-%20HTTPS连接服务器端资源占用高很多，支持访客多的网站需要投入更大的成本。-%20HTTPS协议握手阶段比较费时，对网站的响应速度有影响，影响用户体验。比较好的方式是采用分而治之，类似12306网站的主页使用HTTP协议，有关于用户信息等方面使用HTTPS。%20%20————————————————版权声明：本文为CSDN博主「会飞的狗~」的原创文章，遵循%20CC%204.0%20BY-SA%20版权协议，转载请附上原文出处链接及本声明。原文链接：https:&#x2F;&#x2F;blog.csdn.net&#x2F;xiaoming100001&#x2F;article&#x2F;details&#x2F;81109617---#%20%20Request##%20%20什么是request`request`是`Servlet.service()`方法的一个参数，类型为`javax.servlet.http.HttpServletRequest`。在客户端发出每个请求时，服务器都会创建一个request对象，并把请求数据封装到request中，然后在调用`Servlet.service()`方法时传递给`service()`方法，这说明在`service()`方法中可以通过`request`对象来获取请求数据。![图例](https:&#x2F;&#x2F;img-blog.csdn.net&#x2F;20160816101242457?watermark&#x2F;2&#x2F;text&#x2F;aHR0cDovL2Jsb2cuY3Nkbi5uZXQv&#x2F;font&#x2F;5a6L5L2T&#x2F;fontsize&#x2F;400&#x2F;fill&#x2F;I0JBQkFCMA==&#x2F;dissolve&#x2F;70&#x2F;gravity&#x2F;Center%20)request的功能可以分为以下几种：-%20封装了请求头数据；-%20封装了请求正文数据，如果是GET请求，那么就没有正文；-%20request是一个域对象，可以把它当成Map来添加获取数据；-%20request提供了请求转发和请求包含功能。##%20%20request域方法request是域对象！在JavaWeb中一共四个域对象，其中ServletContext就是域对象，它在整个应用中只创建一个ServletContext对象。request其中一个，request可以在一个请求中共享数据。一个请求会创建一个request对象，如果在一个请求中经历了多个Servlet，那么多个Servlet就可以使用request来共享数据。现在我们还不知道如何在一个请求中经历几个Servlet。-%20（1）`void%20setAttribute(String%20name,%20Object%20value)：`用来存储一个对象，也可以称之为存储一个域属性，例如：`servletContext.setAttribute(“xxx”,%20“XXX”)`，在request中保存了一个域属性，域属性名称为xxx，域属性的值为XXX。请注意，如果多次调用该方法，并且使用相同的name，那么会覆盖上一次的值，这一特性与Map相同；-%20（2）`Object%20getAttribute(String%20name)：`用来获取request中的数据，当前在获取之前需要先去存储才行，例如：`String%20value%20=%20(String)request.getAttribute(“xxx”);`，获取名为xxx的域属性；-%20（3）`void%20removeAttribute(String%20name)：`用来移除request中的域属性，如果参数name指定的域属性不存在，那么本方法什么都不做；-%20（4）`Enumeration%20getAttributeNames()：`获取所有域属性的名称；##%20%20request获取请求头数据request与请求头相关的方法有：-%20`String%20getHeader(String%20name)：`获取指定名称的请求头；-%20`Enumeration%20getHeaderNames()：`获取所有请求头名称；-%20`int%20getIntHeader(String%20name)：`获取值为int类型的请求头。##%20%20request获取请求相关的其它方法request中还提供了与请求相关的其他方法，有些方法是为了我们更加便捷的方法请求头数据而设计，有些是与请求URL相关的方法。-%20`int%20getContentLength()：`获取请求体的字节数，GET请求没有请求体，没有请求体返回-1；-%20`String%20getContentType()：`获取请求类型，如果请求是GET，那么这个方法返回null；如果是POST请求，那么默认为`application&#x2F;x-%20www-form-urlencoded`，表示请求体内容使用了URL编码；-%20`String%20getMethod()：`返回请求方法，例如：GET-%20`Locale%20getLocale()：`返回当前客户端浏览器的Locale。`java.util.Locale`表示国家和言语，这个东西在国际化中很有用；-%20`String%20getCharacterEncoding()：`获取请求编码，如果没有`setCharacterEncoding()`，那么返回null，表示使用ISO-8859-1编码；-%20`void%20setCharacterEncoding(String%20code)：`设置请求编码，只对请求体有效！注意，对于GET而言，没有请求体！！！所以此方法只能对POST请求中的参数有效！-%20`String%20getContextPath()：`返回上下文路径，例如：&#x2F;hello-%20`String%20getQueryString()：`返回请求URL中的参数，例如：name=zhangSan-%20`String%20getRequestURI()：`返回请求URI路径，例如：&#x2F;hello&#x2F;oneServlet-%20`StringBuffer%20getRequestURL()：`返回请求URL路径，例如：`http:&#x2F;&#x2F;localhost&#x2F;hello&#x2F;oneServlet`，即返回除了参数以外的路径信息；-%20`String%20getServletPath()：`返回Servlet路径，例如：&#x2F;oneServlet-%20`String%20getRemoteAddr()：`返回当前客户端的IP地址；-%20`String%20getRemoteHost()：`返回当前客户端的主机名，但这个方法的实现还是获取IP地址；-%20`String%20getScheme()：`返回请求协议，例如：http；-%20`String%20getServerName()：`返回主机名，例如：localhost-%20`int%20getServerPort()：`返回服务器端口号，例如：8080##%20%20request获取请求参数最为常见的客户端传递参数方式有两种：-%20浏览器地址栏直接输入：一定是GET请求；-%20超链接：一定是GET请求；-%20表单：可以是GET，也可以是POST，这取决与&lt;form&gt;的method属性值； ###%20%20GET请求和POST请求的区别**GET请求**-%20请求参数会在浏览器的地址栏中显示，所以不安全；-%20请求参数长度限制长度在1K之内；-%20GET请求没有请求体，无法通过request.setCharacterEncoding()来设置参数的编码；**POST请求**-%20请求参数不会显示浏览器的地址栏，相对安全；-%20请求参数长度没有限制；下面是使用request获取请求参数的API：-%20`String%20getParameter(String%20name)：`通过指定名称获取参数值；-%20`String[]%20getParameterValues(String%20name)：`当多个参数名称相同时，可以使用方法来获取；-%20`Enumeration%20getParameterNames()：`获取所有参数的名字；-%20`Map%20getParameterMap()：`获取所有参数封装到Map中，其中key为参数名，value为参数值，因为一个参数名称可能有多个值，所以参数值是String[]，而不是String。###%20%20请求转发和请求包含无论是请求转发还是请求包含，都表示由多个Servlet共同来处理一个请求。例如Servlet1来处理请求，然后Servlet1又转发给Servlet2来继续处理这个请求。请求转发和请求包含`RequestDispatcher%20rd%20=%20request.getRequestDispatcher(&quot;&#x2F;MyServlet&quot;);`%20使用`request`获取`RequestDispatcher`对象，方法的参数是被转发或包含的`Servlet`的`Servlet`路径-%20请求转发：`rd.forward(request,response)`;-%20请求包含：`rd.include(request,response)`;有时一个请求需要多个`Servlet`协作才能完成，所以需要在一个`Servlet`跳到另一个`Servlet`！-%20一个请求跨多个`Servlet`，需要使用转发和包含。-%20请求转发：由下一个`Servlet`完成响应体！当前`Servlet`可以设置响应头！（留头不留体）即当前`Servlet`设置的相应头有效，相应体无效。-%20请求包含：由两个`Servlet`共同未完成响应体！（留头又留体）都有效。%20-%20无论是请求转发还是请求包含，都在一个请求范围内！使用同一个`request`和`response`！###%20%20请求转发与请求包含比较1.%20如果在`AServlet`中请求转发到`BServlet`，那么在`AServlet`中就不允许再输出响应体，即不能再使用`response.getWriter()`和`response.getOutputStream()`向客户端输出，这一工作应该由`BServlet`来完成；如果是使用请求包含，那么没有这个限制；2.%20请求转发虽然不能输出响应体，但还是可以设置响应头的，例如：`response.setContentType(”text&#x2F;html;charset=utf-8”)`;3.%20请求包含大多是应用在JSP页面中，完成多页面的合并；4.%20请求转发大多是应用在`Servlet`中，转发目标大多是JSP页面；![图例](https:&#x2F;&#x2F;img-blog.csdn.net&#x2F;20160816102052342?watermark&#x2F;2&#x2F;text&#x2F;aHR0cDovL2Jsb2cuY3Nkbi5uZXQv&#x2F;font&#x2F;5a6L5L2T&#x2F;fontsize&#x2F;400&#x2F;fill&#x2F;I0JBQkFCMA==&#x2F;dissolve&#x2F;70&#x2F;gravity&#x2F;Center%20)###%20%20请求转发与重定向比较-%20请求转发是一个请求，而重定向是两个请求；-%20请求转发后浏览器地址栏不会有变化，而重定向会有变化，因为重定向是两个请求；-%20请求转发的目标只能是本应用中的资源，重定向的目标可以是其他应用；-%20请求转发对`AServlet`和`BServlet`的请求方法是相同的，即要么都是GET，要么都是POST，因为请求转发是一个请求；-%20重定向的第二个请求一定是GET；#%20%20response##%20%20什么是response？`response`是`Servlet.service`方法的一个参数，类型为`javax.servlet.http.HttpServletResponse`。在客户端发出每个请求时，服务器都会创建一个response对象，并传入给`Servlet.service()`方法。`response`对象是用来对客户端进行响应的，这说明在`service()`方法中使用`response`对象可以完成对客户端的响应工作。`response`对象的功能分为以下四种：（1）设置响应头信息（2）发送状态码（3）设置响应正文（4）重定向##%20%20response响应正文`response`是响应对象，向客户端输出响应正文（响应体）可以使用response的响应流，repsonse一共提供了两个响应流对象：-%20`PrintWriter%20out%20=%20response.getWriter()`：获取字符流；-%20`ServletOutputStreamout%20=%20response.getOutputStream()`：获取字节流； 当然，如果响应正文内容为字符，那么使用`response.getWriter()`，如果响应内容是字节，例如下载时，那么可以使用`response.getOutputStream()`。注意，在一个请求中，不能同时使用这两个流！也就是说，要么你使用`repsonse.getWriter()`，要么使用`response.getOutputStream()`，但不能同时使用这两个流。不然会抛出`illegalStateException`异常。###%20%20字符响应流####%20%20字符编码在使用`response.getWriter()`时需要注意默认字符编码为`ISO-8859-1`，如果希望设置字符流的字符编码为`utf-8`，可以使用`response.setCharaceterEncoding(&quot;utf-8&quot;)`来设置。这样可以保证输出给客户端的字符都是使用`UTF-8`编码的！但客户端浏览器并不知道响应数据是什么编码的！如果希望通知客户端使用`UTF-8`来解读响应数据，那么还是使用`response.setContentType(&quot;text&#x2F;html;charset=utf-8&quot;)`方法比较好，因为这个方法不只会调用`response.setCharaceterEncoding(&quot;utf-8&quot;)`，还会设置`content-type`响应头，客户端浏览器会使用`content-type`头来解读响应数据。 ####%20%20缓冲区`response.getWriter()`是`PrintWriter`类型，所以它有缓冲区，缓冲区的默认大小为8KB。也就是说，在响应数据没有输出8KB之前，数据都是存放在缓冲区中，而不会立刻发送到客户端。当`Servlet`执行结束后，服务器才会去刷新流，使缓冲区中的数据发送到客户端。如果希望响应数据马上发送给客户端：向流中写入大于8KB的数据；调用response.flushBuffer()方法来手动刷新缓冲区；##%20%20设置响应头信息可以使用`response`对象的`setHeader()`方法来设置响应头！使用该方法设置的响应头最终会发送给客户端浏览器！（1）`response.setHeader(&quot;content-type&quot;,%20&quot;text&#x2F;html;charset=utf-8&quot;)`：设置`content-type`响应头，该头的作用是告诉浏览器响应内容为html类型，编码为`utf-8`。而且同时会设置`response`的字符流编码为`utf-8`，即`response.setCharaceterEncoding(&quot;utf-8&quot;)`；（2）`response.setHeader(&quot;Refresh&quot;,&quot;5;%20URL=http:&#x2F;&#x2F;www.baidu.com&quot;)`：5秒后自动跳转到百度主页。##%20%20设置状态码及其他方法（1）`response.setContentType(&quot;text&#x2F;html;charset=utf-8&quot;)`：等同与调用`response.setHeader(&quot;content-type&quot;,%20&quot;text&#x2F;html;charset=utf-8&quot;)`；（2）`response.setCharacterEncoding(&quot;utf-8&quot;)`：设置字符响应流的字符编码为`utf-8`；（3）`response.setStatus(200)`：设置状态码；（4）`response.sendError(404,&quot;您要查找的资源不存在”)`：当发送错误状态码时，`Tomcat`会跳转到固定的错误页面去，但可以显示错误信息。##%20%205、重定向###%20%20什么是重定向（两次请求）当你访问`http:&#x2F;&#x2F;www.sun.com`时，你会发现浏览器地址栏中的URL会变成`http:&#x2F;&#x2F;www.Oracle.com&#x2F;us&#x2F;sun&#x2F;index.htm`，这就是重定向了。重定向是服务器通知浏览器去访问另一个地址，即再发出另一个请求。![重定向](https:&#x2F;&#x2F;img-blog.csdn.net&#x2F;20160816095908794?watermark&#x2F;2&#x2F;text&#x2F;aHR0cDovL2Jsb2cuY3Nkbi5uZXQv&#x2F;font&#x2F;5a6L5L2T&#x2F;fontsize&#x2F;400&#x2F;fill&#x2F;I0JBQkFCMA==&#x2F;dissolve&#x2F;70&#x2F;gravity&#x2F;Center%20)###%20%20如何完成重定向？重定向的状态码为302，我们首先使用response对象向浏览器发送302的状态码，之后再设置一个Location，即给出一个可用的URL，由浏览器去访问新的URL，实现重定向。举例：```java public class AServlet extends HttpServlet {      public void doGet(HttpServletRequest request, HttpServletResponse response)              throws ServletException, IOException {          response.setStatus(302);           response.setHeader(&quot;Location&quot;, &quot;http:&#x2F;&#x2F;www.baidu.com&quot;);       }  }  ```上面代码的作用是：当访问`AServlet`后，会通知浏览器重定向到百度主页。客户端浏览器解析到响应码为302后，就知道服务器让它重定向，所以它会马上获取响应头Location，然发出第二个请求。还有一种快捷的重定向方法，即使用`response.sendRedirect()`方法。比如上面例子中的两句可以使用`response.sendRedirect(&quot;http:&#x2F;&#x2F;www.baidu.com&quot;)`代替。#%20%20案例##%20%20用户登录案例需求1.%20编写login.html登录页面，包含username%20&amp;%20password%20两个输入框2.%20使用Druid数据库连接池技术,操作mysql，day14数据库中user表3.%20使用JdbcTemplate技术封装JDBC4.%20登录成功跳转到SuccessServlet展示：登录成功！用户名,欢迎您5.%20登录失败跳转到FailServlet展示：登录失败，用户名或密码错误##%20%20开发步骤1.%20创建项目，导入html页面，配置文件，jar包2.%20创建数据库环境```sql%20%20CREATE%20DATABASE%20userLogin;%20%20USE%20userLogin;%20%20CREATE%20TABLE%20USER(			id%20INT%20PRIMARY%20KEY%20AUTO_INCREMENT,	username%20VARCHAR(32)%20UNIQUE%20NOT%20NULL,	PASSWORD%20VARCHAR(32)%20NOT%20NULL	);%20%20```3.%20创建包cn.domain,创建类User```javapackage%20cn.domain;&#x2F;**%20*%20用户的实体类%20*&#x2F;public%20class%20User%20{%20%20%20%20private%20int%20id;%20%20%20%20private%20String%20username;%20%20%20%20private%20String%20password;%20%20%20%20public%20int%20getId()%20{%20%20%20%20%20%20%20%20return%20id;%20%20%20%20}%20%20%20%20public%20void%20setId(int%20id)%20{%20%20%20%20%20%20%20%20this.id%20=%20id;%20%20%20%20}%20%20%20%20public%20String%20getUsername()%20{%20%20%20%20%20%20%20%20return%20username;%20%20%20%20}%20%20%20%20public%20void%20setUsername(String%20username)%20{%20%20%20%20%20%20%20%20this.username%20=%20username;%20%20%20%20}%20%20%20%20public%20String%20getPassword()%20{%20%20%20%20%20%20%20%20return%20password;%20%20%20%20}%20%20%20%20public%20void%20setPassword(String%20password)%20{%20%20%20%20%20%20%20%20this.password%20=%20password;%20%20%20%20}%20%20%20%20@Override%20%20%20%20public%20String%20toString()%20{%20%20%20%20%20%20%20%20return%20&quot;User{&quot;%20+%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20&quot;id=&quot;%20+%20id%20+%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20&quot;,%20username=&#x27;&quot;%20+%20username%20+%20&#x27;&#x5C;&#x27;&#x27;%20+%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20&quot;,%20password=&#x27;&quot;%20+%20password%20+%20&#x27;&#x5C;&#x27;&#x27;%20+%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20&#x27;}&#x27;;%20%20%20%20}}```4.%20创建包cn.util,编写工具类JDBCUtils```javapackage%20cn.util;import%20com.alibaba.druid.pool.DruidDataSourceFactory;import%20javax.sql.DataSource;import%20javax.xml.crypto.Data;import%20java.io.IOException;import%20java.io.InputStream;import%20java.sql.Connection;import%20java.sql.SQLException;import%20java.util.Properties;&#x2F;**%20*%20JDBC工具类%20使用Durid连接池%20*&#x2F;public%20class%20JDBCUtils%20{%20%20%20%20private%20static%20DataSource%20ds%20;%20%20%20%20static%20{%20%20%20%20%20%20%20%20try%20{%20%20%20%20%20%20%20%20%20%20%20%20&#x2F;&#x2F;1.加载配置文件%20%20%20%20%20%20%20%20%20%20%20%20Properties%20pro%20=%20new%20Properties();%20%20%20%20%20%20%20%20%20%20%20%20&#x2F;&#x2F;使用ClassLoader加载配置文件，获取字节输入流%20%20%20%20%20%20%20%20%20%20%20%20InputStream%20is%20=%20JDBCUtils.class.getClassLoader().getResourceAsStream(&quot;druid.properties&quot;);%20%20%20%20%20%20%20%20%20%20%20%20pro.load(is);%20%20%20%20%20%20%20%20%20%20%20%20&#x2F;&#x2F;2.初始化连接池对象%20%20%20%20%20%20%20%20%20%20%20%20ds%20=%20DruidDataSourceFactory.createDataSource(pro);%20%20%20%20%20%20%20%20}%20catch%20(IOException%20e)%20{%20%20%20%20%20%20%20%20%20%20%20%20e.printStackTrace();%20%20%20%20%20%20%20%20}%20catch%20(Exception%20e)%20{%20%20%20%20%20%20%20%20%20%20%20%20e.printStackTrace();%20%20%20%20%20%20%20%20}%20%20%20%20}%20%20%20%20&#x2F;**%20%20%20%20%20*%20获取连接池对象%20%20%20%20%20*&#x2F;%20%20%20%20public%20static%20DataSource%20getDataSource(){%20%20%20%20%20%20%20%20return%20ds;%20%20%20%20}%20%20%20%20&#x2F;**%20%20%20%20%20*%20获取连接Connection对象%20%20%20%20%20*&#x2F;%20%20%20%20public%20static%20Connection%20getConnection()%20throws%20SQLException%20{%20%20%20%20%20%20%20%20return%20%20ds.getConnection();%20%20%20%20}}```5.%20创建包cn.dao,创建类UserDao,提供login方法```java			package%20cn.dao;import%20cn.domain.User;import%20cn.util.JDBCUtils;import%20org.springframework.dao.DataAccessException;import%20org.springframework.jdbc.core.BeanPropertyRowMapper;import%20org.springframework.jdbc.core.JdbcTemplate;&#x2F;**%20*%20操作数据库中User表的类%20*&#x2F;public%20class%20UserDao%20{%20%20%20%20&#x2F;&#x2F;声明JDBCTemplate对象共用%20%20%20%20private%20JdbcTemplate%20template%20=%20new%20JdbcTemplate(JDBCUtils.getDataSource());%20%20%20%20&#x2F;**%20%20%20%20%20*%20登录方法%20%20%20%20%20*%20@param%20loginUser%20只有用户名和密码%20%20%20%20%20*%20@return%20user包含用户全部数据,没有查询到，返回null%20%20%20%20%20*&#x2F;%20%20%20%20public%20User%20login(User%20loginUser){%20%20%20%20%20%20%20%20try%20{%20%20%20%20%20%20%20%20%20%20%20%20&#x2F;&#x2F;1.编写sql%20%20%20%20%20%20%20%20%20%20%20%20String%20sql%20=%20&quot;select%20*%20from%20user%20where%20username%20=%20?%20and%20password%20=%20?&quot;;%20%20%20%20%20%20%20%20%20%20%20%20&#x2F;&#x2F;2.调用query方法%20%20%20%20%20%20%20%20%20%20%20%20User%20user%20=%20template.queryForObject(sql,%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20new%20BeanPropertyRowMapper&lt;User&gt;(User.class),%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20loginUser.getUsername(),%20loginUser.getPassword());%20%20%20%20%20%20%20%20%20%20%20%20return%20user;%20%20%20%20%20%20%20%20}%20catch%20(DataAccessException%20e)%20{%20%20%20%20%20%20%20%20%20%20%20%20e.printStackTrace();&#x2F;&#x2F;记录日志%20%20%20%20%20%20%20%20%20%20%20%20return%20null;%20%20%20%20%20%20%20%20}%20%20%20%20}}```6.%20编写cn.web.servlet.LoginServlet类```javapackage%20cn.web.servlet;import%20cn.dao.UserDao;import%20cn.domain.User;import%20javax.servlet.ServletException;import%20javax.servlet.annotation.WebServlet;import%20javax.servlet.http.HttpServlet;import%20javax.servlet.http.HttpServletRequest;import%20javax.servlet.http.HttpServletResponse;import%20java.io.IOException;@WebServlet(&quot;&#x2F;loginServlet&quot;)public%20class%20LoginServlet%20extends%20HttpServlet%20{%20%20%20%20@Override%20%20%20%20protected%20void%20doGet(HttpServletRequest%20req,%20HttpServletResponse%20resp)%20throws%20ServletException,%20IOException%20{%20%20%20%20%20%20%20%20&#x2F;&#x2F;1.设置编码%20%20%20%20%20%20%20%20req.setCharacterEncoding(&quot;utf-8&quot;);%20%20%20%20%20%20%20%20&#x2F;&#x2F;2.获取请求参数%20%20%20%20%20%20%20%20String%20username%20=%20req.getParameter(&quot;username&quot;);%20%20%20%20%20%20%20%20String%20password%20=%20req.getParameter(&quot;password&quot;);%20%20%20%20%20%20%20%20&#x2F;&#x2F;3.封装user对象%20%20%20%20%20%20%20%20User%20loginUser%20=%20new%20User();%20%20%20%20%20%20%20%20loginUser.setUsername(username);%20%20%20%20%20%20%20%20loginUser.setPassword(password);%20%20%20%20%20%20%20%20&#x2F;&#x2F;4.调用UserDao的login方法%20%20%20%20%20%20%20%20UserDao%20dao%20=%20new%20UserDao();%20%20%20%20%20%20%20%20User%20user%20=%20dao.login(loginUser);%20%20%20%20%20%20%20%20&#x2F;&#x2F;5.判断user%20%20%20%20%20%20%20%20if(user%20==%20null){%20%20%20%20%20%20%20%20%20%20%20%20&#x2F;&#x2F;登录失败%20%20%20%20%20%20%20%20%20%20%20%20req.getRequestDispatcher(&quot;&#x2F;failServlet&quot;).forward(req,resp);%20%20%20%20%20%20%20%20}else{%20%20%20%20%20%20%20%20%20%20%20%20&#x2F;&#x2F;登录成功%20%20%20%20%20%20%20%20%20%20%20%20&#x2F;&#x2F;存储数据%20%20%20%20%20%20%20%20%20%20%20%20req.setAttribute(&quot;user&quot;,user);%20%20%20%20%20%20%20%20%20%20%20%20&#x2F;&#x2F;转发%20%20%20%20%20%20%20%20%20%20%20%20req.getRequestDispatcher(&quot;&#x2F;successServlet&quot;).forward(req,resp);%20%20%20%20%20%20%20%20}%20%20%20%20}%20%20%20%20@Override%20%20%20%20protected%20void%20doPost(HttpServletRequest%20req,%20HttpServletResponse%20resp)%20throws%20ServletException,%20IOException%20{%20%20%20%20%20%20%20%20this.doGet(req,resp);%20%20%20%20}}```7.%20编写FailServlet和SuccessServlet类```java@WebServlet(&quot;&#x2F;successServlet&quot;)public%20class%20SuccessServlet%20extends%20HttpServlet%20{%20%20%20%20protected%20void%20doPost(HttpServletRequest%20request,%20HttpServletResponse%20response)%20throws%20ServletException,%20IOException%20{%20%20%20%20%20%20%20%20&#x2F;&#x2F;获取request域中共享的user对象%20%20%20%20%20%20%20%20User%20user%20=%20(User)%20request.getAttribute(&quot;user&quot;);%20%20%20%20%20%20%20%20if(user%20!=%20null){%20%20%20%20%20%20%20%20%20%20%20%20&#x2F;&#x2F;给页面写一句话%20%20%20%20%20%20%20%20%20%20%20%20&#x2F;&#x2F;设置编码%20%20%20%20%20%20%20%20%20%20%20%20response.setContentType(&quot;text&#x2F;html;charset=utf-8&quot;);%20%20%20%20%20%20%20%20%20%20%20%20&#x2F;&#x2F;输出%20%20%20%20%20%20%20%20%20%20%20%20response.getWriter().write(&quot;登录成功！&quot;+user.getUsername()+&quot;,欢迎您&quot;);%20%20%20%20%20%20%20%20}%20%20%20%20}		@WebServlet(&quot;&#x2F;failServlet&quot;)public%20class%20FailServlet%20extends%20HttpServlet%20{%20%20%20%20protected%20void%20doPost(HttpServletRequest%20request,%20HttpServletResponse%20response)%20throws%20ServletException,%20IOException%20{%20%20%20%20%20%20%20%20&#x2F;&#x2F;给页面写一句话%20%20%20%20%20%20%20%20&#x2F;&#x2F;设置编码%20%20%20%20%20%20%20%20response.setContentType(&quot;text&#x2F;html;charset=utf-8&quot;);%20%20%20%20%20%20%20%20&#x2F;&#x2F;输出%20%20%20%20%20%20%20%20response.getWriter().write(&quot;登录失败，用户名或密码错误&quot;);%20%20%20%20}%20%20%20%20protected%20void%20doGet(HttpServletRequest%20request,%20HttpServletResponse%20response)%20throws%20ServletException,%20IOException%20{%20%20%20%20%20%20%20%20this.doPost(request,response);%20%20%20%20}}```注意：BeanUtils工具类，用于封装JavaBean的简化数据封装1.%20类必须被public修饰2.%20必须提供空参的构造器3.%20成员变量必须使用private修饰4.%20提供公共setter和getter方法%20%20#%20%20Cookie和Session会话（Session）跟踪是Web程序中常用的技术，用来跟踪用户的整个会话。常用的会话跟踪技术是Cookie与Session。Cookie通过在客户端记录信息确定用户身份，Session通过在服务器端记录信息确定用户身份。##%20%20Cookie在程序中，会话跟踪是很重要的事情。理论上，一个用户的所有请求操作都应该属于同一个会话，而另一个用户的所有请求操作则应该属于另一个会话，二者不能混淆。例如，用户A在超市购买的任何商品都应该放在A的购物车内，不论是用户A什么时间购买的，这都是属于同一个会话的，不能放入用户B或用户C的购物车内，这不属于同一个会话。而Web应用程序是使用HTTP协议传输数据的。HTTP协议是无状态的协议。一旦数据交换完毕，客户端与服务器端的连接就会关闭，再次交换数据需要建立新的连接。这就意味着服务器无法从连接上跟踪会话。即用户A购买了一件商品放入购物车内，当再次购买商品时服务器已经无法判断该购买行为是属于用户A的会话还是用户B的会话了。要跟踪该会话，必须引入一种机制。为了做到这点，就需要使用到Cookie了。服务器可以设置或读取Cookies中包含信息，借此维护用户跟服务器会话中的状态Cookie就是这样的一种机制。它可以弥补HTTP协议无状态的不足。在Session出现之前，基本上所有的网站都采用Cookie来跟踪会话。###%20%20什么是CookieCookie意为&quot;甜饼&quot;，是由W3C组织提出，最早由Netscape社区发展的一种机制。目前Cookie已经成为标准，所有的主流浏览器如IE、Chrome、Firefox、Opera等都支持Cookie。由于HTTP是一种无状态的协议，服务器单从网络连接上无从知道客户身份。服务端会给客户端们颁发一个通行证，客户端访问都必须携带自己通行证。这样服务器就能从通行证上确认客户身份了。这就是Cookie的工作原理。Cookie实际上是一小段的文本信息。客户端请求服务器，如果服务器需要记录该用户状态，就使用response向客户端浏览器颁发一个Cookie。客户端浏览器会把Cookie保存起来。当浏览器再请求该网站时，浏览器把请求的网址连同该Cookie一同提交给服务器。服务器检查该Cookie，以此来辨认用户状态。服务器还可以根据需要修改Cookie的内容。![示意图](http:&#x2F;&#x2F;hi.csdn.net&#x2F;attachment&#x2F;201111&#x2F;9&#x2F;0_13208318702UfF.gif%20)查看某个网站颁发的Cookie很简单。在浏览器地址栏输入`javascript:alert%20(document.%20cookie)`就可以了（需要有网才能查看）。JavaScript脚本会弹出一个对话框显示本网站颁发的所有Cookie的内容，如图![示例](https:&#x2F;&#x2F;imagerepos.oss-cn-beijing.aliyuncs.com&#x2F;images&#x2F;WX20191030-102212@2x.png%20)**注意:Cookie功能需要浏览器的支持。**如果浏览器不支持Cookie（如大部分手机中的浏览器）或者把Cookie禁用了，Cookie功能就会失效。###%20%20记录用户访问次数`Java`中把Cookie封装成了`javax.servlet.http.Cookie`类。每个`Cookie`都是该`Cookie`类的对象。服务器通过操作Cookie类对象对客户端Cookie进行操作。通过`request.getCookie()`获取客户端提交的所有Cookie（以Cookie[]数组形式返回），通过`response.addCookie(Cookiecookie)`向客户端设置`Cookie`。`Cookie`对象使用`key-value`属性对的形式保存用户状态，一个`Cookie`对象保存一个属性对，一个`request`或者`response`同时使用多个`Cookie`。因为`Cookie`类位于包`javax.servlet.http.*`下面，所以JSP中不需要`import`该类。###%20%20Cookie的不可跨域名性很多网站都会使用`Cookie`。例如，Google会向客户端颁发Cookie，Baidu也会向客户端颁发Cookie。但双方是无法相互读取及修改的。`Cookie`具有不可跨域名性。根据`Cookie`规范，浏览器访问`Google`只会携带`Google`的`Cookie`，而不会携带`Baidu`的`Cookie`。`Google`也只能操作`Google`的`Cookie`，而不能操作`Baidu`的`Cookie`。`Cookie`在客户端是由浏览器来管理的。浏览器能够保证`Google`只会操作`Google`的`Cookie`而不会操作`Baidu`的`Cookie`，从而保证用户的隐私安全。浏览器判断一个网站是否能操作另一个网站`Cookie`的依据是域名。`Google`与`Baidu`的域名不一样，因此`Google`不能操作`Baidu`的`Cookie`。需要注意的是，虽然网站`images.google.com`与网站`www.google.com`同属于`Google`，但是域名不一样，二者同样不能互相操作彼此的Cookie。需要注意的是用户登录网站`www.google.com`之后会发现访问`images.google.com`时登录信息仍然有效，而普通的`Cookie`是做不到的。这是因为`Google`做了特殊处理。###%20%20Unicode编码：保存中文中文与英文字符不同，中文属于`Unicode字符`，在内存中占4个字符，而英文属于`ASCII字符`，内存中只占2个字节。`Cookie`中使用`Unicode字符`时需要对`Unicode字符进行编码`，否则会乱码。注意`Cookie`中保存中文只能编码。一般使用`UTF-8`编码即可。不推荐使用`GBK`等中文编码，因为浏览器不一定支持，而且`JavaScript`也不支持`GBK`编码。###%20%20BASE64编码：保存二进制图片`Cookie`不仅可以使用`ASCII`字符与`Unicode`字符，还可以使用二进制数据。例如在`Cookie`中使用数字证书，提供安全度。使用二进制数据时也需要进行编码。`Cookie`中可以存储二进制内容，并不实用。由于浏览器每次请求服务器都会携带`Cookie`，因此`Cookie`内容不宜过多，否则影响速度。###%20%20设置Cookie的所有属性除了name与value之外，Cookie还具有其他几个常用的属性。每个属性对应一个getter方法与一个setter方法。Cookie类的所有属性如表1.1所示。|%20属性名%20|%20描述%20||%20---%20%20|%20---%20||`String%20name`|%20该`Cookie`的名称。`Cookie`一旦创建，名称便不可更改%20||%20`Object%20value`%20|%20该`Cookie`的值。如果值为`Unicode`字符，需要为字符编码。如果值为二进制数据，则需要使用`BASE64`编码%20||%20`int%20maxAge`%20|%20该`Cookie`失效的时间，单位秒。如果为正数，则该`Cookie`在`maxAge`秒之后失效。如果为负数，该`Cookie`为临时`Cookie`，关闭浏览器即失效，浏览器也不会以任何形式保存该`Cookie`。如果为0，表示删除该`Cookie`。默认为–1||%20`boolean%20secure`%20|%20该`Cookie`是否仅被使用安全协议传输。安全协议。安全协议有HTTPS，SSL等，在网络上传输数据之前先将数据加密。默认为`false`|%20|%20`String%20path`%20|%20该`Cookie`的使用路径。如果设置为`“&#x2F;sessionWeb&#x2F;”`，则只有`contextPath`为`“&#x2F;sessionWeb”`的程序可以访问该`Cookie`。如果设置为`“&#x2F;”`，则本域名下`contextPath`都可以访问该`Cookie`。注意最后一个字符必须为`“&#x2F;”`||%20`String%20domain`%20|%20可以访问该`Cookie`的域名。如果设置为`“.google.com”`，则所有以`“google.com”`结尾的域名都可以访问该`Cookie`。注意第一个字符必须为`“.”`|%20|%20`String%20comment`|%20该`Cookie`的用处说明。浏览器显示`Cookie`信息的时候显示该说明%20||%20`int%20version`|%20该`Cookie`使用的版本号。0表示遵循`Netscape`的`Cookie`规范，1表示遵循W3C的RFC%202109规范|%20###%20%20Cookie的有效期Cookie的maxAge决定着Cookie的有效期，单位为秒（Second）。Cookie中通过getMaxAge()方法与setMaxAge(int%20maxAge)方法来读写maxAge属性。如果maxAge属性为正数，则表示该Cookie会在maxAge秒之后自动失效。浏览器会将maxAge为正数的Cookie持久化，即写到对应的Cookie文件中。无论客户关闭了浏览器还是电脑，只要还在maxAge秒之前，登录网站时该Cookie仍然有效。下面代码中的Cookie信息将永远有效。```javaCookie%20cookie%20=%20new%20Cookie(&quot;username&quot;,&quot;hello&quot;);  %20&#x2F;&#x2F;%20新建Cookiecookie.setMaxAge(Integer.MAX_VALUE); &#x2F;&#x2F;%20设置生命周期为MAX_VALUEresponse.addCookie(cookie);%20&#x2F;&#x2F;%20输出到客户端```如果maxAge为负数，则表示该Cookie仅在本浏览器窗口以及本窗口打开的子窗口内有效，关闭窗口后该Cookie即失效。maxAge为负数的Cookie，为临时性Cookie，不会被持久化，不会被写到Cookie文件中。Cookie信息保存在浏览器内存中，因此关闭浏览器该Cookie就消失了。Cookie默认的maxAge值为–1。如果maxAge为0，则表示删除该Cookie。Cookie机制没有提供删除Cookie的方法，因此通过设置该Cookie即时失效实现删除Cookie的效果。失效的Cookie会被浏览器从Cookie文件或者内存中删除，例如：```javaCookie%20cookie%20=%20new%20Cookie(&quot;username&quot;,&quot;helloweenvsfei&quot;);  %20&#x2F;&#x2F;%20新建Cookiecookie.setMaxAge(0);  &#x2F;&#x2F;%20设置生命周期为0，不能为负数response.addCookie(cookie);%20&#x2F;&#x2F;%20必须执行这一句```response对象提供的Cookie操作方法只有一个添加操作add(Cookie%20cookie)。要想修改Cookie只能使用一个同名的Cookie来覆盖原来的Cookie，达到修改的目的。删除时只需要把maxAge修改为0即可。注意：从客户端读取Cookie时，包括maxAge在内的其他属性都是不可读的，也不会被提交。浏览器提交Cookie时只会提交name与value属性。maxAge属性只被浏览器用来判断Cookie是否过期。###%20%20Cookie的修改、删除Cookie并不提供修改、删除操作。如果要修改某个Cookie，只需要新建一个同名的Cookie，添加到response中覆盖原来的Cookie。如果要删除某个Cookie，只需要新建一个同名的Cookie，并将maxAge设置为0，并添加到response中覆盖原来的Cookie。注意是0而不是负数。负数代表其他的意义。读者可以通过上例的程序进行验证，设置不同的属性。修改、删除Cookie时，新建的Cookie除value、maxAge之外的所有属性，例如name、path、domain等，都要与原Cookie完全一样。否则，浏览器将视为两个不同的Cookie不予覆盖，导致修改、删除失败。###%20%20Cookie的域名Cookie是不可跨域名的。域名`www.google.com`颁发的Cookie不会被提交到域名`www.baidu.com`去。这是由Cookie的隐私安全机制决定的。隐私安全机制能够禁止网站非法获取其他网站的Cookie。正常情况下，同一个一级域名下的两个二级域名如`www.google.com`和`images.google.com`%20`google.com`名下的二级域名都可以使用该Cookie，需要设置Cookie的domain参数，例如：```javaCookie%20cookie%20=%20new%20Cookie(&quot;time&quot;,&quot;20190808&quot;);%20&#x2F;&#x2F;%20新建Cookiecookie.setDomain(&quot;.google.com&quot;);      %20   %20&#x2F;&#x2F;%20设置域名cookie.setPath(&quot;&#x2F;&quot;);      %20   %20   %20      %20   %20   %20&#x2F;&#x2F;%20设置路径cookie.setMaxAge(Integer.MAX_VALUE);      %20   %20   %20&#x2F;&#x2F;%20设置有效期response.addCookie(cookie);%20      %20   %20   %20      %20&#x2F;&#x2F;%20输出到客户端```注意：domain参数必须以点(&quot;.&quot;)开始。另外，name相同但domain不同的两个Cookie是两个不同的Cookie。如果想要两个域名完全不同的网站共有Cookie，可以生成两个Cookie，domain属性分别为两个域名，输出到客户端。###%20%20Cookie的路径domain属性决定运行访问Cookie的域名，而path属性决定允许访问Cookie的路径（ContextPath）。例如，如果只允许&#x2F;sessionWeb&#x2F;下的程序使用Cookie，可以这么写：```javaCookie%20cookie%20=%20new%20Cookie(&quot;time&quot;,&quot;20080808&quot;);%20 &#x2F;&#x2F;%20新建Cookiecookie.setPath(&quot;&#x2F;session&#x2F;&quot;);  &#x2F;&#x2F;%20设置路径response.addCookie(cookie);%20%20&#x2F;&#x2F;%20输出到客户端```设置为“&#x2F;”时允许所有路径使用Cookie。path属性需要使用符号“&#x2F;”结尾。name相同但domain相同的两个Cookie也是两个不同的Cookie。注意：页面只能获取它属于的Path的Cookie。例如&#x2F;session&#x2F;test&#x2F;a.jsp不能获取到路径为&#x2F;session&#x2F;abc&#x2F;的Cookie。使用时一定要注意。###%20%20Cookie的安全属性HTTP协议不仅是无状态的，而且是不安全的。使用HTTP协议的数据不经过任何加密就直接在网络上传播，有被截获的可能。使用HTTP协议传输很机密的内容是一种隐患。如果不希望Cookie在HTTP等非安全协议中传输，可以设置Cookie的secure属性为true。浏览器只会在HTTPS和SSL等安全协议中传输此类Cookie。下面的代码设置secure属性为true：```javaCookie%20cookie%20=%20new%20Cookie(&quot;time&quot;,%20&quot;20190808&quot;);%20&#x2F;&#x2F;%20新建Cookiecookie.setSecure(true);%20 &#x2F;&#x2F;%20设置安全属性response.addCookie(cookie);%20 &#x2F;&#x2F;%20输出到客户端```secure属性并不能对Cookie内容加密，因而不能保证绝对的安全性。如果需要高安全性，需要在程序中对Cookie内容加密、解密，以防泄密。###%20%20avaScript操作CookieCookie是保存在浏览器端的，因此浏览器具有操作Cookie的先决条件。浏览器可以使用脚本程序如JavaScript或者VBScript等操作Cookie。这里以JavaScript为例介绍常用的Cookie操作。例如下面的代码会输出本页面所有的Cookie。```js&lt;script&gt;document.write(document.cookie);&lt;&#x2F;script&gt;```由于JavaScript能够任意地读写Cookie，有些好事者便想使用JavaScript程序去窥探用户在其他网站的Cookie。不过这是徒劳的，W3C组织早就意识到JavaScript对Cookie的读写所带来的安全隐患并加以防备了，W3C标准的浏览器会阻止JavaScript读写任何不属于自己网站的Cookie。换句话说，A网站的JavaScript程序读写B网站的Cookie不会有任何结果。###%20%20案例：永久登录如果用户是在自己家的电脑上上网，登录时就可以记住他的登录信息，下次访问时不需要再次登录，直接访问即可。实现方法是把登录信息如账号、密码等保存在Cookie中，并控制Cookie的有效期，下次访问时再验证Cookie中的登录信息即可。保存登录信息有多种方案。最直接的是把用户名与密码都保持到Cookie中，下次访问时检查Cookie中的用户名与密码，与数据库比较。这是一种比较危险的选择，一般不把密码等重要信息保存到Cookie中。还有一种方案是把密码加密后保存到Cookie中，下次访问时解密并与数据库比较。这种方案略微安全一些。如果不希望保存密码，还可以把登录的时间戳保存到Cookie与数据库中，到时只验证用户名与登录时间戳就可以了。这几种方案验证账号时都要查询数据库。本例将采用另一种方案，只在登录时查询一次数据库，以后访问验证登录信息时不再查询数据库。实现方式是把账号按照一定的规则加密后，连同账号一块保存到Cookie中。下次访问时只需要判断账号的加密规则是否正确即可。本例把账号保存到名为account的Cookie中，把账号连同密钥用MD1算法加密后保存到名为ssid的Cookie中。验证时验证Cookie中的账号与密钥加密后是否与Cookie中的ssid相等。相关代码如下：```java&#x2F;&#x2F;代码1.8 loginCookie.jsp&lt;%@%20page%20language=&quot;java&quot;pageEncoding=&quot;UTF-8&quot;%20isErrorPage=&quot;false&quot;%20%&gt;&lt;%!%20   %20      %20   %20   %20      %20   %20   %20      %20   %20   %20&#x2F;&#x2F;%20JSP方法   %20private%20static%20final%20String%20KEY%20=&quot;:cookie@helloweenvsfei.com&quot;;   %20   %20   %20      %20   %20   %20      %20   %20   %20      %20   %20&#x2F;&#x2F;%20密钥    %20public%20final%20static%20String%20calcMD1(Stringss)%20{%20&#x2F;&#x2F;%20MD1%20加密算法   %20  %20String%20s%20=%20ss==null%20?&quot;&quot;%20:%20ss;  %20   %20      %20   %20&#x2F;&#x2F;%20若为null返回空   %20  %20char%20hexDigits[]%20=%20{%20&#x27;0&#x27;,&#x27;1&#x27;,%20&#x27;2&#x27;,%20&#x27;3&#x27;,%20&#x27;4&#x27;,%20&#x27;1&#x27;,%20&#x27;6&#x27;,%20&#x27;7&#x27;,%20&#x27;8&#x27;,%20&#x27;9&#x27;,   %20  %20&#x27;a&#x27;,%20&#x27;b&#x27;,%20&#x27;c&#x27;,%20&#x27;d&#x27;,%20&#x27;e&#x27;,%20&#x27;f&#x27;%20};    %20   %20   %20      %20   %20&#x2F;&#x2F;%20字典   %20  %20try%20{   %20   %20byte[]%20strTemp%20=s.getBytes();  %20   %20      %20   %20   %20   %20&#x2F;&#x2F;%20获取字节   %20   %20MessageDigestmdTemp%20=%20MessageDigest.getInstance(&quot;MD1&quot;);%20&#x2F;&#x2F;%20获取MD1   %20   mdTemp.update(strTemp); %20   %20      %20   %20   %20      %20   %20&#x2F;&#x2F;%20更新数据   %20   %20byte[]%20md%20=mdTemp.digest();%20   %20   %20      %20   %20   %20&#x2F;&#x2F;%20加密   %20   %20int%20j%20=md.length;  %20   %20   %20      %20   %20   %20      %20&#x2F;&#x2F;%20加密后的长度   %20   %20char%20str[]%20=%20newchar[j%20*%202];   %20   %20      %20   %20   %20&#x2F;&#x2F;%20新字符串数组   %20   %20int%20k%20=0;  %20   %20   %20      %20   %20   %20      %20   %20   %20&#x2F;&#x2F;%20计数器k   %20   %20for%20(int%20i%20=%200;%20i&lt;%20j;%20i++)%20{   %20   %20      %20   %20   %20&#x2F;&#x2F;%20循环输出   %20    %20byte%20byte0%20=md[i];   %20    %20str[k++]%20=hexDigits[byte0%20&gt;&gt;&gt;%204%20&amp;%200xf];   %20    %20str[k++]%20=hexDigits[byte0%20&amp;%200xf];   %20   %20}   %20   %20return%20newString(str); %20   %20   %20      %20   %20   %20   %20&#x2F;&#x2F;%20加密后字符串   %20  %20}%20catch%20(Exception%20e){return%20null;%20}   %20}%&gt;&lt;%   request.setCharacterEncoding(&quot;UTF-8&quot;); %20      %20   %20&#x2F;&#x2F;%20设置request编码   %20response.setCharacterEncoding(&quot;UTF-8&quot;);   %20   %20&#x2F;&#x2F;%20设置response编码      %20String%20action%20=request.getParameter(&quot;action&quot;);%20&#x2F;&#x2F;%20获取action参数      %20if(&quot;login&quot;.equals(action)){   %20   %20   %20      %20   %20&#x2F;&#x2F;%20如果为login动作   %20   %20String%20account%20=request.getParameter(&quot;account&quot;);   %20   %20   %20      %20   %20   %20      %20   %20   %20      %20   %20&#x2F;&#x2F;%20获取account参数   %20   %20String%20password%20=request.getParameter(&quot;password&quot;);   %20   %20   %20      %20   %20   %20      %20   %20   %20      %20   %20&#x2F;&#x2F;%20获取password参数   %20   %20int%20timeout%20=%20newInteger(request.getParameter(&quot;timeout&quot;));   %20   %20   %20      %20   %20   %20      %20   %20   %20      %20   %20&#x2F;&#x2F;%20获取timeout参数   %20   %20         %20   %20String%20ssid%20=calcMD1(account%20+%20KEY);%20&#x2F;&#x2F;%20把账号、密钥使用MD1加密后保存   %20      %20   %20CookieaccountCookie%20=%20new%20Cookie(&quot;account&quot;,%20account);   %20   %20   %20   %20      %20   %20   %20      %20   %20   %20      %20&#x2F;&#x2F;%20新建Cookie   %20   accountCookie.setMaxAge(timeout);  %20      %20   %20&#x2F;&#x2F;%20设置有效期   %20      %20   %20Cookie%20ssidCookie%20=new%20Cookie(&quot;ssid&quot;,%20ssid);  %20&#x2F;&#x2F;%20新建Cookie   %20   ssidCookie.setMaxAge(timeout); %20   %20      %20   %20&#x2F;&#x2F;%20设置有效期   %20      %20   response.addCookie(accountCookie); %20   %20      %20&#x2F;&#x2F;%20输出到客户端   %20   response.addCookie(ssidCookie);%20   %20      %20&#x2F;&#x2F;%20输出到客户端   %20      %20   %20&#x2F;&#x2F;%20重新请求本页面，参数中带有时间戳，禁止浏览器缓存页面内容   %20   response.sendRedirect(request.getRequestURI()%20+%20&quot;?&quot;%20+%20System.   %20   %20currentTimeMillis());   %20   %20return;   %20}   %20elseif(&quot;logout&quot;.equals(action)){  %20      %20   %20   %20&#x2F;&#x2F;%20如果为logout动作   %20      %20   %20CookieaccountCookie%20=%20new%20Cookie(&quot;account&quot;,%20&quot;&quot;);   %20   %20   %20      %20   %20   %20      %20   %20   %20      %20&#x2F;&#x2F;%20新建Cookie，内容为空   %20   accountCookie.setMaxAge(0);%20   %20      %20   %20&#x2F;&#x2F;%20设置有效期为0，删除   %20   %20         %20   %20Cookie%20ssidCookie%20=new%20Cookie(&quot;ssid&quot;,%20&quot;&quot;);%20&#x2F;&#x2F;%20新建Cookie，内容为空   %20   ssidCookie.setMaxAge(0);   %20      %20   %20   %20&#x2F;&#x2F;%20设置有效期为0，删除   %20   response.addCookie(accountCookie); %20   %20   &#x2F;&#x2F;%20输出到客户端   %20   response.addCookie(ssidCookie);%20   %20   %20&#x2F;&#x2F;%20输出到客户端   %20   %20&#x2F;&#x2F;重新请求本页面，参数中带有时间戳，禁止浏览器缓存页面内容   %20   response.sendRedirect(request.getRequestURI()%20+%20&quot;?&quot;%20+%20System.   %20   %20currentTimeMillis());   %20   %20return;   %20}   %20boolean%20login%20=%20false;    %20   %20   %20      %20   %20&#x2F;&#x2F;%20是否登录   %20String%20account%20=%20null;    %20   %20   %20      %20   %20&#x2F;&#x2F;%20账号   %20String%20ssid%20=%20null;%20      %20   %20   %20      %20   %20&#x2F;&#x2F;%20SSID标识      %20if(request.getCookies()%20!=null){  %20   %20   %20   %20&#x2F;&#x2F;%20如果Cookie不为空   %20   %20for(Cookie%20cookie%20:request.getCookies()){ %20&#x2F;&#x2F;%20遍历Cookie   %20   %20   if(cookie.getName().equals(&quot;account&quot;)) %20&#x2F;&#x2F;%20如果Cookie名为   %20   %20   %20      %20   %20   %20      %20   %20   %20      %20  %20account   %20   %20      %20account%20=%20cookie.getValue();      %20&#x2F;&#x2F;%20保存account内容   %20   %20   if(cookie.getName().equals(&quot;ssid&quot;))%20&#x2F;&#x2F;%20如果为SSID   %20   %20      %20ssid%20=%20cookie.getValue();  %20      %20&#x2F;&#x2F;%20保存SSID内容   %20   %20}   %20}   %20if(account%20!=%20null%20&amp;&amp;%20ssid%20!=null){   %20&#x2F;&#x2F;%20如果account、SSID都不为空   %20   %20login%20=ssid.equals(calcMD1(account%20+%20KEY));   %20   %20   %20      %20   %20   %20      %20   %20&#x2F;&#x2F;%20如果加密规则正确,%20则视为已经登录   %20}%&gt;&lt;!DOCTYPE%20HTML%20PUBLIC%20&quot;-&#x2F;&#x2F;W3C&#x2F;&#x2F;DTD%20HTML%204.01Transitional&#x2F;&#x2F;EN&quot;&gt;   %20   &lt;legend&gt;&lt;%=%20login%20?%20&quot;欢迎您回来&quot;%20:%20&quot;请先登录&quot;%&gt;&lt;&#x2F;legend&gt;   %20   %20&lt;%%20if(login){%&gt;   %20   %20   %20欢迎您,"/>{ cookie.account.value }. &nbsp;&nbsp;
  
           <a href="<img src="https://latex.codecogs.com/gif.latex?{%20pageContext.request.requestURI%20}?action=logout&quot;&gt;   %20   %20   %20注销&lt;&#x2F;a&gt;   %20   %20&lt;%%20}%20else%20{%&gt;   %20   %20&lt;formaction=&quot;"/>{ pageContext.request.requestURI }?action=login"
        method="post">
  
           <table>
  
               <tr><td>账号： </td>
  
                   <td><input type="text"name="account" style="width:
                   200px; "></td>
  
               </tr>
  
               <tr><td>密码： </td>
  
                   <td><inputtype="password" name="password"></td>
  
               </tr>
  
               <tr>
  
                   <td>有效期： </td>
  
                   <td><inputtype="radio" name="timeout" value="-1"
                   checked> 关闭浏览器即失效 <br/> <input type="radio"
                   name="timeout" value="<%= 30 *24 * 60 * 60 %>"> 30天
                   内有效 <br/><input type="radio" name="timeout" value=
                   "<%= Integer.MAX_VALUE %>"> 永久有效 <br/> </td> </tr>
  
               <tr><td></td>
  
                   <td><input type="submit"value=" 登  录 " class=
                   "button"></td>
  
               </tr>
  
           </table>
  
        </form>
  
        <% } %>
```
  
登录时可以选择登录信息的有效期：关闭浏览器即失效、30天内有效与永久有效。
  
提示：该加密机制中最重要的部分为算法与密钥。由于MD1算法的不可逆性，即使用户知道了账号与加密后的字符串，也不可能解密得到密钥。因此，只要保管好密钥与算法，该机制就是安全的。
  
##  Session
  
  
除了使用Cookie，Web应用程序中还经常使用Session来记录客户端状态。Session是服务器端使用的一种记录客户端状态的机制，使用上比Cookie简单一些，相应的也增加了服务器的存储压力。
  
###  什么是Session
  
  
Session是另一种记录客户状态的机制，不同的是Cookie保存在客户端浏览器中，而Session保存在服务器上。客户端浏览器访问服务器的时候，服务器把客户端信息以某种形式记录在服务器上。这就是Session。客户端浏览器再次访问时只需要从该Session中查找该客户的状态就可以了。
  
如果说Cookie机制是通过检查客户身上的“通行证”来确定客户身份的话，那么Session机制就是通过检查服务器上的“客户明细表”来确认客户身份。Session相当于程序在服务器上建立的一份客户档案，客户来访的时候只需要查询客户档案表就可以了。
  
###  实现用户登录
  
  
Session对应的类为`javax.servlet.http.HttpSession`类。每个来访者对应一个Session对象，所有该客户的状态信息都保存在这个Session对象里。Session对象是在客户端第一次请求服务器的时候创建的。Session也是一种key-value的属性对，通过`getAttribute(Stringkey)`和`setAttribute(String key，Objectvalue)`方法读写客户状态信息。Servlet里通过`request.getSession()`方法获取该客户的Session，
  
```java
  
HttpSession session = request.getSession(); // 获取Session对象
session.setAttribute("loginTime", new Date()); // 设置Session中的属性
  
System.out.println("登录时间为：" +(Date)session.getAttribute("loginTime")); // 获取Session属性
  
```
request还可以使用 `getSession(boolean create)`来获取Session。区别是如果该客户的Session不存在，`request.getSession()`方法会返回null，而`getSession(true)`会先创建Session再将Session返回。
  
Servlet中必须使用request来编程式获取HttpSession对象，而JSP中内置了Session隐藏对象，可以直接使用。如果使用声明了`<%@page session="false" %>`，则Session隐藏对象不可用。下面的例子使用Session记录客户账号信息。
  
```java
<%@ page language="java" pageEncoding="UTF-8"%>
  
<jsp:directive.page import="com.helloweenvsfei.sessionWeb.bean.Person"/>
  
<jsp:directive.page import="java.text.SimpleDateFormat"/>
  
<jsp:directive.page import="java.text.DateFormat"/>
  
<jsp:directive.page import="java.util.Date"/>
  
<%!
  
    DateFormat dateFormat = newSimpleDateFormat("yyyy-MM-dd");         // 日期格式化器
  
%>
  
<%
  
    response.setCharacterEncoding("UTF-8");        // 设置request编码
  
    Person[] persons =
  
    {          
  
       // 基础数据，保存三个人的信息
  
        new Person("Liu Jinghua","password1", 34, dateFormat.parse
        ("1982-01-01")),
  
        new Person("Hello Kitty","hellokitty", 23, dateFormat.parse
        ("1984-02-21")),
  
        new Person("Garfield", "garfield_pass",23, dateFormat.parse
        ("1994-09-12")),
  
     };
  
  
  
    String message = "";                      // 要显示的消息
  
  
  
    if(request.getMethod().equals("POST"))
  
    {
  
        // 如果是POST登录       
  
        for(Person person :persons)
  
        {          
  
            // 遍历基础数据，验证账号、密码
  
            // 如果用户名正确且密码正确
  
           if(person.getName().equalsIgnoreCase(request.getParameter("username"))&&person.getPassword().equals(request.getParameter("password")))
  
           {              
  
               // 登录成功，设置将用户的信息以及登录时间保存到Session
  
               session.setAttribute("person", person);                   // 保存登录的Person
  
               session.setAttribute("loginTime", new Date());          // 保存登录的时间              
  
               response.sendRedirect(request.getContextPath() + "/welcome.jsp");
  
               return;
  
            }
  
        }      
  
        message = "用户名密码不匹配，登录失败。";       // 登录失败
  
    }
  
%>
  
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01Transitional//EN">
  
<html>
  
    // ... HTML代码为一个FORM表单，代码略，请看随书光盘
  
</html>
  
```
  
登录界面验证用户登录信息，如果登录正确，就把用户信息以及登录时间保存进Session，然后转到欢迎页面welcome.jsp。welcome.jsp中从Session中获取信息，并将用户资料显示出来。
  
  
```java
<%@ page language="java" pageEncoding="UTF-8"%>
  
<jsp:directive.pageimport="com.helloweenvsfei.sessionWeb.bean.Person"/>
  
<jsp:directive.page import="java.text.SimpleDateFormat"/>
  
<jsp:directive.page import="java.text.DateFormat"/>
  
<jsp:directive.page import="java.util.Date"/>
  
<%!
  
    DateFormat dateFormat = newSimpleDateFormat("yyyy-MM-dd");         // 日期格式化器
  
%>
  
<%
  
    Person person =(Person)session.getAttribute("person");                       // 获取登录的person
  
    Date loginTime =(Date)session.getAttribute("loginTime");                     // 获取登录时间
  
%>
  
    // ... 部分HTML代码略
  
            <table>
  
               <tr><td>您的姓名：</td>
  
                   <td><%= person.getName()%></td>
  
               </tr>
  
               <tr><td>登录时间：</td>
  
                   <td><%= loginTime%></td>
  
               </tr>
  
               <tr><td>您的年龄：</td>
  
                   <td><%= person.getAge()%></td>
  
               </tr>
  
               <tr><td>您的生日：</td>
  
                   <td><%=dateFormat.format(person.getBirthday()) %></td>
  
               </tr>
  
            </table>
```
  
注意程序中`Session`中直接保存了`Person`类对象与Date类对象，使用起来要比`Cookie`方便。
  
当多个客户端执行程序时，服务器会保存多个客户端的`Session`。获取`Session`的时候也不需要声明获取谁的`Session`。`Session`机制决定了当前客户只会获取到自己的`Session`，而不会获取到别人的`Session`。各客户的`Session`也彼此独立，互不可见。
  
`Session`的使用比`Cookie`方便，但是过多的`Session`存储在服务器内存中，会对服务器造成压力。
  
###  Session的生命周期
  
  
`Session`保存在服务器端。为了获得更高的存取速度，服务器一般把`Session`放在内存里。每个用户都会有一个独立的`Session`。如果`Session`内容过于复杂，当大量客户访问服务器时可能会导致内存溢出。因此，`Session`里的信息应该尽量精简。
  
`Session`在用户第一次访问服务器的时候自动创建。需要注意只有访问`JSP、Servlet`等程序时才会创建`Session`，只访问`HTML、IMAGE`等静态资源并不会创建`Session`。如果尚未生成`Session`，也可以使用`request.getSession(true)`强制生成`Session`。
  
`Session`生成后，只要用户继续访问，服务器就会更新`Session`的最后访问时间，并维护该`Session`。用户每访问服务器一次，无论是否读写Session，服务器都认为该用户的Session`“活跃（active）”`了一次。
  
  
  
###   Session的有效期
  
  
由于会有越来越多的用户访问服务器，因此`Session`也会越来越多。为防止内存溢出，服务器会把长时间内没有活跃的`Session`从内存删除。这个时间就是`Session`的超时时间。如果超过了超时时间没访问过服务器，`Session`就自动失效了。
  
`Session`的超时时间为`maxInactiveInterval`属性，可以通过对应的`getMaxInactiveInterval()`获取，通过`setMaxInactiveInterval(longinterval)`修改。
  
`Session`的超时时间也可以在`web.xml`中修改。另外，通过调用`Session`的`invalidate()`方法可以使`Session`失效。
  
  
  
###  Session的常用方法
  
  
Session中包括各种方法，使用起来要比Cookie方便得多。
  
**Session的常用方法如表**
  
|方法名 |  描述 |
| --- | ---|
| void setAttribute(String attribute, Object value)|设置Session属性。value参数可以为任何Java Object。通常为Java Bean。value信息不宜过大|
|String getAttribute(String attribute)|返回Session属性|
|Enumeration getAttributeNames()| 返回Session中存在的属性名|
|void removeAttribute(String attribute)| 移除Session属性|
|String getId()| 返回Session的ID。该ID由服务器自动创建，不会重复|
|long getCreationTime()| 返回Session的创建日期。返回类型为long，常被转化为Date类型，例如：Date createTime = new Date(session.get CreationTime())|
|long getLastAccessedTime()| 返回Session的最后活跃时间。返回类型为long|
|int getMaxInactiveInterval()|返回Session的超时时间。单位为秒。超过该时间没有访问，服务器认为该Session失效|
| void setMaxInactiveInterval(int second)| 设置Session的超时时间。单位为秒|
|void putValue(String attribute, Object value)|不推荐的方法。已经被setAttribute(String attribute, Object Value)替代|
|Object getValue(String attribute)|不被推荐的方法。已经被getAttribute(String attr)替代|
|boolean isNew()| 返回该Session是否是新创建的 |
|void invalidate()|使该Session失效|
  
  
Tomcat中Session的默认超时时间为20分钟。通过setMaxInactiveInterval(int seconds)修改超时时间。可以修改web.xml改变Session的默认超时时间。例如修改为60分钟：
  
```xml
  
<session-config>
  
   <session-timeout>60</session-timeout> <!-- 单位：分钟 -->
  
</session-config>
  
```
  
注意：<session-timeout>参数的单位为分钟，而setMaxInactiveInterval(int s)单位为秒。
  
  
###  Session对浏览器的要求
  
  
虽然Session保存在服务器，对客户端是透明的，它的正常运行仍然需要客户端浏览器的支持。这是因为Session需要使用Cookie作为识别标志。HTTP协议是无状态的，Session不能依据HTTP连接来判断是否为同一客户，因此服务器向客户端浏览器发送一个名为JSESSIONID的Cookie，它的值为该Session的id（也就是HttpSession.getId()的返回值）。Session依据该Cookie来识别是否为同一用户。
  
该Cookie为服务器自动生成的，它的maxAge属性一般为–1，表示仅当前浏览器内有效，并且各浏览器窗口间不共享，关闭浏览器就会失效。
  
因此同一机器的两个浏览器窗口访问服务器时，会生成两个不同的Session。但是由浏览器窗口内的链接、脚本等打开的新窗口（也就是说不是双击桌面浏览器图标等打开的窗口）除外。这类子窗口会共享父窗口的Cookie，因此会共享一个Session。
  
  
注意：新开的浏览器窗口会生成新的Session，但子窗口除外。子窗口会共用父窗口的Session。例如，在链接上右击，在弹出的快捷菜单中选择“在新窗口中打开”时，子窗口便可以访问父窗口的Session。
  
如果客户端浏览器将Cookie功能禁用，或者不支持Cookie怎么办？例如，绝大多数的手机浏览器都不支持Cookie。Java Web提供了另一种解决方案：URL地址重写。
  
  
###   URL地址重写
  
  
URL地址重写是对客户端不支持Cookie的解决方案。URL地址重写的原理是将该用户Session的id信息重写到URL地址中。服务器能够解析重写后的URL获取Session的id。这样即使客户端不支持Cookie，也可以使用Session来记录用户状态。`HttpServletResponse`类提供了`encodeURL(Stringurl)`实现URL地址重写，例如：
  
```HTML
<td>
  
    <a href="<%=response.encodeURL("index.jsp?c=1&wd=Java") %>">
    Homepage</a>
  
</td>
  
```
  
该方法会自动判断客户端是否支持Cookie。如果客户端支持Cookie，会将URL原封不动地输出来。如果客户端不支持Cookie，则会将用户Session的id重写到URL中。重写后的输出可能是这样的：
  
```html
<td>
  
    <ahref="index.jsp;jsessionid=0CCD096E7F8D97B0BE608AFDC3E1931E?c=
    1&wd=Java">Homepage</a>
  
</td>
  
```
  
即在文件名的后面，在URL参数的前面添加了字符串“;jsessionid=XXX”。其中XXX为Session的id。分析一下可以知道，增添的jsessionid字符串既不会影响请求的文件名，也不会影响提交的地址栏参数。用户单击这个链接的时候会把Session的id通过URL提交到服务器上，服务器通过解析URL地址获得Session的id。
  
如果是页面重定向（Redirection），URL地址重写可以这样写：
  
```java
<%
  
    if(“administrator”.equals(userName))
  
    {
  
       response.sendRedirect(response.encodeRedirectURL(“administrator.jsp”));
  
        return;
  
    }
  
%>
```
  
效果跟response.encodeURL(String url)是一样的：如果客户端支持Cookie，生成原URL地址，如果不支持Cookie，传回重写后的带有jsessionid字符串的地址。
  
对于WAP程序，由于大部分的手机浏览器都不支持Cookie，WAP程序都会采用URL地址重写来跟踪用户会话。比如用友集团的移动商街等。
  
注意：TOMCAT判断客户端浏览器是否支持Cookie的依据是请求中是否含有Cookie。尽管客户端可能会支持Cookie，但是由于第一次请求时不会携带任何Cookie（因为并无任何Cookie可以携带），URL地址重写后的地址中仍然会带有jsessionid。当第二次访问时服务器已经在浏览器中写入Cookie了，因此URL地址重写后的地址中就不会带有jsessionid了。
  
###  Session中禁止使用Cookie
  
  
既然WAP上大部分的客户浏览器都不支持Cookie，索性禁止Session使用Cookie，统一使用URL地址重写会更好一些。Java Web规范支持通过配置的方式禁用Cookie。下面举例说一下怎样通过配置禁止使用Cookie。
  
打开项目sessionWeb的WebRoot目录下的META-INF文件夹（跟WEB-INF文件夹同级，如果没有则创建），打开context.xml（如果没有则创建），编辑内容如下：
  
```xml
<!-- /META-INF/context.xml -->
  
<?xml version='1.0' encoding='UTF-8'?>
  
<Context path="/sessionWeb"cookies="false">
  
</Context>
  
```
  
或者修改Tomcat全局的conf/context.xml，修改内容如下：
  
  
```xml
<!-- The contents of this file will be loaded for eachweb application -->
  
<Context cookies="false">
  
    <!-- ... 中间代码略 -->
  
</Context>
  
```
  
部署后TOMCAT便不会自动生成名JSESSIONID的Cookie，Session也不会以Cookie为识别标志，而仅仅以重写后的URL地址为识别标志了。
  
  
注意：该配置只是禁止Session使用Cookie作为识别标志，并不能阻止其他的Cookie读写。也就是说服务器不会自动维护名为JSESSIONID的Cookie了，但是程序中仍然可以读写其他的Cookie。
  
  