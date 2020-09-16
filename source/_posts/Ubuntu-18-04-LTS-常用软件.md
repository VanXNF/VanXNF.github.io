---
title: Ubuntu 18.04 LTS 常用软件
date: 2018-09-01 19:27:02
updated: 2018-09-26 21:29:19
tags: [Ubuntu 18.04 LTS]
categories: Software
---

### 网易云音乐
&nbsp;&nbsp;首先从 [https://music.163.com/#/download](https://music.163.com/#/download) 下载最新版本。然后使用以下命令安装：
```
sudo dpkg -i netease-cloud-music_1.1.0_amd64_ubuntu16.04.deb
```
&nbsp;&nbsp;安装完成后发现桌面图标打不开面板，搜索发现两个有效的解决方案，第二种方案揭示了问题的本质，~~但目前对于 gnome-shell，第二种方案需要另写一个脚本来运行，并且存在每次启动都是全新启动，无法读取之前设置的问题。~~推荐使用第二种方案。

&nbsp;&nbsp;[Ubuntu 18.04 网易云音乐无法打开最简单解决办法](https://notes.ijustplay.cn/software/ubuntu-netease-cloud-music.html)

&nbsp;&nbsp;[Ubuntu 18.04 装了网易云音乐，难道只能用 sudo 启动吗？ - Fancy的回答 - 知乎](https://www.zhihu.com/question/277330447/answer/478510195)

&nbsp;&nbsp;如果遇到无法保存配置的问题，以下是解决方案：

&nbsp;&nbsp;在 Home 目录下搜索 netease-cloud-music 可以发现在 home 下的 `.cache` 和 `.config` 下都存在这个文件夹，对于 `.cache` 下的文件夹直接删除，对于 `.config` 下的文件夹，需要改变所有者，执行以下命令：
```
cd ~/.config
sudo chown -R vanxnf netease-cloud-music
sudo chown -R vanxnf:vanxnf netease-cloud-music
```
&nbsp;&nbsp;修改文件夹权限如下：

![文件夹权限](https://s1.ax1x.com/2018/09/26/iMcEx1.png)

&nbsp;&nbsp;文件夹内三个文件的权限均设置成如下图所示：

![文件权限](https://s1.ax1x.com/2018/09/26/iMcZKx.png)

### 画图 [draw.io](https://www.draw.io/)
&nbsp;&nbsp;这严格来说并不是一款软件，而是一款Chrome的插件,能够添加到桌面。非常好用、易用，可以满足大部分画图功能。进网页后选择`帮助`->`Download draw.io Desktop...`下载后使用以下命令安装即可：
```
sudo dpkg -i draw.io-amd64-8.8.0.deb
```

### 图片处理 GIMP
&nbsp;&nbsp;在 Ubuntu Software 中搜索即可安装。

### 视频播放器 SMPlayer
&nbsp;&nbsp;执行以下命令安装：
```
sudo apt-get install smplayer
```

### 拼音 谷歌拼音
&nbsp;&nbsp;打字确实是搜狗拼音舒服一点，但是搜狗拼音时不时的会出现候选词乱码问题。网络上的解决方案都治标不治本，因此还是主要用谷歌拼音了。
&nbsp;&nbsp;执行以下命令安装谷歌拼音：
```
sudo apt-get install fcitx-googlepinyin
```
&nbsp;&nbsp;`system setting`-> `Language Support` 中 `Keyboard input method system` 选择 **fcitx**。**重启**后在 Fcitx Config Tool 中启动谷歌拼音即可。

### 截图工具 Shutter
&nbsp;&nbsp;执行以下命令安装：
```
sudo add-apt-repository ppa:shutter/ppa
sudo apt-get update
sudo apt-get install shutter
```
&nbsp;&nbsp;在 `Settings` -> `Devices` -> `Keyboard` 中的 Custom Shortcuts 中添加：
![](https://s1.ax1x.com/2018/09/01/PxVBq0.png)
&nbsp;&nbsp;选中后按 **Enter** 确认即可。

### 办公套件 WPS
&nbsp;&nbsp;首先从 [http://community.wps.cn/download/](http://community.wps.cn/download/) 官网下载最新版文件。执行命令安装：
```
sudo dpkg -i wps-office_10.1.0.6634_amd64.deb
```
&nbsp;&nbsp;修复缺失字体问题
1. 下载文件并解压
[百度云](https://pan.baidu.com/s/1mh0lcbY)
2.  继续执行命令
&nbsp;&nbsp;将得到文件解压进一个文件夹内，进入这个文件夹，将里面的字体文件都复制到 /usr/share/fonts 下：
```
sudo cp * /usr/share/fonts
```
&nbsp;&nbsp;生成字体的索引信息
```
sudo mkfontscale
sudo mkfontdir
```
&nbsp;&nbsp;更新字体缓存
```
sudo fc-cache
```

### 解压 unrar
&nbsp;&nbsp;首先执行以下命令安装：
```
sudo apt-get install unrar
```

&nbsp;&nbsp;这个网上教程很多，但很遗憾，一开始那位写错了，后面的都抄错了。最常用命令是：
```
unrar x xxx.rar
```
&nbsp;&nbsp;这样可以保持压缩包文件目录结构解压出来。

### PDF 阅读器 okular
&nbsp;&nbsp;执行以下命令安装：
```
sudo apt-get install okular
```
