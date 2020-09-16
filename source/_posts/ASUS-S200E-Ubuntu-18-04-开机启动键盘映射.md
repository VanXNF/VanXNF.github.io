---
title: ASUS S200E Ubuntu 18.04 开机启动键盘映射
date: 2018-09-01 20:08:45
updated: 2018-09-01 20:08:45
tags: [ASUS, S200E, Ubuntu 18.04 LTS, 开机启动, 键盘映射]
categories: Programming
---

# 设置键盘映射

&nbsp;&nbsp;老笔电 S200E 跑 Win10 有点吃力了，键盘上 Caps Lock 与左 Shift 键又坏了。趁着假期在家，在X宝上买了配套的键盘换上了（第一次拆超极本，真的费劲），又安装了一下 Ubuntu 18.04 LTS，重获新生啊有没有。
***
&nbsp;&nbsp;但是当我安装好Ubuntu，简单美化后，居然发现这款电脑键盘右上角有个专门的功能键？？？功能键就功能键吧，这时才发现X宝上买来换上的键盘右上角这颗功能键键帽印了 “insert” ？？？这怎么能忍，最关键的是这颗键在 Ubuntu 上就是个摆设：

&nbsp;&nbsp;终端下输入 
```
xev
```
&nbsp;&nbsp;或者
```
xev | grep keycode
```
&nbsp;&nbsp;会弹出图形窗口，此时**按键盘即可查看对应键信息**。一看keycode 248 keysym空 ？？？

&nbsp;&nbsp;于是 Plan A 走起，然而事情并不简单，扣下旧键帽一看内部搭扣结构，果然和新的不一样，因吹斯听，换键帽路线 OVER；那就只能 Plan B了，本来键帽正确键闲着也就闲着好了，然而它印了 insert 那一切就不一样了，这是要逼死强迫症啊，然而作者算是Linux初级用户，没法自己想出解决方案，于是开始百度谷歌键盘映射，还真给我找到了，这里记录亲身测试过的一种（也是对我这种情况最简单的一种）

&nbsp;&nbsp;首先用上述指令获取**想修改的键的keycode**，以及**目标键的键值（keysym）**

&nbsp;&nbsp;之后，就在 “~” 目录下创建 **.xmodmaprc**（在别的目录下也行啦）文件
```
sudo vim ～/.xmodmaprc
```
&nbsp;&nbsp;输入内容如下（248是我这颗空闲的功能键的 keycode，而 0xff63 则是键帽上的 insert 对应的 keysym）
```
keycode 248 = 0xff63 0xff63
```
&nbsp;&nbsp;保存之后，在终端输入
```
xmodmap ~/.xmodmaprc
```
&nbsp;&nbsp;即可直接生效。

# 设置开机启动

&nbsp;&nbsp;但是每次开机后要重新执行一次，很麻烦对不对。于是想到了开机自动执行脚本，然而作者真的菜，搜遍搜索引擎，从 rc.local 到 systemd 全都失败了，看其他大佬的评论大概是xmodmap依赖于x桌面，没加载好前是执行不了的，然而还是没法解决。前前后后试了一天，都要放弃了，终于在个小论坛里看到个方案，尝试了一下真的成功了。

&nbsp;&nbsp;Ubuntu 自带一个 **Startup Applications Preferences**

&nbsp;&nbsp;点击 add，name可以随便写，command中填
```
/bin/bash -c "sleep 30; /usr/bin/xmodmap ~/.xmodmaprc"
```
&nbsp;&nbsp;Comment也可以随意填写，上面的代码里后面的是文件路径。

![](https://s1.ax1x.com/2018/09/01/PxVtPg.png)

&nbsp;&nbsp;重启后终于成功了。

&nbsp;&nbsp;完结撒花。
