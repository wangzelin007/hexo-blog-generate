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
hexo generate && hexo deploy #部署
hexo s -g #启动服务预览
hexo clean #清除缓存
```

```
hexo new page categories 新建目录
type: "categories"
categories: hexo

hexo new page tags 新建tags
type: "tags"
tags: [hexo]

删除文件
hexo clean ~/hexo-blog/myBlog/source/categories/index-1.md
```

```
theme
git clone git@github.com:iissnan/hexo-theme-next.git
```