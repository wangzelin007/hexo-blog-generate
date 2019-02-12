---
title: html语言学习01
toc: true
mathjax: true
date: 2019-01-27 22:05:08
tags: [html]
categories: Html
---
## 起源
+ HTML 全称 HyperText Markup Language **超文本标记语言**，常与CSS、JavaScript一起设计网页。
+ HTML 主要负责网站的**结构和内容**  
+ CSS 主要负责网站的**样式**  
+ JavaScript 主要负责网站的**行为**
+ HTML和CSS的标准均由W3C(万维网联盟)指定和发布
+ 本文主要介绍HTML5的常用标签

## HTML 学习网站
+ [<font color=#0099ff>MDN</font>](https://developer.mozilla.org/zh-CN/ "MDN")
+ [<font color=#0099ff>W3school</font>](http://www.w3school.com.cn/html5/index.asp "w3school")
+ [<font color=#0099ff>Quizlet</font>](https://quizlet.com/subject/html5/ "Quizlet")


## HTML 常用标签

### a anchor 锚元素
+ 可以创建一个到其他网页、文件、同一页面其他位置、电子邮件地址或者其他URL的超链接<br>
+ 描述部分可以嵌套img使用<br>
+ _top/_blank/_parent/_slef
+ 示例：  
`<a href="http://www.baidu.com">百度</a>`
+ 伪协议，待补充。  
`<a href="javascript:;" name="price">test</a>`

###head 
+ 定义网页相关元数据，如标题、引用的样式、脚本等
+ 示例：
```html
<html>
  <head>
    <title>文档标题</title>
  </head>
</html>
```

### body 
+ HTML body 元素表示文``档的内容。
+ 示例：`<body>内容</body>`

### footer
+ 定义网页页脚。页脚通常包含：作者、版权、相关链接等信息
+ 示例：`<footer>页脚</footer>`

### br break row
+ 强制换行
+ 示例：`<br>`

### hr horizontal rule
+ 水平线，常表示段落级元素之间的主题转换。
+ 示例：`<hr>`

### button 按钮
+ 示例：`<button name="button">Click me</button>`

### h1~h6 Heading
+ Heading元素呈现了六个不同级别的标题
+ 示例：`<h1>一级标题</h1>`

### p paragraph
+ 表示文本的一个段落
+ 示例: `<p>段落</p>`

### dl description list
+ 一个包含术语描述以及术语定义的列表，通常用于展示词汇表或者键-值对列表<br>

|子元素|全称                    |含义|
|:---:|-------------          |-------|
|dt   |description term       |描述术语 |
|dd   |description definition |术语定义 |  
+ 示例：
```html
<dl class="dt">
  <dt>Mac</dt>
  <dd>a computer</dd>
</dl>
```

### ul un-ordered list
+ 无序列表
+ 内部li代表list item
+ 示例：
```html
<ul>
  <li>橘子</li>
  <li>苹果</li>
  <li>橙子</li>
</ul>
```

### ol ordered list
+ 有序列表
+ 内部li代表list item
+ 示例：
```html
<ol>
  <li>第一名</li>
  <li>第二名</li>
  <li>第三名</li>
</ol>
```

### div HTML Content Division element
+ **没有默认样式**
+ HTML 网页分区元素
+ 通用型的流内容容器
+ block-level element
+ 示例：
```html
<div>
  <p>一切由你做主</p>
</div>
```

### span 
+ **没有默认样式**
+ 短语内容的通用行内容器
+ inline element
```html
<P><span>Some text</span></P>
```

### img image
+ 代表网页中的图像，如果无法显示图像，使用alt属性定义的内容替换
+ 显示图像：`<img src="mdn-logo-sm.png" alt="MDN">`
+ 图像链接：`<a href="#"><img src="mdn-logo-sm.png" alt="MDN"></a>`

### nav navigation bar
+ 导航栏，描绘一个含有多个超链接的区域
```html
<nav>
  <ul>
   <li><a href="#">Home</a></li>
   <li><a href="#">About</a></li>
   <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

### link
+ 定义了外部资源和当前文档的关系，最常用于链接样式表
示例：`<link href="default.css" rel="stylesheet" title="Fancy">`

### section
+ 章节，一般包含`<h1>-<h6>`
+ 示例：
```html
<section>
    <h1>Introduction</h1>
    <p>...</p>
</section>

<section>
    <h1>Equipment</h1>
    <p>...</p>
</section>
```

### form & input
+ form一个包含交互控件的区域(表单)
+ input 用于接受来自用户的数据,为基于表单创建交互式控件
+ 示例：
```html
<!--示例一-->
<form action="" method="get" class="form-example">
  <div class="form-example">
    <label for="name">Enter your name: </label>
    <input type="text" name="name" id="name" required>
  </div>
  <div class="form-example">
    <label for="email">Enter your email: </label>
    <input type="email" name="email" id="email" required>
  </div>
  <div class="form-example">
    <input type="submit" value="Subscribe!">
  </div>
</form>

<!-- 一个简单的表单，这个表单会发送一个 GET 请求 -->
<form action="">
  <label for="GET-name">Name:</label>
  <input id="GET-name" type="text" name="name">
  <input type="submit" value="Save">
</form>

<!-- 一个简单的表单，发送 POST 请求 -->
<form action="" method="post">
  <label for="POST-name">Name:</label>
  <input id="POST-name" type="text" name="name">
  <input type="submit" value="Save">
</form>

<!-- 使用 fieldset, legend, and label 的表单 -->
<form action="" method="post">
  <fieldset>
    <legend>Title</legend>
    <input type="radio" name="radio" id="radio"> <label for="radio">Click me</label>
  </fieldset>
</form>
```
+ 效果：
<form action="" method="get" class="form-example">
  <div class="form-example">
    <label for="name">Enter your name: </label>
    <input type="text" name="name" id="name" required>
  </div>
  <div class="form-example">
    <label for="email">Enter your email: </label>
    <input type="email" name="email" id="email" required>
  </div>
  <div class="form-example">
    <input type="submit" value="Subscribe!">
  </div>
</form>

<!-- 一个简单的表单，这个表单会发送一个 GET 请求 -->
<form action="">
  <label for="GET-name">Name:</label>
  <input id="GET-name" type="text" name="name">
  <input type="submit" value="Save">
</form>

<!-- 一个简单的表单，发送 POST 请求 -->
<form action="" method="post">
  <label for="POST-name">Name:</label>
  <input id="POST-name" type="text" name="name">
  <input type="submit" value="Save">
</form>

<!-- 使用 fieldset, legend, and label 的表单 -->
<form action="" method="post">
  <fieldset>
    <legend>Title</legend>
    <input type="radio" name="radio" id="radio"> <label for="radio">Click me</label>
  </fieldset>
</form>

### table
+ 二维表格数据
+ thead tbody tfoot
+ td table data tr table row th table head
+ col colgroup 待补充
示例：
```html
<p>Table with thead, tfoot, and tbody</p>
<table>
  <thead>
    <tr>
      <th>Header content 1</th>
      <th>Header content 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Body data 1</td>
      <td>Body data 2</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>Footer data 1</td>
      <td>Footer data 2</td>
    </tr>
  </tfoot>
</table>
```
效果：
<table>
  <thead>
    <tr>
      <th>Header content 1</th>
      <th>Header content 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Body data 1</td>
      <td>Body data 2</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>Footer data 1</td>
      <td>Footer data 2</td>
    </tr>
  </tfoot>
</table>

### small
+ 副标题，使文字变小一号
示例：`<small>word.</small>`

### strong
+ 强调语气，表示十分重要
示例：`<strong>words</strong>`

### bold
+ 粗体
示例：`<b>words</b>`

### kbd Keyboard Input
+ 键盘输入元素，表示用户数入
示例：`<kbd>Ctrl</kbd> + <kbd>S</kbd>`

### video
+ 嵌入视频内容
示例：
`<video src="videofile.ogg" autoplay poster="posterimage.jpg">葫芦娃01</video>`

### audio
+ 嵌入语音内容
示例：
`<audio src="audio.ogg" autoplay>葫芦娃02</audio>`

### svg Scalable Vector Graphics
+ 不规则图形
+ 未完待续

###iframe
+ 内联框架元素，将另一个HTML页面嵌入到当前页面
+ 示例：
```html
<iframe src="#" 
  title="iframe example 1" 
  width="400" 
  height="300">
</iframe>
```

## 空元素 empty element
+ 不存在子节点的元素
+ HTML中的空元素：
```html
<area>
<base>
<br>
<col>
<colgroup> when the span is present
<command>
<embed>
<hr>
<img>
<input>
<keygen>
<link>
<meta>
<param>
<source>
<track>
<wbr>
```

## 可替换标签
+ 可替换标签的展示不是由css控制，外观渲染独立。
+ HTML典型可替换元素：
```html
<img>
<object>
<video>
表单元素：<textarea> 、<input>
特殊情况下的可替换元素：<audio> 、<canvas>
``` 


