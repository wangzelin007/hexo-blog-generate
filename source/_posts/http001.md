---
title: http1.1学习
toc: true
mathjax: true
date: 2019-01-27 22:04:55
tags: [http]
categories: Http
---
## HTTP起源

### HTTP全称
HTTP即**HyperText Transfer Protocol**，**超文本传输协议**，是应用层协议，万维网的数据通信基础。本文主要介绍HTTP1.1。

### HTTP1.1改进  
+ 缓存处理
+ 带宽优化及网络连接的使用
+ 错误通知的管理
+ 消息在网络中的发送
+ 互联网地址的维护
+ 安全性及完整性

### HTTP2.0  
最初由google研发，2015年5月作为互联网标准正式发布。

![服务器与浏览器的交互](001.png "服务器与浏览器的交互")

## HTTP请求

### 请求四部分
+ 请求行
`GET /index.html HTTP/1.1`
+ 请求头
```
Cache-Control:max-age=0
Cookie:gsScrollPos=; _ga=GA1.2.329038035.1465891024; _gat=1
If-Modified-Since:Sun, 01 May 2016 11:19:03 GMT
User-Agent:Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.84 Safari/537.36
```
+ 空行
+ 消息体


### 请求方法8种
+ GET
  读取数据
+ HEAD
  与GET一样是发出资源请求，服务器不返回资源的文本部分。
+ POST
  提交数据（文件或表单）
+ PUT
  上传最新内容（多用于修改）
+ DELETE
  删除资源
+ TRACE
  回显服务器收到的请求，用于测试或诊断
+ OPTIONS
  返回资源支持的所有HTTP方法
+ CONNECT
  将连接改为管道方式的代理服务器，多用于SSL加密服务的连接。
  
### HTTP Header
[<font color=#0099ff>HTTP Header详细说明</font>](https://zh.wikipedia.org/wiki/HTTP%E5%A4%B4%E5%AD%97%E6%AE%B5 "HTTP-Header")

#### HTTP Header Content-Type
[<font color=#0099ff>Content-Type详细说明</font>](http://www.iana.org/assignments/media-types/media-types.xhtml "Content-Type")

+ 常用的Content-Type
  + Type application
  ```text
  application/EDI-X12   
  application/EDIFACT   
  application/javascript   
  application/octet-stream   
  application/ogg   
  application/pdf  
  application/xhtml+xml   
  application/x-shockwave-flash    
  application/json  
  application/ld+json  
  application/xml   
  application/zip

  ```
  + Type audio
  ```text
  audio/mpeg   
  audio/x-ms-wma   
  audio/vnd.rn-realaudio   
  audio/x-wav

  ```
  + Type image
  ```text

  image/gif   
  image/jpeg   
  image/png   
  image/tiff    
  image/vnd.microsoft.icon    
  image/x-icon   
  image/vnd.djvu   
  image/svg+xml
  ```
  + Type multipart
  ```text

  multipart/mixed    
  multipart/alternative   
  multipart/related (using by MHTML (HTML mail).)  
  ```
  + Type text
  ```text
  text/css    
  text/csv    
  text/html    
  text/javascript (已废弃)    
  text/plain    
  text/xml
  ```
  + Type video
  ```text
  video/mpeg    
  video/mp4    
  video/quicktime    
  video/x-ms-wmv    
  video/x-msvideo    
  video/x-flv   
  video/webm 
  ```

## HTTP响应

### 响应四部分
+ 状态行
`HTTP/1.1 200 OK`
+ 响应头
```
Connection:keep-alive
Content-Encoding:gzip
Content-Type:text/html; charset=utf-8
Date:Fri, 24 Jun 2016 06:23:31 GMT
Server:nginx/1.9.12
Transfer-Encoding:chunked
```
+ 空行
+ 消息体

### 响应状态码
[<font color=#0099ff>详细说明</font>](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81 "HTTP Status-code")

**常用status_code:**    
+ 1xx消息--请求已经被服务器接受，继续处理  
  不常用，略
  
+ 2xx成功--请求已成功被服务器接收、理解、并接受  
  常用响应如下：  
  + 201 Created：创建成功，返回URI
  + 202 Accepted：服务器已接受请求，多用于异步。
  + 204 No Content: 服务器成功处理了请求，不返回任何内容。

+ 3xx重定向--需要后续操作才能完成这一请求
  常用响应如下：
  + 301 Moved Permanently：资源已永久移动，在**Location**中返回新的若干个URI。
  + 302 Found：临时重定向
  + 303 See Other：为了替代302，实现POST后的GET重定向。
  + 304 Not Modified: 资源未改变，使用缓存。

+ 4xx请求错误--请求含有词法错误或者无法被执行
  常用响应如下：
  + 400 Bad Request：客户端明显错误
  + 401 Unauthorized：未认证
  + 403 Forbidden：拒绝执行
  + 404 Not Found：找不到资源
  + 405 Method Not Allowed
  + 408 Request Timeout
  + 409 Conflict
  + 423 Locked
  + 429 Too Many Requests
  
+ 5xx服务器错误--服务器在处理某个正确请求时发生错误
  常用响应如下：
  + 500 Internal Server Error:
  + 502 Bad Gateway:
  + 503 Service Unavailable
  + 504 Gateway Timeout

### HTTP—ETag

[<font color=#0099ff>详细说明</font>](https://zh.wikipedia.org/wiki/HTTP_ETag "ETag")

ETag提供一种**缓存验证**机制，如果资源改变，hash之后的ETag值就会变化。  
`ETag： "686897696a7c876b7e"`

![URL的常见组成](002.jpg "URL")

## CURL命令学习 

### 定义
Transfers data from or to a server.  
支持大多数协议，包括HTTP，FTP and POP3 ，这里主要介绍HTTP相关的。

### 全称
Command Line URL Viewer，是一个Linux命令行工具。

### 用法简介
+ 下载URL内容到文件[output]：  
  curl `http://www.baidu.com` -o filename
  
+ 将url输出保存在对应的文件名下[remote-name]：  
  curl -O `http://www.baidu.com/filename`

+ 跟随重定向[Location]，自动续传[Continue]，保存到对应的文件名下：  
  curl -O -L -C `http://www.baidu.com/filename`

+ 模拟post请求[data]:  
  curl -d 'name=bob' `http://www.baidu.com/form`

+ 指定method(默认GET）和[header]:  
  curl -H 'X-My-Header: 123' -X PUT `http://www.baidu.com`

+ 发送Json数据，指定content-type：  
  curl -d '{"name": "bob"}' -H 'Content-Type: application/json' `http://www.baidu.com/users/1234`
  
+ 使用用户认证[user authentication]：  
  curl -u username:password `http://www.baidu.com`

+ 传递客户端证书[certificate]和资源密钥[key]，跳过证书验证：  
  curl --cert client.pem --key key.pem --insecure `https://www.baidu.com`

+ silence & verbose  
  curl -s -v -- `http://www.baidu.com`