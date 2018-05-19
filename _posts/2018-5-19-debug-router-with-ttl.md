---
title: Debug router with TTL
categories:
  - exploit
tags: router-exploitation
published: true
---

# Introduction

一些路由器默认无法通过 telnet 或者 ssh 登录，除了可以对固件添加自定义后门后进行重打包，还可以通过路由器上提供的
TTL 或者 JTAG 来连接路由器，对其进行调试。

# Flash router to origin firmware

如果路由器是刷过 openwrt 或者 ddwrt 的，无法直接通过 web 服务刷回原厂固件。最近入了个二手 netgear wndr3800，
详细信息可以看 openwrt 的 [wiki](https://wiki.openwrt.org/toh/netgear/wndr3800)，支持 JTAG 和 Serial 即 TTL。
拿到手的时候别人已经刷好了 openwrt，而我们要对原厂固件进行测试就要刷回来。openwrt 默认是开启了 ssh 的，尝试
默认密码登录上去，可以 scp 或者 wget 上传原厂固件，上传后执行以下命令：

```bash
mtd -rf write WNDR3800-V1.0.0.52.img firmware   # *** OpenWrt中执行 ***
mtd -r write WNDR3800-V1.0.0.52.img linux       # *** DD-Wrt中执行  ***
```

之后路由器会重启，至电源灯闪烁绿灯时表示已开启 tftpd 服务等待 tftp 上传。其实不用 ssh 登录也行，开启电源时按住
reset 键不放，路由器电源灯先会黄灯闪烁然后等到绿灯闪烁时表示已开启 tftpd 服务，上传之前设置本机为静态ip：

![]({{site.baseurl}}/images/05-19-18-1.png)

设置好后 tftp 上传，路由器刷机就完成了。

![]({{site.baseurl}}/images/05-19-18-2.png)

# Connect with TTL

这款路由没找到 telnet 连的方式，尝试过 netgear telnetenable 的方法解锁 netgear 路由的 telent 服务，发现不行。
所以尝试用 TTL 连接。

其实也很简单，先对路由进行拆机，然后参考 openwrt 的 wiki，usb 转 ttl 线的 GND 插路由板上的 GND，TXD 插 RXD，
RXD 插 TXD，剩下电压接上 3.3V 的口，大概是这样子：

![]({{site.baseurl}}/images/05-19-18-3.png)

从右往左依次是 GND、RX、TX、VCC(3.3V)。

linux 平台下可以安装 minicom 软件连接串口，插上连接线后查看下 dev 目录，会出现 ttyUSB0:

![]({{site.baseurl}}/images/05-19-18-4.png)

安装配置 minicom:

```bash
sudo apt install minicom
sudo minicom -s
```

![]({{site.baseurl}}/images/05-19-18-5.png)

然后可以打开电源，等待启动完毕再连上 ttl：

![]({{site.baseurl}}/images/05-19-18-6.png)

这样我们就获得了一个 shell，可以上 gdbserver 对某一进程进行调试。

后续可以尝试 JTAG 连接调试，不过你需要准备好一个电烙铁 ^_^。

# Reference

- [How to Debrick Your NETGEAR WNR3500L Using Ubuntu 10.04 Lucid Lynx](https://www.myopenrouter.com/article/how-debrick-your-netgear-wnr3500l-using-ubuntu-1004-lucid-lynx)

- [Netgear WNDR3800 [OpenWrt Wiki]](https://wiki.openwrt.org/toh/netgear/wndr3800)
