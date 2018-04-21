---
title: Hexo+Github搭建博客后的保存迁移
date: 2018-01-14
categories: blog
tags: [hexo,github]
---

## 搭建教程

参考使用hexo+github搭建免费个人博客详细教程
https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html
按以上教程完成之后，需要保存迁移，以便在更换电脑时依然能够使用，可使用如下方法。

## 一、创建流程

1. 在github上创建分支hexo，<font style="color:red">需要两个分支，一个master用以运行静态文件，一个hexo用以存放源码</font>
<!-- more -->
2. clone github上原有仓库到本地，只留下.git文件夹
3. 将原来的xxx.github.io所有内容放入刚拷贝的本地仓库中
4. 进入拷贝下的仓库主目录，进行操作并提交，最终达到master分支存在静态文件，hexo分支存放源码
5. 当需要在其它电脑上修改时，使用git拷贝到那台电脑本地，进入目录后通过git和hexo命令分别提交源码和生成的静态文件

## 二、主要步骤
1. 在github上创建一个分支hexo，至此，就拥有了两个分支master和hexo
2. 使用<b>git clone git@github.com:Acheron2012/Acheron2012.github.io.git</b>拷贝到本地仓库
3. 进入刚拷贝的仓库目录，使用<b>git checkout hexo</b>命令切换到hexo分支（使用git branch查看当前所处分支）
4. 删除该目录下除.git文件夹外的所有文件
5. 再进入本地原先的git文件夹（即按《使用hexo+github搭建免费个人博客详细教程》创建的Acheron2012.github.io文件夹），ctrl+a全选所有内容并拷贝到第3步的仓库文件夹中
6. 进入刚拷贝完成的文件夹，打开.gitigonre文件，并删除里面所有内容（这一步是为保证提交源码到hexo分支做准备，若不删除，源码内容会提交不全）
7. 检查<i>_config.yml</i>文件，确定其中的deploy参数为master（保证hexo部署时只提交用以运行的静态页面，由默认的master分支运行静态文件，可在setting中设置运行分支）
8. 依次执行<b>git add .</b>、<b>git commit -m "..."</b>、<b>git push blog hexo</b>提交源码到hexo分支（若无blog项目，则先通过<b>git remote add blog git@github.com:Acheron2012/Acheron2012.github.io.git</b>添加项目）
9. 执行<b>hexo g</b>生成网站并用<b>hexo d</b>部署到GitHub上
 如此，在GitHub上的https://github.com/Acheron2012/Acheron2012.github.io 仓库就有两个分支，一个hexo分支用来存放网站的原始文件，一个master分支用来存放生成的静态网页。

## 三、日常改动 
1.在其它电脑上想修改博客时，方法如下。
- 安装git (https://git-scm.com/downloads)
- node.js (http://nodejs.cn/download/)
- hexo (使用npm install -g hexo)
2.使用<b>git clone git@github.com:Acheron2012/Acheron2012.github.io.git</b>拷贝到本地仓库
3.使用<b>git checkout hexo</b>命令切换到hexo分支（使用git branch查看当前所处分支）
4.在修改代码后，先使用<b>hexo g</b>生成网站修改结果（本地启动为hexo s），并依次执行<b>git add .</b>、<b>git commit -m "..."</b>、<b>git push blog hexo</b>提交源码到github上的hexo分支，并通过<b>hexo d</b>部署到github上的master分支（为保证突发情况，若死机或断电时提交顺序不会有问题，应先执行git操作，再执行hexo操作。

## 注：git最后提交命令为<font style="color:red">git push blog hexo</font>，是<b>hexo分支</b>，不要弄错了

## 参考
https://www.zhihu.com/question/21193762/answer/79109280
