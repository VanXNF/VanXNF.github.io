---
title: Sublime Text 3 插件及注册码
date: 2018-09-01 19:31:35
updated: 2018-09-01 19:31:35
tags: [Sublime Text 3, 注册码]
categories: Software
---
### Sublime Text 3 注册码及破解

#### [**破解方案一**](https://gist.github.com/laptrinhcomvn/ae127424a9026f507a3c)
&nbsp;&nbsp;退出 sublime， 在终端输入以下代码:
```
printf'\x00\01'| sudo dd seek=$((0xD538)) conv=notrunc bs=1of=/opt/sublime_text/sublime_text
```
&nbsp;&nbsp;然后编辑 hosts 文件：
```
vim /etc/hosts
```
&nbsp;&nbsp;在最下方加入:
```
0.0.0.0 license.sublimehq.com
```
&nbsp;&nbsp;重新打开 sublime 即可。

#### **破解方案二**
输入以下注册码：
```
----- BEGIN LICENSE -----
sgbteam
Single User License
EA7E-1153259
8891CBB9 F1513E4F 1A3405C1 A865D53F
115F202E 7B91AB2D 0D2A40ED 352B269B
76E84F0B CD69BFC7 59F2DFEF E267328F
215652A3 E88F9D8F 4C38E3BA 5B2DAAE4
969624E7 DC9CD4D5 717FB40C 1B9738CF
20B3C4F1 E917B5B3 87C38D9C ACCE7DD8
5F7EF854 86B9743C FADC04AA FB0DA5C0
F913BE58 42FEA319 F954EFDD AE881E0B
------ END LICENSE ------
```
### 插件推荐
&nbsp;&nbsp;首先安装 Package Control 组件：按 Ctrl+ ` (此符号为 tab 按键上面的按键) 调出 console（注：避免热键冲突）到命令行执行以下代码：
```
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```
#### Emmet（原名 Zen Coding）
&nbsp;&nbsp;一种快速编写 html/css 的方法
#### html5
&nbsp;&nbsp;支持 hmtl5 规范的插件包
&nbsp;&nbsp;注意：与 Emmet 插件配合使用，效果更好
&nbsp;&nbsp;使用方法：新建 html 文档>输入 html5 >敲击 Tab 键>自动补全 html5 规范文档
#### jQuery
&nbsp;&nbsp;支持 JQuery 规范的插件包
#### javascript-API-Completions
&nbsp;&nbsp;支持 Javascript、JQuery、Twitter Bootstrap 框架、HTML5 标签属性提示的插件，是少数支持sublime text 3 的后缀提示的插件，HTML5 标签提示 sublime text 3 自带，不过 JQuery 提示还是很有用处的，也可设置要提示的语言。
&nbsp;&nbsp;安装方法（请阅读链接详情）：[http://www.ithao123.cn/content-10545789.html](http://www.ithao123.cn/content-10545789.html)
#### JSFormat
&nbsp;&nbsp;JS 代码格式化插件。
&nbsp;&nbsp;使用方法：使用快捷键 ctrl+alt+f
#### SublimeLinter
&nbsp;&nbsp;一个支持 lint 语法的插件，可以高亮 linter 认为有错误的代码行，也支持高亮一些特别的注释，比如 “TODO”，这样就可以被快速定位。（IntelliJ IDEA 的 TODO 功能很赞，这个插件虽然比不上，但是也够用了吧）
#### BracketHighlighter
&nbsp;&nbsp;类似于代码匹配，可以匹配括号，引号等符号内的范围。
&nbsp;&nbsp;使用方法：系统默认为白色高亮，可以使用链接所述方法进行自定义配置
[http://www.360doc.com/content/14/1111/15/15077656_424301780.shtml](http://www.360doc.com/content/14/1111/15/15077656_424301780.shtml)
#### Alignment
&nbsp;&nbsp;代码对齐，如写几个变量，选中这几行，Ctrl+Alt+A，哇，齐了。
#### Ctags
&nbsp;&nbsp;函数跳转，我的电脑上是 Alt+点击 函数名称，会跳转到相应的函数
#### Doc​Blockr
&nbsp;&nbsp;注释插件，生成优美的注释。标准的注释，包括函数名、参数、返回值等，并以多行显示，省去手动编写。
&nbsp;&nbsp;使用方法见：[http://www.cnblogs.com/huangtailang/p/4499988.html](http://www.cnblogs.com/huangtailang/p/4499988.html)
#### SideBarEnhancements
&nbsp;&nbsp;侧栏右键功能增强，非常实用
#### 主题
&nbsp;&nbsp;Boxy （[ihodev/sublime-boxy](https://link.zhihu.com/?target=https%3A//github.com/ihodev/sublime-boxy)）
&nbsp;&nbsp;Boxy（The most hackable theme for Sublime Text 3）自带多种主题风格，可以融合 [ihodev/sublime-file-icons](https://link.zhihu.com/?target=https%3A//github.com/ihodev/sublime-file-icons)，切换主题风格不必改配置。安装方法：
1\. `install package` -> Boxy Theme
2\. `install package` -> A File Icon
