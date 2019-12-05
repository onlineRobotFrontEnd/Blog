---
title: css属性:表格table
date: 2018-08-01
author: liuzhaozhao
category: css basic
tags: 
- css基础
---

<!--more-->

## table-layout:

* fixed  : 固定布局
* auto： 自动算法

   {% raw %}
  <iframe height='265' scrolling='no' title='table-layout' src='//codepen.io/liuzhaozhao/embed/zLWvQe/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/liuzhaozhao/pen/zLWvQe/'>table-layout</a> by liuzhaozhao828 (<a href='https://codepen.io/liuzhaozhao'>@liuzhaozhao</a>) on <a href='https://codepen.io'>CodePen</a>.
  </iframe>
  {% endraw %}



## border-collapse:

* collapse:  相邻边框合并
* separate:  边框独立

   {% raw %}
  <iframe height='265' scrolling='no' title='border-collapse' src='//codepen.io/liuzhaozhao/embed/NBYxdY/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/liuzhaozhao/pen/NBYxdY/'>border-collapse</a> by liuzhaozhao828 (<a href='https://codepen.io/liuzhaozhao'>@liuzhaozhao</a>) on <a href='https://codepen.io'>CodePen</a>.
  </iframe>
  {% endraw %}



## border-spacing:

* 只在<font color=#ff0000>boder-collapse为 separate</font>的情况下有效果
* 复合属性，横向相邻和纵向相邻分开设置：border-spacing：10px 20px
* IE6/7无效，兼容方式`<table border="1" cellspacing="20">`

   {% raw %}
  <iframe height='265' scrolling='no' title='border-spacing' src='//codepen.io/liuzhaozhao/embed/WKzrMg/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/liuzhaozhao/pen/WKzrMg/'>border-spacing</a> by liuzhaozhao828 (<a href='https://codepen.io/liuzhaozhao'>@liuzhaozhao</a>) on <a href='https://codepen.io'>CodePen</a>.
  </iframe>
  {% endraw %}



## caption-side:

* caption的位置
* 取值 top bottom
* left right   <font color=#ff0000>(只有Firefox支持)</font>

   {% raw %}
  <iframe height='265' scrolling='no' title='caption-side' src='//codepen.io/liuzhaozhao/embed/OwvMov/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/liuzhaozhao/pen/OwvMov/'>caption-side</a> by liuzhaozhao828 (<a href='https://codepen.io/liuzhaozhao'>@liuzhaozhao</a>) on <a href='https://codepen.io'>CodePen</a>.
  </iframe>
  {% endraw %}



## empty-cells:

* 取值  hide show
* 单元格没值时，隐藏边框
* <font color=#ff0000>只在boder-collapse为 separate的情况下有效果</font><br>

   {% raw %}
  <iframe height='265' scrolling='no' title='empty-cells' src='//codepen.io/liuzhaozhao/embed/LBdNRj/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/liuzhaozhao/pen/LBdNRj/'>empty-cells</a> by liuzhaozhao828 (<a href='https://codepen.io/liuzhaozhao'>@liuzhaozhao</a>) on <a href='https://codepen.io'>CodePen</a>.
  </iframe>
  {% endraw %}






