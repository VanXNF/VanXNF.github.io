---
title: 'Exception: Java gateway process exited before sending its port number 解决方案'
date: 2019-03-15 15:09:01
updated: 2019-03-15 15:09:01
tags: [Exception, Spark]
categories: [Programming]
---
> 在阿里云轻量应用服务器上安装 Spark 时遇到了一个异常： `Exception: Java gateway process exited before sending its port number`，搜遍谷歌百度无法解决，花费数小时终于解决，特此记录。

## 问题及解决方案
&nbsp;&nbsp;首先，先来看看这个 Exception:
![Exception 本体](https://upload-images.jianshu.io/upload_images/3153051-6042f42137687b42.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

&nbsp;&nbsp;网上已有大量关于此 Exception 的问题、issues，但经过仔细筛选之后，发现和我遇到的这个问题还是有区别的。现有的问题大多是使用 PyCharm 或 Jupyter notebook 时遇到的问题，而我遇到这个 Exception 则是在执行 `pyspark` 命令时。

&nbsp;&nbsp;因此需要自己找一下问题所在了，这时候就需要读一读报错的日志了：
![日志](https://upload-images.jianshu.io/upload_images/3153051-9d52c1dc75807c2c.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

&nbsp;&nbsp;从日志中可以很明显的看到：
`Caused by: java.net.UnknownHostException: iZbp1a349oujk6t83ot6u1Z: iZbp1a349oujk6t83ot6u1Z: Name or service not known`
&nbsp;&nbsp;其中 `iZbp1a349oujk6t83ot6u1Z` 是服务器的主机名称，那么这个问题即是 Spark 无法识别出我的主机名导致的了，对于这种情况，我想到的一个方案是在 /etc/hosts 文件添加映射：
```bash
vim /etc/hosts
```
&nbsp;&nbsp;在文件中添加一行：
```bash
127.0.0.1       iZbp1a349oujk6t83ot6u1Z
```
&nbsp;&nbsp;保存退出。再次执行 `pyspark` 即可正常启动 pyspark 了。

![pyspark 成功启动](https://upload-images.jianshu.io/upload_images/3153051-b733ffff61fbe3f8.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 感想
&nbsp;&nbsp;这个问题只需读一读报错日志即可解决，但我一开始抱着偷懒的心态，首先想着通过搜索引擎获取现有的解决方案，在搜索、浏览信息和尝试解决方案上花费了大量时间，但最终还是没能解决问题。最终还是需要通过阅读错误日志，来定位真正的错误原因，从而针对性的解决问题，这才是最高效的解决方案。
