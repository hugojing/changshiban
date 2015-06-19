---
layout: post
title: 使用 Vagrant 搭建跨平台开发环境(1)
description: 为何有经验的工程师都在虚拟机里跑程序？来来来，我给你瞎掰两下。
category: blog
---

## 为什么要搭建跨平台开发环境

大家在开发的时候，使用不同平台（Windows/Linux/OSX）下的不同开发工具，并且在各自平台下运行测试。

但是，经常会遇到在一些问题：

+ 在这台机子上可以运行在别的机子上不行
+ 配置这个 runtime 配置那个 database ，没有很好的隔离，造成莫名其妙的问题
+ 开发、测试、实际部署的平台都不同，各种麻烦的配置和调试
+ etc

如何解决？

使用虚拟机。


## 搭建目标

要求是 Linux 环境，并且这个 Linux 版本：

+ 足够轻量，占用资源少；
+ 用命令行界面来进行操作，最好没有 GUI 桌面；
+ 使用 Docker 容器来进行代码实例 的 pull & run ，傻瓜式管理，简单易用；
+ 宿主机和虚拟机之间连通网络和共享文件夹，使得虚拟机可以取用在宿主机上写好的代码、宿主机的浏览器可以访问虚拟机中运行的 server；


## 解决方案

针对以上目标，我们的方案应该是这样的：

```
Container | Container | ... 
----------------------------
          Docker
----------------------------
  CoreOS (or other Linux)
---------------------------- 
   Vagrant (Virtual Box) 
---------------------------- 
Local Machine (OSX or other)
```

用 Vagrant 来配置和生成虚拟机，虚拟机的操作系统采用 CoreOS ，当然你也可以使用 CentOS 或者 Ubuntu 等等。

其他的 Linux 也可以自行安装 Docker ，CoreOS 是原生支持 Docker 的。

Docker 并不是什么高深的东西，对我们来说只是好用的工具（类似于包管理器）。

如果你不愿使用 Docker ，当然也可以不用的。


## 搭建（以 OSX 下为例）

### 下载并安装 Vagrant 和 Virtual Box

略

### 下载和配置 coreos-vagrant

在终端执行：

bash：

```
git clone https://github.com/coreos/coreos-vagrant.git
cd coreos-vagrant
```

修改两个文件 user-data.sample 和 config.rb.sample
并把它们保存为 user-data 和 config.rb

实际上你能修改的地方有：

bash：

```
curl  http://discovery.etcd.io/new
```

获得一个返回的 token ，复制并替换到 user-data 中。

在 config.rb 中指定你要下载的 CoreOS 的版本。

config.rb：

```
# Official CoreOS channel from which updates should be downloaded
$update_channel='beta'
```

（此时我用的 beta 版本的版本号为 695.2.0）

### 生成虚拟机 & 启动

直接用 启动 命令启动这台虚拟机，如果它检测到缺少系统镜像会自动下载，并在首次启动时安装生成虚拟机：

bash：

```
cd coreos-vagrant
vagrant up
```

但是结果是这样的：

bash：

```
Bringing machine 'core-01' up with 'virtualbox' provider...
==> core-01: Box 'coreos-beta' could not be found. Attempting to find and install...
    core-01: Box Provider: virtualbox
    core-01: Box Version: >= 308.0.1
You specified a box version constraint with a direct box file
path. Box version constraints only work with boxes from Vagrant
Cloud or a custom box host. Please remove the version constraint
and try again.
```

因为 ｀Box 'coreos-beta'｀ 的下载地址被墙了，就算使用 socks 代理之类，也会因为 20k/s 的速度太慢而下载失败。

所以此时我们需要 hack 一下。

1.自行 hack （如果觉得麻烦可以直接跳过去使用 2.快速 hack ）

先查看一下这个文件

Vagrantfile:

```
config.vm.box_url = "http://%s.release.core-os.net/amd64-usr/current/coreos_production_vagrant.json" % $update_channel
```

因为我指定的 ｀$update_channel｀ 是 ｀beta｀ ，所以它会访问的是

```
http://beta.release.core-os.net/amd64-usr/current/coreos_production_vagrant.json
```

来获取当前 beta CoreOS 的 ｀vmbox｀ 文件下载地址。


实际访问这个 json 文件，会得到：

```
{
  "name": "coreos-beta",
  "description": "CoreOS beta",
  "versions": [{
    "version": "695.2.0",
    "providers": [{
      "name": "virtualbox",
      "url": "http://beta.release.core-os.net/amd64-usr/695.2.0/coreos_production_vagrant.box",
      "checksum_type": "sha256",
      "checksum": "5c1afe9f0f6cdaebed083c9af075c7a515c29000d3db44bde00edc9a67f05ee4"
    }]
  }]
}
```

下载地址即为：

```
http://beta.release.core-os.net/amd64-usr/695.2.0/coreos_production_vagrant.box
```

你可以翻墙用小水管下完这个 ｀vmbox｀ 文件（200M+），并伪造 coreos_production_vagrant.json 文件，一并放置到一个本地搭建的 HTTP server , 修改 Vagrantfile 文件：


coreos_production_vagrant.json：

```
"url": "http://localhost:3000/coreos_production_vagrant.box",
```

Vagrantfile:

```
config.vm.box_url = "http://localhost:3000/coreos_production_vagrant.json"
```

这样就可以再次

bash：

```
cd coreos-vagrant
vagrant up
```

觉得费事？来，我帮你。

2.快速 hack

如果你也想使用 ｀CoreOS 695.2.0｀ , 那么你可以使用我做好的国内镜像，你需要做的只有修改：

Vagrantfile:

```
config.vm.box_url = "http://changshiban.qiniudn.com/image/coreos/amd64-usr/695.2.0/coreos_production_vagrant.json"
```
然后再次

bash：

```
cd coreos-vagrant
vagrant up
```

## ssh 登入 CoreOS

bash：

```
cd coreos-vagrant
vagrant ssh core-01 -- -A
```

如果显示这样的：

```
Last login: Thu Jun 18 15:46:07 2015 from 10.0.2.2
CoreOS beta (695.2.0)
core@core-01 ~ $ 
```
即为成功。

##待续

好了，至此，虚拟机搭建完成。
至于 Docker 的使用、宿主机与虚拟机的网络及共享文件夹设置、虚拟机如何从宿主机取用文件、宿主机如何访问虚拟机上跑的 server ，这些问题我还没搞清楚呢，静待下文哈~


