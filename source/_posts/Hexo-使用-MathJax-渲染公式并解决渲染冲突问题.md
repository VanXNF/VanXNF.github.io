---
title: Hexo 使用 MathJax 渲染公式并解决渲染冲突问题
date: 2018-09-11 17:53:08
updated: 2018-09-11 17:53:08
tags: [Hexo, MathJax]
categories: Programming
---
&nbsp;&nbsp;Hexo 是默认支持 mathjax 公式渲染的，但依然需要解决渲染冲突。

# 更改渲染引擎
&nbsp;&nbsp;卸载默认渲染引擎并安装另一个：
```
npm uninstall hexo-renderer-marked --save
npm install hexo-renderer-kramed --save
```
&nbsp;&nbsp;这里的安装可能出问题，可以先更新一下 npm 再安装（需要权限）：
```
npm install -g npm
```

# 解决渲染冲突
&nbsp;&nbsp;然后更改  `/node_modules/hexo-renderer-kramed/lib/renderer.js` 中的：
```
// Change inline math rule
function formatText(text) {
    // Fit kramed's rule: $$ + \1 + $$
    return text.replace(/`\$(.*?)\$`/g, '$$$$$1$$$$');
}
```
&nbsp;&nbsp;为：
```
// Change inline math rule
function formatText(text) {
    return text;
}
```
&nbsp;&nbsp;然后找到博客目录下的 `/node_modules/kramed/lib/rules/inline.js`
进行下列修改：
```
//escape: /^\\([\\`*{}\[\]()#$+\-.!_>])/,      第11行，将其修改为
escape: /^\\([`*\[\]()#$+\-.!_>])/,
//em: /^\b_((?:__|[\s\S])+?)_\b|^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,    第20行，将其修改为
em: /^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
```
&nbsp;&nbsp;上面的改动取消了公式中 `_` 的渲染，原本会被渲染为 `<em>` 标签以表示斜体，在公式中表示下标。另外还取消了 `\, {, }` 的转义。

&nbsp;&nbsp;此时出现在公式中下标和换行的问题就完美解决了。

# 使用 LATEX 编辑公式
&nbsp;&nbsp;MathJax 是一个开源 JavaScript 库。它支持 LaTeX、MathML、AsciiMath 符号，可以运行于所有流行浏览器上。

&nbsp;&nbsp;这里已经配置好了，我们只需要了解 LATEX 语法来书写公式就可以了。

&nbsp;&nbsp;至于 LATEX 语法可参考:
- [markdown使用LaTex输入数学公式类](https://blog.csdn.net/u010185803/article/details/50865150)
- [Cmd Markdown 公式指导手册](https://www.zybuluo.com/codeep/note/163962#6%EF%BF%AF%EF%BE%BF%EF%BE%A5%EF%BF%AF%EF%BE%BE%EF%BE%A6%EF%BF%AF%EF%BE%BE%EF%BE%82%EF%BF%AF%EF%BE%BF%EF%BE%A4%EF%BF%AF%EF%BE%BE%EF%BE%BD%EF%BF%AF%EF%BE%BE%EF%BE%95%EF%BF%AF%EF%BE%BF%EF%BE%A8%EF%BF%AF%EF%BE%BE%EF%BE%BE%EF%BF%AF%EF%BE%BE%EF%BE%93%EF%BF%AF%EF%BE%BF%EF%BE%A5%EF%BF%AF%EF%BE%BE%EF%BE%85%EF%BF%AF%EF%BE%BE%EF%BE%A5%EF%BF%AF%EF%BE%BF%EF%BE%A7%EF%BF%AF%EF%BE%BE%EF%BE%9C%EF%BF%AF%EF%BE%BE%EF%BE%81%EF%BF%AF%EF%BE%BF%EF%BE%A7%EF%BF%AF%EF%BE%BE%EF%BE%95%EF%BF%AF%EF%BE%BE%EF%BE%A5%EF%BF%AF%EF%BE%BF%EF%BE%A5%EF%BF%AF%EF%BE%BE%EF%BE%8F%EF%BF%AF%EF%BE%BE%EF%BE%B7)
