---
title: css属性:过渡(Transition)
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
 
## transition
<!--more-->
### 概述
**CSS transitions** 提供了一种在更改CSS属性时控制动画速度的方法。 其可以让属性变化成为一个持续一段时间的过程，而不是立即生效的。比如，将一个元素的颜色从白色改为黑色，通常这个改变是立即生效的，使用 CSS transitions 后该元素的颜色将逐渐从白色变为黑色，按照一定的曲线速率变化。这个过程可以自定义。
通常将两个状态之间的过渡称为**隐式过渡（implicit transitions）**，因为开始与结束之间的状态由浏览器决定。

CSS transitions 
- 可以决定哪些属性发生动画效果 (明确地列出这些属性)，
- 何时开始 (设置 delay），
- 持续多久 (设置 duration) 
- 以及如何动画 (定义timing funtion，比如匀速地或先快后慢)。


```
默认值:
- transition-delay: 0s
- transition-duration: 0s
- transition-property: all
- transition-timing-function: ease
适用于：    所有元素，包含伪对象:after和:before
继承性：    无
动画性：    否
计算值：    看每个独立属性
媒体：      交互
```


[参考：可动画属性列表 ](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties) 

### 语法
**transition**是一个简写属性，用于**transition-property**, **transition-duration**, **transition-timing-function**, 和 **transition-delay**。


```
/* Apply to 1 property */
/* property name | duration */
transition: margin-right 4s;

/* property name | duration | delay */
transition: margin-right 4s 1s;

/* property name | duration | timing function */
transition: margin-right 4s ease-in-out;

/* property name | duration | timing function | delay */
transition: margin-right 4s ease-in-out 1s;

/* Apply to 2 properties */
transition: margin-right 4s, color 1s;

/* Apply to all changed properties */
transition: all 0.5s ease-out;

/* Global values */
transition: inherit;
transition: initial;
transition: unset;
```

**注意**：在transition属性中，各个值的书写顺序是很重要的：第一个可以解析为时间的值会被赋值给transition-duration，第二个可以解析为时间的值会被赋值给transition-delay。

## transition-property
### 概述
**transition-property** 指定应用过渡属性的名称

```
默认值：    all
适用于：    所有元素，包含伪对象:after和:before
继承性：    无
动画性：    否
计算值：    指定值
媒体：      视觉
```

### 语法

```
/* Keyword values */
transition-property: none;
transition-property: all;

/* <custom-ident> values */
transition-property: test_05;
transition-property: -specific;
transition-property: sliding-vertically;

/* Multiple values */
transition-property: test1, animation4;
transition-property: all, height, all;
transition-property: all, -moz-specific, sliding;

/* Global values */
transition-property: inherit;
transition-property: initial;
transition-property: unset;
```

- **none**：没有过渡动画。
- **all**：所有可被动画的属性都表现出过渡动画。
- **IDENT**：属性名称。由小写字母 a 到 z，数字 0 到 9，下划线（_）和破折号（-）。第一个非破折号字符不能是数字。同时，不能以两个破折号开头。[参考：可动画属性列表 ](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties) 

## transition-duration
### 概述
**transition-duration** 属性以秒或毫秒为单位指定过渡动画所需的时间。默认值为 0s ，表示不出现过渡动画。

可以指定多个时长，每个时长会被应用到由 transition-property 指定的对应属性上。如果指定的时长个数小于属性个数，那么时长列表会重复。如果时长列表更长，那么该列表会被裁减。两种情况下，属性列表都保持不变。


```
默认值：    0s
适用于：    所有元素，包含伪对象:after和:before
继承性：    无
动画性：    否
计算值：    指定值
媒体：      交互
```

### 语法

```
/* <time> 值 */
transition-duration: 6s;
transition-duration: 120ms;
transition-duration: 1s, 15s;
transition-duration: 10s, 30s, 230ms;

/* 全局值 */
transition-duration: inherit;
transition-duration: initial;
transition-duration: unset;
```

- <**time**>
<**time类型**>。表示过渡属性从旧的值转变到新的值所需要的时间。如果时长是 0s ，表示不会呈现过渡动画，属性会瞬间完成转变。不接受负值。

## transition-timing-function
### 概述
CSS属性受到 transition effect的影响，会产生不断变化的中间值，而 **CSS transition-timing-function 属性**用来描述这个中间值是怎样计算的。实质上，通过这个函数会建立一条加速度曲线，因此在整个transition变化过程中，变化速度可以不断改变。


```
默认值：    ease
适用于：    所有元素，包含伪对象:after和:before
继承性：    无
动画性：    否
计算值：    指定值
媒体：      交互
```

### 语法

```
transition-timing-function: ease
transition-timing-function: ease-in
transition-timing-function: ease-out
transition-timing-function: ease-in-out
transition-timing-function: linear
transition-timing-function: cubic-bezier(0.1, 0.7, 1.0, 0.1)
transition-timing-function: step-start
transition-timing-function: step-end
transition-timing-function: steps(4, end)

transition-timing-function: ease, step-start, cubic-bezier(0.1, 0.7, 1.0, 0.1)

transition-timing-function: inherit
```

- **<timing-function>**
通过transition-property中定义被过渡属性，每个 <timing-function>的值代表与这个属性相对应的timing function.
    - **cubic-bezier(x1, y1, x2, y2)**: 特定的贝塞尔曲线类型，4个数值需在[0, 1]区间内
    - **steps(number_of_steps, direction)**: 接受两个参数的步进函数。第一个参数必须为正整数，指定函数的步数。第二个参数取值可以是start或end，指定每一步的值发生变化的时间点。第二个参数是可选的，默认值为end。
    - **step-start**：等同于 steps(1, start)
    - **step-end**：等同于 steps(1, end)
    - **ease-in-out**: 由慢到快再到慢。等同于贝塞尔曲线(0.42, 0, 0.58, 1.0)
    - **ease-out**：由快到慢。等同于贝塞尔曲线(0, 0, 0.58, 1.0)
    - **ease-in**：由慢到快。等同于贝塞尔曲线(0.42, 0, 1.0, 1.0)
    - **ease**: 平滑过渡。等同于贝塞尔曲线(0.25, 0.1, 0.25, 1.0)
    - **linear**: 线性过渡。等同于贝塞尔曲线(0.0, 0.0, 1.0, 1.0)

## transition-delay
### 概述
- **transition-delay属性**规定了在过渡效果开始作用之前需要等待的时间。
- 值以秒（s）或毫秒（ms）为单位，表明动画过渡效果将在何时开始。取值为正时会延迟一段时间来响应过渡效果；取值为负时会导致过渡立即开始。


```
默认值：    0
适用于：    所有元素，包含伪对象:after和:before
继承性：    无
动画性：    否
计算值：    指定值
媒体：      交互
```

### 语法

```
/* <time>?值 */
transition-delay: 3s;
transition-delay: 2s, 4ms;

/* 全局变量 */
transition-delay: inherit;
transition-delay: initial;
transition-delay: unset;
```

- <**time**>
表明动画效果属性生效之前需要等待的时间。

[transition代码实例](https://codepen.io/lord2416/pen/mGpZJM)