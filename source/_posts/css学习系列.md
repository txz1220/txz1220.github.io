---
title: css学习系列
categories:
- 技术
- css      
tags:
- css
---

## 语法

### 语法    

```css
/* 选择器 */
.m-userlist {
  /* 属性声明 */
  margin: 0 0 30px;
  /* 属性名:属性值; */
}
.m-userlist .list {
  position: relative;
  height: 100px;
  overflow: hidden;
}
```
<!--more-->

### 浏览器私有属性

- Google Chrome, Safari (-webkit)
- Firefox (-moz-)
- IE (-ms-)
- Opera (-o-)

```css
.pic {
  -webkit-transform: rotate(-3deg);
  -ms-transform: rotate(-3deg);
  transform: rotate(-3deg);
}
```

>CSS 预处理器（Sass，Less，Stylus）或编辑器插件可自动添加浏览器厂商的私有属性前缀。


@规则

常用的规则:

- @media （用于响应式布局）
- @keyframes （CSS 动画的中间步骤）
- @font-face （引入外部字体）


其他规则（不常用）

- @import
- @charset
- @namespace
- @page
- @supports
- @document

### 选择器

#### 简单选择器

标签选择器

类选择器

id 选择器

通配符选择器   *

属性选择器

[attr] 或 [attr=val] 来选择相应的元素。#nav{...} 既等同于 [id=nav]{...}。

[attr~=val] 可选用与选择包含 val 属性值的元素，像class="title sports" 与 class="sports"。.sports{...} 既等同于 [class~=sports]{...}

[attr|=val] 可以选择val开头及开头紧接-的属性值

[attr^=val] 可选择以val开头的属性值对应的元素，如果值为符号或空格则需要使用引号 ""。

[attr$=val] 可选择以val结尾的属性值对应的元素。

[attr*=val] 可选择以包含val属性值对应的元素。

伪类选择器
常用伪类选择器：

- :link IE6+
- :visited IE7+
- :hover IE6中仅可用于链接
- :active IE6/7中仅可用于链接
- :enabled IE9+
- :disabled IE9+
- :checked IE9+
- :first-child IE8+
- :last-child IE9+
- :nth-child(even) 可为 odd even 或数字 IE9+
- :nth-last-child(n) n从 0 开始计算 IE9+
- :only-child 仅选择唯一的元素 IE9+
- :only-of-type IE9+
- :first-of-type IE9+
- :last-of-type IE9+
- :nth-of-type(even) IE9+
- :nth-last-of-type(2n) IE9+

>element:nth-of-type(n) 指父元素下第 n 个 element 元素，element:nth-child(n) 指父元素下第 n 个元素且元素为 element，若不是，选择失败


其他选择器
伪元素选择器
注意与伪类学则器的区分。

- ::first-letter IE6+
- ::first-line IE6+
- ::before{content: "before"} 需与 content 一同使用 IE8+
- ::after{content: "after"} 需与 content 一同使用 IE8+
- ::selection 被用户选中的内容（鼠标选择高亮属性）IE9+ Firefox需用 -moz 前缀

组合选择器
- 后代选择器 .main h2 {...}，使用 表示 IE6+
- 子选择器 .main>h2 {...}，使用>表示 IE7+
- 兄弟选择器 h2+p {...}，使用+表示 IE7+
h2~p {...}，使用~表示（此标签无需紧邻）IE7+


选择器分组

```css
h1, h2, h3 {color: red;}
```

#### 继承、优先、层级

子元素继承父元素的样式，但并不是所有属性都是默认继承的。通过文档中的 inherited: yes 来判断属性是否可以自动继承。

自动继承属性：

- color
- font
- text-align
- list-style

非继承属性：

- background
- border
- position


### 文本

#### 字体

改变字号

```css
div
  font-size 12px
  p#sample0
    font-size 16px
  p#sample1
    font-size 2em
  p#sample2
    font-size 200%
```

>以上两值在开发中并不常用。2em 与 200% 都为父元素默认大小的两倍（参照物为父元素的字体大小 12px）。


改变字体

font-family: arial, Verdana, sans-serif;
>优先使用靠前的字体

加粗字体

font-weight: normal;
font-weight: bold;

倾斜字体
font-style: normal | italic | oblique | inherit

更改行距
```css
/* length 类型 */
line-height: 40px;
line-height: 3em;
/* percentage 类型 */
line-height: 300%;
/* number 类型 */
line-height: 3;
```

>当line-height为 number 类型时，子类直接继承其数值（不计算直接继承）。 而当为 percentage 类型时，子类则会先计算再显示（先计算后继承）。

字间距（字母间距）

letter-spacing: normal | <length>

其用于设置字间距或者字母间距，此属性适用于中文或西文中的字母。 如果需要设置西文中词与词的间距或标签直接的距离则需要使用 word-spacing。


改变文字颜色
color: 

```css

element { color: red; }
element { color: #f00; }
element { color: #ff0000; }
element { color: rgb(255,0,0); }
element { color: rgb(100%, 0%, 0%); }
element { color: hsl(0, 100%, 50%); }

/* 50% translucent */
element { color: rgba(255, 0, 0, 0.5); }
element { color: hsla(0, 100%, 50%, 0.5); }

/* 全透明 */
element { color: transparent' }
element { color: rgba(0, 0, 0, 0); }
```


对齐方式:

文字居中
text-align: start | end | left | right | center | justify | match-parent | start end

文本垂直对齐
vertical-align: baseline | sub | super | text-top | text-bottom | middle | top | bottom 

文本缩进
text-indent: `<length>` | `<percentage>` && [ hanging || each-line ]

>缩进两个字可使用 text-indent: 2em;

#### 格式处理

保留空格格式
white-space: normal | pre | nowrap | pre-wrap | pre-line

文字换行
word-wrap: normal | break-word

#### 文本装饰

文字阴影

```css
p {
  text-shadow: 1px 1px 1px #000,
               3px 3px 5px blue;
}
```

- value = The X-coordinate X 轴偏移像素
- value = The Y-coordinate Y 轴偏移像素
- value = The blur radius 阴影模糊半径
- value = The color of the shadow 阴影颜色（默认为文字颜色）

文本装饰（下划线等）
text-decoration: 

```css
h1.under {
    text-decoration: underline;
}
h1.over {
    text-decoration: overline;
}
p.line {
    text-decoration: line-through;
}
p.blink {
    text-decoration: blink;
}
a.none {
    text-decoration: none;
}
p.underover {
    text-decoration: underline overline;
}
```


#### 高级设置

省略字符
text-overflow: [ clip | ellipsis | <string> ]{1,2}

```css

/* 常用配合 */
text-overflow: ellipsis;
overflow: hidden; /* 溢出截取 */
white-space: nowrap; /* 禁止换行 */

```

更换鼠标形状
cursor:

常用属性

- `<uri>` 图片资源地址代替鼠标默认形状
- `<default>` 默认光标
- `<none>` 隐藏光标
- `<pointer>` 手型光标
- `<zoom-in>`
- `<zoom-out>`
- `<move>`

强制继承
inherit 会强制继承父元素的属性值。

```css
font-size: inherit;
font-family: inherit;
font-weight: inherit;
...
word-wrap: inherit;
work-break: inherit
text-showdow: inherit
```



### 盒模型

盒子模型是网页布局的基石。它有边框、外边距、内边距、内容组成。

盒子由上到下依次分为五层，它们自上而下的顺序是。

- border 边框
- content + padding 内容与内边距
- background-image 背景图片
- background-color 背景颜色
- margin 外边距

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fspshx1777j30kj07275o.jpg)


width
内容盒子宽

height
内容盒子高


border-radius


overflow

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fspsk7lf2dj30lo07lady.jpg)

box-sizing

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fspsku93soj30ki06odgg.jpg)

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fspslj52p5j30m309375z.jpg)  

box-shadow

box-shadow: 4px  6px   3px  0px red;
             |    |     |    |
          水平偏移|     |    |
               垂直偏移 |    |
                    模糊半径 |
                          阴影大小



### 背景

background-color

background-image

background-image: url("../image/pic.png");

>当background-color 与 background-image 共存时，背景颜色永远在最底层（于背景图片之下）。

background-repeat

- background-repeat 需与背景图片数量一致。
- space 平铺并在水平和垂直留有空隙，空隙的大小为图片均匀分布后完整覆盖显示区域的宽高
- round 不留空隙平铺且覆盖显示区域，图标会被缩放以达到覆盖效果（缩放不一定等比）


background-attachment

当页面内容超过显示区域时，使用 local 使背景图片同页面内容一同滚动。
```css
background-attachment: `<attachment>`[, `<attachment>`]*
`<attachment>` = scroll | fixed | local

```

background-position

```css

/* 默认位置为 */
background-position: 0 0;

/* percentage 是容器与图片的百分比重合之处*/
background-position: 20% 50%;

/* 等同效果 */
background-position: 50% 50%;
background-position: center center;

background-position: 0 0;
background-position: left top;

background-position: 100% 100%;
background-position: right bottom;

```

### 布局、变形、动画  单独有文章分析了  这里略过

