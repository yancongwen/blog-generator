---
title: HTTP总结（前端开发中的常识性问题）
date: 2018-04-11 13:33:00
tags:
 - 计算机网络
---

## 1. TCP/IP 简介
- 首先应该理解 TCP/IP 协议族中的四个分层：应用层、传输层、网络层、数据链路层，详细请看另一篇[博客](http://blog.yancongwen.cn/2018/01/08/%E5%9B%BE%E8%A7%A3HTTP%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%EF%BC%88%E4%B8%80%EF%BC%89%EF%BC%9A%E7%BD%91%E7%BB%9C%E5%9F%BA%E7%A1%80/)。
    - HTTP 位于应用层，负责生成或解析报文
    - TCP、UDP 位于传输层，负责将报文方便、可靠得传输
    - IP 位于网络层，负责搜索地址、路由中转、传输
    - 数据链路层是硬件设备

## 2. HTTP
- HyperText Transfer Protocol，超文本转移协议，是TCP/IP 协议族的子集，用于客户端和 服务器之间的通信。详细请看其他文章：[HTTP基础](http://blog.yancongwen.cn/2018/01/09/%E5%9B%BE%E8%A7%A3HTTP%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%EF%BC%88%E4%B8%89%EF%BC%89%EF%BC%9AHTTP%E5%9F%BA%E7%A1%80/)、[HTTP报文](http://blog.yancongwen.cn/2018/01/10/%E5%9B%BE%E8%A7%A3HTTP%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%EF%BC%88%E5%9B%9B%EF%BC%89%EF%BC%9AHTTP%E6%8A%A5%E6%96%87/)、[HTTP状态码](http://blog.yancongwen.cn/2018/01/11/%E5%9B%BE%E8%A7%A3HTTP%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%EF%BC%88%E4%BA%94%EF%BC%89%EF%BC%9AHTTP%E7%8A%B6%E6%80%81%E7%A0%81/)、[HTTP首部](http://blog.yancongwen.cn/2018/01/12/%E5%9B%BE%E8%A7%A3HTTP%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%EF%BC%88%E5%85%AD%EF%BC%89%EF%BC%9AHTTP%E9%A6%96%E9%83%A8/)。
- 请求报文
![](http://img.yancongwen.cn/18-4-13/64617528.jpg)
- 响应报文
![](http://img.yancongwen.cn/18-4-13/27833394.jpg)
- Chrome开发者工具查看 HTTP 报文
  - ① 打开 Network    
  - ② 地址栏输入网址   
  - ③ 在 Network 点击，查看 Request/Response Headers，点击「view source」    

## 3. TCP、UDP 
- TCP（三次握手，四次挥手）
    - 可靠：三次握手、四次挥手；
    - 字节流服务：为了方便传输，将大块数据分割成以报文段为单位的数据包进行管理；
    - 可靠、面向连接、相对 UDP 较慢；
- UDP 
    - 不可靠，不面向连接、相对 TCP 较快

## 4. curl 命令的使用
- 在Linux中curl是一个利用URL规则在命令行下工作的文件传输工具，可以说是一款很强大的http命令行工具。
- 语法：
    ```
    # curl [option] [url]
    ```
- 常见参数
    - -s ：silent，安静模式，不显示过程或错误信息
    - -v ：verbose，显示请求和响应报文
    - -I ：head，仅仅显示响应报文，不显示请求返回的内容
    - -i ：include，显示响应报文
    - -H ：header，增加请求时的请求头信息
    - -X ：request，自定义请求方法，默认为GET
    - -d ：data，定义POST请求中发送的数据
    - -A ：agent，自定义User-Agent用户代理
    - -o : output，保存到指定文件
- 示例
    
    ```
    // 最简单用法，显示请求过程和请求结果
    $ curl www.baidu.com    
    
    // 最常用用法，显示请求报文、响应报文、请求结果
    $ curl -s -v www.baidu.com  
    
    // 自定义用POST方法进行HTTP通信，并添加自定义请求头
    $ curl -X POST -s -v -H "Frank: xxx" -- "https://www.baidu.com"   
    
    // 发送数据
    $ curl -X POST -d "1234567890" -s -v -H "Frank: xxx" -- "https://www.baidu.com" 
    
    // 下载文件保存到本地指定文件
    $ curl http://www.baidu.com > index.html
    $ curl -o index.html http://www.baidu.com
    ```