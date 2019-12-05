---
title: css属性:position
date: 2018-07-25
author: scliuyang
category: css basic
tags: 
- css基础
---

`postion`用于指定一个元素在文档中的定位方式

# 使用语法

支持属性`static | relative | absolute | fixed | sticky`,其中默认值为`static`
注意，position 属性只针对`display`不为`table-column-group | table-column`的元素生效
<!--more-->
## static
默认值,left、top、bottom、right四个定位属性不会生效

## relative
对象遵循常规流，并且参照自身在常规流中的位置通过top，right，bottom，left这4个定位偏移属性进行偏移时不会影响常规流中的任何元素。
{% raw %}
<iframe height='265' scrolling='no' title='position_relative' src='//codepen.io/scliuyang/embed/GBEvwo/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/GBEvwo/'>position_relative</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

## absolute
对象脱离常规流，此时偏移属性参照的是离自身最近的定位祖先元素，如果没有定位的祖先元素(或者说祖先元素都是position:static)，则一直回溯到`window也就是整个窗口`元素。盒子的偏移位置不影响常规流中的任何元素，其margin不与其他任何margin折叠(这里是由于创建了BFC，块级格式化上下文导致的，推荐阅读[深入理解BFC和Margin Collapse](https://www.w3cplus.com/css/understanding-bfc-and-margin-collapse.html))。
他跟relative最大的区别就是脱离文档流，也就是说相邻元素会无视并占据它所在的位置
{% raw %}
<iframe height='265' scrolling='no' title='position_absolute' src='//codepen.io/scliuyang/embed/jpwLjY/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/jpwLjY/'>position_absolute</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

## fixed
与absolute一致，但偏移定位是以窗口为参考。当出现滚动条时，对象不会随着滚动。

## sticky
对象在常态时遵循常规流。它就像是relative和fixed的合体，当在屏幕中时按常规流排版，当卷动到屏幕外时则表现如fixed。该属性的表现是现实中你见到的吸附效果
{% raw %}
<iframe height='265' scrolling='no' title='position_sticky' src='//codepen.io/scliuyang/embed/xJrXZo/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/xJrXZo/'>position_sticky</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}
不过这属性兼容性不咋的
![兼容性](https://p0.meituan.net/dpnewvc/df3fd4d54611b8cbd4af1e389e9e5420337001.png)

# 定位属性

## top/bottom
支持属性`auto | <length> | <percentage>`,默认值为`auto`,仅在position非`static`时生效
- auto：无特殊定位，根据HTML定位规则在文档流中分配
- <length>：用长度值来定义距离顶部的偏移量。可以为负值。
- <percentage>：用百分比来定义距离顶部的偏移量。百分比参照包含块的高度。可以为负值。


在`relative`时,auto计算值为0,如果top和bottom其中一个为auto，则auto相当于另一个的负值，即top = -bottom；如果top和bottom的值都不为auto，则忽略bottom。
在`absolute`时,auto计算为元素的正常文档流位置,如果top和bottom都设值会设置元素的高度，相当于离包含块的顶部和底部多少距离
{% raw %}
<iframe height='265' scrolling='no' title='absolute_top_bttom' src='//codepen.io/scliuyang/embed/pZwdyM/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/pZwdyM/'>absolute_top_bttom</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

## left/right
和`top/bottom`基本一致，只是`percentage`计算参照的是包含块的宽度

*demo水平垂直居中*

{% raw %}
<iframe height='265' scrolling='no' title='水平垂直居中' src='//codepen.io/scliuyang/embed/ZjyaaW/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/ZjyaaW/'>水平垂直居中</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}


## clip(被废弃，clip-path取代)
- rect(<number>|auto <number>|auto <number>|auto <number>|auto)：依据上-右-下-左的顺序提供自对象左上角为(0,0)坐标计算的四个偏移数值，其中任一数值都可用auto替换，即此边不剪切。
必须设置`absolute`或者`fixed`才会生效，没有clip-path好用

{% raw %}
<iframe height='265' scrolling='no' title='clip' src='//codepen.io/scliuyang/embed/JBJOaO/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/JBJOaO/'>clip</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}