---
title: css属性:尺寸与补白
date: 2018-08-01
author: fengguangnan
category: css basic
tags: 
- css基础
---

## 尺寸
`Dimension`用于控制元素的高度和宽度，包含属性有width、height、min-width、max-height、max-width、max-height;
<!--more-->

语法
`<length> | <percentage> | auto `默认值为auto

**适用于**：除非置换内联元素，table-row, table-row-group之外的所有元素  
`width` `height`设置或检索对象的宽度和高度   
- 对于img对象来说，仅指定一个尺寸属性，另一值将根据图片源尺寸等比例缩放；     
特殊的比如iframe, canvas，当width的计算值为auto时，则宽度的使用值为300px,height为auto时,高度的使用值为150px。

<iframe height='265' scrolling='no' title='尺寸' src='//codepen.io/fengguangnan/embed/gjoreO/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/fengguangnan/pen/gjoreO/'>尺寸</a> by Fengguangnan (<a href='https://codepen.io/fengguangnan'>@fengguangnan</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

---
`min-width` `min-height`设置或检索对象的最小宽度和最小高度   
`max-width` `max-height` 设置或检索对象的最大宽度和最大高度  
-  `min-*` 值小于width(height)时，`min-*`会被忽略、大于width(height)时，`min-*`属性将会被忽略，同时width(height)会忽略自己的值定义而使用`min-*`的值作为自己的使用值；   
-  `max-*` 值小于width(height)时，会被忽略，同时width(height)会忽略自己的值定义而使用`max-*`的值作为自己的使用值、值大于width(height)时，`max-*`属性将会被忽略；    
- 如果`min-*`属性的值大于`max-*`属性的值，`max-*`将会自动以`min-*`的值作为自己的值。   

<iframe height='265' scrolling='no' title='尺寸' src='//codepen.io/fengguangnan/embed/BPJKmN/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/fengguangnan/pen/BPJKmN/'>尺寸</a> by Fengguangnan (<a href='https://codepen.io/fengguangnan'>@fengguangnan</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

---


## 补白
###  margin(外补白)
指从**自身边框到另一个容器边框之间的距**离，就是容器外距离
语法
`[ <length> | <percentage> | auto ]{1,4}`  

**取值**：`auto`：水平（默认）书写模式下，margin-top/margin-bottom计算值为0，margin-left/margin-right取决于可用空间     
   `<length>`： 用长度值来定义margin。==可以为负值==    
   `<percentage>`：用百分比来定义外补白。水平（默认）书写模式下，参照其父元素的 width 进行计算，其它情况参照 height ，==可以为负值  == 
   
如果提供全部四个参数值顺序顺序 margin:top、right、bottom、left;    

**适用于**：所有元素，除非 table | inline-table | table-caption 的表格类元素之外

属性值也可以拆分成四个：`margin-top`、`margin-right`、`margin-bottom`、`margin-left`    
`margin-top`、`margin-bottom`:非置换内联元素要使用该属性必须转为块级或行内块级

<iframe height='265' scrolling='no' title='margin' src='//codepen.io/fengguangnan/embed/LBQvqW/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/fengguangnan/pen/LBQvqW/'>margin</a> by Fengguangnan (<a href='https://codepen.io/fengguangnan'>@fengguangnan</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

---

### padding(内补白)
指**自身边框到自身内部另一个容器边框之间的距**离，就是容器内距离。
#### 语法
`[ <length> | <percentage>]{1,4}`   

**取值**：`<length>`：用长度值来定义内补白。==不允许负值==  
`<percentage>`：用百分比来定义内补白。水平（默认）书写模式下，参照其包含块 width 进行计算，其它情况参照 height 。==不允许负值==

如果提供全部四个参数值顺序与margin相同:top、right、bottom、left;  

**适用于**：所有元素，除 table-row-group | table-header-group | table-footer-group | table-column-group | table-row 外

属性值也可以拆分成四个：`padding-top`、`padding-right`、`padding-bottom`、`padding-left`    
- 给行内元素定义纵向内补白（padding-top/padding-bottom）时，虽然不需要将之转化为行内块或者块级，但是给行内元素设置纵向内补白并不会影响布局。内补白会在当前元素的行框基础上向顶部和顶部外延，

<iframe height='265' scrolling='no' title='padding' src='//codepen.io/fengguangnan/embed/NBYWRR/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/fengguangnan/pen/NBYWRR/'>padding</a> by Fengguangnan (<a href='https://codepen.io/fengguangnan'>@fengguangnan</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>