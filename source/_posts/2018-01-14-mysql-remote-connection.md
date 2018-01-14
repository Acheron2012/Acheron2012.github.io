---
title: Mysql设置允许外网访问（远程连接）
date: 2018-01-14
categories: blog
tags: [mysql,外网访问]
---

## 主要流程
1、打开mysql.exe(MySQL Command Line Client)，输入密码（windows就进入my.ini修改，然后用任务管理器重启服务）

2、输入：use mysql;

3、查询host输入： select user,host from user;
<!-- more -->
4、创建host（如果有"%"这个host值，则跳过这一步）

如果没有"%"这个host值,就执行下面这两句:

    mysql> update user set host='%' where user='root';
    mysql> flush privileges;

5、授权用户

（1）任意主机以用户root和密码ictwsn连接到mysql服务器

    mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'ictwsn' WITH GRANT OPTION;
    mysql> flush privileges;

（2）指定IP为（如192.168.1.100）的主机以用户tuser和密码tpwd连接到mysql服务器

    mysql> GRANT ALL PRIVILEGES ON *.* TO 'tuser'@'192.168.1.100' IDENTIFIED BY 'tpwd' WITH GRANT OPTION; 
    mysql> flush privileges;

6、修改 mysql 的配置文件(针对ubuntu系统)：

    sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
找到 "bind-address = 127.0.0.1" , 这一行要注释掉，只需在前面加个#。

<b>#bind-address = 127.0.0.1</b>
或改为<br>
<b>bind-address = 0.0.0.0</b>
