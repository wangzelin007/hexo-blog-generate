---
title: mysql-pt 套件使用 001
tags: [mysql]
toc: true
mathjax: true
date: 2019-02-26 11:13:07
categories: db
---
## percona-xtrabackup 
**不停机备份工具**  
`yum install -y percona-xtrabackup` 
 
连接mysql服务器  
`xtrabackup --user=DVADER --password=14MY0URF4TH3R --backup --target-dir=/data/backups/`  

创建备份  
`xtrabackup --backup --target-dir=/data/backups/`  

准备备份 -- 处理一致性  
`xtrabackup --prepare --target-dir=/data/backups/`  

恢复备份  
`rsync -avrP /data/backups/ /var/lib/mysql/`  
`rsync -avz /root/wzl/backups/ root@100.68.8.27:/var/lib/mysql/`  

修改权限  
`chown -R mysql:mysql /var/lib/mysql` 

跳过单个主备不一致
```
set global sql_slave_skip_counter=1;
start slave;  
```

查看每个表的数据大小  
**这个不准不要用！**  
`select table_name,table_rows,data_length/1024/1024 "data_length" from information_schema.tables where table_schema in ('neutron','keystone') order by table_rows desc;`

## percona-toolkit
依赖  
```
rpm -qa perl-DBI perl-DBD-MySQL perl-Time-HiRes perl-IO-Socket-SSL  
yum install -y perl-DBI perl-DBD-MySQL perl-Time-HiRes perl-IO-Socket-SSL perl-Digest perl-Digest-MD5 perl-TermReadKey  
```

安装  
```
https://www.percona.com/downloads/percona-toolkit/LATEST/  
rpm -ivh percona-toolkit  
rpm -ivh percona-toolkit-debuginfo  
```

确认  
```
pt-query-digest -help  
pt-table-checksum -help  
```

权限  
```
CREATE USER 'new_root'@'%' IDENTIFIED BY '***';    
GRANT ALL PRIVILEGES ON *.* TO 'new_root'@'%' IDENTIFIED BY '***' WITH GRANT OPTION;  
```

**--create-replicate-table** 只有第一次需要 
 
检查数据库的一致性  
`pt-table-checksum --nocheck-replication-filters --no-check-binlog-format --databases=neutron,keystone h=192.168.1.102,u=root,p=root,P=3306`  

检查表的一致性  
`pt-table-checksum --nocheck-replication-filters --no-check-binlog-format --replicate=neutron.checksums --create-replicate-table --databases=neutron --tables=haha h=192.168.1.101,u=root,p=123456,P=3306`  

只打印  
`pt-table-sync --replicate=neutron.checksums h=192.168.1.101,u=root,p=123456 h=192.168.1.102,u=root,p=123456 --print`  

执行修复  
`pt-table-sync --replicate=neutron.checksums h=192.168.1.101,u=root,p=123456 h=192.168.1.102,u=root,p=123456 --execute`  

## binlog
以二进制日志记录了所有的 DDL(数据定义) 语句 和 DML(数据操作) 语句。  
语句以事件保存，不包括查询语句，主要用于数据的恢复和复制。
```
show binary logs;
mysqlbinlog mysqld-bin.000001
-d -database
mysqlbinlog -d neutron mysqld-bin.000001 > neutron.txt
-D --disable-log-bin 禁用
mysqlbinlog -D mysqld-bin.000001
-s --short-form 只输出sql
--start-datetime
--stop-datetime
--start-position
--stop-position
```

**远程读取** 
```
-R --read-from-remote-server  
-h --host  
mysqlbinlog -R -h 192.168.0.1 -p root mysqld-bin.000001
```

