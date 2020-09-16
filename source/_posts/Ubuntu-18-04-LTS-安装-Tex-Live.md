---
title: Ubuntu 18.04 LTS 安装 Tex Live
date: 2018-09-15 22:35:29
updated: 2018-09-16 11:33:26
tags: [Ubuntu 18.04 LTS, Tex Live]
categories: Software
---

### 下载安装包
&nbsp;&nbsp;如果身在国内，推荐改用国内的镜像，比如清华大学的 tuna。以下都以这个镜像为例。

&nbsp;&nbsp;在  [https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet/](https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet/) 下载 `install-tl-unx.tar.gz`，解压并进入文件夹 `install-tl-20180915`。日期请按照你解压的文件夹名字来。

&nbsp;&nbsp;执行以下命令安装：
```
wget https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet/install-tl-unx.tar.gz
tar -xzf install-tl-unx.tar.gz
cd install-tl-20180915
sudo ./install-tl
```

&nbsp;&nbsp;没有特殊需要的话，collection 可以不必全部安装，尤其是很多小语种。不过后果是之后可能会缺包。不愿意之后手动安装，并且空间足够、网速足够，也可以全部安装。注意 TeX Live 完全安装后大约要占 6 GB 空间，安装前请务必做好准备。中途断网很可能导致安装失败。其他选项没有必要保持默认即可。

### 环境变量设置
&nbsp;&nbsp;此时 TeX Live 虽已安装，但其路径对于 Linux 来说仍是不可识别的。所以需要更改环境变量。

&nbsp;&nbsp;打开 `~/.zshrc` (非 zsh 用户 修改 bashrc)，在最后添加：
```
export PATH=/usr/local/texlive/2018/bin/x86_64-linux:$PATH
export MANPATH=/usr/local/texlive/2018/texmf-dist/doc/man:$MANPATH
export INFOPATH=/usr/local/texlive/2018/texmf-dist/doc/info:$INFOPATH
```
&nbsp;&nbsp;还需保证开启 sudo 模式后路径仍然可用。命令行中执行
```
sudo visudo
```
&nbsp;&nbsp;找到如下一段代码

```
Defaults        env_reset
Defaults        mail_badpass
Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
```
&nbsp;&nbsp;将第三行更改为:
```
Defaults        secure_path="/usr/local/texlive/2018/bin/x86_64-linux:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
```
&nbsp;&nbsp;也就是加入 TeX Live 的执行路径。如果在安装时作了修改，这里的路径也都要与安装时的保持一致。

### 字体设置
&nbsp;&nbsp;要在整个系统中使用 TeX 字体，还需要将 TeX 自带的配置文件复制到系统目录下。命令行中执行:
```
sudo cp /usr/local/texlive/2018/texmf-var/fonts/conf/texlive-fontconfig.conf /etc/fonts/conf.d/09-texlive.conf
```
&nbsp;&nbsp;之后再执行
```
sudo fc-cache -fv
```
&nbsp;&nbsp;刷新字体数据库。

### 检查
&nbsp;&nbsp;到此整个 TeX Live 2018 就已经安装完毕。可以做下面的一些检查：

&nbsp;&nbsp;基本命令：
```
tlmgr --version
pdftex --version
xetex --version
luatex --version
```
&nbsp;&nbsp;包管理器：
```
sudo tlmgr update --list
```
&nbsp;&nbsp;这一步是检查更新，如果有就顺手更了吧：
```
sudo tlmgr update --self --all
```
&nbsp;&nbsp;`--self` 用来更新 `tlmgr` 自身，如果上一步没有提示可以不加这个选项。

### 测试
&nbsp;&nbsp;可以编译一个简短的测试文件：
```
% hello.tex
\documentclass[UTF8]{ctexart}
\begin{document}
欢迎来到 \TeX{} 世界！
\end{document}
```
&nbsp;&nbsp;用 xelatex 或 lualatex 编译：
```
xelatex hello
lualatex hello
```
&nbsp;&nbsp;编译得到的 PDF 文件如果显示正常，则说明 TeX Live 基本工作正常。
