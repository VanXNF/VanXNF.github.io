---
title: Android Studio 资源文件分包
date: 2018-10-04 21:29:07
updated: 2018-10-04 21:29:07
tags: [Android]
categories: Android
---
# 写在前面
&nbsp;&nbsp;随着 Android 开发的不断推进，Android 项目内的资源文件会越来越多，在寻找时带来一些麻烦，因此对资源的分包势在必行。

# 资源分包
&nbsp;&nbsp;方法很简单，先创建好文件夹，然后配置 app 文件夹下的 `build.gradle` 文件，比如我的：
```
android {
    ...
    sourceSets {
        main {
            res.srcDirs('src/main/res', 'src/main/res_account')
        }
    }
}
```
&nbsp;&nbsp;此时 sync project 即可。要新增资源文件夹时也在此处操作。
