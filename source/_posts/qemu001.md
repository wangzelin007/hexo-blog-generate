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

- 直接压缩转换`qemu-img 
- convert -c -O qcow2 source.qcow2 shrunk.qcow2`

### qcow2 镜像增加网卡
- virsh domiflist snale
- virsh attach-interface snale --type bridge --source br0  --config
- virsh dumpxml snale >/etc/libvirt/qemu/snale.xml
- virsh define /etc/libvirt/qemu/snale.xml
- virsh detach-interface snale  --type bridge --mac  52:54:00:14:86:cf  // 删除网卡

### 安装kvm
- yum -y install qemu-kvm libvirt virt-install bridge-utils
- systemctl start libvirtd && systemctl enable libvirtd

### error : Activation of org.freedesktop.machine1 timed out
service systemd-machined restart
service libvirtd restart
systemd-machined.service start operation timed out.

### virsh console 不能用
```
# add after </interface>
<serial type='pty'>
  <target port='0'/>
</serial>
<console type='pty'>
  <target type='serial' port='0'/>
</console>
```