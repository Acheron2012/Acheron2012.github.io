---
title: windows上安装tensorflow(gpu)
date: 2018-01-12
categories: blog
tags: [windows,tensorflow,gpu]
---

## 一、安装python3
### 1、下载并安装python3
官网下载：https://www.python.org/downloads/windows/
增加环境变量（若无），进入python安装目录并将python.exe修改为python3.exe
### 2、安装pip3
下载脚本：https://bootstrap.pypa.io/get-pip.py
运行脚本：<b>python3 get-pip.py</b>
<!-- more -->

## 二、安装tensorflow（GPU）
使用pip命令执行：
<b>pip install --ignore-installed --upgrade tensorflow-gpu </b>
## 三、安装CUDA
首先要检查电脑的显卡型号是否支持GPU加速。
点击查看是否支持自己的gpu：https://developer.nvidia.com/cuda-gpus
<img src="clipboard1.png" width="40%" height="40%">
确定电脑显卡支持GPU加速后，选择对应版本并开始下载Cuda:
 https://developer.nvidia.com/cuda-downloads
下载后推荐使用默认安装，安装路径一般为
<u>C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0</u>
![logo2](clipboard2.png)
安装完后会默认配置环境变量，且为了后续依赖包不报错，还需要在path中添加：
<u>C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0\bin</u>              及 
<u>C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0\lib\x64</u>
两个环境变量。
## 四、安装Cudnn
选择对应版本下载cudnn：https://developer.nvidia.com/rdp/cudnn-download
<img src="clipboard3.png" width="50%" height="50%">
下载后面附有cuda版本号，需和上面相一致（红色方框部分是cudnn7，可能会报错，推荐它下面的一个安装V6.0）
<font color="red">Cudnn解压后将bin,include,lib三个文件夹里面的内容原封不对覆盖至Cuda安装目录下即可，</font>默认主路径如上一步。



## 五、运行测试
运行如下代码
```python
import tensorflow as tf  
    sess = tf.Session()  
    x = tf.constant(5)  
    y = tf.constant(35)  
    print(sess.run(x * y))  
  }
```
<b>结果：175</b>
![logo4](clipboard4.png)
<i>（若报"pywrap_tensorflow_internal"错误，一般为版本不对，需要进入cuda主目录，将cudnn64_7修改为如上图所示的cudnn64_6)</i>

## 六、可能错误
* <b>Cannot remove entries from nonexistent file</b>
如果在安装 TensorFlow 的时候出现类似Cannot remove entries from nonexistent file c:\users\li\anaconda3\lib\site-packages\easy-install.pth 的错误，那么可以参考 Cannot remove entries from nonexistent #622 和 osx 10.11 installation issues #135，里面说了好多种解决办法，我在这里介绍一种方法：
在 <u>pip3 install --upgrade tensorflow-gpu</u> 之前先执行 <u>pip install --upgrade --ignore-installed setuptools</u> 。 
* <b>ImportError: DLL load failed: 找不到指定的模块。 和ImportError: No module named '_pywrap_tensorflow_internal' </b>
如果在 import tensorflow 的时候这两个问题同时出现，那么很有可能是你的 cuda 和 cudnn 版本有问题，例如你的 cuda 版本是8.0.60，而正确的是 8.0.44，重新安装正确的版本（文章里提供的）就可以。参考 On Windows, running “import tensorflow” generates No module named “_pywrap_tensorflow” error 。

## 参考文献
https://www.tensorflow.org/install/install_windows
http://blog.csdn.net/u010099080/article/details/52333935
http://blog.csdn.net/u010099080/article/details/53418159
http://blog.csdn.net/flying_sfeng/article/details/58057400