---
title: javascript08
tags: [js]
toc: true
mathjax: true
date: 2019-04-04 20:12:55
categories: javascript
---
>DOM Level0
+ onclick
+ onerror
+ onload
+ onmousexxx
+ 唯一，互相覆盖

![面试题](1.png)
> DOM Level2
+ 队列，先进先出
```
x. addEventListener('click', function(){})
x. removeEventListener('click', function(){})
```
+ one 
![one](2.png)
+ 捕获冒泡阶段 => 从上到下，从下到上
  + 自身同时存在捕获冒泡，使用队列模式
  + 非自身，按照捕获冒泡的顺序
![捕获冒泡](3.png)

> DOM API
Document Object Model  
>有点类似 ORM 一个是将数据库映射为对象，一个是将 documnet 映射为对象 , 主要功能是将页面中的节点通过对应的构造函数转换成对象

> Node 包含：
+ Documnet  
+ Element  
+ Text 
+ 其他(比如comment) 
> Node API 关键字：
+ child/children/parent
+ node/nodes
+ first/last
+ next/previous
+ sibling/siblings 兄弟
+ type
+ value/text/content
+ inner/outer
+ element
> Node 属性:
+ childNodes \\ 子节点
+ children \\ 子标签，不包含 text
+ firstChild lastChild \\ 包含text
+ firstElementChild lastElementChild \\ 不包含text
+ previousSibling nextSibling
+ previousElementSibling nextElementSibling
+ outerText innerText  // 触发重排，性能低；清除其他子元素
+ textContent // 包括 script 和 style；会返回隐藏元素文本 
+ nodeName nodeValue nodeType // 1 element 3 text
+ ownerDocument
+ parentElement parentNode

> DocumentFragment 优化

> Node 方法：
+ appendChild()
+ cloneNode(false)  // 默认浅拷贝，true 深拷贝
+ contains()
+ hasChildNodes()
+ insertBefore()
+ isEqualNode() // 相等
+ isSameNode() // 相同 ===
+ removeChild()
+ replaceChild()
+ normalize() // 常规化

> Document 属性
+ anchors // 弃用，获取所有a标签，必须要有name
+ body
+ characterSet // 字符编码
+ childElementCount 
+ children
+ doctype
+ documentElement // html 元素
+ domain // 域名
+ head
+ images
+ links // 获取所有a标签
+ location
+ onXxx
+ plugins // 插件
+ readyState 
+ referrer // 引荐人，从哪一个页面跳转来的，安全性
+ scripts
+ scrollingElement
+ styleSheets
+ title
+ visibilityState // 页面激活状态
> Document 方法
+ open()
+ close()
+ write()
+ wirteln() // writeline
+ createDocumentFragment()
+ createElement()
+ createNextNode()
+ execCommand()
+ exitFullscreen() // 退出全屏
+ getElementById()
+ getElementByClassName()
+ getElementByName()
+ getElementByTagName()
+ getSelection() // 获取选中文本
+ hasFocus()
+ querySelector() // 支持路径法 div > div; 伪数组
+ querySelectorAll()
+ registerElement()
> document 类似 file，都有open -> wirte -> close
```
document.write(1)
document.write(2)
setTimeout(()=>{
  document.write(3)
},3000) // 3 write 的危险性
```
> childNodes 是动态集合。DOM树删除或新增一个相关节点，都会立刻反映在NodeList接口中。
document.querySelectorAll返回的是一个静态集合。DOM内部的变化，并不会实时反映在返回结果之中。
```
var parent = document.getElementById('parent');
parent.childNodes.length // 假设是2
parent.appendChild(document.createElement('div'));
parent.childNodes.length // 3

var allDiv = document.querySelectorAll('div')
allDiv.length // 假设是 2
document.body.appendChild(  document.createElement('div')  )
allDiv.length // 2
```

> element 属性
+ attributes
+ childElementCount
+ children
+ classList
+ className
+ clientHeight clientWidth clientLeft clientTop
+ id
+ firstElementChild lastElementChild
+ innerHTML // 不要用，安全问题
> element 方法
+ querySelector()
+ querySelectorAll()

> HTMLCollection & NodeList
+ HTMLCollection实例对象的成员只能是Element节点，NodeList实例对象的成员可以包含其他节点。
+ HTMLCollection实例对象可以用id属性或name属性引用节点元素，NodeList只能使用数字索引引用。

> ChildNode
ChildNode是一个原始接口，它通过Element、DocumentType 和 CharacterData 对象实现。
+ ChildNode.remove()
+ ChildNode.before()
+ ChildNode.after()
+ ChildNode.replaceWith()