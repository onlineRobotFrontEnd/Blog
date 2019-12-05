---
title: 位操作符
date: 2019-03-14
author: leonliu
category: 计算机基础
tags: 
- 计算机基础
---

## 原码, 反码, 补码
<!--more-->
### 原码（True Form）
使用高位作为符号位。最高位为0时表示正数，最高位为1时则表示为负数。其余位使用此数字数值本身二进制的绝对值表示。

**原码的设计不便于加减运算。**

### 反码（Ones' Complement）
使用高位作为符号位。最高位为0时表示正数，最高位为1时则表示为负数。正数的反码还是正数本身，负数的补码就是其绝对值相同的正数取反的结果。即在原码的基础上，符号位不变，其他位取反的结果。

**反码的设计依然不便于加减运算。**

### 补码（Twos' Complement）
使用高位作为符号位。最高位为0时表示正数，最高位为1时则表示为负数。正数的补码就是正数本身，负数的补码就是其原码取反加一的结果。补码设计的目的，就是讲将原二进制数，分一半做负数，而取反加一的规律则是在此设计的基础上归纳得来的。所以，使用“取反加一”来定义补码，是与设计相悖的。

**补码的设计，方便了二进制的加减运算。**

### 转换
- 正数：原码，反码，补码都一样。
- 负数：
    - 原码和反码的相互转换：符号位不变，数值位按位取反
    - 原码和补码的相互转换：符号位不变，数值位按位取反,末位再加1
    - 已知补码，求原码的负数的补码：符号位和数值位都取反，末位再加1


```
// 8的八位原码，反码，补码
// 0000 1000

// -8的八位原码，反码，补码
// 原：1000 1000
// 反：1111 0111
// 补：1111 1000

// 实现一个二进制类：
function Binary(num, opt){
    this.num = num;
    this.opt = opt;
    this.binary_str = num.toString(2);
}

Binary.prototype.getTrues= function(bitwise) {
    var trues = '';
    if (this.num >= 0) {
        trues = (Array(bitwise).join("0") + this.binary_str).slice(-bitwise);
    }

    if(this.num < 0){
        trues = '1' + (Array(bitwise).join("0") + this.binary_str).slice(-(bitwise - 1)).replace('-',0);
    }
    return trues;
}

Binary.prototype.getOnes =function(bitwise) {
    var ones = '';
    if (this.num >= 0) {
        ones = (Array(bitwise).join("0") + this.binary_str).slice(-bitwise);
    }

    if(this.num <= 0){
        ones = '1' + (Array(bitwise).join("0") + this.binary_str).slice(-(bitwise - 1)).replace('-',0).split('').map(bit=>bit=='0'?'1':'0').join('');
    }
    return ones;
}

Binary.prototype.getTwos =function(bitwise) {
    var twos = '',
        parse_ones_add_1 = parseInt(this.getOnes(bitwise), 2) + 1;
    if (this.num >= 0) {
        twos = (Array(bitwise).join("0") + this.binary_str).slice(-bitwise);
    }

    if(this.num <= 0){
        twos = '1'+(Array(bitwise).join("0") + parse_ones_add_1.toString(2)).slice(-(bitwise - 1)).replace('-',0);
    }
    return twos;
}

Binary.prototype.toString = function(bitwise = 32) {
   var str = 
   `
   ======
    真值: ${this.binary_str};
    原码: ${this.getTrues(bitwise)};
    反码：${this.getOnes(bitwise)};
    补码：${this.getTwos(bitwise)};
   ======
   `;
   return str;
}

Binary.prototype.valueOf = function() {
   return parseInt(this.num, 10);
}

Binary.format = function(str = '', length = 4, replaceStr = ' ') {
    var reg = new RegExp(`(\\d)(?=(\\d{${length}})+(?!\\d))`, 'gi');
    return str.replace(reg, `$&${replaceStr}`);
}

var a = new Binary(+new Binary(-11123));
var format = Binary.format;
console.log(a.toString(32));
console.log(format(a.getTrues(32)));
console.log(format(a.getOnes(32)));
console.log(format(a.getTwos(32)));
```
[在线实例：实现二进制类](http://js.jsrun.net/2dXKp/edit)

## 位操作符
### 概述
**按位操作符（Bitwise operators）** 将其操作数（operands）当作32位的比特序列（由0和1组成），而不是十进制、十六进制或八进制数值。例如，十进制数9，用二进制表示则为1001。按位操作符操作数字的二进制形式，但是返回值依然是标准的JavaScript数值。


运算符 | 用法 | 描述
---|--- | ---
按位与（ AND） | a & b | 对于每一个比特位，只有两个操作数相应的比特位都是1时，结果才为1，否则为0。
按位或（OR） | a &#124; b | 对于每一个比特位，当两个操作数相应的比特位至少有一个1时，结果为1，否则为0。
按位异或（XOR） | a ^ b | 对于每一个比特位，当两个操作数相应的比特位有且只有一个1时，结果为1，否则为0。
按位非（NOT） | ~a | 反转操作数的比特位，即0变成1，1变成0。
左移（Left shift）| a << b | 将 a 的二进制形式向左移 b (< 32) 比特位，右边用0填充。
有符号右移 | a >> b | 将 a 的二进制表示向右移 b (< 32) 位，丢弃被移出的位。
无符号右移 | a >>> b | 将 a 的二进制表示向右移 b (< 32) 位，丢弃被移出的位，并使用 0 在左侧填充。

### 有符号32位整数
所有的按位操作符的操作数都会被转成补码（two's complement）形式的有符号32位整数。补码形式是指一个数的负对应值（negative counterpart）（如 5和-5）为数值的所有比特位反转后，再加1。反转比特位即该数值进行’非‘位运算，也即该数值的反码。


## 按位逻辑操作符
从概念上讲，按位逻辑操作符按遵守下面规则：
- 操作数被转换成32位整数，用比特序列（0和1组成）表示。超过32位的数字会被丢弃。
例如, 以下具有32位以上的整数将转换为32位整数。
- 第一个操作数的每个比特位与第二个操作数的相应比特位匹配：第一位对应第一位，第二位对应第二位，以此类推。
- 位运算符应用到每对比特位，结果是新的比特值。

```
function logOperate(a, b, op) {
    var ba = new Binary(a),
        bb = new Binary(b),
        format = Binary.format,
        opList = {
           '&': (a, b) => a & b,
           '|': (a, b) => a | b,
           '^': (a, b) => a ^ b,
           '~': a => ~a,
           '<<': (a, b) => a << b,
           '>>': (a, b) => a >> b,
           '>>>': (a, b) => a >> b,
        },
        bop = new Binary(opList[op](a, b));

//  console.log(format(ba.getTrues(32)));
//  console.log(format(bb.getTrues(32)));
//  console.log(format(bop.getTrues(32)));

//  console.log(format(ba.getOnes(32)));
//  console.log(format(bb.getOnes(32)));
//  console.log(format(bop.getOnes(32)));

    console.log(format(ba.getTwos(32)));
    console.log(format(bb.getTwos(32)));
    console.log(format(bop.getTwos(32)));    
}
```

### & (按位与)
对每对比特位执行与（AND）操作。只有 a 和 b 都是 1 时，a AND b 才是 1。与操作的真值表如下:

a | b | a&b
---|---|---
0 | 0 | 0
0 | 1 | 0
1 | 0 | 0
1 | 1 | 1

**将任一数值 x 与 0 执行按位与操作，其结果都为 0。将任一数值 x 与 -1 执行按位与操作，其结果都为 x。**

```
logOperate(2, 3, '&');
// 0000 0000 0000 0000 0000 0000 0000 0010
// 0000 0000 0000 0000 0000 0000 0000 0011
// 0000 0000 0000 0000 0000 0000 0000 0010

logOperate(-2, -3, '&');
// 1111 1111 1111 1111 1111 1111 1111 1110
// 1111 1111 1111 1111 1111 1111 1111 1101
// 1111 1111 1111 1111 1111 1111 1111 1100
```

### | (按位或)
对每一对比特位执行或（OR）操作。如果 a 或 b 为 1，则 a OR b 结果为 1。或操作的真值表：

a | b | a &#124; b
---|---|---
0 | 0 | 0
0 | 1 | 1
1 | 0 | 1
1 | 1 | 1

**将任一数值 x 与 0 进行按位或操作，其结果都是 x。将任一数值 x 与 -1 进行按位或操作，其结果都为 -1。**

```
logOperate(2, 3, '|');
// 0000 0000 0000 0000 0000 0000 0000 0010
// 0000 0000 0000 0000 0000 0000 0000 0011
// 0000 0000 0000 0000 0000 0000 0000 0011

logOperate(-2, -3, '|');
// 1111 1111 1111 1111 1111 1111 1111 1110
// 1111 1111 1111 1111 1111 1111 1111 1101
// 1111 1111 1111 1111 1111 1111 1111 1111
```

```
1 | 0 ;                       // 1

1.1 | 0 ;                     // 1

'asfdasfda' | 0 ;             // 0

0 | 0 ;                       // 0

(-1) | 0 ;                    // -1

(-1.5646) | 0 ;               // -1

[] | 0 ;                      // 0

({}) | 0 ;                    // 0

"123456" | 0 ;            // 123456

1.23E2 | 0;               // 123

1.23E12 | 0;              // 1639353344

-1.23E2 | 0;              // -123

-1.23E12 | 0;             // -1639353344
```

### ^ (按位异或)
对每一对比特位执行异或（XOR）操作。当 a 和 b 不相同时，a XOR b 的结果为 1。异或操作真值表：

a | b | a ^ b
---|---|---
0 | 0 | 0
0 | 1 | 1
1 | 0 | 1
1 | 1 | 0

```
logOperate(2, 3, '^');
// 0000 0000 0000 0000 0000 0000 0000 0010
// 0000 0000 0000 0000 0000 0000 0000 0011
// 0000 0000 0000 0000 0000 0000 0000 0001

logOperate(-2, -3, '^');
// 1111 1111 1111 1111 1111 1111 1111 1110
// 1111 1111 1111 1111 1111 1111 1111 1101
// 0000 0000 0000 0000 0000 0000 0000 0011
```

将任一数值 x 与 0 进行异或操作，其结果为 x。将任一数值 x 与 -1 进行异或操作，其结果为 ~x。

### ~ (按位非)
对每一个比特位执行非（NOT）操作。NOT a 结果为 a 的反转（即反码）。非操作的真值表：

a | ~a
---|---
0 | 1
1 | 1 

对任一数值 x 进行按位非操作的结果为 -(x + 1)。例如，~5 结果为 -6。

```
// 判断字符串是否存在：
// eg: 
var str = 'heaven is a place nearby!';
var search = 'a';

// str.indexOf(search) >= 0
// -str.indexOf(search) <= 0
// ~str.indexOf(search)

logOperate(2, 0, '~');
// 0000 0000 0000 0000 0000 0000 0000 0010
// 1111 1111 1111 1111 1111 1111 1111 1101
```

## 按位移动操作符
按位移动操作符有两个操作数：第一个是要被移动的数字，而第二个是要移动的长度。移动的方向根据操作符的不同而不同。

按位移动会先将操作数转换为大端字节序顺序(big-endian order)的32位整数,并返回与左操作数相同类型的结果。右操作数应小于 32位，否则只有最低 5 个字节会被使用。


```
注：Big-Endian:高位字节排放在内存的低地址端，低位字节排放在内存的高地址端，
又称为"高位编址"。
Big-Endian是最直观的字节序：
①把内存地址从左到右按照由低到高的顺序写出；
②把值按照通常的高位到低位的顺序写出；
③两者对照，一个字节一个字节的填充进去。
```

### << (左移)
该操作符会将第一个操作数向左移动指定的位数。向左被移出的位被丢弃，右侧用 0 补充。

**在数字 x 上左移 y 比特得到 x * 2y.**

```
logOperate(2, 3, '~'); // 16
// 0000 0000 0000 0000 0000 0000 0000 0010
// 0000 0000 0000 0000 0000 0000 0001 0000

logOperate(-2, 3, '~'); // -16
// 1111 1111 1111 1111 1111 1111 1111 1110
// 1111 1111 1111 1111 1111 1111 1111 0000
```

### >> (有符号右移)
该操作符会将第一个操作数向右移动指定的位数。向右被移出的位被丢弃，拷贝最左侧的位以填充左侧。由于新的最左侧的位总是和以前相同，符号位没有被改变。所以被称作“符号传播”。

```
logOperate(8, 3, '>>');
// 0000 0000 0000 0000 0000 0000 0000 1000
// 0000 0000 0000 0000 0000 0000 0000 0001

logOperate(-5, 4, '>>');
// 1111 1111 1111 1111 1111 1111 1111 1011
// 1111 1111 1111 1111 1111 1111 1111 1111
```

### >>> (无符号右移)
该操作符会将第一个操作数向右移动指定的位数。向右被移出的位被丢弃，左侧用0填充。因为符号位变成了 0，所以结果总是非负的。（译注：即便右移 0 个比特，结果也是非负的。）

对于非负数，有符号右移和无符号右移总是返回相同的结果。

```
logOperate(8, 3, '>>>');
// 0000 0000 0000 0000 0000 0000 0000 1000
// 0000 0000 0000 0000 0000 0000 0000 0001

logOperate(-8, 3, '>>>');
// 1111 1111 1111 1111 1111 1111 1111 1000
// 1111 1111 1111 1111 1111 1111 1111 1111
```
[位操作符代码实例](http://js.jsrun.net/vdXKp/edit)

## 掩码
位运算经常被用来创建、处理以及读取标志位序列——一种类似二进制的变量。虽然可以使用变量代替标志位序列，但是这样可以节省内存（1/32）。

掩码 (bitmask) 是一个通过与/或来读取标志位的位序列。典型的定义每个标志位的原语掩码如下，
例如，有四个标志位：A,B,C,D

```
var FLAG_A = 1; // 0001
var FLAG_B = 2; // 0010
var FLAG_C = 4; // 0100
var FLAG_D = 8; // 1000
```

新的掩码可以在以上掩码上使用逻辑运算创建。例如，掩码 1011 可以通过 FLAG_A、FLAG_B 和 FLAG_D 逻辑或得到：

```
var mask = FLAG_A | FLAG_B | FLAG_D; // 0001 | 0010 | 1000 => 1011
```

某个特定的位可以通过与掩码做逻辑与运算得到，通过与掩码的与运算可以去掉无关的位，得到特定的位。例如，掩码 0100 可以用来检查标志位 C 是否被置位：

```
// 判断是否含有FLAG_C
if (flags & FLAG_C) { // 0101 & 0100 => 0100 => true
   // do stuff
}
```

一个有多个位被置位的掩码表达任一/或者的含义。例如，以下两个表达是等价的：

```
// 如果我们有 FLAG_B 或者 FLAG_C 至少一个
// (0101 & 0010) || (0101 & 0100) => 0000 || 0100 => true
if ((flags & FLAG_B) || (flags & FLAG_C)) {
   // do stuff
}

// 等价于

var mask = FLAG_B | FLAG_C; // 0010 | 0100 => 0110
if (flags & mask) { // 0101 & 0110 => 0100 => true
   // do stuff
}
```

可以通过与掩码做或运算设置标志位，掩码中为 1 的位可以设置对应的位。例如掩码 1100 可用来设置位 C 和 D：

```
var mask = FLAG_C | FLAG_D; // 0100 | 1000 => 1100
flags |= mask;   // 0101 | 1100 => 1101
```

可以通过与掩码做与运算清除标志位，掩码中为 0 的位可以设置对应的位。掩码可以通过对原语掩码做非运算得到。例如，掩码 1010 可以用来清除标志位 A 和 C ：

```
var mask = ~(FLAG_A | FLAG_C); // ~0101 => 1010
flags &= mask;   // 1101 & 1010 => 1000
```

如上的掩码同样可以通过 ~FLAG_A & ~FLAG_C 得到（德摩根定律）：

```
var mask = ~FLAG_A & ~FLAG_C;
flags &= mask;   // 1101 & 1010 => 1000
```

标志位可以使用异或运算切换。所有值为 1 的为可以切换对应的位。例如，掩码 0110 可以用来切换标志位 B 和 C：

```
var mask = FLAG_B | FLAG_C;
flags = flags ^ mask;   // 1100 ^ 0110 => 1010
```

最后，所有标志位可以通过非运算翻转:

```
// entering parallel universe...
flags = ~flags;    // ~1010 => 0101
```

## 位操作使用实例
### 1.判断一个数a的奇偶：

```
// 奇数
a & 1 === 1;

// 偶数
a & 1 === 0;
```

### 2.两个整数x,y的平均值：

```
const avarage = (x, y) => (x & y) + ((x ^ y) >> 1); 
```

### 3.不使用缓存交换两个整数：

```
// 正常版本
var swap1 = (x, y) => {
  if (x !== y ) {
    var z = x;
    x = y;
    y = z;
  }
}

// 使用位操作符
var swap = (x, y) => {
  if (x !== y ) {
    x ^= y;
    y ^= x;
    x ^= y;   
  }
}
```

### 4.老鼠试毒：
假设有1000杯水，其中有一杯有毒，至少用多少只老鼠试出哪杯有毒?

```
// 使用位掩码解决
// 假设共有8杯水，标记：
var cup_a = 1; // 0001
var cup_b = 2; // 0010
var cup_c = 3; // 0011
var cup_d = 4; // 0100
var cup_e = 5; // 0101
var cup_f = 6; // 0110
var cup_g = 7; // 0111
var cup_h = 8; // 1000

// 转置矩阵可得：
0000 0001
0001 1110
0110 0110
1010 1010

1234 5678

// 
mouse_a = 8;
mouse_b = 4 | 5 | 6 | 7;
mouse_c = 2 | 3 | 6 | 7;
mouse_d = 1 | 3 | 5 | 7;

2^4 = 8;
....
2^10 = 1024
也就是：0000000001，0000000010，0000000011，...，1111101000；
道理同上。
```

### 5.权限问题：
在实际开发中，我们常常遇到权限的判断的问题，比如说，不同的用户对系统有不同的操作权限，有的用户可能有多种权限，我们最常规的办法就是每一个权限定义一个BOOL值。
假设，某系统有4种权限，那么，就有了：

```
// var role = {
//  a: 'a',
//  b: 'b',
//  c: 'c',
//  c: 'd',
// };

// 判断某用户有三种权限： role.a && role.b && role.c

// 使用位操作：
// var role = {
//  a: 1 << 0, // 0001
//  b: 1 << 1, // 0010
//  c: 1 << 2, // 0100
//  d: 1 << 3, // 1000
// }

// 判断某用户有三种权限： role.a | role.b | role.c

var role = {
 a: 1 << 0, // 0001
 b: 1 << 1, // 0010
 c: 1 << 2, // 0100
 d: 1 << 3, // 1000
}

function Permission(flag){
    this.flag = flag;
}

// 设置权限
Permission.prototype.set = function(perm) {
    this.flag = perm;
}

// 添加一项或多项权限
Permission.prototype.enable = function(perm) {
    this.flag |= perm;
}

// 删除一项或多项权限
Permission.prototype.disable = function(perm) {
    this.flag &= ~perm;
}

// 是否拥有某些权限
Permission.prototype.has = function(perm) {
    return (this.flag & perm) === perm;
}

// 是否禁用了某些权限
Permission.prototype.not = function(prem) {
    return (this.flag & perm) === 0;
}

// 是否仅仅拥有某些权限
Permission.prototype.only = function(perm) {
    return this.flag === perm;
}

// 打印当前权限
Permission.prototype.log = function() {
   var perm_list_key = [];
   Object.keys(role).forEach(key => {
       if(this.has(role[key])){
           perm_list_key.push(key);
       }
   });
   console.log('当前权限:',perm_list_key.join(','));
   return perm_list_key;
}
var perm_a = new Permission(role.a | role.b | role.c);

// perm_a.disable(role.a);
console.log(perm_a);
```
[通过位操作实现一个权限类](http://js.jsrun.net/wdXKp/edit)