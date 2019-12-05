---
title: css属性:背景与边框
date: 2018-08-02
author: ChenEnjun
category: css basic
tags:
- css基础
---

# 边框
## border
> 定义元素边框的外观特性
```
border：<line-width> || <line-style> || <color>
```
<!--more--> 
### border-width
> 定义元素的边框厚度
```
border-width:top right bottom left
```

### border-style
> 定义元素的边框样式

```
//可用取值
hidden：隐藏边框。
dotted：点状轮廓。
ashed：虚线轮廓。
solid：实线轮廓
double：双线轮廓。两条单线与其间隔的和等于指定的border-width值
groove：3D凹槽轮廓。
ridge：3D凸槽轮廓。
inset：3D凹边轮廓。
outset：3D凸边轮廓。
```
<iframe width="100%" height="300" src="//jsrun.net/FsgKp/embedded/all/light/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

### border-color
> 定义元素的边框颜色

### border-shadow
> 定义元素的阴影

```
//可用取值
none：无阴影
<length>①：第 1 个长度值定义元素的阴影水平偏移值。正值，阴影出现在元素右侧；负值，则阴影出现在元素左侧
<length>②：第 2 个长度值定义元素的阴影垂直偏移值。正值，阴影出现在元素底部；负值，则阴影出现在元素顶部
<length>③：第 3 个长度值定义元素的阴影模糊值半径（如果提供了）。该值越大阴影边缘越模糊，若该值为0，阴影边缘不出现模糊。不允许负值
<length>④：第 4 个长度值定义元素的阴影外延值（如果提供了）。正值，阴影将向四面扩展；负值，则阴影向里收缩
<color>：定义元素阴影的颜色。如果该值未定义，阴影颜色将默认取当前最近的文本颜色
inset：定义元素的阴影类型为内阴影。该值为空时，则元素的阴影类型为外阴影
```
<iframe width="100%" height="300" src="//jsrun.net/xsgKp/embedded/all/light/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

> 结合伪类实现阴影

<iframe width="100%" height="300" src="//jsrun.net/GsgKp/embedded/all/light/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

### border-radius
> 定义元素的阴影

```
border-radius：<length> | <percentage>
border-radius = border-top-left-radius,
                border-top-right-radius,
                border-bottom-right-radius,
                border-bottom-left-radius
```

### border-image
> 定义将图像应用到元素的边框上

```
border-image-source：
定义元素边框背景图像，可以是图片路径或使用渐变创建的“背景图像”。
border-image-slice：
定义元素边框背景图像从什么位置开始分割。
border-image-width：
定义元素边框背景图像厚度。
border-image-outset：
定义元素边框背景图像的外延尺寸。
border-image-repeat：
定义元素边框背景图像的平铺方式。
```
# 背景
## background
> 定义元素的背景特性
- [ ] 一个元素可以设置多组背景图像，每组属性间使用逗号分隔。（背景色background-color不能设置多组，背景色通常都定义在最后一组上）
- [ ] 如果设置的多组背景图之间存在着交集（即存在着重叠关系），前面的背景图会覆盖在后面的背景图之上。

### background-color
> 定义元素使用的背景颜色
- [ ] 背景图像会覆盖在背景颜色。

```
background-color:transparent；   //设置背景色透明
```


### background-image
> 定义元素使用的背景图像

```
 渐变属性：inear-gradient, radial-gradient, repeating-linear-gradient, repeating-radial-gradient
```
#### linear-gradient

```
下述值用来表示渐变的方向，可以使用角度或者关键字来设置：
<angle>：用角度值指定渐变的方向（或角度）。
to left：设置渐变为从右到左。相当于: 270deg
to right：设置渐变从左到右。相当于: 90deg
to top：设置渐变从下到上。相当于: 0deg
to bottom：设置渐变从上到下。相当于: 180deg。这是默认值，等同于留空不写。
<color-stop> 用于指定渐变的起止颜色：
<color>：指定颜色。
<length>：用长度值指定起止色位置。不允许负值
<percentage>：用百分比指定起止色位置。

background-image:linear-gradient(135deg, #9DC3E6 0%, #F4B183 25%, #C9C9C9 50%, #FFD966 75%, #A9D18E 100%);
```
<iframe width="100%" height="300" src="//jsrun.net/usgKp/embedded/all/light/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>
- [ ] 渐变图标 http://lea.verou.me/css3patterns/

### background-repeat
> 定义元素的背景图像如何填充。

```
repeat-x：背景图像在横向上平铺
repeat-y：背景图像在纵向上平铺
repeat：背景图像在横向和纵向平铺
no-repeat：背景图像不平铺
round：当背景图像不能以整数次平铺时，会根据情况缩放图像。（CSS3）
space：当背景图像不能以整数次平铺时，会用空白间隙填充在图像周围。（CSS3）
```
### background-attachment
> 定义滚动时背景图像相对于谁固定

```
fixed：背景图像相对于视口（viewport）固定。
scroll：背景图像相对于元素固定，也就是说当元素内容滚动时背景图像不会跟着滚动，因为背景图像总是要跟着元素本身。但会随元素的祖先元素或窗体一起滚动。
local：背景图像相对于元素内容固定，也就是说当元素随元素滚动时背景图像也会跟着滚动，因为背景图像总是要跟着内容。（CSS3）
```
### background-position
> 指定背景图像在元素中出现的位置

```
<percentage>：用百分比指定背景图像在元素中出现的位置。可以为负值。参考容器尺寸减去背景图尺寸进行换算。
<length>：用长度值指定背景图像在元素中出现的位置。可以为负值。
center：背景图像横向或纵向居中。
left：背景图像从元素左边开始出现。
right：背景图像从元素右边开始出现。
top：背景图像从元素顶部开始出现。
bottom：背景图像从元素底部开始出现。

示例：假设要定义背景图像在容器中右下方，并且距离右边和底部各有20px
background: url(test1.jpg) no-repeat right 20px bottom 20px;
```
- [ ] 雪碧图 https://www.toptal.com/developers/css/sprite-generator
- .icon2{background-position: -40px -40;}

### background-origin
> 指定的背景图像计算background-position时的参考原点(位置)

```
border-box从border区域（含border）开始显示背景图像。
padding-box：从padding区域（含padding）开始显示背景图像。
content-box：从content区域开始显示背景图像。
```
### background-clip
> 指定对象的背景图像向外裁剪的区域

```
border-box：从border区域（含border）开始向外裁剪背景。
padding-box：从padding区域（含padding）开始向外裁剪背景。
content-box：从content区域开始向外裁剪背景。
text：从前景内容的形状（比如文字）作为裁剪区域向外裁剪，如此即可实现使用背景作为填充色之类的遮罩效果。
```

- [ ] 文字遮罩 http://demo.doyoe.com/css3/background-clip/mask-text2.htm
### background-size
> 定义背景图像的尺寸大小

```
<length>：用长度值指定背景图像大小。不允许负值。
<percentage>：用百分比指定背景图像大小。不允许负值。
auto：背景图像的真实大小。
cover：将背景图像等比缩放到完全覆盖容器，背景图像有可能超出容器。
contain：将背景图像等比缩放到宽度或高度与容器的宽度或高度相等，背景图像始终被包含在容器内
```
