---
title: Windows 10 配置 Maven 环境
date: 2018-09-26 10:10:21
updated: 2018-09-26 10:10:21
tags: [Windows 10, Maven]
categories: Software
---

# 下载 Maven
&nbsp;&nbsp;首先从 [http://maven.apache.org/download.cgi](http://maven.apache.org/download.cgi) 下载 Maven 压缩包， `apache-maven-3.5.4-bin.zip` 或者 `apache-maven-3.5.4-bin.tar.gz` 均可。下载完成后解压即可，我解压后文件夹路径为 `D:\Maven\apache-maven-3.5.4`。Maven 文件夹是我自行创建的，可随意更换。

# 创建本地仓库
&nbsp;&nbsp;在 `D:\Maven\` 下另外创建一个文件夹 `LocalRepository` 用作本地仓库，名字可自取。
进入 `D:\Maven\apache-maven-3.5.4\conf` 文件夹下，编辑 `settings.xml` 文件，找到下面的内容：
```
<!-- localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ${user.home}/.m2/repository
  <localRepository>/path/to/local/repo</localRepository>
  -->
```
&nbsp;&nbsp;在下方添加一条本地仓库记录，路径写成自己创建的本地仓库文件夹路径，修改完成后如下:
```
<!-- localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ${user.home}/.m2/repository
  <localRepository>/path/to/local/repo</localRepository>
  -->
	<localRepository>D:\Maven\LocalRepository</localRepository>
```

# 配置环境变量
&nbsp;&nbsp;系统变量下新建一个变量，名称为 **Maven**，变量值为 Maven 解压路径，即上面的 `D:\Maven\apache-maven-3.5.4`, 然后在 path 变量下添加一条值 `%Maven%\bin`，保存退出即可。

# 测试
&nbsp;&nbsp;到此基本配置完毕了，输入以下命令测试是否成功：
```
mvn --version
```
&nbsp;&nbsp;返回版本号即为成功。
