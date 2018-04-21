---
title: Frp内网穿透配置(windows远程桌面)
date: 2018-04-21
categories: blog
tags: [Frp,内网穿透,windows]
---

#### 1. Frp下载
- <font size=3>[Frp的下载地址](https://github.com/fatedier/frp/releases)</font>
- <font size=3>[Frp的官方中文文档](https://github.com/fatedier/frp/blob/master/README_zh.md)</font>

这里下载的版本为：frp_0.16.1_windows_amd64（windows客户端，内网IP）
frp_0.16.1_linux_amd64.tar.gz（linux服务端 公网IP）

#### 2. Frp说明
linux（服务端）版解压出来使用<b>frps</b>和<b>frps.ini</b>，为服务端的程序和配置文件。（s后缀代表server）
windows（客户端）版本解压使用<b>frpc.exe</b>和<b>frpc.ini</b>，为客户端的程序和配置文件。（c后缀代表client）
<font color=gray>*外网机器系统linux（有公网IP），内网机器windows，其他系统配置上没有区别。*</font>
<!-- more -->

#### 3. 软件配置

**服务端frps.ini**

```flow
[common]
bind_port = 7000 #客户端和服务端之间通信的端口
vhost_http_port = 6081 #访问客户端web服务自定义的端口号 
```

<font>**客户端frpc.ini**</font>
```flow
[common] 
server_addr = 47.93.47.188 ##公网服务器ip
server_port = 7000 #与服务端bind_port一致

[RemoteDesktop]
type = tcp #连接协议
local_ip = 127.0.0.1 #内网服务器ip，可以是本地IP
local_port = 3389 #内网机器远程桌面端口
remote_port = 6000 #内网机器提供外网远程桌面链接的端口
```
<font color=gray size=3>*即用户连接公网47.93.47.188:6000，相当于连接127.0.0.1:3389,即内网windows桌面*</font> 

#### 4. 启动服务

配置好后,服务端上传到外网服务器，客户端上传到家里的内网主机。采用命令行启动，格式为：程序 -c 配置文件。
命令：
<font face="黑体" color="red" size=3><b>./frps -c ./frps.ini #服务端启动(linux)<b></font> 
<font face="黑体" color="red" size=3><b>frpc.exe -c frpc.ini #客户端启动(windows)<b></font> 


服务端看到如下启动信息，即启动成功：
```linux
2017/12/12 22:11:59 [I] [service.go:87] frps tcp listen on 0.0.0.0:7080
2017/12/12 22:11:59 [I] [service.go:112] http service listen on 0.0.0.0:8080
2017/12/12 22:11:59 [I] [main.go:112] Start frps success
2017/12/12 22:11:59 [I] [main.go:114] PrivilegeMode is enabled, you should pay more attention to security issues
```

客户端看到如下启动信息，即启动成功：
```linux
2017/12/12 22:19:02 [I] [control.go:277] [xxxxxxxxxxxxxxxx] login to server success, get run id [xxxxxxxxxxxxxxxx], server udp port [0]
2017/12/12 22:19:02 [I] [control.go:412] [xxxxxxxxxxxxxxxx] [web] start proxy success
2017/12/12 22:19:02 [I] [control.go:412] [xxxxxxxxxxxxxxxx] [RemoteDesktop] start proxy success
```

注：如果内网程序启动时链接服务端失败，可能是由于服务端端口被防火墙屏蔽，可以查看防火墙设置。

#### 参考
http://www.yizu.org/archives/528/
https://blog.csdn.net/u013144287/article/details/78589643
https://blog.csdn.net/qq_25351621/article/details/78947477
    

