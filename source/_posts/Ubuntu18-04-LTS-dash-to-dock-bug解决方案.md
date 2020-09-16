---
title: Ubuntu18.04 LTS dash to dock bug解决方案
date: 2018-09-01 20:21:27
updated: 2018-09-01 20:21:27
tags: [Ubuntu 18.04 LTS, dash to dock]
categories: Software
---
&nbsp;&nbsp;截至到目前dash to dock GNOME 3.28**第63版**依旧存在**登陆界面出现dock栏**的问题。

&nbsp;&nbsp;这其实是**自带的dock栏**导致的，在Extensions中即使关闭它也会有这个问题，输入以下命令将自带dock移动到～下，重启后即可解决此问题(也可移动到其他目录或者直接rm删除)。**Ubuntu 更新后需要再执行一遍**，因为更新会修复自带的 dock。
```
sudo mv /usr/share/gnome-shell/extensions/ubuntu-dock@ubuntu.com ~/
```
或者
```
sudo rm -rf /usr/share/gnome-shell/extensions/ubuntu-dock@ubuntu.com
```
