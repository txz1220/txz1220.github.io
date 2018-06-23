---
title: CSS3
categories:
- 技术
- 前端基础知识
- css3
tags:
- CSS3
---

### 引入方式：

1、内联方式 Inline Styles

><p style="color:#f00">这一行的字体颜色将显示为红色</p>

2、内部样式块对象 Embedding a Style Block

```html
<style>
    .test2 {
        color: #000;
    }
</style>
```
<!--more-->
3、外部样式表 Linking to a Style Sheet

你可以先建立外部样式表文件*.css，然后使用 HTML 的 link 对象。或者使用 @import 来引入。 示例代码：

```html
<!-- Use link elements -->
<link rel="stylesheet" href="core.css">

<!-- Use @imports -->
<style>
  @import url("more.css");
</style>
```

#### 二、选择器权重

权重主要分为 4 个等级：
- 第一等：代表内联样式，如: style=""，权值为1000
- 第二等：代表ID选择器，如：#content，权值为100
- 第三等：代表类，伪类和属性选择器，如.content，权值为10
- 第四等：代表类型选择器和伪元素选择器，如div p，权值为1


### 动画

#### CSS3 @keyframes 规则

要创建CSS3动画，你将不得不了解@keyframes规则。
@keyframes规则是用来创建动画。 @keyframes规则内指定一个 CSS样式和动画将逐步从目前的样式更改为新的样式。

#### CSS3 动画


当在@keyframe创建动画，把它绑定到一个选择器，否则动画不会有任何效果。
指定至少这两个 CSS3 的动画属性绑定向一个选择器：
- 规定动画的名称
- 规定动画的时长
- 
例子：

```css
#animated_div {
    animation: animated_div 5s infinite;
    -moz-animation: animated_div 5s infinite;
    -webkit-animation: animated_div 5s infinite;
}
```


##### 常用属性

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsbthjfx5bj30me0c1dgs.jpg)


#### 第一部分：CSS Transition

在CSS 3引入Transition（过渡）这个概念之前，CSS是没有时间轴的。也就是说，所有的状态变化，都是即时完成。

```css
img{
    height:15px;
    width:15px;
}

img:hover{
    height: 450px;
    width: 450px;
}

```

transition的作用在于，指定状态变化所需要的时间。

```css
img{
    transition: 1s;
}
```


我们还可以指定transition适用的属性，比如只适用于height。

```css
img{
    transition: 1s height;
}
```


###### transition-delay

在同一行transition语句中，可以分别指定多个属性。

```css
img{
    transition: 1s height, 1s width;
}
```
我们希望，让height先发生变化，等结束以后，再让width发生变化。实现这一点很容易，就是为width指定一个delay参数。
```css
img{
    transition: 1s height, 1s 1s width;
}
```


###### transition-timing-function

ransition的状态变化速度（又称timing function），默认不是匀速的，而是逐渐放慢，这叫做ease。

除了ease以外，其他模式还包括:

（1）linear：匀速

（2）ease-in：加速

（3）ease-out：减速

（4）cubic-bezier函数：自定义速度模式



##### transition的各项属性:

transition的完整写法如下

```css
img{
    transition: 1s 1s height ease;
}

```


###### transition的局限

transition的优点在于简单易用，但是它有几个很大的局限。

（1）transition需要事件触发，所以没法在网页加载时自动发生。

（2）transition是一次性的，不能重复发生，除非一再触发。

（3）transition只能定义开始状态和结束状态，不能定义中间状态，也就是说只有两个状态。

（4）一条transition规则，只能定义一个属性的变化，不能涉及多个属性。

CSS Animation就是为了解决这些问题而提出的。


#### 第二部分：CSS Animation


首先，CSS Animation需要指定动画一个周期持续的时间，以及动画效果的名称。
```css
div:hover {
  animation: 1s rainbow;
}
```

上面代码表示，当鼠标悬停在div元素上时，会产生名为rainbow的动画效果，持续时间为1秒。为此，我们还需要用keyframes关键字，定义rainbow效果。

```css
@keyframes rainbow {
  0% { background: #c00; }
  50% { background: orange; }
  100% { background: yellowgreen; }
}

```


默认情况下，动画只播放一次。加入infinite关键字，可以让动画无限次播放。

```css
div:hover {
  animation: 1s rainbow infinite;
}
```
也可以指定动画具体播放的次数，比如3次。

```css
div:hover {
  animation: 1s rainbow 3;
}
```


#####  animation-fill-mode

动画结束以后，会立即从结束状态跳回到起始状态。如果想让动画保持在结束状态，需要使用animation-fill-mode属性。
```css
div:hover {
  animation: 1s rainbow forwards;
}
```

forwards表示让动画停留在结束状态，效果如下。


animation-fill-mode还可以使用下列值:

（1）none：默认值，回到动画没开始时的状态。

（2）backwards：让动画回到第一帧的状态。

（3）both: 根据animation-direction（见后）轮流应用forwards和backwards规则。


##### animation-direction

动画循环播放时，每次都是从结束状态跳回到起始状态，再开始播放。animation-direction属性，可以改变这种行为。

下面看一个例子，来说明如何使用animation-direction。假定有一个动画是这样定义的。

```css
@keyframes rainbow {
  0% { background-color: yellow; }
  100% { background: blue; }
}
```

默认情况是，animation-direction等于normal。
此外，还可以等于取alternate、reverse、alternate-reverse等值。它们的含义见下图（假定动画连续播放三次）。
简单说，animation-direction指定了动画播放的方向，最常用的值是normal和reverse。浏览器对其他值的支持情况不佳，应该慎用。


##### animation的各项属性

同transition一样，animation也是一个简写形式。

```css
div:hover {
  animation: 1s 1s rainbow linear 3 forwards normal;
}
```


### 下面来介绍下边框：

CSS3 Border（边框）主要有以下属性：

- border-radius
- box-shadow
- border-image

border-radius （圆角边框）

```css
border-radius: 25px;
```


box-shadow （边框阴影）
```css
box-shadow: 15px 15px 5px #888245;
```
border-image （边框图片）

```css
-moz-border-image: url(/images/border.png) 30 30 round; /* Firefox */
    -webkit-border-image: url(/images/border.png) 30 30 round; /* Safari and Chrome */
    -o-border-image: url(/images/border.png) 30 30 round; /* Opera */
    border-image: url(/images/border.png) 30 30 round;
 ```



### 接下来是背景知识：

主要是2个背景属性：
- background-size
- background-origin

background-size

该属性规定背景图片的尺寸。
在 CSS3 之前，背景图片的尺寸是由图片的实际尺寸决定的。在 CSS3 中，可以规定背景图片的尺寸，这就允许我们在不同的环境中重复使用背景图片。
您能够以像素或百分比规定尺寸。如果以百分比规定尺寸，那么尺寸相对于父元素的宽度和高度。


background-origin

该属性指定了背景图像的位置区域。
content-box, padding-box,和 border-box 区域内可以放置背景图像。

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsg8xh9xoej30ad05v0to.jpg)



### 字体

以前 CSS3 的版本，网页设计师不得不使用用户计算机上已经安装的字体。
使用 CSS3，网页设计师可以使用他/她喜欢的任何字体。
当你发现您要使用的字体文件时，只需简单的将字体文件包含在网站中，它会自动下载给需要的用户。
您所选择的字体在新的 CSS3 版本有关于@font-face规则描述。
您"自己的"的字体是在 CSS3 @font-face 规则中定义的。


在 @font-face 规则中，您必须首先定义字体的名称（比如 FontAwesome ），然后指向该字体文件 fontawesome-webfont.woff 。

```css
@font-face {
    font-family: 'FontAwesome';
    src: url('fonts/fontawesome-webfont.woff');
}
```


### 文本效果


SS3 文本效果是这样一个术语用来在正常的文本中实现一些额外的特性。
主要是两个属性的 CSS3 文本效果,如下:
- text-shadow
- word-wrap


text-shadow

文本阴影。 您指定了水平阴影，垂直阴影，模糊的距离，以及阴影的颜色：
```css
.text-shadow {
    text-shadow: 10px 10px 10px #6AAFCF;
}
```


word-wrap
换行。 CSS3中，自动换行属性允许您强制文本换行 - 即使这意味着分裂它中间的一个字：

```css
.word-wrap {
    word-wrap: break-word;
    width: 150px;
    border: 1px solid #ff0000;
}
```

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsg9d9zxo6j30n10gc0tw.jpg)




### 2D 转换


CSS3 2D转换，我们可以斜拉(skew)，缩放(scale)，旋转(rotate)以及位移(translate)元素。

常用 2D 变换方法：
- translate()
- rotate()
- scale()
- skew()
- matrix()

translate()
translate()方法，根据左(X轴)和顶部(Y轴)位置给定的参数，从当前元素位置移动


rotate()
rotate()方法，在一个给定度数沿着元素中心顺时针旋转的元素。负值是允许的，这样是元素逆时针旋转。

```css
.rotate
{
    transform:rotate(30deg);
    -ms-transform:rotate(30deg); /* IE 9 */
    -webkit-transform:rotate(30deg); /* Safari and Chrome */
}
```

scale()
scale()方法，该元素增加或减少的大小，取决于宽度（X轴）和高度（Y轴）的参数：
```css
.scale
{
    transform: scale(2,4);
    -ms-transform: scale(2,4); /* IE 9 */
    -webkit-transform: scale(2,4); /* Safari and Chrome */
}
```

skew()
skew()方法，该元素会根据横向（X轴）和垂直（Y轴）线参数给定角度：
```css
.skew
{
    transform:skew(30deg,20deg);
    -ms-transform:skew(30deg,20deg); /* IE 9 */
    -webkit-transform:skew(30deg,20deg); /* Safari and Chrome */
}
```

matrix()
matrix()方法和2D变换方法合并成一个。
matrix 方法有六个参数，包含旋转，缩放，移动（平移）和倾斜功能。




### 3D 转换

CSS3 3D Transform,用于 3 维动画或旋转。
CSS3 3D 转换是一个属性,用于改变元素的实际形式。这个特性可以改变元素的形状、大小和位置。
主要有下列方法：
- rotateX()
- rotateY()
- rotateZ()


注意：Internet Explorer 10 和 Firefox 支持 3D 转换； Chrome 和 Safari 必须添加前缀 -webkit-； Opera 还不支持 3D 转换(支持 2D 转换 )

rotateX()
rotateX()方法，围绕其在一个给定度数X轴旋转的元素。
```css
.rotate-x {
    transform: rotateX(60deg);
    -webkit-transform: rotateX(120deg); /* Safari and Chrome */
}
```

y、z轴 类似。

rotate3d()
otate3d(x,y,z,a)中取值说明：

- x：是一个0到１之间的数值，主要用来描述元素围绕X轴旋转的矢量值；
- y：是一个０到１之间的数值，主要用来描述元素围绕Y轴旋转的矢量值；
- z：是一个０到１之间的数值，主要用来描述元素围绕Z轴旋转的矢量值；
- a：是一个角度值，主要用来指定元素在3D空间旋转的角度，如果其值为正值，元素顺时针旋转，反之元素逆时针旋转。 面介绍的三个旋转函数功能等同：



<完>