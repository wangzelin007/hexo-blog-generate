---
title: javascript 标准库
tags: [js]
toc: true
mathjax: true
date: 2019-03-26 17:00:13
categories: javascript
---
加 new 生成对象，不加 new 生成基本类型
+ Number() 数字
+ String() 字符串
+ Boolean() 布尔值

------
加不加 new 都一样
+ Object()
+ Array()
> 用于构造数组的全局对象
> 数组是按顺序排列的一组值
```
不一致性
var a = Array(3) // 只申明了数组的长度
0 in a // false 
var a = Array(3,3) // a[0] = 3, a[1] = 3
等价
var a = [3,3]
```
Array.prototype
```
push
pop
shift
join
```
forEach 
```
三个参数分别是value,key,a
第三个参数不是必须的
a.forEach(function(x,y,[z]){
  console.log(x,y,z)
})
```
forEach 底层实现
```
var obj = {0:'a', 1:'b', length:2}
obj.forEach = function(x){
  for(let i=0; i<obj.length; i++){
    x(this[i], i)
  }
}
```
sort 
```
a.sort() // sort 会改变本身
a.sort(function(x,y){return x-y})
a.sort(function(x,y){return y-x})
```
其他
```
a.join() //默认逗号
a.concat(b)
var b = a.concat([]) //产生一个新数组
a.map(function(value, key){return value * 2})
a.map(value => value * 2)
a.filter(function(value, key){return value > 5})
a.reduce(function(x, y){return x + y}, 0) // x 指每一次的结果, y 指a的每一项, return 即下一次的x, 0 x的初始值 
a.reduce((x, y) => x + y, 0)
a.reduce(function(arr, n){
	arr.push(n * 2)
	return arr
	}, []) // 使用 reduce 实现 map
a.reduce(function(arr, n){
  if(n % 2 === 0){
    arr.push(n)
  }
  return arr
}, []) // 使用 reduce 实现 filter
```
题目
```
排序
var students = ['小明','小红','小花']
var scores = { 小明: 59, 小红: 99, 小花: 80 }
students.sort(function(x, y) {
    return scores[y] - scores[x]
    }
    
偶数的平方
var a = [1,2,3,4,5,6,7,8,9]
a.filter(x => x % 2 === 0).map(value => value*value)

基数的和
var a = [1,2,3,4,5,6,7,8,9]
a.reduce(function(x, y){
    if (y%2 === 1) {
        return x + y }
    else return x
}, 0)
```

arguments 伪数组

+ Function()
```
var f = function(a,b) {
  return a+b
}
var f = new Function('a', 'b', 'return a+b')
```
Function.prototype
```
call
bind
apply
```
