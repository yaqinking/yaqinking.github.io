---
layout: post
title:  "博客迁移到 Github"
date:   2015-03-08 19:40:00
categories: 日常
---

静态站点不折腾

不需要管数据库，不必管 WordPress 漏洞，自己可以写主题


开始前的注意事项

1. 说是用 Github Pages 生成漂亮的网页，其实官方文档说了，Github Pages 是用来生成展示项目的静态网页。
2. 说是用 Jekyll 来生成站点，其实 Jekyll 是用来本地观看自己博客的效果的（Github 自己会选择用是用 Github Pages 还是 Jekyll 生成你的网站）


步骤:


1. 创建一个 `yourusername.github.io`的 Repo
> 很重要，必须是 yourusername.github.io 这个 Repo,只有这个 Repo Github 才会给你用 Jekyll 生成。[官方原文](https://help.github.com/articles/using-jekyll-with-pages/)<br/>我会给你说，我先是尝试用各种 Repo 命名的地址，搞了几个小时都没搞出效果，然后还是看官方文档才知道，原来 Repo 命名必须是这样才可以。

2. Down 一个 Jekyll 主题，写好一个样例的 Post
> 当然，你可以自己写主题
3. 推送本地文件到该 Repo,好了，观看效果吧


## Git命令

`git init`

`git add .`

`git commit -m "First Post"`

`git remote add origin https://github.com/youusername/yourusername.github.io`

`git push -u origin master`

***

至于自己怎样折腾出来的，看教程啊，查官方 Help 啊，一个字就是**搞**


参考：


- [Jekyll offical website](http://jekyllrb.com/)
- [User, Organization, and Project Pages - Github help](https://help.github.com/articles/user-organization-and-project-pages/)
- [Using Jekyll with Pages - Github help](https://help.github.com/articles/using-jekyll-with-pages/)
- [jekyll sites](https://github.com/jekyll/jekyll/wiki/sites)