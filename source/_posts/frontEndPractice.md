---
title: 「JS-React-Redux+Dva」前端项目实践总结
date: 2018-12-27
author: renxiaoyuan
category: front end practice
tags: 
- 前端练习
---
### No.1 网页布局基础学习，实现静态聊天网页
<!--more-->
任务1：
使用HTML+CSS+JS完成一个本地聊天Demo（模仿JTalk-PC），达到输入文本信息后，展示带有样式的内容。

涉及内容：
*   认识HTML标签
*   学习css属性，了解css与html相互作用基础
*   了解网页骨架结构的搭建，学习骨架的搭建，组件的划分
*   认识javascript语法、函数、变量、数据类型、作用域、事件、运算符、字符串、调试、闭包、代码规范
*   了解flex布局方案，学习弹性布局的作用
*   布局调试工具的学习使用

重点：
##### - Html元素类型：块级元素、内联元素(又叫行内元素)、内联块级元素。

针对问题：
开始时使用float浮动布局，因为这个方法破坏了文档流造成高度塌陷，出现多处定位问题，后仔细了解行内块级元素布局方法，完成页面布局。

内联元素（行内）：display：inline；/<a>、<span>、<i>、<em>、<strong>、<label>、<q>
1、和其他元素都在一行上；
2、元素的高度、宽度及顶部和底部边距不可设置；
3、元素的宽度就是它包含的文字或图片的宽度，不可改变。

块级（独占一行）：display：block；/<div>、<p>、<h1>...<h6>、<ol>、<ul>、<dl>、<table>、<address>、<blockquote> 、<form>
1、每个块级元素都从新的一行开始，并且其后的元素也另起一行。（霸道，一个块级元素独占一行）
2、元素的高度、宽度、行高以及顶和底边距都可设置。
3、元素宽度在不设置的情况下，是它本身父容器的100%（和父元素的宽度一致）

行内块：display：inline-block；float:left / right；position：absolute/fixed;<img>、<input>
1、和其他元素都在一行上；
2、元素的高度、宽度、行高以及顶和底边距都可设置

##### - Flexbox 弹性布局

针对问题：寻找将整个Div内容居中在屏幕中心的办法



### No.2 React学习，使用React框架重构前期内容
任务2：
使用React重构完成Demo2，将网页组件化，并完成前端与服务器间的数据操作，做到用户输入消息，请求到服务器，并从服务器返回此消息作为回复。

涉及内容：
* 学习异步编程ajax、Promise、fetch、setTimeout、setInterval
* 根据之前的静态页面，实现静态页面的前端功能
* 认识React框架基础，掌握React生命周期，以及基本代码API

React：
//学习参考
https://segmentfault.com/a/1190000012921279#articleHeader18

* React是一个用来构建UI的JS库，满足前端组件化开发模式。
* babel编译器和webpack打包工具封装在creat-react-app的脚手架中。
* 通过 JS函数 创建无状态组件，通过 class 创建有状态组件，以此将「单纯展示数据」的组件和「有业务逻辑、需要操作数据」的组件分离


重点：
##### - React的生命周期
![52979da4449e861a7a689caf11c1472c](「JS-React-Redux+Dva」前端项目实践总结.resources/97CB38A0-284A-452A-9F76-46F8C231346C.png)
组件的生命周期是从创建到挂载再到卸载的一个完整周期。
这三个阶段总是伴随着组件各种各样的事件，这些事件被统称为组件的生命周期函数。

![80da15d7e472e924045037a705357d66](「JS-React-Redux+Dva」前端项目实践总结.resources/屏幕快照 2018-12-26 上午11.33.53.png)

##### - 异步编程
Javascript语言的执行环境是"单线程"，使用异步模式避免耗时长的操作造成浏览器失去响应。
在Demo2中使用了Ajax操作。

###### AJAX：
是一种在无需重新加载整个网页的情况之下能够更新部分网页的技术。
GET - 从指定的资源请求数据
POST - 向指定的资源提交要处理的数据

使用Ajax请求一个 JSON 数据一般是这样：
``` 
//创建XHR对象
var xhr = new XMLHttpRequest();

//规定请求的类型、URL 以及是否异步处理请求
xhr.open('GET', url/file,true);

//规定当服务器响应已做好被处理的准备时所执行的任务
xhr.onreadystatechange = function() {
   if(xhr.readyState==4){
        if(xhr.status==200){
            //获得字符串形式的响应数据。
            var data=xhr.responseText;
             console.log(data);
   }
};
xhr.onerror = function() {
  console.log("Oh, error");
};

//将请求发送到服务器
xhr.send();
```

使用fetch请求JSON数据：
```
//解析为可读数据
fetch(url).then(response => response.json())

  //执行结果是 resolve就调用then方法
  .then(data => console.log(data))
  
  //执行结果是 reject就调用catch方法
  .catch(err => console.log("Oh, error", err))
```

###### Fetch：
语法简洁，更加语义化； 基于标准 Promise 实现。

###### Promise：
![927bbd870f11b415d20daecfd4f41771](「JS-React-Redux+Dva」前端项目实践总结.resources/821879ED-E24B-4EC7-B1CC-F2922FF7B9AD.png)

fetch方法返回一个Promise对象, 根据 Promise Api 的特性, fetch可以方便地使用then方法将各个处理逻辑串起来, 使用 Promise.resolve() 或 Promise.reject() 方法将分别返会肯定结果的Promise或否定结果的Promise, 从而调用下一个then 或者 catch，catch用来指定reject的回调。

### No.3 Redux、Dva学习，将Demo移植到项目中
任务3：
使用Dva完成Demo3，掌握一次开发的完整过程，在Demo3中完成发送一条消息，能够获取服务器的数据并进行回复展示。

涉及内容：
* 学习异步编程ajax、Promise、fetch、setTimeout、setInterval
* 根据之前的静态页面，实现静态页面的前端功能
* 认识React框架基础，掌握React生命周期，以及基本代码API
* 理解Redux概念和Dva概念

###### Redux：
![1a7d0d5dc04e98b11e23dd74b9f88e74](「JS-React-Redux+Dva」前端项目实践总结.resources/CDFF4472-A7AF-403D-9F20-CF0CF739A555.png)
Redux 是 JavaScript 状态容器，在react项目中，搭配redux数据流开发，将UI层和数据层区分开。惟一改变 state 的办法是触发 action，通过编写 reducers 来描述 action 如何改变 state 。

![3f7144bc6d26e2789ef1a43fbe79c45a.svg+xml](evernotecid://33B584DC-2D43-4939-B991-F9CA2DCFA61C/appyinxiangcom/21119224/ENResource/p59)
![09a5b1d8a4d72944514f519dad429cc3.svg+xml](evernotecid://33B584DC-2D43-4939-B991-F9CA2DCFA61C/appyinxiangcom/21119224/ENResource/p60)
对于没有父子关系的组件需要进行通信的情况，redux在组件树中使用store容器，令组件dispatch状态更改到store中。store中包含的就是更新state的reducers，使得所有的状态更改都通过单一store进行。容器组件使用 React Redux 的 connect() 方法来生成。

![a058737cfdfabe7c26b2067a6c9cdca9](「JS-React-Redux+Dva」前端项目实践总结.resources/IMG_253D59F745E8-1.jpeg)

而Dva在redux数据流方案上，简化了开发体验，额外内置了 react-router 和 fetch。
![bce2b927616d6004d6a5135ff3f20c54](「JS-React-Redux+Dva」前端项目实践总结.resources/9B9ED88F-BD94-4EA5-995C-4DCD0200605A.png)
Dva 通过 model 的概念把一个领域的模型管理起来，包含同步更新 state 的 reducers，处理异步逻辑的 effects，订阅数据源的 subscriptions 。