---
title: Ubuntu 18.04 LTS 开发环境配置
date: 2018-09-01 20:23:24
updated: 2019-03-15 15:31:44
tags: [Ubuntu 18.04 LTS, 开发]
categories: Programming
---
# JDK 配置

## 方法一 手动下载安装

### 下载并安装

&nbsp;&nbsp;首先下载 [JDK8](http://www.oracle.com/technetwork/cn/java/javase/downloads/jdk8-downloads-2133151-zhs.html) ，解压到  /usr/lib/jvm ，我下载的是 **jdk-8u181-linux-x64.tar.gz**，执行
```
sudo mkdir /usr/lib/jvm
sudo tar -zxvf jdk-8u181-linux-x64.tar.gz -C /usr/lib/jvm
```
### 配置环境变量

&nbsp;&nbsp;由于我使用 zsh 因此编辑的是 **~/.zshrc** 文件，使用默认终端的则编辑 **~/.bashrc** 文件，或者**配置所有用户的环境变量**编辑 **/etc/profile** 。

&nbsp;&nbsp;执行：

```
sudo vi ~/.zshrc
```
&nbsp;&nbsp;在文件末尾添加：
```
#set oracle jdk environment
export JAVA_HOME=/usr/lib/jvm/jdk1.8.0_181
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```
&nbsp;&nbsp;然后执行：
```
source ~/.zshrc
```
### 系统设置默认 JDK 

&nbsp;&nbsp;执行：
```
sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_181/bin/java 300
sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_181/bin/javac 300
sudo update-alternatives --install /usr/bin/jar jar /usr/lib/jvm/jdk1.8.0_181/bin/jar 300
sudo update-alternatives --install /usr/bin/javah javah /usr/lib/jvm/jdk1.8.0_181/bin/javah 300
sudo update-alternatives --install /usr/bin/javap javap /usr/lib/jvm/jdk1.8.0_181/bin/javap 300
```
&nbsp;&nbsp;然后执行:
```
sudo update-alternatives --config java
```
&nbsp;&nbsp;若是初次安装 JDK，会有下面的提示:    
```
There is only one alternative in link group java (providing /usr/bin/java): /usr/lib/jvm/jdk1.8.0_181/bin/java
Nothing to configure.
```
&nbsp;&nbsp;否则，选择合适的 JDK即可。

### 查看java版本

&nbsp;&nbsp;查看版本检验是否安装成功：
```
java -version
```
## 方法二 命令行方式安装 oracle JDK

### 安装依赖包
```
sudo apt-get install python-software-properties
```
### 添加仓库源
```
sudo add-apt-repository ppa:webupd8team/java
```
### 更新软件包列表
```
sudo apt-get update
```
### 安装java JDK
```
sudo apt-get install oracle-java8-installer
```
&nbsp;&nbsp;**注意安装过程中需要接受协议**

###5. 查看java版本
```
java -version
```
# 应用软件安装

## Sublime Text 3 

### 安装

&nbsp;&nbsp;参考 Sublime Text 3 的[官方安装文档](https://www.sublimetext.com/docs/3/linux_repositories.html)，按照提示即可正常安装，此处摘录 apt 安装步骤：

&nbsp;&nbsp;Install the GPG key:
```
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
```
&nbsp;&nbsp;Ensure apt is set up to work with https sources:
```
sudo apt-get install apt-transport-https
```
&nbsp;&nbsp;以下按需要二选一即可

&nbsp;&nbsp;Select the channel to use:

**Stable**
```
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
```
**Dev**
```
echo "deb https://download.sublimetext.com/ apt/dev/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
```
&nbsp;&nbsp;Update apt sources and install Sublime Text
```
sudo apt-get update
sudo apt-get install sublime-text
```
&nbsp;&nbsp;注册码及插件请查看 [Sublime Text 3 插件及注册码](https://www.jianshu.com/p/08d07b012d38)。
&nbsp;&nbsp;无法输入中文问题请查看 [Sublime Text 3 Ubuntu 18.04 无法输入中文解决方案](https://www.jianshu.com/p/592a294962c8)。

## 现在可以使用 JetBrain ToolBox 安装全家桶，安装与更新更为便利

## Android Studio
### 安装
&nbsp;&nbsp;首先从 [https://developer.android.com/studio/](https://developer.android.com/studio/) 下载软件压缩包。
&nbsp;&nbsp;右键解压或者使用以下命令：
```
sudo unzip android-studio-ide-173.4907809-linux.zip
```
&nbsp;&nbsp;解压后文件夹名为 android-studio，将文件夹移动至 /opt/下
```
sudo mv android-studio /opt/
```
&nbsp;&nbsp;进入文件夹下
```
cd /opt/android-studio/bin/
```
&nbsp;&nbsp;执行以下命令即可打开 Android Studio，但是不建议这么做，因为这样打开配置文件等均存于root目录下，**建议先创建快捷方式**。
```
sudo ./studio.sh
```
&nbsp;&nbsp;初次启动，将设置选择好，会下载所需的文件，需要较长时间。
### 创建快捷方式
&nbsp;&nbsp;Ubuntu 在 /usr/share/applications 目录下存放着系统应用程序的快捷启动图标，我们可以在这里创建 Android Studio 的快捷方式。
&nbsp;&nbsp;首先进入文件夹
```
cd /usr/share/applications
```
&nbsp;&nbsp;创建快捷方式
```
sudo vim android-studio.desktop
```
&nbsp;&nbsp;添加如下内容：
```
[Desktop Entry]
Name=Android Studio
Name[zh_CN]=Android Studio
Comment=Android Studio
Exec=/opt/android-studio/bin/studio.sh
Icon=/opt/android-studio/bin/studio.png
Terminal=false
Type=Application
Categories=Application;
Encoding=UTF-8
StartupNotify=true
```
&nbsp;&nbsp;然后保存退出，执行：
```
sudo chmod +x android-studio.desktop
```
&nbsp;&nbsp;即可从菜单栏打开 Android Studio 了。

### 配置 adb 环境变量（可选）
&nbsp;&nbsp;编辑 **~/.zshrc** 文件（系统自带终端编辑 ~/.bashrc ，对所有用户生效编辑 /etc/profile）
```
sudo vim ~/.zshrc
```
&nbsp;&nbsp;在下方加入以下内容（ /home/vanxnf/Android/Sdk 部分写你的 sdk 路径）：
```
#set path for android sdk tools
export PATH=$PATH:/home/vanxnf/Android/Sdk/tools/
export PATH=$PATH:/home/vanxnf/Android/Sdk/platform-tools/
```
&nbsp;&nbsp;然后执行以下命令即可生效。
```
source ~/.zshrc
```

## PyCharm
### 安装
&nbsp;&nbsp;首先从 [https://www.jetbrains.com/pycharm/download/#section=linux](https://www.jetbrains.com/pycharm/download/#section=linux) 下载软件压缩包。也可直接使用以下命令安装：
```
sudo snap install [pycharm-professional|pycharm-community] --classic
```
这里采用下载压缩包的形式，解压并将文件夹移动到 /opt/ 下
```
tar -xf pycharm-professional-2018.2.2.tar.gz
sudo mv pycharm-2018.2.2 /opt/
```
进入文件夹下
```
cd /opt/pycharm-2018.2.2/bin
```
执行以下命令即可打开 PyCharm， 但不建议这么做，建议先创建快捷方式。
```
sudo ./pycharm.sh
```
### 创建快捷方式
&nbsp;&nbsp;Ubuntu 在 /usr/share/applications 目录下存放着系统应用程序的快捷启动图标，我们可以在这里创建 PyCharm 的快捷方式。
&nbsp;&nbsp;首先进入文件夹
```
cd /usr/share/applications
```
&nbsp;&nbsp;创建快捷方式
```
sudo vim PyCharm.desktop
```
&nbsp;&nbsp;添加如下内容：
```
[Desktop Entry]
Name=PyCharm
Name[zh_CN]=PyCharm
Comment=PyCharm
Exec=/opt/pycharm-2018.2.2/bin/pycharm.sh
Icon=/opt/pycharm-2018.2.2/bin/pycharm.png
Terminal=false
Type=Application
Categories=Application;
Encoding=UTF-8
StartupNotify=true
```
&nbsp;&nbsp;然后保存退出，执行：
```
sudo chmod +x PyCharm.desktop
```
&nbsp;&nbsp;即可从菜单栏打开 PyCharm 了。

## IntelliJ IDEA
### 安装
&nbsp;&nbsp;首先从 [https://www.jetbrains.com/idea/download/#section=linux](https://www.jetbrains.com/idea/download/#section=linux) 下载软件压缩包。

&nbsp;&nbsp;将压缩包解压并将文件夹移动到 /opt/ 下
```
tar -xf ideaIU-2018.2.2.tar.gz
sudo mv idea-IU-182.4129.33 /opt
```
进入文件夹下
```
cd /opt/idea-IU-182.4129.33/bin
```
执行以下命令即可打开 IDEA， 但不建议这么做，建议先创建快捷方式。
```
sudo ./idea.sh
```
### 创建快捷方式
&nbsp;&nbsp;Ubuntu 在 /usr/share/applications 目录下存放着系统应用程序的快捷启动图标，我们可以在这里创建 IDEA 的快捷方式。
&nbsp;&nbsp;首先进入文件夹
```
cd /usr/share/applications
```
&nbsp;&nbsp;创建快捷方式
```
sudo vim IDEA.desktop
```
&nbsp;&nbsp;添加如下内容：
```
[Desktop Entry]
Name=IDEA
Name[zh_CN]=IDEA
Comment=IDEA
Exec=/opt/idea-IU-182.4129.33/bin/idea.sh
Icon=/opt/idea-IU-182.4129.33/bin/idea.png
Terminal=false
Type=Application
Categories=Application;
Encoding=UTF-8
StartupNotify=true
```
&nbsp;&nbsp;然后保存退出，执行：
```
sudo chmod +x IDEA.desktop
```
&nbsp;&nbsp;即可从菜单栏打开 IDEA 了。

## Anaconda
### 安装
&nbsp;&nbsp;首先从 [https://www.anaconda.com/download/#linux](https://www.anaconda.com/download/#linux) 下载 Anaconda。
&nbsp;&nbsp;执行以下命令安装：
```
bash Anaconda3-5.2.0-Linux-x86_64.sh
```
&nbsp;&nbsp;因为 Anaconda 的脚本只会添加到 ~/.bashrc 下，而使用 zsh 的需要在 ~/.zshrc 下添加
```
# added by Anaconda3 installer
export PATH="/home/vanxnf/anaconda3/bin:$PATH"
```
&nbsp;&nbsp;然后执行：
```
source ~/.zshrc
```
&nbsp;&nbsp;输入：
```
python
```
&nbsp;&nbsp;显示类似以下内容：
```
Python 3.6.5 |Anaconda, Inc.| (default, Apr 29 2018, 16:14:56)
[GCC 7.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
&nbsp;&nbsp;即安装成功。

## Putty
&nbsp;&nbsp;使用以下命令安装即可：
```
sudo apt-get install putty
```
&nbsp;&nbsp;说一下 Ubuntu GNOME 环境下 putty 的复制粘贴，其实 GNOME 自带这个功能，**只需要鼠标选中高亮要复制的内容，在需要粘贴的地方按鼠标中键即可**。

## Atom
&nbsp;&nbsp;从官网下载 [https://atom.io/](https://atom.io/) ，然后使用以下命令安装：
```
sudo dpkg -i atom-amd64.deb
```

## Clion

### 安装
&nbsp;&nbsp;首先从官网下载 [https://www.jetbrains.com/clion/whatsnew/](https://www.jetbrains.com/clion/whatsnew/) 软件压缩包。

&nbsp;&nbsp;将压缩包解压并移动到 /opt/ 下：
```
tar -xf CLion-2018.2.3.tar.gz
sudo mv clion-2018.2.3 /opt/
```
&nbsp;&nbsp;进入文件夹下：
```
cd /opt/clion-2018.2.3/bin
```
&nbsp;&nbsp;执行以下命令即可打开 CLion， 但不建议这么做，建议先创建快捷方式。
```
sudo ./clion.sh
```

### 创建快捷方式

&nbsp;&nbsp;Ubuntu 在 /usr/share/applications 目录下存放着系统应用程序的快捷启动图标，我们可以在这里创建 CLion 的快捷方式。首先进入文件夹:
```
cd /usr/share/applications
```
&nbsp;&nbsp;创建快捷方式:
```
sudo vim Clion.desktop
```
&nbsp;&nbsp;添加如下内容：
```
[Desktop Entry]
Name=CLion
Name[zh_CN]=Clion
Comment=CLion
Exec=/opt/clion-2018.2.3/bin/clion.sh
Icon=/opt/clion-2018.2.3/bin/clion.png
Terminal=false
Type=Application
Categories=Application;
Encoding=UTF-8
StartupNotify=true
```
&nbsp;&nbsp;然后保存退出，执行：
```
sudo chmod +x Clion.desktop
```
&nbsp;&nbsp;即可从菜单栏打开 CLion 了。

# 未完待续
