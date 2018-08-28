title: 在WSL中开发Node.js
author: Yan Congwen
tags:
  - linux
categories: []
date: 2018-08-28 17:19:00
---
### WSL 介绍
- WSL(Windows Subsystem for Linux) 适用于Linux的Windows子系统，有了它，不要再安装臃肿的Vmware和VirtualBox等虚机机系统，就可以直接在Windows上体验原生的Linux应用了，甚至还有图形界面！
- WSL是Win10提供的功能，默认关闭，需要去功能管理中开启WSL功能并重启计算机；然后在 Microsoft Store 中搜索 linux 或者 wsl ，会出现几个版本的linux系统供选择，直接安装想要的linux 发型版本即可。我这里安装的是 Ubuntu 18.04.1 LTS，大小约600MB，安装是一键安装的，安装完成直接点击图标即进入linux命令窗口。
- WSL 安装的Linux子系统，拥有独立的目录系统，其目录在C盘中：`C:\Users\username\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs` 。虽然我们能找到这个目录，但是请不要在Windos中去操作这里的文件！
- 个人理解，WSL安装的linux系统，其实仅仅是给了我们一个linux环境，其任然和Winddows系统共享计算机硬件，共享很多东西，比如磁盘、网络端口，linux中的localhost和windows中的localhost一致的。

### 基础环境安装
安装的Ubuntu自带git、node，但是版本较低，需要升级。具体方法请自行百度。
- git	
	git 需要做一些简单的配置，想要以SSH方式连接远程仓库还要生成SSH Key并将公钥配置到远程仓库。这里要注意的是用户权限问题，在linux中不同用户创建的SSH Key并不相同。请看[另一片文章](https://yancongwen.cn/2018/08/23/Error-Permission-denied-publickey/)。
- node
- yarn
- npm

### 开发模式
开始，我一直疑虑在WSL中应该以怎样的方式进行node开发。使用vim写代码对于我这种菜鸟还是太费力了，难道我还要在linux中再安装一下图形界面，然后再安装VSCode？不不不。还有一种方式，就是直接使用Windows中的VSCode打开Linux目录下的node项目，也就是直接打开上文提到的藏的很深的那个C盘目录下的项目，但是这种方式也很不优雅，一方面，我们使用window的编辑器去编辑改变linux中的文件，另一方面，我们要在linux中去执行node、yarn、git等命令，并且不能使用VScode去执行命令，不能使用VSCode去调试程序。

### 建立软连接
如上文提及，我们使用VSCode去编辑Linux目录中项目，这个目录藏在C盘很深的位置，不仅占用C盘空间，还不方便管理，可以使用建立软连接的方式来解决。首选我们来看一下什么是软连接、硬连接：	
- 软连接：	
	也叫符号连接（Symbolic Link），软链接文件类似于Windows的快捷方式，它实际上是一个特殊的文件。在符号连接中，文件实际上是一个文本文件，其中包含的文本就是连接的另一文件的位置。	
- 硬连接：	
	硬连接指通过索引节点来进行连接。在Linux的文件系统中，保存在磁盘分区中的文件不管是什么类型都给它分配一个编号，称为索引节点号(Inode Index)。在Linux中，多个文件名指向同一索引节点是存在的。一般这种连接就是硬连接。硬连接的作用是允许一个文件拥有多个有效路径名，这样用户就可以建立硬连接到重要文件，以防止“误删”的功能。其原因如上所述，因为对应该目录的索引节点有一个以上的连接。只删除一个连接并不影响索引节点本身和其它的连接，只有当最后一个连接被删除后，文件的数据块及目录的连接才会被释放。也就是说，文件真正删除的条件是与之相关的所有硬连接文件均被删除。

我们可以以建立软连接的方式，将F盘的开发目录连接到linux的目录下，这样既可以方便管理开发项目，也可以节省C盘空间占用。
- Linux ln 命令创建连接
	- 命令形式如下： `ln  (选项) [源文件] [文件连接]`，创建软连接：`ln -s \mnt\f\wsl-dev \home\yancongwen\develop`	 。以上命令就创建了一个软连接，将F盘的目录 wsl-dev 连接到了linux用户目录下的develop，这样我们就可以从linux中的develop访问F盘的开发目录，在linux中，develop目录就形同是一个文件夹，cd 命令可以进入访问。关于ln 命令的更多说明可以看[这里](http://man.linuxde.net/ln)。
    - 这里也记录一下我踩过的坑：
    	- 1、ln 命令前一个参数是真实的数据存储所在，后一个参数是连接文件，不要搞反了；刚开始我就是在F盘创建的连接，而目录在linux目录下，显然是不合理的，也没什么用处；
        - 2、源文件目录和连接文件都一定要采用绝对路径，不要采用`~\develop`这样的相对路径；我一开始没注意到 `~\`就是相对路径，所以创建的连接文件一直进不去，把我郁闷坏了。

- windows mklink 命令创建连接	
windows中同样支持创建软连接和硬连接，使用的是mklink命令。一开始我使用的就是mklink创建的软连接：`mklink /D  C:\Users\username\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs\home\yancongwen\develop   F:\wsl-dev` （注意，这里前一个路径是连接，后一个连接是源文件），然而，才linux系统中，根本就识别不了这个连接，cd 命令进不去。所以不要使用windows的连接命令去连接linux目录。
 
 



**【参考】**
- [Win+Linux单系统解决方案——WSL（入门篇）](https://www.jianshu.com/p/6b02948b3d37)
- [理解 Linux 的硬链接与软链接](https://www.ibm.com/developerworks/cn/linux/l-cn-hardandsymb-links/index.html)
- [linux 创建连接命令 ln -s 软链接](https://www.cnblogs.com/kex1n/p/5193826.html)