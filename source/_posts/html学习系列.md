---
title: html学习系列
categories:
- 技术
- html      
tags:
- html
---


### 简介：
一个html分三部分：

- 文档声明：
`<!DOCTYPE html> ` 必须首行定格

- 文档头部
```html
<head>
    <title> 为文档标题
    <meta charset="utf-8">     //文档解码格式
    <meta name="keywords" content="..."> 和 <meta name="description" content="...">   //提供给搜索引擎使用
    <meta name="viewport" content="width=device-width, initial-scale=1.0">     //移动端浏览器的宽高与缩放
    <link> 标签可以引入 favicon 和样式表 CSS 文件
</head>
```

- 文档主体


<!--more-->


### HTML 语法

书写规范：

- 小写标签和属性
- 属性值双引号
- 代码因嵌套缩进

全局属性

- id, `<div id='unique-element'></div>`，页面中唯一
- class，`<button class='btn'>Click Me</button>`，页面中可重复出现
- style，尽量避免
- title，对于元素的描述类似于 Tooltip 的效果。


### HTML 标签

`<body>` 页面内容 `<header>` 文档头部 `<nav>` 导航 `<aside>` 侧边栏 `<article>` 定义外部内容（如外部引用的文章） `<section>` 一个独立的块 `<footer>` 尾部

页面通常结构

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsppx4xztzj30h80eutbn.jpg)


文本标签

```html
<!-- 默认超链接  -->
<a href="http://sample-link.com" title="Sample Link">Sample</a>
<!-- 当前窗口显示 -->
<a href="http://sample-link.com" title="Sample Link" target="_self">Sample</a>
<!-- 新窗口显示 -->
<a href="http://sample-link.com" title="Sample Link" target="_blank">Sample</a>
<!-- iframe 中打开链接 -->
<a href="http://sample-link.com" title="Sample Link" target="iframe-name">Sample</a>
<iframe name="iframe-name" frameborder="0"></iframe>

<!-- 页面中的锚点 -->
<a href="#achor">Achor Point</a>
<section id="achor">Achor Content</section>

<!-- 邮箱及电话需系统支持 -->
<a href="mailto:sample-address@me.com" title="Email">Contact Us</a>
<!-- 多个邮箱地址 -->
<a href="mailto:sample-address@me.com, sample-address0@me.com" title="Email">Contact Us</a>
<!-- 添加抄送，主题和内容 -->
<a href="mailto:sample-address@me.com?cc=admin@me.com&subject=Help&body=sample-body-text" title="Email">Contact Us</a>

<!-- 电话示例 -->
<a href="tel:99999999" title="Phone">Ring Us</a>
```


组合内容标签

- `<div>`
- `<p>`
- `<ol>`
- `<ul>`
- `<dl>`
- `<pre>`
- `<blockquote>`


#### 文档章节

`<body>` 页面内容 `<header>` 文档头部 `<nav>` 导航 `<aside>` 侧边栏 `<article> `定义外部内容（如外部引用的文章） `<section>` 一个独立的块 `<footer> `尾部

#### 引用
`<cite>` 引用作品的名字、作者的名字等
`<q>` 引用一小段文字（大段文字引用用`<blockquote>`）
`<blockquote>` 引用大块文字
`<pre>` 保存格式化的内容（其空格、换行等格式不会丢失）

```html
<pre>
  <code>
    int main(void) {
      printf('Hello, world!');
      return 0;
  }
</code>
</pre>
```

#### 代码
`<code>` 引用代码

#### 格式化
`<b>` 加粗 `<i> `斜体

#### 强调
`<em>` 斜体。着重于强调内容，会改变语义的强调` <strong> `粗体。着重于强调内容的重要性

#### 换行
`<br>` 换行


#### 列表
##### 无序列表
```html
<ul>
  <li>标题</li>
  <li>结论</li>
</ul>
```

##### 有序列表
```html
<ol>
  <li>第一</li>
  <li>第二</li>
</ol>
```

##### 自定义列表
```html
<dl>
  <dt>作者</dt>
  <dd>爱因斯坦</dd>
  <dt>作品</dt>
  <dd>《相对论》</dd>
  <dd>《时间与空间》</dd>
</dl>
```

#### 一个`<dt>`可以对应多个`<dd>`

> `<dl>` 为自定义列表，其中包含一个或多个 `<dt>` 及 一个或多个 `<dd>`，并且dt 与 dl列表会有缩进的效果。`<pre>` 会保留换行和空格，通常与 `<code>` 一同使用。

`<blockquote>` 拥有 cite 属性，它包含引用文本的出处，示例如下所示：

```html
<blockquote cite="http://example.com/facts">
  <p>Sample Quote...</p>
</blockquote>

```

#### 嵌入

```html

<iframe src=""></iframe> 页面操作可以不影响到iframe的内容

<!--object embed通常用来嵌入外部资源 -->
<object type="application/x-shockwave-player">
  <param name="movie" value="book.pdf">
</object>

<!--视频 track可以引入字幕 autoplay可以使视频加载后自动播放，loop可以使其循环播放 -->
<video autoplay loop controls="controls" poster="poster.jpg">
  <source src="movie.mp4" type="video/mp4">
  <source src="movie.webm" type="video/webm">
  <source src="movie.ogg" type="video/ogg">
  <track kind="subtitles" src="video.vtt" srclang="cn" label="cn">
</video>
```

#### 资源标签

##### 图标签

canvas 基于像素，性能要求比较高，可用于实时数据展示。svg 为矢量图形图像。

##### 热点区域标签

img中套用map以及area可以实现点击某部分图片触发一个链接，点击另一部分触发另一个链接

```html
<img src="mama.jpg" width=100 height=100 usemap="#map" />
<map name="map">
    <area shap="rect" coords="0,0,50,50" href="" alt="">
    <area shap="circle" coords="75,75,25" href="" alt="">
</map>

```


#### 表格

表格代码示例

```html
<table>
  <caption>table title and/or explanatory text</caption>
  <thead>
    <tr>
      <th>header</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>data</td>
    </tr>
  </tbody>
</table>
```

使用 colspan=val 进行跨列，使用 rowspan=val 进行跨行。


#### 表单

```html
<form action="WebCreation_submit" method="get" accept-charset="utf-8">
  <fieldset>
    <legend>title or explanatory caption</legend>
    <!-- 第一种添加标签的方法 -->
    <label><input type="text/submit/hidden/button/etc" name="" value=""></label>
    <!-- 第二种添加标签的方法 -->
    <label for="input-id">Sample Label</label>
    <input type="text" id="input-id">
  </fieldset>
  <fieldset>
    <legend>title or explanatory caption</legend>
    <!-- 只读文本框 -->
    <input type="text" readonly>
    <!-- 隐藏文本框，可提交影藏数据 -->
    <input type="text" name="hidden-info" value="hiden-info-value" hidden>
  </fieldset>
  <button type="submit">Submit</button>
  <button type="reset">Reset</button>
</form>

```

使用fieldset可用于对表单进行分区
表单中的其他控件类型：
- textarea （文本框）   
- select 与 option （下拉菜单可多选）

#### 实体字符

实体字符（ASCII Encoding Reference）是用来在代码中以实体代替与HTML语法相同的字符，避免浏览解析错误。它的两种表示方式，第一种为 & 外加实体字符名称，例如 `&nbsp;`，第二种为 & 加实体字符序号，例如 `&#160;`。

常用HTML字符实体（建议使用实体）：

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fspqeq104rj30m0083q34.jpg)

常用特殊字符实体（不建议使用实体）：

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fspqfjmug9j30lq0epq3i.jpg)


### 浏览器兼容：

主流浏览器都兼容 HTML5 的新标签，对于 IE8 及以下版本不认识 HTML5的新元素，可以使用 JavaScript 创建一个没用的元素来解决，例如：

```html
<script>
    document.createElement("header");
</script>
```
