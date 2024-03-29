# Servlet

## 什么是Servlet
    

Servlet（Server Applet），全称Java Servlet，未有中文译文。是用Java编写的服务器端程序。其主要功能在于交互式地浏览和修改数据，生成动态Web内容。狭义的Servlet是指Java语言实现的一个接口，广义的Servlet是指任何实现了这个Servlet接口的类，一般情况下，人们将Servlet理解为后者。

Servlet运行于支持Java的应用服务器中。从实现上讲，Servlet可以响应任何类型的请求，但绝大多数情况下Servlet只用来扩展基于HTTP协议的Web服务器。

## Servlet工作模式

- 客户端发送请求至服务器
- 服务器启动并调用Servlet，Servlet根据客户端请求生成响应内容并将其传给服务器
- 服务器将响应返回客户端

## Servlet的API概览

Servlet API 包含以下4个Java包：

1. `javax.servlet`其中包含定义servlet和servlet容器之间契约的类和接口。

2. `javax.servlet.http`其中包含定义HTTP Servlet 和Servlet容器之间的关系。

3. `javax.servlet.annotation`其中包含标注servlet，Filter,Listener的标注。它还为被标注元件定义元数据。

4. `javax.servlet.descriptor`，其中包含提供程序化登录Web应用程序的配置信息的类型。


## Servlet 的主要类型

![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20191025111742.png)

## Servlet 的使用方法

Servlet技术的核心是Servlet，它是所有Servlet类必须直接或者间接实现的一个接口。在编写实现Servlet的Servlet类时，直接实现它。在扩展实现这个这个接口的类时，间接实现它。

## Servlet 的工作原理

Servlet接口定义了Servlet与servlet容器之间的契约。这个契约是：Servlet容器将Servlet类载入内存，并产生Servlet实例和调用它具体的方法。但是要注意的是，在一个应用程序中，每种Servlet类型只能有一个实例。

 

用户请求致使Servlet容器调用Servlet的Service（）方法，并传入一个ServletRequest对象和一个ServletResponse对象。ServletRequest对象和ServletResponse对象都是由Servlet容器（例如TomCat）封装好的，并不需要程序员去实现，程序员可以直接使用这两个对象。

ServletRequest中封装了当前的Http请求，因此，开发人员不必解析和操作原始的Http数据。ServletResponse表示当前用户的Http响应，程序员只需直接操作ServletResponse对象就能把响应轻松的发回给用户。

对于每一个应用程序，Servlet容器还会创建一个ServletContext对象。这个对象中封装了上下文（应用程序）的环境详情。每个应用程序只有一个ServletContext。每个Servlet对象也都有一个封装Servlet配置的ServletConfig对象。



## Servlet的体系结构	

Servlet -- 接口
			|
GenericServlet -- 抽象类

将Servlet接口中其他的方法做了默认空实现，只将service()方法作为抽象

* 将来定义Servlet类时，可以继承GenericServlet，实现service()方法即可

			
HttpServlet  -- 抽象类 对http协议的一种封装，简化操作

1. 定义类继承HttpServlet
2. 复写doGet/doPost方法
	
## Servlet相关配置

1. urlpartten:Servlet访问路径
2. 一个Servlet可以定义多个访问路径 ： @WebServlet({"/d4","/dd4","/ddd4"})
3. 路径定义规则：
	1. /xxx：路径匹配
	2. /xxx/xxx:多层路径，目录结构
	3. *.do：扩展名匹配

---
# HTTP 和 HTTPS

## HTTP

### 什么是HTTP?

> 超文本传输协议，是一个基于请求与响应，无状态的，应用层的协议，常基于TCP/IP协议传输数据，互联网上应用最为广泛的一种网络协议,所有的WWW文件都必须遵守这个标准。设计HTTP的初衷是为了提供一种发布和接收HTML页面的方法。

![发展历史](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/WX20191029-102756@2x.png)

使用HTTP/1.1和HTTP/2同时请求379张图片，观察请求的时间，明显看出HTTP/2性能占优势。

![对比](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/WX20191029-102930@2x.png)

**多路复用：** 通过单一的HTTP/2连接请求发起多重的请求-响应消息，多个请求stream共享一个TCP连接，实现多留并行而不是依赖建立多个TCP连接。

![报文格式](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/WX20191029-103238@2x.png)


### 什么是HTTPS？

> 《图解HTTP》这本书中曾提过HTTPS是身披SSL外壳的HTTP。HTTPS是一种通过计算机网络进行安全通信的传输协议，经由HTTP进行通信，利用SSL/TLS建立全信道，加密数据包。HTTPS使用的主要目的是提供对网站服务器的身份认证，同时保护交换数据的隐私与完整性。
> PS:TLS是传输层加密协议，前身是SSL协议，由网景公司1995年发布，有时候两者不区分。



## HTTP VS HTTPS

### HTTP特点

- 无状态：协议对客户端没有状态存储，对事物处理没有“记忆”能力，比如访问一个网站需要反复进行登录操作
- 无连接：HTTP/1.1之前，由于无状态特点，每次请求需要通过TCP三次握手四次挥手，和服务器重新建立连接。比如某个客户机在短时间多次请求同一个资源，服务器并不能区别是否已经响应过用户的请求，所以每次需要重新响应请求，需要耗费不必要的时间和流量。
- 基于请求和响应：基本的特性，由客户端发起请求，服务端响应
- 简单快速、灵活
- 通信使用明文、请求和响应不会对通信方进行确认、无法保护数据的完整性

下面通过一个简单的抓包实验观察使用HTTP请求传输的数据：

![抓包实验](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/WX20191029-103707@2x.png)

![12306结果](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/WX20191029-103913@2x.png)

**结果分析： HTTP协议传输数据以明文形式显示**

针对无状态的一些解决策略：

场景：逛电商商场用户需要使用的时间比较长，需要对用户一段时间的HTTP通信状态进行保存，比如执行一次登陆操作，在30分钟内所有的请求都不需要再次登陆。
- 通过Cookie/Session技术
- HTTP/1.1持久连接（HTTP keep-alive）方法，只要任意一端没有明确提出断开连接，则保持TCP连接状态，在请求首部字段中的Connection: keep-alive即为表明使用了持久连接

### HTTPS特点

基于HTTP协议，通过SSL或TLS提供加密处理数据、验证对方身份以及数据完整性保护

![https的特点](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/WX20191029-104403@2x.png)


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

![https流程](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/WX20191029-105132@2x.png)

非对称加密过程需要用到公钥进行加密，那么公钥从何而来？其实公钥就被包含在数字证书中，数字证书通常来说是由受信任的数字证书颁发机构CA，在验证服务器身份后颁发，证书中包含了一个密钥对（公钥和私钥）和所有者识别信息。数字证书被放到服务端，具有服务器身份验证和数据传输加密功能。

## HTTP通信传输

![HTTP通信传输](https://img-blog.csdn.net/20180719094739178?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

客户端输入URL回车，DNS解析域名得到服务器的IP地址，服务器在80端口监听客户端请求，端口通过TCP/IP协议（可以通过Socket实现）建立连接。HTTP属于TCP/IP模型中的运用层协议，所以通信的过程其实是对应数据的入栈和出栈。

![流程](https://img-blog.csdn.net/20180719094756330?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

报文从运用层传送到运输层，运输层通过TCP三次握手和服务器建立连接，四次挥手释放连接。

![三次握手](https://img-blog.csdn.net/20180719110828114?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

为什么需要三次握手呢？

> 为了防止已失效的连接请求报文段突然又传送到了服务端，因而产生错误。

比如：client发出的第一个连接请求报文段并没有丢失，而是在某个网络结点长时间的滞留了，以致延误到连接释放以后的某个时间才到达server。本来这是一个早已失效的报文段，但是server收到此失效的连接请求报文段后，就误认为是client再次发出的一个新的连接请求，于是就向client发出确认报文段，同意建立连接。

假设不采用“三次握手”，那么只要server发出确认，新的连接就建立了，由于client并没有发出建立连接的请求，因此不会理睬server的确认，也不会向server发送数据，但server却以为新的运输连接已经建立，并一直等待client发来数据。所以没有采用“三次握手”，这种情况下server的很多资源就白白浪费掉了。


![四次握手](https://img-blog.csdn.net/20180719110841774?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

为什么需要四次挥手呢？

> TCP是全双工模式，当client发出FIN报文段时，只是表示client已经没有数据要发送了，client告诉server，它的数据已经全部发送完毕了；但是，这个时候client还是可以接受来server的数据；当server返回ACK报文段时，表示它已经知道client没有数据发送了，但是server还是可以发送数据到client的；当server也发送了FIN报文段时，这个时候就表示server也没有数据要发送了，就会告诉client，我也没有数据要发送了，如果收到client确认报文段，之后彼此就会愉快的中断这次TCP连接。

## HTTPS实现原理

### SSL建立连接过程
![SSL建立连接过程](https://img-blog.csdnimg.cn/20190803111825690.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx,size_16,color_FFFFFF,t_70)

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

![流程](https://img-blog.csdn.net/20180724090424143?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

> 证书如何安全传输，被掉包了怎么办？

![签名是否真实](https://img-blog.csdn.net/20180719095555854?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**数字证书内容**

包括了加密后服务器的公钥、权威机构的信息、服务器域名，还有经过CA私钥签名之后的证书内容（经过先通过Hash函数计算得到证书数字摘要，然后用权威机构私钥加密数字摘要得到数字签名)，签名计算方法以及证书对应的域名。

**验证证书安全性过程**

- 当客户端收到这个证书之后，使用本地配置的权威机构的公钥对证书进行解密得到服务端的公钥和证书的数字签名，数字签名经过CA公钥解密得到证书信息摘要。
- 然后证书签名的方法计算一下当前证书的信息摘要，与收到的信息摘要作对比，如果一样，表示证书一定是服务器下发的，没有被中间人篡改过。因为中间人虽然有权威机构的公钥，能够解析证书内容并篡改，但是篡改完成之后中间人需要将证书重新加密，但是中间人没有权威机构的私钥，无法加密，强行加密只会导致客户端无法解密，如果中间人强行乱修改证书，就会导致证书内容和证书签名不匹配。
  
那第三方攻击者能否让自己的证书显示出来的信息也是服务端呢？（伪装服务端一样的配置）显然这个是不行的，因为当第三方攻击者去CA那边寻求认证的时候CA会要求其提供例如域名的whois信息、域名管理邮箱等证明你是服务端域名的拥有者，而第三方攻击者是无法提供这些信息所以他就是无法骗CA他拥有属于服务端的域名


## 运用与总结

### 安全性考虑

- TTPS协议的加密范围也比较有限，在黑客攻击、拒绝服务攻击、服务器劫持等方面几乎起不到什么作用
- SSL证书的信用链体系并不安全，特别是在某些国家可以控制CA根证书的情况下，中间人攻击一样可行
  
中间人攻击（MITM攻击）是指，黑客拦截并篡改网络中的通信数据。又分为被动MITM和主动MITM，被动MITM只窃取通信数据而不修改，而主动MITM不但能窃取数据，还会篡改通信数据。最常见的中间人攻击常常发生在公共wifi或者公共路由上。

### 成本考虑
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

# Request

## 什么是request

`request`是`Servlet.service()`方法的一个参数，类型为`javax.servlet.http.HttpServletRequest`。在客户端发出每个请求时，服务器都会创建一个request对象，并把请求数据封装到request中，然后在调用`Servlet.service()`方法时传递给`service()`方法，这说明在`service()`方法中可以通过`request`对象来获取请求数据。

![图例](https://img-blog.csdn.net/20160816101242457?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

request的功能可以分为以下几种：

- 封装了请求头数据；

- 封装了请求正文数据，如果是GET请求，那么就没有正文；

- request是一个域对象，可以把它当成Map来添加获取数据；

- request提供了请求转发和请求包含功能。

## request域方法

request是域对象！在JavaWeb中一共四个域对象，其中ServletContext就是域对象，它在整个应用中只创建一个ServletContext对象。request其中一个，request可以在一个请求中共享数据。

一个请求会创建一个request对象，如果在一个请求中经历了多个Servlet，那么多个Servlet就可以使用request来共享数据。现在我们还不知道如何在一个请求中经历几个Servlet。

- （1）`void setAttribute(String name, Object value)：`用来存储一个对象，也可以称之为存储一个域属性，例如：`servletContext.setAttribute(“xxx”, “XXX”)`，在request中保存了一个域属性，域属性名称为xxx，域属性的值为XXX。请注意，如果多次调用该方法，并且使用相同的name，那么会覆盖上一次的值，这一特性与Map相同；

- （2）`Object getAttribute(String name)：`用来获取request中的数据，当前在获取之前需要先去存储才行，例如：`String value = (String)request.getAttribute(“xxx”);`，获取名为xxx的域属性；

- （3）`void removeAttribute(String name)：`用来移除request中的域属性，如果参数name指定的域属性不存在，那么本方法什么都不做；

- （4）`Enumeration getAttributeNames()：`获取所有域属性的名称；

## request获取请求头数据

request与请求头相关的方法有：

- `String getHeader(String name)：`获取指定名称的请求头；

- `Enumeration getHeaderNames()：`获取所有请求头名称；

- `int getIntHeader(String name)：`获取值为int类型的请求头。


## request获取请求相关的其它方法
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

## request获取请求参数

最为常见的客户端传递参数方式有两种：

- 浏览器地址栏直接输入：一定是GET请求；

- 超链接：一定是GET请求；

- 表单：可以是GET，也可以是POST，这取决与<form>的method属性值；

 

### GET请求和POST请求的区别

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

### 请求转发和请求包含

无论是请求转发还是请求包含，都表示由多个Servlet共同来处理一个请求。例如Servlet1来处理请求，然后Servlet1又转发给Servlet2来继续处理这个请求。


请求转发和请求包含`RequestDispatcher rd = request.getRequestDispatcher("/MyServlet");` 使用`request`获取`RequestDispatcher`对象，方法的参数是被转发或包含的`Servlet`的`Servlet`路径

- 请求转发：`rd.forward(request,response)`;
- 请求包含：`rd.include(request,response)`;

有时一个请求需要多个`Servlet`协作才能完成，所以需要在一个`Servlet`跳到另一个`Servlet`！

- 一个请求跨多个`Servlet`，需要使用转发和包含。
- 请求转发：由下一个`Servlet`完成响应体！当前`Servlet`可以设置响应头！（留头不留体）即当前`Servlet`设置的相应头有效，相应体无效。
- 请求包含：由两个`Servlet`共同未完成响应体！（留头又留体）都有效。 
- 无论是请求转发还是请求包含，都在一个请求范围内！使用同一个`request`和`response`！


### 请求转发与请求包含比较

1. 如果在`AServlet`中请求转发到`BServlet`，那么在`AServlet`中就不允许再输出响应体，即不能再使用`response.getWriter()`和`response.getOutputStream()`向客户端输出，这一工作应该由`BServlet`来完成；如果是使用请求包含，那么没有这个限制；

2. 请求转发虽然不能输出响应体，但还是可以设置响应头的，例如：`response.setContentType(”text/html;charset=utf-8”)`;

3. 请求包含大多是应用在JSP页面中，完成多页面的合并；

4. 请求转发大多是应用在`Servlet`中，转发目标大多是JSP页面；

![图例](https://img-blog.csdn.net/20160816102052342?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

### 请求转发与重定向比较

- 请求转发是一个请求，而重定向是两个请求；

- 请求转发后浏览器地址栏不会有变化，而重定向会有变化，因为重定向是两个请求；

- 请求转发的目标只能是本应用中的资源，重定向的目标可以是其他应用；

- 请求转发对`AServlet`和`BServlet`的请求方法是相同的，即要么都是GET，要么都是POST，因为请求转发是一个请求；

- 重定向的第二个请求一定是GET；

# response

## 什么是response？

`response`是`Servlet.service`方法的一个参数，类型为`javax.servlet.http.HttpServletResponse`。在客户端发出每个请求时，服务器都会创建一个response对象，并传入给`Servlet.service()`方法。`response`对象是用来对客户端进行响应的，这说明在`service()`方法中使用`response`对象可以完成对客户端的响应工作。

`response`对象的功能分为以下四种：

（1）设置响应头信息

（2）发送状态码

（3）设置响应正文

（4）重定向


## response响应正文

`response`是响应对象，向客户端输出响应正文（响应体）可以使用response的响应流，repsonse一共提供了两个响应流对象：

- `PrintWriter out = response.getWriter()`：获取字符流；

- `ServletOutputStreamout = response.getOutputStream()`：获取字节流；

 
当然，如果响应正文内容为字符，那么使用`response.getWriter()`，如果响应内容是字节，例如下载时，那么可以使用`response.getOutputStream()`。

注意，在一个请求中，不能同时使用这两个流！也就是说，要么你使用`repsonse.getWriter()`，要么使用`response.getOutputStream()`，但不能同时使用这两个流。不然会抛出`illegalStateException`异常。

### 字符响应流

#### 字符编码

在使用`response.getWriter()`时需要注意默认字符编码为`ISO-8859-1`，如果希望设置字符流的字符编码为`utf-8`，可以使用`response.setCharaceterEncoding("utf-8")`来设置。这样可以保证输出给客户端的字符都是使用`UTF-8`编码的！

但客户端浏览器并不知道响应数据是什么编码的！如果希望通知客户端使用`UTF-8`来解读响应数据，那么还是使用`response.setContentType("text/html;charset=utf-8")`方法比较好，因为这个方法不只会调用`response.setCharaceterEncoding("utf-8")`，还会设置`content-type`响应头，客户端浏览器会使用`content-type`头来解读响应数据。

 

#### 缓冲区

`response.getWriter()`是`PrintWriter`类型，所以它有缓冲区，缓冲区的默认大小为8KB。也就是说，在响应数据没有输出8KB之前，数据都是存放在缓冲区中，而不会立刻发送到客户端。当`Servlet`执行结束后，服务器才会去刷新流，使缓冲区中的数据发送到客户端。

如果希望响应数据马上发送给客户端：

向流中写入大于8KB的数据；

调用response.flushBuffer()方法来手动刷新缓冲区；

## 设置响应头信息

可以使用`response`对象的`setHeader()`方法来设置响应头！

使用该方法设置的响应头最终会发送给客户端浏览器！

（1）`response.setHeader("content-type", "text/html;charset=utf-8")`：设置`content-type`响应头，该头的作用是告诉浏览器响应内容为html类型，编码为`utf-8`。而且同时会设置`response`的字符流编码为`utf-8`，即`response.setCharaceterEncoding("utf-8")`；

（2）`response.setHeader("Refresh","5; URL=http://www.baidu.com")`：5秒后自动跳转到百度主页。



## 设置状态码及其他方法

（1）`response.setContentType("text/html;charset=utf-8")`：等同与调用`response.setHeader("content-type", "text/html;charset=utf-8")`；
（2）`response.setCharacterEncoding("utf-8")`：设置字符响应流的字符编码为`utf-8`；
（3）`response.setStatus(200)`：设置状态码；
（4）`response.sendError(404,"您要查找的资源不存在”)`：当发送错误状态码时，`Tomcat`会跳转到固定的错误页面去，但可以显示错误信息。

## 5、重定向

### 什么是重定向（两次请求）

当你访问`http://www.sun.com`时，你会发现浏览器地址栏中的URL会变成`http://www.Oracle.com/us/sun/index.htm`，这就是重定向了。重定向是服务器通知浏览器去访问另一个地址，即再发出另一个请求。

![重定向](https://img-blog.csdn.net/20160816095908794?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)


### 如何完成重定向？

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

# 案例

## 用户登录案例需求

1. 编写login.html登录页面，包含username & password 两个输入框
2. 使用Druid数据库连接池技术,操作mysql，day14数据库中user表
3. 使用JdbcTemplate技术封装JDBC
4. 登录成功跳转到SuccessServlet展示：登录成功！用户名,欢迎您
5. 登录失败跳转到FailServlet展示：登录失败，用户名或密码错误

## 开发步骤
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


