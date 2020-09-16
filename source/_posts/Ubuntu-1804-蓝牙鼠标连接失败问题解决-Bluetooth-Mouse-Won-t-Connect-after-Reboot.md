---
title: Ubuntu 1804 蓝牙鼠标连接失败问题解决 Bluetooth Mouse Won't Connect after Reboot
date: 2018-09-01 20:04:05
updated: 2018-09-01 20:04:05
tags: [蓝牙鼠标, Ubuntu 18.04 LTS, Bluetooth Mouse]
categories: Programming
---
&nbsp;&nbsp;方案主要参考自 [Ubuntu Forums](https://ubuntuforums.org/showthread.php?t=2390542)

* * *

&nbsp;&nbsp;首先 终端下输入
```
bluetoothctl
```
&nbsp;&nbsp;然后输入
```
list
```
&nbsp;&nbsp;看清楚 **Controller 的 mac 地址**，我的是 AC:2B:6E:91:65:4E ，在终端输入
```
select AC:2B:6E:91:65:4E
```
&nbsp;&nbsp;然后输入
```
show
```
&nbsp;&nbsp;**此时确保你的鼠标配对已打开，处于可被发现状态**，输入
```
scan on
```
&nbsp;&nbsp;在输出信息中找到你的鼠标后，即可输入
```
scan off
```
&nbsp;&nbsp;并记下你**鼠标的mac地址**，如果你的鼠标连接时要求 pin code，则输入以下命令，若不用则跳过这一条（当然不确定的话需不需要 pin code 就执行一下，也没什么影响的）。
```
agent on
```
&nbsp;&nbsp;接下来使用上一条记下的鼠标mac地址， 输入
```
pair DC:2C:26:AE:35:41
```
&nbsp;&nbsp;出现 Pairing successful，即配对成功，中间要求 pin code, 就输入对应 pin code即可。这时配对成功，但是鼠标还不能操作，依次输入
```
connect DC:2C:26:AE:35:41
trust DC:2C:26:AE:35:41
```
&nbsp;&nbsp;鼠标即可正常使用了。

&nbsp;&nbsp;{% post_link Windows-10-和-Ubuntu-18-04-LTS-双系统蓝牙鼠标连接问题的解决方案 %}
