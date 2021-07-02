---
title: hexo教程001
date: 2019-01-25 11:02:55
tags: [hexo]
categories: Hexo
toc: true
mathjax: true
---
```
hexo new $name #新建文章
hexo generate #生成
hexo deploy 
hexo generate && deploy #部署
hexo s -g #启动服务预览
hexo clean #清除缓存
```

```
hexo new page categories
type: "categories"
categories: hexo

hexo new page tags
type: "tags"
tags: [hexo]

```

```
theme
git clone git@github.com:iissnan/hexo-theme-next.git
```