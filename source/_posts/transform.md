---
title: css属性:变化(Transform)
date: 2018-09-27
author: leonliu
category: css basic
tags: 
- css基础
---
参考链接：
- [css.doyoe.com](https://css.doyoe.com/)
- [css2.1中文版](http://www.ayqy.net/doc/css2-1/cover.html)
- [MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS)

 
## transform
<!--more-->
### 概述
 **transform** 属性允许你修改CSS视觉格式模型的坐标空间。使用它，元素可以被转换（translate）、旋转（rotate）、缩放（scale）、倾斜（skew）
> CSS transform 属性 , 只对 block 级元素生效！


```
初始值          none
适用元素        可变换元素
是否是继承属性	否
适用媒体        视觉
计算值          指定值，但相对长度会转换为绝对长度
动画性          是
```

### 示例
```
/* Keyword values */
transform: none;

/* Function values */
transform: matrix(1.0, 2.0, 3.0, 4.0, 5.0, 6.0);
transform: translate(12px, 50%);
transform: translateX(2em);
transform: translateY(3in);
transform: scale(2, 0.5);
transform: scaleX(2);
transform: scaleY(0.5);
transform: rotate(0.5turn);
transform: skew(30deg, 20deg);
transform: skewX(30deg);
transform: skewY(1.07rad);
transform: matrix3d(1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0, 10.0, 11.0, 12.0, 13.0, 14.0, 15.0, 16.0);
transform: translate3d(12px, 50%, 3em);
transform: translateZ(2px);
transform: scale3d(2.5, 1.2, 0.3);
transform: scaleZ(0.3);
transform: rotate3d(1, 2.0, 3.0, 10deg);
transform: rotateX(10deg);
transform: rotateY(10deg);
transform: rotateZ(10deg);
transform: perspective(17px);

/* Multiple function values */
transform: translateX(10px) rotate(10deg) translateY(5px);

/* Global values */
transform: inherit;
transform: initial;
transform: unset;
```

### 语法
- <**transform-function**>
至少一个 CSS transform functions 被应用
- **none**
指定为 不应用transform

### <transform-function>

#### 2D变化

- **matrix()** 用六个指定的值来指定一个均匀的二维（2D）变换矩阵


```
transform:  matrix(a, c, b, d, tx, ty)

/* a, b, c, d 创建了变形矩阵 
   ┌     ┐ 
   │ a b │
   │ c d │
   └     ┘
   tx, ty是变形的值 .  */
   
1.平移效果：
transform: matrix(1, 0, 0, 1, tx, ty);等同于transform：translate(tx, ty);

2.缩放效果：
transform: matrix(sx,0,0,sy,0,0); 等同于transform：scale(sx, sy);

3.旋转效果：
transform: matrix(cosθ,sinθ,-sinθ,cosθ,0,0); 等同于transform：rotate(θ); 
4.拉伸效果：
transform：matrix(1,tan(θy),tan(θx),1,0,0); 等同于transform: skew(θx + "deg"，θy+ "deg");
```

[css transform matrix 工具](http://www.css88.com/tool/css3Preview/Transform-Matrix.html)

- **translate()** 指定对象的2D translation（2D平移）。第一个参数对应X轴，第二个参数对应Y轴。如果第二个参数未提供，则默认值为0
- **translateX()** 指定对象X轴（水平方向）的平移，translate(tx, 0) 的简写形式
- **translateY()** 指定对象Y轴（垂直方向）的平移，translate(0, ty)的简写形式
- **rotate()** 指定对象的2D rotation（2D旋转），需先有 <' transform-origin '> 属性的定义。移动量由指定角度定义;如果为正值，则运动将为顺时针，如果为负值，则为逆时针 。 180°的旋转称为点反射 (point reflection)。

```
rotate(<angle>)
<angle> 代表旋转的角度。正角表示顺时针旋转，负角表示逆时针旋转
```
- **scale()** 
1. 指定对象的2D scale（2D缩放）。第一个参数对应X轴，第二个参数对应Y轴。如果第二个参数未提供，则默认取第一个参数的值。
2. 当超出 [-1, 1]范围外时，缩放将在坐标方向上放大元素；当在该范围内时，它在该方向收缩元素。当等于1时，它什么也不做，当它为负时，它执行点反射和大小修改。


```
scale(sx) or
scale(sx, sy)
```
- **scaleX()** 指定对象X轴的（水平方向）缩放
1. scaleX(sx) 是 scale(sx, 1) 和 scale3d(sx, 1, 1) 的简写形式。
2. scaleX(-1) 表示通过原点的垂直轴定义轴对称（由 transform-origin 属性指定）。
- **scaleY()** 指定对象Y轴的（垂直方向）缩放
1. scaleY(sy) 是 scale(1, sy) 和 scale3d(1, sy, 1) 的简写形式。
2. scaleY(-1) 定义了通过原点的水平轴的轴对称（由 transform-origin 属性指定）。
- **skew()** 指定对象skew transformation（斜切扭曲）。第一个参数对应X轴，第二个参数对应Y轴。如果第二个参数未提供，则默认值为0

> ==注意css斜切坐标系的x，y轴==

- **skewX()**
指定对象X轴的（水平方向）扭曲
- **skewY()**
指定对象Y轴的（垂直方向）扭曲

[Transform 2D 代码演示](https://codepen.io/lord2416/pen/YjLgWO)

#### 3D变化

- **matrix3d()** 用一个 4 × 4 的齐次矩阵来描述一个三维（3D）变换


```
transform: matrix3d(a1, b1, c1, d1, a2, b2, c2, d2, a3, b3, c3, d3, a4, b4, c4, d4);

1.平移变换X, 对应translateX(tx)：
matrix3d(1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, tx, 0, 0, 1)

2.平移变换Y, 对应translateY(ty)：
matrix3d(1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, ty, 0, 1)

3.平移变换，对应translateZ(tz)：
matrix3d(1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, tz, 1)

4.多维平移:
matrix3d(1,0,0,0,0,1,0,0,0,0,1,0,tx,ty,tz,1)

5.多维尺度：
matrix3d(cx, 0, 0, 0, 0, cy, 0, 0, 0, 0, cz, 0, 0, 0, 0, 1 );

6.旋转变换：
X轴：matrix3d(1,0,0,0,0,cos(θ),sin(θ),0,0,-sin(θ),cos(θ),0,0,0,0,1);
Y轴：matrix3d(cos(θ),0,-sin(θ),0,0,1,0,0,sin(θ),0,cos(θ),0,0,0,0,1);
Z轴：matrix3d(cos(θ),sin(θ),0,0,-sin(θ),cos(θ),0,0,0,0,1,0,0,0,0,1);
```
- **translate3d()** 指定对象的3D位移。第1个参数对应X轴，第2个参数对应Y轴，第3个参数对应Z轴，参数不允许省略

[Transform 3D 代码演示](https://codepen.io/lord2416/pen/EppBgy)

## transform-origin
### 概述
**transform-origin** 属性让你更改一个元素变形的原点。

```
初始值          50% 50% 0
适用于          可变换元素
是否可继承      否
适用媒体        视觉
计算值          除了指定绝对值，否则都为百分比
动画性          当值为数值时
```

### 示例
```
/* One-value syntax */
transform-origin: 2px;
transform-origin: bottom;

/* x-offset | y-offset */
transform-origin: 3cm 2px;

/* x-offset-keyword | y-offset */
transform-origin: left 2px;

/* x-offset-keyword | y-offset-keyword */
transform-origin: right top;

/* y-offset-keyword | x-offset-keyword */
transform-origin: top right;

/* x-offset | y-offset | z-offset */
transform-origin: 2px 30% 10px;

/* x-offset-keyword | y-offset | z-offset */
transform-origin: left 5px -3px;

/* x-offset-keyword | y-offset-keyword | z-offset */
transform-origin: right bottom 2cm;

/* y-offset-keyword | x-offset-keyword | z-offset */
transform-origin: bottom right 2cm;

/* Global values */
transform-origin: inherit;
transform-origin: initial;
transform-origin: unset;
```

**transform-origin**属性可以使用一个，两个或三个值来指定，其中每个值都表示一个偏移量。 没有明确定义的偏移将重置为其对应的初始值。

如果定义了两个或更多值并且没有值的关键字，或者唯一使用的关键字是center，则第一个值表示水平偏移量，第二个值表示垂直偏移量。

- 一个值：
    - 必须是<length>，<percentage>，或 left, center, right, top, bottom关键字中的一个。
- 两个值：
    - 其中一个必须是<length>，<percentage>，或left, center, right关键字中的一个。
    - 另一个必须是<length>，<percentage>，或top, center, bottom关键字中的一个。
- 三个值：
    - 前两个值和只有两个值时的用法相同。
    - 第三个值必须是<length>。它始终代表Z轴偏移量。

### 语法    
- x-offset
    - 定义变形中心距离盒模型的左侧的<length>或<percentage>偏移值。
- offset-keyword
    - left，right，top，bottom或center中之一，定义相对应的变形中心偏移。
- y-offset
    - 定义变形中心距离盒模型的顶的<length>或<percentage>偏移值。
- x-offset-keyword
    - left，right或center中之一，定义相对应的变形中心偏移。
- y-offset-keyword
    - top，bottom或center中之一，定义相对应的变形中心偏移。
- z-offset
    - 定义变形中心距离用户视线（z=0处）的<length>（不能是<percentage>）偏移值。


keyword | value
---|---
left | 0%
center | 50%
right | 100%
top | 0%
bottom | 100%

[transform-origin 代码示例](https://codepen.io/lord2416/pen/EppBgy)

## transform-style
### 概述

```
初始值              flat
适用元素            可变换元素
是否是继承属性      否
适用媒体            视觉
计算值              指定值
动画性              否
```

### 示例
```
transform-style: preserve-3d
transform-style: flat

transform-style: inherit
```

### 语法
- **preserve-3d**
    - 指定子元素定位在三维空间内
- **flat**
    - 指定子元素位于此元素所在平面内

## perspective
### 概述
- **perspective** 属性指定了观察者与z=0平面的距离，使具有三维位置变换的元素产生透视效果。z>0的三维元素比正常大，而z<0时则比正常小，大小程度由该属性的值决定。

- 三维元素在观察者后面的部分不会绘制出来，即z轴坐标值大于perspective属性值的部分。

- 默认情况下，消失点位于元素的中心，但是可以通过设置perspective-origin属性来改变其位置。

- 当该属性值不为0和none时，会创建新的层叠上下文。


```
默认值：    none
适用于：    变换元素
继承性：    无
动画性：    当值为<length>时
计算值：    绝对长度或「none」
媒体：      视觉
```

### 示例

```
/* Keyword value */
perspective: none;

/* <length> values */
perspective: 20px;  
perspective: 3.5em;

/* Global values */
perspective: inherit;
perspective: initial;
perspective: unset;
```

[perspective 代码实例](https://codepen.io/lord2416/pen/EppBgy)

## perspective-origin
### 概述
**perspective-origin**属性决定了观察者正在观看的位置，即灭点(vanishing point)位置。


```
默认值      50% 50%，效果等同于center center
适用于      可变换元素
继承性      无
动画性      当值为数值时
计算值      除了指定绝对值，否则都为百分比
媒体        视觉
```


### 示例
```
/* One-value syntax */
perspective-origin: x-position;

/* Two-value syntax */
perspective-origin: x-position y-position;

/* When both x-position and y-position are keywords,
   the following is also valid */
perspective-origin: y-position x-position;

/* Global values */
perspective-origin: inherit;
perspective-origin: initial;
perspective-origin: unset;
```

- 该属性提供2个参数值。
- 如果提供两个，第一个用于横坐标，第二个用于纵坐标。
- 如果只提供一个，该值将用于横坐标；纵坐标将默认为center。

### 语法
- **x-position**指定消失点的横坐标，其值有以下形式：
    - <percentage> 百分比，相对于元素宽度，可为负值。
    - <length> 长度值，可为负值。
    - left，关键字，0值的简记。
    - center，关键字，50%的简记。
    - right，关键字，100%的简记。
- **y-position**指定消失点的纵坐标，其值有以下形式：
    -<percentage> 百分比，相对于元素的高度，可为负值。
    - <length> 长度值，可为负值。
    - top，关键字，0值得简记。
    - center，关键字，50%的简记。
    - bottom，关键字，100%的简记。

[perspective-origin代码示例](https://codepen.io/lord2416/pen/yqxEjx)

## backface-visibility
### 概述
**backface-visibility**属性指定当元素背面朝向观察者时是否可见。元素的背面总是透明的，当其朝向观察者时，显示正面的镜像。

- 决定一个元素背面面向用户时是否可见，需要直接在该元素上定义
**backface-visibility**属性，而不能在其父元素上，因为该属性默认为不可继承。
- 因为2D变换无透视效果，故该属性对2D变换无效。

```
默认值      visible
适用于      变换元素
继承性      无
动画性      否
计算值      指定值
媒体        视觉
```

### 示例

```
backface-visibility: visible
backface-visibility: hidden
```

### 语法
- **visible**：
指定元素背面可见，允许显示正面的镜像。
- **hidden**：
指定元素背面不可见

[backface-visibility代码实例](https://codepen.io/lord2416/pen/yqxEjx)