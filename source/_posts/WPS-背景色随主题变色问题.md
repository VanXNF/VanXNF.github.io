---
title: WPS 背景色随主题变色问题
date: 2018-11-03 17:05:03
updated: 2018-11-03 17:45:14
tags: [WPS, Ubuntu 18.04 LTS]
categories: Programming
---
> UBuntu  18.04 LTS 下使用 GNOME 深色主题会导致 WPS 出现一些奇奇怪怪的问题，之前使用了一段时间浅色主题应急，现在闲下来了，还是想办法解决一下，毕竟，深色党万岁。

# 问题描述
&nbsp;&nbsp;傻傻的 WPS 在我使用 GNOME 深色的主题后，就会出现如下图一样的问题：
![](https://s1.ax1x.com/2018/11/03/i4o2vT.png)
&nbsp;&nbsp;实在是不能忍。同时，wps word 默认字体颜色会变为白色，背景色却仍旧是白色，搞得我好几次以为文档格式有问题，缺字少表的。安装了 LibreOffice 和 CrossOver 装的 Office 2016 就没有这个问题。虽说能用，但是还是不能忍。

# 解决方案
&nbsp;&nbsp;那么接下来是解决方案。首先，修改主题不太现实，万一我下次换个主题岂不是又要修改一遍。那么，问题的突破口就需要在 WPS 这里找了。在网上查到一些资料，desktop 快捷方式启动时可以传入一些参数。那么就编辑一下 WPS 的快捷方式，在里面试着指定主题就好了。

&nbsp;&nbsp;编辑 wps excel 的快捷方式：
```shell
 sudo vim /usr/share/applications/wps-office-et.desktop
```
&nbsp;&nbsp;显示内容如下：
```
[Desktop Entry]
Comment=Use WPS Spreadsheets to analyze manage data.
Comment[zh_CN]=使用WPS表格分析、管理数据
Exec=/usr/bin/et %f
GenericName=WPS Spreadsheets
GenericName[zh_CN]=WPS 表格
MimeType=application/wps-office.et;application/wps-office.ett;application/wps-office.xls;application/wps-office.xlt;application/vnd.ms-excel;application/msexcel;application/x-msexcel;application/wps-office.xlsx;application/wps-office.xltx;
Name=WPS Spreadsheets
Name[zh_CN]=WPS 表格
StartupNotify=false
Terminal=false
Type=Application
Categories=Office;Spreadsheet;Qt;
X-DBUS-ServiceName=
X-DBUS-StartupType=
X-KDE-SubstituteUID=false
X-KDE-Username=
Icon=wps-office-etmain
InitialPreference=3
StartupWMClass=et

```

&nbsp;&nbsp;将 `Exec=/usr/bin/et %f` 这一行修改为 `Exec=/usr/bin/et -style Vimix %f` 其中 Vimix 是我电脑上有的一个亮色主题，可以随意修改为自己有的就行。保存退出后再打开，问题已经解决。另外的两个也是同样的操作，就不再赘述。
