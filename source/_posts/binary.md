---
title: 前端文件及二进制相关
date: 2020-08-05
author: leonliu
category: js 基础
tags: 
- 浏览器
---

## 关系图
![关系图](/Blog/images/assets/binary.jpg)
<!--more-->

## FileReader API
FileReader 对象允许Web应用程序异步读取存储在用户计算机上的文件（或原始数据缓冲区）的内容，使用 File 或 Blob 对象指定要读取的文件或数据。

其中File对象可以是来自用户在一个input元素上选择文件后返回的FileList对象,也可以来自拖放操作生成的 DataTransfer对象,还可以是来自在一个HTMLCanvasElement上执行mozGetAsFile()方法后返回结果。

重要提示： FileReader仅用于以安全的方式从用户（远程）系统读取文件内容 它不能用于从文件系统中按路径名简单地读取文件。 要在JavaScript中按路径名读取文件，应使用标准Ajax解决方案进行服务器端文件读取，如果读取跨域，则使用CORS权限。

[FileReader兼容性](https://www.caniuse.com/#search=FileReader)

[FileReader API](https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader)

[FileReader 实例](http://jsrun.net/7WLKp/edit)

## URL API
URL.createObjectURL() 静态方法会创建一个 DOMString，其中包含一个表示参数中给出的对象的URL。这个 URL 的生命周期和创建它的窗口中的 document 绑定。这个新的URL 对象表示指定的 File 对象或 Blob 对象。

[URL.createObjectURL()](https://developer.mozilla.org/zh-CN/docs/Web/API/URL/createObjectURL)

```
/**
 *  object
 *  用于创建 URL 的 File 对象、Blob 对象或者 MediaSource 对象。​
**/
var objectURL = URL.createObjectURL(object);
```

URL.revokeObjectURL() 静态方法用来释放一个之前已经存在的、通过调用 URL.createObjectURL() 创建的 URL 对象。当你结束使用某个 URL 对象之后，应该通过调用这个方法来让浏览器知道不用在内存中继续保留对这个文件的引用了。

你可以在 sourceopen 被处理之后的任何时候调用 revokeObjectURL()。这是因为 createObjectURL() 仅仅意味着将一个媒体元素的 src 属性关联到一个 MediaSource 对象上去。调用revokeObjectURL() 使这个潜在的对象回到原来的地方，允许平台在合适的时机进行垃圾收集。

[URL.revokeObjectURL()](https://developer.mozilla.org/zh-CN/docs/Web/API/URL/revokeObjectURL)

```
/**
 *  objectURL
 *  一个 DOMString，表示通过调用 URL.createObjectURL() 方法产生的 URL 对象
**/
URL.revokeObjectURL(objectURL);
```

## Blob API
Blob 对象表示一个不可变、原始数据的类文件对象。Blob 表示的不一定是JavaScript原生格式的数据。File 接口基于Blob，继承了 blob 的功能并将其扩展使其支持用户系统上的文件。

要从其他非blob对象和数据构造一个 Blob，请使用 Blob() 构造函数。要创建一个 blob 数据的子集 blob，请使用 slice() 方法。要获取用户文件系统上的文件对应的 Blob 对象，请参阅 File 文档。

接受 Blob 对象的API也被列在 File 文档中。

[Blob API](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob)

### Blob 构造函数
```
var aBlob = new Blob( array, options );
```
- array 是一个由ArrayBuffer, ArrayBufferView, Blob, DOMString 等对象构成的 Array ，或者其他类似对象的混合体，它将会被放进 Blob。DOMStrings会被编码为UTF-8。
- options 是一个可选的BlobPropertyBag字典，它可能会指定如下两个属性：
    - type，默认值为 ""，它代表了将会被放入到blob中的数组内容的MIME类型。
    -   endings，默认值为"transparent"，用于指定包含行结束符\n的字符串如何被写入。 它是以下两个值中的一个： "native"，代表行结束符会被更改为适合宿主操作系统文件系统的换行符，或者 "transparent"，代表会保持blob中保存的结束符不变

### Blob 对象属性

- size 只读
Blob 对象中所包含数据的大小（字节）。
- type 只读
一个字符串，表明该 Blob 对象所包含数据的 MIME 类型。如果类型未知，则该值为空字符串。

### Blob 方法

- Blob.slice([start[, end[, contentType]]])
返回一个新的 Blob 对象，包含了源 Blob 对象中指定范围内的数据。
- Blob.stream()
返回一个能读取blob内容的 ReadableStream。
- Blob.text()
返回一个promise且包含blob所有内容的UTF-8格式的 USVString。
- Blob.arrayBuffer()
返回一个promise且包含blob所有内容的二进制格式的 ArrayBuffer 

[Blob实例](http://jsrun.net/z2LKp/edit)


## ArrayBuffer
ArrayBuffer 对象用来表示通用的、固定长度的原始二进制数据缓冲区。

它是一个字节数组，通常在其他语言中称为“byte array”。

你不能直接操作 ArrayBuffer 的内容，而是要通过类型数组对象或 DataView 对象来操作，它们会将缓冲区中的数据表示为特定的格式，并通过这些格式来读写缓冲区的内容。

### 语法
new ArrayBuffer(length)

- length
  要创建的 ArrayBuffer 的大小，单位为字节。

[ArrayBuffer API](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)

### TypeArray
一个类型化数组（TypedArray）对象描述了一个底层的二进制数据缓冲区（binary data buffer）的一个类数组视图（view）。事实上，没有名为 TypedArray 的全局属性，也没有一个名为 TypedArray 的构造函数。相反，有许多不同的全局属性，它们的值是特定元素类型的类型化数组构造函数，如下所示。在下面的页面中，你会发现一些，与包含任何类型的元素的任意类型化数组一起使用的通用属性和方法。

```
// 下面代码是语法格式，不能直接运行，
// TypedArray 关键字需要替换为底部列出的构造函数。
new TypedArray(); // ES2017中新增
new TypedArray(length); 
new TypedArray(typedArray); 
new TypedArray(object); 
new TypedArray(buffer [, byteOffset [, length]]); 

// TypedArray 指的是以下的其中之一： 

Int8Array(); 
Uint8Array(); 
Uint8ClampedArray();
Int16Array(); 
Uint16Array();
Int32Array(); 
Uint32Array(); 
Float32Array(); 
Float64Array();
```

[TypedArray API](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/TypedArray)

[DataView API](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/DataView)

```
// 使用标准数组语法来获取和设置属性值
var int16 = new Int16Array(2);
int16[0] = 42;
console.log(int16[0]); // 42

// 原型中添加的属性访问不到（此时索引值未超边界，20 < 32）
Int8Array.prototype[20] = "foo";
(new Int8Array(32))[20]; // 0

// 即使索引值超出了边界也一样不能访问（20 > 8）
Int8Array.prototype[20] = "foo";
(new Int8Array(8))[20]; // undefined

// 使用负数索引也不行
Int8Array.prototype[-1] = "foo";
(new Int8Array(8))[-1]; // undefined

// 但是可以使用命名属性的方式访问到
Int8Array.prototype.foo = "bar";
(new Int8Array(32)).foo; // "bar"
```

## Fetch API Response
[Fetch API Response](https://developer.mozilla.org/zh-CN/docs/Web/API/Response)

## WebRTC
[WebRTC](https://developer.mozilla.org/zh-CN/docs/WebRTC)
[MediaSource](https://w3c.github.io/media-source/)
[MediaStream](https://w3c.github.io/mediacapture-main/#mediastream)
[WebRTC samples](https://webrtc.github.io/samples/)

## Canvas绘制播放器
[Canvas播放器](http://jsrun.net/VwLKp/edit)