---
title: 修饰器（装饰器，注解）
date: 2018-08-30
author: ChenEnjun
category: JS
tags:
- 修饰器
---

### 修饰器（装饰器，注解）
#### 1.类的修饰

```
@testable
class MyTestableClass {
  // ...
}

function testable(target) {
  target.isTestable = true;
}

MyTestableClass.isTestable // true
```
<!--more--> 
上面代码中，@testable就是一个修饰器。它修改了MyTestableClass这个类的行为，为它加上了静态属性isTestable。testable函数的参数target是MyTestableClass类本身。

```
也就是说，修饰器是一个对类进行处理的函数。修饰器函数的第一个参数，就是所要修饰的目标类。

function testable(target) {
  // ...
}

testable函数的参数target，就是会被修饰的类。
```
如果觉得一个参数不够用，可以在修饰器外面再封装一层函数。

```
function testable(isTestable) {
  return function(target) {
    target.isTestable = isTestable;
  }
}

@testable(true)
class MyTestableClass {}
MyTestableClass.isTestable // true

@testable(false)
class MyClass {}
MyClass.isTestable // false
```


#### react-redux @connect 装饰器

实际开发中，React 与 Redux 库结合使用时，常常需要写成下面这样。
```
class MyReactComponent extends React.Component {}
export default connect(mapStateToProps, mapDispatchToProps)(MyReactComponent);
```
有了装饰器，就可以改写上面的代码。

```
@connect(mapStateToProps, mapDispatchToProps)
export default class MyReactComponent extends React.Component {}
```
相对来说，后一种写法看上去更容易理解。

#### 2.方法的修饰
修饰器不仅可以修饰类，还可以修饰类的属性。

```
class Person {
  @readonly
  name() { return `${this.first} ${this.last}` }
}
修饰器readonly用来修饰“类”的name方法。
```

修饰器函数readonly一共可以接受三个参数。

```
function readonly(target, name, descriptor){
  // descriptor对象原来的值如下
  // {
  //   value: specifiedFunction,
  //   enumerable: false,
  //   configurable: true,
  //   writable: true
  // };
  descriptor.writable = false;
  return descriptor;
}

readonly(Person.prototype, 'name', descriptor);
// 类似于
Object.defineProperty(Person.prototype, 'name', descriptor);
```

修饰器第一个参数是类的原型对象，上例是Person.prototype，修饰器的本意是要“修饰”类的实例，但是这个时候实例还没生成，所以只能去修饰原型（这不同于类的修饰，那种情况时target参数指的是类本身）；第二个参数是所要修饰的属性名，第三个参数是该属性的描述对象。

例1：修改属性描述对象的enumerable属性，使得该属性不可遍历。

```
class Person {
  @nonenumerable
  get kidCount() { return this.children.length; }
}

function nonenumerable(target, name, descriptor) {
  descriptor.enumerable = false;
  return descriptor;
}
```
例2：下面的@log修饰器，可以起到输出日志的作用。

```
class Math {
  @log
  add(a, b) {
    return a + b;
  }
}

function log(target, name, descriptor) {
  var oldValue = descriptor.value;

  descriptor.value = function() {
    console.log(`Calling ${name} with`, arguments);
    return oldValue.apply(this, arguments);
  };

  return descriptor;
}

const math = new Math();

// passed parameters should get logged now
math.add(2, 4);
```
上面代码中，@log修饰器的作用就是在执行原始的操作之前，执行一次console.log，从而达到输出日志的目的。

另外，修饰器有==注释==的作用。

```
@testable
class Person {
  @readonly
  @nonenumerable
  name() { return `${this.first} ${this.last}` }
}
```
从上面代码中，我们一眼就能看出，Person类是可测试的，而name方法是只读和不可枚举的。

#### 常见的修饰器库
##### core-decorators.js
###### （1）@autobind

autobind修饰器使得方法中的this对象，绑定原始对象。

```
import { autobind } from 'core-decorators';

class Person {
  @autobind
  getPerson() {
    return this;
  }
}

let person = new Person();
let getPerson = person.getPerson;

getPerson() === person;
// true
```
###### （2）@readonly

```
import { readonly } from 'core-decorators';

class Meal {
  @readonly
  entree = 'steak';
}

var dinner = new Meal();
dinner.entree = 'salmon';
// Cannot assign to read only property 'entree' of [object Object]
```
###### （3）@override
override修饰器检查子类的方法，是否正确覆盖了父类的同名方法，如果不正确会报错。
###### （4）@deprecate (别名@deprecated)
deprecate或deprecated修饰器在控制台显示一条警告，表示该方法将废除。

```
import { deprecate } from 'core-decorators';

class Person {
  @deprecate
  facepalm() {}

  @deprecate('We stopped facepalming')
  facepalmHard() {}

  @deprecate('We stopped facepalming', { url: 'http://knowyourmeme.com/memes/facepalm' })
  facepalmHarder() {}
}

let person = new Person();

person.facepalm();
// DEPRECATION Person#facepalm: This function will be removed in future versions.

person.facepalmHard();
// DEPRECATION Person#facepalmHard: We stopped facepalming

person.facepalmHarder();
// DEPRECATION Person#facepalmHarder: We stopped facepalming
//
//     See http://knowyourmeme.com/memes/facepalm for more details.
//
```
#### Postal.js
我们可以使用修饰器，使得对象的方法被调用时，自动发出一个事件。

```
const postal = require("postal/lib/postal.lodash");

export default function publish(topic, channel) {
  const channelName = channel || '/';
  const msgChannel = postal.channel(channelName);
  msgChannel.subscribe(topic, v => {
    console.log('频道: ', channelName);
    console.log('事件: ', topic);
    console.log('数据: ', v);
  });

  return function(target, name, descriptor) {
    const fn = descriptor.value;

    descriptor.value = function() {
      let value = fn.apply(this, arguments);
      msgChannel.publish(topic, value);
    };
  };
}
```
上面代码定义了一个名为publish的修饰器，它通过改写descriptor.value，使得原方法被调用时，会自动发出一个事件。

```
// index.js
import publish from './publish';

class FooComponent {
  @publish('foo.some.message', 'component')
  someMethod() {
    return { my: 'data' };
  }
  @publish('foo.some.other')
  anotherMethod() {
    // ...
  }
}

let foo = new FooComponent();

foo.someMethod();
foo.anotherMethod();
```
#### Mixin
在修饰器的基础上，可以实现Mixin模式。所谓Mixin模式，就是对象继承的一种替代方案，中文译为“混入”（mix in），意为在一个对象之中混入另外一个对象的方法

```
const Foo = {
  foo() { console.log('foo') }
};

class MyClass {}

Object.assign(MyClass.prototype, Foo);

let obj = new MyClass();
obj.foo() // 'foo'
```
上面代码之中，对象Foo有一个foo方法，通过Object.assign方法，可以将foo方法“混入”MyClass类，导致MyClass的实例obj对象都具有foo方法。这就是“混入”模式的一个简单实现。

我们部署一个通用脚本mixins.js，将 Mixin 写成一个修饰器。
```
export function mixins(...list) {
  return function (target) {
    Object.assign(target.prototype, ...list);
  };
}
```
然后，就可以使用上面这个修饰器，为类“混入”各种方法。

```
import { mixins } from './mixins';

const Foo = {
  foo() { console.log('foo') }
};

@mixins(Foo)
class MyClass {}

let obj = new MyClass();
obj.foo() // "foo"
```
通过mixins这个修饰器，实现了在MyClass类上面“混入”Foo对象的foo方法。

#### Trait

Trait 也是一种修饰器，效果与 Mixin 类似，但是提供更多功能，比如防止同名方法的冲突、排除混入某些方法、为混入的方法起别名等等。

以traits-decorator这个第三方模块作为例子。这个模块提供的traits修饰器，不仅可以接受对象，还可以接受 ES6 类作为参数。

```
import { traits } from 'traits-decorator';

class TFoo {
  foo() { console.log('foo') }
}

const TBar = {
  bar() { console.log('bar') }
};

@traits(TFoo, TBar)
class MyClass { }

let obj = new MyClass();
obj.foo() // foo
obj.bar() // bar
```
上面代码中，通过traits修饰器，在MyClass类上面“混入”了TFoo类的foo方法和TBar对象的bar方法。

Trait 不允许“混入”同名方法。一种解决方法是排除TBar的foo方法。

```
import { traits, excludes } from 'traits-decorator';

class TFoo {
  foo() { console.log('foo') }
}

const TBar = {
  bar() { console.log('bar') },
  foo() { console.log('foo') }
};

@traits(TFoo, TBar::excludes('foo'))
class MyClass { }

let obj = new MyClass();
obj.foo() // foo
obj.bar() // bar
```
另一种方法是为TBar的foo方法起一个别名。
```
import { traits, alias } from 'traits-decorator';

class TFoo {
  foo() { console.log('foo') }
}

const TBar = {
  bar() { console.log('bar') },
  foo() { console.log('foo') }
};

@traits(TFoo, TBar::alias({foo: 'aliasFoo'}))
class MyClass { }

let obj = new MyClass();
obj.foo() // foo
obj.aliasFoo() // foo
obj.bar() // bar
```
alias和excludes方法，可以结合起来使用。

```
@traits(TExample::excludes('foo','bar')::alias({baz:'exampleBaz'}))
class MyClass {}
或者
@traits(TExample::as({excludes:['foo', 'bar'], alias: {baz: 'exampleBaz'}}))
class MyClass {}
```
#### 安装方式

```
$ npm install babel-core babel-plugin-transform-decorators
然后，设置配置文件.babelrc
{
  "plugins": ["transform-decorators"]
}
```