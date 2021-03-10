---
title: 浅析Bable
date: 2021-03-10 17:00
comments: true
tags:
    - bable
---

### Bable是什么
> Babel 是一个 JavaScript 编译器。
> Babel 是一个工具链，主要用于将 ECMAScript 2015+ 版本的代码转换为向后兼容的 JavaScript 语法，以便能够运行在当前和旧版本的浏览器或其他环境中。
<!--more-->

#### Bable 能做的事情
+ 语法转换
+ 通过 Polyfill 方式在目标环境中添加缺失的特性 (通过 @babel/polyfill 模块)
+ 源码转换

#### Bable 工作过程
1. Parse(解析)：通过词法分析和语法分析，将源代码转换成抽象语法树AST
2. Transform(转换)：通过插件对AST做一些特殊处理，深度优先遍历AST生成新的AST
3. Generate(代码生成)：将第二步经过转换过的AST生成新的代码

#### 插件
Babel 虽然开箱即用，但是什么动作都不做。它基本上类似于 const babel = code => code; ，将代码解析之后再输出同样的代码。如果想要 Babel 做一些实际的工作，就需要为其添加插件。
+ 转换插件 - 这些插件用于转换你的代码。
+ 语法插件 - 这些插件只允许 Babel 解析（parse） 特定类型的语法（而不是转换）。

#### 配置
1. .babelrc
　　只是项目中经常用到的方式，在项目根目录创建名为.babelrc文件，内部包括两个方面：plugins和presets，如下
    ```javascript
    {
        "presets": [...],
        "plugins": [...]
    }
    ```
2. babel.config.js
　　这种方式是使用js代码编写，如下
    ```javascript
    module.exports = function () {
        return {
            presets: [ ... ],
            plugins: [ ... ]
        };
    }
    ```
3. package.json
　　这种该方式是在项目配置文件package.json中进行配置，如下：
    ```javascript
    {
        "name": "my-package-babel",
        "version": "1.0.0",
        "babel": {
            "presets": [ ... ],
            "plugins": [ ... ]
        }
    }
    ```

[浅析Babel原理](https://www.cnblogs.com/jyybeam/p/13375179.html)