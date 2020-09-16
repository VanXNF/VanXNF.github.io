---
title: 在添加仓库 add-apt-repository 或者更新 apt update命令显示错误
date: 2018-09-01 16:47:37
updated: 2018-09-01 16:47:37
tags: [apt update]
categories: Programming
---

&nbsp;&nbsp;类似以下错误：
![](https://s1.ax1x.com/2018/09/01/PxV0rq.png)

&nbsp;&nbsp;添加的仓库保存在 /etc/apt/sources.list.d目录下。删除对应的错误仓库文件即可。
```
cd /etc/apt/sources.list.d
sudo rm 对应仓库
```
&nbsp;&nbsp;重新执行原操作即可。
