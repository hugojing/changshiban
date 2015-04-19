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

目前的黑客圈子，崇尚白帽子文化，仰慕 扎克伯格、盖茨、史蒂夫•沃兹尼亚克 这样的 Hacker 领袖，致力于发现漏洞、修复漏洞等网络安全事业。

如果你对“黑客”的起源不了解，「推荐」：

+ 书籍： [`《黑客》`][5]， Steven Levy 的黑客文化和伦理的奠基之作 ，从大型机时期的那些打破陈规“非法”访问穿孔卡片计算机的 MIT 的学生，到缔造出 Altair 和 Apple II 电脑这些伟大产品的精英，可以让你领略这样的 DIY 文化。


关于骇客，表面上我们所能看到的，除了 脚本小子 就是那些不慎失手的有一定实力的骇客。可黑暗中，有多少双眼睛在监视着我们，不知道。

如果你想体验一下骇客，「推荐」：

+ 游戏： [`Watch Dogs`][6] ，在游戏中洞察每个人的秘密和银行账户余额，可以满足你熊熊的八卦之心。。。


另外，如果你对 社会工程学 感兴趣，「推荐」：

+ 电影： [`逍遥法外 / Catch Me If You Can`][7]，小李、汤姆汉克斯 主演，这个故事的原型是 天才罪犯 Frank Abagnale ，我觉得这位也是个传奇黑客 + 天生演员;

+ 书籍： [`《欺骗的艺术》/ The Art of Deception`][8]，著名黑客 Kevin Mitnick 著。


##刷机

[Kali NetHunter][2] 目前仅适配 Nexus 和 OnePlus 设备。

之所以适配 OnePlus ，我想有两个原因吧：

1. 高性能;

2. Kali NetHunter 是基于 [CM11][3] 的，而 CyanogenMod 跟  OnePlus 是合作伙伴。在一加手机上，刷 CM 是很常见的，我之前用的 ROM 就是 CM11 .


###参考文档

[http://www.nethunter.com/install][10]

[Pocket Hacking: NetHunter实战指南][4]

我直接在 Windows 下使用了官方提供的傻瓜式安装工具。

###下载刷机工具与镜像

+ 下载并安装 刷机工具 ：`NetHunter Installer` 
下载地址：[http://www.nethunter.com/download][11]


+ 下载适配我的设备的 Kali NetHunter 镜像： `kali_linux_nethunter_1.21_bacon_kitkat.zip`
下载地址：[https://www.offensive-security.com/kali-linux-nethunter-download][12]


###运行 NetHunter Installer

根据提示，进行操作即可，非常简单：

####将手机与 PC 连接，选择设备
![1](http://changshiban.qiniudn.com/post/150419/q1.png)

####先 install 再 Test
记得在之前 打开开发者选项里的调试开关、关闭存储里的MTP
![2](http://changshiban.qiniudn.com/post/150419/q2.png)

####Test 成功后就可以下一步了
![3](http://changshiban.qiniudn.com/post/150419/q3.png)

####选择镜像
 `kali_linux_nethunter_1.21_bacon_kitkat.zip`
![4](http://changshiban.qiniudn.com/post/150419/q4.png)

####自助下载依赖文件
![5](http://changshiban.qiniudn.com/post/150419/q5.png)

「 ps 1 」 `boot.img` 下载后导入失败的话：
![6](http://changshiban.qiniudn.com/post/150419/q6.png)

会弹出这样的框，按步骤手动导入一下即可
![7](http://changshiban.qiniudn.com/post/150419/q7.png)

「 ps 2 」 `Factory Package` 下载失败的话：
![8](http://changshiban.qiniudn.com/post/150419/q8.png)

手动去下载一个 Factory Package ，手动放入 NetHunter Installer 的安装目录下 `NetHunter_Installer/data/MD5check_Depot`，即可
下载地址：[http://forum.xda-developers.com/oneplus-one/general/index-oneplus-one-resources-compilation-t2843675][13]
要下载和设备机型对应的 Factory Package ，比如 OnePlus One 对应的需要下载：`cm-11.0-XNPH44S-bacon-signed-fastboot.zip` 
![9](http://changshiban.qiniudn.com/post/150419/q9.png)

####解锁设备
![10](http://changshiban.qiniudn.com/post/150419/q10.png)

####置入原版安卓
![11](http://changshiban.qiniudn.com/post/150419/q11.png)

![12](http://changshiban.qiniudn.com/post/150419/q12.png)

####置入 ROM 
我建议在点击操作之前，将 `kali_linux_nethunter_1.21_bacon_kitkat.zip` 拷贝到手机存储的 Download 文件夹下，否则往往会因为传输太慢超时
![13](http://changshiban.qiniudn.com/post/150419/q13.png)

![14](http://changshiban.qiniudn.com/post/150419/q14.png)

####刷机成功
![15](http://changshiban.qiniudn.com/post/150419/q15.png)





##界面展示

赶快看看长啥模样～

![20](http://changshiban.qiniudn.com/post/150419/q20.png)

![21](http://changshiban.qiniudn.com/post/150419/q21.png)

![22](http://changshiban.qiniudn.com/post/150419/q22.png)

![23](http://changshiban.qiniudn.com/post/150419/q23.png)


##Let's Hack

到此手里的基础版的黑客手机就打造成功了，可以开始使用。

我对此还没有深入研究，不过有些文档可以参考：


[Pocket Hacking: NetHunter实战指南][4] 的后半部分

[关于zANTI和dsploit两款安卓安全工具的对比][9]


##新开的微信公众号
如果你遇到什么问题，或者想跟我探讨`编程、游戏、黑客、产品`话题，可以通过我刚刚开通的微信订阅号跟我联络：

微信号：`changshibandotcom`



[1]:   http://zhuanlan.zhihu.com/evilcos      " 余弦的知乎专栏"
[2]:   http://www.nethunter.com          "Nethunter 官网"
[3]:   http://www.cyanogenmod.org/        "CM 官网"
[4]:   http://drops.wooyun.org/tips/4634        "前往文章页面"

[6]:   https://www.baidu.com/s?ie=utf-8&f=3&rsv_bp=1&rsv_idx=1&tn=baidu&wd=%E7%9C%8B%E9%97%A8%E7%8B%97&rsv_pq=80dfa49d0000f351&rsv_t=9e12zY%2F3DfoAe8gTiNg1HUvxN%2BpO4YIQUNC4PKNr%2Bdt2qG8j3gM0d9eqzr4&rsv_enter=0&inputT=1910&rsv_sug3=36&rsv_sug1=19&oq=kanme&rsv_sug2=0&rsp=0&rsv_sug4=1911&bs=Catch%20Me%20If%20You%20Can              "百度一下这个"
[7]:   https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&rsv_idx=1&tn=baidu&wd=Catch%20Me%20If%20You%20Can&rsv_pq=ae105df90000ca4c&rsv_t=8c30q7SnEpjZwCIp1RsDZcF0buij1NXixfEjGt7tCtrQimpgPMdUu0%2FmxXA&rsv_enter=0&inputT=1004&rsv_sug3=32&rsv_sug1=14&rsv_n=2&rsv_sug4=1005&rsv_sug=1&bs=%E9%80%8D%E9%81%A5%E6%B3%95%E5%A4%96 "百度一下这个"
[8]:   https://www.baidu.com/s?ie=utf-8&f=3&rsv_bp=1&rsv_idx=1&tn=baidu&wd=%E6%AC%BA%E9%AA%97%E7%9A%84%E8%89%BA%E6%9C%AF&rsv_pq=8e982eba00001f58&rsv_t=fa77YBvI%2FmlI3%2F22FTdWMra9t%2FY7DGrtmVBxIadTl39Ixzc9Ldsnsl2FLoU&rsv_enter=1&inputT=3671&rsv_sug3=21&rsv_sug1=12&rsv_sug2=0&rsp=0&rsv_sug4=8794&rsv_sug=1&bs=Catch%20Me%20If%20You%20Can%20%E5%8E%9F%E5%9E%8B  "百度一下这个"
[9]:   http://drops.wooyun.org/mobile/2503      "前往文章页面" 
[10]:  http://www.nethunter.com/install          ""
[11]:  http://www.nethunter.com/download          ""
[12]:  https://www.offensive-security.com/kali-linux-nethunter-download          ""
[13]:  http://forum.xda-developers.com/oneplus-one/general/index-oneplus-one-resources-compilation-t2843675          ""
