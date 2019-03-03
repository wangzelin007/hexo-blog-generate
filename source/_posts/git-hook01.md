---
title: 初识git-hook01
toc: true
mathjax: true
date: 2019-02-14 16:48:15
tags: [git]
categories: git
---
## git hook 简介
git hook可以在特定操作之前或者之后执行自定义的脚本

## 待研究
在提交代码后，自动部署静态页面
主要使用post-receive实现

## 客户端钩子
commit-msg
pre-commit 提交之前
post-commit 提交之后

## 服务器钩子
pre-receive 接受之前
update 更新之前
post-update 更新之后
post-receive 接受之后
