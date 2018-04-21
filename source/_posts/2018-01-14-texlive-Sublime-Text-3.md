---
title: 使用sublime编写latex(texlive)
date: 2018-01-14
categories: blog
tags: [texlive,sublime,latex]
---

## 一、下载地址
* TeXLive下载地址：
http://ftp.math.purdue.edu/mirrors/ctan.org/systems/texlive/Images/texlive.iso
* Sublime下载地址：
http://sw.bos.baidu.com/sw-search-sp/software/6613504ddd3db/Sublime_Text_3.3126_Setup.exe
* Sumatra PDF下载地址：
http://sw.bos.baidu.com/sw-search-sp/software/0ebcac412a851/SumatraPDF-3.1.2.0-64-install.exe


## 二、主要流程

1. 先安装TeXLive（安装教程：http://jingyan.baidu.com/article/f0e83a2588f6d022e5910128.html）<!-- more -->
2. 再安装sublime，再进入sublime根据下面教程安装LaTeXTools插件
3. 最后安装Sumatra PDF，记住安装路径
4. 然后根据下面的教程进入sublime里面配置一下

## 三、安装LaTeXTools
### 1. 安装Package Control
    1)通过组合键 CTRL + `或是通过菜单命令View -> Show Console来打开控制台，然后将下面的代码输入，按enter即可。（输入的代码网上查找）重启Sublime Text
    2)安装好了之后看以看到下面的选项：Preference->Package Control 
![logo1](1.png)
    3)输入latex，选择 LaTeXTools 进行安装即可

### 2.配置 
选择 Preferences -> Browse Packages，选择并进入LaTeXTools 文件夹，使用 Sublime Text 3打开LaTeXTools.sublime-settings文件。
![logo2](2.png)
修改其中的texpath和sumatra为你的安装路径，并修改distro为texlive。
![logo3](3.png)
将builder改为simple。保存后退出即可。

## 四、配置SumatraPDF
1.修改环境变量PATH 
将 SumatraPDF 的主程序目录添加到环境变量PATH，这一步很重要，否则下一步会无法进行。 
右击我的电脑，选择属性，点击左侧的高级系统设置，再点击下方的环境变量。双击环境变量PATH，在后面加入输入SumatraPDF主目录确定即。<br>
2.配置 SumatraPDF 反向搜索 
打开命令提示符，执行以下命令：（将安装的sublime其中的安装路径替换成你实际的安装路径）
<u>sumatrapdf.exe -inverse-search "\"D:\Sublime\Sublime Text 3\sublime_text.exe\" \"%f:%l\"</u>

## 五、测试运行
建立test.tex文件，复制以下内容：
```javascript
\documentclass{article} 
\author{My Name} 
\title{The Title} 
\begin{document} 
\maketitle 
hello, world % This is comment 
\end{document} 
\end{document}
```

## 参考
http://blog.csdn.net/qazxswed807/article/details/51234834
