---
title: neutron001
tags: [neutron]
toc: true
mathjax: true
date: 2019-04-03 15:17:27
categories: neutron
---
```
select * from ipallocations where ip_address='30.30.3.66';
```
port
```
neutron port-create net_id
指定ip
neutron port-create net_name --fixed-ip ip_address=192.168.2.40
```
