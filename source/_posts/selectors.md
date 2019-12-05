---
title: css属性:Selectors选择符
date: 2018-09-05
author: scliuyang
category: css basic
tags:
  - css基础
---

# 元素选择符

## 通配选择符 \*

选定所有的对象,出于性能考虑通常不建议使用因为会命中文档中所有的元素

``` CSS
* {
  rule
}
```

<!--more-->

## 类型选择符

以文档语言对象类型作为选择符

``` CSS
div {
  rule
}
```

## ID 选择符

以唯一标识符 id 属性作为选择符

``` CSS
#id {
  rule
}
```

## 类选择符

以 class 属性为选择符，不通与 ID 属性，class 属性可以定义多个

``` CSS
.cls {
  rule
}
```

# 关系选择符

## 包含选择符(E F)

``` CSS
E F {
  rule
}
```

选择所有被 E 元素包含的 F 元素。包含选择符将会命中所有符合条件的后代，包括儿子，孙子，孙子的孙子...

## 子选择符(E > F)

``` CSS
E > F {
  rule
}
```

选择所有作为 E 元素的子元素 F。与 包含选择符(E F) 不同的是，子选择符只能命中子元素，而不能命中孙辈。

## 相邻选择符(E + F)

选择紧贴在 E 元素之后 F 元素，元素 E 与 F 必须同属一个父级。

{% raw %}

<iframe height='265' scrolling='no' title='相邻选择符' src='//codepen.io/scliuyang/embed/NLgEZv/?height=265&theme-id=0&default-tab= CSS,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/NLgEZv/'>相邻选择符</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

## 兄弟选择符(E ~ F)

选择 E 元素后面的所有兄弟元素 F，元素 E 与 F 必须同属一个父级。

```HTML
<style>
	/* 相邻选择符(E+F) */
	h3 + p { color: #f00; }
	/* 兄弟选择符(E~F) */
	h3 ~ p { color: #f00; }
</style>
<h3>这是一个标题</h3>
<p>p1</p>
<p>p2</p>
<p>p3</p>
```

这个例子中，如果是相邻选择符，那么只有 p1 会变成红色；如果是兄弟选择符，那么 p1/p2/p3 都会变成红色；

# 属性选择符

## E[att]

选择具有 att 属性的 E 元素。

```HTML
<style>
img[alt] {
	margin: 10px;
}
</style>

<img src="图片url" alt="" />
<img src="图片url" />
```

此例，将会命中第一张图片，因为匹配到了 alt 属性

## E[att="val"]

选择具有 att 属性且属性值等于 val 的 E 元素。

```HTML
<style>
input[type="text"] {
	border: 2px solid #000;
}
</style>

<input type="text" />
<input type="submit" />
```

此例，将会命中第一张 input，因为匹配到了 type 属性，并且属性值为 text

## E[att~="val"]

选择具有 att 属性且属性值为一用空格分隔的字词列表，其中一个等于 val 的 E 元素（包含只有一个值且该值等于 val 的情况）。

```HTML
<style>
div[class~="a"] {
	border: 2px solid #000;
}
</style>

<div class="a">1</div>
<div class="b">2</div>
<div class="a b">3</div>
```

此例，将会命中 1, 3 两个 div，因为匹配到了 class 属性，且属性值中有一个值为 a

## E[att^="val"]

选择具有 att 属性且属性值为以 val 开头的字符串的 E 元素。

```HTML
<style>
div[class^="a"] {
	border: 2px solid #000;
}
</style>

<div class="abc">1</div>
<div class="acb">2</div>
<div class="bac">3</div>
```

此例，将会命中 1, 2 两个 div，因为匹配到了 class 属性，且属性值以 a 开头

## E[att$="val"]

选择具有 att 属性且属性值为以 val 结尾的字符串的 E 元素。

```HTML
<style>
div[class$="c"] {
	border: 2px solid #000;
}
</style>

<div class="abc">1</div>
<div class="acb">2</div>
<div class="bac">3</div>
```

此例，将会命中 1, 3 两个 div，因为匹配到了 class 属性，且属性值以 c 结尾

## E[att*="val"]

选择具有 att 属性且属性值为包含 val 的字符串的 E 元素。

```HTML
<style>
div[class*="b"] {
	border: 2px solid #000;
}
</style>

<div class="abc">1</div>
<div class="acb">2</div>
<div class="bac">3</div>
```

此例，将会命中所有 div，因为匹配到了 class 属性，且属性值中都包含了 b

## E[att|="val"]

如果元素 E 拥有 att 属性，并且值为 val，或者值是以 val-开头的，那么 E 将会被选择。

```HTML
<style>
div[class|="a"] {
	border: 2px solid #000;
}
</style>

<div class="a">0</div>
<div class="a-test">1</div>
<div class="b-test">2</div>
<div class="c-test">3</div>
```

在这个例子中，前 2 个 div 将会被命中：

第 1 个 div，拥有 class 属性，并且值为 a，所以被命中；

第 2 个 div，拥有 class 属性，值是 a 开头并紧跟着连接符“-”，所以被命中；

# 伪类选择符

## E:link,visited,hover,active

如果需要给超链接定义：访问前，鼠标悬停，当前被点击，已访问这4种伪类效果，而又没有按照一致的书写顺序，不同的浏览器可能会有不同的表现

```
a:link {}
a:visited {}
a:hover {}
a:active {}
```
可靠的顺序是：l(link)ov(visited)e h(hover)a(active)te, 即用喜欢(love)和讨厌(hate)两个词来概括
{% raw %}
<iframe height='265' scrolling='no' title='love,hate' src='//codepen.io/scliuyang/embed/RYgdQb/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/RYgdQb/'>love,hate</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

## E:focus

设置对象在成为输入焦点（该对象的onfocus事件发生）时的样式。

## E:lang 
语言类选择符

``` HTML 
<style>
p:lang(zh-cmn-Hans) {
	color: #f00;
}
p:lang(en) {
	color: #090;
}
</style>
</head>
<body>
<p lang="zh-cmn-Hans">大段测试文字</p>
<p lang="en">english</p>
```

## E:not
匹配不含有s选择符的元素E,语法E:not(s)，括号内可以填写所有的选择符

有个列表，每个列表项都有一条底边线，但是最后一项不需要底边线
``` CSS
.demo li:not(:last-child) {
	border-bottom: 1px solid #ddd;
}
```

## :root
匹配E元素在文档的根元素,在HTML中，根元素永远是HTML

``` CSS
:root {
  --main-color: hotpink;
  --pane-padding: 5px 42px;
}
```
声明全局css变量

## E:first-child
匹配父元素的第一个子元素E。要使该属性生效，E元素必须是某个元素的子元素，E的父元素最高是body，即E可以是body的子元素

{% raw %}
<iframe height='265' scrolling='no' title='E:first-child' src='//codepen.io/scliuyang/embed/eLRXwL/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/eLRXwL/'>E:first-child</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

## E:last-child
匹配父元素的最后一个子元素E，和first-child类似

## E:only-child
匹配父元素仅有的一个子元素E,和first-child类似。即父元素的子元素有且仅有一个E

## E:nth-child(n)
匹配父元素的第n个子元素E，假设该子元素不是E，则选择符无效。

奇偶匹配
``` HTML
<style>
li:nth-child(2n){color:#f00;} /* 偶数 */
li:nth-child(2n+1){color:#000;} /* 奇数 */

li:nth-child(even){color:#f00;} /* 偶数 */
li:nth-child(odd){color:#000;} /* 奇数 */
</style>

<ul>
	<li>列表项一</li>
	<li>列表项二</li>
	<li>列表项三</li>
	<li>列表项四</li>
</ul>
```

{% raw %}
<iframe height='265' scrolling='no' title='nth-child' src='//codepen.io/scliuyang/embed/jvwRbZ/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/jvwRbZ/'>nth-child</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

## E:nth-last-child(n)
匹配父元素的倒数第n个子元素E，假设该子元素不是E，则选择符无效。

## E:first-of-type
{% raw %}
<iframe height='265' scrolling='no' title='E:first-of-type' src='//codepen.io/scliuyang/embed/bxRJwY/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/bxRJwY/'>E:first-of-type</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

## E:last-of-type
匹配父元素下的所有E子元素中的倒数第一个。

## E:only-of-type
和only-child差不多，不过父元素可以有多个子元素，但其中的子元素E必须是唯一的，不能出现多个。

## E:nth-of-type(n)
匹配父元素的第n个子元素E。
匹配的是父元素的第n个为E的子元素（被命中的不一定是第n个子元素，因为匹配的不是第n个子元素，而是第n个为E的子元素）

## E:nth-last-of-type(n)
匹配父元素的倒数第n个子元素E。

## E:empty
匹配没有任何子元素（包括text节点）的元素E。
{% raw %}
<iframe height='265' scrolling='no' title='E:empty' src='//codepen.io/scliuyang/embed/xareeV/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/xareeV/'>E:empty</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

## E:checked
匹配用户界面上处于选中状态的元素E。(用于input type为radio与checkbox时)

## E:enabled
匹配用户界面上处于可用状态的元素E。
{% raw %}
<iframe height='265' scrolling='no' title='E:enabled' src='//codepen.io/scliuyang/embed/EeXJBV/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/EeXJBV/'>E:enabled</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

## E:disabled
匹配用户界面上处于禁用状态的元素E。

## E:target
URL后面跟锚点#，指向文档内某个具体的元素。这个被链接的元素就是目标元素(target element)，:target选择器用于选取当前活动的目标元素。
{% raw %}
<iframe height='265' scrolling='no' title='E:target' src='//codepen.io/scliuyang/embed/yxXrmd/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/yxXrmd/'>E:target</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

# 伪对象选择符

## E::first-letter

设置对象内的第一个字符的样式。
此伪对象仅作用于块对象。内联对象要使用该伪对象，必须先将其设置为块级对象。
{% raw %}
<iframe height='265' scrolling='no' title='E::first-letter' src='//codepen.io/scliuyang/embed/gdRJaz/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/gdRJaz/'>E::first-letter</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

## E:first-line
设置对象内的第一行的样式。

## E::before，E::after
设置在对象前（依据对象树的逻辑结构）发生的内容。用来和content属性一起使用，并且必须定义content属性
这个属性常用来实现一些ui特效或者动画效果，可以减少dom元素的数量。

## E::placeholder
设置对象文字占位符的样式。注意加上浏览器前缀

## E::selection
设置对象被选择时的样式。
- 需要注意的是，::selection只能定义被选择时的background-color，color及text-shadow
{% raw %}
<iframe height='265' scrolling='no' title='E::selection' src='//codepen.io/scliuyang/embed/dqREOV/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/scliuyang/pen/dqREOV/'>E::selection</a> by scliuyang (<a href='https://codepen.io/scliuyang'>@scliuyang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}



# 选择器优先级

|编号   |   权重   |  选择器或样式   |
|------ |---------|---------------|
|1      |1000     |  内联样式      |
|2      |100      |  ID选择器：#id{...}|     |
|3      |10       |  类选择器，伪类选择器，属性选择器：.class{...}、:hover{...}、[arrtibute=value]       |
|4      |1        |  标签选择器，伪元素选择器：div{...}、::after{...}    |
|5      |0        |  其他选择器：通配选择器(*)，子选择器(>)，相邻同胞选择器(+)    |
|6      |无穷大    |  important    |

{% raw %}
<iframe height='265' scrolling='no' title='selectorPriority' src='//codepen.io/liuzhaozhao/embed/MqGLvp/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/liuzhaozhao/pen/MqGLvp/'>selectorPriority</a> by liuzhaozhao828 (<a href='https://codepen.io/liuzhaozhao'>@liuzhaozhao</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}