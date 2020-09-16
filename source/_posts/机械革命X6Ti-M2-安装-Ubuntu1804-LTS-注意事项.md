---
title: 机械革命 X6Ti-M2 安装 Ubuntu1804 LTS 注意事项
date: 2018-09-01 20:11:23
updated: 2018-09-01 20:11:23
tags: [机械革命, Ubuntu 18.04 LTS, X6Ti-M2]
categories: Programming
---
&nbsp;&nbsp;这台机械革命买来有日子了，最初的时候网上教程不全，安装 Ubuntu 总是卡开机画面，现在教程也有一些了，但还是打算稍微记一下关键步骤，方便以后安装。

* * *

## 一

&nbsp;&nbsp;此电脑安装 Ubuntu 时，需要禁用 acpi 才能进入。

&nbsp;&nbsp;Ubuntu 安装界面通过键盘定位到 Install…… 选项，然后按 e 键进入编辑模式。

&nbsp;&nbsp;找到 --- 之后输入一个空格后，再输入 **acpi=off** ，按 F10 键，加载新的启动参数，启动 Ubuntu 的安装界面。

![acpi=off](https://s1.ax1x.com/2018/09/01/PxVU2j.png)

&nbsp;&nbsp;这时可以正常安装了。

&nbsp;&nbsp;安装完重启卡开机，可以使用同样的操作。不过我安装完重启的时候没有遇到卡开机的问题。

## 二

&nbsp;&nbsp;安装完成后，安装一下独显的驱动。

![独显驱动安装](https://s1.ax1x.com/2018/09/01/PxVwMn.png)

&nbsp;&nbsp;安装完成后，修改grub， 输入
```
sudo vim /etc/default/grub
```
&nbsp;&nbsp;将 GRUB_CMDLINE_LINUX="acpi=off" 中的 acpi=off 去掉，保存退出。

![](https://s1.ax1x.com/2018/09/01/PxVNGQ.png)

&nbsp;&nbsp;然后执行：
```
sudo update-grub
```
&nbsp;&nbsp;此时系统的睡眠、开关机都正常了。
