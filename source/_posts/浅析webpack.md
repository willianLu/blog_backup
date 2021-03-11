---
title: 浅析webpack
date: 2021-03-10 18:00
comments: true
tag:
    - webpack
---

> 本质上，webpack 是一个用于现代 JavaScript 应用程序的_静态模块打包工具_。当 webpack 处理应用程序时，它会在内部构建一个 依赖图(dependency graph)，此依赖图对应映射到项目所需的每个模块，并生成一个或多个 bundle。
<!-- more -->
#### 概念
+ 入口(entry) - 指示 webpack 应该使用哪个模块，来作为构建其内部 依赖图(dependency graph) 的开始。
+ 输出(output) - output 属性告诉 webpack 在哪里输出它所创建的 bundle，以及如何命名这些文件。
+ loader - webpack 只能理解 JavaScript 和 JSON 文件，这是 webpack 开箱可用的自带能力。loader 让 webpack 能够去处理其他类型的文件，并将它们转换为有效 模块，以供应用程序使用，以及被添加到依赖图中。
+ 插件(plugin) - loader 用于转换某些类型的模块，而插件则可以用于执行范围更广的任务。包括：打包优化，资源管理，注入环境变量。
+ 模式(mode) - 通过选择 development, production 或 none 之中的一个，来设置 mode 参数，你可以启用 webpack 内置在相应环境下的优化。
+ 浏览器兼容性(browser compatibility) - webpack 支持所有符合 ES5 标准 的浏览器（不支持 IE8 及以下版本）。
+ 环境(environment) - webpack 5 运行于 Node.js v10.13.0+ 的版本。
[官网概念详解](https://webpack.docschina.org/concepts/)

#### 打包流程

+ 初始化配置对象，创建compiler对象
+ 实例化插件，调用插件的apply方法，挂载插件的监听
+ 从入口文件执行编译，按照文件类型调用相应的loader，在合适的时间调用plugin执行，并查找各个模块的依赖
+ 将编译后的代码组装成一个个代码块（chunk），并安依赖和配置确定输出内容
+ 根据output把文件输出到对应的目录下

