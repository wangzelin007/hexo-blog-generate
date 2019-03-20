---
title: javascript04
tags: [js]
toc: true
mathjax: true
date: 2019-03-14 09:03:35
categories: javascript
---
7种数据类型
number/string/boolean/symbol/null/undefined/object

number
十进制 3
二进制 0b11 = 3
八进制 011 = 9
十六进制 0x11 = 17

string  
多行字符串
```
不推荐
var s1 = '12345 \
          67890'
推荐
var s2 = '12345' + 
         '67890'
ES6
var s3 = `12345
67890`
```

boolean
&& 与 || 或

null & undefined
1. 变量没有值 undefined
2. 空对象 unll
3. 空非对象 undefined

object
key 如果有引号，无限制 
如果没有引号遵循变量名命名规范
符合规范的也可以使用 person.name 方式 ，注意：name 表示 'name'
delete person.name

typeof
1. typeof null : object
2. typeof fn : function

btoa 转Base64
atob 转回
非ASCII码
btoa(encodeURI('王')) //encodeURIComponent
decodeURI(atob("JUU3JThFJThC")) //decodeURIComponent

转换

|-->|number|string|boolean|symbol|null|undefined|object|
|:---:|---|---|---|---|---|---|---|
|number|\|toString 或者 + ''|Boolean() 或者!!|||||
|string|.|\|!!|||||
|boolean|.|toString 或者 + ''|\|||||
|symbol|.|X||\||||
|null|.|toString报错 + ''|!!||\|||
|undefined|.|toString报错 + ''|!!|||\||
|object|.|toString 或者+ '' '[obj Obj]'|!!||||\|

老司机使用 + '' 代替 toString 也可以用 String()  
七个falsy值：  
flase 0 NaN '' "" null undefined  
所有对象都是true

str --> number
1. Number('1') === 1
2. parseInt('1',10) === 1
3. parseFloat('1.23') === 1.23
4. '1' - 0 === 1 推荐
5. `+ '1' === 1`

简单数据直接存在 Stack  
复杂数据在 Stack 存储 Heap 地址，是对内存的引用。

循环引用
var a = {}
a.self = a
a.self.self

面试题
var a = {n:1};
var b = a;
a.x = a = {n:2};
alert(a.x); //undefined
alert(b.x); //[object Object]

垃圾回收
如果一个对象没有被引用，将被回收。
var fn = function(){}
document.body.onclick = fn
fn = null //function(){} 不会被回收

深拷贝 vs 浅拷贝  
针对对象  
浅拷贝 var a=b