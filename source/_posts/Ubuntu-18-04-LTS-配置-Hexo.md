---
title: Ubuntu 18.04 LTS 配置 Hexo
date: 2018-09-01 15:17:54
updated: 2018-09-01 15:17:54
tags: ["Ubuntu 18.04 LTS","Hexo"]
categories: Programming
---

GitHub Pages + Hexo 搭建博客可查看 {% post_link Ubuntu-18.04-LTS-GitHub-Pages-Hexo-搭建博客 %}

---

# 环境搭建
- **git**
首先需要在系统中安装git：`sudo apt install git`
可以先检查是否安装git：`git --version`
然后是对git的一些基本配置：
    ```
    git config --global user.name "username"
    git config --global user.email "youremail"
    ```
- **node.js**
安装：`sudo apt install nodejs`

- **npm**
npm ( nodejs的包管理工具)：`sudo apt insatll npm`
管理工具的使用：
升级新版npm：`sudo npm install npm -g`
使用npm安装模块：`npm install module_name`
查看所有全局安装的npm模块：`npm ls -g`
模块的卸载：`npm uninstall module_name`
更新模块：`npm update module_name`

# 安装 Hexo
1. 创建目录
    ```
    mkdir hexo
    ```
2. 切换目录
    ```
    cd hexo
    ```
3. 全局安装 Hexo
    ```
    sudo npm install -g hexo-cli
    ```
4. 初始化 Hexo
    ```
    hexo init
    ```
5. 运行 Hexo
    ```
    hexo server
    ```
    成功运行的话会提示：
    ```
    INFO  Start processing
    INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
    ```
# Hexo 主题
&nbsp;&nbsp;Hexo 主题可以从这里找：[https://hexo.io/themes/](https://hexo.io/themes/)
&nbsp;&nbsp;推荐安装主题 NexT
&nbsp;&nbsp;到目录 hexo 下：
```
cd ~/Documents/hexo/
git clone https://github.com/iissnan/hexo-theme-next themes/next
```
&nbsp;&nbsp;并在目录 hexo 下的 _config.yml 中找到 theme: 修改后面的参数，默认是 landscape，改为
```
theme: next
```
# 常用指令
- 新建博客项目，默认为指定的 folder 文件夹;
    ```
    hexo init [folder]
    ```
- 新建文章，总共有`post`、`draft`、`page`三种 layout，文章以你指定的 title 名创建，title 中如果有空格请使用“”括起来;
    ```
    hexo new [layout] <title>
    ```
- 生成静态文件，下面的代码为简写，可以添加 `-w` 参数监视文件的变动;
    ```
    hexo generate
    hexo g
    ```
- 启动本地服务器，可以添加参数 `-p` 指定服务器的端口，默认在端口4000
    ```
    hexo server
    hexo s
    ```
- 博客项目部署
    ```
    hexo deploy
    hexo d
    ```
- 一键静态文件生成与部署
    ```    
    hexo g -d
    hexo d -g
    ```
- 清楚缓存和生成的静态文件，对应于 db.json 和 public 目录下的文件
    ```
    hexo clean
    hexo cl
    ```
- 列出博客文件树
    ```
    hexo list route
    ```
