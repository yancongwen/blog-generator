title: Git基础
tags:
  - Git
date: 2018-04-15 21:37:08
---

## 1、工作区、暂存区、版本库、远程库
- 工作区（Working Directory）  
    就是你在电脑里能看到的目录
- 版本库（Repository）  
    工作区有一个隐藏目录.git就是版本库。
- 暂存区  
    Git 的版本库里存了很多东西，其中最重要的就是称为 stage（或者叫index）的暂存区，还有 Git 为我们自动创建的第一个分支 master，以及指向 maste r的一个指针叫HEAD。
- 远程库  
    指 github 或码云等 git 服务器上的版本库，也可以自己搭建 git 服务器。

## 2、常用命令
- git init：初始化一个Git仓库
- git add：把文件修改添加到暂存区，可反复多次使用，添加多个文件
    - git add -A   // 添加所有改动
    - git add *    //加新建文件和修改，但是不包括删除
    - git add .    //加新建文件和修改，但是不包括删除
    - git add -u   //加修改和删除，但是不包括新建文件
- git commit：提交更改，把暂存区的所有内容提交到当前分支
- git status：查看仓库当前的状态
  - -s：以简洁的形式显示
  - -b：也显示分支的状态 
- git diff：查看改变
- git log：查看提交历史
- git reflog：查看命令历史
    - --pretty=oneline 一行显示 
- git reset：回退到指定版本。HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id
- git clone :克隆远程库
    ``` GIT
    // SSH加密
    git clone git@github.com:yancongwen/仓库名.git
    // HTTPS加密，采用此协议的话以后每次推送都要登陆，比较繁琐
    git clone https://github.com/yancongwen/仓库名.git
    // 克隆分支: 
    git clone -b <branch name> [remote repository address].git
    // 或者：
    git clone <respository-name>,先克隆库
    git checkout <branchname>,检出分支
    git pull 取回远程主机某个分支的更新，再与本地的指定分支合并
    ```
- git pull: 取回远程主机某个分支的更新，再与本地的指定分支合并

    ```
    $ git pull --rebase <远程主机名> <远程分支名>:<本地分支名>
    // 例：
    $ git pull origin next:master 
    // 取回origin主机的next分支，与本地的master分支合并
    ```
- git push：将本地分支的更新，推送到远程主机
    ```
    $ git push <远程主机名> <本地分支名>:<远程分支名>
    ```

## 3、命令
![Git命令.png](https://upload-images.jianshu.io/upload_images/3731280-8f32b6551e73d878.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![git常用命令图解.png](https://upload-images.jianshu.io/upload_images/3731280-6c1704b05d8391d8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![Git命令.jpg](https://upload-images.jianshu.io/upload_images/3731280-2d0e8582ee365ea1.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

