---
title: Windows 10 配置 Git
date: 2018-09-26 09:11:07
updated: 2018-09-26 09:11:07
tags: [Windows 10, Git]
categories: Software
---
# 下载安装 Git
&nbsp;&nbsp;首先从 [Git 官网](https://git-scm.com/downloads) 下载安装包，基本保持默认选项，安装即可。

&nbsp;&nbsp;安装完成后，Git bash 或者 cmd 中可以输入 `git --version`，验证是否安装成功，输出版本号即为安装成功。

# 配置用户
&nbsp;&nbsp;安装完成有配置一下全局的用户名和邮箱，输入如下命令：
```
git config --global user.name "自定义用户名"
git config --global user.email "邮箱"
```
&nbsp;&nbsp;使用如下命令可以取消全局设置：
```
git config --global --unset user.name
git config --global --unset user.email
```

# 生成 SSH 秘钥
&nbsp;&nbsp;输入下面的命令生成 SSH Key:
```
ssh-keygen -t rsa -C "邮箱"
```
&nbsp;&nbsp;生成单个 SSH Key 时可以连续回车，不输入密钥文件名字和密码。生成的秘钥在 `C:\Users\用户名\.ssh` 下。其中 id_rsa.pub 为公钥，用文本编辑器打开后，复制内容添加到 Github SSH 列表中即可。

# 托管秘钥至 ssh-agent
&nbsp;&nbsp;执行以下命令即可将秘钥添加至 ssh-agent：
```
ssh-add ~/.ssh/id_rsa
```
&nbsp;&nbsp;添加失败时，出现错误 `Could not open a connection to your authentication agent` 可执行以下命令：
```
ssh-agent bash
```
&nbsp;&nbsp;再添加秘钥即可。

# 测试连接
&nbsp;&nbsp;执行以下命令：
```
ssh -T git@github.com
```
&nbsp;&nbsp;出现类似返回内容，即为添加成功。
```
You've successfully authenticated, but GitHub does not provide shell access.
```
