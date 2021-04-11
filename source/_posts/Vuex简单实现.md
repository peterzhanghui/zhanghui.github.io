---
title: Vuex
categories: 前端开发
tags: js
date: 2021-04-07 17:21:42
---

> Vuex 是专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态。Vuex 和单纯的全局对象主要有两点不同，一 Vuex 的状态存储是响应式的。你不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。

## Vuex 的持久化处理

使用 Vuex 的插件 vuex-persist [github 连接](https://github.com/championswimmer/vuex-persist#tips-for-nuxt)文中有详细教程不在赘述，主要说一下在 nuxt.js 中的配置

按照官网的教程新建 plugins 配置后，需要在配置 Vuex 的 store 文件夹 的 index.js 添加 插件配置。最总就可以实现持久化缓存了。

```
import VuexPersistence from 'vuex-persist';
export const plugins = [new VuexPersistence().plugin];
```

## nuxt.js 使用 nuxtServerInit 获取组件数据

运行在服务端，都能帮助我们在页面渲染（组件加载 ）前操作 store。当我们想将服务端的一些数据传到客户端时，这个方法是灰常好用的。

使用方法示例，具体可以结合自己业务需要处理相关数据

```
export const actions = {
    nuxtServerInit({ commit }, { req }) {
        let cookie = req.headers.cookie;
        if (cookie) {
            cookie.split(';').map(item => {
                if (item.split('=')[0].trim() === 'token') {
                    let token = item.split('=')[1];
                    commit('setToken', token);
                }
            })
        }
    },
};

```
