---
title: CSS 各种用法
categories:
- 技术
- 前端基础知识
- css 各种用法
tags:
- CSS 各种用法
---


### 一、CSS写自适应大小的正方形

```html
<style type="text/css">
/* 以图片为例
background 写法 */
	.img{
		width: 100%;
		height: 0;
		padding-bottom: 100%;		//关键所在
		overflow: hidden;
		background:url(../res/images/haha.png) center/100% 100% no-repeat;
	}
	.img img{
		width: 100%;
	}

/* img 写法 */
	.img{
		position: relative;
		width: 100%;
		height: 0;
		padding-bottom: 100%;		//关键所在
		overflow: hidden;
	}
	.img img{
		position: absolute;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
	}
</style>
<div class="img"></div>
```
<!--more-->


### 二、多列等高

代码：

```css

<style type="text/css">
	.web_width{
		width: 100%;
		overflow: hidden;			//关键所在
	}
	.left{
		float: left;
		width: 20%;
		min-height: 10em;
		background: #66afe9;
		padding-bottom: 2000px;		//关键所在
		margin-bottom: -2000px;		//关键所在
	}
	.right{
		float: right;
		width: 80%;
		height: 20em;
		background: #f00;
	}
</style>
```

padding补偿法

在高度小的元素上加一个数值为正padding-bottom和一个数值为负margin-bottom，再在父级加上overflow: hidden隐藏子元素超出的padding-bottom

>padding-bottom、margin-bottom之和要等于0（建议值不要太大，够用就行）


### 三、绘制三角形

代码

```html
<style type="text/css">
.demo {
	width: 0;
	height: 0;
	border-left: 50px solid transparent;
	border-right: 50px solid transparent;
	border-bottom: 50px solid red;
}
</style>
```

>利用盒模型中的border属性
>当盒模型的width/height为 0 时，border 边的形状是一个三角形，通过只设置三条边的 border ，并将所绘制的三角形相邻两边的 border 的颜色设置为 transparent, 最后通过调整border-width的比例绘制自己所需要的三角形
