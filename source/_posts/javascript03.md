---
title: javascript03
tags: [js]
toc: true
mathjax: true
date: 2019-02-26 17:15:00
categories: javascript
---
函数作用域
全局作用域
块级作用域 ES6

**局部变量只能在函数内部声明**  
**其他区块声明的是全局变量**
```
if (true) {
  var x = 5;
}
console.log(x);  // 5
```

**函数内部也存在变量提升**  
**函数执行时所在的作用域，是定义时的作用域，而不是调用时所在的作用域**
例一
```
var a = 1;
var x = function () {
  console.log(a);
};

function f() {
  var a = 2;
  x();
}

f() // 1
```

例二
```
var x = function () {
  console.log(a);
};

function y(f) {
  var a = 2;
  f();
}

y(x)
// ReferenceError: a is not defined
```

例三
```
function foo() {
  var x = 1;
  function bar() {
    console.log(x);
  }
  return bar;
}

var x = 2;
var f = foo();
f() // 1
```

## 参数
**参数是原始类型（数字、字符、布尔），传值传递**  
```
var p = 2;

function f(p) {
  p = 3;
}
f(p);

p // 2
```
+ **参数是符合类型（数组、对象、其他函数），传址传递** 
  + 例外：如果替换掉整个参数，不会影响原始值，重新赋值导致指向另一个地址
```
var obj = { p: 1 };

function f(o) {
  o.p = 2;
}
f(obj);

obj.p // 2

---------------------

var obj = [1, 2, 3];

function f(o) {
  o = [2, 3, 4];
}
f(obj);

obj // [1, 2, 3]

```

## 闭包
**将函数内外连接的桥梁**  
**函数内部定义函数**  
作用：
+ 避免使用全局变量
+ 读取函数内部变量
+ 使它的诞生环境留存
+ 封装对象的私有属性和方法
缺点：
+ 内存消耗大  
**外层函数每次运行，都会生成一个新的闭包，而这个闭包又会保留外层函数的内部变量，所以内存消耗很大。**    
**在退出函数之前把不使用的局部变量全部删除** 

例一：
```
function f1() {
  var n = 999;
}

console.log(n)
// Uncaught ReferenceError: n is not defined
```
例二：
```
function f1() {
  var n = 999;
  function f2() {
    console.log(n);
  }
  return f2;
}

var result = f1();
result(); // 999
```
例三：
```
function createIncrementor(start) {
  return function () {
    return start++;
  };
}

var inc = createIncrementor(5);

inc() // 5
inc() // 6
inc() // 7
```
例四：
```
function Person(name) {
  var _age;
  function setAge(n) {
    _age = n;
  }
  function getAge() {
    return _age;
  }

  return {
    name: name,
    getAge: getAge,
    setAge: setAge
  };
}

var p1 = Person('张三');
p1.setAge(25);
p1.getAge() // 25
```

## 立刻调用函数表达式 IIFE
+ 不必为函数命名
+ 避免污染全局变量
+ 封装一些私有变量
```
// 写法一 bad
var tmp = newData;
processData(tmp);
storeData(tmp);

// 写法二 good
(function () {
  var tmp = newData;
  processData(tmp);
  storeData(tmp);
}());
```