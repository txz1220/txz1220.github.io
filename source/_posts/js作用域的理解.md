---
title: JS作用域的理解
categories:
- 技术
- js作用域
tags:
- react
- js作用域
---

### 1.执行环境（execution context）


执行环境定义了变量和函数有权访问的其他数据，决定了他们各自的行为。每个执行环境都有与之对应的变量对象（variable object），保存着该环境中定义的所有变量和函数。我们无法通过代码来访问变量对象，但是解析器在处理数据时会在后台使用到它。

执行环境有全局执行环境（也称全局环境）和函数执行环境之分。执行环境如其名是在运行和执行代码的时候才存在的，所以我们运行浏览器的时候会创建全局的执行环境，在调用函数时，会创建函数执行环境。
<!--more-->

#### 1.1 全局执行环境
　　全局执行环境是最外围的一个执行环境，在web浏览器中，我们可以认为他是window对象，因此所有的全局变量和函数都是作为window对象的属性和方法创建的。代码载入浏览器时，全局环境被创建，关闭网页或者关闭浏览时全局环境被销毁。

#### 1.2 函数执行环境
　　每个函数都有自己的执行环境，当执行流进入一个函数时，函数的环境就被推入一个环境栈中，当函数执行完毕后，栈将其环境弹出，把控制权返回给之前的执行环境。

### 2 作用域、作用域链

#### 2.1 全局作用域（globe scope）和局部作用域（local scope）

　　全局作用域可以在代码中的任何地方都能被访问，例如：

```js
1  var name1="haha";
2 function changName(){
3     var name2="xixi";
4     console.log(name1); // haha
5     console.log(name2);// xixi
6 } 
7 changName();
8 console.log(name1);//haha
9 console.log(name2);//Uncaught ReferenceError: name2 is not defined
```
>局部作用域一般只在固定的代码片段内可以访问得到，例如上述代码中的name2，只有在函数内部可以访问得到。

#### 2.2 作用域链（scope chain）

全局作用域和局部作用域中变量的访问权限，其实是由作用域链决定的。

　　每次进入一个新的执行环境，都会创建一个用于搜索变量和函数的作用域链。作用域链是函数被创建的作用域中对象的集合。作用域链可以保证对执行环境有权访问的所有变量和函数的有序访问。

　　作用域链的最前端始终是当前执行的代码所在环境的变量对象（如果该环境是函数，则将其活动对象作为变量对象），下一个变量对象来自包含环境（包含当前还运行环境的环境），下一个变量对象来自包含环境的包含环境，依次往上，直到全局执行环境的变量对象。全局执行环境的变量对象始终是作用域链中的最后一个对象。

　　标识符解析是沿着作用域一级一级的向上搜索标识符的过程。搜索过程始终是从作用域的前端逐地向后回溯，直到找到标识符（找不到，就会导致错误发生）。

例如：

```js
var name1 = "haha";
function changeName(){
    var name2="xixi";
    function swapName(){
        console.log(name1);//haha
        console.log(name2);//xixi
        var tempName=name2;
        name2=name1;
        name1=tempName;
        console.log(name1);//xixi
        console.log(name2);//haha
        console.log(tempName);//xixi
    }
    swapName();
    console.log(name1);//haha
    console.log(name2);//xixi
    //console.log(tempName);抛出错误：Uncaught ReferenceError: tempName is not defined
}
changName();
console.log(name1);
//console.log(name2); 抛出错误：Uncaught ReferenceError: name2 is not defined
//console.log(tempName);抛出错误：Uncaught ReferenceError: tempName is not defined
```

上述代码中，一共有三个执行环境：全局环境、changeName()的局部环境和 swapName() 的局部环境。所以，

　1.函数 swapName()的作用域链包含三个对象：自己的变量对象----->changeName()局部环境的变量对象 ----->全局环境的变量对象。

　2.函数changeName()的作用域包含两个对象：自己的变量对象----->全局环境的变量对象。

> - 函数的局部环境可以访问函数作用域中的变量，也可以访问和操作父环境（包含环境）乃至全局环境中的变量。
> - 父环境只能访问其包含环境和自己环境中的变量和函数，不能访问其子环境中的变量和函数。
> - 全局环境只能访问全局环境中的变量和函数，不能直接访问局部环境中的任何数据。


### 3.提升（hoisting）

变量提升：  把变量放在最前面，单线程执行，不提升，可能读取不到！