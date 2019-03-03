---
title: 初识javascript01
tags: [js]
mathjax: true
date: 2019-02-21 20:10:24
categories: javascript
---

**javascript 不一定要以;结尾**

```
var a = 1;
等价于
var a;
a = 1;
```

* 变量提升
```console.log(a);
var a = 1;
在实际代码执行中会变成：
var a;
console.log(a);
a = 1;
最后的结果是显示 undefined
```

* 变量命名规则  
  + 第一个字符，可以是任意 unicode 字符 (包括英文字母和其他语言的字母） ，以及美元符号 ($) 和下划线 (_)  
  + 第二个字符，除了 Unicode 字母、美元符号和下划线，还可以使用数字0-9。

* if 语句
```
if (m === 0) {
  // ...
} else if (m === 1) {
  // ...
} else if (m === 2) {
  // ...
} else {
  // ...
}
```

* switch 语句
```
var x = 1;

switch (x) {
  case 1:
    console.log('x 等于1');
    break;
  case 2:
    console.log('x 等于2');
    break;
  default:
    console.log('x 等于其他值');
}
```

* 三元运算符
```
（条件）? 表达式1 : 表达式2
var even = (n % 2 === 0) ? true : false;
```
* while 循环
```
var i = 0;
while(i < 100) {
  console.log(i)
  i += 1;
}
```
* for 循环 
```
var x = 3;
for (var i = 0; i < x; i++) {
  console.log(i)
}
```
* do while 循环
```
var x = 3;
var i = 0;
do {
  console.log(i);
  i++;
} while (i < x);
```
* label + break | continue
```
top:
  for (var i = 0; i < 3; i++){
    for (var j = 0; j < 3; j++){
      if (i === 1 && j === 1) break top;
      console.log('i=' + i + ', j=' + j);
    }
  }
// i=0, j=0
// i=0, j=1
// i=0, j=2
// i=1, j=0

top:
  for (var i = 0; i < 3; i++){
    for (var j = 0; j < 3; j++){
      if (i === 1 && j === 1) continue top;
      console.log('i=' + i + ', j=' + j);
    }
  }
// i=0, j=0
// i=0, j=1
// i=0, j=2
// i=1, j=0
// i=2, j=0
// i=2, j=1
// i=2, j=2
```
* NaN
  + NaN 特殊值，表示非数字
  + NaN 是数字类型，表示执行数学运算失败的结果
  + NaN === NaN //false