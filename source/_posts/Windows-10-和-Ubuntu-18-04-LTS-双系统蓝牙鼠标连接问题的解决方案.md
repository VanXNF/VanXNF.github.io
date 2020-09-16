---
title: Windows 10 和 Ubuntu 18.04 LTS 双系统蓝牙鼠标连接问题的解决方案
date: 2018-09-01 19:57:17
updated: 2018-09-01 19:57:17
tags: [蓝牙鼠标, Bluetooth Mouse, Windows 10, Ubuntu 18.04 LTS, 鼠标]
categories: Programming
---
&nbsp;&nbsp;笔记本安装了双系统，蓝牙鼠标连接一个系统之后重启到另一个系统就需要把鼠标删掉重新连接，十分麻烦。本文旨在为这个问题提供可行的解决方案。主要参考自 [CSDN](https://blog.csdn.net/10km/article/details/61201268)。

* * *

#### 第一步

&nbsp;&nbsp;首先在 Windows 10 下连上蓝牙鼠标，目的是留下连接记录，方便之后来修改连接值。

#### 第二步

&nbsp;&nbsp;在Ubuntu 18.04 LTS 中连上蓝牙鼠标，鼠标连不上的看 [Ubuntu 1804 蓝牙鼠标连接失败问题解决 Bluetooth Mouse Won't Connect after Reboot](https://www.jianshu.com/p/ad06b7e26b45)

#### 第三步

&nbsp;&nbsp;获取 Ubuntu 18.04 LTS下的蓝牙配对 linkkey 值。

&nbsp;&nbsp;首先切换到 root 账户：
```
su
```
&nbsp;&nbsp;然后执行
```
cd /var/lib/bluetooth/
```
&nbsp;&nbsp;执行（两个小写的L），获得电脑的蓝牙地址。
```
ll
```
&nbsp;&nbsp;cd 这个地址，再次执行 ll，获得鼠标的蓝牙地址。
```
ll
```
&nbsp;&nbsp;cd 鼠标的蓝牙地址，并执行：
```
cat info
```
&nbsp;&nbsp;找到 [LinkKey]，记下这个值
```
Key=966B5BDD8EAECD793FC26700B8A6B337
```
![](https://s1.ax1x.com/2018/09/01/PxVsaT.png)


#### 第四步

&nbsp;&nbsp;回到 Windows 10 系统，此时蓝牙鼠标自动连接上了（之前有连接记录），但是不能操控。

&nbsp;&nbsp;别急，首先到微软官网下载 [PSTools](https://technet.microsoft.com/en-us/sysinternals/bb897553) 工具，下载完成后解压到文件夹即可，在文件夹内以管理员身份运行 **cmd**，执行：
```
PsExec.exe -s -i regedit
```
&nbsp;&nbsp;找到 **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\BTHPORT\Parameters\Keys\\**  下的文件夹，正常情况下是以电脑 mac 地址命名的，找到文件夹内的以蓝牙鼠标 mac 地址命名的文件，修改它的值为之前第三步获取的 **key** 的值即可。

#### 第五步

&nbsp;&nbsp;重启电脑，这时无论是进 Ubuntu， 还是进 Windows，都能正常使用了。
