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

* network
```
/etc/init.d/network status #查看所有配置的设备
```

* ethtool   
```
ethtool ens5f1
ethtool ens5f1|grep Link # 查看连线
```

* lldptool  
```
lldptool -t -n -i ens5f1
lldptool -t -n -i ens5f1|grep -C 3 'Port ID TLV' # 端口
lldptool -t -n -i ens5f1|grep -C 3 'System Name TLV' # 交换机
```

* bond
`cat /proc/net/bonding/bond0`

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

* 获取IP
```
dhclient eth0
sed -i 's/static/dhcp/g' /etc/sysconfig/network-scripts/ifcfg-eth0
dhclient -r eth0
ifconfig eth0 0
cat /var/lib/dhclient/dhclient.leases
```

* ifcfg-eth0
```
TYPE=Ethernet # 以太网
BOOTPROTO=dhcp # dhcp 自动获取ip static
DEFROUTE=yes # 默认路由
PEERDNS=no # 不设置DNS
PEERROUTES=no # 是否从DHCP服务器获得默认网关的路由表条目信息。
IPV4_FAILURE_FATAL=no # yes 同时配置了 ipv4 和 ipv6 ,如果 ipv4 失败认为整体失败。
IPV6INIT=no # 禁用IPV6
NAME=eth0
DEVICE=eth0 
ONBOOT=yes # 开机自启动
```