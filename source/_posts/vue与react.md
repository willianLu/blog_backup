---
title: vue与react
date: 2021-03-09 10:00
comments: true
tag:
    - vue
    - react
---

#### Vue介绍
> Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。
#### React介绍
> React 是一个声明式，高效且灵活的用于构建用户界面的 JavaScript 库。使用 React 可以将一些简短、独立的代码片段组合成复杂的 UI 界面，这些代码片段被称作“组件”。
<!-- more -->
#### 相同点
1. 使用虚拟DOM
2. 提供了响应式和组件化
3. 都专注于核心库，将其他功能交给相关库（如路由和状态管理）
4. 支持服务端渲染
5. 支持native方案，如react-native（react），weex（vue）

#### 不同点
1. vue推荐使用模版的方式开发，.vue文件包含template、script、style，支持jsx；react采用jsx语法编程，推崇HTML和CSS全都写进JavaScript里，即all-in-js的方式。
2. 数据驱动，都推行单向数据流。vue通过依赖搜集方式对数据劫持/代理，实现响应式和双向绑定。react数据不可变，需要手动调用setState已达到响应的目的，数据的变化使用diff的方式去计算。
3. 渲染更新的方式不同
    + 因为vue数据变化采用的依赖搜集方式，当数据变化是，会通知相关的watcher进行更新，比较有针对性
    + react当数据发生变化时，是以当前组件为根重新渲染整个组件子树，如果要避免不必要的子组件渲染，需要使用PureComponent或者手动实现shouldComponentUpdate方法
4. 组件引用的不同，vue采用全局和局部注册的方式，react采用import来引用。
5. vue支持插槽使用，react通过props的children字段实现插槽功能。
6. 组件之间通讯方式不同，vue支持props、事件监听、inject/provide等方式，react支持props、函数回调、context等方式。
7. vue除了核心组件库之外，路由和状态管理库都有官方团队维护；而react只专注核心库，相关库都交由社区来维护，相对来讲社区更加繁荣。

在使用上其实有很多不同点的，比如vue的指令

#### 学习难度（参考晚上资料）
vue上手简单，易学习；react学习曲线陡峭，有一定难度。


[对比其他框架-vue官网](https://cn.vuejs.org/v2/guide/comparison.html)