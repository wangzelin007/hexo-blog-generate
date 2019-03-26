---
title: qemu001
tags: [qemu]
toc: true
mathjax: true
date: 2019-03-21 22:40:18
categories: qemu
---

### qcow2 镜像释放磁盘空间

#### 方法一

- 用0填满磁盘`dd if=/dev/zero of=~/junk`
- 释放空间 `rm junk`
- 关机`virsh shutdown kvm`
- 转换`qemu-img convert -O qcow2 source.qcow2 shrunk.qcow2`

#### 方法二

- 直接压缩转换`qemu-img convert -c -O qcow2 source.qcow2 shrunk.qcow2`