---
title: 命令行基础
date: 208-01-12 20:00:00
tags:
 - 计算机网络
---


## HTTP 的缺点
- 通信使用明文（不加密），内容可能会被窃听；
- 不验证通信方的身份，因此有可能遭遇伪装（ DoS 攻击，拒绝服务攻击）；
- 无法证明报文的完整性，所以有可能已遭篡改（中间人攻击，MITM）；

## HTTPS =  HTTP + 加密 + 认证 + 完整性保护
### 1、HTTPS 是身披 SSL 外壳的 HTTP 
&emsp;&emsp;HTTPS 并非是应用层的一种新协议。只是 HTTP 通信接口部分用 SSL（Secure Socket Layer）和 TLS（Transport Layer Security）协议代替而已。通常，HTTP 直接和 TCP 通信。当使用 SSL 时，则演变成先和 SSL 通信，再由 SSL 和 TCP 通信了。简言之，所谓 HTTPS，其实就是身披 SSL 协议这层外壳的 HTTP。   
&emsp;&emsp;SSL 是独立于 HTTP 的协议，所以不光是 HTTP 协议，其他运行在应用层的 SMTP 和 Telnet 等协议均可配合 SSL 协议使用。可以说 SSL 是 当今世界上应用最为广泛的网络安全技术。

### 2、相互交换密钥的公开密钥加密技术 
- 共享密钥加密  
![](http://ww1.sinaimg.cn/large/9f4be9b7gy1fncnj1jvymj20j10co3zf.jpg)
- 使用两把密钥的公开密钥加密        
![](http://ww1.sinaimg.cn/large/9f4be9b7gy1fncnilv6nvj20jk0ffaav.jpg)
- HTTPS 采用混合加密机制        
![](http://ww1.sinaimg.cn/large/9f4be9b7gy1fncnidgpvmj20gp0edjt7.jpg)

### 3、证明公开密钥正确性的证书
&emsp;&emsp;遗憾的是，公开密钥加密方式还是存在一些问题的。那就是无法证明公开密钥本身就是货真价实的公开密钥。为了解决上述问题，可以使用由数字证书认证机构（CA，Certificate Authority）和其相关机关颁发的公开密钥证书。   
![](http://ww1.sinaimg.cn/large/9f4be9b7gy1fncnm6hz2vj20lk0glmyw.jpg)

### 4、HTTPS 的安全通信机制
![](http://ww1.sinaimg.cn/large/9f4be9b7gy1fncns8xcsaj20lk0didh7.jpg)

### 5、HTTPS 缺点
- 消耗更多 CPU 及内存等资源，导致处理速度变慢；
- 和HTTP相比，SSL 通信使通信量会增加；
- HTTPS 比 HTTP 要慢 2 到 100 倍；
- 证书必须向认 证机构（CA）购买；
