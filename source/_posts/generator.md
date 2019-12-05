---
title: 生成器基础和扩展
date: 2018-11-11
author: leonliu
category: JS
tags: 
- 生成器
---
## 生成器基础和扩展
<!--more-->
### 可迭代协议和迭代器协议
#### 可迭代协议
可迭代协议允许 JavaScript 对象去定义或定制它们的迭代行为, 例如（定义）在一个 for..of 结构中什么值可以被循环（得到）。一些内置类型都是内置的可迭代对象并且有默认的迭代行为, 比如 Array or Map, 另一些类型则不是 (比如Object) 。

为了变成可迭代对象， 一个对象必须实现 @@iterator 方法, 意思是这个对象（或者它原型链 prototype chain 上的某个对象）必须有一个名字是 Symbol.iterator 的属性:

属性 | 	值
---|---
[Symbol.iterator] | 返回一个对象的无参函数，被返回对象符合迭代器协议。

当一个对象需要被迭代的时候（比如开始用于一个for..of循环中），它的@@iterator方法被调用并且无参数，然后返回一个用于在迭代中获得值的迭代器。

#### 迭代器协议
该迭代器协议定义了一种标准的方式来产生一个有限或无限序列的值。

当一个对象被认为是一个迭代器时，它实现了一个 next() 的方法并且拥有以下含义：

- 属性: next
- 值：返回一个对象的无参函数，被返回对象拥有两个属性：
    - done (boolean)
        - 如果迭代器已经经过了被迭代序列时为 true。这时 value 可能描述了该迭代器的返回值。返回值在这里有更多解释。
        - 如果迭代器可以产生序列中的下一个值，则为 false。这等效于连同 done 属性也不指定。
    - value - 迭代器返回的任何 JavaScript 值。done 为 true 时可省略。 

### 迭代器
它是一种接口，为各种不同的数据结构提供统一的访问机制。

Iterator 的作用有三个：一是为各种数据结构，提供一个统一的、简便的访问接口；二是使得数据结构的成员能够按某种次序排列；三是 ES6 创造了一种新的遍历命令for...of循环，Iterator 接口主要供for...of消费。

ES6 规定，默认的 Iterator 接口部署在数据结构的Symbol.iterator属性，或者说，一个数据结构只要具有Symbol.iterator属性，就可以认为是“可遍历的”（iterable）。
该迭代器可以被 for...of 循环使用。

原生具备 Iterator 接口的数据结构如下：

- Array
- Map
- Set
- String
- TypedArray
- 函数的 arguments 对象
- NodeList 对象

#### 创建自定义迭代器

```
var myIterable = {
    *[Symbol.iterator] (){
        yield 1;
        yield 2;
        yield 3;
    }
}
console.log([...myIterable]);
for(let i of myIterable){
    console.log(i);
}
```
[Symbol.iterator迭代器代码示例](https://jsrun.net/RehKp/edit)

#### 使用场合
1. 结构赋值：
    对数组和 Set 结构进行解构赋值时，会默认调用Symbol.iterator方法。

```
let set = new Set().add('a').add('b').add('c');

let [x,y] = set;
// x='a'; y='b'

let [first, ...rest] = set;
// first='a'; rest=['b','c'];
```

2. spread运算符（...）：
    spread运算符（...）也会调用默认的 Iterator 接口。

```
// 例一
var str = 'hello';
[...str] //  ['h','e','l','l','o']

// 例二
let arr = ['b', 'c'];
['a', ...arr, 'd']
// ['a', 'b', 'c', 'd']
```

3. yield*
    
```
let generator = function* () {
  yield 1;
  yield* [2,3,4];
  yield 5;
};

var iterator = generator();

iterator.next() // { value: 1, done: false }
iterator.next() // { value: 2, done: false }
iterator.next() // { value: 3, done: false }
iterator.next() // { value: 4, done: false }
iterator.next() // { value: 5, done: false }
iterator.next() // { value: undefined, done: true }
```

4. 其他场合
- for...of
- Array.from()
- Map(), Set(), WeakMap(), WeakSet()（比如new Map([['a',1],['b',2]])）
- Promise.all()
- Promise.race()


### 生成器
生成器对象是由一个 generator function 返回的,并且它符合可迭代协议和迭代器协议。

#### 语法
```
function *gen() { 
  yield 1;
  yield 2;
  yield 3;
}

let g = gen(); 
// "Generator { }"
```
#### 方法
- Generator.prototype.next()：返回一个由 yield表达式生成的值。
- Generator.prototype.return()：返回给定的值并结束生成器。
- Generator.prototype.throw()： 向生成器抛出一个错误。

#### next()
next() 方法返回一个包含属性 done 和 value 的对象。该方法也可以通过接受一个参数用以向生成器传值。

```
gen.next(value)
```

- 参数value: 向生成器传递的值。
- 返回值： 
    - done(Boolean): 
        - 当迭代器遍历到迭代序列末端时返回值 true。此时，迭代器可以将返回值作为 value。
        - 当迭代器仍可继续在迭代序列中向前遍历时返回值 false。这相当于不指定 done 属性。
    - value: 迭代器返回的任意的Javascript值。当 done 的值为 true 时可以忽略该值。

#### return()
return() 方法返回给定的值并结束生成器。

```
gen.return(value)
```

- value: 需要返回的值
- 返回值：{ value, done: true }

#### throw()
throw() 方法用来向生成器抛出异常，并恢复生成器的执行，返回带有 done 及 value 两个属性的对象。


```
gen.throw(exception)
```

- exception：用于抛出的异常
- 返回值：
    - done (boolean)：
        - 如果迭代器已经返回了迭代序列的末尾，则值为 true。在这种情况下，可以指定迭代器 value 的返回值。
        - 如果迭代能够继续生产在序列中的下一个值，则值为 false。 这相当与不指定 done 属性的值。
    - value - 迭代器返回的任何 JavaScript 值。当 done 是 true 的时候可以省略。

### 生成器函数
function* 这种声明方式(function关键字后跟一个星号）会定义一个生成器函数 (generator function)，它返回一个  Generator  对象。

#### 语法

```
function *name([param[, param[, ... param]]]) { statements }

或者

new GeneratorFunction ([arg1[, arg2[, ...argN]],] functionBody)
// arg1, arg2, ... argN: 参数 
// 函数使用的名称作为形式参数名称。
// 每个必须是一个字符串，
// 对应于一个有效的JavaScript标识符或这样的字符串的列表，
// 用逗号分隔；如“x”，“theValue”或“a,b”。


// functionBody: 一个包含多条表示JavaScript函数体语句的字符串

// 注意：GeneratorFunction并不是一个全局对象，通过：
// Object.getPrototypeOf(function*(){}).constructor获取
```

#### 描述
1. 生成器函数在执行时能暂停，后面又能从暂停处继续执行。
2. 调用一个生成器函数并不会马上执行它里面的语句，而是返回一个这个生成器的迭代器（iterator）对象。
3. 当这个迭代器的 next()方法被首次（后续）调用时，其内的语句会执行到第一个（后续）出现yield的位置为止，yield 后紧跟迭代器要返回的值。或者如果用的是 yield*（多了个星号），则表示将执行权移交给另一个生成器函数（当前生成器暂停执行）
4. next()方法返回一个对象，这个对象包含两个属性：value 和 done，value 属性表示本次 yield 表达式的返回值，done 属性为布尔类型，表示生成器后续是否还有 yield 语句，即生成器函数是否已经执行完毕并返回
5. 调用 next()方法时，如果传入了参数，那么这个参数会作为上一条执行的  yield 语句的返回值

[generator 声明方式](https://jsrun.net/nehKp/edit)

### 生成器委托
yield* 表达式用于委托给另一个generator 或可迭代对象

#### 语法

```
yield* [[expression]];
```
- expression： 返回一个可迭代对象的表达式。

#### 描述
- yield* 表达式迭代操作数，并产生它返回的每个值。
- yield* 表达式本身的值是当迭代器关闭时返回的值（即done为true时）。

[生成器委托](https://jsrun.net/pQhKp/edit)

[生成器委托传入值](https://jsrun.net/iQhKp/edit)

[生成器委托中含return](https://jsrun.net/qQhKp/edit)

[生成器委托throw](https://jsrun.net/ZQhKp/edit)

### 高级用法
#### 1.生成器的传入值与传出值

```
function *foo(x) {
    var y = 2 * (yield (x + 1));
    var z = yield (y / 3);
    return (x + y + z);
}

var it = foo( 5 );
console.log( it.next() );       // { value:6, done:false }
console.log( it.next( 12 ) );   // { value:8, done:false }
console.log( it.next( 13 ) );   // { value:42, done:true }
```

#### 2.错误处理

```
function *foo(x){
  try{
    var a = yield x;
    console.log('a:', a);
  } catch(e) {
    console.log('err', e);      
  }
}

var gen = foo(3);
gen.next();
gen.throw('ops!');
```


[生成器的传入值与传出值](https://jsrun.net/YQhKp/edit)

#### 3.生成器自执行器

```
function run(genFuc, initialValue) {
  const gen = genFuc(initialValue);
  iterate(gen);

  function iterate(gen) {
    step();
    function step(arg, isError) {
      const {value: express, done} = isError ? gen.throw(arg) : gen.next(arg); 
      let response;
      if (!done) {
        if (typeof express === 'function') {
          response = express();  
        } else {
          response = express;    
        }
        Promise.resolve(response).then(step, err => step(err, true));
      }
    }
  }
}
```

#### 4.遍历一棵二叉树

```
class Btree{
    constructor(value, left=null, right=null) {
        this.value = value;
        this.left = left;
        this.right = right;
    }

    /** 默认先序 */
    * [Symbol.iterator]() {
        yield this.value;
        if (this.left) {
            yield* this.left;
        }
        if (this.right) {
            yield* this.right;
        }
    }
    
    /** 先序遍历 */
    *preOrder() {
        yield console.log(this.value);
        if (this.left) {
            yield *this.left.preOrder();
        }
        if (this.right) {
            yield *this.right.preOrder();
        }
    }
    
    /** 中序遍历 */  
    *inOrder() {
        if(this.left){
          yield *this.left.inOrder();
        }
        yield console.log(this.value);
        if(this.right){
          yield *this.right.inOrder();
        }
    }
    
    /** 后序遍历 */   
    *postOrder() {
        if(this.left){
          yield *this.left.postOrder();
        }
        if(this.right){
          yield *this.right.postOrder();
        }
        yield console.log(this.value);
    }
}

let tree = new Btree('a',
    new Btree('b',
        new Btree('c'),
        new Btree('d')),
    new Btree('e'));

for (let x of tree) {
    console.log(x);
}
// Output: a,b,c,d,e
```
[generator实现一棵二叉树的先中后序遍历](https://jsrun.net/SehKp/edit)

#### 5.生成器的并发

[生成器的并发](https://jsrun.net/UQhKp/edit)

### async 函数
async function是什么？其实就是generator的语法糖，即generator + 自动执行器。

async function对Generator 函数的改进，体现在：
1. 内置执行器
2. 更好的语义： async 和 await语法
3. 返回值是Promise

#### 语法
```
async function name([param[, param[, ... param]]]) { statements }

或者

var name = async () => {}

或者

var AsyncFunction= Object.getPrototypeOf(async function(){}).constructor;
var asyncInstance = new AsyncFunction([arg1[, arg2[, ...argN]],] functionBody)；
```

#### 错误处理
将async 函数内部的await语句用try...catch结构包裹.

```
async f(){
  try {
    await f1();
    await f2();
    ....
  } catch(err) {
//  console.log(err);
//  或者
//  return Promise.reject(err);
//  再通过返回的Promise结果的catch方法捕获异常。
  }
}
```

### *异步迭代器
异步迭代器的next()方法返回一个{ value, done } 的 promise。

```
 const asyncIter = {
-  [Symbol.iterator]: () => {
+  [Symbol.asyncIterator]: () => {
     const items = ['h', 'e', 'l', 'l', 'o'];
     return {
-      next: () => ({
+      next: () => Promise.resolve({
         done: items.length === 0,
         value: items.shift()
       })
     }
   }
 }
```
#### for await..of
- 用来遍历异步的 Iterator 接口。
- ==for-await-of 只能在 async 函数或者 async 生成器里面使用==。

[异步遍历器](https://jsrun.net/gQhKp/edit)