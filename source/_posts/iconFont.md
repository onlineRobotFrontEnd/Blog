---
title: iconFont
date: 2018-10-17
author: vivizhou0596
category: css 高级
tags: 
    - css高级, -iconFont, -svg-sprite
---

# 1.原理
## 1.1 系统字体
    
计算机中，各种信息都是以二进制编码的形式存在的，不管是文字还是其它各种信息，在计算机中都是以０和１组成的二进制代码表示的，之所以能区别这些信息的不同，是因为它们采用的编码规则不同。英文字母用的是单字节的ASCII码，汉字采用的是双字节的汉字内码。
 1. 字符（英文，包括字母、数字、标点、运算符等）编码，国际通用的ASCII码；
 2. 汉字的编码
    * 汉字内码；
    * 汉字外码；
    * 汉字字形码。
    
在计算机内表示汉字而统一的编码方式形成汉字编码叫内码（如国标码），内码是惟一的。为方便汉字输入而形成的汉字编码为输入码，属于汉字的外码，输入码因编码方式不同而不同，是多种多样的。为显示和打印输出汉字而形成的汉字编码为字形码，计算机通过汉字内码在字模库中找出汉字的字形码，实现其转换。

## 1.2 web字体
**css font-family** 
    通过定义web上面文字的fontfamily,确定页面显示字体。
<!--more-->
---
```
.font{
    font-size: 16px;
    font-family: '微软雅黑';
}
```
但是这种情况下只能用系统默认的一些字体，限制比较大。web前端工程师必须使用已在用户计算机上安装好的字体。

css3可以自定义字体，加载自己的字体，使用 @font-face 定义一个字体family：

**css @font-face** 

这是一个叫做CSS@规则，它允许网页开发者为其网页指定在线字体，通过这种作者自备字体的方式，@font-face可以消除对用户电脑字体的依赖。
```
    @font-face {
      [ font-family: <family-name>; ] ||  /* 必填。所指定的字体名字将会被用于font或font-family属性 */
      [ src: <src>; ] || /* 必填。远程字体文件位置的URL或者用户计算机上的字体名称， 可以使用local语法通过名称指定用户的本地计算机上的字体( i.e. src: local('Arial'); )。 如果找不到该字体，将会尝试其他来源，直到找到它。*/
      [ unicode-range: <unicode-range>; ] || /* 可选。定义该字体支持Unicode字符的范围。默认值是"ü+0-10 FFFF"*/
      [ font-weight: <font-weight>; ] || /*  可选。定义字体的粗细。默认值是"正常" */
      [ font-style: <font-style>; ] /* 可选。定义该字体应该是怎样样式。默认值是"正常" */
      [ font-variant: <font-variant>; ] ||  
      [ font-feature-settings: <font-feature-settings>; ] ||  
      [ font-variation-settings: <font-variation-settings>; ] ||
      [ font-stretch: <font-stretch>; ] || /*可选。定义该字体应该如何被拉长。默认值是"正常"*/
    }
  
```
{% raw %}
<iframe height='265' scrolling='no' title='MPQbKd' src='//codepen.io/vivizhou0596/embed/MPQbKd/?height=265&theme-id=0&default-tab=css,result' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/vivizhou0596/pen/MPQbKd/'>MPQbKd</a> by vivizhou0596 (<a href='https://codepen.io/vivizhou0596'>@vivizhou0596</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}
使用示例

```
/* 定义字体 */
@font-face {
  font-family: "iconfont";
    src: url('iconfont.eot?t=1538029788022'); /* IE9*/
    src: url('iconfont.eot?t=1538029788022#iefix') format('embedded-opentype'), /* IE6-IE8 */
         url('data:application/x-font-woff;charset=utf-8;base64,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') format('woff'),
         url('iconfont.ttf?t=1538029788022') format('truetype'), /* chrome, firefox, opera, Safari, Android, iOS 4.2+*/
         url('iconfont.svg?t=1538029788022#iconfont') format('svg'); /* iOS 4.1- */
}

/* 使用字体 */
.iconfont {
  font-family:"iconfont" !important;
  font-size:16px;
  font-style:normal;
}
```
*注释：
   1. Firefox、Chrome、Safari 以及 Opera 支持 .ttf (True Type Fonts) 和 .otf (OpenType Fonts) 类型的字体。
   2. Internet Explorer 9+ 支持新的 @font-face 规则，但是仅支持 .eot 类型的字体 (Embedded OpenType)。
   3. Internet Explorer 8 以及更早的版本不支持新的 @font-face 规则。

    
# 2.实践

##2.1 创建项目，引用图标
先在阿里巴巴矢量图形库创建一个项目，添加一些图标。然后帮项目下载下来。

解压缩阿里图标库下载的文件，生成目录结构如下的文件夹：
  
  ```
    -fontIcon
    --demo_fontclass.html
    --demo_symbol.html
    --demo_unicode.html
    --iconfont.css
    --iconfont.eot
    --iconfont.js
    --iconfont.svg
    --iconfont.tty
    --iconfont.woff
  ```
  - css、html、js文件，是关于使用的说明和demo；
  - ttf、eot、woff、svg字体文件，最常用的ttf文件，另外三个是为了兼容不同的浏览器而额外引入的。
  
 ## 2.2 解析字体文件 
  工具软件：[FontForge](http://fontforge.github.io/en-US/downloads/)
  按如下步骤操作，查看系统的calibri字体：
    1.打开控制面板-字体-找到calibri字体，将文件拷到新的文件夹中;
    2.使用FontoForge打开calibri文件，会看到如下一张表；
   
    ![unicode](../../images/doge.png)
  
  - 字体文件就是这样以unicode作为索引的字形表，双击里面的某个字形，可以对它进行编辑，每个字形其实就是一个矢量图，因此ttf文件所表示的字库也叫矢量字库；
  - 与之对应的另一种字库——点阵字库，两者最大的区别就是点阵字库可以在Console Mode（命令行模式）下被渲染出来，而矢量字库必须在Graphics Mode（图形模式）中被渲染。
 
 ## 2.3 字体定义
 打开iconfont.css，可以看到 @font-face 声明，前文提到的自定义字体的声明，其中font-family属性定义了这个字体的名称，src属性定义了该要渲染字体需要下载的字体文件。
 ```
    @font-face {font-family: "iconfont";
      src: url('iconfont.eot?t=1537518751733'); /* IE9*/
      src: url('iconfont.eot?t=1537518751733#iefix') format('embedded-opentype'), /* IE6-IE8 */
           url('data:application/x-font-woff;charset=utf-8;base64,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') format('woff'),
           url('iconfont.ttf?t=1537518751733') format('truetype'), /* chrome, firefox, opera, Safari, Android, iOS 4.2+*/
           url('iconfont.svg?t=1537518751733#iconfont') format('svg'); /* iOS 4.1- */
    }
```
 
 ### 为何有两个src？
 ```
    绝大多数情况下，第一个 src 是可以去掉的，除非需要支持 IE9 下的兼容模式。在 IE9 中可以使用 IE7 和 IE8 的模式渲染页面，微软修改了在兼容模式下的 CSS 解析器，导致使用 ? 的方案失效。由于 CSS 解释器是从下往上解析的，所以在上面添加一个不带问号的 src 属性便可以解决此问题。
```
### #iefix有何作用？
```
   IE9 之前的版本没有按照标准解析字体声明，当 src 属性包含多个 url 时，它无法正确的解析而返回 404 错误，而其他浏览器会自动采用自己适用的 url。因此把仅 IE9 之前支持的 EOT 格式放在第一位，然后在 url 后加上 ?，这样 IE9 之前的版本会把问号之后的内容当作 url 的参数。至于 #iefix 的作用，一是起到了注释的作用，二是可以将 url 参数变为锚点，减少发送给服务器的字符。
```

后面的src和一堆url主要是为了兼容不同的浏览器，format属性告诉浏览器这个字体的格式，可选的字体格式有 woff、woff2、truetype、opentype、embedded-opentype、svg。

## 2.4 字体使用
  阿里提供Unicode、Font-class、Symbol三种引用方式。
  ### 2.4.1 Unicode
  ```
  /* HTML */
    <i class="iconfont">&#xe626;</i>
  
  /* css */
    .iconfont {
      font-family:"iconfont" !important;
      font-size:16px;
      font-style:normal;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
    }
```
html中'&#xe626;'其中&表示转义，#x可以用于表示16进制转义字符（Unicode主流的规范是UCS-2，即3个字节表示一个字符，所以unicode字符可以用一个16进制数表示）。

事实上，你也可以用“&#”对10进制的数进行转义，比如0xe626用十进制表示为58918，在html中你就可以这么写：
```
    <i class="icon testfont">&#58918;</i>
```
 - 我们可以直接从下载的demo_unicode.html文件中找到该图标对应的16进制数；
 如果你想对这个图形做一些修改，可以用fontForge打开字体文件，接着根据16进制数或者图标名字来定位到该图标：
 当在你在FontForge中修改了字形后，点击File->Generage Fonts.. 生成字体文件（记住每种格式导出一份），然后在font-face中修改文件的引用地址即可。
 
 ### 2.4.2 Font-class
 这种引入方式和原理第一种类似
  ```
 /* html */
    <i class="iconfont icon-guanbi"></i>

 /* css */
    .icon-guanbi:before { content: "\e626"; }
 ```
这种方式只是在原来的dom上增加一个伪元素，css中正斜杠\表示一个16进制数字。这样写的好处是可以直接通过审查dom元素就知道它引用的是哪个字形，看起来更加语义化。

   ### 2.4.3 Symbol
   iconfont事实上使用的是使用系统字体渲染引擎，而它是只支持单色的。
   官网称Symbol可以实现多色，如何做到的呢？以下是官网对其的描述：
```
    这是一种全新的使用方式，应该说这才是未来的主流，也是平台目前推荐的用法。这种用法其实是做了一个svg的集合，与另外两种相比具有如下特点：
    
    - 支持多色图标了，不再受单色限制。
    - 通过一些技巧，支持像字体那样，通过font-size,color来调整样式。
    - 兼容性较差，支持 ie9+,及现代浏览器。
    - 浏览器渲染svg的性能一般，还不如png。
```
使用步骤如下：

第一步：引入项目下面生成的symbol代码：
```
    <script src="./iconfont.js"></script>
```
第二步：加入通用css代码（引入一次就行）：
```
<style type="text/css">
    .icon {
     /* 通过设置 font-size 来改变图标大小 */
     width: 1em; height: 1em;
     /* 图标和文字相邻时，垂直对齐 */
     vertical-align: -0.15em;
     /* 通过设置 color 来改变 SVG 的颜色/fill */
     fill: currentColor;
     /* path 和 stroke 溢出 viewBox 部分在 IE 下会显示
        normalize.css 中也包含这行 */
     overflow: hidden;
   }
</style>
```
第三步：挑选相应图标并获取类名，应用于页面：
```
<svg class="icon" aria-hidden="true">
  <use xlink:href="#icon-xxx"></use>
</svg>
```
这里使用了SVG-Sprite，所以使用了js文件将svg嵌入了文档中而不是单独拿出来，因为SVG Sprite只能在同一个文档中使用svg的symbol。
因为svg的大小不是不支持font-size修改的，这里用了一个比较hack的方式，就是把图标元素的宽高都写为1em，而em的大小是相对于该元素的字体大小的，这样就实现了svg宽高跟着svg的字体大小一起变了。

# 3. SVG Sprite:

## 3.1 概述
    SVG Sprite类似于CSS中的Sprite技术，图标图形整合在一起，实际呈现的时候准确显示特定图标。
```
    <div>
        <div>
            <svg>
            <!-- 定义图形对象以供重复使用 -->
                <defs>
                    <g id="shape">
                        <rect x="0" y="0" width="50" height="50" />
                        <circle cx="0" cy="0" r="50" />
                    </g>
                </defs>
            <!-- 从svg文档中获取节点，并复制使用 -->    
                <use xlink:href="#shape" x="50" y="50" />
                <use xlink:href="#shape" x="200" y="50" />
            </svg>
        </div>
    
        <div>
            <h1>垮SVG调用</h1>
            <!-- SVG中的use元素可以调用其他SVG文件的元素，只要在一个文档中。 -->    
            <svg width="500" height="110">
                <use xlink:href="#shape" x="50" y="50" />
            </svg>
        </div>
    </div>
```
小结：
  1. 跨SVG调用就是“SVG Sprite技术”的核心所在。 
  2. 在页面载入一个充满Sprite(symbol)的SVG文件（或直接include SVG代码），在页面的任何角落，只要想使用这个图标，通过svg->use即可。
  3. 图标尺寸CSS控制，里面只有一个仅有xlink:href属性的use元素。

## 3.1 SVG Sprite实际应用

### 3.1.1 svg图标来源
    
1. 拿来主义,在图库下载
    - [阿里巴巴矢量图标库](http://www.iconfont.cn/)
    - [icoMoon](https://icomoon.io/)
2. 自己动手丰衣足食，使用专业的绘图工具[Adobe Illustrator]手动绘制

###3.1.1 合并svg图标
1. 站在巨人肩膀上
   使用[阿里巴巴矢量图标库](http://www.iconfont.cn/)或者[icoMoon](https://icomoon.io/)专业矢量图标网站；
2. 自己动手丰衣足食
   
    [svg-sprite-loader](https://github.com/kisenka/svg-sprite-loader)实现自己的icon组件
    
    原理：利用svg的symbol元素，将每个icon包括在symbol中，通过use元素使用该symbol.
    
    配置步骤如下：
    
    1、安装svg-sprite-loader，配置webpack rules
   ```
       // 安装 svg-sprite-loader
        npm install svg-sprite-loader --save
        
       // 配置webpack rules
       
       {
           test: /\.svg$/,
           use:[{loader: 'svg-sprite-loader'}],
       }
  
    ```
    svg-sprite-loader会把icon塞到一个个symbol中，symbol的id如果不特别指定，就是文件名。它最终会在你的html中嵌入一个svg，你就可以像这样：<use xlink:href="#symbolId"></use> 使用icon了。
    
    2、引入svg文件
    ```
        //引入 svg
        import default32 from './icons/assets/default32.svg';
        
        // 使用icon
        <div>
            <svg>
                <use xlinkHref={`#${default32.id}`} />
            </svg>
        </div>
    ```
    上面我们的基本功能已经完成了，还有最后一个小小的问题——我们每次引用一个文件的时候就得import一下，这还是很麻烦也不利于项目的管理。
    
    在这里，我们可以使用webpack的require.contextAPI来动态引入所有的Icon.
    
    现在我们是不能动态引入模块，但是webpack为我们提供了相关功能，webpack允许我们使用表达式动态引入模块。比如：require('./template/'+name+'.ejs');此时webpack会生成一个context module
    
    它接受三个参数，第一个是文件夹，第二个是是否使用子文件，第三个是文件匹配的正则。
    ```
        require.context(directory, useSubdirectories = false, regExp = /^\.\//)
    ```
   require.context会返回一个函数，并且该函数有keys()，id，resolve()属性。
    
    * keys()方法返回的该模块可以处理的所有可能请求的模块的数组，简单一点就是满足该参数的模块；
    * resolve()返回的是请求的module的id;
    * id是该context module的id;
   
   相关api可以查阅webpack关于[require-context](https://webpack.js.org/guides/dependency-management/#require-context)
       
   3、组件化
     ```
        // ./icon/index.js 动态引入所有的svg icon
        
            // requires and returns all modules that match
            const requireAll = requireContext => requireContext.keys().map(requireContext);
            // import all svg
            const req = require.context('./assets', false, /\.svg$/);
            export default requireAll(req);
        
        // ./Icon.jsx
            import React,{Component} from 'react'
            import iconImg  from './icons/index.js';
            
            export default  class Icon extends Component{
                render(){
                    const { name } = this.props;
                    const symbolId = iconImg.find(({default:{id}})=>id===name)
                    return (
                        <div>
                            <svg>
                                <use xlinkHref={`#${symbolId.default.id}`} />
                            </svg>
                        </div>
                    )
                }
            }
    ```
# 小结
    
   1. @font-face 自定义一个字体；
   2. Unicode、Font-class、Symbol引入字体；
   3. SVG Sprite 原理及应用。
   

参考链接：
- [浏览器字体渲染](http://www.woshipm.com/pd/97092.html)
- [使用阿里矢量图标库操作流程](https://blog.csdn.net/xingfaup/article/details/80333491)
- [SVG Sprite技术介绍](https://www.zhangxinxu.com/wordpress/2014/07/introduce-svg-sprite-technology/)
- [真正了解CSS3背景下的@font face规则](https://www.zhangxinxu.com/wordpress/2017/03/css3-font-face-src-local/)
- [webpack插件svg-sprite-loader--实现自己的icon组件](https://www.cnblogs.com/teemor/p/9565841.html)

