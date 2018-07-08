---
title: CSS专业技巧
categories:
- 技术
- css
- CSS专业技巧
tags:
- css
- CSS专业技巧
---


## 使用CSS复位

CSS复位可以在不同的浏览器上保持一致的样式风格。您可以使用CSS reset 库[normalize](http://necolas.github.io/normalize.css/)等，也可以使用一个更简化的复位方法：

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
```

注意：如果你遵循接下来继承 box-sizing讲解的这个技巧, 你不需要在以上代码中添加 box-sizing 属性。

### 继承 box-sizing

从 html 元素继承 box-sizing ：

```css
html {
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}
```
<!--more-->

### 使用unset而不是重置所有属性

重置元素的属性时，不需要重置每个单独的属性：

```css
button {
  all: unset;
}
```

>所有速记在IE11中不被支持，目前正在考虑Edge的支持。 IE11不支持unset。

### 使用 :not() 选择器来决定表单是否显示边框

先为元素添加边框

```css
/* 添加边框 */
.nav li {
  border-right: 1px solid #666;
}

```

然后，为最后一个元素去除边框

```css
/* 去掉边框 */
.nav li:last-child {
  border-right: none;
}

```


不过不要这么做，使用 :not() 伪类来达到同样的效果：

```css
.nav li:not(:last-child) {
  border-right: 1px solid #666;
}
```

### 为 body 元素添加行高

不必为每一个 <p>，<h*> 元素逐一添加 line-height，直接添加到 body 元素：
```css
body {
  line-height: 1.5;
}
```
文本元素可以很容易地继承 body 的样式。

### 垂直居中任何元素

```css
html,
body {
  height: 100%;
  margin: 0;
}

body {
  -webkit-align-items: center;  
  -ms-flex-align: center;  
  align-items: center;
  display: -webkit-flex;
  display: flex;
}
```


### 逗号分隔列表

使列表的每项都由逗号分隔：

```css
ul > li:not(:last-child)::after {
  content: ",";
}
```

> 这一技巧对于无障碍，特别是屏幕阅读器而言并不理想。而且复制粘贴并不会带走CSS生成的内容,需要注意。

### 使用负的 nth-child 来选择元素

使用负的 nth-child 可以选择 1 至 n 个元素。

```css
li {
  display: none;
}

/* 选择第 1 至第 3 个元素并显示出来 */
li:nth-child(-n+3) {
  display: block;
}
```

### 使用 “形似猫头鹰” 的选择器

这个名字可能比较陌生，不过通用选择器 (*) 和 相邻兄弟选择器 (+) 一起使用，效果非凡：

```css
* + * {
  margin-top: 1.5em;
}
```

在此示例中，文档流中的所有的相邻兄弟元素将都将设置 margin-top: 1.5em 的样式。


### 使用 max-height 来建立纯 CSS 的滑块

```css
.slider {
  max-height: 200px;
  overflow-y: hidden;
  width: 300px;
}

.slider:hover {
  max-height: 600px;
  overflow-y: scroll;
}
```

### 创造格子等宽的表格

table-layout: fixed 可以让每个格子保持等宽：

```css
.calendar {
  table-layout: fixed;
}
```

### 利用 Flexbox 去除多余的外边距

与其使用 nth-， first-， 和 last-child 去除列之间多余的间隙，不如使用 flexbox 的 space-between 属性：

```css
.list {
  display: flex;
  justify-content: space-between;
}

.list .person {
  flex-basis: 23%;
}
```


### 利用属性选择器来选择空链接
当 `<a> `元素没有文本内容，但有 href 属性的时候，显示它的 href 属性：

```css
a[href^="http"]:empty::before {
  content: attr(href);
}
```

### 给 “默认” 链接定义样式
给 “默认” 链接定义样式：

```css
a[href]:not([class]) {
  color: #008000;
  text-decoration: underline;
}
```

### 一致垂直节奏

通用选择器 (*) 跟元素一起使用，可以保持一致的垂直节奏：

```css
.intro > * {
  margin-bottom: 1.25rem;
}
```


### 固定比例盒子

要创建具有固定比例的一个盒子，所有你需要做的就是给 div 设置一个 padding：

```css
.container {
  height: 0;
  padding-bottom: 20%;
  position: relative;
}

.container div {
  border: 2px dashed #ddd;	
  height: 100%;
  left: 0;
  position: absolute;
  top: 0;
  width: 100%;
}
```

>使用20％的padding-bottom使得框等于其宽度的20％的高度。与视口宽度无关，子元素的div将保持其宽高比（100％/ 20％= 5:1）。


### 为破碎图象定义样式

只要一点CSS就可以美化破碎的图象：

```css
img::before {  
  content: "We're sorry, the image below is broken :(";
  display: block;
  margin-bottom: 10px;
}

img::after {  
  content: "(url: " attr(src) ")";
  display: block;
  font-size: 12px;
}
```


### 用 rem 来调整全局大小；用 em 来调整局部大小

在根元素设置基本字体大小后 (html { font-size: 100%; }), 使用 em 设置文本元素的字体大小:

```css
h2 { 
  font-size: 2em;
}

p {
  font-size: 1em;
}
```

然后设置模块的字体大小为 rem:

```css
article {
  font-size: 1.25rem;
}

aside .module {
  font-size: .9rem;
}
```

>现在，每个模块变得独立，更容易、灵活的样式便于维护。
>rem是CSS3新增的一个相对单位（root em，根em），这个单位引起了广泛关注。这个单位与em有什么区别呢？区别在于使用rem为元素设定字体大小时，仍然是相对大小，但相对的只是HTML根元素。这个单位可谓集相对大小和绝对大小的优点于一身，通过它既可以做到只修改根元素就成比例地调整所有字体大小，又可以避免字体大小逐层复合的连锁反应。


### 使用选择器:root来控制字体弹性

在响应式布局中，字体大小应需要根据不同的视口进行调整。你可以计算字体大小根据视口高度的字体大小和宽度，这时需要用到:root:
```css
:root {
  font-size: calc(1vw + 1vh + .5vmin);
}
```

现在，您可以使用 root em

```css
body {
  font: 1rem/1.6 sans-serif;
}
```




### 使用指针事件來控制鼠标事件

指针事件允許您指定鼠标如何与其触摸的元素进行交互。 要禁用按钮上的默认指针事件，例如：

```css
.button-disabled {
  opacity: .5;
  pointer-events: none;
}
```


