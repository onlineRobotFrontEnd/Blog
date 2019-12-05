---
title: css属性:内容与媒体查询
date: 2018-09-12
author: ChenEnjun
category: css basic
tags:
- css基础
---

# 内容
## content
> 用来和:after及:before伪元素一起使用，在对象前或后显示内容。
<!--more--> 
## counter-increment
> 设定当一个selector发生时计数器增加的值。取值：id number
## counter-reset
> 将指定selector的计数器复位。取值：id number
```
normal：默认值。表现与none值相同
none：不生成任何值。
<attr>：插入标签属性值
<url>：使用指定的绝对或相对地址插入一个外部资源（图像，声频，视频或浏览器支持的其他任何资源）
<string>：插入字符串
counter(name)：使用已命名的计数器
counter(name,list-style-type)：使用已命名的计数器并遵从指定的list-style-type属性
counters(name,string)：使用所有已命名的计数器
counters(name,string,list-style-type)：使用所有已命名的计数器并遵从指定的list-style-type属性
no-close-quote：并不插入quotes属性的后标记。但增加其嵌套级别
no-open-quote：并不插入quotes属性的前标记。但减少其嵌套级别
close-quote：插入quotes属性的后标记
open-quote：插入quotes属性的前标记
```
<iframe width="100%" height="300" src="//jsrun.net/FSgKp/embedded/all/light/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

## quotes
设置或检索对象内使用的嵌套标记。
取值 none | [<string> <string> <string> <string>]

# 媒体查询
> 通过不同的媒体类型和条件定义样式表规则。
1. 媒体查询让CSS可以更精确作用于不同的媒体类型和同一媒体的不同条件。
1. 媒体查询的大部分媒体特性都接受min和max用于表达“大于或等于”和“小与或等于”。如：width会有min-width和max-width
1. 媒体查询可以被用在CSS中的@media和@import规则上，也可以被用在HTML和XML中。

```
eg:
@media screen and (width:800px){ … }
@import url(example.css) screen and (width:800px);
<link media="screen and (width:800px)" rel="stylesheet" href="example.css" />
<?xml-stylesheet media="screen and (width:800px)" rel="stylesheet" href="example.css" ?>
```
## media

```
语法：
@media mediatype and|not|only (media feature) {
    CSS-Code;
}
针对多个媒体类型的CSS规则，可以用逗号来隔开
@media handheld and (min-width:360px),screen and (min-width:480px){
body{font-size:large;}
}
```
## mediatype
```
媒体类型mediatype 取值有 
all：用于所有设备
print：用于打印机和打印预览
screen: 用于电脑屏幕，平板电脑，智能手机等
speech: 应用于屏幕阅读器等发声设备
media 4 废弃：
braille	盲文
embossed 盲文打印
handheld 手持设备
projection 项目演示，比如幻灯
speech 演讲
tty	固定字母间距的网格的媒体，比如电传打字机
tv 电视
```
## 媒体特性

### width | height
> 定义输出设备中的页面可见区域宽度/高度 （接受min/max）

### aspect-ratio
> 定义输出设备中的页面可见区域宽度与高度的比率 （接受min/max）

### orientation（判断显示屏横向纵向）
> 定义输出设备中的页面可见区域高度是否大于或等于宽度
- [ ] landscape: 设备横向
- [ ] portrait: 设备纵向

### resolution 
> 定义设备的分辨率 eg:96dpi, 300dpi, 118dpcm （接受min/max）

### scan
> 定义电视类设备的扫描工序 
- [ ] progressive: 连续扫描
- [ ] interlace: 交织扫描

### grid
> 用来查询输出设备是否使用栅格或点阵 1代表是，0代表否

### color | color-index | monochrome
> 定义输出设备每一组彩色原件的个数 | 定义在输出设备的彩色查询表中的条目数 | 定义在一个单色框架缓冲区中每像素包含的单色原件个数 （接受min/max）

- [ ] 如果不是彩色设备，则值等于0

media 4废弃，针对移动设备

### device-width | device-height | device-aspect-ratio
> 定义输出设备的屏幕可见宽度宽度/高度 | 输出设备的屏幕可见宽度与高度的比率 （接受min/max）

## Media Queries Level 4
### 简洁语法

```
简洁语法：

@media (height > 600px) {
    body { line-height: 1.4; }
}

@media (400px <= width <= 700px) {
    body { line-height: 1.4; }
}
```

### update
> 输出设备修改内容外观的频率
- [ ] none 渲染后，无法再更新布局。如：打印在纸上的文档。
- [ ] slow 布局可以根据CSS的通常规则动态地改变，但是输出设备不能足够快地渲染或显示变化以使它们被感知为平滑动画。示例：电子书阅读器或严重不足的设备。
- [ ] fast 布局可以根据CSS的通常规则动态地改变，并且输出设备的速度不受异常限制，因此可以使用诸如CSS动画之类的定期更新。比如：计算机屏幕。

### overflow-block
> 输出设备如何处理沿块轴溢出视口的内容？
- [ ] none 不显示溢出块轴的内容。
- [ ] scroll 通过滚动可以看到溢出块轴的内容。
- [ ] optional-paged 可以通过滚动查看溢出块轴的内容，但可以手动触发分页符（例如via break-inside等），以使以下内容显示在下一页上。
- [ ] paged 内容被分解为不连续的页面; 在块轴中溢出一页的内容显示在下一页上。

### overflow-inline
> 可以滚动沿着内联轴溢出视口的内容吗？
- [ ] none 不显示溢出块轴的内容。
- [ ] scroll 通过滚动到内容轴可以看到溢出内联轴的内容。