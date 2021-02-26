---
title: css样式相关面试题
categories: 面试题
tags: css
date: 2021-02-26 16:43:26
---

> 总结梳理前端开发在面试中遇到的高频 css 面试题

## 子 div 在父 div 中水平垂直居中的方式

1. display: flex 弹性和布局，需要考虑 ie 兼容问题

```
.outside{
    width: 400px;
    height: 400px;
    background: goldenrod;
    display: flex;
    justify-content: center;
    align-items: center;
}
.inside{
    width: 100px;
    height: 100px;
    background: forestgreen;
}
```

## flex 弹性布局

1. 设置盒子的 display 属性为 flex，或者 line-flex，其对应还有六个 css 属性，分别为：

1）flex-direction：设置子元素的排列方式（row，column，row-reverse，column-reverse）

2）flex-warp：设置子元素的是否换行（nowarp，warp，warp-reverse）

3）flex-flow：flex-direction 和 flex-warp 的缩写，默认为 row nowarp

4）justify-content：设置子元素的水平排列方式（flex-start，flex-end，center，span-around，span-between）

5）align-items：设置子元素的垂直方式（flex-start，flex-end，center，stretch，baseline）

6）align-content：设置多个轴线的排列方式（flex-start，flex-end，center，spand-around，spand-between，stretch）

2. 对应的子元素项目也拥有自身的六个 css 属性，分别为：

1）order：设置元素的排列权重 值越大越在后

2）flex-grow：设置元素的放大比例

3）flex-shrink：设置元素的缩小比例

4）flex-basis：设置多余空间项目主轴所占比例空间

5）flex：flex-grow 和 flex-shrink 和 flex-basis 的缩写方式 默认为 0 1 auto

6）align-self：设置子元素自己的垂直排列方式，默认为盒子的 align-items 的值

:warning:：设置 flex 布局后，子元素的 float，clear，vertical-align 都无效
