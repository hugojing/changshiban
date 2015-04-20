---
layout: post
title: 上网利器 Shadowsocks :服务器端的部署 & Android 客户端的使用
category: blog
description: 久仰 Shadowsocks 的大名，上手使用了一下，发现竟然非常简单便捷。感谢开源的 Shadowsocks ，感谢自由软件和开源社区。
---

## Shadowsocks

[Shadowsocks][1] , 中文名“影梭”。它是一个安全的 `SOCKS5` 代理，用于保护网络流量，是一个开源项目。

为了使用它，我们需要一个安全的 `Shadowsocks` 服务器；然后在客户端上连接服务器，即可使用。

我使用了我的 `VPS` （ 之前写的文章 [DigitalOcean VPS 服务器初体验][2] 中提到的那台，在 Sanfran 机房）来构建 `Shadowsocks 服务器端`；而本地使用了Shadowsocks 的 `Android 客户端`

##只需 5 秒，Shadowsocks 服务器端的搭建与运行

参考文档： [https://github.com/shadowsocks/shadowsocks][3]

打开终端，4 行命令搞定：
	

	ssh root@104.236.133.82
	// SSH 远程连接到服务器，104.236.133.82 是我的服务器的 IP 地址

	apt-get install python-pip
	// 安装 pip

	pip install shadowsocks
	// 安装 shadowsocks

	sudo ssserver -p 443 -k password -m aes-256-cfb --user nobody -d start
	// 启动 shadowsocks 服务器端程序，设置端口为 443 ，密码为 password ，加密方式为 aes-256-cfb ，并且后台运行。

	

好了，服务器端搞定。下面才是正片。



## Android 客户端的使用



###下载

 * `iOS` 设备的话，可以前往 `App Store` 下载客户端。`其他系统`自己 Google/百度。

下载 `Shadowsocks` 客户端，中文名称是 `影梭`，下载地址：

[http://apps.evozi.com/apk-downloader/?id=com.github.shadowsocks][5]



###配置 & 开启


![服务器设置](http://changshiban.qiniudn.com/post/150420/ss_set1.png)

如图所示，服务器设置中：填写 `服务器`、`密码`、选择`加密方式`；



![功能设置](http://changshiban.qiniudn.com/post/150420/ss_set2.png)

功能设置中：`路由`选择`绕过局域网及中国大陆地址`，勾选`全局代理`，勾选`自动连接`。



最后在右上角 `开启` 即可。



###实际效果

测试一下，效果不错：

####Youtube
![Youtube](http://changshiban.qiniudn.com/post/150420/ef_youtube.png)

####Google 服务
![GoogleService](http://changshiban.qiniudn.com/post/150420/ef_googleservice.png)

####Instagram
![Ins](http://changshiban.qiniudn.com/post/150420/ef_ins.png)

####Google ，Google 的 App
![Google](http://changshiban.qiniudn.com/post/150420/unuse_okgoogle.png)
![Google](http://changshiban.qiniudn.com/post/150420/ef_google.png)

####Facebook
![Facebook](http://changshiban.qiniudn.com/post/150420/ef_fb.png)

####Twitter
![Twitter](http://changshiban.qiniudn.com/post/150420/ef_twitter.png)



###一些 Google 应用无法使用

不过，有一些应用还是无法使用，比如这样：

####Play 商店
![Play 商店](http://changshiban.qiniudn.com/post/150420/unuse_playstore.png)
压根无法看到和购买应用、设备；

或者这样：

####Play 音乐
![Play 音乐](http://changshiban.qiniudn.com/post/150420/unuse_playmusic.png)
只能使用本地的音乐，当前往在线音乐页面的时候，卡在这里，再怎么点 `开始` 都不动。

还有这样：

####Google
![Google](http://changshiban.qiniudn.com/post/150420/unuse_okgoogle.png)
只能文字搜索，一按 `语音` 按钮就崩溃，不清楚是不是个案。



###无法使用的原因

那么，到底是为什么无法使用呢？




查看 Google 的帮助页，才搞清楚了无法使用的原因是：

 Google 的一些应用并不是给`所有的国家/地区`提供服务的，而`中国大陆`就不在 `Play 商店`、`Play 音乐` 的支持列表。

怪不得当年 Nexus 5 在 Play 商店上架的时候，划分地区来上货，比如美国 Play 商店、香港 Play 商店。

顺便提一句，Play 商店也不支持台湾（偷笑ing），原因是 Google 不答应当地政府的要求，自行关闭了台湾 Play 商店。




按理说，此时使用这些`服务器在境外`的应用时，我应该是 `美国 IP` ；

因此，可见这几个 Google 应用并不是由 `访客 IP` 来判断是否提供服务的。

真正原因是：

它应该是根据 `移动设备的地理位置` 或者 `Google 账号上由手机号码/信用卡所验证的国家/地区`来判断的。

看来想体验 Play 商店 的话，只能使用一些特殊方法（比如`模拟地理位置` 或者 `用已验证的美国/香港 Google 账号登录`）；

据说老外来中国的时候，依然可以打开 Play 商店 ，这应该是和账号有关系的。

那就暂时体验不了完整的 Google Android 的生态了。




###Google 的语音功能（Voice Search）

至于谷歌最重要的 App ： `Google`，我倒是倒腾出了它的语音功能（Voice Search）。

Yes，就是那句酷炫的 `“Ok Google”`。



####修改主要语言为 English（US）

前面说了，在 Google App 中，一点击 `语音` 按钮就崩溃；

原来是因为它预装的离线语言包只有 `English（US）`，而系统语言是 `中文（简体）`，因此应用崩溃。

既然这样，那就先搞定它好了。




![设置](http://changshiban.qiniudn.com/post/150420/unuse_okgoogle.png)
隐去键盘，拉到最底下，点击右下角的 `三个点`，再点击 `设置`；

![设置](http://changshiban.qiniudn.com/post/150420/cn_google_set.png)
噢，我们在这里可以看到，`Google 即时` 也就是比仅仅语音功能更多酷炫的 `Google Now`，也不支持中国大陆；

好吧，不管它，点击 `语音` 继续。



![语音](http://changshiban.qiniudn.com/post/150420/cn_voice_set_chinese.png)
点击`语言`，添加 `English（US）`为主要语言；
![添加语言](http://changshiban.qiniudn.com/post/150420/cn_voice_set_add_english.png)
确认更改；
![更改语言](http://changshiban.qiniudn.com/post/150420/cn_voice_set_chinese_change.png)
结果如下：
![更改之后](http://changshiban.qiniudn.com/post/150420/cn_voice_set_english.png)



####打开“Ok Google”启动指令

点击上一张图中的 `“Ok Google”启动指令检测`：
![“Ok Google”启动指令检测](http://changshiban.qiniudn.com/post/150420/cn_okgoogle_set.png)
勾选 `在任一屏幕中`，弹出“Ok Google”启动指令的设置页面：
![“Ok Google”启动指令设置](http://changshiban.qiniudn.com/post/150420/okgoogle_set_1.png)
继续下一步，对着手机嚎三声 “Ok Google”：
![“Ok Google”启动指令设置](http://changshiban.qiniudn.com/post/150420/okgoogle_set_2.png)
![“Ok Google”启动指令设置](http://changshiban.qiniudn.com/post/150420/okgoogle_set_3.png)

至此，“Ok Google”指令已经打开。


####“Ok Google”

只要在没锁屏没关机的情况下，对着手机说声 “Ok Google” ，就可以呼出语音助手了。
![“Ok Google”](http://changshiban.qiniudn.com/post/150420/okgoogle.png)


提示给了几个英语的使用例子：
![“Ok Google”eg](http://changshiban.qiniudn.com/post/150420/okgoogle_eg_1.png)
![“Ok Google”eg](http://changshiban.qiniudn.com/post/150420/okgoogle_eg_2.png)

然而并没有什么卵用。。。
![call](http://changshiban.qiniudn.com/post/150420/okgoogle_call.png)
我通讯录里的姓名都是中文吧。。再者，其他命令我也不能总是讲英语吧。。何况我英语那么渣。。囧

好吧，Just for fun ~

 Google App 也和之前不一样了些。。

![Google](http://changshiban.qiniudn.com/post/150420/cn_google.png)


###结束

终于写完了，话说有谁会搞定 Google Now 的，可以指点我下。

我的微信订阅号：`changshibandotcom`



[1]:   http://zh.wikipedia.org/wiki/Shadowsocks  "Wiki 百科"
[2]:   http://changshiban.com/digitalocean-vps-1st-exp.html "前往阅读"
[3]:   https://github.com/shadowsocks/shadowsocks  "官方文档"
[5]:   http://apps.evozi.com/apk-downloader/?id=com.github.shadowsocks  "apk 下载器 / Play 商店的搬运工"
