---
title: Hexo 主题同步
date: 2018-09-02 20:42:46
updated: 2018-09-03 19:07:32
tags: [Hexo, 主题]
categories: Programming
---

>写在前面，本篇解决方案针对的是以 {% post_link Ubuntu-18.04-LTS-GitHub-Pages-Hexo-搭建博客 %} 搭建出来的 Hexo 博客，但对一般搭建方法也有一定参考价值，具体请自行判断。

### 问题

&nbsp;&nbsp;由于修改`hexo`主题的默认设置需要使用`git`管理来方便备份，所以如何同步主题的设置也是一件很重要的事。

### 原因

&nbsp;&nbsp;[Hiker](https://github.com/iTimeTraveler/hexo-theme-hiker)的使用方法

```
git clone https://github.com/iTimeTraveler/hexo-theme-hiker.git themes/hiker
```

&nbsp;&nbsp;这样配置完其实`thems/next/`就是一个包含`.git/`的子项目仓库。所以在`push`主项目的时候不会上传子项目，子项目的文件夹是灰的，并且里面是空的。所以从远程仓库拉取的项目中是没有 Hiker 主题的。

<!-- more -->

### 解决

&nbsp;&nbsp;使用`fork + subtree`来解决这个问题。

&nbsp;&nbsp;首先要 fork 一下 Hiker 这个项目，然后拉取到本地做修改，修改好后 push 到远程仓库。然后用`git subtree`把`themes/hiker/`当做子项目来统一管理。

### 创建 subtree 步骤

- 首先进入 Hexo 博客所在的目录，本例子中是 `Hexo`。

- 新建名为 `themes` 的分支:

  ```
  git branch themes
  ```

  切换到 `themes` 分支:

  ```
  git checkout themes
  ```

- 绑定 `fork` 的 `hiker` 仓库：

  ```shell
  git remote add -f hiker git@github.com:username/hexo-theme-hiker.git
  ```

- 添加 `subtree`：

  ```
  git subtree add --prefix=themes/hiker hiker master
  ```

  这样就把 `fork` 之后的 `hiker` 的 `master` 分支所有 `checkout`出来的文件作为一次提交加到了 `Hexo` 项目的 `themes` 分支中。

- 合并 `themes` 分支到主分支 source：

  ```
  git checkout source
  git merge themes --squash
  git commit
  ```

### 提交对主题配置文件的修改

```
git checkout themes
git merge source
git subtree push --prefix=themes/hiker hiker master
```

&nbsp;&nbsp;这样提交之后 `fork` 的 `hiker` 主题仓库也会保持更新。

### 更新主题

```
git checkout themes
git subtree pull --prefix=themes/hiker hiker master
git checkout source
git merge themes --squash
git commit
```
