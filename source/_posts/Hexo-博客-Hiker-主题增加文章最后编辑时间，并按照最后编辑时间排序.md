---
title: Hexo 博客 Hiker 主题增加文章最后编辑时间，并按照最后编辑时间排序
date: 2018-09-03 16:12:07
updated: 2018-09-03 18:46:02
tags: [Hexo, Hiker, Updated, 更新时间]
categories: Programming
---

# 前言
&nbsp;&nbsp;写在前面，建好了 Hexo 博客之后，慢慢的文章也写了十几篇了，发现一个问题：无法知道这篇文章最后更新于什么时候。一篇文章发布得越早，就在越下面，可是我想让它把我重新编辑过的文章排到前头来啊，同时也想让文章能够显示最后更新于什么时候。有需求那就去解决啊，可是搜索了谷歌、百度，发现全世界都用的是 Next 主题，给的方案也是针对 Next 主题的，对我所用的 `Hiker 主题`完全不适用啊，于是，经过一番摸索，就有了这篇文章。废话结束了，下面开始正文。

# 开启 Updated 排序
&nbsp;&nbsp;在 Hexo 内部，是支持 updated 这个参数的，意思就是，你在建立文章的时候，已经默认地给你添加了一个名为 update 的参数。但这个数据只是添加在 db.json 中，并不会添加到你的 md 文件中。但它的效果其实和你直接在 md 文件中写是一样的，像下面这样：
```
title:
date:
updated:
tags:
categories:
```
&nbsp;&nbsp;但是写在 md 文件中更加的方便，能够手动的控制更新日期，避免 db.json 被删除后，‘更新日期’数据丢失的情况出现。因此我们需要让 Hexo 默认生成的 post格式中存在 `updated` 这个属性，以免每次需要手动输入。(手写是不可能手写的，这辈子都不可能的)

## 调整 post 默认生成格式
&nbsp;&nbsp;我的 Hexo 博客主目录为 `Hexo`，之后的操作就在这个目录下了。 post 的生成模板在  `Hexo/scaffolds/` 里，那个 `post.md`就是了。打开这个文件，因为生成的时候发布时间和最后更新时间一样的嘛，改成如下内容后保存即可：
```
---
title: {{ title }}
date: {{ date }}
updated: {{ date }}
---
```

&nbsp;&nbsp;这个时候你就可以生成一篇新的博客看看有没有效果了。你想加别的内容也是这样修改。之后修改了文章内容之后，把 updated 后面的时间改一下就 OK 了。

&nbsp;&nbsp;使用 Atom 写博客的快速输入 update 时间戳，可以查看 {% post_link 在-Atom-中快速输入时间戳 %}

## 调整 Hexo 主配置文件
&nbsp;&nbsp;然后找到主配置文件 `_config.yml`（**注意：不是主题的 _config.yml**），修改 index_generator 的 order_by 为 -updated 即可开启更新时间排序，你最后修改过的文章就会显示到最前面了:
```
# Home page setting
# path: Root path for your blogs index page. (default = '')
# per_page: Posts displayed per page. (0 = disable pagination)
# order_by: Posts order. (Order by date descending by default)
index_generator:
  path: ''
  per_page: 10
  order_by: -updated
```
&nbsp;&nbp;但是你发现修改过之后，文章只显示到时期，根本看不到时间对不对，那么继续修改 date_format 部分，改成如下的 `YYYY-MM-DD HH:mm:ss`格式，再重新生成一下网页就能看到具体的时间了。
```
# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD HH:mm:ss
time_format: HH:mm:ss
```

# 修改 Hiker 主题
&nbsp;&nbsp;Hiker 主题默认是没有更新时间显示的，所以需要自己修改，新增一个更新时间显示。`hiker` 文件夹位于 `Hexo/themes/hiker` 。首先查看了 `hiker/layout` 文件夹下的 `post.ejs` 文件，发现里面引入的是 `_partial/article`的内容，好的，找到  `hiker/layout/_partial` 文件夹下的 `article.ejs`，因为是修改时间嘛，那就找 date 相关的内容，于是找到了 9-13 行：
```
<div class="article-meta">
  <%- partial('post/date', {class_name: 'article-date', date_format: null}) %>
  <%- partial('post/category') %>
  <%- partial('post/busuanzi-analytics',{index: index, class_name: 'article-views'}) %>
</div>
```
&nbsp;&nbsp;看第10行，原来是引用的 `post/date`，那就打开 `hiker/layout/_partial/post` 文件夹下的 `date.ejs`，看到如下内容：
```
<% if (!is_current("about", false)){ %>
	<a href="<%- url_for(post.path) %>" class="<%= class_name %>">
	  <time datetime="<%= date_xml(post.date) %>" itemprop="datePublished"><%= date(post.date, date_format) %></time>
	</a>
<% } %>
```
&nbsp;&nbsp;到这里也就清楚了，我们主要需要关注的文件是 `hiker/layout/_partial/post/date.ejs`、`hiker/layout/_partial/article.ejs`，这两个文件。那么接下来开始修改。

## 新建 updated.ejs 文件
&nbsp;&nbsp;由于 `date.ejs` 这个文件在很多地方会被引用到，可谓是牵一发而动全身啊，如果你改在这个文件上，就会发现所有原本出现发布时间的地方同时还会有更新时间，看上去真的是有点丑啊。我不需要它在文章正文以外的部分出现更新时间，所以选择新建一个 `updated.ejs` 文件，就放在 `date.ejs` 所在的 post 文件夹。
`Updated.ejs` 内容如下：
```
<% if (!is_current("about", false)){ %>
	<a href="<%- url_for(post.path) %>" class="<%= class_name %>">
	  <%= __('updated') %> <time datetime="<%= date_xml(post.updated) %>" itemprop="dateUpdated"><%= date(post.updated, date_format) %></time>
	</a>
<% } %>
```
&nbsp;&nbsp;大体上与 date.ejs 内容相仿，post.date 改成了 post.updated，细心的读者还会发现，多了一个 `<%= __('updated') %>`，这是因为原来的格式只显示时间，那么当我们全部修改好之后，就会发现文章下面确实有两个时间，但不知道哪个是哪个，看的人很乱（这里不接受修改时间当然比发布时间迟的一看就知道了这样的吐槽），为了用户体验，还是加上提示比较好。同样的，可以将 `date.ejs` 的内容修改成如下所示：
```
<% if (!is_current("about", false)){ %>
	<a href="<%- url_for(post.path) %>" class="<%= class_name %>">
	  <%= __('published') %> <time datetime="<%= date_xml(post.date) %>" itemprop="datePublished"><%= date(post.date, date_format) %></time>
	</a>
<% } %>
```

## 增加字段
&nbsp;&nbsp;由于 date.ejs 和 updated.ejs 中分别引入了 published 和 updated 字段，因此我们需要去在语言文件中新增对应的字段，语言文件在 `hiker/languages`中，你博客设置成什么语言，就修改对应的语言文件，没指定就修改 default.yml 文件。这里以 default.yml 为例，打开文件，在最上面增加两行：
```
published: Published
updated: Updated
```
&nbsp;&nbsp;保存退出即可。简单解释一下，格式为`字段名：字段值`，字段名不变，字段值可以随意更改。

## 修改 article.ejs 文件
&nbsp;&nbsp;新增了一个 update.ejs 文件，我们需要将它引用进去。打开 article.ejs 文件，找到第 10 行： `<%- partial('post/date', {class_name: 'article-date', date_format: null}) %>`，在下面添加一行 `<%- partial('post/updated', {class_name: 'article-date', date_format: null}) %>`，保存退出即可。

# 最后
&nbsp;&nbsp;执行一下 `hexo g`、`hexo server` 看看效果：
![](https://s1.ax1x.com/2018/09/03/Pz4bi4.png)
