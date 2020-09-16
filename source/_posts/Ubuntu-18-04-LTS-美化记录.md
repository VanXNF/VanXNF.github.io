---
title: Ubuntu 18.04 LTS 美化记录
date: 2018-09-01 19:35:22
updated: 2018-09-08 15:13:05
tags: [Ubuntu 18.04 LTS, 美化]
categories: Programming
---
# Grub2 美化

&nbsp;&nbsp;在 [https://www.gnome-look.org/browse/cat/109/](https://www.gnome-look.org/browse/cat/109/) 选择一款合适自己的主题安装，具体操作参照文件介绍即可。
&nbsp;&nbsp;我使用的是 [Grub-theme-vimix](https://www.gnome-look.org/p/1009236/) 这款，背景图片可以自己替换，修改过之后文件名不同的话记得在 Vimix 文件夹下的 **theme.txt** 中对应修改。

&nbsp;&nbsp;默认安装的话：
```
cd ~/Downloads/grub-theme-vimix
sudo ./Install
```

&nbsp;&nbsp;注意：安装主题后记得在 `/etc/default/grub` 中找到 `GRUB_GFXMODE`这一行，然后删去最前面的 `#` 将后面的分辨率改成自己的就可以了。结果如下：
```
GRUB_GFXMODE=1920x1080
```

# 主题美化

&nbsp;&nbsp;Ubuntu采用了GNOME，因此要美化主题，首先需要安装 gnome-tweak-tool 。
```
sudo apt-get update
sudo apt-get install gnome-tweak-tool
```
&nbsp;&nbsp;接下来，需要安装 User themes 才能启用第三方主题，直接从 Ubuntu 自带商店中搜索安装即可。

![](https://s1.ax1x.com/2018/09/01/PxVyIU.png)

&nbsp;&nbsp;安装完成后，就可以设置主题了。推荐两款主题

&nbsp;&nbsp;对于想仿 mac 美化的，推荐 [macOS High Sierra](https://www.opendesktop.org/s/Gnome/p/1013714/) 这款主题，点击即可访问，选择 File 下载到本地，解压一下丢到 **~/.themes** 下重新打开 Tweak Tool 即可看到， 它有配套的 cursor 和 icon ，解压后丢到 **~/.icons** 下即可，字体解压后直接安装或者丢到 **~/.fonts** 下。

&nbsp;&nbsp;对于扁平化主题，推荐 [Vimix-Gtk-Theme](https://www.gnome-look.org/p/1013698/) 这款主题，点击即可访问下载，详细安装方法参见主题的介绍页，或者到该主题的 github 主页，有中文安装说明。如果都不喜欢，那就到 [https://www.opendesktop.org/s/Gnome](https://www.opendesktop.org/s/Gnome) 去自己探索一下。

&nbsp;&nbsp;个人比较喜欢 Vimix-Dark-Laptop-Doder ，整体效果如下

![](https://s1.ax1x.com/2018/09/01/PxZoXn.png)

# 登录界面美化

&nbsp;&nbsp;Ubuntu 自带的登录界面万年纯色背景不是很喜欢，也有直接替换背景图片的办法，这里我就偷个懒，用别人写好的代码，访问 [High Ubunterra](https://www.opendesktop.org/s/Gnome/p/1207015/) 下载它准备好的文件，解压后有如下几个文件：

![](https://s1.ax1x.com/2018/09/01/PxVrZV.png)

&nbsp;&nbsp;在文件夹中打开终端，或者 cd 到此文件夹下都行，执行：
```
sudo chmod +x install.sh
sudo ./install.sh
```
&nbsp;&nbsp;然后换上你想放到登录页的壁纸，对图片右键，选 Set As Wallpaper 就行，然后执行：
```
sudo ./SetAsWallpaper
```
&nbsp;&nbsp;Picture文件夹下会出现一张名为 **gdmlock.jpg **的图片，Tweak Tool 中 Appearance 下 Lock Screen 设为这张图就行了。

# 终端美化

## 安装 zsh 和 oh-my-zsh

&nbsp;&nbsp;终端选用 zsh ，首先执行：
```
sudo apt-get install zsh
```
&nbsp;&nbsp;接下来我们需要下载 oh-my-zsh 项目来帮我们配置 zsh，采用wget安装
```
sh -c "$(wget[https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh](https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)-O -)"
```
## 安装插件

### 语法高亮

&nbsp;&nbsp;安装语法高亮插件 highlight：
```
cd ~/.oh-my-zsh/custom/plugins &&\
git clone git://github.com/zsh-users/zsh-syntax-highlighting.git
```
&nbsp;&nbsp;在Oh-my-zsh的配置文件中 **~/.zshrc** 中添加插件：
```
plugins=( [plugins...], zsh-syntax-highlighting)
```
&nbsp;&nbsp;重新打开终端即可生效。

### 自动补全
```
git clone git://github.com/zsh-users/zsh-autosuggestions$ZSH_CUSTOM/plugins/zsh-autosuggestions
```
&nbsp;&nbsp;在 ~/.zshrc 中添加：
```
plugins=( [plugins...],  zsh-autosuggestions)
```
&nbsp;&nbsp;重新打开终端即可生效。

## 设置 zsh 主题

&nbsp;&nbsp;编辑 ~/.zshrc ，找到ZSH_THEME修改为你想要的主题即可。

&nbsp;&nbsp;agnoster这款主题不错，但配套使用需要先安装一下配套字体 Powerline：
```
git clone git@github.com:powerline/fonts.git
cd fonts
sudo ./install.sh
```
&nbsp;&nbsp;在设置中启用第三方字体即可：

![](https://s1.ax1x.com/2018/09/01/PxVJIS.png)

## 其他操作

&nbsp;&nbsp;编辑 ~/.zshrc，在最下方添加，:
```
DEFAULT_USER=$USER
```
&nbsp;&nbsp;保存退出即可。
