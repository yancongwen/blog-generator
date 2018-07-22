title: Hexo搭建博客
author: Yan Congwen
tags:
  - 工具
categories: []
date: 2018-07-16 11:39:00
---
> 	本文主要记录一下本人使用 hexo + github 搭建个人博客的流程及hexo使用技巧和相关辅助工具。

## 1.Hexo搭建博客
### 1.1 Hexo介绍
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，可利用靓丽的主题生成静态网页。Hexo可以托管到github等代码托管平台上，开启page功能就可以访问。
### 1.2 第一篇博客	
- 安装hexo	
```
$ npm install -g hexo-cli
```
- 新建项目	
```
$ mkdir filename && cd filename  // 创建并进入一个目录
$ hexo init  // 初始化
$ hexo install  // 安装依赖包
```
- 生成页面	
```
$ hexo generate
```
- 部署	
```
$ hexo server
```
第一篇博客就搭建完成了。访问[http://localhost:4000]() 就可看到你的博客

### 1.3 github部署	
将生成的博客页面部署到github上就可以让别人访问了。
- 新建github仓库，仓库名要和用户名一样
- 修改配置文件_config.yml,如下，设置github仓库的ssh地址（可以同时部署到码云gitee等其他平台上）	
```
deploy: 		
  type: git		
  repo: 		
    github: git@github.com:username/username.github.io.git	
    gitee: git@gitee.com:username/username.git	
  branch: master	
```
- 访问 [http://username.github.io.]()就是你的博客了
- 还可以设置自定义域名

### 1.4 主题设置
hexo提供了很多主题，更换主题也比较简单
- 第一步，克隆主题到本地 themes目录下
- 第二步，修改配置文件_config.yml下的them项就好了

### 1.5 使用流程
hexo写博客的一般流程是下面这样的：
```
hexo new title // 新建文章	
hexo g      // 文章写好之后生成页面
hexo s     // 开启本地服务器来预览页面
hexo d     // 部署	
```

## 2 开启HTTPS	
近年来Google一直在力推HTTPS加密协议，替换HTTP协议，Chrome浏览器68版本更是直接将所有的HTTP页面都标上“不安全”标签。虽然个人博客不会涉及账号密码登录泄露等问题，但为了获取浏览器的信任，开启HTTPS还是很有必要的。HTTPS协议要求整个页面所引用的和加载的资源必须也为HTTPS协议方可。
- Github开启HTTPS	
直接在博客仓库下的设置项中找到 Enforce HTTPS选项打钩即可 
- 申请免费SSL证书	
如果绑定了个人域名，需要申请SSL证书。腾讯云里可以申请免费的证书。
- 七牛云开启HTTPS	
七牛云用于存储博客的图片、视频等资源。将申请的SSL证书导入七牛云，然后开启HTTPS服务。

## 3 Hexo-admin管理博客
hexo-admin是一款帮助我们管理文章的插件，比较实用。如下所示，只要我们跑起来server，就可以访问[http://localhost:4000/admin/]()了，这个页面就是我们管理文章的页面了。不过deploy部署命令有点问题。	
```
npm install --save hexo-admin
hexo server -d
open http://localhost:4000/admin/
```

## 4 多终端使用	
有时候可能想在不同的电脑写文章，所以我们需要将博客的生成代码做一下备份。「你的用户名.github.io」上保存的只是你的博客，并没有保存「生成博客的程序代码」，你需要再创建一个名为 blog-generator 的空仓库，用来保存「生成博客的程序代码」。	
以后每次 hexo deploy 完之后，博客就会更新；然后你还要要 add / commit /push 一下「生成博客的程序代码」，将源文件也更新一下。这样你在另一台电脑上就可以clone这份源码，同时部署相同的环境（node、git、hexo、hexo-admin），就可以写代码了。