---
title: javascript09
tags: [js]
toc: true
mathjax: true
date: 2019-04-05 14:55:10
categories: javascript
---
> jQUERY
jQuery 的本质，选取元素，对其操作。
```
// 修改公共prototype
Node.prototype.getSiblings = function (){
  var allChildren = this.parentNode.children
  var array = {length:0}
  for (let i=0; i<allChildren.length; i++){
    if (allChildren[i] !== this){
      array[i] = allChildren[i]
      array.length += 1
    }
  }
  return array
}

Node.prototype.addClass = function (classes){
  for (let key in classes){
    var value = classes[key]
    method = value ? 'add' : 'remove'
    this.classList[method](key)
  }
}

item.getSiblings()
item.addClass({'a':true, 'b':false})
```

```
// 无侵入node
window.jQuery = function(nodeOrString){
  let node
  if(typeof nodeOrString === 'string'){
    node = document.querySelector(nodeOrString)
  } else {
    node = nodeOrString
  }
  
  return{
    getSiblings: function (){
  var allChildren = node.parentNode.children
  var array = {length:0}
  for (let i=0; i<allChildren.length; i++){
    if (allChildren[i] !== node){
      array[i] = allChildren[i]
      array.length += 1
    }
  }
  return array
},
    addClass: function (classes){
  for (let key in classes){
    var value = classes[key]
    method = value ? 'add' : 'remove'
    node.classList[method](key)
  }
}
  }
}
var node2 = jQuery (item)
node2.getSiblings()
node2.addClass({'a':true, 'b':false})
```

```
window.jQuery = function(nodeOrString){
  let nodes = {}
  if(typeof nodeOrString === 'string'){
    let temp = document.querySelectorAll(nodeOrString)
    for (let i=0; i<temp.length; i++){
      nodes[i] = temp[i]
    }
    nodes.length = temp.length
  } else if (nodeOrString instanceof Node){
    nodes = {
      0: nodeOrString,
      length: 1
    } 
  }
  
  nodes.addClass = function(classes){
    classes.forEach((value) => {
      for (let i=0; i<nodes.length; i++){
        nodes[i].classList.add(value)
      }
    })
  }
  
  nodes.text = function(text){
    if (text === undefined){
    	var texts = []
      for (let i=0; i<nodes.length; i++){
        texts.push(nodes[i].textContent)
      }
      return texts
    } else {
      for (let i=0; i<nodes.length; i++){
        nodes[i].textContent = text
      }
    }
  }
  return nodes
}
window.$ = jQuery;
var $node2 = $('ul > li')
$node2.addClass(['blue'])
```
> [jQuery中文文档](https://www.jquery123.com "jQuery中文文档")

> window.$ = jQuery (alias)
>
> jQuery 构造出来的对象也最好以 $ 开头

>
>
>jQuery 下载包的区别：
>
>+ production：压缩、转换后的的源码
>+ development： 源码
>+ map： 信息文件，记录了转换后的代码所对应的转换前的位置信息。

> jQuery 获取元素
>
> + by id：`$("#id")`
>
> + by class: `$(".classs")`
>
```
面试题 请说出 div 和 $div 的区别和联系：
<div id=x></div>
var div = document.getElementById('x')
var $div = $('#x')

$div 是 jQuery 对象，div 是 DOM 对象，不能混用对方的方法。
$div 得到的是[object Object] div 得到的是[object HTMLDivElement]
$div 转 div: $div[0] 或者 $div.get(0)
div 转 $div: $(div)
div 的属性和方法有 childNodes firstChid nodeType 等  
$div 的 属性和方法有 addClass removeClass toggleClass 等
```
+ 不要覆盖全局变量。
+ 使用局部变量，申明一个匿名函数，立刻调用  。
+ 解决立即执行报错 `() - + ! ~` 
+ ES6 let 可以表示局部变量，{} 是包不住 var 的。
+ 不要使用 $.show() $.hide() js 只控制行为，不控制样式，即只 add remove class