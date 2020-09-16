---
title: Ubuntu 18.04 LTS GitHub Pages + Hexo 搭建博客
date: 2018-09-01 18:04:05
updated: 2018-09-01 18:04:05
tags: [静态独立博客, Hexo, GitHub Page, Git, Ubuntu 18.04 LTS]
categories: Programming
---


# 前言
&nbsp;&nbsp;这是一篇在 Ubuntu 18.04 LTS 中使用 GitHub Pages 和 Hexo 搭建免费独立博客的总结。我有自己的服务器，出于某种需要，我用我的服务器反代了 GitHub Pages, 将会使用自己的域名访问 GitHub Pages 上的博客。同时，为了在多台电脑上都可以更新博客，采用两个分支的方式来存放文件，master 分支存放 Hexo 渲染出来的文件， 新建的分支存放源文件。

# 必要配置

## GitHub Pages 仓库

### 创建对应仓库

&nbsp;&nbsp;在自己的 GitHub 账号下创建一个新的仓库，命名为 username.github.io（username是你的账号名)。

&nbsp;&nbsp;在这里，要知道，GitHub Pages 有两种类型：User/Organization Pages 和 Project Pages，而我所使用的是 User Pages。

&nbsp;&nbsp;简单来说，User Pages 与 Project Pages 的区别是：
1. User Pages 是用来展示用户的，而 Project Pages 是用来展示项目的。
2. 用于存放 User Pages 的仓库必须使用 username.github.io 的命名规则，而 Project Pages 则没有特殊的要求。
3. User Pages 将使用仓库的 master 分支，而 Project Pages 将使用 gh-pages 分支。
4. User Pages 通过 `http(s)://username.github.io` 进行访问，而 Projects Pages 通过 `http(s)://username.github.io/projectname` 进行访问。

### 相关资料
* [GitHub Pages Basics / User, Organization, and Project Pages](https://help.github.com/articles/user-organization-and-project-pages/)

## Git

### 安装 Git

```bash
sudo apt-get install git
```

### 配置 Git
&nbsp;&nbsp;当安装完 Git 应该做的第一件事情就是设置用户名称和邮件地址。这样做很重要，因为每一个 Git 的提交都会使用这些信息，并且它会写入你的每一次提交中，不可更改：

```bash
git config --global user.name "username"
git config --global user.email "username@example.com"
```

&nbsp;&nbsp;对于 user.email，因为在 GitHub 的 commits 信息上是可见的，所以如果你不想让人知道你的 email，可以 Keeping your email address private:

1. 在GitHub右上方点击你的头像，选择`Settings`；
2. 在右边的`Personal settings`侧边栏选择`Emails`；
3. 选择`Keep my email address private`。

&nbsp;&nbsp;这样，你就可以使用如下格式的 email 进行配置：

```bash
$ git config --global user.email "username@users.noreply.github.com"
```

### 相关资料
* [安装 Git](http://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)
* [配置 Git](http://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%88%9D%E6%AC%A1%E8%BF%90%E8%A1%8C-Git-%E5%89%8D%E7%9A%84%E9%85%8D%E7%BD%AE)
* [Setting your email in Git](https://help.github.com/articles/setting-your-email-in-git/)
* [Keeping your email address private
](https://help.github.com/articles/keeping-your-email-address-private/)

## Git 与 GitHub

### 与github建立联系
&nbsp;&nbsp;为了能够在本地使用 git 管理 github 上的项目，需要进行一些配置，这里介绍 SSH 的方法。

#### 检查电脑是否已经有 SSH keys。
``` bash
ls ~/.ssh
# Lists the files in your .ssh directory, if they exist
```

&nbsp;&nbsp;默认情况下，public keys 的文件名是以下的格式之一：id_dsa.pub、id_ecdsa.pub、id_ed25519.pub、id_rsa.pub。因此，如果列出的文件有 public 和 private 钥匙对（例如id_ras.pub和id_rsa），证明已存在 SSH keys。

#### 如果没有 SSH key，则生成新的 SSH key。
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
# Creates a new ssh key, using the provided email as a label
```
&nbsp;&nbsp;之后一路回车即可。

#### 向 ssh-agent 添加 key。
&nbsp;&nbsp;首先确保 ssh-agent 可运行：
```bash
# start the ssh-agent in the background
ssh-agent -s
```
&nbsp;&nbsp;然后添加 SSH key：
```bash
ssh-add ~/.ssh/id_rsa
```

#### 在 GitHub 添加 SSH key。
&nbsp;&nbsp;首先，拷贝 key：
```bash
sudo cat ~/.ssh/id_rsa.pub
# Copies the contents of the id_rsa.pub file to your cllipboard
```
&nbsp;&nbsp;然后，在 GitHub 右上方点击头像，选择`Settings`，在右边的`Personal settings`侧边栏选择`SSH Keys`。接着粘贴 key，点击`Add key`按钮。最后，测试链接：
```bash
ssh -T git@github.com
# Attempts to ssh to GitHub
```
&nbsp;&nbsp;如果你看到：
```bash
The authenticity of host 'github.com (207.97.227.239)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)?
```
&nbsp;&nbsp;就键入：yes。之后将会看到如下信息：

```bash
Hi username! You've successfully authenticated, but GitHub does not
provide shell access.
```

### 相关资料
* [Generating SSH keys](https://help.github.com/articles/generating-ssh-keys/)

## Hexo

&nbsp;&nbsp;具体安装方法及主题配置请查看：{% post_link Ubuntu-18-04-LTS-配置-Hexo %}

## 搭建方法
&nbsp;&nbsp;在上面，我们已经配置好了所需的前置条件，也了解了 Hexo 博客搭建方法。现在，需要使用 GitHub Pages 搭建一个别人能够访问的 Hexo 博客了。

### 创建仓库
&nbsp;&nbsp;创建一个名为`username.github.io`的仓库。

### 搭建 hexo 博客 并创建两个分支：master 与 source

#### 首先建立 hexo 博客
```bash
mkdir ~/Documents/Hexo
cd ~/Documents/Hexo
sudo npm install -g hexo-cli
hexo init
sudo npm install
sudo npm install hexo-deployer-git
```

#### 创建 source 分支，并使其为默认分支：
```bash
git init
git remote add origin git@github.com:username/username.github.io.git
git add .
#添加修改
git commit -m "init hexo"
#初次提交
git checkout -b source
#建立分支 hexo 并切换到分支 hexo
git push -u origin source
#将分支 hexo 提交到 github
```

#### 创建 空白分支 master
```bash
cd ..
#退回上一级目录
mkdir new
#创建一个新的文件夹用以创建空白分支
cd ~/Documents/new
git init
touch README.md
#随意创建一个文件，用于提交分支
git add .
git commit -m "new branch"
git remote add origin git@github.com:username/username.github.io.git
git push origin master
#将分支 master 提交到 github
rm README.md
git add .
git commit -m "clear new branch"
git push origin master
cd ~/Documents/
rm -rf new
cd Hexo
git pull
```
&nbsp;&nbsp;执行完成之后，该仓库的默认分支被设为 source，同时还有空白的 master 分支用于存放网页。

#### 设置域名
&nbsp;&nbsp;在 username.github.io 仓库首页选择`Settings`，向下拉，在`GitHub Pages`部分的`Custom domain`中填上自己的域名，点击`save`保存。此操作会在 master 分支下生成一个 CNAME 文件，里面就是刚填写的域名。

#### 配置 hexo 提交方式
&nbsp;&nbsp;编辑该文件夹下的`_config.yml`的`deploy`参数，分支应为 master。

默认生成的_config.yml：
```bash
# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type:
```

修改后的_config.yml：
```bash
deploy:
  type: git
  repo: 对应仓库的SSH地址（可以在 GitHub 对应的仓库中复制）
  branch: 分支（User Pages 为 master，Project Pages 为 gh-pages）
```

#### 修改博客及部署操作
&nbsp;&nbsp;修改博客内容后依次执行以下命令来提交网站相关的文件：
```bash
git add .
git commit -m "自定义内容即可"
git push origin source
```
&nbsp;&nbsp;然后执行以下任意一条生成网站并部署到 GitHub 上。
```
hexo generate -d
```
```
hexo g -d
```

&nbsp;&nbsp;这样一来，在 GitHub 上的 username.github.io 仓库就有两个分支，一个 source 分支用来存放网站的原始文件，一个 master 分支用来存放生成的静态网页。

#### 域名重置问题及解决方案

##### 问题
&nbsp;&nbsp;每次执行完`hexo g -d`之后，github 仓库设置中的 `Custom domain`总是被重置，导致域名访问出现 404 错误。

##### 解决方案
&nbsp;&nbsp;在 Hexo 生成的博客的 source 目录下新建一个 CNAME 文件，里面填上自己的域名即可。


## 博客管理

### 博客管理流程

#### 日常修改
&nbsp;&nbsp;在本地对博客进行修改（添加新博文、修改样式等等）后，通过下面的流程进行管理：

1. 依次执行`git add .`、`git commit -m "..."`、`git push origin source`指令将改动推送到 GitHub（此时当前分支应为 source）；
2. 然后才执行 `hexo g -d` 或 `hexo generate -d` 发布网站到 master 分支上。

#### 本地资料丢失
&nbsp;&nbsp;当重装电脑之后，或者想在其他电脑上修改博客，可以使用下列步骤：

1. 使用 `git clone git@github.com:username/username.github.io.git` 拷贝仓库（默认分支为 source）；
2. 在本地新拷贝的`username.github.io`文件夹下通过终端依次执行下列指令：`sudo npm install -g hexo-cli`、`sudo npm install`、`sudo npm install hexo-deployer-git`
