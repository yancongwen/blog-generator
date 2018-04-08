---
title: 命令行基础
date: 208-01-09 22:00:00
tags:
 - 计算机网络
---


> HTTP，即 超文本传输协议 (HyperText Transfer Protocol)。
##  HTTP 方法
![](http://ww1.sinaimg.cn/large/9f4be9b7gy1fn990ea9saj20j30anq2x.jpg)

## 持久连接
&emsp;&emsp;持久连接旨在建立 1 次 TCP 连接后进行多次请求和响应的交互。在 HTTP/1.1 中，所有的连接默认都是持久连接，但在 HTTP/1.0 内并 未标准化。
## 管线化
&emsp;&emsp;持久连接使得多数请求以管线化（pipelining）方式发送成为可能。从前发送请求后需等待并收到响应，才能发送下一个请求。管线化技术出现后，不用等待响应亦可直接发送下一个请求。这样就能够做到同时并行发送多个请求，而不需要一个接一个地等待响应了。
## 使用 Cookie 的状态管理
&emsp;&emsp;HTTP 是无状态协议，它不对之前发生过的请求和响应的状态进行管理。Cookie 技术通过在请求和响应报文中写入 Cookie 信息来控制客户端的状态。  
&emsp;&emsp;Cookie 会根据从服务器端发送的响应报文内的一个叫做 Set-Cookie 的首部字段信息，通知客户端保存 Cookie。当下次客户端再往该服务器发送请求时，客户端会自动在请求报文中加入 Cookie 值后发送出去。
