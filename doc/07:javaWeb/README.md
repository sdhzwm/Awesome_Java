
  
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
  
  
  
  
#  Cookie和Session
  
  
会话（Session）跟踪是Web程序中常用的技术，用来跟踪用户的整个会话。常用的会话跟踪技术是Cookie与Session。Cookie通过在客户端记录信息确定用户身份，Session通过在服务器端记录信息确定用户身份。
  
##  Cookie
  
  
  
在程序中，会话跟踪是很重要的事情。理论上，一个用户的所有请求操作都应该属于同一个会话，而另一个用户的所有请求操作则应该属于另一个会话，二者不能混淆。例如，用户A在超市购买的任何商品都应该放在A的购物车内，不论是用户A什么时间购买的，这都是属于同一个会话的，不能放入用户B或用户C的购物车内，这不属于同一个会话。
  
而Web应用程序是使用HTTP协议传输数据的。HTTP协议是无状态的协议。一旦数据交换完毕，客户端与服务器端的连接就会关闭，再次交换数据需要建立新的连接。这就意味着服务器无法从连接上跟踪会话。即用户A购买了一件商品放入购物车内，当再次购买商品时服务器已经无法判断该购买行为是属于用户A的会话还是用户B的会话了。要跟踪该会话，必须引入一种机制。为了做到这点，就需要使用到Cookie了。服务器可以设置或读取Cookies中包含信息，借此维护用户跟服务器会话中的状态
  
Cookie就是这样的一种机制。它可以弥补HTTP协议无状态的不足。在Session出现之前，基本上所有的网站都采用Cookie来跟踪会话。
  
###  什么是Cookie
  
  
Cookie意为"甜饼"，是由W3C组织提出，最早由Netscape社区发展的一种机制。目前Cookie已经成为标准，所有的主流浏览器如IE、Chrome、Firefox、Opera等都支持Cookie。
  
由于HTTP是一种无状态的协议，服务器单从网络连接上无从知道客户身份。服务端会给客户端们颁发一个通行证，客户端访问都必须携带自己通行证。这样服务器就能从通行证上确认客户身份了。这就是Cookie的工作原理。
  
Cookie实际上是一小段的文本信息。客户端请求服务器，如果服务器需要记录该用户状态，就使用response向客户端浏览器颁发一个Cookie。客户端浏览器会把Cookie保存起来。当浏览器再请求该网站时，浏览器把请求的网址连同该Cookie一同提交给服务器。服务器检查该Cookie，以此来辨认用户状态。服务器还可以根据需要修改Cookie的内容。
  
![示意图](http://hi.csdn.net/attachment/201111/9/0_13208318702UfF.gif )
  
查看某个网站颁发的Cookie很简单。在浏览器地址栏输入`javascript:alert (document. cookie)`就可以了（需要有网才能查看）。JavaScript脚本会弹出一个对话框显示本网站颁发的所有Cookie的内容，如图
  
![示例](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/WX20191030-102212@2x.png )
  
**注意:Cookie功能需要浏览器的支持。**
  
如果浏览器不支持Cookie（如大部分手机中的浏览器）或者把Cookie禁用了，Cookie功能就会失效。
  
###  记录用户访问次数
  
  
`Java`中把Cookie封装成了`javax.servlet.http.Cookie`类。每个`Cookie`都是该`Cookie`类的对象。服务器通过操作Cookie类对象对客户端Cookie进行操作。通过`request.getCookie()`获取客户端提交的所有Cookie（以Cookie[]数组形式返回），通过`response.addCookie(Cookiecookie)`向客户端设置`Cookie`。
  
`Cookie`对象使用`key-value`属性对的形式保存用户状态，一个`Cookie`对象保存一个属性对，一个`request`或者`response`同时使用多个`Cookie`。因为`Cookie`类位于包`javax.servlet.http.*`下面，所以JSP中不需要`import`该类。
  
  
  
###  Cookie的不可跨域名性
  
  
很多网站都会使用`Cookie`。例如，Google会向客户端颁发Cookie，Baidu也会向客户端颁发Cookie。但双方是无法相互读取及修改的。
  
`Cookie`具有不可跨域名性。根据`Cookie`规范，浏览器访问`Google`只会携带`Google`的`Cookie`，而不会携带`Baidu`的`Cookie`。`Google`也只能操作`Google`的`Cookie`，而不能操作`Baidu`的`Cookie`。
  
`Cookie`在客户端是由浏览器来管理的。浏览器能够保证`Google`只会操作`Google`的`Cookie`而不会操作`Baidu`的`Cookie`，从而保证用户的隐私安全。浏览器判断一个网站是否能操作另一个网站`Cookie`的依据是域名。`Google`与`Baidu`的域名不一样，因此`Google`不能操作`Baidu`的`Cookie`。
  
需要注意的是，虽然网站`images.google.com`与网站`www.google.com`同属于`Google`，但是域名不一样，二者同样不能互相操作彼此的Cookie。
  
需要注意的是用户登录网站`www.google.com`之后会发现访问`images.google.com`时登录信息仍然有效，而普通的`Cookie`是做不到的。这是因为`Google`做了特殊处理。
  
###  Unicode编码：保存中文
  
  
中文与英文字符不同，中文属于`Unicode字符`，在内存中占4个字符，而英文属于`ASCII字符`，内存中只占2个字节。`Cookie`中使用`Unicode字符`时需要对`Unicode字符进行编码`，否则会乱码。
  
注意`Cookie`中保存中文只能编码。一般使用`UTF-8`编码即可。不推荐使用`GBK`等中文编码，因为浏览器不一定支持，而且`JavaScript`也不支持`GBK`编码。
  
  
  
###  BASE64编码：保存二进制图片
  
  
`Cookie`不仅可以使用`ASCII`字符与`Unicode`字符，还可以使用二进制数据。例如在`Cookie`中使用数字证书，提供安全度。使用二进制数据时也需要进行编码。
  
`Cookie`中可以存储二进制内容，并不实用。由于浏览器每次请求服务器都会携带`Cookie`，因此`Cookie`内容不宜过多，否则影响速度。
  
###  设置Cookie的所有属性
  
  
除了name与value之外，Cookie还具有其他几个常用的属性。每个属性对应一个getter方法与一个setter方法。Cookie类的所有属性如表1.1所示。
  
| 属性名 | 描述 |
| ---  | --- |
|`String name`| 该`Cookie`的名称。`Cookie`一旦创建，名称便不可更改 |
| `Object value` | 该`Cookie`的值。如果值为`Unicode`字符，需要为字符编码。如果值为二进制数据，则需要使用`BASE64`编码 |
| `int maxAge` | 该`Cookie`失效的时间，单位秒。如果为正数，则该`Cookie`在`maxAge`秒之后失效。如果为负数，该`Cookie`为临时`Cookie`，关闭浏览器即失效，浏览器也不会以任何形式保存该`Cookie`。如果为0，表示删除该`Cookie`。默认为–1|
| `boolean secure` | 该`Cookie`是否仅被使用安全协议传输。安全协议。安全协议有HTTPS，SSL等，在网络上传输数据之前先将数据加密。默认为`false`| 
| `String path` | 该`Cookie`的使用路径。如果设置为`“/sessionWeb/”`，则只有`contextPath`为`“/sessionWeb”`的程序可以访问该`Cookie`。如果设置为`“/”`，则本域名下`contextPath`都可以访问该`Cookie`。注意最后一个字符必须为`“/”`|
| `String domain` | 可以访问该`Cookie`的域名。如果设置为`“.google.com”`，则所有以`“google.com”`结尾的域名都可以访问该`Cookie`。注意第一个字符必须为`“.”`| 
| `String comment`| 该`Cookie`的用处说明。浏览器显示`Cookie`信息的时候显示该说明 |
| `int version`| 该`Cookie`使用的版本号。0表示遵循`Netscape`的`Cookie`规范，1表示遵循W3C的RFC 2109规范| 
  
  
###  Cookie的有效期
  
  
Cookie的maxAge决定着Cookie的有效期，单位为秒（Second）。Cookie中通过getMaxAge()方法与setMaxAge(int maxAge)方法来读写maxAge属性。
  
如果maxAge属性为正数，则表示该Cookie会在maxAge秒之后自动失效。浏览器会将maxAge为正数的Cookie持久化，即写到对应的Cookie文件中。无论客户关闭了浏览器还是电脑，只要还在maxAge秒之前，登录网站时该Cookie仍然有效。下面代码中的Cookie信息将永远有效。
  
```java
  
Cookie cookie = new Cookie("username","hello");   // 新建Cookie
  
cookie.setMaxAge(Integer.MAX_VALUE); // 设置生命周期为MAX_VALUE
  
response.addCookie(cookie); // 输出到客户端
  
```
  
如果maxAge为负数，则表示该Cookie仅在本浏览器窗口以及本窗口打开的子窗口内有效，关闭窗口后该Cookie即失效。maxAge为负数的Cookie，为临时性Cookie，不会被持久化，不会被写到Cookie文件中。Cookie信息保存在浏览器内存中，因此关闭浏览器该Cookie就消失了。Cookie默认的maxAge值为–1。
  
如果maxAge为0，则表示删除该Cookie。Cookie机制没有提供删除Cookie的方法，因此通过设置该Cookie即时失效实现删除Cookie的效果。失效的Cookie会被浏览器从Cookie文件或者内存中删除，
  
  
  
例如：
  
```java
Cookie cookie = new Cookie("username","helloweenvsfei");   // 新建Cookie
  
cookie.setMaxAge(0);  // 设置生命周期为0，不能为负数
  
response.addCookie(cookie); // 必须执行这一句
  
  
```
  
response对象提供的Cookie操作方法只有一个添加操作add(Cookie cookie)。
  
要想修改Cookie只能使用一个同名的Cookie来覆盖原来的Cookie，达到修改的目的。删除时只需要把maxAge修改为0即可。
  
  
  
注意：从客户端读取Cookie时，包括maxAge在内的其他属性都是不可读的，也不会被提交。浏览器提交Cookie时只会提交name与value属性。maxAge属性只被浏览器用来判断Cookie是否过期。
  
  
  
###  Cookie的修改、删除
  
  
Cookie并不提供修改、删除操作。如果要修改某个Cookie，只需要新建一个同名的Cookie，添加到response中覆盖原来的Cookie。
  
如果要删除某个Cookie，只需要新建一个同名的Cookie，并将maxAge设置为0，并添加到response中覆盖原来的Cookie。注意是0而不是负数。负数代表其他的意义。读者可以通过上例的程序进行验证，设置不同的属性。
  
修改、删除Cookie时，新建的Cookie除value、maxAge之外的所有属性，例如name、path、domain等，都要与原Cookie完全一样。否则，浏览器将视为两个不同的Cookie不予覆盖，导致修改、删除失败。
  
  
  
###  Cookie的域名
  
  
Cookie是不可跨域名的。域名`www.google.com`颁发的Cookie不会被提交到域名`www.baidu.com`去。这是由Cookie的隐私安全机制决定的。隐私安全机制能够禁止网站非法获取其他网站的Cookie。
  
正常情况下，同一个一级域名下的两个二级域名如`www.google.com`和`images.google.com` `google.com`名下的二级域名都可以使用该Cookie，需要设置Cookie的domain参数，例如：
  
```java
Cookie cookie = new Cookie("time","20190808"); // 新建Cookie
  
cookie.setDomain(".google.com");           // 设置域名
  
cookie.setPath("/");                              // 设置路径
  
cookie.setMaxAge(Integer.MAX_VALUE);               // 设置有效期
  
response.addCookie(cookie);                       // 输出到客户端
  
```
  
注意：domain参数必须以点(".")开始。另外，name相同但domain不同的两个Cookie是两个不同的Cookie。如果想要两个域名完全不同的网站共有Cookie，可以生成两个Cookie，domain属性分别为两个域名，输出到客户端。
  
  
  
###  Cookie的路径
  
  
domain属性决定运行访问Cookie的域名，而path属性决定允许访问Cookie的路径（ContextPath）。例如，如果只允许/sessionWeb/下的程序使用Cookie，可以这么写：
  
```java
Cookie cookie = new Cookie("time","20080808");  // 新建Cookie
  
cookie.setPath("/session/");  // 设置路径
  
response.addCookie(cookie);  // 输出到客户端
```
  
设置为“/”时允许所有路径使用Cookie。path属性需要使用符号“/”结尾。name相同但domain相同的两个Cookie也是两个不同的Cookie。
  
  
  
注意：页面只能获取它属于的Path的Cookie。例如/session/test/a.jsp不能获取到路径为/session/abc/的Cookie。使用时一定要注意。
  
  
  
###  Cookie的安全属性
  
  
HTTP协议不仅是无状态的，而且是不安全的。使用HTTP协议的数据不经过任何加密就直接在网络上传播，有被截获的可能。使用HTTP协议传输很机密的内容是一种隐患。如果不希望Cookie在HTTP等非安全协议中传输，可以设置Cookie的secure属性为true。浏览器只会在HTTPS和SSL等安全协议中传输此类Cookie。下面的代码设置secure属性为true：
  
```java
  
Cookie cookie = new Cookie("time", "20190808"); // 新建Cookie
  
cookie.setSecure(true);  // 设置安全属性
  
response.addCookie(cookie);  // 输出到客户端
  
```
  
secure属性并不能对Cookie内容加密，因而不能保证绝对的安全性。如果需要高安全性，需要在程序中对Cookie内容加密、解密，以防泄密。
  
  
  
###  avaScript操作Cookie
  
  
Cookie是保存在浏览器端的，因此浏览器具有操作Cookie的先决条件。浏览器可以使用脚本程序如JavaScript或者VBScript等操作Cookie。这里以JavaScript为例介绍常用的Cookie操作。例如下面的代码会输出本页面所有的Cookie。
  
```js
  
<script>document.write(document.cookie);</script>
```
由于JavaScript能够任意地读写Cookie，有些好事者便想使用JavaScript程序去窥探用户在其他网站的Cookie。不过这是徒劳的，W3C组织早就意识到JavaScript对Cookie的读写所带来的安全隐患并加以防备了，W3C标准的浏览器会阻止JavaScript读写任何不属于自己网站的Cookie。换句话说，A网站的JavaScript程序读写B网站的Cookie不会有任何结果。
  
  
  
###  案例：永久登录
  
  
如果用户是在自己家的电脑上上网，登录时就可以记住他的登录信息，下次访问时不需要再次登录，直接访问即可。实现方法是把登录信息如账号、密码等保存在Cookie中，并控制Cookie的有效期，下次访问时再验证Cookie中的登录信息即可。
  
保存登录信息有多种方案。最直接的是把用户名与密码都保持到Cookie中，下次访问时检查Cookie中的用户名与密码，与数据库比较。这是一种比较危险的选择，一般不把密码等重要信息保存到Cookie中。
  
还有一种方案是把密码加密后保存到Cookie中，下次访问时解密并与数据库比较。这种方案略微安全一些。如果不希望保存密码，还可以把登录的时间戳保存到Cookie与数据库中，到时只验证用户名与登录时间戳就可以了。
  
这几种方案验证账号时都要查询数据库。
  
本例将采用另一种方案，只在登录时查询一次数据库，以后访问验证登录信息时不再查询数据库。实现方式是把账号按照一定的规则加密后，连同账号一块保存到Cookie中。下次访问时只需要判断账号的加密规则是否正确即可。本例把账号保存到名为account的Cookie中，把账号连同密钥用MD1算法加密后保存到名为ssid的Cookie中。验证时验证Cookie中的账号与密钥加密后是否与Cookie中的ssid相等。相关代码如下：
  
```java
//代码1.8 loginCookie.jsp
  
<%@ page language="java"pageEncoding="UTF-8" isErrorPage="false" %>
  
<%!                                                  // JSP方法
  
    private static final String KEY =":cookie@helloweenvsfei.com";
                                                     // 密钥 
  
    public final static String calcMD1(Stringss) { // MD1 加密算法
  
       String s = ss==null ?"" : ss;                  // 若为null返回空
  
       char hexDigits[] = { '0','1', '2', '3', '4', '1', '6', '7', '8', '9',
       'a', 'b', 'c', 'd', 'e', 'f' };                        // 字典
  
       try {
  
        byte[] strTemp =s.getBytes();                          // 获取字节
  
        MessageDigestmdTemp = MessageDigest.getInstance("MD1"); // 获取MD1
  
       mdTemp.update(strTemp);                                // 更新数据
  
        byte[] md =mdTemp.digest();                        // 加密
  
        int j =md.length;                                 // 加密后的长度
  
        char str[] = newchar[j * 2];                       // 新字符串数组
  
        int k =0;                                         // 计数器k
  
        for (int i = 0; i< j; i++) {                       // 循环输出
  
         byte byte0 =md[i];
  
         str[k++] =hexDigits[byte0 >>> 4 & 0xf];
  
         str[k++] =hexDigits[byte0 & 0xf];
  
        }
  
        return newString(str);                             // 加密后字符串
  
       } catch (Exception e){return null; }
  
    }
  
%>
  
<%
  
   request.setCharacterEncoding("UTF-8");             // 设置request编码
  
    response.setCharacterEncoding("UTF-8");        // 设置response编码
  
  
  
    String action =request.getParameter("action"); // 获取action参数
  
  
  
    if("login".equals(action)){                       // 如果为login动作
  
        String account =request.getParameter("account");
                                                     // 获取account参数
  
        String password =request.getParameter("password");
                                                     // 获取password参数
  
        int timeout = newInteger(request.getParameter("timeout"));
                                                     // 获取timeout参数
  
  
  
        String ssid =calcMD1(account + KEY); // 把账号、密钥使用MD1加密后保存
  
  
  
        CookieaccountCookie = new Cookie("account", account);
                                                     // 新建Cookie
  
       accountCookie.setMaxAge(timeout);              // 设置有效期
  
  
  
        Cookie ssidCookie =new Cookie("ssid", ssid);   // 新建Cookie
  
       ssidCookie.setMaxAge(timeout);                 // 设置有效期
  
  
  
       response.addCookie(accountCookie);             // 输出到客户端
  
       response.addCookie(ssidCookie);            // 输出到客户端
  
  
  
        // 重新请求本页面，参数中带有时间戳，禁止浏览器缓存页面内容
  
       response.sendRedirect(request.getRequestURI() + "?" + System.
        currentTimeMillis());
  
        return;
  
    }
  
    elseif("logout".equals(action)){                  // 如果为logout动作
  
  
  
        CookieaccountCookie = new Cookie("account", "");
                                                 // 新建Cookie，内容为空
  
       accountCookie.setMaxAge(0);                // 设置有效期为0，删除
  
  
  
        Cookie ssidCookie =new Cookie("ssid", ""); // 新建Cookie，内容为空
  
       ssidCookie.setMaxAge(0);                   // 设置有效期为0，删除
  
       response.addCookie(accountCookie);         // 输出到客户端
  
       response.addCookie(ssidCookie);         // 输出到客户端
  
        //重新请求本页面，参数中带有时间戳，禁止浏览器缓存页面内容
  
       response.sendRedirect(request.getRequestURI() + "?" + System.
        currentTimeMillis());
  
        return;
  
    }
  
    boolean login = false;                        // 是否登录
  
    String account = null;                        // 账号
  
    String ssid = null;                           // SSID标识
  
  
  
    if(request.getCookies() !=null){               // 如果Cookie不为空
  
        for(Cookie cookie :request.getCookies()){  // 遍历Cookie
  
           if(cookie.getName().equals("account"))  // 如果Cookie名为
                                                    account
  
               account = cookie.getValue();       // 保存account内容
  
           if(cookie.getName().equals("ssid")) // 如果为SSID
  
               ssid = cookie.getValue();          // 保存SSID内容
  
        }
  
    }
  
    if(account != null && ssid !=null){    // 如果account、SSID都不为空
  
        login =ssid.equals(calcMD1(account + KEY));
                                      // 如果加密规则正确, 则视为已经登录
  
    }
  
%>
  
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01Transitional//EN">
  
       <legend><%= login ? "欢迎您回来" : "请先登录"%></legend>
  
        <% if(login){%>
  
            欢迎您, ${ cookie.account.value }. &nbsp;&nbsp;
  
           <a href="${ pageContext.request.requestURI }?action=logout">
            注销</a>
  
        <% } else {%>
  
        <formaction="${ pageContext.request.requestURI }?action=login"
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
  
  