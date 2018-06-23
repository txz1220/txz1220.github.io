---
title: Sass学习2
categories:
- 技术
- Sass
tags:
- Sass
---

### 一、Sass的基本特性

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fs9glhsm5xj30lv08jjyt.jpg)


上图非常清楚告诉了大家，Sass 的变量包括三个部分：

1.声明变量的符号“$”
2.变量名称
3.赋予变量的值

<!--more-->
#### 1.1普通变量和默认变量：

1、普通变量
定义之后可以在全局范围内使用。

2、默认变量
sass 的默认变量仅需要在值后面加上 !default 即可。

sass 的默认变量一般是用来设置默认值，然后根据需求来覆盖的，覆盖的方式也很简单，只需要在默认变量之前重新声明下变量即可。
```scss
$baseLineHeight: 2;
$baseLineHeight: 1.5 !default;
body{
    line-height: $baseLineHeight; 
}
```
#### 1.2变量的调用

#### 1.3 全局比那里和局部变量
```scss
//SCSS
$color: orange !default;//定义全局变量(在选择器、函数、混合宏...的外面定义的变量为全局变量)
.block {
  color: $color;//调用全局变量
}
em {
  $color: red;//定义局部变量
  a {
    color: $color;//调用局部变量
  }
}
span {
  color: $color;//调用全局变量
}
```

**什么时候声明变量？**

我的建议，创建变量只适用于感觉确有必要的情况下。不要为了某些骇客行为而声明新变量，这丝毫没有作用。只有满足所有下述标准时方可创建新变量：

- 该值至少重复出现了两次；
- 该值至少可能会被更新一次；
- 该值所有的表现都与变量有关（非巧合）。
基本上，没有理由声明一个永远不需要更新或者只在单一地方使用变量。


### 嵌套-选择器嵌套

>Sass 中还提供了选择器嵌套功能，但这也并不意味着你在 Sass 中的嵌套是无节制的，因为你嵌套的层级越深，编译出来的 CSS 代码的选择器层级将越深，这往往是大家不愿意看到的一点。这个特性现在正被众多开发者滥用。

Sass 的嵌套分为三种：
- 选择器嵌套
- 属性嵌套
- 伪类嵌套


#### 选择器嵌套

假设我们有一段这样的结构：
```html
<header>
<nav>
    <a href=“##”>Home</a>
    <a href=“##”>About</a>
    <a href=“##”>Blog</a>
</nav>
<header>
```
想选中 header 中的 a 标签，在 Sass 中，就可以使用选择器的嵌套来实现：
```scss
nav {
  a {
    color: red;

    header & {
      color:green;
    }
  }  
}
```

#### 属性嵌套

Sass 中还提供属性嵌套，CSS 有一些属性前缀相同，只是后缀不一样，比如：border-top/border-right，与这个类似的还有 margin、padding、font 等属性。假设你的样式中用到了：

```css
.box {
    border-top: 1px solid red;
    border-bottom: 1px solid green;
}
```

在 Sass 中我们可以这样写：
```scss
.box {
  border: {
   top: 1px solid red;
   bottom: 1px solid green;
  }
}
```

#### 伪类嵌套

```scss
.clearfix{
&:before,
&:after {
    content:"";
    display: table;
  }
&:after {
    clear:both;
    overflow: hidden;
  }
}
```

避免选择器嵌套：
>选择器嵌套最大的问题是将使最终的代码难以阅读。开发者需要花费巨大精力计算不同缩进级别下的选择器具体的表现效果。
选择器越具体则声明语句越冗长，而且对最近选择器的引用(&)也越频繁。在某些时候，出现混淆选择器路径和探索下一级选择器的错误率很高，这非常不值得。



#### 混合宏-声明混合宏

如果你的整个网站中有几处小样式类似，比如颜色，字体等，在 Sass 可以使用变量来统一处理，那么这种选择还是不错的。但当你的样式变得越来越复杂，需要重复使用大段的样式时，使用变量就无法达到我们目了。这个时候 Sass 中的混合宏就会变得非常有意义。

1、声明混合宏

不带参数混合宏：

在 Sass 中，使用“@mixin”来声明一个混合宏。如：

```scss
@mixin border-radius{
    -webkit-border-radius: 5px;
    border-radius: 5px;
}
```
其中 @mixin 是用来声明混合宏的关键词，有点类似 CSS 中的 @media、@font-face 一样。border-radius 是混合宏的名称。大括号里面是复用的样式代码。

带参数混合宏：

除了声明一个不带参数的混合宏之外，还可以在定义混合宏时带有参数，如：
```scss
@mixin border-radius($radius:5px){
    -webkit-border-radius: $radius;
    border-radius: $radius;
}
```

复杂的混合宏：

上面是一个简单的定义混合宏的方法，当然， Sass 中的混合宏还提供更为复杂的，你可以在大括号里面写上带有逻辑关系，帮助更好的做你想做的事情,如：
```scss
@mixin box-shadow($shadow...) {
  @if length($shadow) >= 1 {
    @include prefixer(box-shadow, $shadow);
  } @else{
    $shadow:0 0 4px rgba(0,0,0,.3);
    @include prefixer(box-shadow, $shadow);
  }
}
```


#### 混合宏-调用混合宏

在 Sass 中通过 @mixin 关键词声明了一个混合宏，那么在实际调用中，其匹配了一个关键词“@include”来调用声明好的混合宏。例如在你的样式中定义了一个圆角的混合宏“border-radius”:

```scss
@mixin border-radius{
    -webkit-border-radius: 3px;
    border-radius: 3px;
}
```
在一个按钮中要调用定义好的混合宏“border-radius”，可以这样使用:

```scss
button {
    @include border-radius;
}
```


#### 混合宏的参数--传一个不带值的参数

```scss
@mixin border-radius($radius){
  -webkit-border-radius: $radius;
  border-radius: $radius;
}
```
在混合宏“border-radius”中定义了一个不带任何值的参数“$radius”。

在调用的时候可以给这个混合宏传一个参数值：
```scss
.box {
  @include border-radius(3px);
}
```

#### 混合宏的参数--传一个带值的参数

#### Sass 混合宏除了能传一个参数之外，还可以传多个参数，如：
```scss
@mixin center($width,$height){
  width: $width;
  height: $height;
  position: absolute;
  top: 50%;
  left: 50%;
  margin-top: -($height) / 2;
  margin-left: -($width) / 2;
}
```


有一个特别的参数“…”。当混合宏传的参数过多之时，可以使用参数来替代，如：

```scss
@mixin box-shadow($shadows...){
  @if length($shadows) >= 1 {
    -webkit-box-shadow: $shadows;
    box-shadow: $shadows;
  } @else {
    $shadows: 0 0 2px rgba(#000,.25);
    -webkit-box-shadow: $shadow;
    box-shadow: $shadow;
  }
}
```

#### 继承

在 Sass 中是通过关键词 “@extend”来继承已存在的类样式块，从而实现代码的继承。如下所示：

```scss
//SCSS
.btn {
  border: 1px solid #ccc;
  padding: 6px 10px;
  font-size: 14px;
}

.btn-primary {
  background-color: #f36;
  color: #fff;
  @extend .btn;
}

.btn-second {
  background-color: orange;
  color: #fff;
  @extend .btn;
}
```

#### 占位符   （重点）


Sass 中的占位符 %placeholder 功能是一个很强大，很实用的一个功能，这也是我非常喜欢的功能。他可以取代以前 CSS 中的基类造成的代码冗余的情形。因为 %placeholder 声明的代码，如果不被 @extend 调用的话，不会产生任何代码。来看一个演示：

```scss
%mt5 {
  margin-top: 5px;
}
%pt5{
  padding-top: 5px;
}
```
这段代码没有被 @extend 调用，他并没有产生任何代码块，只是静静的躺在你的某个 SCSS 文件中。只有通过 @extend 调用才会产生代码：

```scss
//SCSS
%mt5 {
  margin-top: 5px;
}
%pt5{
  padding-top: 5px;
}

.btn {
  @extend %mt5;
  @extend %pt5;
}

.block {
  @extend %mt5;

  span {
    @extend %pt5;
  }
}
```


#### 混合宏 VS 继承 VS 占位符


##### a) Sass 中的混合宏使用

>编译出来的 CSS 清晰告诉了大家，他不会自动合并相同的样式代码，如果在样式文件中调用同一个混合宏，会产生多个对应的样式代码，造成代码的冗余，这也是 CSSer 无法忍受的一件事情。不过他并不是一无事处，他可以传参数。

个人建议：如果你的代码块中涉及到变量，建议使用混合宏来创建相同的代码块。


##### b) Sass 中继承

>总结：使用继承后，编译出来的 CSS 会将使用继承的代码块合并到一起，通过组合选择器的方式向大家展现，比如 .mt, .block, .block span, .header, .header span。这样编译出来的代码相对于混合宏来说要干净的多，也是 CSSer 期望看到。但是他不能传变量参数。

个人建议：如果你的代码块不需要专任何变量参数，而且有一个基类已在文件中存在，那么建议使用 Sass 的继承。

##### c) 占位符

>总结：编译出来的 CSS 代码和使用继承基本上是相同，只是不会在代码中生成占位符 mt 的选择器。那么占位符和继承的主要区别的，“占位符是独立定义，不调用的时候是不会在 CSS 中产生任何代码；继承是首先有一个基类存在，不管调用与不调用，基类的样式都将会出现在编译出来的 CSS 代码中。”


#### [Sass]插值#{}

```scss
$properties: (margin, padding);
@mixin set-value($side, $value) {
    @each $prop in $properties {
        #{$prop}-#{$side}: $value;
    }
}
.login-box {
    @include set-value(top, 14px);
}
```

它可以让变量和属性工作的很完美，上面的代码编译成 CSS：

```css

.login-box {
    margin-top: 14px;
    padding-top: 14px;
}
```


### Sass的基本特性-运算

#### [Sass运算]加法

加法运算是 Sass 中运算中的一种，在变量或属性中都可以做加法运算。如：

```scss
.box {
  width: 20px + 8in;
}
```
编译出来的 CSS:
```css
.box {
  width: 788px;
}
```
但对于携带不同类型的单位时，在 Sass 中计算会报错，如下例所示：
```scss
.box {
  width: 20px + 1em;
}
```

#### [Sass运算]减法

Sass 的减法运算和加法运算类似，我们通过一个简单的示例来做阐述：

```scss
$full-width: 960px;
$sidebar-width: 200px;

.content {
  width: $full-width -  $sidebar-width;
}
```

#### [Sass运算]乘法

Sass 中的乘法运算和前面介绍的加法与减法运算还略有不同。虽然他也能够支持多种单位（比如 em ,px , %），但当一个单位同时声明两个值时会有问题。比如下面的示例：

```scss
.box {
  width:10px * 2px;  
}
```

如果进行乘法运算时，两个值单位相同时，只需要为一个数值提供单位即可。上面的示例可以修改成：

```scss
.box {
  width: 10px * 2;
}
```

#### [Sass运算]除法

Sass 的乘法运算规则也适用于除法运算。不过除法运算还有一个特殊之处。众所周知“/”符号在 CSS 中已做为一种符号使用。因此在 Sass 中做除法运算时，直接使用“/”符号做为除号时，将不会生效，编译时既得不到我们需要的效果，也不会报错。一起先来看一个简单的示例：

```scss
.box {
  width: 100px / 2;  
}
```
这样的结果对于大家来说没有任何意义。要修正这个问题，只需要给运算的外面添加一个小括号( )即可：

```scss
.box {
  width: (100px / 2);  
}
```
除了上面情况带有小括号，“/”符号会当作除法运算符之外，如果“/”符号在已有的数学表达式中时，也会被认作除法符号。如下面示例：

```scss
.box {
  width: 100px / 2 + 2in;  
}
```
另外，在 Sass 除法运算中，当用变量进行除法运算时，“/”符号也会自动被识别成除法，如下例所示：

```scss
$width: 1000px;
$nums: 10;

.item {
  width: $width / 10;  
}

.list {
  width: $width / $nums;
}
```