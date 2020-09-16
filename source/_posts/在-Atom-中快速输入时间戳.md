---
title: 在 Atom 中快速输入时间戳
date: 2018-09-03 18:30:58
updated: 2018-09-03 18:30:58
tags: [Atom, timestamps]
categories: Software
---

# 问题

&nbsp;&nbsp;如何在 Atom 中可以快速插入时间戳？

# 解决方案

## 修改 Atom 启动脚本
&nbsp;&nbsp;在 atom 中选择 `edit` -> `Preferences`会弹出 `Settings` 标签页，选择底部的 `Open Config Folder`，此时在弹出窗口找到 `~/.atom/init.coffee` ，在文件中添加如下代码：
```js
daysOfWeek = ['日', '一', '二', '三', '四', '五', '六']
pad = (str, length) ->
  str = String(str)
  str = '0' + str  while(str.length < length)
  str
dateOrTime = (kind) ->
  now = new Date()
  yyyy = now.getYear() + 1900
  mm = pad(now.getMonth() + 1, 2)
  dd = pad(now.getDate(), 2)
  ddd = daysOfWeek[now.getDay()]
  hh24 = pad(now.getHours(), 2)
  mi = pad(now.getMinutes(), 2)
  ss = pad(now.getSeconds(), 2)
  if kind == 1
    "#{yyyy}-#{mm}-#{dd} #{ddd})"
  else if kind == 2
    "#{hh24}:#{mi}:#{ss}"
  else
    # "#{yyyy}-#{mm}-#{dd}(#{ddd}) #{hh24}:#{mi}:#{ss}"
    "#{yyyy}-#{mm}-#{dd} #{hh24}:#{mi}:#{ss}"

insertText = (str) ->
  return unless editor = atom.workspace.getActiveTextEditor()
  selection = editor.getLastSelection()
  selection.insertText(str)

atom.commands.add 'atom-text-editor', 'atom-date:date', ->
  insertText(dateOrTime(1))
atom.commands.add 'atom-text-editor', 'atom-date:time', ->
  insertText(dateOrTime(2))
atom.commands.add 'atom-text-editor', 'atom-date:datetime', ->
  insertText(dateOrTime(0))
```

## 设置快捷键
&nbsp;&nbsp;编辑同一目录下的 `keymap.cson`，在里面添加如下代码：

```
'atom-text-editor':
  'alt-d': 'atom-date:date'
  'alt-t': 'atom-date:time'
  'alt-n': 'atom-date:datetime'
```

&nbsp;&nbsp;保存后重启 Atom。

## 使用方法

`Alt + d` : `2018-09-03-一)`

`Alt + t` : `18:44:41`

`Alt + n` : `2018-09-03 18:44:59`
