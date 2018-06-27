title: Shadowsocks配置
author: Yan Congwen
tags:
  - 工具
categories: []
date: 2018-04-22 01:27:00
---
> 记录一下Shadowsocks的配置过程

### 1. 通过SSH连接主机
### 2. 安装Shadowsocks
    ```
    # apt-get update                              // 更新源中包列表
    # apt-get install python-pip                  // 安装pip
    # pip install --upgrade pip                   // 更新pip
    # pip install shadowsocks                     // 安装Shadowsocks
    ```

### 3. 配置Shadowsocks
- 编辑配置文件
	```    
	# vi /etc/shadowsocks.json
	```
- 在文件中输入以下内容，保存
   ```
	{
      "server":"0.0.0.0",
      "local_port":1080,
      "timeout":600,
      "method":"aes-256-cfb",
      "port-password":{
          // 设置端口号和对应的密码，自定义即可
          "9001":"666666666",
          "9002":"666666666"
		}
	}
   ```
- 配置完成以上内容，就可以运行ss了
   ```
   # ssserver -c /etc/shadowsocks.json -d start
   ```
    

### 4. 设置开机启动
- 编辑以下文件
	```
	# vi /etc/rc.local
	```
- 在文件中添加以下内容保存
	```
	ssserver -c /etc/shadowsocks.json -d start
	```