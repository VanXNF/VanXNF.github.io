---
title: Ubuntu 18.04 LTS QQ、微信解决方案
date: 2018-09-01 20:19:00
updated: 2018-09-01 20:19:00
tags: [QQ, 微信, Ubuntu 18.04 LTS]
categories: Software
---
#Deepin-wine 环境安装

&nbsp;&nbsp;首先安装deepin-wine环境：[https://gitee.com/wszqkzqk/deepin-wine-for-ubuntu](https://gitee.com/wszqkzqk/deepin-wine-for-ubuntu) 下载zip包（或用git方式克隆），解压到本地文件夹，在文件夹中打开终端，**切换到 root 账户**，输入：
```
sh ./install.sh
```
## 安装应用容器

&nbsp;&nbsp;然后安装 deepin.com 应用容器，在 [http://mirrors.aliyun.com/deepin/pool/non-free/d/](http://mirrors.aliyun.com/deepin/pool/non-free/d/) 中下载想要的容器，**建议在终端下使用dpkg -i安装容器，**双击 deb 安装也可。以下为推荐容器:

>QQ：[http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.im/](http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.im/)

>TIM：[http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.office/](http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.office/)

>QQ轻聊版：[http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.im.light/](http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.im.light/)

>微信：[http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.wechat/](http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.wechat/)

## 托盘图标

&nbsp;&nbsp;在 Ubuntu 18.04 LTS 中，应用的托盘图标依赖于 GNOME 插件 **TopIconPlus**，可以在 Ubuntu 商店直接安装 TopIconPlus 的 gnome-shell 扩展，也可以使用命令安装：
```
sudo apt-get install gnome-shell-extension-top-icons-plus gnome-tweaks
```
&nbsp;&nbsp;然后用gnome-tweaks开启这个扩展即可。
