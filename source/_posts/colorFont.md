---
title: css属性:颜色(color)与字体(font)
date: 2018-08-21
author: vivizhou0596
category: css basic
tags: 
- css基础
---

# 颜色 color

检索或设置对象的文本颜色。无默认值
默认值：由user agent决定

适用于：所有元素

继承性：有

动画性：是

计算值：指定值

取值:  color：指定颜色
<!--more-->
## 说明

1.可以使用Color Name(颜色名称), HEX, RGB, RGBA, HSL, HSLA, transparent来指定color。

- Color Name(颜色名称)：red,blue;
- HEX（十六进制）：#RRGGBB；#ff0000,#ffffff;
- RGB: RGB(R,G,B); rgb(255,0,0);
- RGBA:此色彩模式与RGB相同，只是在RGB模式上新增了Alpha透明度rgb(255,0,0,0.5)；
- HSL、HSLA:色调（0-360），饱和度（0%-100%），亮度（0-100%）；
- transparent：transparent是全透明黑色(black)的速记法，即一个类似rgba(0,0,0,0)这样的值。
{% raw %}
<iframe height='265' scrolling='no' title='MqYgEv' src='//codepen.io/vivizhou0596/embed/MqYgEv/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/vivizhou0596/pen/MqYgEv/'>MqYgEv</a> by vivizhou0596 (<a href='https://codepen.io/vivizhou0596'>@vivizhou0596</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

2.注意，用颜色名称指定color可能不被一些浏览器接受。

3.color属性值被间接用来提供一个中间值currentColor以供其他接受颜色值的属性使用。

{% raw %}
<iframe height='265' scrolling='no' title='yxyBZp' src='//codepen.io/vivizhou0596/embed/yxyBZp/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/vivizhou0596/pen/yxyBZp/'>yxyBZp</a> by vivizhou0596 (<a href='https://codepen.io/vivizhou0596'>@vivizhou0596</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

# 字体 font

## font
font 简写属性在一个声明中设置所有字体属性。

复合属性：`[ [font-style||font-variant||font-weight||font-stretch]?font-size[ /line-height]?font-family] | caption | icon | menu | message-box | small-caption | status-bar`

取值：
- font-style：指定文本字体样式
- font-variant：指定文本是否为小型的大写字母
- font-weight：指定文本字体的粗细
- font-stretch：指定文本字体拉伸变形
- font-size：指定文本字体尺寸
- line-height：指定文本字体的行高
- font-family：指定文本使用某个字体或字体序列
- caption：使用有标题的系统控件的文本字体（如按钮，菜单等）（CSS2）
- icon：使用图标标签的字体（CSS2）
- menu：使用菜单的字体（CSS2）
- message-box：使用信息对话框的文本字体（CSS2）
- small-caption：使用小控件的字体（CSS2）
- status-bar：使用窗口状态栏的字体（CSS2）

注：使用font属性参数必须按照如上的排列顺序，且font-size和font-family是不可忽略的。每个参数仅允许有一个值。忽略的将使用其参数对应的独立属性的默认值。
{% raw %}
<iframe height='265' scrolling='no' title='GXgRym' src='//codepen.io/vivizhou0596/embed/GXgRym/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/vivizhou0596/pen/GXgRym/'>GXgRym</a> by vivizhou0596 (<a href='https://codepen.io/vivizhou0596'>@vivizhou0596</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

## font-style
 定义字体的风格
 - normal：指定文本字体样式为正常的字体
 - italic：指定文本字体样式为斜体。对于没有设计斜体的特殊字体，如果要使用斜体外观将应用oblique
 - oblique：指定文本字体样式为倾斜的字体。人为的使文字倾斜，而不是去选取字体中的斜体字

## font-variant
把段落设置为小型大写字母字体
- normal：正常的字体
- small-caps：小型的大写字母字体

## font-weight
设置文本的粗细
- normal：正常的字体。相当于数字值400
- bold：粗体。相当于数字值700。
- bolder：定义比继承值更重的值
- lighter：定义比继承值更轻的值
- <integer>：用数字表示文本字体粗细。取值范围：100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900

## font-size
可设置字体的尺寸
- absolute-size：根据对象字号进行调节。以 medium 作为基础参照，xx-small相当于medium 3/5 (h6)，x-small: 3/4，small: 8/9 (h5)，medium: 1 (h4)，large: 6/5 (h3)，x-large: 3/2 (h2)，xx-large: 2/1 (h1)，
- relative-size：相对于父对像中字号进行相对调节。使用成比例的em单位计算。
- length：用长度值指定文字大小。不允许负值。
- percentage：用百分比指定文字大小。其百分比取值是基于父对象中字体的尺寸。不允许负值。

## font-family
规定元素的字体系列
- family-name：字体名称。按优先顺序排列。以逗号隔开。如果字体名称包含空格或中文，则应使用引号括起
- generic-family：字体序列名称。
font-family 可以把多个字体名称作为一个“回退”系统来保存。如果浏览器不支持第一个字体，则会尝试下一个。也就是说，font-family 属性的值是用于某个元素的字体族名称或/及类族名称的一个优先表。浏览器会使用它可识别的第一个值。

有两种类型的字体系列名称：

   - 字体名称：具体字体的名称，比如："times"、"courier"、"arial","宋体"。
   - 通常字体系列名称：比如："serif"（笔画两端有脚）、"sans-serif"（笔画两端没有脚）、"cursive"、"fantasy"、"monospace"（所有字符宽度都一样）

**提示：**
   1.使用逗号分割每个值，并始终提供一个类族名称作为最后的选择。
   2.所有的表单元素都是无法继承body的字体属性的，所以平常的只在body后加入字体是不行的，需要为用的表单元素单独设计字体

# 多列
通过 CSS3，您能够创建多个列来对文本进行布局 - 就像报纸那样！

常用属性：

1.column-count 属性规定元素应该被分隔的列数；
2.column-gap 属性规定列之间的间隔；
3.column-rule 属性设置列之间的宽度、样式和颜色规则。
{% raw %}
<iframe height='265' scrolling='no' title='GXggeP' src='//codepen.io/vivizhou0596/embed/GXggeP/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/vivizhou0596/pen/GXggeP/'>GXggeP</a> by vivizhou0596 (<a href='https://codepen.io/vivizhou0596'>@vivizhou0596</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}