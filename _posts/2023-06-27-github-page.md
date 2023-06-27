---
layout: post
title: github-page网站绑定域名，及其过程中遇到的坑
categories: [github-page, giscus]
description: 
keywords: github-page, giscus 
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

### 绑定域名后，giscus评论组件无法正常显示
github中评论仓库的根目录里的giscus.json必须重新配置originsRegex属性的值，改为自己的域名，否则还用xx.github.io是渲染不出来的，没绑定域名之前是用的xx.github.io