---
title: 'Hexo页面中嵌入豆瓣插件展示豆瓣图书电影'
copyright: true
date: '2022-11-29 17:05'
tags: 'Hexo'
categories: '个人博客'
---

## Hexo页面中嵌入豆瓣插件展示豆瓣图书电影

### 安装

```
npm install hexo-douban --save
```

### 配置
在博客站点的配置文件 _config.yml 中添加以下内容（注意：不是主题的配置文件）
```
# 豆瓣 
douban:
  id: 191537030
  book:
    path: books/index.html
    title: 'CodeRain 的书架'
    quote: ''
  movie:
    path: movies/index.html
    title: '刻骨铭心的电影'
    quote: '她'
  timeout: 10000 
```

- user: 你的豆瓣ID(纯数字格式，不是自定义的域名)。获取方法可以参考怎样获取豆瓣的数字 ID ？
- path: 生成页面后的路径，默认生成在 //yourblog/books/index.html 等下面。如需自定义路径，则可以修改这里。
- title: 该页面的标题。
- quote: 写在页面开头的一段话,支持html语法。
- timeout: 爬取数据的超时时间，默认是 10000ms ,如果在使用时发现报了超时的错(ETIMEOUT)可以把这个数据设置的大一点。
如果只想显示某一个页面(比如movie)，那就把其他的配置项注释掉即可。

### 主题兼容
对于使用 hexo-theme-butterfly 等使用 pjax 进行渲染的主题，需要在 _config.yml 中将豆瓣页进行排除，否则 js 会失效导致页面异常 @ISSUE 108 :
```
pjax:
  enable: true
  exclude:
    - /movies/
    - /books/
    - /games/
```

### 菜单
如果上面的显示没有问题就可以在主题的配置文件 _config.yml 里添加如下配置来为这些页面添加菜单链接.
```
menu:
  Home: /
  Archives: /archives
  Books: /books     #This is your books page
  Movies: /movies   #This is your movies page
  Games: /games   #This is your games page
```
注意这些页面不需要new创建 
而是使用`hexo douban -bmg`创建

### 使用
```
$ hexo douban -h
Usage: hexo douban

Description:
Generate pages from douban

Options:
  -b, --books   Generate douban books only
  -g, --games   Generate douban games only
  -m, --movies  Generate douban movies only
如果不加参数，那么默认参数为-bgm。
```
需要注意的是，通常大家都喜欢用hexo d来作为hexo deploy命令的简化，但是当安装了hexo douban之后，就不能用hexo d了，因为hexo douban跟hexo deploy的前缀都是hexo d。


官方指导文档：https://github.com/mythsman/hexo-douban

### 效果

执行`hexo douban -bm`

![](Hexo 页面中嵌入豆瓣插件展示豆瓣图书电影/2291368-20221129160808235-2056680578.png)
