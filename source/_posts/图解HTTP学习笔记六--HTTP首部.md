---
title: 图解HTTP学习笔记(六)：HTTP首部
date: 2018-01-12 18:00:00
tags:
 - 计算机网络
---


> HTTP 协议的请求和响应报文中必定包含 HTTP 首部。首部内容为客户端和服务器分别处理请求和响应提供所需要的信息。报文结构：

![](http://img.yancongwen.cn/18-4-13/85199769.jpg)

## 一、首部字段
>HTTP/1.1 规范定义了 47 种首部字段。HTTP 首部字段根据实际用途被分为以下 4 种类型：

- 通用首部字段：请求报文和响应报文双方都会使用的首部  

首部字段名 | 说明
---|---
Cache-Control | 控制缓存的行为
Connection | 逐跳首部、连接的管理
Date | 创建报文的日期时间
Program | 报文指令
Trailer | 报文末端的首部一览
Transfer-Encoding | 指定报文主体的传输编码方式
Upgrade	 | 升级为其他协议
Via	 | 代理服务器的相关信息
Warning	 | 错误通知

- 请求首部字段：请求报文中，用于补充请求的附加信息、客户端信息、对响应内容相关的优先级等。  

首部字段名 | 说明
---|---
Accept | 用户代理可处理的媒体类型
Accept-Charset | 优先的字符集
Accept-Encoding | 优先的内容编码
Accept-Language | 优先的语言（自然语言）
Authorization | Web认证信息
Expect | 期待服务器的特定行为
From | 用户的电子邮箱地址
Host | 请求资源所在的服务器
If-Match | 比较实体标记（ETag）
If-Modified-Since | 比较资源的更新时间
If-None-Match | 比较实体标记（与If-Match相反）
If-Range | 资源未更新时发送实体Byte的范围请求
If-Unmodified-Since | 比较资源的更新时间（与If-Modified-Since相反）
Max-Forwards | 最大传输逐跳数
Proxy-Authorization | 代理服务器要求客户端的认证信息
Range | 实体的字节范围请求
Referer | 对请求中的URI的原始获取方
TE | 传输编码的优先级
User-Agent | HTTP客户端程序的信息

- 响应首部字段：响应报文中， 用于补充响应的附加信息、服务器信息，以及对客户端的附加要求等信息  

首部字段名 | 说明
---|---
Accept-Ranges | 是否接受字节范围请求
Age | 推算资源创建经过时间
Content-Disposition | 可以控制返回的资源是下载还是预览（图片）
ETag | 资源的匹配信息
Location | 令客户端重定向至指定URI
Proxy-Authenticate | 代理服务器对客户端的认证信息
Retry-After | 对再次发起请求的时机要求
Server | HTTP服务器的安装信息
Vary | 代理服务器缓存的管理信息
WWW-Authenticate | 服务器对客户端的认证信息

- 实体首部字段：包含在请求报文和响应报文中的实体部分所使用的首部，用于补充内容的更新时间等与实体相关的信息    

首部字段名 | 说明
---|---
Allow | 资源可支持的HTTP方法
Content-Encoding | 实体主体使用的编码方式
Content-Language | 实体主体的自然语言
Content-Length | 实体主体的大小（单位：字节）
Content-Location | 替换对应资源的URI
Content-MD5 | 实体主体的报文摘要
Content-Range | 实体主体的位置范围
Content-Type | 实体主体的媒体类型
Expires | 实体主体过期的日期时间
Last-Modified | 资源的最后修改日期时间 

## 二、通用首部字段

- 1、Cache-Control  
请求指令：  
![](http://img.yancongwen.cn/18-4-13/71727595.jpg)  
响应指令：  
![](http://img.yancongwen.cn/18-4-13/86078800.jpg)   

- 2、Connection 
    - 控制不再转发给代理的首部字段  
![](http://img.yancongwen.cn/18-4-13/40889356.jpg)
    - 管理持久连接
![](http://img.yancongwen.cn/18-4-13/58156556.jpg)
    - HTTP/1.1 版本的默认连接都是持久连接。为此，客户端会在持久连接上连续发送请求。当服务器端想明确断开连接时，则指定 Connection 首部字段的值为 Close。 
    - HTTP/1.1 之前的 HTTP 版本的默认连接都是非持久连接。为此，如果想在旧版本的 HTTP 协议上维持持续连接，则需要指定 Connection 首部字段的值为 Keep-Alive。

![](http://img.yancongwen.cn/18-4-13/9599479.jpg)

- 3、Data

- 4、Pragma

- 5、Trailer

- 6、Transfer-Encoding

- 7、Upgrade

- 8、Via
    > 报文经过代理或网关时，会先在首部字段 Via 中附加该服务器的信息，然后再进行转发。

- 9、Warning
    >该首部通常会告知用户一些与缓存相关的问题的警告

## 三、请求首部字段
- 1、Accept
    > Accept 首部字段可通知服务器，用户代理能够处理的媒体类型及媒体类型的相对优先级。

- 2、Accept-Charset
    > 用来通知服务器用户代理支持的字符集及字符集的相对优先顺序。另外，可一次性指定多种字符集。与首部字段 Accept 相同的是可用权重 q 值来表示相对优先级。

- 3、Accept-Encoding
    > 用来告知服务器用户代理支持的内容编码及 内容编码的优先级顺序

- 4、Accept-Language
    > 告知服务器用户代理能够处理的自然语言集（指中文或英文等），以及自然语言集的相对优先级。

- 5、Authorization
    > 是用来告知服务器，用户代理的认证信息（证书值）。通常，想要通过服务器认证的用户代理会在接收到返回的 401 状态码响应后，把首部字段 Authorization 加入请求中。

- 6、Expect
    > 告知服务器，期望出现的某种特定行为

- 7、From
    > 用来告知服务器使用用户代理的用户的电子邮件地址。通常，其使用目的就是为了显示搜索引擎等用户代理的负责人的 电子邮件联系方式。

- 8、Host
    > 告知服务器，请求的资源所处的互联网主机名和端口号。Host 首部字段在 HTTP/1.1 规范内是唯一一个必须被包含在请求内的首部字段。

- 9、If-Match
![](http://img.yancongwen.cn/18-4-13/8635584.jpg)
    > 形如 If-xxx 这种样式的请求首部字段，都可称为条件请求。服务器接收到附带条件的请求后，只有判断指定条件为真时，才会执行请求。        

    > 只有当 If-Match 的字段值跟 ETag 值匹配一致时，服务器才会接受请求

- 10、If-None-Match
    > 只有在 If-None-Match 的字段值与 ETag 值不一致时，可处理该请求

- 11、If-Modified-Since
    > 如果在 If-Modified-Since 字段指定的日期时间后，资源发生了更新，服务器会接受请求

- 12、If-Unmodified-Since
    > 如果在 If-Unmodified-Since 字段指定的日期时间后，资源没有发生更新，服务器才会接受请求

- 13、If-Range
    > 它告知服务器若指定的 IfRange 字段值（ETag 值或者时间）和请求资源的 ETag 值或时间相一 致时，则作为范围请求处理。反之，则返回全体资源。

- 14、Max-Forwards
    > 通过 TRACE 方法或 OPTIONS 方法，发送包含首部字段 MaxForwards 的请求时，该字段以十进制整数形式指定可经过的服务器最大数目。服务器在往下一个服务器转发请求之前，Max-Forwards 的 值减 1 后重新赋值。当服务器接收到Max-Forwards 值为 0 的请求 时，则不再进行转发，而是直接返回响应。

- 15、Proxy-Authorization
    > 接收到从代理服务器发来的认证质询时，客户端会发送包含首部字段 Proxy-Authorization 的请求，以告知服务器认证所需要的信息。 

- 16、Range
    > 可告知服务器资源的指定范围。接收到附带 Range 首部字段请求的服务器，会在处理请求之后返回状 态码为 206 Partial Content 的响应。无法处理该范围请求时，则会返回状态码 200 OK 的响应及全部资源。

- 17、Referer
    > 告知服务器请求的原始资源的 URI。    
    > *Referer 的正确的拼写应该是 Referrer，但不知为何，大家一直沿用这个错误的拼写。*

- 18、TE
    > 告知服务器客户端能够处理响应的传输编码方式及相对优先级。它和首部字段 Accept-Encoding 的功能很相像，但是用于传输编码。

- 19、User-Agent
    > 将创建请求的浏览器和用户代理名称等信息传达给服务器。

## 四、响应首部字段

- 1、Accept-Ranges
    > 用来告知客户端服务器是否能处理范围请求，以指定获取服务器端某个部分的资源。可指定的字段值有两种，可处理范围请求时指定其为 bytes，反之则指定其为 none。 

- 2、Age
    > 告知客户端，源服务器在多久前创建了响应

- 3、ETag
    > 告知客户端实体标识。例如，当使用中文版的浏览器访问 http://www.google.com/ 时，就会返回中文版对应的资源，而使用英文版的浏览器访问时，则会返回英文版对应的资源。两者的 URI 是相同的，所以仅凭 URI 指定缓存的资源是相当困难的。若在下 载过程中出现连接中断、再连接的情况，都会依照 ETag 值来指定资源。

- 4、Location
    > 将响应接收方引导至某个与请求 URI 位置不同的资源。基本上，该字段会配合 3xx ：Redirection 的响应，提供重定向的 URI。 几乎所有的浏览器在接收到包含首部字段 Location 的响应后，都会强制性地尝试对已提示的重定向资源的访问。

- 5、Proxy-Authenticate
    > 把由代理服务器所要求的认证信息发送给客户端。

- 6、Retry-After
    > 告知客户端应该在多久之后再次发送请求。主要配合状态码 503 Service Unavailable 响应，或 3xx Redirect 响应一起使用。

- 7、Server
    > 告知客户端当前服务器上安装的 HTTP 服务器应用程序的信息

- 8、Vary
    > 可对缓存进行控制。

- 9、WWW-Authenticate
    > 用于 HTTP 访问认证。它会告知客户端适用于访问请求 URI 所指定资源的认证方案（Basic 或是 Digest）和带参数提示的质询（challenge）。状态码 401 Unauthorized 响应中， 肯定带有首部字段 WWW-Authenticate。

## 五、实体首部字段

- 1、Allow
    > 用于通知客户端能够支持 Request-URI 指定资源的所 有 HTTP 方法。当服务器接收到不支持的 HTTP 方法时，会以状态码 405 Method Not Allowed 作为响应返回。与此同时，还会把所有能支持的 HTTP 方法写入首部字段 Allow 后返回。 

- 2、Content-Encoding
    > 告知客户端服务器对实体的主体部分选 用的内容编码方式。     
    > 主要采用以下 4 种内容编码的方式: gzip、compress、deflate、identity 

- 3、Content-Language
    > 实体主体使用的自然语言 

- 4、Content-Length
    > 实体主体部分的大小。

- 5、Content-Location
    > 给出与报文主体部分相对应的 URI。和首部字段 Location 不同，Content-Location 表示的是报文主体返回资源对应的 URI。 

- 6、Content-MD5
    > 是一串由 MD5 算法生成的值，其目的在于检查报文主体在传输过程中是否保持完整，> 以及确认传输到达

- 7、Content-Range
    > 针对范围请求，告知客户端作为响应返回的实体的哪个部分符合范围请求

- 8、Content-Type
    > 了实体主体内对象的媒体类型

- 9、Expires
    > 将资源失效的日期告知客户端

- 10、Last-Modified
    > 资源最终修改的时间

## 六、为 Cookie 服务的首部字段 

首部字段名 | 说明 | 首部类型
---|---|---
Set-Cookie | 开始状态管理所使用的Cookie信息 | 响应首部字段
Cookie | 服务器接收到的Cookie信息 | 请求首部字段

- 1、Set-Cookie     
    >属性表： 

属性 | 说明 
---|---
NAME=VALUE | 赋予Cookie的名称和其值（必需项）
expires=DATE | Cookie的有效期（若不明确指定则默认为浏览器关闭前为止）
path=PATH | 将服务器上的文件目录作为Cookie的适用对象（若不指定则默认为文档所在的文件目录）
domain=域名 | 作为Cookie适用对象的域名（若不指定则默认为创建Cookie的服务器的域名）
Secure | 仅在HTTPS完全通信时才会发送Cookie
HttpOnly | 加以限制，使Cookie不能被JavaScript脚本访问

- 2、Cookie
    > 告知服务器，当客户端想获得 HTTP 状态管理支持时，就会在请求中包含从服务器接收到的 Cookie。接收到多个 Cookie 时，同样可以以多个 Cookie 形式发送。 

## 七、其他首部字段
HTTP 首部字段是可以自行扩展的。所以在 Web 服务器和浏览器的应用上，会出现各种非标准的首部字段。如：
- 1、X-Frame-Options 
- 2、X-XSS-Protection 
- 3、DNT
- 4、P3P
