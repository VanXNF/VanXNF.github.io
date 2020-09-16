---
title: Ubuntu 18.04 LTS 使用 Minecraft 我的世界第三方启动器 HMCL
date: 2018-09-01 20:20:17
updated: 2018-09-01 20:20:17
tags: [Ubuntu 18.04 LTS, Minecraft, HMCL]
categories: Programming
---
### 下载安装
&nbsp;&nbsp;首先在下方链接下载第三方启动器：

> [**http://www.mcbbs.net/thread-142335-1-1.html**](http://www.mcbbs.net/thread-142335-1-1.html)

&nbsp;&nbsp;由于是在 Ubuntu 下运行，下载 jar 版本的即可。

&nbsp;&nbsp;在将 jar 文件复制到文件夹中，这里我放置在 ~/Documents/MC 下，首先创建这个文件夹：
```
mkdir ~/Documents/MC
```
&nbsp;&nbsp;我下载在 Downloads 文件夹下，因此将它移动到MC文件夹下去：
```
sudo mv ~/Downloads/HMCL-3.1.94.jar ~/Documents/MC
```
&nbsp;&nbsp;此刻在MC文件夹下执行：
```
java -jar HMCL-3.1.94.jar 
```
**&nbsp;&nbsp;即可运行 HMCL 启动器。**

### 创建快捷方式
&nbsp;&nbsp;Ubuntu 在 /usr/share/applications 目录下存放着系统应用程序的快捷启动图标，我们可以在这里创建 Minecraft 的快捷方式。
&nbsp;&nbsp;首先**准备一张 minecraft 的图标图片**，作为快捷方式的启动图标，放置在 MC 文件夹下，再在这个文件夹下创建启动脚本：
```
vim minecraft.sh
```
&nbsp;&nbsp;写入以下内容：
```
#!bin/sh
cd ~/Documents/MC && java -jar HMCL-3.1.94.jar
```
&nbsp;&nbsp;保存并退出，执行以下命令授予权限：
```
 sudo chmod +x minecraft.sh
```
&nbsp;&nbsp;前期准备工作到此完成，接下来创建快捷方式：
```
cd /usr/share/applications
sudo vim minecraft.desktop
```
输入以下内容（**注意：这里的 vanxnf 请替换成你自己的登录名**，存放路径不同的修改成自己的路径）：
```
[Desktop Entry]
Name=Minecraft
Name[zh_CN]=Minecraft
Comment=Minecraft HMCL
Exec=sh /home/vanxnf/Documents/MC/minecraft.sh
Icon=/home/vanxnf/Documents/MC/minecraft.png
Terminal=false
Type=Application
Categories=Application;
Encoding=UTF-8
StartupNotify=true
```
保存退出，执行以下命令授予权限：
```
sudo chmod +x minecraft.desktop
```
此时在菜单栏中已经可以找到 Minecraft 的启动图标了，双击即可启动。以这种方式启动，**将不再出现终端窗口**。

---

### 注意

&nbsp;&nbsp;另外，我测试发现，以下两种终端启动方式，读取的**配置文件不共享**：

**第一种：**
```
java -jar ~/Documents/MC/HMCL-3.1.94.jar
```
**第二种：**
```
cd ~/Documents/MC && java -jar HMCL-3.1.94.jar
```
&nbsp;&nbsp;因此，认准一种启动，设置好后，之后都要使用相同的启动方式才能读取配置。

&nbsp;&nbsp;我设置时使用的是第二种，方便起见，使用 alias 快捷启动，由于我使用的是**zsh**，执行 (默认终端 应编辑 ~/.bashrc)：
```
sudo vim ~/.zshrc
```
&nbsp;&nbsp;在最下方加上，并保存退出。
```
#Minecraft**
alias MC='cd ~/Documents/MC && java -jar HMCL-3.1.94.jar'
```
&nbsp;&nbsp;最后执行即可（编辑 bashrc 的 source ~/.bashrc 即可）
```
source ~/.zshrc
```
&nbsp;&nbsp;以后启动时，只需要在终端输入 
```
MC
```
&nbsp;&nbsp;即可运行。
