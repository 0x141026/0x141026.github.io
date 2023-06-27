---
layout: post
title: github-page网站绑定域名，及其过程中遇到的坑
categories: [github-page, giscus, Jekyll]
description: 
keywords: github-page, giscus, Jekyll 
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

### 绑定域名后，giscus评论组件无法正常显:joy:
1. 首先在github中评论仓库里，根目录中的giscus.json必须重新配置originsRegex属性的值，改为自己的域名，否则还用xx.github.io是渲染不出来的，没绑定域名之前是用的xx.github.io
2. originsRegex指的是从哪个域名请求过来，比如绑定的域名是a.b.org,那么_config.yml<sup><a href="#ref1">1</a></sup>文件中的url的值必须也是a.b.org<sup><a href="#ref1">2</a></sup>




---
1. <p name = "ref1">Jekyll的配置文件,{{}}是Jekyll的语法</p>
2. <a name = "ref2" href="https://niejianzhou.cn">https://niejianzhou.cn</a>