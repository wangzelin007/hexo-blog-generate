---
title: interview001
tags: [interview]
toc: true
mathjax: true
date: 2019-04-08 21:06:58
categories: interview
---
>请写出一个符合 W3C 规范的 HTML 文件，要求
>
>1.页面标题为「我的页面」
>2.页面中引入了一个外部 CSS 文件，文件路径为 /style.css
>3.页面中引入了另一个外部 CSS 文件，路径为 /print.css，该文件仅在打印时生效
>4.页面中引入了另一个外部 CSS 文件，路径为 /mobile.css，该文件仅在设备宽度小于 500 像素时生效
>5.页面中引入了一个外部 JS 文件，路径为 /main.js
>6.页面中引入了一个外部 JS 文件，路径为 /gbk.js，文件编码为 GBK
>7.页面中有一个 SVG 标签，SVG 里面有一个直径为 100 像素的圆圈，颜色随意
>8.注意题目中的路径

```
<!doctype html>
<html lang="zh-Hans">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>我的页面</title>
    <link rel="stylesheet" href="style.css">
    <link rel="stylesheet" href="print.css" media="print">
    <link rel="stylesheet" href="mobile.css" media="(max-width: 500px)">
</head>
<body>
<svg width="600" height="600">
    <circle r="50" cx="200" cy="200" stroke="black" stroke-width="1" fill="red" />
</svg>
<script src="main.js"></script>
<script src="gbk.js" charset="GBK"></script>
</body>
</html>
```
> 移动端怎么做适配的
+ meta viewport
  `<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">`
+ 媒体查询
```
<script>
	@media (max-width: 960px) {css}
	@media (min-width: 320px) and (max-width:480px) {css}
</script>
<link ref="stylesheet" href="style.css" media="(max-width:320px)">
```
+ 动态 rem 方案
```
原理：
rem 是根据根元素的字体大小来设置元素宽高的，在不同屏幕尺寸中可以等比例缩放
1rem = 根元素字体大小
改变 html 的 font-size 可以等比例改变所有使用了 rem 的元素

在 scss 文件中添加
@function px2rem( $px ){
  @return $px/$designWidth*10 + rem;
}  
$designWidth : 640;

$designWidth 是设计稿的宽度
调用方式：px2rem(x)
```
+ 直接写两套，一套专门为移动端准备，后端根据userAgent切换


> 使用 css3 实现圆角矩形和阴影
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
    .rectangle {
      background: black;
      width: 300px;
      height: 300px;
      border-radius: 20px;
      box-shadow: 2px 2px 2px 1px red, inset 2px 2px 2px 1px yellow;
    }
  </style>
</head>
<body>
<div class="rectangle"></div>
</body>
</html>
box-shadow 参数含义：
inset 投影方向，默认向外投影，inset 向内投影
x-offset x轴偏移量
y-offset y轴偏移量
blur-radius 模糊半径
spread-radius 传播半径
color
```

> 什么是闭包，闭包的用途
> 定义在一个函数内部的函数，闭包本质上市将函数内部和函数外部连接起来的一座桥梁。
> 1.从外部读取函数内部的变量
> 2.让变量始终保存在内存中
> 3.封装对象的私有属性和私有方法
>
> ```
> var name = "The Window";
> 
> var object = {
>     name : "My Object",
>     getNameFunc : function(){
> 　　　　 return function(){
> 　　　　     return this.name;
> 　　　　 };
> 　　 }
> };
> 
> alert(object.getNameFunc()()); // The Window
> 　　
> var name = "The Window";
> 
> var object = {
> 　　 name : "My Object",
> 　　 getNameFunc : function(){
> 　　　　　var that = this;
> 　　　　　return function(){
> 　　　　　　　 return that.name;
> 　　　　　};
> 　　 }
> };
> 
> alert(object.getNameFunc()()); // My Object
> ```

> call、apply、bind 的用法
```
call(this,para1,para2)
apply(this,[para1,para2])
bind(this,para1,para2)
call 是函数正常的调用方式，第一个参数指定上下文this
apply 与 call 的区别是 apply 接收的是数组参数，call 接收的是连续参数。
bind 会生成新的函数，但不会立即执行，还需要调用()
例子：
function test(firstName, lastName) {
            console.log(this)
            console.log(`我的全名是"${firstName}${lastName}`)
        }
test.call('xxx','wang','zelin')
test.apply('yyy',['wang','zelin'])
let test1 = test.bind('zzz','wang','zelin')
test.bind('uuu','wang','zelin')()
test1()
```

> 说出常见的 HTTP 状态码和含义
>
> ```
> 200 OK 请求已成功，POST请求会包含操作结果的实体。
> 201 Created 资源已创建
> 202 Accepted 服务器已经接受请求，但还没有处理。
> 204 No Content服务器成功处理了请求，没有返回任何内容。
> 301 Moved Permanently 请求的资源已经永久移动到新位置。
> 302 Found 要求客户端执行临时重定向。
> 303 See Other 请求的响应可以在另外的URL找到。
> 304 Not Modified 不需要重新传输资源。
> 400 Bad Request 客户端错误，服务器不能处理请求。
> 401 Unauthorized 未认证。
> 403 Forbidden 服务器理解了请求，但拒绝执行。
> 404 Not Found 服务器未发现该资源。
> 405 Method Not Allowed
> 409 Conflict 请求存在冲突，如多个同步更新的冲突。
> 500 Internal Server Error 通用错误消息，服务器错误。
> 502 Bad Gateway 网关服务器执行请求时，从上游服务器接收到无效的响应。
> 503 Service Unavailable 临时的服务器维护，无法处理请求。
> 504 Gateway Timeout 网关服务器执行请求时，从上游服务器接收请求超时。
> ```
>
> 

> 请写出一个 HTTP post 请求的内容，包括四部分。
> 第四部分的内容是 username=ff&password=123
> 第二部分必须含有 Content-Type 字段
> 请求的路径为 /path
>
> ```
> 1 POST /path HTTP/1.1
> 2 Host: passport.baidu.com 
> 2 User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.103 Safari/537.36
> 2 Accept: application/json
> 2 Content-Length: 24
> 2 Content-Type: application/x-www-form-urlencoded
> 3
> 4 username=ff&password=123
> ```
>
> 

> 请说出至少三种排序的思路，这三种排序的时间复杂度分别为
O(n*n)
O(n log2 n)
O(n + max)
O(n*n):
插入排序：对于未排序的数据，在已排序序列中从后向前扫描，找到相应位置并插入
冒泡排序：重复的走访序列，依次比较相邻两个元素，知道没有相邻的元素需要排序
选择排序：从未排序序列中找min或者max，放到排序序列，再从剩余未排序序列中找min或max，放到排序序列，重复知道所有元素均已排序
O(n log2 n):
快速排序：冒泡排序的改进，每次选基准值，将数据分为比基准值要小的部分和比基准值要大的部分，递归进行，直到整个序列有序。
堆排序：
归并排序：
O(n*n):
基数排序：


> 一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？

> 如何实现数组去重？
> 不要做多重循环，只能遍历一次
请给出两种方案，一种能在 ES 5 环境中运行，一种能在 ES 6 环境中运行（提示 ES 6 环境多了一个 Set 对象）
```
array = [1,5,2,3,4,2,3,1,3,4]
```

