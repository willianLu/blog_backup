---
title: JS数据类型及栈和堆
date: 2021-03-01 11:00
comments: true
tags:
    - js
---

#### JS数据类型
最新的 ECMAScript 标准定义了 9 种数据类型:
<!--more-->
+ 6 种原始类型，undefined、Boolean、Number、String、BigInt、Symbol
+ null: typeof instance === "object"。
+ Object：typeof instance === "object"。任何 constructed 对象实例的特殊非数据结构类型，也用做数据结构：new Object，new Array，new Map，new Set，new WeakMap，new WeakSet，new Date，和几乎所有通过 new keyword 创建的东西。
+ 非数据结构，尽管 typeof 操作的结果是：typeof instance === "function"。这个结果是为 Function 的一个特殊缩写，尽管每个 Function 构造器都由 Object 构造器派生。

#### 原始值
> 除 Object 以外的所有类型都是不可变的（值本身无法被改变）。例如，与 C 语言不同，JavaScript 中字符串是不可变的（译注：如，JavaScript 中对字符串的操作一定返回了一个新字符串，原始字符串并没有被改变）。我们称这些类型的值为“原始值”。
+ 布尔类型。表示一个逻辑实体，可以有两个值：true 和 false。
+ null类型。只有一个值：null。
+ undefined类型。一个没有被赋值的变量会有个默认值 undefined。
+ 数字类型。根据 ECMAScript 标准，JavaScript 中只有一种数字类型：基于 IEEE 754 标准的双精度 64 位二进制格式的值（-(253 -1) 到 253 -1）。它并没有为整数给出一种特定的类型。除了能够表示浮点数外，还有一些带符号的值：+Infinity，-Infinity 和 NaN (非数值，Not-a-Number)。
+ BigInt类型是 JavaScript 中的一个基础的数值类型，可以用任意精度表示整数。
+ 字符串类型。JavaScript的字符串类型用于表示文本数据。它是一组16位的无符号整数值的“元素”。在字符串中的每个元素占据了字符串的位置。第一个元素的索引为0，下一个是索引1，依此类推。字符串的长度是它的元素的数量。
+ 符号类型。符号(Symbols)是ECMAScript 第6版新定义的。符号类型是唯一的并且是不可修改的, 并且也可以用来作为Object的key的值。

#### 对象
在计算机科学中, 对象是指内存中的可以被 标识符引用的一块区域。在 Javascript 里，对象可以被看作是一组属性的集合。
+ 属性。
1.数据属性，数据属性是键值对。
2.访问器属性有一个或两个访问器函数 (get 和 set) 来存取数值。
+ “标准”对象和函数，一个 Javascript 对象就是键和值之间的映射。
+ 日期，内建Date对象。
+ 有序集: 数组和类型数组。数组是一种使用整数作为键(integer-key-ed)属性和长度(length)属性之间关联的常规对象。类型数组(Typed Arrays)是ECMAScript Edition 6中新定义的 JavaScript 内建对象，提供了一个基本的二进制数据缓冲区的类数组视图。
+ 键控集: Maps, Sets, WeakMaps, WeakSets

[相关文献](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures)

#### 基本类型和引用类型
在js中数据类型可以分为基本类型和引用类型。基本类型是存在栈内存中，引用类型是存在堆内存中，而引用类型的引用地址还是存在栈内存中。当我们操作两种类型的变量时有下面几个特点：
1. 基本类型可以直接复制，复制之后的内容和原内容没有联系。
2. 引用类型直接赋值给另一个变量以后相互之间的修改会互相影响对方，进而引出浅拷贝与深拷贝的问题。
3. 基本类型不能添加属性或方法，而引用类型可以动态添加或删除属性/方法。

#### 栈内存
栈是一种先进后出的数据结构，栈内存是内存中用于存放临时变量的一片内存块。当声明一个基本变量时，它就会被存储到栈内存中。
如：
```javascript
    let a = 1;
    let b = 'js';
```
存储对应：

| 变量名 | 变量值 |
| :---: | :---: |
| a | 1 |
| b | js |

而当发生改变时，如下

```javascript
    a = 2;
    let c = b;
```
存储对应：

| 变量名 | 变量值 |
| :---: | :---: |
| a | 2 |
| b | js |
| c | js |

栈内存特点：存取速度快，但是不灵活，同时由于结构简单，在变量使用完成后就可以将其释放，内存回收容易实现。

#### 堆内存

堆内存的存储不同与栈，虽然他们都是内存中的一片空间，但是堆内存存储变量时没有什么规律可言。

```javascript
	let obj = {
        foo: 1,
        bar: 2
    }
    let foo = 1;
    let bar = 2;
```
内存模型如下：
![内存模型](/static/images/内存模型.jpg)

修改与赋值
```javascript
let obj1 = {
    foo: 'foo',
    bar: 'bar'
}

let obj2 = obj1;
let obj3 = {
    foo: 'foo',
    bar: 'bar'
}

console.log(obj1 === obj2);
console.log(obj1 === obj3);

obj2.foo = 'foofoo';

console.log(obj1.foo === 'foofoo');
```
内存模型如下：
![内存模型](/static/images/内存模型2.jpg)

堆内存的访问地址是存储在栈内存中，查询时先由变量名查找到栈内存中的堆内存地址，然后才查到具体堆内存。

