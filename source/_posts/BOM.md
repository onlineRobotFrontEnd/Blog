---
title: BOM（Browser Object Model）浏览器对象模型
date: 2019-3-21
author: vivizhou0596
category: js 基础
tags: 
    - js基础, -BOM, -浏览器
---

# 1.定义
## 1.1 BOM是什么？
   BOM（Browser Object Model）即浏览器对象模型。
   BOM提供了独立于内容 而与浏览器窗口进行交互的对象,其核心对象是window；
  BOM由一系列相关的对象构成，并且每个对象都提供了很多方法与属性；
  BOM缺乏标准，JavaScript语法的标准化组织是ECMA，DOM的标准化组织是W3C，BOM最初是Netscape浏览器标准的一部分。W3C 为了把浏览器中JavaScript 最基本的部分标准化，已经将BOM的主要方面纳入了HTML5 的规范中。
  <!--more-->
  ---
## 1.2 BOM包含什么？

![avatar](https://p0.meituan.net/dpnewvc/dd20ddbf2469b3c35ea046e2d3d31145162372.jpg)

# 2.window对象
## 2.1 全局作用域
BOM的核心对象是window，它表示浏览器的一个实例。在浏览器中，window对象有双重角色，它既是通过javascript访问浏览器窗口的一个接口，又是ECMAScript规定的Global对象。

因此，所有全局作用域中声明的变量、函数都会变成window对象的属性和方法。
```aidl
   var age=26;//这里定义的全局变量和全局函数被自动归在了window对象名下
  function sayAge(){
    console.log(this.age);
  }
  console.log(window.age);//26
  sayAge();//26 相当于window.sayAge()
  window.sayAge();//26
 
  //全局变量和在window对象上直接定义属性的唯一区别：全局变量不能够通过delete操作符删除，而直接在window对象上定义的属性可以
  window.color='red';
  delete window.age;
  delete window.color;
  console.log(window.age);//26
  console.log(window.color);//undefined
```

{% raw %}
<iframe height="265" style="width: 100%;" scrolling="no" title="ErrdKK" src="//codepen.io/vivizhou0596/embed/ErrdKK/?height=265&theme-id=0&default-tab=js,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/vivizhou0596/pen/ErrdKK/'>ErrdKK</a> by vivizhou0596
  (<a href='https://codepen.io/vivizhou0596'>@vivizhou0596</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
{% endraw %}

```aidl
    /*
    还要注意：尝试访问未声明的变量会抛出错误，但是通过查询window对象，可以知道某个可能未经声明的变量是否存在
     */
    //这会抛出错误，因为oldValue未定义
    var newValue=oldValue;
    //这不会抛出错误，因为是一次属性查询
    var newValue=window.oldValue;

```
## 2.2 窗口关系及框架

如果页面中包含框架，则每个框架都拥有自己的window对象，并且保存在frames集合中。在frames集合中，可以通过数值索引(从0开始，从左到右，从上到下)或者框架名称来访问相应的window对象。每个window对象都有一个name属性，其中包含着框架的名称。

可以通过window.frames[0]或者window.frames[“topFrame”]来引用上方的框架。不过，最好使用top，而不是window来引用这些框架。因为，top对象始终指向最高(最外)层的框架，也就是浏览器窗口。使用它可以确保在一个框架中正确地访问另一个框架。因为对于一个在框架中编写的任何代码来说，其中的window对象指向的都是那个框架的特定实例，而不是最高层的框架。

与top相对的另一个window对象是parent。parent对象始终指向当前框架的直接上层框架。

与框架有关的最后一个对象是self，它始终指向window。self和window对象可以互换使用。

在使用框架的情况下，浏览器中会存在多个Global对象。在每个框架中定义的全局变量会自动成为框架中window对象的属性。由于每个window对象都包含原生类型的构造函数，因此每个框架都有一套自己的构造函数，这些构造函数一一对应，但并不相等。

① 如果文档包含框架（frame 或iframe标签），浏览器会为HTML文档创建一个window对象，并为每个框架创建一个额外的window对象。

② window.frames 返回窗口中所有命名的框架

③parent是父窗口（如果窗口是顶级窗口，那么parent==self==top）；

top是最顶级父窗口（有的窗口中套了好几层frameset或者iframe）；

self是当前窗口（等价window）；

opener是用open方法打开当前窗口的那个窗口；

## 2.3窗口位置与大小
### 2.3.1窗口位置
窗口位置：窗口相对于屏幕左边和上边的位置
screenLeft和screenTop属性：IE、Safari、Opera、Chrome
screenX和screenY属性：Firefox、Safari、Chrome

在IE、Opera中，screenLeft和screenTop中保存 的是从屏幕左边和上边到由window对象表示的页面可见区域的距离 
在Chrome、Firefox和Safari中，screenY或screenTop中保存的是整个浏览器窗口相对于屏幕的坐标值，即在窗口的y轴坐标为0时返回0。

```
var leftPos = (typeof window.screenLeft === 'number') ? window.screenLeft : window.screenX;

var rightPos = (typeof window.screenTop === 'number') ? window.screenTop : window.screenY;
```
### 2.3.1窗口大小
跨浏览器确定一个窗口的大小不是一件简单的事。IE9+、Firefox、Safari、Opera 和Chrome 均为此提供了4 个属性：innerWidth、innerHeight、outerWidth 和outerHeight。
红宝书《JavaScript高级程序设计》上对这几个属性的描述如下：

```aidl
 在IE9+、 Safari 和 Firefox、Opera中， outerWidth 和outerHeight 返回浏览器窗口本身的尺寸，而 innerWidth 和 innerHeight则表示该容器中页面视图区的大小(减去边框宽度)。在 Chrome中相应宽高返回相同的值，即视 口( viewport)大小而非浏览器窗口大小。
```
随手在windows上的Chrome上测试了一下，发现在并不如书中所述，并且在窗口处于最大化和最小化时表现也不一致，因此这些属性对于不同系统不同版本的浏览器表现可能都不一致，不能作为精确值使用。
```aidl
 var pageWidth=window.innerWidth,
        pageHeight=window.innerHeight,
        windowWdith=window.outerWidth,
        windowHeight=window.outerHeight;
    document.write("innerWidth="+pageWidth+"&emsp;&emsp;");
    document.write("innerHeight="+pageHeight+"<br />");
    document.write("outerWidth="+windowWdith+"&emsp;&emsp;");
    document.write("outerHeight="+windowHeight);
```
![avatar](https://p1.meituan.net/dpnewvc/c7a6ca2873212f7bc2312a15d3e7996e78717.png)

## 2.4超时调用和间歇调用(定时器)
javascript是单线程语言，但允许通过设置超时值和间歇值来设定代码在特定时刻执行

超时调用（执行一次）：是在指定的时间过后执行代码

间歇调用（重复执行）：每隔指定的时间就执行一次代码

超时调用：需要使用window对象的setTimeout()方法，接收两个参数：要执行的代码和以毫秒表示的时间。

第二个参数是一个表示等待多长时间的毫秒数，但经过该时间后指定的代码不一定执行。因为，javascript是一个单线程的解释器，因此一定时间内只能执行一段代码。第二个参数表示再过多长时间把当前任务添加到队列中。如果队列是空的，则代码会立刻执行，否则就要等待前面的代码执行完了以后再执行。

调用setTimeout()后，该方法会返回一个数值ID,表示超时调用。要取消未执行的超时调用计划，可以调用clearTimeout()方法并将相应的超时调用ID作为参数传递给它即可。

间歇调用：使用setInterval()方法

与超时调用类似，只不过它会按照指定的时间间隔重复执行代码，直到间歇调用被取消或者页面被卸载。它接收的参数与setTimeout()方法一样


**demo1** 
```aidl
  //设置超时调用
 var timeoutId = setTimeout(function() {
   alert("Hello world!");
 }, 1000);
 //取消超时调用
 clearTimeout(timeoutId);
```
**demo2** 
```aidl
    var num = 0;
    var max = 10;
    var intervalId = null;
    function incrementNumber() {
      console.log(num++);
      if (num == max) {
        clearInterval(intervalId);
        alert("Done");
      }
    }
    intervalId = setInterval(incrementNumber, 500);
```
**demo3** 
```aidl
 /*
  使用超时调用来实现
   */
    var num = 0;
    var max = 100;
    function incrementNumber() {
      num++;
      if (num < max) {
        setTimeout(incrementNumber, 500);
      } else {
        alert("Done");
      }
    }
    setTimeout(incrementNumber, 500);
```
在使用超时调用时，没有必要跟踪超时调用ID，因为每次执行代码之后，如果不再设置另一次超时调用，调用就会自动停止。一般认为，使用超时调用来模拟间歇调用是一种最佳模式。间歇调用一般较少使用，因为后一个间歇调用可能会在前一个间歇调用结束之前启动

## 2.5系统对话框
alert()、confirm()和prompt()
浏览器通过alert()、confirm()和prompt()方法可以调用系统对话框向用户显示消息。系统对话框与在浏览器中显示的网页没有关系，也不包含HTML。它们的外观由操作系统及（或）浏览器设置决定，而不是由CSS 决定。此外，通过这几个方法打开的对话框都是同步和模态的。也就是说，显示这些对话框的时候代码会停止执行，而关掉这些对话框后代码又会恢复执行。
```aidl
    alert("Hello world!");
```
 confirm()方法用于显示一个带有指定消息和确认及取消按钮的对话框。判断用户点击了OK还是Cancel，可以检查confirm()方法返回的布尔值：true表示单击了OK，false表示单击了Cancel或单击了右上角的X按钮。

```aidl
    if (confirm("Are you sure?")) {
      alert("I'm so glad you're sure! ");
    } else {
       alert("I'm sorry to hear you're not sure. ");
    }
```
prompt()方法用来生成一个"提示"框，用于提示用户输入一些文本。提示框除了显示OK和Cancel按钮之外 ，还会显示一个文本输入域，用来输入文本内容。该方法接收两个参数：要显示给用户的文本提示和文本输入域的默认值(可以是一个空字符串)

```aidl
    var result = prompt("What is your name? ", "");
    if (result !== null) {
     alert("Welcome, " + result);
    }
```

# 3.Location对象
location对象是一个很特殊的对象，因为它既是window对象的属性，也是document对象的属性；换句话说，window.location和document.location引用的是同一个对象。location对象的用处不只表现在它保存着当前文档的信息，还表现在它将URL解析为独立的片段，让开发人员可以通过不同的属性访问这些片段。下标列出了location对象的所有属性（省略了每个属性前面的location前缀）：

|属性名|	例子	|说明|
|-----|------|---|
|hash |"#contents"| 返回URL中的hash（#号后跟零或多个字符），如果URL中不包含散列，则返回空字符串
|host |"www.wrox.com:80"| 返回服务器名称和端口号（如果有）
|hostname| "www.wrox.com" |返回不带端口号的服务器名称
|href |"http:/www.wrox.com" |返回当前加载页面的完整URL。而location对象的toString()方法也返回这个值
|pathname| "/WileyCDA/" |返回URL中的目录和（或）文件名
|port |"8080" |返回URL中指定的端口号。如果URL中不包含端口号，则这个属性返回空字符串
|protocol| "http:" |返回页面使用的协议。通常是http:或https:
|search| "?q=javascript"| 返回URL的查询字符串。这个字符串以问号开头

查询字符串参数
虽然上面的属性可以访问到location对象的大多数信息，但是其中访问URL包含的查询字符串的属性并不方便。尽管location.search返回从问号到URL末尾的所有内容，但是却没有办法逐个访问其中的每个查询字符串参数。因此可以创建一个函数，用以解析查询字符串，然后返回包含所以参数的一个对像。

```aidl
    function getQueryStringArgs(){
        //取得查询字符串并去掉开头的问号
        var qs = (location.search.length > 0 ? location.search.substring(1) : ""),
        //保存数据的对象
        args = {},
        //取得每一项
        items = qs.length ? qs.split("&") : [],
        item = null,
        name = null,
        value = null,
        //在for 循环中使用
        i = 0,
        len = items.length;
        //逐个将每一项添加到args 对象中
        for (i=0; i < len; i++){
            item = items[i].split("=");
            name = decodeURIComponent(item[0]);
            value = decodeURIComponent(item[1]);
            if (name.length) {
                args[name] = value;
            }
        }
        return args;
   }
```


## 3.1位置操作
使用location对象可以通过很多方式来改变浏览器的位置。最常用的方式就是使用
assign()方法并为它传递一个参数URL：
```aidl
    location.assign('http://www.wrox.com');
```
这样就可以打开新URL，并在浏览器的历史记录中生成一条记录。如果将location.href和window.location设置为一个URL值。也会以该值调用assign()方法。下面的两行代码的效果是一样的：
```aidl
     window.location = 'http://www.wrox.com';
    location.href = 'http://www.wrox.com';
```
最常用的是设置location.href属性。
修改location对象的其他属性也可以改变当前加载的页面：
```aidl
    //假设初始值URL为：http://www.wrox.com/WileyCDA
    //将URL修改为：http://www.wrox.com/WileyCDA/#section
    location.hash = '#section';
    //将URL修改为：http://www.wrox.com/WileyCDA/?q=javascript
    location.search = '?q=javascript';
    //将URL修改为：http://www.wrox.com/WileyCDA/
    location.hostname = 'www.wrox.com';
    //将URL修改为：http://www.wrox.com/mydir
    location.pathname = 'mydir';
    //将URL修改为：http://www.wrox.com:8080/WileyCDA/
    location.port = 8080;
    // 每次修改location的属性（hash除外）都会以新URL重新加载
```

当通过上述任何一种方式修改URL后，浏览器的历史记录中就会生成一条新记录。要禁用这种行为可以使用replace()方法，这个方法只接收一个参数，既要导航到的URL，结果虽然导致浏览器位置变化，但不在历史记录中生成新记录。在调用replace()方法后，用户不能回到前一个页面，此时后退按钮将处于禁用状态：
```aidl
    location.replace('www.wrox.com');
```
与为重有关的最后一个方法是reload()，作用是重新加载当前显示的页面。如果调研那个reload()不传递任何参数，页面就以最有效的方式重载，也就是从浏览器缓存中冲洗加载；如果想强制从服务器重新加载，则需要：
```aidl
    location.reload();       //从页面加载
    location.reload(true);   //从服务器加载
```
位于reload()方法后的代码可能会也可能不会执行，这要取决于网络延迟或系统资源等因素，因此，最好将reload()放在代码的最后一行。

# 4.Navigator对象

最早由NetscapeNavigator2.0引入的navigator对象，现在已经成为识别客户端浏览器的事实标准。虽然其他浏览器也通过其他方式提供了相同或相似的信息（例如，IE 中的window.clientInformation和Opera 中的window.opera），但navigator 对象却是所有支持JavaScript 的浏览器所共有的。与其他BOM 对象的情况一样，每个浏览器中的navigator 对象也都有一套自己的属性。

Navigator属性虽然多，但是感觉都不太实用，列出几个在项目中实际用到的东西。
 *1、navigator.appCodeName（不准确）：属性是一个只读字符串，声明了浏览器的代码名。

    在所有以 Netscape 代码为基础的浏览器中，它的值是 "Mozilla"。为了兼容起见，在 Microsoft 的浏览器中，它的值也是 "Mozilla"，同时在safari在浏览器的console里运行navigator.appCodeName得出的结果还是"Mozilla"，所以这个看起来并不实用，因为IE、chrome、safari返回的都是“Mozilla”。
 *2、navigator.appName（不准确）：返回所使用浏览器的名称。
  
    由于兼容性问题，HTML5 规范允许该属性返回 "Netscape"。该属性并不一定能返回正确的浏览器名称。在基于 Gecko 的浏览器 （例如 Firefox）和基于 WebKit 的浏览器（例如 Chrome 和 Safari）中，返回的浏览器名称都是 "Netscape"。

 *3、navigator.appVersion（已废弃）：属性可返回浏览器的平台和版本信息。

    该属性是一个只读的字符串。该特性已经从 Web 标准中删除，虽然一些浏览器目前仍然支持它，但也许会在未来的某个时间停止支持，请尽量不要使用该特性。

 *4、navigator.platform：属性是一个只读的字符串，声明了运行浏览器的操作系统和（或）硬件平台。

    可能的值有: "Win32", "Linux i686", "MacPPC", "MacIntel"等。

 *5、navigator.userAgent（用的最多，也可以说相对更准确）：属性是一个只读的字符串，声明了浏览器用于 HTTP 请求的用户代理头的值。
 
    由于是各家浏览器厂商都想要自己的浏览器被其他的兼容，所以都会或多或少的加上一些其他的信息在里面。
    
# 5.History对象
history对象记录了用户曾经浏览过的页面(URL)，并可以实现浏览器前进与后退相似导航的功能。

注意:从窗口被打开的那一刻开始记录，每个浏览器窗口、每个标签页乃至每个框架，都有自己的history对象与特定的window对象关联。

语法：

window.history.[属性|方法]
注意：window可以省略。

  **History 对象属性**

|属性 | 描述 |
|-----|------|
|length | 浏览器历史列表中的URL数量

 **History 对象方法**
 
|方法| 描述 |
|-----|------|
|back() | 加载 history 列表中的前一个 URL。
|forward() | 加载 history 列表中的下一个 URL。
|go() | 根据当前所处的页面，加载 history 列表中的某个具体的页面。

HTML5引入了histtory.pushState()和history.replaceState()这两个方法，他们允许添加和修改history实体。同时，这些方法会和window.onpostate事件一起工作。
pushState方法
pushState()有三个参数:state对象，标题(现在是被忽略，未作处理)，URL(可选)。具体细节：

- state对象 –state对象是一个JavaScript对象，它关系到由pushState()方法创建出来的新的history实体。用以存储关于你所要插入到历史 记录的条目的相关信息。State对象可以是任何Json字符串。因为firefox会使用用户的硬盘来存取state对象，这个对象的最大存储空间为640k。如果大于这个数 值，则pushState()方法会抛出一个异常。如果确实需要更多的空间来存储，请使用本地存储。

- title—firefox现在回忽略这个参数，虽然它可能将来会被使用上。而现在最安全的使用方式是传一个空字符串，以防止将来的修改。或者可以传一个简短的标题来表示state

- URL—这个参数用来传递新的history实体的URL，注意浏览器将不会在调用pushState()方法后加载这个URL。但也许会过一会尝试加载这个URL。比如在用户重启了浏览器后，新的url可以不是绝对路径。如果是相对路径，那么它会相对于现有的url。新的url必须和现有的url同域，否则pushState()将抛出异常。这个参数是选填的，如果为空，则会被置为document当前的url。

某种意义上来说，调用pushState()方法很像设置了window.location = “#foo”,这两者都会创建和激活另一个关联到当前document的history实体，但pushState()另外有一些优点：

l 如果不需要，你可以不修改url。对比而言，设置window.location = “#foo”;仅产生新的history实体，如果你当前的hash不是#foo

2 你可以将任意的数据与你的新history实体关联。使用基于hash的方法，需要将所有相关的数据编码为一个短字符串。

注意，pushState()方法不会使hashchange时间发生，即使是新旧url只是hash不同。

- replaceState()方法
history.replaceState() 用起来很像pushState()，除了replaceState()是用来修改当前的history实体而不是创建一个新的。这个方法有时会很有用，当 你需要对某些用户行为作反应而更新一个state对象或者当前history实体时，可以使用它来更新state对象或者当前history实体的url。

- popstate事件
当history实体被改变时，popstate事件将会发生。如果history实体是有pushState和replaceState方法产生的，popstate事件的state属性会包含一份来自history实体的state对象的拷贝

详见window.onpopstate

- 读取当前的state
当页面加载时，它可能会有一个非空的state对象。这可能发生在当页面设置一个state对象(使用pushState或者replaceState)之后用户重启了浏览器。当页面重新加载，页面将收到onload事件，但不会有popstate事件。然而，如果你读取history.state属性，将在popstate事件发生后得到这个state对象
var currentState = history.state;


# 6.小结
浏览器对象模型（BOM）以window 对象为依托，表示浏览器窗口以及页面可见区域。同时，window对象还是ECMAScript 中的Global 对象，因而所有全局变量和函数都是它的属性，且所有原生的构造函数及其他函数也都存在于它的命名空间下。本章讨论了下列BOM的组成部分。

- 在使用框架时，每个框架都有自己的window 对象以及所有原生构造函数及其他函数的副本。
每个框架都保存在frames 集合中，可以通过位置或通过名称来访问。
- 有一些窗口指针，可以用来引用其他框架，包括父框架。
- top 对象始终指向最外围的框架，也就是整个浏览器窗口。
- parent 对象表示包含当前框架的框架，而self 对象则回指window。
- 使用location 对象可以通过编程方式来访问浏览器的导航系统。设置相应的属性，可以逐段
或整体性地修改浏览器的URL。
- 调用replace()方法可以导航到一个新URL，同时该URL 会替换浏览器历史记录中当前显示
的页面。
- navigator 对象提供了与浏览器有关的信息。到底提供哪些信息，很大程度上取决于用户的浏
览器；不过，也有一些公共的属性（如userAgent）存在于所有浏览器中。
BOM 中还有两个对象：screen 和history，但它们的功能有限。screen 对象中保存着与客户端
显示器有关的信息，这些信息一般只用于站点分析。history 对象为访问浏览器的历史记录开了一个
小缝隙，开发人员可以据此判断历史记录的数量，也可以在历史记录中向后或向前导航到任意页面。


参考链接：
- [react-router原理](https://blog.csdn.net/qq_36223144/article/details/83247008)


