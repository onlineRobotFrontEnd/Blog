---
title: 微信小程序
date: 2018-09-19
author: liuzhaozhao
category: wechart
tags: 
- 小程序
---

## 项目结构
<!--more-->


```
- page
- - index
- - - index.js
- - - index.json
- - - index.wxml
- - - index.wxss
- - log
- - - log.js
- - - log.json
- - - log.wxml
- - - log.wxss
- utils
- - util.js
- app.js
- app.json
- app.wxss
- project.config.json
```

四类文档：
- .json：配置文件
- .wxml：模板文件
- .wxss：样式文件
- .js： js文件


## 配置文件

- 全局配置
```
{
  "pages": [
    "pages/index/index",
    "pages/logs/index"
  ],
  "window": {
    "backgroundTextStyle": "light",            //下拉 loading 的样式，仅支持 dark / light
    "navigationBarBackgroundColor": "#fff",    //导航栏背景颜色
    "navigationBarTitleText": "Demo",          //导航栏标题文字内容
    "navigationBarTextStyle": "black",         //导航栏标题颜色，仅支持 black / white
    "enablePullDownRefresh": true,             //是否全局开启下拉刷新
    "backgroundColor": "#000"                  //页面上拉触底事件触发时距页面底部距离，单位为px
  },
  "tabBar": { 
    "color":"#00ff00",                         //字体颜色；
    "selectedColor": "#ff0000",                //选中tab字体颜色；
    "backgroundColor": "yellow",               //tab背景颜色；
    "borderStyle": "black",                    //tab边框，只能为black和white；
    "position":"bottom",                       //tabBar位置；
    "list": [{                                 //只能配置最少2个、最多5个 tab
      "pagePath": "pages/index/index",
      "text": "首页"
    }, {
      "pagePath": "pages/logs/logs",
      "text": "日志"
    }]
  },
  "networkTimeout": {
    "request": 10000,
    "downloadFile": 10000
  },
  "debug": true
}
```

- 页面配置 
```
{
    "navigationBarBackgroundColor": "#fff”,    //导航栏背景颜色
    "navigationBarTitleText": "WeChat”,        //导航栏标题文字内容
    "navigationBarTextStyle":"black”,          //导航栏标题颜色，仅支持 black / white
    "backgroundTextStyle":"light”,             //下拉 loading 的样式，仅支持 dark / light
    "backgroundColor":  "#ffffff",             //窗口的背景色
    "enablePullDownRefresh":  false,           //是否开启下拉刷新。
    "onReachBottomDistance”:  50,              //页面上拉触底事件触发时距页面底部距离，单位为px
    
    //只在页面配置中有效，无法在 app.json 中设置
    "disableScroll":  false,                   //设置为 true 则页面整体不能上下滚动；
}

```

## 逻辑层

#### 注册小程序  

- App(Object)：注册小程序，只能在app.js里面调用，且只能调用一次
```
App({
 onLaunch: function({               //小程序初始化完成时触发，全局只触发一次。
    path,                              //打开小程序的路径
    query,                             //打开小程序的query
    scene,                             //打开小程序的场景
    referrerInfo:{                     //当场景为由从另一个小程序或公众号或App打开时，返回此字段
       appId,                          //部分场景支持
       extraData,                      //数据
    },
 }) {},
 onShow: function(options) {},      //小程序启动，或从后台进入前台显示时触发。options和onLaunch一样
 onHide: function() {},             //小程序从前台进入后台时触发。
 onError: function(msg) {},
 onPageNotFound: function({         //小程序初始化完成时触发，全局只触发一次。
   path,                              //不存在页面的路径
   query,                             //打开不存在页面的query
   isEntryPage: true,                 //是否本次启动的首个页面
   }) {},    
 globalData: 'I am global data’     //自定义数据，用this可以访问。
})
```

- getApp()：获取App实例
```
    var appInstance = getApp()
    console.log(appInstance.globalData)       // I am global data
```


#### 注册页面  

- Page(Object) 
```
Page({
  data,                                     //初始化数据

  //以下为生命周期函数
  onLoad: function({                        //页面加载时触发。一个页面只会调用一次。
    query,    
    }) {},
  onShow: function(options) {},             //页面显示/切入前台时触发
  onReady: function() {},                   //初次渲染完成时触发。一个页面只会调用一次，代表页面已经准备妥当，可以和视图层进行交互。
  onHide: function(options) {},             //页面隐藏/切入后台时触发
  onUnload: function(msg) {},               //页面卸载时触发
  
  //以下为事件处理函数
  onPullDownRefresh: function() {},         //监听用户下拉刷新事件。  【wx.startPullDownRefresh，wx.stopPullDownRefresh】  
  onReachBottom: function() {},             //监听用户上拉触底事件
  onPageScroll: function({                  //页面卸载时触发
        srollTop,                               //页面在垂直方向已经滚动的距离
    }) {}, 
  onShareAppMessage: function({             //监听用户点击页面内转发按钮（<button> 组件 open-type="share"）或右上角菜单“转发”按钮的行为
        from,                                   //1, button; 2, menu
        target,                                 //  button||undefined
        webViewUrl,                             //页面中包含<web-view>组件时，返回当前<web-view>的url
  }) {
    return {
        title,                                  //转发标题
        path,                                   //转发路径
        imageUrl,                               //转发封面图片
    }
  }, 
  onTabItemTap: function({                 //点击 tab 时触发，1.9.0版本以上
        index,                                  //被点击tabItem的序号，从0开始
        pagePath,                               //  被点击tabItem的页面路径
        text,                                   //被点击tabItem的按钮文字
    }) {}, 
})
```

- Page.setData()
- Page.route


## 视图层

#### 数据绑定
```
<view> {{message}} </view>
```

#### 条件渲染 ： wx:if， wx:elif，wx:else
```
<view class='test-view test-view-if'>
  <text wx:if="{{length > 5}}"> 1 </text>
  <text wx:elif="{{length > 2}}"> 2 </text>
  <text wx:else> 3 </text>
</view>
```

#### 列表渲染
```
//默认下标： index， 当前项默认变量：item
<view wx:for="{{array}}">
  {{index}}: {{item.message}}
</view>

//使用 wx:for-item 可以指定数组当前元素的变量名，使用 wx:for-index 可以指定数组当前下标的变量名
<view wx:for="{{array}}" wx:for-index="idx" wx:for-item="itemName">
  {{idx}}: {{itemName.message}}
</view>
```


#### 模板
```
<template name="msgItem">
  <view>
    <text> {{index}}: {{msg}} </text>
    <text> Time: {{time}} </text>
  </view>
</template>

<template is="msgItem" data="{{...item}}"/>
```

#### 事件
```
<view id="tapTest" data-hi="WeChat" bindtap="tapName"> Click me! </view>

<view id="tapTest" data-hi="WeChat” bind:tap="tapName"> Click me! </view>
```

1. bind：不阻止冒泡
2. catch： 阻止冒泡


#### 引用

import：可以使用引用文件定义的template  

`<import src="a.wxml"/>`

include：类似于将引用文件的全部代码拷贝到引用位置
```
<include src="header.wxml"/>
   <view> body </view>
<include src="footer.wxml"/>
```


#### 样式： WXSS

对css的两点扩充：
- 尺寸单位rpx
- 样式导入：
    `@import "common.wxss";`

支持以下选择器：

|选择器   |   样例   |  样例描述   |
|------ |---------|---------------|
|.class     |.intro      |  选择所有拥有 class="intro" 的组件  |
| #id       |#firstname  |  选择拥有 id="firstname" 的组件     |
| element   |view        |  选择所有 view 组件                |
| element, element       |view, checkbox |  选择所有文档的 view 组件和所有的 checkbox 组件      |
| ::after   |view::after        |  在 view 组件后边插入内容                |
| ::before   |view::before        |         在 view 组件前面边插入内容       |



#### wxs 

- wxs标签

|属性名|	类型	|说明|
|-----|------|---|
|module	|String	|	当前 <wxs> 标签的模块名。必填字段。
|src	|String	|	引用 .wxs 文件的相对路径。仅当本标签为单闭合标签或标签的内容为空时有效。

- .wxs 文件

wxml 通过wxs标签获取； wxs文件通过require 获取

## 自定义组件

#### 组件规则
1. 类似于页面，一个自定义组件由 json wxml wxss js 4个文件组成
2.  json 文件中进行自定义组件声明： component: true
3. 使用Component() 注册组件


#### 使用组件
```
{
  "usingComponents": {
    "component-tag-name": "path/to/the/custom/component"
  }
}
```

- slot 
- 向组件传递数据 
- 组件事件： triggerEvent()