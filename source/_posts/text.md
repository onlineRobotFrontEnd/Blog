---
title: css属性:文本(Text)
date: 2018-08-16
author: leonliu
category: css basic
tags: 
- css基础
---
参考链接：
- [css.doyoe.com](https://css.doyoe.com/)
- [css2.1中文版](http://www.ayqy.net/doc/css2-1/cover.html)
- [MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS)


## 一.text-transform
**text-transform** 属性指定如何将元素的文本进行大小写变形。它可以用于使文本显示为全大写或全小写，也可单独对每一个单词进行操作。

<!--more-->
---


```
初始值              none
适用元素            all elements. It also applies to ::first-letter and ::first-line.
是否是继承属性      yes
适用媒体            visual
计算值              as specified
Animation type      discrete
正规顺序            the unique non-ambiguous order defined by the formal grammar
```
#### 语法

```
/* Keyword values */
text-transform: capitalize;
text-transform: uppercase;
text-transform: lowercase;
text-transform: none;
text-transform: full-width;

/* Global values */
text-transform: inherit;
text-transform: initial;
text-transform: unset;
```
- **capitalize:**   将文本中的每个单词以大写字母开头(只会对每个单词第一个字母做变形，对其他字母保持不变)
- **uppercase:**    将文本中的所有字符变为大写
- **lowercase：**   将文本中的所有字符变为小写
- **none：**    默认值，不对文本进行大小写转换
- **full-width：**  将所有字符转换成fullwidth形式。如果字符没有相应的fullwidth形式，将保留原样。这个值通常用于排版拉丁字符和数字等表意符号。(全角)

[text-transform代码演示](https://codepen.io/lord2416/pen/VBMmEv)


## 二、white-space
**white-space** 属性是用来设置如何处理元素中的空白。

```
初始值              normal
适用元素            all elements
是否是继承属性      yes
适用媒体            visual
计算值              as specified
Animation type      discrete
正规顺序            the unique non-ambiguous order defined by the formal grammar
```

语法

```
white-space: normal
white-space: nowrap
white-space: pre
white-space: pre-wrap
white-space: pre-line

white-space: inherit
```
- **normal**    默认值,连续的空白符会被合并，换行符会被当作空白符来处理。填充line盒子时，必要的话会换行。
- **nowrap**    和 normal 一样，连续的空白符会被合并。但文本内的换行无效。
- **pre**   连续的空白符会被保留。在遇到换行符或者<br>元素时才会换行。
- **pre-wrap**  连续的空白符会被保留。在遇到换行符或者<br>元素，或者需要为了填充line盒子时才会换行。
- **pre-line**  连续的空白符会被合并。在遇到换行符或者<br>元素，或者需要为了填充line盒子时会换行。


---| 换行符	| 空格和制表符 |文字转行
---|---|---|---
normal | 合并 | 合并 | 转行
nowrap | 合并 | 合并 | 不转行
pre | 保留 | 保留 | 不转行
pre-wrap | 保留 | 保留 | 转行
pre-line | 保留 | 合并 | 转行

[white-space代码示例](https://codepen.io/lord2416/pen/NBavjK)


## 三、tab-size
**tab-size** 定义元素内容中制表符的长度。(a tab (U+0009) character),只有当white-space的属性值为：pre | pre-wrap时，该属性的定义才有效


```
初始值	        8
适用元素	    block containers
是否是继承属性	yes
适用媒体	    visual
计算值	        the specified integer or an absolute length
Animation type	a length
正规顺序	    the unique non-ambiguous order defined by the formal grammar
```


```
/* <integer> values */
tab-size: 4;
tab-size: 0;

/* <length> values */
tab-size: 10px;
tab-size: 2em;

/* Global values */
tab-size: inherit;
tab-size: initial;
tab-size: unset;
```

[tab-size代码示例](https://codepen.io/lord2416/pen/rrGKKq)

## 四、word-break
**word-break**定义元素内容文本的字间与字符间的换行行为

```
初始值              normal
适用元素            all elements
是否是继承属性      yes
适用媒体            visual
计算值	            as specified
Animation type	    discrete
正规顺序            the unique non-ambiguous order defined by the formal grammar
```


```
word-break: normal 
word-break: break-all 
word-break: keep-all

/* Global values */
word-break: inherit;
word-break: initial;
word-break: unset;
```
- **normal**
使用默认的断行规则。
- **break-all**
对于non-CJK (CJK 指中文/日文/韩文) 文本，可在任意字符间断行。
- **keep-all**
CJK 文本不断行。 Non-CJK 文本表现同 normal。
- **break-word**
与break-all相同，不同的地方在于它要求一个没有断行破发点的词必须保持为一个整体单位。这与word-wrap的break-word值效果相同

[word-break代码示例](https://codepen.io/lord2416/pen/gjGjKv)

## 五、word-wrap/overflow-wrap

> 注：word-wrap 属性原本属于微软的一个私有属性，在 CSS3 现在的文本规范草案中已经被重名为 overflow-wrap 。 word-wrap 现在被当作 overflow-wrap 的 “别名”。 稳定的谷歌 Chrome 和 Opera 浏览器版本支持这种新语法。


```
初始值              normal
适用元素            all elements
是否是继承属性      yes
适用媒体            visual
计算值              as specified
Animation type      discrete
正规顺序            the unique non-ambiguous order defined by the formal grammar
```


```
/* Keyword values */
overflow-wrap: normal;
overflow-wrap: break-word;

/* Global values */
overflow-wrap: inherit;
overflow-wrap: initial;
overflow-wrap: unset;
```

- **normal**
表示在正常的单词结束处换行。
- **break-word**
表示如果行内没有多余的地方容纳该单词到结尾，则那些正常的不能被被分割的单词会被强制分割换行。

[word-wrap/overflow-wrap代码示例](https://codepen.io/lord2416/pen/WKZgvB)

## 六、text-align
**text-align** CSS属性定义行内内容（例如文字）如何相对它的块父元素对齐。text-align 并不控制块元素自己的对齐，只控制它的行内内容的对齐。


```
初始值              start, or a nameless value that acts as left if direction is ltr, right if direction is rtl if start is not supported by the browser.
适用元素            block containers
是否是继承属性	    yes
适用媒体            visual
计算值	            as specified, except for the match-parent value which is calculated against its parent's direction value and results in a computed value of either left or right
Animation type	    discrete
正规顺序	        order of appearance in the formal grammar of the values
```


### 语法

```
/* Keyword values */
text-align: left;
text-align: right;
text-align: center;
text-align: justify;
text-align: justify-all;
text-align: start;
text-align: end;
text-align: match-parent;

/* Character-based alignment in a table column */
text-align: ".";
text-align: "." center;

/* Block alignment values (Non-standard syntax) */
text-align: -moz-center;
text-align: -webkit-center;

/* Global values */
text-align: inherit;
text-align: initial;
text-align: unset;
```

- **start** 
如果内容方向是左至右，则等于left，反之则为right。
- **end**
如果内容方向是左至右，则等于right，反之则为left。
- **left**
行内内容向左侧边对齐。
- **right**
行内内容向右侧边对齐。
- **center**
行内内容居中。
- <**string**>
第一个出现的该（单字符）字符串被用来对齐。跟随的关键字定义对齐的方向。例如，可用于让数字值根据小数点对齐。
- **justify**
文字向两侧对齐，对最后一行无效。
- **justify-all**
和justify一致，但是强制使最后一行两端对齐。
- **match-parent** 
和inherit类似，区别在于start和end的值根据父元素的direction确定，并被替换为恰当的left或right。

[text-align示例](https://codepen.io/lord2416/pen/ZjXMxL?editors=1111)

## 七、text-align-last
**text-align-last** 描述的是一段文本中最后一行在被强制换行之前的对齐规则。

**注意**：
IE浏览器下，如果text-align-last要生效，必须先定义text-align为justify；


```
初始值              auto
适用元素            block containers
是否是继承属性      yes
适用媒体            visual
计算值              as specified
Animation type      discrete
正规顺序            the unique non-ambiguous order defined by the formal grammar
```

```
/* Keyword values */
text-align-last: auto;
text-align-last: start;
text-align-last: end;
text-align-last: left;
text-align-last: right;
text-align-last: center;
text-align-last: justify;

/* Global values */
text-align-last: inherit;
text-align-last: initial;
text-align-last: unset;
```


- **auto**
每一行的对齐规则由 text-align 的值来确定，当 text-align 的值是 justify，text-align-last 的表现和设置了 start 的表现是一样的，即如果文本的展示方向是从左到右，则最后一行左侧对齐与内容盒子。
经测试，当 text-align 的值为 right，并且 text-align-last 设置为 auto 时，文本最后一行的对齐方式相当于 text-align-last 被设置为 right 时的效果。即 text-align-last 设置为 auto 后的表现跟 text-align 的设置有关。
- **start**
与 direction 的设置有关。
如果文本展示方向是从左到右，起点在左侧，则是左对齐；
如果文本展示方向是从右到左，起点在右侧，则是右对齐。
如果没有设置 direction ，则按照浏览器文本的默认显示方向来确定。
- **end**
与 direction 的设置有关。
如果文本展示方向是从左到右，末尾在右侧，则是右对齐；
如果文本展示方向是从右到左，末尾在左侧，则是左对齐。
如果没有设置 direction ，则按照浏览器文本的默认显示方向来确定。
- **left**
最后一行文字与内容盒子的左侧对齐
- **right**
最后一行文字与内容盒子的右侧对齐
- **center**
最后一行文字与内容盒子居中对齐
- **justify**
最后一行文字的开头语内容盒子的左侧对齐，末尾与右侧对齐。

[text-align-last示例](https://codepen.io/lord2416/pen/ejGPoQ?editors=1111)

## 八、text-justify

**text-justify**定义的是当文本的 text-align 属性被设置为 :justify 时的齐行方法。


```
初始值          auto
适用元素        inline-level and table-cell elements
是否是继承属性  yes
适用媒体        visual
计算值          as specified
Animation type	discrete
正规顺序        the unique non-ambiguous order defined by the formal grammar
```


- **auto：**
允许浏览器用户代理确定使用的两端对齐法则。
- **none：**
禁止两端对齐。
- **inter-word：**
通过增加字之间的空格对齐文本。该行为是对齐所有文本行最快的方法，它的两端对齐行为对段落的最后一行无效。
- **inter-ideograph：**
为表意字文本提供完全两端对齐，增加或减少表意字和词间的空格。
- **inter-cluster**：
调整文本无词间空格的行。这种模式的调整是用于优化亚洲语言文档的
- **distribute：**
通过增加或减少字或字母之间的空格对齐文本，适用于东亚文档，尤其是泰国。
- **kashida：**
通过拉长选定点的字符调整文本。这种调整模式是特别为阿拉伯脚本语言提供的。需要IE5.5+支持
- **inter-character**
通过在文本中的字符之间添加空间来实现行对齐（这将会改变 letter-spacing 的值），比如日语就是最适合使用这个属性的语言。

[text-justify示例](https://codepen.io/lord2416/pen/ZjXmeZ?editors=1111)

## 九、word-spacing

**word-spacing**属性用于声明标签和单词直接的间距行为。


```
初始值              normal
适用元素            all elements. It also applies to ::first-letter and ::first-line.
是否是继承属性      yes
Percentages         refer to the width of the affected glyph
适用媒体            visual
计算值              an optimum, minimum, and maximum value, each consisting of either an absolute length, a percentage, or the keyword normal
Animation type      a length
正规顺序            the unique non-ambiguous order defined by the formal grammar
```


```
/* Keyword value */
word-spacing: normal;

/* <length> values */
word-spacing: 3px;
word-spacing: 0.3em;

/* <percentage> values */
word-spacing: 50%;
word-spacing: 200%;

/* Global values */
word-spacing: inherit;
word-spacing: initial;
word-spacing: unset;
```

- **normal**初始值，正常的单词间距，由当前字体和/或浏览器定义。
- <**length**>通过指定具体的额外间距来增加字体的单词间距。
- <**percentage**>通过指定受影响字符的宽度的百分比的方式来增加的间距。

[word-spacing示例](https://codepen.io/lord2416/pen/zLprmN)

## 十、letter-spacing

**letter-spacing**属性明确了文字字母的间距行为。


```
初始值              normal
适用元素            all elements. It also applies to ::first-letter and ::first-line.
是否是继承属性      yes
适用媒体            visual
计算值              an optimum value consisting of either an absolute length or the keyword normal
Animation type      a length
正规顺序            the unique non-ambiguous order defined by the formal grammar
```


```
letter-spacing: normal;

letter-spacing: 0.3em;
letter-spacing: 3px;
letter-spacing: .3px;

letter-spacing: inherit;
```

- **normal**(默认值) 此间距是按照当前字体的正常间距确定的。 用户代理根据此属性来确定文字的默认对齐方式。等同于间距 0。
- <**length**>指定文字间的间距以替代默认间距。可以是负值，但有可能会出现 implementation 限制。用户代理不会在此基础上进一步增加或缩减间距来对齐文字。

[letter-spacing示例](https://codepen.io/lord2416/pen/XBVwYz) 

**合理使用**：
一个很大的正或负的letter-spacing值会将应用这个样式的单词边为不可读的。给文本letter-spacing属性应用了一个很大的正值，字母之间的距离会很远，以至于文本中的单词将显示为一系列单独的，无有任何关联的字母。给文本letter-spacing属性应用了一个很大的负值，字母将会互相重叠到一个点，在这个点上单词可能无法识别了。

一个最佳的易辨认的字母间距（letter-spacing）必须根据具体情况来确定，因为不同的字体系列具有不同的字符宽度。没有任何一个值可以确保所有字体系列自动保持它们的可读性。


## 十一、text-indent
**text-indent** 属性 规定了 一个元素 首行 文本内容之前应该有多少水平空格。水平空格是块级包含元素的内容盒子的左边(对于从右向左布局来说是右边).


```
初始值                  0
适用元素                block containers
是否是继承属性          yes
Percentages             refer to the width of the containing block
适用媒体                visual
计算值                  the percentage as specified or the absolute length, plus any keywords as specified
Animation type          a length, percentage or calc();
正规顺序                The length or percentage before the keywords, if both are present. If several keywords are present, they appear in the same order as their appearance in the formal grammar.
```


```
/* <length> values */
text-indent: 3mm;
text-indent: 40px;

/* <percentage> value
   relative to the containing block width */
text-indent: 15%;

/* Keyword values */
text-indent: 5em each-line;
text-indent: 5em hanging;
text-indent: 5em hanging each-line;

/* Global values */
text-indent: inherit;
text-indent: initial;
text-indent: unset;
```

- <**length**>使用固定的<length>值来指定文本的缩进。允许使用负值。
- <**percentage**>使用包含块宽度的百分比作为缩进。
- **each-line**（css3）文本缩进会影响第一行，以及使用<br>强制断行后的第一行。
- **hanging**（css3）该值会对所有的行进行反转缩进：除了第一行之外的所有的行都会被缩进，看起来就像第一行设置了一个负的缩进值。

**注：**
**each-line**和**hanging**均为实验性功能
- chrome开启: chrome://flags/#enable-experimental-web-platform-features

[text-indent代码示例](https://codepen.io/lord2416/pen/LBeKPq)

## 十二、vertical-align

**vertical-align**属性用来指定行内元素（inline）或表格单元格（table-cell）元素的垂直对齐方式。


```
初始值              baseline
适用元素            inline-level and table-cell elements. It also applies to ::first-letter and ::first-line.
是否是继承属性      否
Percentages         refer to the line-height of the element itself
适用媒体            visual
计算值              for percentage and length values, the absolute length, otherwise the keyword as specified
Animation type      a length
正规顺序            the unique non-ambiguous order defined by the formal grammar
```


```
/* keyword values */
vertical-align: baseline;
vertical-align: sub;
vertical-align: super;
vertical-align: text-top;
vertical-align: text-bottom;
vertical-align: middle;
vertical-align: top;
vertical-align: bottom;

/* <length> values */
vertical-align: 10em;
vertical-align: 4px;

/* <percentage> values */
vertical-align: 20%;

/* Global values */
vertical-align: inherit;
vertical-align: initial;
vertical-align: unset;
```

#### 取值 (对于行内(inline)元素)
下列值只对父级行内元素或者一个父级块容器元素的[strut](http://www.ayqy.net/doc/css2-1/visudet.html#strut)有效

在下面的定义中，对于行内非替换元素，用于对齐的盒是那个高度为'line-height'（包括该盒的字形和两边的半行距，见上文）的盒。对于其它所有元素，用于对齐的盒都是外边距框（margin box）
- **baseline**默认。把盒的基线与父级盒的基线对齐。如果该盒没有基线，就把下外边距边界和父级的基线对齐。
- **sub**把该盒的基线降低到合适的位置作为父级盒的下标（该值不影响该元素文本的字体大小）
- **super**把该盒的基线提升到合适的位置作为父级盒的上标（该值不影响该元素文本的字体大小）
- **text-top**把该盒的顶端和父级的内容区（content area）的顶端对齐
- **text-bottom**把该盒的底端和父级的内容区的底端对齐
- **middle**把该盒的垂直中点与父级盒的基线加上父级的半x-height对齐
- <**length**>把该盒提升（正值）或者降低（负值）这个距离。值'0cm'表示与“基线”相同
- <**percentage**>把该盒提升（正值）或者降低（负值）这个距离（'line-height'值的百分比）。值'0%'表示与“基线”相同


以下两个值是相对于整行来说的：
- **top**元素及其后代的顶端与line-box正行的顶端对齐。
- **bottom**元素及其后代的底端与line-box整行的底端对齐。

如果元素没有基线baseline，则以它的外边距的下边缘为基线。

#### 取值 (对于table-cell元素)
- **baseline** (and **sub**, **super**, **text-top**, **text-bottom**, <**length**>, and <**percentage**>)与同行单元格的基线对齐。
- **top**单元格的内边距的上边缘与行的顶端对齐。
- **middle**单元格垂直居中。
- **bottom**单元格的内边距的下边缘与行的底端对齐。

可以取负值。

[vertical-align代码示例](https://codepen.io/lord2416/pen/oMEjdN)

## 十四、line-height

**line-height** 属性用于设置多行元素的空间量，比如文本。对于块级元素，它指定元素行盒（line boxes）的最小高度。对于非替代的inline元素，它用于计算行盒（line box）的高度。


```
Value:  	    normal | <number> | <length> | <percentage> | inherit
初始值:  	    normal
适用元素:  	    所有元素
是否可继承:  	yes
Percentages:  	参考元素自身的字体大小
Media:  	    visual
Computed value: 对于<length>和<percentage>是绝对的值，否则与指定值相同
```

```
/* Keyword value */
line-height: normal;

/* Unitless values: use this number multiplied
by the element's font size */
line-height: 3.5;

/* <length> values */
line-height: 3em;

/* <percentage> values */
line-height: 34%;

/* Global values */
line-height: inherit;
line-height: initial;
line-height: unset;
```

- **normal**
告诉用户代理根据该元素的字体把应用值设置为一个“合理的”值。该值与<number>的含义相同。我们推荐介于1.0到1.2的“常规”应用值。计算值为'normal'
- <**length**>
指定的长度用来计算行框的高度。负值是非法的
- <**number**>
该属性的应用值为这个数字乘以该元素的字体大小。负值是非法的。计算值与指定值相同
- <**percentage**>
该属性的计算值为这个百分比乘以该元素的字体大小的计算值。负值是非法的

[line-height代码示例](https://codepen.io/lord2416/pen/RBMaMe)

## 十五、text-size-justify
**text-size-adjust** 属性 允许我们控制将文本溢出算法应用到一些手机设备上。这个属性还没有写进标准，使用时必须加上前缀：-moz-text-size-adjust，-webkit-text-size-adjust,，和 -ms-text-size-adjust。

许多网页还没有用手机开发，智能手机浏览器和桌面浏览器渲染网页时在一些地方有不同。他们不是以设备屏幕宽度布局网页，而是用比屏幕宽一些的视窗去布局网页，通常是800到1000像素。为了将视窗上的布局映射到原始设备屏幕上，手机浏览器要么只渲染整个页面的一部分，要么将视窗缩放至原始屏幕大小。

因为缩放适配小屏幕而导致文字会变得很小，许多手机浏览器会使用文本溢出算法让文本变大而更易读。当一个包含文本的元素宽度用了100%，他的文本大小会增加直到达到一个易读的大小，但是不会修改布局。

text-size-adjust   这个属性允许开发者去除或者修改这个浏览器默认行为，因为当网页设计已经处理小屏幕的宽度问题时不需要他。

> - 这个属性并不是标准。 你必须为每个你想要应用的浏览器加上属性前缀。
> - 不同浏览器，这个属性有不同的行为和语法。更多的信息，请查看下面的浏览器兼容性部分。
> - 这个属性只有在一些智能手机和平板电脑上使用。 桌面浏览器和一些平板电脑浏览器并没有一些溢出算法。
> - 如果 -webkit-text-size-adjust 显式设置为 none, 老的基于桌面的WebKit和平板电脑浏览器，像 Chrome≤26 或者 Safari≤5, 不会忽略这个属性, 反而会阻止用户在web界面放大或缩小。#
> - 不是所有的浏览器都支持这个属性使用百分比值(例如 Webkit 和 Trident , 但是 Gecko不支持). 检查下面浏览器兼容的部分查看更多的信息。


```
/* 文本不会放大 */
text-size-adjust: none;

/* 文本可能会被放大 */
text-size-adjust: auto;

/* 文本固定为原大小的80% */
text-size-adjust: 80%;

/* 全局的值 */
text-size-adjust: inherit;
text-size-adjust: initial;
text-size-adjust: unset;
```

- **none**
禁用浏览器的文本溢出算法。在老的基于webkit内核的桌面端浏览器，这将阻止用户将网页放大或缩小。
- **auto**
启用 浏览器的文本溢出算法。该值用于取消先前使用CSS设置的none。
- <**percentage**>
启用 浏览器的文本溢出算法，具体用一个百分数来确定文本放大范围。

[text-size-justify代码示例](https://codepen.io/lord2416/pen/bjvqVo/)