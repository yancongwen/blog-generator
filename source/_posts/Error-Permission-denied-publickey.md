title: 'Error: Permission denied (publickey)'
author: Yan Congwen
tags:
  - git
  - linux
categories: []
date: 2018-08-23 19:37:00
---
## Git Error: Permission denied (publickey)

> 最近接触到一个nodejs后端服务项目，项目需要运行在linux环境中，经leader推荐，决定使用Win10的WSL功能，安装了Ubuntu 18.04。在Ubuntu中配置git中遇到了以下问题。

### 问题描述

Ubuntu中自带了git，但是使用之前需要做一些配置。首先要做的事情就是设置你的名字和邮件地址，此外，使用ssh连接github或者gitlab这些远程仓库需要配置公钥。我按照如下命令生成了SSH Key，生成的密钥在 `~/.ssh` 文件夹下，将公钥复制到github中即可。
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

然而，当我执行 `sudo git clone git@gitlab.com:***.git` 时，就失败了，显示如下信息:
```
git@gitlab.com: Permission denied (publickey).
fatal: Could not read from remote repository.
```	

### 问题解决

上面的信息显示应该是公钥出了问题。反复确认，我的公钥确实没有配置错误啊，而且执行`ssh git@gitlab.com`的时候确实显示SSH链接已经建立了呀。然而，当我执行`sudo ssh git@gitlab.com`的时候，同样抛出了`Permission denied (publickey)`，说明可能和`sudo` 有关。	
反反复复查资料，发现也有其他人出现了这个[问题](https://gitlab.com/gitlab-com/support-forum/issues/171),但是按照里面的方法我并没有解决问题。	
最后，还是在github的[帮助文档](https://help.github.com/articles/error-permission-denied-publickey/#platform-linux)找到了问题所在。原来，在git命令前加上sudo权限后，使用的密匙就应该是 sudo权限下生成的 SSH Key，这个SSH Key 在`\root\.ssh`目录下，而我们配置的是`~/.ssh` 目录下的SSH Key。	
所以我所做的，就是使用sudo权限重新生成了SSH Key，然后将`\root\.ssh`目录下的公钥配置到github中，这样再执行`sudo git`这样的命令就OK了	




**参考**
- [Generating a new SSH key and adding it to the ssh-agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#platform-linux)
- [Error: Permission denied (publickey)](https://help.github.com/articles/error-permission-denied-publickey/#platform-linux)