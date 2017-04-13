---
layout: post
title: 以源码方式在Linux安装TensorFlow记录
category: 工具安装
tagline: 
tags: [工具安装, TensorFlow, Bazel]
theme :
  name : bootstrap-3
---
{% include JB/setup %}

TensorFlow ([官网地址](https://www.tensorflow.org/)) 是Google开源出的一个用于各种感知和语言理解任务的机器学习软件库。TensorFlow可以安装在Linux, Mac OS X, Windows等操作系统上。为了省去大家自行编译TensorFlow，TensorFlow为各个操作系统都准备了编译好的TensorFlow二进制文件，大家只要安装即可。当然TensorFlow也可以由我们自行编译，然后再安装。后者需要更多的一些准备工作，比如需要安装Bazel ([官网地址](https://bazel.build/)) 软件构建工具等，安装流程稍微会繁琐些。本文就介绍以源码方式在Linux系统上安装TensorFlow。官方文档介绍得很详细，可谓是“滴水不漏”，这里可能会多介绍下准备工作，权且当做一份补充材料或者对照材料。

## 1. 基础知识

首先，需要了解机器装的是哪个Linux操作系统。Linux有很多种发行版，比如Redhat, Ubuntu等。想大概了解不同发行版的区别联系，可以看这个网页 [http://blog.csdn.net/ithomer/article/details/9729933](http://blog.csdn.net/ithomer/article/details/9729933) 。查看Linux内核版本或者Linux操作系统版本等信息的命令有：

```
cat /proc/version

uname -a

cat /etc/*release*
```

如果是Redhat系统，就需要用基于RPM包的yum包管理工具；如果是Ubuntu系统，就需要用apt-get包管理工具。TensorFlow官网是围绕Ubuntu系统来介绍安装步骤，内容很详细。笔者给Redhat系统安装TensorFlow，发现大体流程和在Ubuntu上安装是类似的，无非是用yum代替apt-get命令，当然有时候需要花点功夫找到对应的RPM包，但总体上并不困难。下文就Redhat系统介绍安装情况。

RPM包在命名时，有时候会带上noarch。noarch是”no architecture”的简称，意思是这个RPM包可以用在不同的CPU机器上。可以用”yum list \| grep noarch”查看有哪些RMP包是noarch的。

关于更详细的系统环境检测，比如GPU型号和个数、GCC编译器版本等环境，可以看nvidia介绍如何安装Cuda工具包的文章，其中第2节就是介绍系统环境检测 [http://docs.nvidia.com/cuda/cuda-installation-guide-linux/#pre-installation-actions](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/#pre-installation-actions) 。

## 2. 准备工作

因为需要安装不少工具，所以申请root权限是必不可少的。

有时候在linux下使用wget不能成功，可能要在windows上先下载文件，然后传到linux上。像后者这样的需求，需要机器有rz/sz工具或者ftp工具。如果需要安装rz/sz工具，可以用” sudo yum install lrzsz”。

## 3. 按照官网描述的流程安装TensorFlow

参考链接：[https://www.tensorflow.org/install/install_sources](https://www.tensorflow.org/install/install_sources) 。这是TensorFlow官网提供的源码方式安装流程的介绍。笔者执行这个流程时，没碰到特殊情况。

下面依官网文档的步骤分小节描述安装过程。

### 3.1 迁出TensorFlow代码

git clone https://github.com/tensorflow/tensorflow

### 3.2 环境准备

#### 3.2.1 安装Bazel

TensorFlow官网给了Bazel官网的安装页面 [https://bazel.build/versions/master/docs/install.html](https://bazel.build/versions/master/docs/install.html) 。照着这个页面介绍的流程执行即可，下面就源码方式安装Bazel的方式来介绍。源码方式安装Bazel的介绍页面是 [https://bazel.build/versions/master/docs/install-compile-source.html](https://bazel.build/versions/master/docs/install-compile-source.html) 。

<div align="center">
  <img src="/images/2017-04-13-install-tensorflow-on-linux-from-sources-figure1.jpg" style="max-width:324px; text-align:center" alt=""/>
</div>
图1 源码编译Bazel的流程（实际操作中可能因为下载的内容不同而有一点区别）

首先，Bazel需要Java，且建议最好安装Java8。另外因为我们需要编译Bazel源码，所以需要JDK，而不只是JRE。参照页面 [http://openjdk.java.net/install/](http://openjdk.java.net/install/) ，RedHat系统需要的是 java-1.8.0-openjdk-devel.x86_64 （”sudo yum install java-1.8.0-openjdk-devel.x86_64”）

其次，当前Bazel最新的版本是0.4.5。基于机器环境，选好相应的版本。下载地址是： [https://github.com/bazelbuild/bazel/releases/tag/0.4.5](https://github.com/bazelbuild/bazel/releases/tag/0.4.5) 。笔者选的是 bazel-0.4.5-installer-linux-x86_64.sh 。下载完这个文件后，可以用sha256sum命令比对sha256值。（说明：下载的文件和图1第2步描述的内容不一样，因为当时碰到 “bazel-<VERSION>-dist.zip” 文件下载不下来的情况）

最后，执行”sh bazel-0.4.5-installer-linux-x86_64.sh”，会把bazel工具装到默认目录/usr/local下。建议执行脚本前看下脚本的 usage() 接口的实现。如果Bazel安装的路径不对，需要卸载，请照这个网页 [https://github.com/bazelbuild/bazel/issues/962](https://github.com/bazelbuild/bazel/issues/962) 执行，以确保没有残留。

#### 3.2.2 安装TensorFlow依赖的python环境

TensorFlow官网介绍需要numpy, dev, pip, wheel四个包。可以用yum安装下面4个包：
+ numpy.x86_64
+ python-devel.x86_64
+ python2-pip.noarch
+ python-wheel.noarch

说明：注意机器的python版本是python2还是python3。

这些包应该也可以用pip安装，笔者暂时还没有尝试。

#### 3.2.3 安装带有GPU支持的TensorFlow

TensorFlow官网介绍需要安装Cuda和cuDNN。

安装Cuda工具包，请详细阅读nvidia官网的安装介绍页面 [http://docs.nvidia.com/cuda/cuda-installation-guide-linux](http://docs.nvidia.com/cuda/cuda-installation-guide-linux)

说明：
1. Package Manager Installation方案和Runfile Installation方案是2种不同的安装方案。笔者按照Package Manager Installation方案执行。对于是否需要支持跨平台，视需求而定。
2. Cuda含有的库很多，有80余个，所以安装CUDA需要的时间较长，可能要半个多小时。在安装的过程中，可能会碰到某些库因为网络连接等问题导致安装失败。对这个问题，首先要看在最后脚本是否自动重装了这些失败的库，如果自动重装了，那就不用在意，否则可以用上面那个网页提到的yumdownloader命令安装这些失败的库。

安装失败的库的log示例

```
cuda-cufft-dev-8-0-8.0.61-1.x8               FAILED ]  431 B/s | 273 MB 713:54:04 ETA
http://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/cuda-cufft-dev-8-0-8.0.61-1.x86_64.rpm: [Errno 12] Timeout on http://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/cuda-cufft-dev-8-0-8.0.61-1.x86_64.rpm: (28, 'Operation too slow. Less than 1000 bytes/sec transferred the last 30 seconds')

```

3. 安装完Cuda后的一些工作。可以参考网页的第6节，特别是第6.2节。nvidia给了很多示例代码，这个参考网页会指导编译和执行几个有代表性的程序。nvcc是编译Cuda程序的编译命令。

接下来安装cuDNN工具包，请详细阅读nvidia官网的安装介绍页面 [https://developer.nvidia.com/cudnn](https://developer.nvidia.com/cudnn) ，按照TensorFlow的建议，选择 cuDNN v5.1 (Jan 20, 2017), for CUDA 8.0。下载下来是个tgz文件，笔者放到 /usr/local/cudnn 目录下，解压后如图2所示，解压后会产出cuda的目录，笔者不建议将其中的include文件和lib64文件并到/usr/local/cuda目录下，因为这样可以隔离开Cuda和cuDNN的升级维护。

<div align="center">
  <img src="/images/2017-04-13-install-tensorflow-on-linux-from-sources-figure2.jpg" style="max-width:324px; text-align:center" alt=""/>
</div>
图2 解压cudnn包后的结果

说明：
1. TensorFlow官网说最后还需要安装libcupti-dev。这句话应该是对ubuntu系统来说的，而对redhat系统来说，在安装Cuda时，已经把cupti给装了，可以查看机器的/usr/local/cuda-8.0/extras/CUPTI/这个目录。
2. 修改环境变量。示例：
```
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cudnn/cuda/lib64:/usr/local/cuda/lib64:/usr/local/cuda/extras/CUPTI/lib64:$LD_LIBRARY_PATH
```
如果希望让机器的全部用户都可以使用Cuda和cuDNN，那么可以把这些内容加到/etc/profile文件中。

### 3.3 为安装TensorFlow配置环境

走到这步，其实已经走完最麻烦的步骤，离最终安装完TensorFlow工具，就只剩下几行命令而已。
```
./configure
```
会有几个交互问题，结合机器环境和自己的需求，填写答案。

### 3.4 构建TensorFlow的pip包

构建有GPU支持的TensorFlow的pip包，参照TensorFlow官网的介绍先后执行下面2条命令：
```
bazel build --config=opt --config=cuda //tensorflow/tools/pip_package:build_pip_package

bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
```

### 3.5 安装TensorFlow的pip包

参照TensorFlow官网的介绍：
```
sudo pip install /tmp/tensorflow_pkg/tensorflow-1.0.1-py2-none-any.whl
```

### 3.6 验证TensorFlow是否安装成功

参照TensorFlow官网的介绍。

* * *

**原创文章，转载请注明：**转载自[{{ site.title }}]({{ site.production_url }})

**本文链接地址：**[{{ page.title }}]({{ site.production_url }}{{ page.url }})

* * *
