---
title: 命令行基础
date: 208-01-08 22:00:00
tags:
 - 计算机网络
---

# 统一资源标识符 URI
- 统一资源标识符 URI (Uniform Resource Identifier)
    > URI 就是标识某一互联网资源的字符串。  
    URI可被视为定位符（URL），名称（URN）或两者兼备。
- 统一资源定位符 URL (Universal Resource Locator)
    > URL是URI的最常见形式，它标识一个互联网资源，也被称为 Web 地址。 URL 是 URI 的子集。例如：

    ```
    https://developer.mozilla.org
    https://developer.mozilla.org/en-US/docs/Learn/
    https://developer.mozilla.org/en-US/search?q=URL
    ftp://ftp.is.co.za/rfc/rfc1808.txt
    mailto:John.Doe@example.com
    ```
- 统一资源名称 URN (Universal Resource Name)   
    > 通过特定命名空间中的唯一名称来标识资源。例如：  

    ```
    urn:isbn:9780141036144
    urn:ietf:rfc:7230
    上面两个 URN 分别标识了下面的资源：
        - 乔治·奥威尔所著的《1984》
        - IETF规范7230，超文本传输协议 (HTTP/1.1)：Message Syntax and Routing.
    ```
    
- 三者关系
    > URL和URN都是URI的子集。统一资源名（URN）如同一个人的名称，而统一资源定位符（URL）代表一个人的住址。   
    在[知乎](https://www.zhihu.com/question/21950864)上有人这么回答：原来URI包括URL和URN，后来URN没流行起来，导致几乎目前所有的URI都是URL。

![](http://ww1.sinaimg.cn/large/9f4be9b7gy1fn95xb3o33j208204cmwx.jpg)

# URI 格式 
![](http://ww1.sinaimg.cn/large/9f4be9b7gy1fn974z54thj20p4057gmd.jpg)
- 方案或协议：“http://”告诉浏览器使用何种协议。对于大部分 Web 资源，通常使用 HTTP 协议或其安全版本，HTTPS 协议。还有：ftp、data、file、mailto、tel等协议。
- 服务器地址： IPv4、IPV6地址或域名。
- 端口号：若使用默认端口号可以省略，默认端口（HTTP为80，HTTPS为443）。
- 路径：资源的路径。
- 查询字符串：是提供给 Web 服务器的额外参数，这些参数是用 & 符号分隔的键/值对列表。
- 片段标识符： #ch1 是资源本身的某一部分的一个锚点。锚点代表资源内的一种“书签”，它给予浏览器显示位于该“加书签”点的内容的指示。 例如，在HTML文档上，浏览器将滚动到定义锚点的那个点上；在视频或音频文档上，浏览器将转到锚点代表的那个时间。值得注意的是 # 号后面的部分，也称为片段标识符，永远不会与请求一起发送到服务器。

参考：  
1. [Mozilla中统一资源标识符的语法](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics_of_HTTP/Identifying_resources_on_the_Web#%E7%BB%9F%E4%B8%80%E8%B5%84%E6%BA%90%E6%A0%87%E8%AF%86%E7%AC%A6%E7%9A%84%E8%AF%AD%E6%B3%95_(URI))  
2. [URL和URI的区别](http://www.cnblogs.com/hust-ghtao/p/4724885.html)