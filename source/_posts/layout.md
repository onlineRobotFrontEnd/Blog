---
title: css属性:布局layout
date: 2018-07-31
author: liuzhaozhao
category: css basic
tags: 
- css基础
---

## display

<!--more-->

- none：
   1.不展示
   2.不占物理空间（区别visibility：hidden)

- inline：
   1.内联元素
   2.Line-height:可以设置内联元素的高度
   3.Margin:  内联非替换元素margin-top, margin-bottom无效

   {% raw %}
  <iframe height='265' scrolling='no' title='display-1' src='//codepen.io/liuzhaozhao/embed/EpExdG/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/liuzhaozhao/pen/EpExdG/'>display-1</a> by liuzhaozhao828 (<a href='https://codepen.io/liuzhaozhao'>@liuzhaozhao</a>) on <a href='https://codepen.io'>CodePen</a>.
  </iframe>
   {% endraw %}

   4.Padding: 父元素未指宽高，内联非替换不会撑高父元素，内联替换会撑高父元素

   {% raw %}
   <iframe height='265' scrolling='no' title='display-2' src='//codepen.io/liuzhaozhao/embed/bjvNGo/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/liuzhaozhao/pen/bjvNGo/'>display-2</a> by liuzhaozhao828 (<a href='https://codepen.io/liuzhaozhao'>@liuzhaozhao</a>) on <a href='https://codepen.io'>CodePen</a>.
   </iframe>
   {% endraw %}

- block：
   1.块元素
   2.独占一行

- inline-block：
   1.内联块元素
   2.内联块之间有缝隙 回车字符占用了4px，解决方法：父元素设置 font-size: 0

- table系属性值
   1.table：块元素级的表格，相当于标签`<table>`
   2.inline-table：内联元素级的表格，相当于标签`<table>`
   3.table-caption：表格标题，相当于标签`<caption>`
   4.table-cell：表格单元格，相当于标签`<td>`
   5.table-row：指定对象作为表格行，相当于标签`<tr>`
   6.table-row-group：表格行组，相当于标签`<tbody>`
   7.table-column：表格列，相当于标签`<col>`
   8.table-column-group：表格列组显示，相当于标签`<colgroup>`
   9.table-header-group：表格标题组，相当于标签`<thead>`
   10.table-footer-group：表格脚注组，相当于标签`<tfoot>`

- 其他：
   1.list-item：列表项目
   2.run-in:根据上下文决定是内联还是块, ***chrome不支持***



## visibility

- 取值： visible  hidden
- hidden隐藏元素，但是保留物理空间


## clear

- 取值： both left right


## float

- 取值： none，left， right
- 特性：
   1.脱离文档流
   2.变为块元素
- 清除浮动的三种办法：
   1.增加div元素，该元素通过clear属性清除浮动
   2.增加伪元素:after，通过clear属性清除浮动
   3.父元素增加属性overflow:hidden，生成BFC清除浮动

   {% raw %}
  <iframe height='265' scrolling='no' title='float-clear' src='//codepen.io/liuzhaozhao/embed/BProQj/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/liuzhaozhao/pen/BProQj/'>float-clear</a> by liuzhaozhao828 (<a href='https://codepen.io/liuzhaozhao'>@liuzhaozhao</a>) on <a href='https://codepen.io'>CodePen</a>.
  </iframe>
  {% endraw %}


## overflow

- 取值：visible, hidden，scroll, auto
- overflow等同于 overflow-x  overflow-y
- 值为***非visibile***时，将会为它的内容创建一个新的块格式化上下文（BFC）



