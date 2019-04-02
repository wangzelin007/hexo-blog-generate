---
title: javascript 函数
tags: [js]
toc: true
mathjax: true
date: 2019-03-27 08:33:10
categories: javascript
---

> 函数五种申明方法

**函数就是可以反复调用的代码块**
```
function f(arg1, arg2){return undefined} // f 全局
var f = function(arg1, arg2){return} // 匿名函数必须要赋值
var x = function f(){} // f 函数内
[√] console.log(x)
[x] console.log(f)
f = new Function('x', 'y', 'return x + y')
f = (x, y) => {return x + y} //箭头函数
f = (x, y) => x + y
f = x => x * x
```
> call
> this 是函数和对象间的羁绊
```
f()
f.call(undefined, arg1, arg2)
call 的第一个参数可以用 this 得到
call 后面的参数可以用 arguments 得到
undefined => this
[arg1, arg2] => arguments // 伪数组
```
调用堆栈 call stack，每进入一个函数，会记录位置，先进后出
递归有上限 -- stack overflow
如果一个函数，使用了范围外的变量，就是闭包
**面试题**
```
var f1 = function f2(){} // f1.name === 'f2' f2.naem 未定义

function f(){
	‘use strict'
	console.log(this)
	}
f.call(1) // if(use strict){1} else {Number 对象1}

var a = console.log(1) // a undefined

var a = (1,2) // a === 2

var liTags = document.querySelectorAll('li')
for (var i=0; i<liTags.length; i++){
  liTags[i].onclick = function(){
    console.log(i)
  }
}
// 点击li2 打印6
```
> apply
不确定参数个数时，使用apply
fn.apply(asThis, params)
> bind
bind 返回一个新的函数（没有调用），这个新函数会call原来的函数。
```
var view = {
  element: $('#div1'),
  bindEvents: function(){
    this.element.onclick = this.onClick.bind(this)
  },
  onClick: function(){
    this.element.addClass('active')
  }
}
```
> 柯里化/高阶函数
+ 柯里化
返回函数的函数
用于模板引擎和惰性求值
```
function Handlerbar(template){
  return function(data){
    return template.replace('{{name}}', data.name)
  }
}
var t = Handlerbar('<h1>Hi, I am {{name}}</h1>')
t({name:'frank'})
```
+ 高阶函数
  + 接受一个或多个函数作为输入
  + 输出一个函数
  + 同时满足两个条件
```
array.sort(function(a,b){a-b})
array.forEach(function(a){})
array.map(function(){})
array.filter(function(){})
array.reduce(function(){})
fn.bind.call(fn,{},1,2,3)
高阶函数的写法
array.filter(function(n){n%2===0}).reduce(function(prev,next){return prev+next},0)
reduce(filter(array, function(n){n%2===0}), function(prev,next){return prev+next},0)
sort(filter(array, function(n){n%2===1}), function(a,b){return a-b})
```
+ 回调
  + 被当做参数的函数就是回调
  + 一定会调用
  + 和同步异步无关
+ 构造函数
  + 返回对象的函数就是构造函数
  + 一般首字母大写
```
Number(1)
Object()
```
+ 箭头函数
  + 没有this

+ 理解函数
```
function curry(func , fixedParams){
    if ( !Array.isArray(fixedParams) ) { fixedParams = [ ] }
    return function(){
        let newParams = Array.prototype.slice.call(arguments); // 新传的所有参数
        if ( (fixedParams.length+newParams.length) < func.length ) {
            return curry(func , fixedParams.concat(newParams));
        }else{
            return func.apply(undefined, fixedParams.concat(newParams));
        }
    };
}
var abc = function(a, b, c) {
  return [a, b, c];
};
var curried = curry(abc);

curried(1)(2)(3);
// => [1, 2, 3]
curried(1, 2)(3);
// => [1, 2, 3]
curried(1, 2, 3);
// => [1, 2, 3]
```