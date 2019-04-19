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
>7.页面中有一个 SVG 标签，SVG 里面有一个直径为 100 像素的圆圈，颜色随意
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

> 请写出一个 HTTP post 请求的内容，包括四部分。
> 第四部分的内容是 username=ff&password=123
> 第二部分必须含有 Content-Type 字段
> 请求的路径为 /path

> 请说出至少三种排序的思路，这三种排序的时间复杂度分别为
O(n*n)
O(n log2 n)
O(n + max

> 一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？

> 如何实现数组去重？
> 不要做多重循环，只能遍历一次
请给出两种方案，一种能在 ES 5 环境中运行，一种能在 ES 6 环境中运行（提示 ES 6 环境多了一个 Set 对象）
```
array = [1,5,2,3,4,2,3,1,3,4]
```

