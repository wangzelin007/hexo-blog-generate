---
title: 初识javascript02
tags: [js]
toc: true
mathjax: true
date: 2019-02-23 19:39:40
categories: javascript
---
* 事件
// 键盘事件  
onkeypress  
// 鼠标点击  
onclick  
// 错误  
onerror  
// 按住鼠标  
onmousedown  
// 移动鼠标  
onmousemove  
// 松开鼠标  
onmouseup  
// touch 事件  
ontouchstart  
ontouchmove  
ontouchend  

search js detect touch  
支持 touch null 不支持 touch undefined  
document.body.ontouchstart !== undefined  
'ontouchstart' in document.body  

getElementById  
createElement  
appendChild  

* 坐标
鼠标的坐标  
clientX  
clientY  
触控的坐标 // 注意有多点触控  
touches[0].clientX  
touches[0].clientY  
小 tips：  
(x-3) (y-3)  
**canvas 不需要**  

canvas 默认样式inline-block  
不能通过 css width height指定画布大小  
解决方案：  
获取初始viewport宽高  
var pageWidth = document.documentElement.clientWidth  
var pageHeight = document.documentElement.clientHeight  
canvas.width = pageWidth  
canvas.height = pageHeight  
动态调整  
window.onresize时再次获取   
## 初始化  
var ctx = canvas.getContext('2d')  

## 矩形
ctx.fillStyle = 'red';  
ctx.fillRect(10,10,100,100); //rectangle 矩形  
分别代表x,y,长,宽  

ctx.strokeStyle = 'yellow';  
ctx.strokeRect(10,10,100,100); //stroke 描边  

ctx.clearRect(50,50,10,10); //橡皮擦  

## 三角形
ctx.fillStyle = 'red';  
ctx.beginPath();  
ctx.moveTo(240,240);   
ctx.lineTo(300,240);  
ctx.lineTo(300,300);  
ctx.fill();  

## 圆弧
ctx.beginPath();  
ctx.arc(150,150,20,0,Math.PI*2); // x,y,半径,开始弧度,结束弧度  
弧度=(Math.PI/180)*角度。  
ctx.fill(); //填充    
ctx.stroke(); //描边  

canvas 画图时坐标是相对于viewport的而不是body  
1.可以去掉body的margin  

解决填充频率的方法：  
使用canvas在两点间画线  

## 画线
ctx.beginPath()  
ctx.moveTo(0,0)    
ctx.lineTo(100,0)   
ctx.stroke() //需要closePath闭合  
ctx.fill() //会自动闭合  
ctx.closePath()  

ctx.lineWidth = 10; //线宽  

点击开关  
eraserEnabled = !eraserEnabled  

关于画笔 橡皮檫  
使用两个按钮表示  
如果将if else 表示为平铺直叙，会减少代码bug  

禁用滚动  
preventDefault()  