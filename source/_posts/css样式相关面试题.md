---
title: css样式相关面试题
categories: 面试题
tags: css
date: 2019-02-26 16:43:26
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

宽高和背景色属性下面实现中省略

2. position 定位 + maring(子元素高度确定) / transform（子元素高度不确定）

```
.outside{
    width: 600px;
    height: 400px;
    padding: 30px;
    background: goldenrod;
    position: relative;
}
.inside{
    width: 100px;
    height: 100px;
    position: absolute;
    top: 50%;
    left: 50%;
    margin: -50px 0 0 -50px;
    /* transform:translate(-50%,-50%); */
    background: forestgreen;
}
```

3. display：table-cell，vertical-align：middle;

```
.outside{
    width: 600px;
    height: 400px;
    padding: 30px;
    background: goldenrod;
    display:table-cell;
    vertical-align:middle;
}
.inside{
    width: 100px;
    height: 100px;
    margin: 0 auto;
    background: forestgreen;
}
```

## 用纯 CSS 创建一个三角形？

```
/*
  采用的是相邻边框链接处的均分原理
  将元素的宽高设为0，只设置 border ,
  将任意三条边隐藏掉（颜色设为 transparent ）,剩下的就是一个三角形
 */
#demo{
  width: 0;
  height: 0;
  border-width: 20px;
  border-style: solid;
  border-color: transparent transparent red transparent;
}

```

## 清除浮动

> 当不给父元素设置宽高时，父元素的宽高会被子元素的内容撑开。但当子元素设置浮动属性（float） 后，子元素会溢出到父元素外，父元素的宽高也不会被撑开，这称之为“高度塌陷”。可以理解为使用浮动后的副作用，解决方法大体有以下两种

1.  子元素添加 clear 属性

```
.clearfix {
  zoom: 1;
}
.clearfix:after {
  display: block;
  height: 0;
  clear: both;
  visibility: hidden;
  overflow: hidden;
  content: ".";
}

```

2. 父元素添加 overflow: hiden;触发浮动元素父元素的 BFC (Block Formatting Contexts, 块级格式化上下文)，使到该父元素可以包含浮动元素

第二种虽然代码量小，但是超出尺寸的内容会被隐藏（不推荐）目前主流的做法是使用第一种

## 盒模型

- 标准盒模型 (box-sizing: content-box;) 宽高大小不包含 padding,border
- IE 盒模型 （box-sizing: border-box;）宽高大小包含 padding,border
  目前采用最多的是 ie 盒模型，设置宽高包含这个元素尺寸，不需要在计算

- flex 布局
- 多列布局 (column-count: 3;容器分三列布局，一般用于 平板电脑等 宽屏上的文章布局)
- 网格布局 （grid）

## 经典布局方案

左右固定，中间自适应

- 圣杯布局

```
.clearfix{
        zoom: 1;
    }
    .clearfix::after{
        clear: both;
        content: '.';
        visibility: hidden;
        display: block;
        overflow: hidden;
        height: 0;
    }
    .content{
        overflow: hidden;
        height: 100%;
        padding: 0 100px;
    }
    .center,.left, .right{
        float: left;
    }
    .center{
        width: 100%;
        min-height: 400px;
        background: goldenrod;
    }
    .left, .right{
        width: 100px;
        height: 100px;
        background: forestgreen;
    }
    .left{
        margin-left: -100%;
        position: relative;
        left: -100px;
    }
    .right{
        margin-right: -100px;
    }
        <div class="content ">
       <div class="center"></div>
       <div class="left"></div>
       <div class="right"></div>
   </div>
```

- 双飞翼布局
  和圣杯布局不同的就是 left，right 和 center 不在同一个父级元素下

  ```
  <div class="clearfix">
        <div class="content ">
            <div class="center"></div>
        </div>
        <div class="left"></div>
        <div class="right"></div>
    </div>
     .clearfix{
            zoom: 1;
        }
        .clearfix::after{
            clear: both;
            content: '.';
            visibility: hidden;
            display: block;
            overflow: hidden;
            height: 0;
        }
        .content{
            width: 100%;
            height: 100%;
        }
        .content,.left, .right{
            float: left;
        }
        .center{
            margin: 0 100px 0 100px;
            min-height: 400px;
            background: goldenrod;
        }
        .left, .right{
            width: 100px;
            height: 100px;
            background: forestgreen;
        }
        .left{
            margin-left: -100%;
        }
        .right{
            margin-left: -100px;
        }
  ```

  - 使用 flex 布局

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

5）**flex：flex-grow 和 flex-shrink 和 flex-basis 的缩写方式 默认为 0 1 auto**

6）align-self：设置子元素自己的垂直排列方式，默认为盒子的 align-items 的值

:warning:：设置 flex 布局后，子元素的 float，clear，vertical-align 都无效

## CSS3 新增属性用法的整理：

1、box-shadow（阴影效果）

2、border-color（为边框设置多种颜色）

3、border-image（图片边框）

4、text-shadow（文本阴影）

5、text-overflow（文本截断）

6、word-wrap（自动换行）

7、border-radius（圆角边框）

8、opacity（透明度）

9、box-sizing（控制盒模型的组成模式）

10、resize（元素缩放）

11、outline（外边框）

12、background-size（指定背景图片尺寸）

13、background-origin（指定背景图片从哪里开始显示）

14、background-clip（指定背景图片从什么位置开始裁剪）

15、background（为一个元素指定多个背景）

16、hsl（通过色调、饱和度、亮度来指定颜色颜色值）

17、hsla（在 hsl 的基础上增加透明度设置）

18、rgba（基于 rgb 设置颜色，a 设置透明度）

## 移动端响应式布局开发的方案

- media
- rem
- vh / vw 类似百分比布局

## content-visibility: auto

使用 content-visibility 可以跳过渲染屏幕之外的内容
