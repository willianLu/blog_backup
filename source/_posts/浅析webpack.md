---
title: 浅析webpack
date: 2021-03-10 18:00
comments: true
tag:
    - webpack
---

> 本质上，webpack 是一个用于现代 JavaScript 应用程序的_静态模块打包工具_。当 webpack 处理应用程序时，它会在内部构建一个 依赖图(dependency graph)，此依赖图对应映射到项目所需的每个模块，并生成一个或多个 bundle。
<!-- more -->

#### 打包流程

+ 初始化配置对象，创建compiler对象
+ 实例化插件，调用插件的apply方法，挂载插件的监听
+ 从入口文件执行编译，按照文件类型调用相应的loader，在合适的时间调用plugin执行，并查找各个模块的依赖
+ 将编译后的代码组装成一个个代码块（chunk），并安依赖和配置确定输出内容
+ 根据output把文件输出到对象的目录下

