---
title: 初识network001
tags: [ip,route]
toc: true
mathjax: true
date: 2019-02-25 18:20:31
categories: network
---
* 网卡临时添加ip
ifconfig eth0 30.30.3.67 netmask 255.255.255.192 broadcast 30.30.3.127 up

* 添加静态路由
route add -net 10.25.0.0/16 gw 30.30.3.65

* ethtool 
ethtool ens5f1

* lldptool
lldptool -t -n -i ens5f1

