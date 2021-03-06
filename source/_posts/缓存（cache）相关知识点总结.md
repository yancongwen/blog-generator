title: 缓存（cache）相关知识点总结
author: Yan Congwen
tags:
  - Javascript
  - 计算机网络
categories: []
date: 2018-10-16 21:07:00
---
# 缓存（cache）相关知识点总结

## Cache-Control

Cache-Control: max-age=1000 ，设置的是 1000 s 后缓存失效；在缓存有效期内不再请求数据；
一般设置很长很长一段时间，如一年，设置十年；每次版本迭代之后，修改文件名就行了，这样缓存就失效了，会请求新数据，一般不回缓存 html 文件。

## Expire

设置缓存过期的时间点，超过这个时间点就请求，一般推荐使用 Cache-Control；

## ETag

通过文件的 MD5 值来判断文件是否改变，改变就返回数据，不改变就不返回；不管数据变不变，都要发送请求；
任然要发送请求，只是不返回数据而已，所以效率不如 Cache-Control， Cache-Control 直接就不请求数据。

- MD5 是什么
- 缓存与 304 的区别
  - 缓存没有请求。
  - 304 有请求，有响应，但是响应没有第四部分。

### 参考

- [一文读懂前端缓存](https://mp.weixin.qq.com/s/e42vFNPPxt7zcd1N0Li7pg)
