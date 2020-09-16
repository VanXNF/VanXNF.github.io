---
title: Sublime Text 3 配置 python3 编译环境（Ubuntu 18.04 LTS）
date: 2018-09-01 19:33:40
updated: 2018-09-01 19:33:40
tags: [Sublime Text 3, python, Ubuntu 18.04 LTS]
categories: Software
---

### 获取 python3 路径
&nbsp;&nbsp;在终端下输入
```
which python3
```
&nbsp;&nbsp;即可显示 python3 所在路径，记下这个路径。

### 新建编译配置文件
&nbsp;&nbsp;打开 sublime text 3，点击上部菜单栏 `Tools`->`Build System`->`new Build System`
清空新打开的模板，输入以下代码（ /usr/bin/python3 为第一步得到的路径）：
```
{
 "cmd": ["/usr/bin/python3", "-u", "$file"],
 "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
 "selector": "source.python"
 }
```
&nbsp;&nbsp;保存即可。

### 选择编译配置文件
&nbsp;&nbsp;点击上部菜单栏 `Tools`->`Build System` ，选择刚才保存的文件即可。
