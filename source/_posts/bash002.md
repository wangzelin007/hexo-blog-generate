---
gtitle: bash002
toc: true
mathjax: true
date: 2019-02-01 17:08:37
tags: [bash]
categories: Linux
---

* du  
从小到大显示所有的文件(包含隐藏文件)  
`du -ahd1|sort -h`  
* egrep  
egrep "^[^#]" /etc/neutron.conf 不太理解

* crontab
```
*　　*　　*　　*　　*　　command  
分　时　日　月　周　命令
第1列表示分钟1～59 每分钟用*或者 */1表示  
第2列表示小时1～23（0表示0点）  
第3列表示日期1～31  
第4列表示月份1～12  
第5列标识号星期0～6（0表示星期天）  
第6列要运行的命令  
0 4 * * 0 /usr/bin/systemctl stop ntpd && /usr/sbin/ntpdate 192.168.0.1 && /usr/bin/systemctl start ntpd
```

* ln -s 源文件 链接文件

* 统计
  + ls -l|grep "^-"|wc -l
  + ls -l|grep "^d"|wc -l
  + -R 递归

* tar
  + tar -czvf target.tar.gz dir
  + tar -xzf source.tar.gz -C dir

* grep
  + grep -C 3 Failed (context around 3 lines)
  + grep -E '2019-03-18 18:4[0-9]|2019-03-18 18:5[0-9]' 正则匹配某个时间段的日志
  + grep -i 不区分大小写

* watch 
  + watch command
  + watch -n 60 command
  + watch -d ls -l 监控目录变化

* 获取用户输入，定义变量
  + read -p "Input the Instance Name: " InstName

* pidof
  + pidof haproxy