---
layout: post
title: 打造你的黑客手机：当 Kali NetHunter 遇上 OnePlus One
category: blog
description: 育碧大作 Watch Dogs 里主人公 艾登皮尔斯 的主要武器——黑客手机，想必给大家留下了深刻的印象。用它骇入安保系统、摄像头、汽车、移动设备、红绿灯等，藉此获得无限想象的能力。这篇文章，就是我在看了知道创宇 余弦 大大的黑客手机系列之后，立即去尝试并写下的体验。
---

##Web 与 Hack

Web 与 Hack ，只有一步之遥。

比如 Hacker 的技能要求中，必须要了解 Web 前后端;

而 Web 开发者的技能图谱中，也要掌握一些 Hack 技巧。

在知乎关注 [余弦][1] 大大很久了，有幸拜读了他的黑客手机系列;

又恰好刚从 iOS 换到 Andriod 阵营，手里的正是 一加手机（OnePlus One）;

于是迅速行动，刷了 Kali NetHunter ，成功打造出基础的黑客手机。


##黑客与骇客

目前国内的黑客圈子，崇尚白帽子文化，仰慕 扎克伯格、盖茨、史蒂夫•沃兹尼亚克 这样的 Hacker 领袖，致力于发现漏洞、修复漏洞等网络安全事业。

如果你对“黑客”的起源不了解，「推荐」：

书籍： [`《黑客》`][5]， Steven Levy 的黑客文化和伦理的奠基之作 ，从大型机时期的那些打破陈规“非法”访问穿孔卡片计算机的 MIT 的学生，到缔造出 Altair 和 Apple II 电脑这些伟大产品的精英，可以让你领略这样的 DIY 文化。


关于骇客，表面上我们所能看到的，除了 脚本小子 就是那些不慎失手的有一定实力的骇客。可黑暗中，有多少双眼睛在监视着我们，不知道。

如果你想体验一下骇客，「推荐」：

游戏： [`Watch Dogs`][6] ，在游戏中洞察每个人的秘密和银行账户余额，可以满足你熊熊的八卦之心。。。


另外，如果你对 社会工程学 感兴趣，「推荐」：

电影： [`逍遥法外 / Catch Me If You Can`][7]，小李、汤姆汉克斯 主演，这个故事的原型是 天才罪犯 Frank Abagnale ，我觉得这位也是个传奇黑客 + 天生演员;

书籍： [`《欺骗的艺术》/ The Art of Deception`][8]，著名黑客 Kevin Mitnick 著。


##刷机

[Kali NetHunter][2] 目前仅适配 Nexus 和 OnePlus 设备。

之所以适配 OnePlus ，我想有两个原因吧：

1. 高性能;

2. Kali NetHunter 是基于 [CM11][3] 的，而 CyanogenMod 跟  OnePlus 是合作伙伴。在一加手机上，刷 CM 是很常见的，我之前用的 ROM 就是 CM11 .


###参考文档：

[http://www.nethunter.com/install]
[Pocket Hacking: NetHunter实战指南][4]

我直接在 Windows 下使用了官方提供的傻瓜式安装工具。

###下载工具和镜像

+ 下载并安装 刷机工具 ：NetHunter Installer 
下载地址：[http://www.nethunter.com/download]


+ 下载适配我的设备的 Kali NetHunter 镜像： kali_linux_nethunter_1.21_bacon_kitkat.zip
下载地址：[https://www.offensive-security.com/kali-linux-nethunter-download]


###运行 NetHunter Installer

根据提示，进行操作即可，非常简单：

![1](http://changshiban.qiniudn.com/post/150419/q1.png)
![2](http://changshiban.qiniudn.com/post/150419/q2.png)
![3](http://changshiban.qiniudn.com/post/150419/q3.png)
![4](http://changshiban.qiniudn.com/post/150419/q4.png)
![5](http://changshiban.qiniudn.com/post/150419/q5.png)
![6](http://changshiban.qiniudn.com/post/150419/q6.png)
![7](http://changshiban.qiniudn.com/post/150419/q7.png)
![8](http://changshiban.qiniudn.com/post/150419/q8.png)
![9](http://changshiban.qiniudn.com/post/150419/q9.png)
![10](http://changshiban.qiniudn.com/post/150419/q10.png)
![11](http://changshiban.qiniudn.com/post/150419/q11.png)
![12](http://changshiban.qiniudn.com/post/150419/q12.png)




###刷机成功

赶快看看长啥模样～

![20](http://changshiban.qiniudn.com/post/150419/q20.png)
![21](http://changshiban.qiniudn.com/post/150419/q21.png)
![22](http://changshiban.qiniudn.com/post/150419/q22.png)
![23](http://changshiban.qiniudn.com/post/150419/q23.png)


###Let's Hack

到此手里的只是基础版的黑客手机，还需要一些武器和增强作用。

我对此还没有研究，不过有些文档可以参考：


[Pocket Hacking: NetHunter实战指南][4] 的后半部分

[关于zANTI和dsploit两款安卓安全工具的对比][9]



[1]:   http://www.budidc.com      " 萌芽主机"
[2]:   http://www.net.cn          "万网"
[3]:   http://www.cyanogenmod.org/        "Jekyll"
[4]:   http://drops.wooyun.org/tips/4634        " Github Pages"
[5]:   http://www.nethunter.com/install      " Gitcafe Pages"
[6]:   https://leancloud.cn/              "LeanCloud"
[7]:   https://www.digitalocean.com/?refcode=325e3dc13b2a "DigitalOcean"
[8]:   https://education.github.com/pack  "官网页面"
[9]:   http://drops.wooyun.org/mobile/2503      "文章页面" 
