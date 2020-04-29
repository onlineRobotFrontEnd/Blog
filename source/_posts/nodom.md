---
title: Nodom.js前端框架介绍
date: 2020-1-1
author: zhangzhihui
category: js framework
tags:
- js框架, MVVM
---

# Nodom介绍
<!-- more -->
## Nodom.js是什么？

NoDom是一套轻量级的MVVM框架，以模块化为基础，用于构建SPA(Single Page Application)应用，主要服务于WebApp开发。提供基于数据驱动的渲染模式，页面变化只需修改数据即可实现。

目前Nodom.js兼容ES5，不支持ie浏览器（Edge除外）

nodom官网：[NoDom-数据驱动渲染MVVM框架](http://www.nodom.org)

![特色](/Blog/images/nodom/character.png)

# 模块

## 简介

模块是Nodom的核心内容，Nodom开发的每个应用都是从模块开始，所有页面由模块组成，一个页面是一个模块，可能嵌套多个子模块。

> 模块主要包含两个部分：模版和数据
> - 模版用于基本元素的编写，数据用于对模版的渲染，其中模版分为三种方式引入:元素、模版串、模版文件。
> - 数据分为两种引入方式:数据对象和数据文件，模版文件和数据文件可以在模块初次使用时动态加载。

## 用法

```html
<!-- 基本用法 -->
<div class="root">
  我是_{ name }_，_{age}_ 岁. <br>
  是<span x-if="age>10">成年人</span>
  <span x-else>未成年人</span>
</div>
<script>
  DD.createModule({
    name: 'module1',
    el: '.root',
    data: {
      age: 10,
      name: 'nodom',
    }
  });
</script>

<!-- 文件加载 -->
<!-- 请注意配置DD.config.appPath属性，路径以相对路径给出，如DD.config.appPath='/yourapp/app/'，创建模块时templateUrl设置为view/view1.html，
调用时，NoDom会对两部分进行合并，从/yourapp/app/view/view1.html加载，请注意路径不要用多余的/。
数据需给定url完整地址，可以是一个http响应，也可以是一个json数据文件。 -->

<div class="root">
</div>
<script>
 DD.createModule({
  el:'.root',
  /*请修改dataUrl和templateUrl*/
  dataUrl:'datapath/dataname.json',
  templateUrl:'viewpath/viewname.html'
});
</script>

<!-- 模块嵌套 -->
<div class="root">
</div>
<script>
  DD.createModule({
    el: '.root',
    /*用template模版串作为模版，模块中都不使用数据*/
    template: '<div style="border:1px solid #999">这是父模块<div class="code31"></div><div class="code32"></div></div>',
    modules: [
      /*子模块1，也是采用模版串*/
      {
        template: '<div style="border:2px solid #900;margin:5px 0;">这是内部的子模块1</div>',
        el: '.code31',
      },
      /*子模块2，也是采用模版串*/
      {
        template: '<div style="border:2px solid #009">这是内部的子模块2</div>',
        el: '.code32'
      }]
  });
</script>

<!-- 模块通信 -->
<!-- 每个模块都可以通过NoDom提供消息机制与兄弟模块、父模块和子模块进行通信，主要通过broadcast方法(广播消息)和send方法(定向发送)、onReceive钩子处理收到的消息。 -->
<div class="root"></div>
<script>
  DD.createModule({
    /*给模块设置名字，方便在收到消息时针对不同模块做不同操作*/
    name: 'module1',
    el: '.mod1',
    templateUrl: 'view/tutorial/module/communication.html',
    data: { smsg: '', rmsg: '' },
    /*消息接收钩子*/
    onReceive: function (module, data) {
      this.data.rmsg = '来自' + module + '的消息：' + data.smsg;
    },
    methods: {
      /*发送消息方法，由send按钮的e-click指定*/
      sendMsg: function () {
        /*broadcast为模块方法，用来向外部发送消息*/
        this.broadcast(this.data);
      }
    },
    modules: [{
      name: 'module2',
      el: '.code41',
      data: { smsg: '', rmsg: '' },
      onReceive: function (module, data) {
        this.data.rmsg = '来自' + module + '的消息：' + data.smsg;
      },
      methods: {
        sendMsg: function () {
          this.broadcast(this.data);
        }
      }
    }, {
      name: 'module3',
      el: '.code42',
      data: { smsg: '', rmsg: '' },
      onReceive: function (module, data) {
        this.data.rmsg = '来自' + module + '的消息：' + data.smsg;
      },
      methods: {
        sendMsg: function () {
          this.broadcast(this.data);
        }
      }
    }]
  });
</script>
```

# 模型
模型是Nodom的提供者，用于管理整个模块的数据<br>
> 注意：
> 模型数据对象必须为json object，如果为数组，数组元素也必须是json object。
> view只能使用x-model指令指定的模型数据(如果没有x-model指令，则向上取第一个父view带x-model指令指定的模型数据)，不能跨x-model指令取数据。

# 表达式

Nodom中，双大括号 _{}_ 里面的内容会被解析成表达式。表达式项主要用于获取数据项，计算并渲染到DOM中。表达式支持“(”、“)”、 “*”、 “/”、 “+” 、 “-”、 “>”、 “<”、 “>=”、 “<=”、 “==”、 “===”、 “&&”、 “||” 算数逻辑运算和过滤器运算符“|”。其中过滤器运算符“|”运算法优先级仅低于括号()运算法。

```html
<div class='result code1'>
  <div>(3+4)/5的结果是:_{(3 + 4) / 5}_</div>
  <div>商品名:_{ name }_</div>
  <div>商品价格：_{ price }_</div>
  <div>商品折扣价:_{ price*discount}_</div>
  <!--引入过滤器，把计算结果转换为货币-->
  <div>商品折扣价(精确到分):_{(price * discount) | currency:¥}_</div>
  <div>生产日期是:_{ genDate| date:'yyyy-MM-dd'}_</div>
  <div>是否是低价商品:_{ price<30}_</div>
  <div>是否是低价商品并且还有折扣:_{ price<30 && discount !== undefined }_</div>
</div>
<script>
  DD.createModule({
    el: '.code1',
    data: {
      price: 20,
      discount: 0.855,   /*折扣*/
      name: '测试商品',
      genDate: (new Date()).getTime()   	/*生产日期*/
    }
  });
</script>
```

# 过滤器

过滤器以“|”来分隔待过滤内容和过滤器方法，如content|filtermethod，其中date、currency、number、tolowercase、touppercase主要用于表达式过滤，orderBy过滤器主要用于配合数组排序，select用于数组元素过滤。

```html
<div class="root">
  <!-- date -->
  <div class="time">
    <!--注意日期格式两边的单引号-->
    <div>当前日期是:_{date1|date:'yyyy/MM/dd'}_</div>
    <div>当前时间是:_{date1|date:'HH:mm:ss'}_</div>
    <div>当前日期和时间是:_{date1|date:'yyyy-MM-dd HH:mm:ss'}_</div>
  </div>
  <!-- currency -->
  <div class="currency">
    <!--默认货币为¥-->
    <div>商品价格是:_{price|currency}_</div>
    <div>商品价格是:_{price|currency:$}_</div>
  </div>
  <!-- number -->
  <div class="number">
    <div>保留3位小数:_{progress|number:3}_</div>
    <div>保留0位小数:_{progress|number:0}_</div>
  </div>
  <!-- tolowercase／touppercase -->
  <div class="lower_uppercase">
    <div>转换为小写字母:_{name|tolowercase}_</div>
    <div>转换为大写字母:_{name|touppercase}_</div>
  </div>
  <!-- orderBy -->
  <div class='orderBy'>
    升序排序
    <ul>
      <li x-repeat='rows|orderBy:name'>_{name}_'s address is _{addr}_</li>
    </ul>
    降序排序
    <ul>
      <li x-repeat='rows|orderBy:name:desc'>_{name}_'s address is _{addr}_</li>
    </ul>
  </div>
  <!-- select -->
  <div class='select'>
    <!--select结合repeat指令使用-->
    <div class='imp'>odd用法</div>
    <ul>
      <li x-repeat='rows|select:odd'>_{name}_'s address is _{addr}_</li>
    </ul>
    even用法
    <ul>
      <li x-repeat='rows|select:even'>_{name}_'s address is _{addr}_</li>
    </ul>
    range用法
    <ul>
      <li x-repeat='rows|select:range:1:3'>_{name}_'s address is _{addr}_</li>
    </ul>
    index用法
    <ul>
      <li x-repeat='rows|select:index:1:3'>_{name}_'s address is _{addr}_</li>
    </ul>
    v用法
    <ul>
      <li x-repeat="rows|select:yang">_{name}_'s address is _{addr}_</li>
    </ul>
    {prop:v}用法，这里的参数必须为正确的json串，比如yang是字符串，需在两边添加引号
    <ul>
      <li x-repeat="rows|select:{addr:'yang'}">_{name}_'s address is _{addr}_</li>
    </ul>
    func用法
    <ul>
      <li x-repeat='rows|select:func:selectArr'>_{name}_'s address is _{addr}_</li>
    </ul>
  </div>
</div>
<script>
  DD.createModule({
    el: '.root',
    data: {
      date1: (new Date()).getTime(),
      price: 15.323,
      progress: 35.89992,
      name: 'Hello world!',
      rows: [
        { name: 'yang', addr: 'chengdu' },
        { name: 'zhangs', addr: 'mianyang' },
        { name: 'NoDom', addr: 'luoyang' },
        { name: 'hello', addr: 'beijing' },
      ],
    },
    methods: {
      selectArr: function (arr) {
        var a = [];
        //过滤出name为yang的数组元素
        arr.forEach(function (item) {
          if (item.name === 'yang') {
            a.push(item);
          }
        });
        return a;
      }
    }
  });
</script>
```

# 指令

指令主要包括：model, repeat, if/else, class, show, field(双向绑定), validity(校验), router(路由), 用法是 x-指令名称，如x-model。

## model指令

model指令用于给view绑定数据，数据采用层级关系，如:需要使用数据项data1.data2.data3，可以直接使用data1.data2.data3，也可以分2层设置分别设置x-model='data1'，x-model='data2'，然后使用数据项data3。

例子: [model指令](http://www.nodom.org/route/tutorial/dmodel)

## repeat指令

repeat指令用于给按照绑定的数组数据重复生成多个相同的view，每个view由指定数组索引对应的数据对象或数据进行渲染。使用方式为x-repeat='items|filter',其中items为json数组，filter为过滤器。

例子：[repeat指令](http://www.nodom.org/route/tutorial/drepeat)

## if/else指令

if/else指令用于进行条件渲染，如果if指令对应条件为真，则渲染该节点下的子节点，如果设置else指令，则条件为假时，渲染else指令对应节点的子节点。其中nodom不支持if...elseif,需要在else中嵌套

例子：[if/else指令](http://www.nodom.org/route/tutorial/dif)

## class指令

class指令用于按条件给view添加或移除css class。使用方式为x-class='{class1:condition1,class2:condition2,...}'，当满足condition1时，添加class1,反之则移除class1，condition2处理方式相同。配置内容需符合json格式。

例子：[class指令](http://www.nodom.org/route/tutorial/dclass)

## show指令

show指令用于显示或隐藏view，如果show对应的条件为真，则显示该view，否则隐藏该view。使用方式为x-show='condition'。

例子：[show指令](http://www.nodom.org/route/tutorial/dshow)

## field指令

field指令用于绑定form表单下的输入类型元素，如input、select、textarea等，可以实现输入元素与数据项之间的双向绑定。

> 其中：
> 单选框radio，多个radio的x-field必须设置为同一个数据项，同时需设置value属性，该属性与数据项可能选值保持一致
> 复选框checkbox，checkbox除了设置x-field外，还需要设置yes-value 和 no-value 属性，分别对应为选中时x-field对应数据项的值和未选中时的值。
> 下拉列表select，option可以由给定数据用repeat生成，select设置x-field即可。

例子：[field指令](http://www.nodom.org/route/tutorial/dfield)

## validity指令

validity指令用于form表单的数据项校验，该指令对应的view必须放置于form元素下才能正常工作，使用方式为x-validity='fieldname',fieldname对应输入框的name属性，表示针对该输入框进行校验，仅支持html5规范中支持的校验规则，包括required、min、max、pattern、type。<br>
使用该指令包，系统会自动生成DD.$validity对象，DD.$validity.check()方法可用于检测对应的form校验是否通过。

例子：[validity指令](http://www.nodom.org/route/tutorial/dvalidity)

## router指令

路由用于管理模块的加载模块和模块间的切换，类似于（但不限于）一个超链接操作后执行页面切换。目前仅支持html5的pushstate和popstate方法，所以路由的支持需要浏览器支持html5。

> 浏览器刷新
> > 路由切换通过pushstate修改浏览器地址，如www.yourdomain.com/route1/xxx，而你的网站不存在此资源，这个时候进行刷新，服务器会返回404错误，为了服务器能正常返回，可以在服务器配置404错误跳转页面，请参考各应用服务器配置说明。为解决该问题，需要在页面中得到服务器返回的路由路径，并调用DD.Router.start方法进行路由跳转
>
> 参数路由
> > 路由可以带参数进行传递,以“/:参数名”方式进行定义，如/path/:param1/:param2，使用时x-route='/path/:v1/:v2'，这样在当前模块可以使用$route.data['param1'] 得到v1。
>
> 路由嵌套
>> 路由设置子路由，在设置x-route指令时，需要从根路由到子路由的每一级路径合并在一起。如父路由r1路径为“/route1”，r1的子路由r2路径为“/route2”,r2的子路由r3的路径为“/route3”，则x-route='/route1/route2/route3'才能访问到路由r3，加载方式为，先加载并渲染r1对应的模块，然后加载并渲染r2对应的模块，最后加载并渲染r3对应的模块。
>
> 切换效果设置
>> 路由切换支持动画效果，NoDom支持左右滑动的切换效果，需在路由使用前设置DD.Router.switch.style='slide'，该配置项设置路由切换效果为滑动，默认为none，DD.Router.switch.switcType='0.5s'，该配置为滑动时长为0.5秒，默认为1s。
>
> 路由创建
>> 可通过DD.createRoute(config)创建一个或多个路由对象。config可以为一个参数对象，返回创建的路由，也可以为参数对象数组，无返回。参数对象配置参考配置对象参数说明。

```html
<div>
  <div class="root">当前时间:_{date1|date:'yyyy/MM/dd'}_</div>
  <a x-route='/router' x-class="{cls1:'page1'}" active='_{page1}_'>page1</a>
  <div x-router></div>
</div>
<script>
  DD.config.appPath = '/examples/route/pages/';
  DD.config.routerPrePath = '/route';
  DD.createModule({
    name: 'mainModule',
    el: '.root',
    root: true,
    data: {
      page1: true,
      page2: false,
      date1: (new Date()).getTime(),
      x: {
        y: {
          z: 1
        }
      }
    },
    methods: {

    }
  });


  DD.createModule([{
    name: 'tdir_router',
    templateUrl: '/router/router.html',
    data: {
      routes: [{
        title: '路由用法1-基本用法',
        path: '/router/route1',
        active: true
      },
      {
        title: '路由用法2-路由参数用法',
        path: '/router/directive/route2',
        active: false
      },
      {
        title: '路由用法3-路由嵌套用法',
        path: '/router/route3',
        active: false
      }
      ]
    },
    delayInit: true,
  }, {
    name: 'r_pmod1',
    templateUrl: 'router/router1.html',
    data: {
      home: true,
      list: false,
      data: false
    },
    methods: {
      onFirstRender: function () {
        // console.log(this);
      }
    }
  }, {
    name: 'r_pmod2',
    templateUrl: 'router/router2.html',
    data: {
      routes: [{
        title: '首页',
        path: '/router/directive/route2/rparam/home/1',
        active: true
      },
      {
        title: '列表',
        path: '/router/directive/route2/rparam/list/2',
        active: false
      },
      {
        title: '数据',
        path: '/router/directive/route2/rparam/data/3',
        active: false
      }
      ]
    }
  }, {
    name: 'r_pmod3',
    templateUrl: 'router/router3.html'
  }, {
    name: 'r_mod1',
    template: "<div>这是首页,路径是_{$route.path}_</div>"
  }, {
    name: 'r_mod2',
    template: "<div>这是商品列表页,路径是_{$route.path}_</div>"
  }, {
    name: 'r_mod3',
    template: "<div>这是数据页,路径是_{$route.path}_</div>"
  }, {
    name: 'r_mod4',
    template: "<div test='1'>这是_{$route.data.page}_页,编号是_{$route.data.id}_</div>"
  }, {
    name: 'r_mod5',
    template: "<div class='code1'>路由r1加载的模块<dir x-router></div></div>"
  }, {
    name: 'r_mod6',
    template: '路由r2加载的模块'
  }]);

  DD.createRoute({
    path: '/router',
    module: 'tdir_router',
    routes: [{
      path: '/route1',
      module: 'r_pmod1',
      routes: [{
        path: '/home',
        module: 'r_mod1',
        useParentPath: true
      }, {
        path: '/list',
        module: 'r_mod2',
        useParentPath: true
      }, {
        path: '/data',
        module: 'r_mod3',
        useParentPath: true
      }],
      onLeave: function (model) {
        // console.log(this,model);
      }
    }, {
      path: '/directive/route2',
      module: 'r_pmod2',
      onEnter: function () {
        // console.log('route2');
      },
      routes: [{
        path: '/rparam/:page/:id',
        module: 'r_mod4',
        onEnter: function () {
          // console.log('route2/rparam');
        }
      }]
    }, {
      path: '/route3',
      module: 'r_pmod3',
      routes: [{
        path: '/r1',
        module: 'r_mod5',
        routes: [{
          path: '/r2',
          module: 'r_mod6'
        }]
      }]
    }]
  });
</script>
```

# event

NoDom提供了专门的事件类DD.Event，用于处理view的事件操作。类似于指令用法，事件用e-开头，如e-click，e-touchstart等，事件支持所有的html元素标准事件。事件处理方法必须在模块的methods中定义，事件方法会自带三个参数 event(事件)、viewdata(触发事件的view对应的数据对象)、view(视图)，this指向model(模型)。

NoDom提供了触屏操作事件，包括tap(点击)、swipeleft(左滑)、swiperight(右滑)、swipeup(上滑)、swipedown(下滑)。

NoDom支持delg(事件代理)、nopopo(禁止冒泡)、once(单次执行)配置。

```html
<div class='result code1'>
  <div class='colorimp'>点击后查看控制台输出内容</div>
  <button e-click='clickdiv'>
    点击我试试
  </button>
  <div class='colorimp'>点击下面的商品，查看控制台输出内容。</div>
  <ul>
    <!--这儿做了事件代理，事件会注册到ul元素上-->
    <li x-repeat='datas'  e-click='clickli:delg'>
        _{name}_ 的价格是_{price}_,折扣是_{discount}_。
    </li>
  </ul>
</div>
<script>
  DD.createModule({
    el: '.code1',
    data: {
      datas: [
        { name: '酷炫夹克', price: 200, discount: 0.6 },
        { name: '运动棉袜', price: 8, discount: 0.9 },
        { name: '钥匙扣', price: 15, discount: 0.7 }
      ]
    },
    methods: {
      clickdiv: function (e, data, view) {
        console.log(e, data, view);
      },
      clickli: function (e, data, view) {
        console.log(e, data, view);
      }
    }
  });
</script>
```

# API

详见官网API，[Nodom API](http://www.nodom.org/route/api/content/module/ddmodulecls)

