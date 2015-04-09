---
layout: post
title: DigitalOcean VPS 服务器初体验
category: blog
description: 随着云主机、PaaS、BaaS 的流行，再不体验体验 IDC 时代功能丰富、权限强大的 VPS ，恐怕就再也找不回那个曾经让我着迷不已并乐在其中的感觉了。
---

##回顾一下以往用过的服务器

+ 高二（2011）：第一个虚拟主机，由 [萌芽主机][1] 赠送，美国主机，免费使用半年。当时还花了几美刀在 GoDaddy （狗大爹） 上买了人生中的第一个域名 baoyula.com （哦～好有纪念意义） Linux ，具体什么系统那时候也不懂，玩 Apche、PHP、Wordpress ;

+ 大一（2012年末）：第二个虚拟主机， [万网][2] M3型主机，圣诞节活动买一年送一年，先是在万网北京机房，中途万网被阿里云收购后，地理位置转移到杭州阿里云机房。随之一起购买的域名 changshiban.com ，并且以个人名义备案。RedHat 系统，一开始做网站，后来用  [Jekyll][3] 做博客。闲置了好久，跑去玩 [Github Pages][4] & [Gitcafe Pages][5] （不知道它们能否被视为 静态文件服务器？）。是的，你现在看到的这篇文章就位于 Gitcafe Pages 上。

+ 中途帮别人做网站，接触过香港主机，速度不错，不用备案。

+ 大三（2014）：也就是直到现在，做东西用的 BaaS（后端即服务）： [LeanCloud][6] ，确实是服务器，而且底层的东西替你搞定了，你只需要用 express 去写新的业务逻辑。测试了一下，在北京的机房。至于价格，每月有免费额度，你的使用量增大后才开始计费。目前我还没有付费过。


##DigitalOcean 支付方式

[DigitalOcean][7]，美国新锐主机提供商，拥有多个机房，VPS 最低 $5/月。

我使用它的缘由是： Github 送的 [Github Student Developer Pack][8] 里，包含 DigitalOcean $100 代金券。

不得不说，这个学生开发者工具包里都是真金白银， DigitalOcean 的服务器、Namecheap 的域名、Unreal 的游戏引擎、Github 的私有仓库，等等）。

说到这，顺便说个国内的类似的东西，七牛云存储推出的 [青葱创业计划][9] ，里面包含的东西……呃，对于学生开发者来说，毫无含金量。不过七牛云存储很棒，我一直是它的用户。

以上两个工具包，均需要验证 `edu 邮箱`来获取。

回归正题。

DigitalOcean 的账号注册之后，需要先验证信用卡或者用 [PayPal][10] 充值一次，才能进行 填写代金券/优惠码、购买服务器 等操作。

![信用卡](http://changshiban.qiniudn.com/post/credit.png)

我是用 PayPal 充值了 5 美刀 ，然后填写代金券，账户上就有了 105 美刀。
![paypal](http://changshiban.qiniudn.com/post/paypal.png)

##Droplet 的创建

DigitalOcean 把每个服务器叫 Droplet ，添加了信用卡扣款方式或者账户有余额，就可以创建 Droplet 了。

填写服务器名，选择不同的配置、所位于的机房、额外服务、操作系统。用户体验比国内的主机提供商好很多。

+ 配置：
![配置](http://changshiban.qiniudn.com/post/size.png)

+ 机房：
![机房](http://changshiban.qiniudn.com/post/region.png)
据说 San Fran 的机房和中国大陆直连，是最适合中国用户的选择。国内各城市 [Ping][11] 值平均 200 。

+ 操作系统：
![操作系统](http://changshiban.qiniudn.com/post/image.png)
还有额外的服务可以勾选，最后是填写 SSH key （可不填，不填的话会发送 `root 初始密码`到你的邮箱）

点击创建， 55秒生成一个 VPS 服务器。
![droplet](http://changshiban.qiniudn.com/post/droplet.png)

如图，我的 VPS 内存 512 M ，20G SSD 存储，独立 IP ，root 权限。

##SSH 连接服务器

通过 SSH 管理服务器。

打开 Terminal ，输入：

```
root@hugosdebian:/home/hugo# ssh root@104.236.133.82
	
```

输入密码或是有 SSH key 免密码，连接到远程服务器上后，就会显示：
```
root@Lamp:~# 
```
此时表明已经连接到远程服务器了，可以为所欲为了～～（=_= 呵呵哒）


##VPS 的用途

啥？你问我用 VPS 服务器能干啥？

我天，用来当梯子、游戏开服、私人云盘、Web 页面、挖比特币、提供下载、大量发邮件、甚至划分成若干虚拟主机卖给别人都可以好吗～～

这篇文章写的还行：[亲身体验：digitalocean vps能做的10件事][12]


##送你 $10

通过我的邀请链接注册，可以获得 10 美刀。链接如下：

https://www.digitalocean.com/?refcode=325e3dc13b2a


[1]:   http://www.budidc.com      " 萌芽主机"
[2]:   http://www.net.cn          "万网"
[3]:   http://jekyllrb.com/        "Jekyll"
[4]:   https://pages.github.com/        " Github Pages"
[5]:   https://gitcafe.com/GitCafe/Help/wiki/Pages-%E7%9B%B8%E5%85%B3%E5%B8%AE%E5%8A%A9#wiki      " Gitcafe Pages"
[6]:   https://leancloud.cn/              "LeanCloud"
[7]:   https://www.digitalocean.com/?refcode=325e3dc13b2a "DigitalOcean"
[8]:   https://education.github.com/pack  "官网页面"
[9]:   http://qingcong.qiniu.io/pack      "官网页面" 
[10]:  https://www.paypal.com             "paypal" 
[11]:  http://ping.chinaz.com/            "Ping 检测"
[12]:  http://since1989.org/digitalocean/vps-vpn-shadowsocks.html  "亲身体验：digitalocean vps能做的10件事"

