---
title: JS实现new
date: 2021-03-01 15:00
comments: true
tags:
    - js
---

#### 实现过程
+ 创建一个新对象
+ 将构造函数的作用域赋值给新对象（原型链接this指向）
+ 执行构造函数中的代码
+ 返回新对象
<!-- more -->

代码实现：
```javascript
function newFun(fn) {
    const obj = Object.create(fn.prototype);
    const arg = Array.prototype.slice.call(arguments, 1);
    const result = fn.apply(obj, arg)
    return typeof result === 'object' ? result : obj
}

function Fun(name) {
    this.name = name;
}
function Fun2(name) {
    this.name = name;
    return {
        name: 'mk2'
    }
}

const o1 = new Fun('mk');
const o2 = new Fun2('mk');
const o3 = newFun(Fun, 'mk');
const o4 = newFun(Fun2, 'mk');
console.log(o1, o2, o3, o4); // {name: mk}, {name: mk2}, {name: mk}, {name: mk2}
```