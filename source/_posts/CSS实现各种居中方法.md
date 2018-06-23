---
title: CSS 实现各种居中
categories:
- 技术
- 前端基础知识
- css
tags:
- CSS
- 居中
---

### 一、水平居中

#### 1、行内元素居中

 顾名思义，行内元素居中是只针对行内元素的，比如文本（text）、图片（img）、按钮等行内元素，可通过给父元素设置 text-align:center 来实现。另外，如果块状元素属性display 被设置为inline时，也是可以使用这种方法。但有个首要条件是子元素必须没有被float影响，否则一切都是无用功。

 ```css
 .div1{
        text-align:center;
    }
<div class="div1">Hello world</div>
```
<!--more-->
#### 2、块状元素居中

##### （1）、定宽块状元素居中

 满足定宽（块状元素的宽度width为固定值）和块状两个条件的元素可以通过设置“左右margin”值为“auto”来实现居中。

 ```css
 .div1{
　　　　 width:200px;
　　　　 border:1px solid red;
        margin:0 auto;
    }
<div class="div1">Hello world</div>
```

##### （2）、不定宽块状元素居中

在实际工作中我们会遇到需要为“不定宽度的块状元素”设置居中，比如网页上的分页导航，因为分页的数量是不确定的，所以我们不能通过设置宽度来限制它的弹性。(不定宽块状元素：块状元素的宽度width不固定。)

有三种方法可以对不定宽块状元素进行居中：

方法1：

将要显示的元素加入到 table 标签当中，然后为 table 标签设置“左右margin”值为“auto”来实现居中； 或使用 display : table；然后设该元素“左右margin”值为“auto”来实现居中。后面的display:table; 方法会更简洁。

为什么加入table标签? 是利用table标签的长度自适应性---即不定义其长度也不默认父元素body的长度（table其长度根据其内文本长度决定），因此可以看做一个定宽度块元素，然后再利用定宽度块状居中的margin的方法，使其水平居中。

```html
table{
    margin:0 auto;
}

<div>
<table>
  <tbody>
    <tr><td>
    <ul>
        <li>Hello world</li>
        <li>Hello world</li>
    </ul>
    </td></tr>
  </tbody>
</table>
</div>
```

```html
.wrap{
    background:#ccc;
    display:table;
    margin:0 auto;
}

<div class="wrap">
  Hello world  
</div>
```

方法2：

改变块级元素的 display 为 inline 类型（设置为 行内元素 显示），然后使用 text-align:center 来实现居中效果。

这种方法相比第一种方法的优势是不用增加无语义标签，但也存在着一些问题：它将块状元素的 display 类型改为 inline，变成了行内元素，所以少了一些功能，比如设定长度值（变成inline-block就可以设置宽高）。

```css
.container{
    text-align:center;
 }
.container ul{
    list-style:none;
    margin:0;
    padding:0;
    display:inline;  //怎么这一句用不用都是一样效果的？
 }

<div class="container">
    <ul>
        <li>Hello world</li>
        <li>Hello world</li>
    </ul>
</div>
```

方法3：

 通过给父元素设置 float，然后给父元素设置 position:relative 和 left:50%，子元素设置 position:relative 和 left: -50% 来实现水平居中。

 先设置父元素wrap清除浮动，然后左浮动。定位让wrap向右偏移50%。然后定义子元素相对于父元素向左偏移50%。脱离父元素。加个边框就可以明白一些了。另外用绝对定位也是可以的。
```css
 .wrap{
    float:left;
    position:relative;
    left:50%;
    clear:both;
}
.wrap-center{
    background:#ccc;
    position:relative;
    left:-50%;
}

<div class="wrap">
    <div class="wrap-center">Hello world</div>
</div>
```

### 二、垂直居中

垂直居中可分为父元素高度确定的单行文本，以及父元素高度确定的多行文本。

1、父元素高度确定的单行文本的竖直居中的方法是通过设置父元素的 height 和 line-height 高度一致来实现的。(height: 该元素的高度，line-height: 顾名思义，行高，指在文本中，行与行之间的 基线间的距离 )。

```css
.wrap h2{
    margin:0;
    height:100px;
    line-height:100px;
    background:#ccc;
}

<div class="wrap">
    <h2>Hello world</h2>
</div>
```

2、父元素高度确定的多行文本

有两种方法：

方法1：使用插入 table  (包括tbody、tr、td)标签，同时设置 vertical-align：middle。

```html css
.wrap{
    height:300px;
    background:#ccc;
    vertical-align:middle;   /* td 标签默认情况下就默认设置了 vertical-align 为 middle，可以不需要显式地设置 */
}

<table>
    <tbody>
        <tr>
            <td class="wrap">
                <div>
                    <p>Hello world</p>
                    <p>Hello world</p>
                    <p>Hello world</p>
                </div>
            </td>
        </tr>
    </tbody>
</table>
```


方法2：

设置块级元素的 display 为 table-cell（设置为表格单元显示），激活 vertical-align 属性。但这种方法兼容性比较差， IE6、7 并不支持这个样式。

```css
.wrap{
    height:300px;
    background:#ccc;
    
    display:table-cell;/*IE8以上及Chrome、Firefox*/
    vertical-align:middle;/*IE8以上及Chrome、Firefox*/
}

<div class="wrap">
    <p>Hello world</p>
    <p>Hello world</p>
    <p>Hello world</p>
</div>
```