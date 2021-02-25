---
layout: post
title: "javascript基础知识点"
date: 2021-02-25 17:00
comments: true
tags: 
	- js
---

#### 隐式类型转换

加法的隐式转换规则：
  1. 如果两边都是数字，则就是普通的数学计算
  2. 如果有一边是字符串，则另一边也转成字符串，变成字符串的拼接
  3. 如果没有字符串，则调用Number方法，转成数字，再进行相加
  4. 如果有一边是对象，则对象调用toString得到字符串表示，再进行计算


  <!-- more -->

  ```javascript
  1 + 1 => 2
  'a' + 1 => 'a1'
  null + 1 => 1
  const fun = () => {}
  fun + 1 => '() => {}1'
  const obj = {}
  obj + 1 => '[object Object]1'
  ```

“==”隐式转换规则：
  1. 数字与字符串比较时，字符串转换为数字
  2. 有一边为布尔值，则将布尔值转换为1 / 0
  3. nul == undefined , 除此之外 null 与 undefined 与其他任何值都不相等
  4. 有一边对象或者数组类型，另一边是数字或字符串，则需要调用toString()或者valueOf()方法转化成简单类型，然后进行比较


  ```javascript
  1 == '1' => true
  1 == true => true
  0 == false => true
  null == undefined => true
  const obj = {}
  obj == '[object Object]' => true
  ```

#### 数组常用方法

+ push()      向数组的末尾增加一项成员 返回值 -> 增加后数组的长度
+ unshift()   向数组的开头增加一项成员 返回值 -> 增加后数组的长度
+ pop()        从数组的末尾删除一项成员 返回值 -> 删除项
+ shift()       从数组的开头删除一项成员 返回值 -> 删除项
+ sort()        排序 在原始的数组上进行排序  不传参数 默认按照ASCII值进行排序 传函数参数 参数应该具有两个参数a 和 b， 函数返回值 a < b, a 就在 b 之前；a = b，a 和 b 不换位置；a > b, a 排在 b 后。
+ slice()        截取数组，参数[startIndex， endIndex），返回一个新的数组。
+ splice()      删除/新增数组成员， 参数1开始删除位置的索引（包含），参数2 要删除多少项，参数3新增的项（从删除的位置新增）。
+ indexOf()   查询传入参数所在位置的索引，没有返回-1。
+ includes()  查询传入参数是否存在在数组中，返回一个布尔值。
+ find()         参数是一个函数，返回数组中第一个符合条件的成员。
+ findIndex() 参数是一个函数，返回数组中第一个符合条件的成员的索引。
+ Array.of()   更正了Array()创建数组时只传一个参数的问题。
+ Array.from() 可以将类数组转换为真正的数组
