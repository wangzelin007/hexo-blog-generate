---
title: httpd
tags: [httpd]
toc: true
mathjax: true
date: 2019-03-18 14:24:02
categories: httpd
---
使用UTF-8编码，文件名全显示
`IndexOptions Charset=UTF-8 NameWidth=*`

正向代理
```
环境：
node-1 作为代理服务器
node-2 作为测试代理的客户端
1、在Node-1上面打开代理功能
[root@CNSZ046159 conf.d]# vim /etc/httpd/conf.modules.d/00-proxy.conf 
# This file configures all the proxy modules:
LoadModule proxy_module modules/mod_proxy.so
LoadModule lbmethod_bybusyness_module modules/mod_lbmethod_bybusyness.so
LoadModule lbmethod_byrequests_module modules/mod_lbmethod_byrequests.so
LoadModule lbmethod_bytraffic_module modules/mod_lbmethod_bytraffic.so
LoadModule lbmethod_heartbeat_module modules/mod_lbmethod_heartbeat.so
LoadModule proxy_ajp_module modules/mod_proxy_ajp.so
LoadModule proxy_balancer_module modules/mod_proxy_balancer.so
LoadModule proxy_connect_module modules/mod_proxy_connect.so
LoadModule proxy_express_module modules/mod_proxy_express.so
LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so
LoadModule proxy_fdpass_module modules/mod_proxy_fdpass.so
LoadModule proxy_ftp_module modules/mod_proxy_ftp.so
LoadModule proxy_http_module modules/mod_proxy_http.so
LoadModule proxy_scgi_module modules/mod_proxy_scgi.so
LoadModule proxy_wstunnel_module modules/mod_proxy_wstunnel.so
ProxyRequests On   #####打开代理功能
2、在Node-1上面配置代理的端口和允许通过的IP
[root@CNSZ046159 conf.d]# vim /etc/httpd/conf.d/001-default.conf 
Listen 8080     
<VirtualHost *:8080>
        Servername  172.25.56.21
        DocumentRoot /var/www/
        ProxyRequests On
        ProxyVia On
        <Proxy *>
           Order Deny,Allow
           Deny from all
           Allow from 172.25.56.22 172.25.56.23 127.0.0.1 
        </Proxy>
        ErrorLog /var/log/httpd/error.log
        LogLevel warn
        CustomLog /var/log/httpd/access.log combined
</VirtualHost>
3、重启Node-1上面的httpd
4、在Node-2上面使用如下命令，可以测试是否代理成功。
[root@CNSZ046161 ~]#  curl -x  172.25.56.21:8080 -I https://www.baidu.com
HTTP/1.0 200 Connection Established
Proxy-agent: Apache/2.4.6 (CentOS)
HTTP/1.1 200 OK
Server: bfe/1.0.8.18
Date: Thu, 24 Nov 2016 13:14:26 GMT
Content-Type: text/html
Content-Length: 277
Connection: keep-alive
Last-Modified: Mon, 13 Jun 2016 02:50:21 GMT
ETag: "575e1f6d-115"
Cache-Control: private, no-cache, no-store, proxy-revalidate, no-transform
Pragma: no-cache
Accept-Ranges: bytes
监控：
curl -x 100.68.5.204:8080 -I http://10.25.83.81:12057/api/global_push
bonree：
curl -x 100.68.5.204:8080 -I http://api.bonree.com/BigDataCenter
ddos：
curl -x 100.68.5.204:8080 -I https://api.ucloud.cn
```
参考资料：
https://httpd.apache.org/docs/current/mod/mod_proxy.html#forwardreverse

----

反向代理
```
重定向：（perl语言）
step1：
/etc/httpd/conf/httpd.conf
LoadModule rewrite_module modules/mod_rewrite.so
step2：
vim /etc/httpd/conf.d/virtual.conf
<VirtualHost *:80>
        ServerName cloudgear.paic.com.cn
        ErrorLog logs/cloudgear-error.log
        CustomLog logs/cloudgear-access.log common
        RewriteEngine on
        RewriteCond  %{HTTP_HOST} ^(cloudgear.paic.com.cn)
        RewriteRule ^/(.*) http://cloudgear.paic.com.cn:8081/ [L]
```
参考资料：
http://www.cnblogs.com/juandx/p/5339571.html
http://man.linuxde.net/htpasswd