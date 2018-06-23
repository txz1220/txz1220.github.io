---
title: jQuery选择器
categories:
- 技术
- jQuery选择器
tags:
- jQuery选择器
---

---------------

### 一、选择器

#### 按ID查找

// 查找<div id="abc">:
var div = $('#abc');

 > #abc以#开头。返回的对象是jQuery对象。


 什么是jQuery对象？jQuery对象类似数组，它的每个元素都是一个引用了DOM节点的对象。

以上面的查找为例，如果id为abc的<div>存在，返回的jQuery对象如下：

[<div id="abc">...</div>]

如果id为abc的<div>不存在，返回的jQuery对象如下：

[]

<!--more-->

#### 按tag查找

按tag查找只需要写上tag名称就可以了：

var ps = $('p'); // 返回所有<p>节点
ps.length; // 数一数页面有多少个<p>节点


#### 按class查找

按class查找注意在class名称前加一个.：

var a = $('.red'); // 所有节点包含`class="red"`都将返回
// 例如:
// <div class="red">...</div>
// <p class="green red">...</p>



通常很多节点有多个class，我们可以查找同时包含red和green的节点：

var a = $('.red.green'); // 注意没有空格！
// 符合条件的节点：
// <div class="red green">...</div>
// <div class="blue green red">...</div>



#### 按属性查找

一个DOM节点除了id和class外还可以有很多属性，很多时候按属性查找会非常方便，比如在一个表单中按属性来查找：

var email = $('[name=email]'); // 找出<??? name="email">
var passwordInput = $('[type=password]'); // 找出<??? type="password">
var a = $('[items="A B"]'); // 找出<??? items="A B">


当属性的值包含空格等特殊字符时，需要用双引号括起来。

**按属性查找还可以使用前缀查找或者后缀查找：**

var icons = $('[name^=icon]'); // 找出所有name属性值以icon开头的DOM
// 例如: name="icon-1", name="icon-2"
var names = $('[name$=with]'); // 找出所有name属性值以with结尾的DOM
// 例如: name="startswith", name="endswith"
这个方法尤其适合通过class属性查找，且不受class包含多个名称的影响：

var icons = $('[class^="icon-"]'); // 找出所有class包含至少一个以`icon-`开头的DOM
// 例如: class="icon-clock", class="abc icon-home"


#### 组合查找

组合查找就是把上述简单选择器组合起来使用。如果我们查找$('[name=email]')，很可能把表单外的<div name="email">也找出来，但我们只希望查找<input>，就可以这么写：

var emailInput = $('input[name=email]'); // 不会找出<div name="email">


同样的，根据tag和class来组合查找也很常见：

var tr = $('tr.red'); // 找出<tr class="red ...">...</tr>


#### 多项选择器

多项选择器就是把多个选择器用,组合起来一块选：
$('p,div'); // 把<p>和<div>都选出来
$('p.red,p.green'); // 把<p class="red">和<p class="green">都选出来


#### 层级选择器（Descendant Selector）

如果两个DOM元素具有层级关系，就可以用$('ancestor descendant')来选择，层级之间用空格隔开。


#### 子选择器（Child Selector）

子选择器$('parent>child')类似层级选择器，但是限定了层级关系必须是父子关系，就是<child>节点必须是<parent>节点的直属子节点。

#### 过滤器（Filter）

过滤器一般不单独使用，它通常附加在选择器上，帮助我们更精确地定位元素。观察过滤器的效果：

```javascript
$('ul.lang li'); // 选出JavaScript、Python和Lua 3个节点

$('ul.lang li:first-child'); // 仅选出JavaScript
$('ul.lang li:last-child'); // 仅选出Lua
$('ul.lang li:nth-child(2)'); // 选出第N个元素，N从1开始
$('ul.lang li:nth-child(even)'); // 选出序号为偶数的元素
$('ul.lang li:nth-child(odd)'); // 选出序号为奇数的元素
```

#### 表单相关

针对表单元素，jQuery还有一组特殊的选择器：

- :input：可以选择<input>，<textarea>，<select>和<button>；

- :file：可以选择<input type="file">，和input[type=file]一样；

- :checkbox：可以选择复选框，和input[type=checkbox]一样；

- :radio：可以选择单选框，和input[type=radio]一样；

- :focus：可以选择当前输入焦点的元素，例如把光标放到一个<input>上，用$('input:focus')就可以选出；

- :checked：选择当前勾上的单选框和复选框，用这个选择器可以立刻获得用户选择的项目，如$('input[type=radio]- :checked')；

- :enabled：可以选择可以正常输入的<input>、<select>
等，也就是没有灰掉的输入；

- :disabled：和:enabled正好相反，选择那些不能输入的。




#### 查找和过滤


通常情况下选择器可以直接定位到我们想要的元素，但是，当我们拿到一个jQuery对象后，还可以以这个对象为基准，进行查找和过滤。

**最常见的查找是在某个节点的所有子节点中查找，使用find()方法，**它本身又接收一个任意的选择器。


```html
<!-- HTML结构 -->
<ul class="lang">
    <li class="js dy">JavaScript</li>
    <li class="dy">Python</li>
    <li id="swift">Swift</li>
    <li class="dy">Scheme</li>
    <li name="haskell">Haskell</li>
</ul>
```

##### 用find()查找：

```javascript
var ul = $('ul.lang'); // 获得<ul>
var dy = ul.find('.dy'); // 获得JavaScript, Python, Scheme
var swf = ul.find('#swift'); // 获得Swift
var hsk = ul.find('[name=haskell]'); // 获得Haskell
```

如果要从当前节点开始向上查找，使用parent()方法;

对于位于同一层级的节点，可以通过next()和prev()方法;

##### 过滤

和函数式编程的map、filter类似，jQuery对象也有类似的方法。

filter()方法可以过滤掉不符合选择器条件的节点：

var langs = $('ul.lang li'); // 拿到JavaScript, Python, Swift, Scheme和Haskell
var a = langs.filter('.dy'); // 拿到JavaScript, Python, Scheme


