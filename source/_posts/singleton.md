---
title: singleton
tags: [singleton]
toc: true
mathjax: true
date: 2019-09-02 15:50:23
categories: singleton
---

单例模式的应用场景
1.windows 的 Task Manager
2.windows 的 Recycle Bin
3.网站的计数器
4.应用程序的日志
5.web应用的配置对象的读取
6.数据库连接池的设计
7.多线程的线程池的设计
8.操作系统的文件系统
9.HttpApplication

单例模式应用场景一般满足以下条件:
1.需要生成唯一序列的环境
2.需要频繁实例化然后销毁的对象。
3.创建对象时耗时过多或者耗资源过多，但又经常用到的对象。 
4.方便资源相互通信的环境
