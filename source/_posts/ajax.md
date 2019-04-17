---
title: ajax
tags: [ajax]
toc: true
mathjax: true
date: 2019-04-14 14:33:38
categories: ajax
---
> 问题
+ 用 form 可以发请求，但是会刷新页面或者新开页面
+ 用 a 可以发 get 请求，但是会刷新页面或新开页面
+ 用 img 可以发 get 请求，只能以图片形式展示
+ 用 link 可以发 get 请求，只能以 CSS、favicon 形式展示
+ 用 script 可以发 get 请求，只能以脚本形式运行

> AJAX
> Asynchronous JavaScript and XML 

> 什么是AJAX：
+ XMLHttpRequest 解决了发请求的难题
+ 服务器返回 XML 格式字符串 (现在一般都使用 json 格式)
+ JS 解析 XML，并更新局部页面

```
面试题：请使用原生 JS 来发送 AJAX 请求
myButton.addEventListener('click', (e)=>{
  let request = new XMLHttpRequest()
  request.open('GET', '/xxx')
  reqeust.send()
  request.onreadystatechange = ()=>{
    if(request.readyState === 4){
      console.log('请求响应完毕')
      if(request.status >= 200 && request.status < 300){
        console.log('请求成功')
        console.log(request.responseText)
        \\ xml
        let parser = new DOMParser();
        let xmlDoc = parser.parseFromString(request.responseText,"text/xml");
        let title = xmlDoc.getElementsByTagName('heading')[0].textContent
        \\ json
        let string = request.responseText
        let object = window.JSON.parse(string)
        console.log(title)
      }else if(request.status >= 400){
        console.log('请求失败')
      }
    }
  }
})
```
+ request.readyState === 4 代表请求结束

JS VS JSON 
+ JSON 没有 function、undefined、变量  
+ JSON 字符串首尾必须是双引号 ” 
+ JSON 支持 number string null object array boolean

> ajax 只有协议+端口+域名 一模一样才允许发请求 (同源策略)
> readystate === 0
> No Access-Control-Allow-Origin 错误 

> CORS  Cross-Origin-Resource-Sharing 跨域资源共享
> 后台增加响应头
`response.setHeader('Access-Control-Allow-Origin', 'http://允许的网站')`





















































