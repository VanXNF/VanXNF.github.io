---
title: Sublime Text 3 Ubuntu 18.04 无法输入中文解决方案
date: 2018-09-01 16:26:09
updated: 2018-09-01 16:26:09
tags: [Ubuntu 18.04 LTS, Sublime Text 3]
categories: Software
---

**&nbsp;&nbsp;本方案来自 GitHub 项目 [sublime-text-imfix](https://github.com/lyfeyaj/sublime-text-imfix) ， 感谢 [lyfeyaj](https://github.com/lyfeyaj) 的付出。**

---
#  前置条件
  - 已安装 Sublime Text 3
  - 已安装 Fcitx 输入框架
#  后续步骤
  1. 更新系统到最新
  ```
  sudo apt-get update && sudo apt-get upgrade
  ```
  2. 克隆项目到本地
  ```
  git clone https://github.com/lyfeyaj/sublime-text-imfix.git
  ```
  3. 进入项目文件夹
  ```
  cd sublime-text-imfix
  ```
  4. 执行修复脚本
  ```
  sudo ./sublime-imfix
  ```
  - 显示以下内容即修复成功：
  ```
  Done!

  Thanks for using this script to fix CJK Input Method problem of SublimeText 2/3.

  Re-login your X windows and start to use SublimeText 2/3 with Fcitx!
  ```
