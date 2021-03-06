---
layout: post
title: 生存类游戏 Don't Starve Together（饥荒联机版）Linux 专用服务器的搭建
category: blog
description: Don't Starve （饥荒），可是很多 PC 玩家的心头爱。它的联机版 Don't Starve Together 正在 Steam 游戏平台上抢先体验。这篇就介绍一下在 Linux 上 Dedicated Server （专用服务器）的搭建。
---

##须知

+ `Don't Starve Together` ， 下文简称为 `DST` ;

+ 本文仅针对 `Steam` 平台上的 `DST` ，启动后可以在服务器列表中找到所搭建的服务器;


##准备

+ 游戏厂商官方给出的 `token` （令牌），相当于服务器入驻 Steam 平台的许可;

+ 官网的英文参考文档，`Windows` & `Linux` 均有： [Dont Starve Together Dedicated Servers][1]

+ 一名玩家的中文指南，仅限 `Windows` ：[【CN】DST Dedicated Server服务器配置教程][2]



##搭建

###获取 token

1. 运行 `Steam`
2. 运行 `DST`
3. 按 `～` 键，输入指令：`TheNet:GenerateServerToken()`，回车

然后你会在你的用户文档相应位置找到 `server_token.txt` 文件，非常重要。

我是在 Windows 7 下生成这个文件的，然后拿到 Debian 7 系统上，通过 `scp` 命令放到服务器上的。

如果你也是这样，注意：请一定用 U盘/云盘 将这个文件拷贝转移，不要单纯的记住文本，在另一个 电脑/系统 上新建文本文件并写下;否则……（我被折腾惨了。。）

###连接到服务器

DST 服务器端程序是用 `Lua` 编写的，在 Linux 上是运行在 32 位（i386）模式上。

我把它部署在 `DigitalOcean` 的 VPS 上，先后换个三个系统，才跑起来。

`CentOS 7.0 x64`

`Debian 6.0 x64`

前面用的两个 64 位系统，均跑不起来，最后使用了：

`Debian 7.0 x32`

到现在的情况就是：

+ 我的电脑： `hugosdebian` `Debian 7.0 x64`

+ 服务器  ： `Lamp`        `Debian 7.0 x32`


好了，「开始」：

在 Linux 下，`SSH` 连接到服务器：

```

root@hugosdebian:/home/hugo# ssh root@104.236.133.82

Linux Lamp 3.2.0-4-686-pae #1 SMP Debian 3.2.65-1+deb7u1 i686

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Fri Apr 10 02:43:14 2015 from 1.85.7.230
root@Lamp:~# 

```

表明此时已经连接到了远程的服务器上，前方高能！！展现 Linux 命令行界面高效的时候到了！ `「为何这么激动。。。」`

###下载服务器端程序

按照官方文档，开始下载程序：

```
sudo apt-get update
sudo apt-get install libgcc1
sudo apt-get install libcurl4-gnutls-dev:i386
sudo useradd -m steam
chmod a+rw `tty`  # Note those are backticks, not single quotes
sudo su - steam
mkdir ~/steamcmd
cd ~/steamcmd
wget http://media.steampowered.com/installer/steamcmd_linux.tar.gz
tar -xvzf steamcmd_linux.tar.gz
./steamcmd.sh
login anonymous
force_install_dir /home/steam/steamapps/DST (or whatever absolute path you want)
app_update 343050 validate
quit

```

###试运行

程序下载结束，准备运行：

```
cd /home/steam/steamapps/DST/bin/
screen -S "DST Server" ./dontstarve_dedicated_server_nullrenderer

```

打住，此处官网文档有一点小错误，当前用户为 `"steam"` , 应该使用 `"root"` 来运行它，所以先加一句再运行：

```

su - root
cd /home/steam/steamapps/DST/bin/
screen -S "DST Server" ./dontstarve_dedicated_server_nullrenderer

```



`——————————小插曲—————————————`

+ 因为我的服务器是 `Debian 7.0` ，官方文档里额外说明了这个系统下存在 库的版本老旧 的问题，所以额外给了 Hack 方法，服务器非 `Debian 7.0` 的不用理会：

```
su - root
mkdir ~/dst_lib && cd ~/dst_lib
wget https://github.com/dgibbs64/linuxgameservers/raw/master/Insurgency/dependencies/libc.so.6
wget https://github.com/dgibbs64/linuxgameservers/raw/master/Insurgency/dependencies/libpthread.so.0
wget https://github.com/dgibbs64/linuxgameservers/raw/master/Insurgency/dependencies/librt.so.1

```

当然，它的运行略有不同：

```
cd /home/steam/steamapps/DST/bin/
screen -S "DST Server" bash -c 'LD_LIBRARY_PATH=~/dst_lib ./dontstarve_dedicated_server_nullrenderer'

```

+ `screen` 是一个 好用的[?] 命令行下多任务管理软件，可以自行安装。

`——————————小插曲结束—————————————`




刚刚第一次运行了，等待几秒，显示出运行结果如下：

```
root@Lamp:~# cd /home/steam/steamapps/DST/bin/
root@Lamp:/home/steam/steamapps/DST/bin# screen -S "DST Server" bash -c 'LD_LIBRARY_PATH=~/dst_lib ./dontstarve_dedicated_server_nullrenderer'
......（中间好长，略）
......（中间好长，略）
[200] Account Failed (6): "E_INVALID_TOKEN"
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!! Your Server Will Not Start !!!!
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
If you wish to run your server without authentication
Or if you wish to use your server for a LAN game
You must run it in 'lan mode'
Add the command line argument -lan

To generate a server_token from a game client, open console
open console with the tilda key (~)
Type: TheNet:GenerateServerToken()

```

喔，还没有写上 `token` ，好吧。


###配置

+ `token`

用 `logout`命令 回到本地，用 `scp` 命令传输本地的 `server_token.txt` 文件到服务器的 `~/.klei/DoNotStarveTogether` 目录下：

```

root@hugosdebian:/home/hugo# scp /home/hugo/downloads/server_token.txt root@104.236.133.82:~/.klei/DoNotStarveTogether
 
server_token.txt    100%   33     0.0KB/s   00:00

```

传输成功。

+ `settings.ini`

还应该打开同目录下的服务器配置文件 `settings.ini`，配置一下：

```

root@Lamp:~# cd .klei/DoNotStarveTogether/
root@Lamp:~/.klei/DoNotStarveTogether# ls
chat_log.txt  log.txt  save
root@Lamp:~/.klei/DoNotStarveTogether# vim settings.ini

......


```

具体如何配置，官网文档都有，主要就是这些：

```

default_server_name = Your unique server name
default_server_description = A very nice server description
server_port = 10999
server_password = password
max_players = 1 .. 64
pvp = true | false
game_mode = endless | survival | wilderness

```

`vim`，著名编辑器，自行安装。在命令行下写完东西后如何保存退出？ 依次按 `Esc`+`:wq`+`Enter` ，「我也是新学的。。」


###再运行

再运行一次，哦，成功了。

「不要问我显示什么就算成功了，反正你的 `screen` 不终止就对了。 」

=_=|什么鬼...



##去看看服务器列表


[http://my.jacklul.com/dstservers][3]

服务器在此列中，就说明已经成功入驻 `DST on Steam` 了。



[1]:   http://dont-starve-game.wikia.com/wiki/Don%E2%80%99t_Starve_Together_Dedicated_Servers      "官网文档"
[2]:   http://steamcommunity.com/sharedfiles/filedetails/?id=382584094&searchtext=dedicated          "中文文档"
[3]:   http://my.jacklul.com/dstservers        "服务器列表"

