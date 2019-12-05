---
title: css属性:动画(Animation)
date: 2018-09-28
author: leonliu
category: css basic
tags: 
- css基础
---
参考链接：
- [css.doyoe.com](https://css.doyoe.com/)
- [css2.1中文版](http://www.ayqy.net/doc/css2-1/cover.html)
- [MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS)

## animation
<!--more-->
### 概述
 **animation**属性是如下属性的一个简写属性形式: 
 - **animation-name**: 检索或设置对象所应用的动画名称
 - **animation-duration**: 检索或设置对象动画的持续时间
 - **animation-timing-function**: 检索或设置对象动画的过渡类型
 - **animation-delay**: 检索或设置对象动画延迟的时间
 - **animation-iteration-count**: 检索或设置对象动画的循环次数
 - **animation-direction**: 检索或设置对象动画在循环中是否反向运动
 - **animation-fill-mode**: 检索或设置对象动画时间之外的状态
 - **animation-play-state**: 检索或设置对象动画的状态。w3c正考虑是否将该属性移除，因为动画的状态可以通过其它的方式实现，比如重设样式

```
默认值：    看每个独立属性
适用于：    所有元素，包含伪对象:after和:before
继承性：    无
动画性：    否
计算值：    看每个独立属性
媒体：      视觉
```


## animation-name
### 概述
**animation-name**属性指定应用的一系列动画，每个名称代表一个由@keyframes定义的动画序列


```
默认值：    none
适用于：    所有元素，包含伪对象:after和:before
继承性：    无
动画性：    否
计算值：    指定值
媒体：      视觉
相关属性：  [ @keyframes ]
```

### 示例
```
/* Single animation */
animation-name: none;
animation-name: test_05;
animation-name: -specific;
animation-name: sliding-vertically;

/* Multiple animations */
animation-name: test1, animation4;
animation-name: none, -moz-specific, sliding;

/* Global values */
animation-name: initial
animation-name: inherit
animation-name: unset
```

### 语法
- **none**: 特殊关键字，表示无关键帧。可以不改变其他标识符的顺序而使动画失效，或者使层叠的动画样式失效。
- <**IDENT**>: 标识动画的字符串，由大小写不敏感的字母a-z、数字0-9、下划线(_)和/或横线(-)组成。第一个非横线字符必须是字母，数字不能在字母前面，不允许两个横线出现在开始位置。


## animation-duration
### 概述
**animation-duration**属性指定一个动画周期的时长。默认值为0s，表示无动画。


```
默认值：    0s
适用于：    所有元素，包含伪对象:after和:before
继承性：    无
动画性：    否
计算值：    指定值
媒体：      视觉
```

### 语法
- <**time**>：
一个动画周期的时长，单位为秒(s)或者毫秒(ms)，无单位值无效。

```
animation-duration: 6s
animation-duration: 120ms
animation-duration: 1s, 15s
animation-duration: 10s, 30s, 230ms
```

## animation-timing-function
### 概述
**animation-timing-function**属性定义CSS动画在每一动画周期中执行的节奏。可能值为一或多个 <**timing-function**>。


```
默认值：    ease
适用于：    所有元素，包含伪对象:after和:before
继承性：    无
动画性：    否
计算值：    指定值
媒体：      视觉
```

### 语法

```
/* Keyword values */
animation-timing-function: ease;
animation-timing-function: ease-in;
animation-timing-function: ease-out;
animation-timing-function: ease-in-out;
animation-timing-function: linear;
animation-timing-function: step-start;
animation-timing-function: step-end;

/* Function values */
animation-timing-function: cubic-bezier(0.1, 0.7, 1.0, 0.1);
animation-timing-function: steps(4, end);
animation-timing-function: frames(10);

/* Multiple animations */
animation-timing-function: ease, step-start, cubic-bezier(0.1, 0.7, 1.0, 0.1);

/* Global values */
animation-timing-function: inherit;
animation-timing-function: initial;
animation-timing-function: unset;
```

- <**timing-function**>
    - **linear**：
    线性过渡。等同于贝塞尔曲线(0.0, 0.0, 1.0, 1.0)
    - **ease**：
    平滑过渡。等同于贝塞尔曲线(0.25, 0.1, 0.25, 1.0)
    - **ease-in**：
    由慢到快。等同于贝塞尔曲线(0.42, 0, 1.0, 1.0)
    - **ease-out**：
    由快到慢。等同于贝塞尔曲线(0, 0, 0.58, 1.0)
    - **ease-in-out**：
    由慢到快再到慢。等同于贝塞尔曲线(0.42, 0, 0.58, 1.0)
    - **step-start**：
    等同于 steps(1, start)
    - **step-end**：
    等同于 steps(1, end)
    - **steps(<integer>[, [ start | end ] ]?)**：
    接受两个参数的步进函数。第一个参数必须为正整数，指定函数的步数。第二个参数取值可以是start或end，指定每一步的值发生变化的时间点。第二个参数是可选的，默认值为end。
    - **cubic-bezier(<number>, <number>, <number>, <number>)**：
    特定的贝塞尔曲线类型，4个数值需在[0, 1]区间内

## animation-delay
### 概述
**animation-delay**属性定义动画于何时开始，即从动画应用在元素上到动画开始的这段时间的延迟多久。

```
默认值：    0s
适用于：    所有元素，包含伪对象:after和:before
继承性：    无
动画性：    否
计算值：    指定值
媒体：      视觉
```

- 0s是该属性的默认值，代表动画在应用到元素上后立即开始执行。否则，该属性的值代表动画样式应用到元素上后会延迟执行；
- 定义一个负值会让动画立即开始。但是动画会从它的动画序列中某位置开始。例如，如果设定值为-1s，动画会从它的动画序列的第1秒位置处立即开始。
- 如果为动画延迟指定了一个负值，但起始值是隐藏的，则从动画应用于元素的那一刻起就获取起始值。
 
### 语法

```
animation-delay: 3s;
animation-delay: 2s, 4ms;
```

- <**time**>
从动画样式应用到元素上到元素开始执行动画的时间差（延迟）。该值可用单位为秒(s)和毫秒(ms)。如果未设置单位，定义无效。

## animation-iteration-count
### 概述
**animation-iteration-count**属性定义动画循环播放的次数。默认次数为1。

```
默认值：    1
适用于：    所有元素，包含伪对象:after和:before
继承性：    无
动画性：    否
计算值：    指定值
媒体：      视觉
```

### 语法

```
animation-iteration-count: infinite;
animation-iteration-count: 3;
animation-iteration-count: 2.3;
animation-iteration-count: 2, 0, infinite;
```

- **infinite**: 无限循环播放。
- <**number**>: 动画播放的次数 不可为负值。 可以用小数定义循环(0.5 将播放动画到关键帧的一半（from 0 ~ 50%)。

## animation-direction
### 概述
**animation-direction** 属性指示动画是否反向播放。

```
默认值：    normal
适用于：    所有元素，包含伪对象:after和:before
继承性：    无
动画性：    否
计算值：    指定值
媒体：      视觉
```

### 语法

```
animation-direction: normal
animation-direction: reverse
animation-direction: alternate
animation-direction: alternate-reverse
animation-direction: normal, reverse
animation-direction: alternate, reverse, normal
```

- **normal**: 每个循环内动画向前循环，换言之，每个动画循环结束，动画重置到起点重新开始，这是默认属性
- **alternate**: 动画交替反向运行，反向运行时，动画按步后退，同时，带时间功能的函数也反向，比如，ease-in 在反向时成为ease-out。计数取决于开始时是奇数迭代还是偶数迭代
- **reverse**: 反向运行动画，每周期结束动画由尾到头运行
- **alternate-reverse**: 反向交替， 反向开始交替。动画第一次运行时是反向的，然后下一次是正向，后面依次循环。决定奇数次或偶数次的计数从1开始
 
## animation-play-state
### 概述
**animation-play-state** 属性定义一个动画是否运行或者暂停。
- 可以通过查询它来确定动画是否正在运行。另外，它的值可以被设置为暂停和恢复的动画的重放。
- 恢复一个已暂停的动画，将从它开始暂停的时候，而不是从动画序列的起点开始在动画。

### 语法

```
/* Single animation */
animation-play-state: running;
animation-play-state: paused;

/* Multiple animations */
animation-play-state: paused, running, running;

/* Global values */
animation-play-state: inherited;
animation-play-state: initial;
animation-play-state: unset;
```

- **running**: 运行
- **paused**： 停止

## animation-fill-mode
### 概述
animation-fill-mode 属性用来指定在动画执行之前和之后如何给动画的目标应用样式。

```
默认值：    none
适用于：    所有元素，包含伪对象:after和:before
继承性：    无
动画性：    否
计算值：    指定值
媒体：      视觉
```

### 语法

```
animation-fill-mode: none
animation-fill-mode: forwards
animation-fill-mode: backwards
animation-fill-mode: both

/* 可以应用多个参数，这个时候使用逗号隔开  */
/* 各个参数应用于与次序相对应的动画名 */
animation-fill-mode: none, backwards
animation-fill-mode: both, forwards, none
```

- **none**: 默认值。不设置对象动画之外的状态
- **forwards**: 目标保持动画最后一帧的样式，最后一帧是哪个取决于animation-direction和 animation-iteration-count:

animation-direction | animation-iteration-count | last keyframe encountered
---|---|---
normal | even or odd | 100% or to
reverse | even or odd | 0% or from
alternate | even | 0% or from
alternate | odd	 | 100% or to
alternate-reverse |	even | 100% or to
alternate-reverse | odd | 0% or from

- **backwards**: 动画采用相应第一帧的样式，保持 animation-delay，第一帧取法如下：

animation-direction	| first relevant keyframe
---|---
normal or alternate | 0% or from
reverse or alternate-reverse | 100% or to

- **both**: 动画将会执行 forwards 和 backwards 执行的动作。

## @keyframe 关键帧
### 概述
**@keyframes** 规则通过在动画序列中定义关键帧（或waypoints）的样式来控制CSS动画序列中的中间步骤。

- @keyframes定义的动画名称用来被animation-name所使用
- 定义动画时，简单的动画可以直接使用关键字from和to，即从一种状态过渡到另一种状态
- 如果复杂的动画，可以混合<percentage>去设置某个时间段内的任意时间点的样式
- 当然，也可以不使用关键字from和to，而都使用<percentage>

**注意**：
- ==让关键帧序列生效==
    - 如果一个关键帧规则没有指定动画的开始或结束状态（也就是，0%/from 和100%/to，浏览器将使用元素的现有样式作为起始/结束状态。这可以用来从初始状态开始元素动画，最终返回初始状态。
    - 如果在关键帧的样式中使用了不能用作动画的属性，那么这些属性会被忽略掉，支持动画的属性仍然是有效的，不受波及。
- ==重复定义(Duplicate resolution)==
    - 如果多个关键帧使用同一个名称，以最后一次定义的为准。 @keyframes 不存在层叠样式(cascade)的情况，所以动画在一个时刻（阶段）只会使用一个的关键帧的数据。
    - 如果一个@keyframes 里的关键帧的百分比存在重复的情况，以最后一次定义的关键帧为准。 因为@keyframes 的规则不存在层叠样式(cascade)的情况，即使多个关键帧设置相同的百分值也不会全部执行。
- ==属性个数不定==
    - 如果一个关键帧中没有出现其他关键帧中的属性，那么这个属性将使用插值(不能使用插值的属性除外, 这些属性会被忽略掉)
    
```
@keyframes identifier {
  0% { top: 0; left: 0; }
  30% { top: 50px; }
  68%, 72% { left: 50px; }
  100% { top: 100px; left: 100%; }
}
//例子中，"top"属性分别出现在 0%, 30%和100%的关键帧中，"left"属性分别出现在0%, 68%和100% 关键帧中.
```
- ==当关键帧被重复定义==
    - 如果某一个关键帧出现了重复的定义，且重复的关键帧中的css属性值不同，以最后一次定义的属性为准。
- ==关键帧中的 !important 关键词==
    - 关键帧中出现的 !important 关键词将会被忽略


```
@keyframes important1 {
  from { margin-top: 50px; }
  50%  { margin-top: 150px !important; } /* 忽略 */
  to   { margin-top: 100px; }
}

@keyframes important2 {
  from { margin-top: 50px;
         margin-bottom: 100px; }
  to   { margin-top: 150px !important; /* 忽略 */
         margin-bottom: 50px; }
}
```

### 语法
- <**identifier**>
帧列表的名称。 名称必须符合 CSS 语法中对标识符的定义。
- **from**
等效于 0%.
- **to**
等效于 100%.
- <**percentage**>
动画序列中，触发关键帧的时间点，使用百分值来表示。

[animation代码实例，旋转的正方体](https://codepen.io/lord2416/pen/gdjYxq)

[系列动画](https://designmodo.com/demo/stepscss/index.html)