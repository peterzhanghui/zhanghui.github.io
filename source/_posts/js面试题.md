---
title: js面试题
categories: 前端开发
tags:
  - js
  - 面试
date: 2019-02-27 14:09:45
---

## 堆栈

堆：存储引用类型值的空间

栈：存储基本类型值和指定代码的环境

## 如何判断一个数据是 NaN

1. NaN 非数字 但是用 typeof 检测是 number 类型 所以可以 （typeof XXX == number && isNaN(XXX)）
2. 利用 NaN 是唯一一个不等于任何自身的特点 n !== n
3. Object.is(value1, value2)方法（判断两个值是否相等）
4. Number.isNaN(val)

## Object.is 和 == 和 === 的区别

相同点都是判断两个值是否相等的操作

区别如下：

- == 对比时如果两边变量的类型不同会进行强制类型转换， === 和 Object.is 不会
- === 运算符 (也包括 == 运算符) 将数字 -0 和 +0 视为相等 ，而将 Number.NaN 与 NaN 视为不相等，Object.is 可以区分

```
Object.is(null, null);       // true

// 特例
Object.is(0, -0);            // false
Object.is(0, +0);            // true
Object.is(-0, -0);           // true
Object.is(NaN, 0/0);         // true
```

## Js 中 null 与 undefined 区别

Null 表示一个值被定义了，但是这个值是空值
Undefined 变量声明但未赋值

- number 转换的值不同 number（null）为 0 number（undefined） 为 NaN
- 相同点是如果使用 if 判断都会转换为 false

## Promise 的理解

### 一、什么是 Promise？

我们都知道，Promise 是承诺的意思，承诺它过一段时间会给你一个结 果。Promise 是一种解决异步编程的方案，相比回调函数和事件更合理和更 强大。 从语法上讲，promise 是一个对象，从它可以获取异步操作的消息；

### 二、promise 有三种状态：

pending 初始状态也叫等待状态，fulfiled 成功状态，rejected 失败状态；状态一旦改变，就不会再变。创造 promise 实例后，它会立即执行。

### 三、Promise 的两个特点

1. Promise 对象的状态不受外界影响
2. Promise 的状态一旦改变，就不会再变，任何时候都可以得到这个结 果，状态不可以逆，

### 四、Promise 的三个缺点

1. 无法取消 Promise,一旦新建它就会立即执行，无法中途取消
2. 如果不设置回调函数，Promise 内部抛出的错误，不会反映到外部
3. 当处于 pending（等待）状态时，无法得知目前进展到哪一个阶段， 是刚刚开始还是即将完成

### 五、主要解决的问题

1. 链式调用，主要解决回调地狱问题
2. 支持并发请求

### Promise 原理 （待做）

## Vue 组件中的 data 为什么是函数

Data 是一个函数时，每个组件实例都有自己的作用域，每个实例相互独 立，不会相互影响如果是引用类型（对象），当多个组件共用一个数据源时，一处数据改变， 所有的组件数据都会改变，所以要利用函数通过 return 返回对象的拷贝， （返回一个新数据），让每个实例都有自己的作用域，相互不影响。

## Vue 双数据绑定过程中，这边儿数据改变了怎么通知另一边

改变数据劫持和观察者模式 Vue 数据双向绑定是通过数据劫持和观察者模式来实现的， 数据劫持，object.defineproperty 它的目的是：当给属性赋值的时候，程序可以感知到，就可以控制属性值的有效范围，可以改变其他属性的 值观察者模式它的目的是当属性发生改变的时候，使用该数据的地方也发 生改变

## Vuex 流程

在 vue 组件里面，通过 dispatch 来触发 actions 提交修改数据的操作， 然后通过 actions 的 commit 触发 mutations 来修改数据，mutations 接收到 commit 的请求，就会自动通过 mutate 来修改 state，最后由 store 触发每一个调用它的组件的更新

### vuex 的 State 特性是？

State 就是数据源的存放地 State 里面的数据是响应式的，state 中的数据改变，对应这个数据的组 件也会发生改变 State 通过 mapstate 把全局的 state 和 getters 映射到当前组件的计算 属性中

### vuex 的 Getter 特性是？

Getter 可以对 state 进行计算操作，它就是 store 的计算属性 Getter 可以在多组件之间复用 如果一个状态只在一个组件内使用，可以不用 getters 51.vuex 的 Mutation 特性是？ 更改 vuex store 中修改状态的唯一办法就是提交 mutation，可以在回 调函数中修改 store 中的状态

### vuex 的 actions 特性是？

Action 类似于 mutation，不同的是 action 提交的是 mutation，不是 直接变更状态，可以包含任意异步操作

### vuex 的优势

优点：解决了非父子组件的通信，减少了 ajax 请求次数，有些可以直接 从 state 中获取 缺点：刷新浏览器，vuex 中的 state 会重新变为初始状态，解决办法是 vuex-along，得配合计算属性和 sessionstorage 来实现

## Vue3.0 是如何变得更快的？（底层，源码）

1. diff 方法优化 Vue2.x 中的虚拟 dom 是进行全量的对比。

2. Vue3.0 中新增了静态标记（PatchFlag）：在与上次虚拟结点进行对 比的时候，值对比带有 patch flag 的节点，并且可以通过 flag 的信息 得知当前节点要对比的具体内容化。hoistStatic 静态提升 Vue2.x : 无论元素是否参与更新，每次都会重新创建。 Vue3.0 : 对不参与更新的元素，只会被创建一次，之后会在每次渲染时 候被不停的复用。

3. cacheHandlers 事件侦听器缓存 默认情况下 onClick 会被视为动态绑定，所以每次都会去追踪它的 变化但是因为是同一个函数，所以没有追踪变化，直接缓存起来复用 即可。

## nuxt.js （待做）

## webpack （待做）

## vue-router （待做）
