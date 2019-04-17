---
title: 初识network001
tags: [ip,route]
toc: true
mathjax: true
date: 2019-02-25 18:20:31
categories: network
---
* 网卡临时添加ip
```
ifconfig eth0 10.25.114.30 netmask 255.255.255.192 up
ifconfig eth0 30.30.3.67 netmask 255.255.255.192 broadcast 30.30.3.127 up
```

* 添加静态路由
```
route add -net 10.25.0.0/16 gw 30.30.3.65
route del -net 0.0.0.0/0 gw 192.168.68.229

route add -net 10.25.91.0 gw 10.25.114.1 netmask 255.255.255.0 dev eth0 metric 0
route del -net 10.25.91.0 gw 10.25.114.1 netmask 255.255.255.0 dev eth0

sudo route add -net default gw 10.25.60.161 netmask 0.0.0.0 dev eth0 metric 1
sudo route del -net default gw 10.25.60.161 netmask 0.0.0.0 dev eth0 metric 1

ip route add 10.25.0.0/16 via 10.25.60.161 dev eth0
```

* ethtool   
  `ethtool ens5f1`

* lldptool  
  `lldptool -t -n -i ens5f1`

* bond
  `cat /proc/net/bonding/bond0`

* 没有自动分配ip
  需要在/etc/sysconfig/network-scripts 里面增加 ifcfg-eth1 并且使用dhcp

* arp
  `arp -n|grep 30.30.3.66`

* vlan
  `cat /proc/net/vlan/config`

* cpu

  `cat /proc/cpuinfo | grep "cores"|uniq`

* 磁盘
```
fdisk -l|grep -i disk
vgs
cat /proc/partitions
partprobe -s
pvcreate /dev/sdb
vgextend VolGroup00 /dev/sdb
```