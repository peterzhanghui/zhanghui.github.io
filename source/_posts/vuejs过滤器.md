---
title: vuejs
date: 2021-01-12 23:18:25
tags: vuejs
---

> 总结一些 vue 相关的知识点

## 组件中 data 必须是一个函数？

一个组件的 data 选项必须是一个函数，因此每个实例可以维护一份被返回对象的独立的拷贝：

## watch 监听$route 变化第一次不会执行

项目中我们需要根据动态路由传递的参数来请求数据，如果只方在 created 总组件切换不会请求，放到 watch 中第一次不会请求。解决方法可以给 watch 返回一个对象

```
watch : {
    $route: {
        immediate: true, // 加载立即触发
        handler() {
            console.log('router变了')
        }
    }
}
```
