---
title: css属性:列表list
date: 2018-07-25
author: scliuyang
category: css basic
tags: 
- css基础
---

# 列表 list

给 li 或者 display:list-item 的元素设置样式
<!--more-->
## list-style

复合属性`list-style：<' list-style-type '> || <' list-style-position '> || <' list-style-image '>`

## list-style-type
设置列表样式,取值
- disc：实心圆(CSS1)
- circle：空心圆(CSS1)
- square：实心方块(CSS1)
- decimal：阿拉伯数字(CSS1)
- lower-roman：小写罗马数字(CSS1)
- upper-roman：大写罗马数字(CSS1)
- lower-alpha：小写英文字母(CSS1)
- upper-alpha：大写英文字母(CSS1)
- none：不使用项目符号(CSS1)
- armenian：传统的亚美尼亚数字(CSS2)
- cjk-ideographic：浅白的表意数字(CSS2)
- georgian：传统的乔治数字(CSS2)
- lower-greek：基本的希腊小写字母(CSS2)
- hebrew：传统的希伯莱数字(CSS2)
- hiragana：日文平假名字符(CSS2)
- hiragana-iroha：日文平假名序号(CSS2)
- katakana：日文片假名字符(CSS2)
- katakana-iroha：日文片假名序号(CSS2)
- lower-latin：小写拉丁字母(CSS2)
- upper-latin：大写拉丁字母(CSS2)

仅当`list-style-image`属性为`none`或指定图像不可用时才生效

{% raw %}
<iframe height='500' scrolling='no' title='list-type' src='//codepen.io/scliuyang/embed/xJrpXa/?height=265&theme-id=0&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/xJrpXa/'>list-type</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

## list-style-image
设置样式为图片，取值
- none:不指定图像，默认内容标记将被 <' list-style-type '> 代替。
- url:使用绝对或相对地址指定列表项标记图像。如果图像地址无效，默认内容标记将被 <' list-style-type '> 代替。
- 
{% raw %}
<iframe height='265' scrolling='no' title='list-img' src='//codepen.io/scliuyang/embed/djRJdL/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/djRJdL/'>list-img</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

## list-style-position
设置或检索作为对象的列表项标记如何根据文本排列。取值
- outside: 列表项目标记放置在文本以外，且环绕文本不根据标记对齐
- inside: 列表项目标记放置在文本以内，且环绕文本根据标记对齐

{% raw %}
<iframe height='265' scrolling='no' title='list-position' src='//codepen.io/scliuyang/embed/BPZJPz/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/BPZJPz/'>list-position</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}