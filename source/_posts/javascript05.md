---
title: javascript05
tags: [js]
toc: true
mathjax: true
date: 2019-03-17 20:13:41
categories: javascript
---
## JS 对象

全局对象window  
window. 可以省略  
mdn window 详细了解  

**ECMAScript 规定：**
+ parseInt  
+ parseFloat  
+ Number() 还可以初始化为对象  
+ String() 还可以初始化为对象  
+ Boolean() 还可以初始化为对象  
+ Object() 还可以初始化为对象  
+ setTimeout(function(){}, 3000) 指定时间 ms 后执行函数  

**私有：**
+ alert 弹窗  
+ prompt 输入框  
+ confirm 确认框  
+ console.log
+ console.dir 
+ document (文档) DOM
+ document.createElement
+ document.getElementById  
+ history (浏览器) BOM  

DOM
+ 获取元素父节点 parentNode，parentElement
+ 检测元素是标签还是文字 nodeType === 1,nodeType === 3
+ 子标签 children
+ 子节点(包括标签和文字) childNodes
+  获取下一个标签 循环访问 nextSibling 直到 nodeType === 1
+ 获取所有兄弟标签 声明空数组 siblings，遍历 div.parentNode.children，将 div 以外的元素 push 到数组里
+ DOM博客 http://luopq.com/2015/11/30/javascript-dom/

```
var n = 1
n.xxx = 2
n.xxx // undefined
var n = new Number(1)
n.xxx = 2
n.xxx // 2

var f1 = false
var f2 = new Boolean(false)
if(f1){console.log(1)} // 
if(f2){console.log(2)} // 2

s.charAt(0) 等同于 s[0]
s.charCodeAt(0) 获取ascii编码
s.charCodeAt(0).toString(16) 获取16进制ascii编码
s.trim() 去除字符串 python strip
```

## 原型链
共用属性 底层实现this  
proto 原型  
__proto__: Object 保存所有Object共用方法  
__proto__: Number __proto__: Object (Number 有两层)  
Boolean String 同 Number  
var 对象 = new 函数对象  
```
var o1 = new Object()
var o2 = new Object()
var n1 = new Number()
o1 === o2 // false
o1.toString() === o2.toString() // true
o1.toString() === n1.toString() // false
对象.__proto__ === 函数.prototype
o1.__proto__ === Object.prototype // true
n1.__proto__ === Number.prototype // true
n1.__proto__.__proto__ === Object.prototype // true
声明一个变量，会把 __proto__ 绑定到 prototype

Object.__proto__ === Function.prototype
Object.prototype.__proto__ === null
var function = new Function()
function.__proto__ === Function.prototype

// 另外，所有函数都是由 Function 构造出来的，所以
Number.__proto__ === Function.prototype // 因为 Number 是函数，是 Function 的实例
Object.__proto__ === Function.prototype // 因为 Object 是函数，是 Function 的实例
Function.__proto__ === Function.prototye // 因为 Function 是函数，是 Function 的实例！
```
