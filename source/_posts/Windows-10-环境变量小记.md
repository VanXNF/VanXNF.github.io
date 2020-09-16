---
title: Windows 10 环境变量小记
date: 2018-09-30 07:44:26
updated: 2018-09-30 07:44:26
tags: [Windows 10, 环境变量]
categories: Settings
---

>新买了一个固态硬盘，打算重装一下系统，在此记录一下环境变量的配置情况，以便恢复环境作为参考。

# 系统变量

## JAVA
- 变量名： `JAVA_HOME`
- 变量值： `C:\Program Files\Java\jdk1.8.0_172`

&nbsp;&nbsp;然后在 path 中添加以下内容：
- `%JAVA_HOME%\bin`

&nbsp;&nbsp;再新建一个系统变量：
- 变量名：`CLASSPATH`
- 变量值：`.;%JAVA_HOME%\lib;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar`

## ADB
&nbsp;&nbsp;ADB 需要链接到 Android Sdk 安装的目录下，我是在安装 Android Studio 时默认安装，则变量如下：
- 变量名 `ADB_HOME`
- 变量值 `C:\Users\VanXN\AppData\Local\Android\Sdk\platform-tools;C:\Users\VanXN\AppData\Local\Android\Sdk\tools`

&nbsp;&nbsp;再在 path 中添加 一条 `%ADB_HOME%` 值即可。

## MAVEN
&nbsp;&nbsp;Maven 没什么好说的，直接添加即可：
- 变量名 `MAVEN_HOME`
- 变量值 `D:\Maven\apache-maven-3.5.4`

&nbsp;&nbsp; 在 path 中新增一条 `%MAVEN_HOME%\bin` 值即可。

# 用户变量

# OneDrive
&nbsp;&nbsp;OneDrive 的默认路径可以在此处更改。
