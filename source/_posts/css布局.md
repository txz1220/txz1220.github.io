---
title: CSS布局知识
categories:
- 技术
- css布局
tags:
- css布局
---


-------------

### display

设置元素的显示方式

display | 默认宽度 | 可设置宽高 | 起始位置
------------ | -------------|---------|---------
block | 父元素宽度|是|换行
inline | 内容宽度|否|同行
inline-block | 内容宽度|是|同行

<!--more-->

#### display:block

默认为block的元素：<div>, <p>, <h1> ~ <h6>, <ul>, <form>

#### display:inline

默认为inline的元素：<span>, <a>, <label>, <cite>, <em>

#### display:inline-block

默认为inline-block的元素：`<input>`, `<textarea>`, `<select>`, `<button>`



#### display:none

设置元素不显示

>display:none 与 visibility:hidden 的区别为 display:none 不显示且不占位，但 visibility:hidden 不显示但占位。


### position

position 用于设置定位的方式与top right bottom left z-index 则用于设置参照物位置（必须配合定位一同使用）。

三种定位形式
- 静态定位（static）
- 相对定位（relative）
- 绝对定位（absolute、fixed）

#### position:relative

相对定位的元素仍在文档流之中，并按照文档流中的顺序进行排列。
参照物为元素本身的位置。

>最常用的目的为改变元素层级和设置为绝对定位的参照物


#### position:absolute

建立以包含块为基准的定位，其随即拥有偏移属性和 z-index 属性。
- 默认宽度为内容宽度
- 脱离文档流
- 参照物为第一个定位祖先或根元素（<html> 元素）


#### position:fixed
- 默认宽度为内容宽度
- 脱离文档流
- 参照物为视窗

#### z-index

其用于设置 Z 轴上得排序，默认值为 0 但可设置为负值。（如不做设置，则按照文档流的顺序排列。后面的元素将置于前面的元素之上）


### float

CSS 中规定的定位机制，其可实现块级元素同行显示并存在于文档流之中。浮动仅仅影响文档流中下一个紧邻的元素。

#### clear

clear: both | left | right | none | inherit

- 应用于后续元素
- 应用于块级元素（block）

使用方法：

- 优先级自上而下
- clearfix 于父元素
- 浮动后续空白元素 .emptyDiv {clear: both}
- 为受到影响的元素设置 width: 100% overflow: hidden 也可
- 块级元素可以使用 <br> 不建议使用，影响 HTML 结构


### flex

专门文章介绍了，在这里不做介绍。