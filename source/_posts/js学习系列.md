---
title: javascript基础知识整理
categories:
- 技术
- JavaScript
- 基础知识
tags:
- JavaScript
---

### 一、基础语法：

#### 变量标示符

变量的命名
var _name = null;
var $name = null;
var name0 = null;

#### 关键字与保留字
JavaScript 在语言定义中保留的字段，这些字段在语言使用中存在特殊意义或功能，在程序编写的过程中不可以当做变量或函数名称使用。无需记忆，报错修改即可。

#### 字符敏感
字符串的大小写是有所区分的，不同字符指代不同的变量。

<!--more-->

#### 严格模式

##### 使用方法

```js
<!-- 全局使用 严格 模式 -->
"use strict";
(function(){
  console.log('>>> Hello, world!');
})()

<!-- 或者在函数内部声明使用 严格 模式 -->
(function(){
  "use strict";
  console.log('>>> Hello, world!');
})()
```

### 类型系统


javascript 类型系统可以分为标准类型和对象类型，进一步标准类型又可以分为原始类型和引用类型，而对象类型又可以分为内置对象类型、普通对象类型、自定义对象类型。

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsqu3rdqgvj30hw0ecjwn.jpg)

#### 标准类型

标准类型共包括了6个分别是：

原始类型（值类型）：

- Undefined undefined
- Null null
- Boolean true
- String 'hello'
- Number 123

引用类型（对象类型）：
Object

```js
var obj = {};
<!-- 原始类型变量的包装类型如下 -->
var bool = new Boolean(true);
var str = new String("hello");
var num = new Number(1);
var obj0 = new Object();
```

原始类型和引用类型的区别：

原始类型储存在栈（Stack）中储存变量的值，而引用类型在栈中保存的是所引用内容储存在堆（Heap）中的值。类似于指针的概念，引用类型并非储存变量真实数值而是地址，所以对已引用类型的复制其实只是复制了相同的地址而非实际的变量值。


Undefined 值：undefined 出现场景：

- 以声明为赋值的变量 var obj;
- 获取对象不存在的属性 var obj = {x: 0}; obj.y;
- 无返回值函数的执行结果 function f(){}; var obj = f();
- 函数参数没有传入 function f(i){console.log(i)}; f();
- void(expression)



Null 值：null 出现场景：

- 获取不存在的对象 document.getElementById('not-exist-element')


Boolean 值：true, false 出现场景：

- 条件语句导致的系统执行的隐式类型转换 if(隐式转换){}
- 字面量或变量定义 var bool = true;

String 值：字符串 出现场景：

- var str = 'Hello, world!';

Number 值：整型直接量，八进制直接量（0-），十六进制直接量（0x-)，浮点型直接量 出现场景：

- 1026
- 3.14
- 1.2e5
- 0x10
 
Object 值：属性集合 出现场景：
- var obj = {name: 'Xinyang'};


![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsqumhbmn8j30mg0gzdg5.jpg)

类型识别
- typeof
- Object.prototype.toString
- constructor
- instanceof


typeof：
可以是标准类型（Null 除外）
不可识别具体的对象类型（Function 除外）

Object.prototype.toString：
可识别标准类型及内置对象类型（例如，Object, Date, Array）
不能识别自定义对象类型


constructor：
可以识别标准类型（Undefined/Null 除外）
可识别内置对象类型
可识别自定义对象类型

```js
function getConstructiorName(obj) {
  return obj && obj.constructor && obj.constructor.toString().match(/function\s*([^(]*)/)[1];
}
getConstructiorName([]) === "Array"; // true
```

instanceof：
不可判别原始类型
可判别内置对象类型
可判别自定义对象类型


### 类型判断

avaScript的数据类型可以分为：标准类型和对象类型。
标准类型有：undefined Null Boolean Date Number Object
对象类型（构造器类型）：Boolean Date Number Object Array Date Error Function RegExp

下面我们写一个HTML来检验一下：

```js
<html>
<head>
    <title>JavaScript类型判断</title>
    <meta charset="utf-8">
    <style type="text/css">
        .red{
            background-color:red;
        }
    </style>
</head>
<body>
    <script type="text/javascript">
        /* Standard Type */
        var a;    //undefined
        var b = document.getElementById("no_exist_element"); //null
        var c = true;    //Boolean
        var d = 1;    //Number
        var e = "str";     //String
        var f = {name : "Tom"};    //Object

        /* Object Type */
        var g = new Boolean(true);    //Boolean Object
        var h = new Number(1);    //Number Object
        var i = new String("str");    //String Object
        var j = new Object({name : "Tom"}); //Object Object
        var k = new Array([1, 2, 3, 4]);    //Array Object
        var l = new Date();    //Date Object
        var m = new Error();
        var n = new Function();
        var o = new RegExp("\\d");

        /* Self-Defined Object Type */
        function Point(x, y) {
          this.x = x;
          this.y = y;
        }

        Point.prototype.move = function(x, y) {
          this.x += x;
          this.y += y;
        }

        var p = new Point(1, 2);

        /* Use the Prototype.toString() to judge the type */
        function type(obj){
            return Object.prototype.toString.call(obj).slice(8, -1).toLowerCase();
        }
    </script>
    <table border="1" cellspacing="0">
        <tr>
            <td></td>
            <td>typeof</td>
            <td>toString</td>
            <td>constructor</td>
            <td>instanceof</td>
        </tr>
        <tr>
            <td>undefined</td>
            <td><script type="text/javascript">document.write(typeof a)</script></td>
            <td><script type="text/javascript">document.write(type(a))</script></td>
            <td class="red"><script type="text/javascript">document.write(a.constructor)</script></td>
            <td class="red"><script type="text/javascript">document.write(a instanceof "undefined")</script></td>
        </tr>
        <tr>
            <td>Null</td>
            <td class="red"><script type="text/javascript">document.write(typeof b);</script></td>
            <td><script type="text/javascript">document.write(type(b));</script></td>
            <td class="red"><script type="text/javascript">document.write(b.constructor);</script></td>
            <td class="red"><script type="text/javascript">document.write(b instanceof "null");</script></td>
        </tr>
        <tr>
            <td>Boolean</td>
            <td><script type="text/javascript">document.write(typeof c);</script></td>
            <td><script type="text/javascript">document.write(type(c));</script></td>
            <td><script type="text/javascript">document.write(c.constructor);</script></td>
            <td class="red"><script type="text/javascript">document.write(c instanceof "boolean");</script></td>
        </tr>
        <tr>
            <td>Number</td>
            <td><script type="text/javascript">document.write(typeof d);</script></td>
            <td><script type="text/javascript">document.write(type(d));</script></td>
            <td><script type="text/javascript">document.write(d.constructor);</script></td>
            <td class="red"><script type="text/javascript">document.write(d instanceof "number");</script></td>
        </tr>
        <tr>
            <td>String</td>
            <td><script type="text/javascript">document.write(typeof e);</script></td>
            <td><script type="text/javascript">document.write(type(e));</script></td>
            <td><script type="text/javascript">document.write(e.constructor);</script></td>
            <td class="red"><script type="text/javascript">document.write(e instanceof "string");</script></td>
        </tr>
        <tr>
            <td>Object</td>
            <td><script type="text/javascript">document.write(typeof f);</script></td>
            <td><script type="text/javascript">document.write(type(f));</script></td>
            <td><script type="text/javascript">document.write(f.constructor);</script></td>
            <td class="red"><script type="text/javascript">document.write(f instanceof "object");</script></td>
        </tr>
        <tr><td colspan="5">-----------------------</td></tr>
        <tr>
            <td>Boolean Object</td>
            <td class="red"><script type="text/javascript">document.write(typeof g);</script></td>
            <td><script type="text/javascript">document.write(type(g));</script></td>
            <td><script type="text/javascript">document.write(g.constructor);</script></td>
            <td><script type="text/javascript">document.write(g instanceof Boolean);</script></td>
        </tr>
        <tr>
            <td>Number Object</td>
            <td class="red"><script type="text/javascript">document.write(typeof h);</script></td>
            <td><script type="text/javascript">document.write(type(h));</script></td>
            <td><script type="text/javascript">document.write(h.constructor);</script></td>
            <td><script type="text/javascript">document.write(h instanceof Number);</script></td>
        </tr>
        <tr>
            <td>String Object</td>
            <td class="red"><script type="text/javascript">document.write(typeof i);</script></td>
            <td><script type="text/javascript">document.write(type(i));</script></td>
            <td><script type="text/javascript">document.write(i.constructor);</script></td>
            <td><script type="text/javascript">document.write(i instanceof String);</script></td>
        </tr>
        <tr>
            <td>Object Object</td>
            <td class="red"><script type="text/javascript">document.write(typeof j);</script></td>
            <td><script type="text/javascript">document.write(type(j));</script></td>
            <td><script type="text/javascript">document.write(j.constructor);</script></td>
            <td><script type="text/javascript">document.write(j instanceof Object);</script></td>
        </tr>
        <tr>
            <td>Array Object</td>
            <td class="red"><script type="text/javascript">document.write(typeof k);</script></td>
            <td><script type="text/javascript">document.write(type(k));</script></td>
            <td><script type="text/javascript">document.write(k.constructor);</script></td>
            <td><script type="text/javascript">document.write(k instanceof Array);</script></td>
        </tr>
        <tr>
            <td>Date Object</td>
            <td class="red"><script type="text/javascript">document.write(typeof l);</script></td>
            <td><script type="text/javascript">document.write(type(l));</script></td>
            <td><script type="text/javascript">document.write(l.constructor);</script></td>
            <td><script type="text/javascript">document.write(l instanceof Date);</script></td>
        </tr>
        <tr>
            <td>Error Object</td>
            <td class="red"><script type="text/javascript">document.write(typeof m);</script></td>
            <td><script type="text/javascript">document.write(type(m));</script></td>
            <td><script type="text/javascript">document.write(m.constructor);</script></td>
            <td><script type="text/javascript">document.write(m instanceof Error);</script></td>
        </tr>
        <tr>
            <td>Function Object</td>
            <td><script type="text/javascript">document.write(typeof n);</script></td>
            <td><script type="text/javascript">document.write(type(n));</script></td>
            <td><script type="text/javascript">document.write(n.constructor);</script></td>
            <td><script type="text/javascript">document.write(n instanceof Function);</script></td>
        </tr>
        <tr>
            <td>RegExp Object</td>
            <td class="red"><script type="text/javascript">document.write(typeof o);</script></td>
            <td><script type="text/javascript">document.write(type(o));</script></td>
            <td><script type="text/javascript">document.write(o.constructor);</script></td>
            <td><script type="text/javascript">document.write(o instanceof RegExp);</script></td>
        </tr>
        <tr><td colspan="5">-----------------------</td></tr>
        <tr>
            <td>Point Objct</td>
            <td class="red"><script type="text/javascript">document.write(typeof p);</script></td>
            <td class="red"><script type="text/javascript">document.write(type(p));</script></td>
            <td><script type="text/javascript">document.write(p.constructor);</script></td>
            <td><script type="text/javascript">document.write(p instanceof Point);</script></td>
        </tr>
    </table>
</body>
</html>
```
执行的结果如下：

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsqv81lj3rj30lw0f9tdp.jpg)




### 内置对象

通常情况下只有对象才存在方法，但 JavaScript 不同它具有12种内置对象。内置对象又分为两类，普通对象（属性和方法）与构造器对象（可用于实例化普通对象，它还包含原型对象属性和方法，及实例对象属性和方法）。


JavaScript 对象原型链的简要说明

```js
function Point(x, y) {
  this.x = x;
  this.y = y;
}
Point.prototype.move = function(x, y) {
  this.x += x;
  this.y += y;
}
var p = new Point(1, 1);
p.move(2,2);

```

`__proto__` 称之为原型链，有如下特点：

- `__proto__ `为对象内部的隐藏属性
- `__proto__` 为实例化该对象的构造器的 prototype 对象的引用，因此可以直接方法 prototype 的所有属性和方法
- 除了 Object 每个对象都有一个 `__proto__` 属性且逐级增长形成一个链，原型链顶端是一个 Object 对象。
- 在调用属性或方法时，引擎会查找自身的属性如果没有则会继续沿着原型链逐级向上查找，直到找到该方法并调用。
- `__proto__` 跟浏览器引擎实现相关，不同的引擎中名字和实现不尽相同(chrome、firefox中名称是 `__proto__` ，并且可以被访问到，IE中无法访问)。基于代码兼容性、可读性等方面的考虑，不建议开发者显式访问 `__proto__` 属性或通过 __proto__更改原型链上的属性和方法，可以通过更改构造器prototype 对象来更改对象的 `__proto__` 属性。
构造器对象与普通对象的区别


#### 构造器对象与普通对象的区别

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsqwwycr0oj30ta0mw424.jpg)

- 构造器对象原型链中的 __proto__ 是一个 Function.prototype 对象的引用，因此可以调用 Function.prototype的属性及方   法
- 构造器对象本身有一个 prototype 属性，用该构造器实例化对象时该 prototype 会被实例对象的 __proto__ 所引用
- 构造器对象本身是一个 function 对象，因此也会有自身属性


#### 标准内置对象
##### 构造器对象
- Object
- Boolean
- String
- Number
- Function
- Array
- RegExp
- Date
- Error


其他对象

- Math
- JSON
- 全局对象



内置对象，其实也叫内置构造器，它们可以通过 new 的方式创建一个新的实例对象。内置对象所属的类型就叫内置对象类型。其声明方式如下：

```js

var i = new String("str");          // String Object
var h = new Number(1);              // Number Object
var g = new Boolean(true);          // Boolean Object
var j = new Object({name : "Tom"}); // Object Object
var k = new Array([1, 2, 3, 4]);    // Array Object
var l = new Date();                 // Date Object
var m = new Error();
var n = new Function();
var o = new RegExp("\\d");

```

>虽然标准类型中有Boolean String Number Object，内置对象类型中也有Boolean String Number Object，但它们其实是通过不同的声明方式来进行区别的。标准类型通过直接赋值，而对象类型则是通过构造器实现初始化

##### Object

构造器的原型对象在对象实例化时将会被添加到实例对象的原型链当中。` __proto__ `为原型链属性，编码时不可被显像调用。但是实例化对象可以调用原型链上的方法。
用 String/Number 等构造器创建的对象原型链顶端对象始终是一个Object对象，因此这些对象可以调用Object的原型对象属性和方法。所以 String/Number 等构造器是 Object 的子类。

##### 构造器说明：
Object 是属性和方法的集合
String/Number/Boolean/Array/Date/Error 构造器均为 Object 的子类并集成 Object 原型对象的属性及方法。

##### 实例化方法

```js
var obj0 = new Object({name: 'X', age: 13});
// 常用方法
var obj1 = {name: 'Q', age: 14};
```

属性及方法

- prototype
- create
- keys
- ...


**原型对象属性及其方法
- constructor
- toString
- valueOf
- hasOwnProperty
- ...


##### Object.create
功能：基于原型对象创造新对象

```js
// Object.create(prototype[, propertiesObject])
var prototype = {name: 'X', age: 13};
var obj = Object.create(proto);
```

##### Object.prototype.toString
功能：获取方法调用者的标准类型


```js
// objectInstance.toString()
var obj = {};
obj.toString(); // Object
```

##### Object.prototype.hasOwnProperty
功能：判断一个属性是否是一个对象的自身属性

```js
// objectInstance.hasOwnProperty("propertyName")
var obj = Object.create({a: 1, b: 2});
obj.c = 3;
obj.hasOwnProperty('a'); // false
obj.hasOwnProperty('c'); // true
```


##### String
构造器说明：单双引号内的字符串
实例化方法
```js
'Hello, world!'
var str0 = 'Xinyang';
var str1 = new String('Xinyang');
```

属性及方法
- prototype
- fromCharCode（转换 ASCII 代码为字符）

原型对象属性及其方法
- constructor
- indexOf
- replace
- slice
- split
- charCodeAt
- toLowerCase

##### String.prototype.indexOf

功能：获取子字符串在字符串中的索引
```js
// stringObject.indexOf(searchValue, fromIndex)
var str = "I am X. From China!";
var index = str.indexOf('a'); // 2
str.indexOf('a', index + 1); // 16
str.indexOf('Stupid'); // -1 字符串不存在
```

##### String.prototype.replace

功能：查找字符串替换成目标文字
```js
// stringObject.replace(regexp/substr, replacement)
var str = "apple is bad";
str = str.replace('bad', 'awesome');
```


##### String.prototype.split

功能：按分隔符将分隔符分成字符串数组

```js
// stringObject.split(separator, arrayLength)
var str = '1 2 3 4';
str.split(' '); // ['1', '2', '3', '4'];
str.split(' ', 3); // ['1', '2', '3'];
str.split(/\d+/); // ["", " ", " ", " ", ""]
```

#### Number

构造器说明：整型直接量，八进制直接量（0-），十六进制直接量（0x-)，浮点型直接量
实例化方法

```js
10
1.2e5
var count = 0x10;
var pi = new Number(3.1415);
```


属性及方法

- prototype
- MAX_VALUE
- MIN_VALUE
- NaN
- NEGATIVE_INFINITY
- POSITIVE_INFINITY


原型对象属性及其方法

- constructor
- toFixed
- toExponential
- ...

##### Number.prototype.toFixed

功能：四舍五入至指定小数位

```js
// numberObject.toFixed(num)
var num0 = 3.14;
num0.toFixed(1); // 3.1
var num1 = 3.35;
num1.toFixed(1); // 3.4
```

#### Array

构造器说明：定义数组对象
实例化方法

```js
var a0 = [1, 'abc', true, function(){}];
var a1 = new Array();
var a2 = new Array(1, 'abc', true);
```

属性及方法
- prototype
- isArray


原型对象属性及其方法
- constructor
- splice
- forEach
- find
- concat
- pop
- push
- reverse
- shift
- slice
- ...


Array.prototype.splice

功能：从数组中删除或添加元素，返回被删除的元素列表（作用域原有数组）

```js
// arrayObject.splice(start, deleteCount[, item1[, item2[, ...]]])
var arr = ['1', '2', 'a', 'b', '6'];
var ret = arr.splice(2, 2, '3', '4', '5'); // ['a', 'b']
arr; // ['1', '2', '3', '4', 5', '6']
```

#### Function

........

--------------------




### DOM编程


#### 节点操作

##### 获取节点

父子关系

- element.parentNode
- element.firstChild/ element.lastChild
- element.childNodes/ element.children

兄弟关系

- element.previousSibling/ element.nextSibling
- element.previousElementSibling/ element.nextElementSibling

>通过节点直接的关系获取节点会导致代码维护性大大降低（节点之间的关系变化会直接影响到获取节点），而通过接口则可以有效的解决此问题。


##### 接口获取元素节点


- getElementById
- getElementsByTagName
- getElementsByClassName
- querySelector
- querySelectorAll


##### 创建节点

创建节点 -> 设置属性 -> 插入节点
```js
var element = document.createElement('tagName');
```

##### 修改节点

textContent
获取或设置节点以及其后代节点的文本内容（对于节点中的所有文本内容）。

```js
element.textContent; // 获取
element.textContent = 'New Content';
```

innerText （不符合 W3C 规范）
获取或设置节点以及节点后代的文本内容。其作用于 textContent 几乎一致。
```js
element.innerText;
```


##### 插入节点

appendChild
在指定的元素内追加一个元素节点。
var aChild = element.appendChild(aChild);


insertBefore
在指定元素的指定节点前插入指定的元素。
var aChild = element.insertBefore(aChild, referenceChild);


##### 删除节点
删除指定的节点的子元素节点。
var child = element.removeChild(child);



##### innerHTML

获取或设置指定节点之中所有的 HTML 内容。替换之前内部所有的内容并创建全新的一批节点（去除之前添加的事件和样式）。innerHTML 不检查内容，直接运行并替换原先的内容。

>只建议在创建全新的节点时使用。不可在用户可控的情况下使用。

var elementsHTML = element.innerHTML;



#### 属性操作

```html
<div>
    <label for="username">User Name:</label>
    <input type="input" name="username" id="username"  class="text"  value="">
<div>
```
对应的属性

```
input.id;        // 'username'
input.type;      // 'text'
input.className; // 'text'

label.htmlFor;   // 'username'
```

属性操作方式

- Property Accessor

通过属性方法符得到的属性为转换过的实例对象（并非全字符串）。

特点

X 通用行差（命名异常，使用不同的命名方式进行访问）
X 扩展性差
√ 实用对象（取出后可直接使用）

读取属性
```html
<div>
  <label for="username">User Name: </label>
  <input type="input" name="username" id="username" class="text" value="">
</div>

input.className; // 'text'
input[id];        // 'username'
```

写入属性

可增加新的属性或改写已有属性。
```
input.value = 'new value';
input[id] = 'new-id';
```

- getAttribute / setAttribute
- 
特点

X 仅可获取字符串（使用时需转换）
√ 通用性强
读取属性

获取到的均为属性的字符串。

var attribtue = element.getAttribute('attributeName');

写入属性

可增加新的属性或改写已有属性。
element.setAttribute('attributeName', value);



- dataset
自定义属性，其为 HTMLElement 上的属性也是 data-* 的属性集。主要用于在元素上保存数据。获取的均为属性字符串。数据通常使用 AJAX 获取并存储在节点之上。

<div id='user' data-id='1234' data-username='x' data-email='mail@gmail.com'></div>


```
div.dataset.id;         // '1234'
div.dataset.username;   // 'x'
div.dataset.email;      // 'mail@gmail.com'

```

>dataset 在低版本 IE 不可使用，但可通过 getAttribute 与 setAttribute 来做兼容。



#### 样式操作

##### 更新样式

```js
element.style
element.style.color = 'red';
element.style.background = 'black';
```

增加样式后得到的结果
```html
<div style="color: red; background: black;"></div>
```


缺点

每个属性的更新都需要一个命令
命名异常（以驼峰命名法命名属性）



##### element.style.cssText

一次同时设置多个行内样式，其结果同 element.style 单独设置相同。

```js
element.style.cssText = 'color: red; background: black';
```

##### 更新 class


首先需要创建对应样式的 CSS 样式。

```css
.angry {
  color: red;
  background: black;
}
```

然后再在 JavaScript 中，在对应的事件中给元素添加需要的类即可。

element.className += ' angry';

增加样式后得到的结果
<div class="angry"></div>



##### 统一更新多个元素样式

以上方法均不适合同时更新多个样式，通过更换样式表的方式则可同时更改多个页面中的样式。将需要的大量样式也在一个皮肤样式表中，通过 JavaScript 来直接更换样式表来进行样式改变。（此方法也可用于批量删除样式）

```html
<link rel="stylesheet" type="text/css" href="base.css">
<link rel="stylesheet" type="text/css" href="style1.css">
```


element.setAttribute('href', 'style2.css');


element.setAttribute('href','style2.css')



#### 获取样式
element.style
其对应的为元素的行内样式表而不是实际样式表。


<input type="checkbox" name="" value="">


element.style.color; // ""




#### 事件

##### DOM 事件
何为 DOM 事件，HTML DOM 使JavaScript 有能力对 HTML 事件做出反应。（例如，点击 DOM 元素，键盘被按，输入框输入内容以及页面加载完毕等）


##### 事件流
一个 DOM 事件可以分为捕获过程、触发过程、冒泡过程。 DOM 事件流为 DOM 事件的处理及执行的过程。下面以一个`<a>`元素被点击为例。



##### 事件注册

事件注册，取消以及触发其作用对象均为一个 DOM 元素。

注册事件

eventTarget.addEventListener(type, listener[,useCapture])

- evenTarget 表示要绑定事件的DOM元素
- type 表示要绑定的事件，如："click"
- listener 表示要绑定的函数
- useCapture 可选参数，表示是否捕获过程



>useCapture 为设定是否为捕获过程，默认事件均为冒泡过程，只有 useCapture 为 true 时才会启用捕获过程。


```js
// 获取元素
var elem = document.getElemenyById('id');

// 事件处理函数
var clickHandler = function(event) {
  // statements
};

// 注册事件
elem.addEventListener('click', clickHandler, false);

// 第二种方式，不建议使用
elem.onclick = clickHandler;
// 或者来弥补只可触发一个处理函数的缺陷
elem.onclick = function(){
  clickHandler();
  func();
  // 其他处理函数
};
```

##### 取消事件
eventTarget.removeEventListener(type, listener[,useCapture]);

```js
// 获取元素
var elem = document.getElemenyById('id');

// 取消事件
elem.removeEventListener('click', clickHandler, false);

// 第二种方式。不建议使用
elem.onclick = null;

```


##### 触发事件

点击元素，按下按键均会触发 DOM 事件，当然也可以以通过代码来触发事件。

eventTarget.dispatchEvent(type);

```js
// 获取元素
var elem = document.getElemenyById('id');

// 触发事件
elem.dispatchEvent('click');
```

##### 事件对象

调用事件处理函数时传入的信息对象，这个对象中含有关于这个事件的详细状态和信息，它就是事件对象 event。其中可能包含鼠标的位置，键盘信息等。


##### 属性和方法

通用属性和方法
属性

- type 事件类型
- target(srcElement IE 低版本) 事件触发节点
- currentTarget 处理事件的节点


方法

- stopPropagation 阻止事件冒泡传播
- preventDefault 阻止默认行为
- stopImmediatePropagation 阻止冒泡传播

阻止事件传播
event.stopPropagation()（W3C规范方法），如果在当前节点已经处理了事件，则可以阻止事件被冒泡传播至 DOM 树最顶端即 window 对象。
event.stopImmediatePropagation() 此方法同上面的方法类似，除了阻止将事件冒泡传播值最高的 DOM 元素外，还会阻止在此事件后的事件的触发。


#### 事件分类


##### Event


![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsszuwi6t0j30ls0733yr.jpg)

window
- load 页面全部加载完毕
- unload 离开本页之前的卸载
- error 页面异常
- abort 取消加载


image
- load 图片加载完毕
- error 图标加载错误
- abort 取消图标加载
在目标图标不能正常载入时，载入备份替代图来提供用户体验。
<img src="http://sample.com/img.png" onerror="this.src='http://sample.com/default.png'">



##### UIEvent

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsszvy1a5gj30m505yglw.jpg)


##### MouseEvent
DOM 事件中最常见的事件之一

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsszwltgo6j30n70d8wf6.jpg)


属性
- clientX, clientX
- screenX, screenY
- ctrlKey, shiftKey, altKey, metaKey 如果被按下则为真（true）
- button(0, 1, 2) 鼠标的间位


![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsszxxgfrfj30b008fq4h.jpg)


MouseEvent 顺序
鼠标的移动过程中会产生很多事件。事件的监察频率又浏览器决定。
例子：从元素 A 上方移动过
mousemove -> mouseover(A) -> mouseenter(A) -> mousemove(A) -> mouseout(A) -> mouseleave(A)
例子：点击元素
mousedown -> [mousemove] -> mouseup -> click


##### 滚轮事件（Wheel）

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsszzf9y0nj30ly02qdfq.jpg)

属性

- deltaMode 鼠标滚轮偏移量的单位
- deltaX
- deltaY
- deltaZ

##### FocusEvent
其用于处理元素获得或失去焦点的事件。（例如输入框的可输入状态则为获得焦点，点击外部则失去焦点）

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fst00hwrhpj30m5078aac.jpg)

>blur 失去焦点时，focus 获得焦点时，focusin 即将获得焦点，focusout即将失去焦点。

##### KeyboardEvent


其用于处理键盘事件

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fst01wx5smj30ms03ot8p.jpg)



#### JavaScript 动画

帧，为动画的最小单位，一个静态的图像。帧频，每秒播放的帧的数量。一个动画是由很多帧组成的，因为人眼的暂留特性，当图片交替的速度大于每秒 30 帧以上既有动画的感觉。


##### JavaScript 动画三要素


![](https://ws1.sinaimg.cn/large/006c6oKBgy1fst0srska7j30mn0a5jth.jpg)


定时器

setInterval

- func 为执行改变属性的操作
- delay 为出发时间间隔（毫秒为单位）
- para1 为执行时可传入改变属性函数的参数

```js
var intervalId = setInterval(func, delay[, param1, param2, ...]);
clearInterval(intervalId);
```

>使用 setInterval 可以调用一次定时器既可实现连贯的动画。使用 clearInterval 即可清除动画效果。


setTimeout

- func 为执行改变属性的操作
- delay 为出发时间间隔（毫秒为单位）默认为 0
- para1 为执行时可传入改变属性函数的参数

```js
var timeoutId = setTimeout(func[, delay, param1, param2, ...]);
clearTimeout(timeoutId);
```

>使用 setTimeout 实现动画，则需要在动画每一帧结束时再次调用定时器。但它无需清除定时器。


区别

setTimeout 在延时后只执行一次，setInterval 则会每隔一个延时期间后会再执行。


requestAnimationFrame

类似于 setTimeout 但是无需设定时间间隔。此定时器为 HTML5 中的新标准，其间隔时间不由用户控制，而是由显示器的刷新频率决定。（市面上的显示器刷新频率为每秒刷新60次）


常见动画

大多的复杂动画都是有下列的简单动画所组成的。

- 形变，改变元素的宽高
- 位移，改变元素相对位置
- 旋转
- 透明度
- 其他...