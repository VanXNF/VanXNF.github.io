---
title: Ubuntu 18.04 LTS Putty 字体设置
date: 2018-09-02 23:47:43
updated: 2018-09-02 23:47:43
tags: [Ubuntu 18.04 LTS, Putty]
categories: Software
---

#### 前言
&nbsp;&nbsp;在 Ubuntu 下 putty 的字体可以说是小得辣眼睛了，难受的不得了。接下来讲讲怎么换字体及设置字号，以及设置窗体行列数来让代码显示舒服一点。

#### 准备工作
&nbsp;&nbsp;个人而言，比较喜欢 consola 字体，因此在网上找到了网友制作的`微软雅黑 consola 混合字体`，安装到系统上后准备工作就完成了。当然你可以选择你自己喜欢的字体。

#### 更改 putty 字体
&nbsp;&nbsp;运行 `putty SSH client` 后，可以看到左侧有一个菜单，选择里面的 Window 下 的 Fonts 标签，可以看到如下画面：
![](https://s1.ax1x.com/2018/09/03/PzFxYQ.png)
&nbsp;&nbsp;在上面的图中，`Font used for ordinary text` 部分就是修改字体的地方那个了，当然，呈现的画面是我已经修改好了的结果。点击 旁边的 `change...` 按钮，会出来以下画面：
![](https://s1.ax1x.com/2018/09/03/PzFzWj.png)
&nbsp;&nbsp;找不到你安装的字体的话记得把第四个勾勾上，选择好之后点 `OK`就行了。

#### 更改窗体显示行列数
&nbsp;&nbsp;更改了字体及字号之后，原来的窗体就显得有些小了。点击左侧的 `Window` 标签，如图所示修改其中的 Columns 和 Rows 即可：
![](https://s1.ax1x.com/2018/09/03/PzFvFg.png)

#### 注意
&nbsp;&nbsp;修改好之后，千万要记得回到 `Session` 标签保存下来啊，不然下一次还要在来一遍。
