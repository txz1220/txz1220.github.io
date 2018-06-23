---
title: 深入理解JS函数
categories:
- 技术
- 深入理解JS函数
tags:
- 深入理解JS函数
---


### 一、函数的三种角色

-----------------------

首先要先了解在函数本身会有一些自己的属性，比如：

- `length`：形参的个数；
- `name`：函数名；
- `prototype`：类的原型，在原型上定义的方法都是当前这个类的实例的公有方法；
- `__proto__`：把函数当做一个普通对象，指向Function这个类的原型
<!--more-->

函数在整个JavaScript中是最复杂也是最重要的知识，对于一个函数来说，会存在多种角色：


```js
function Fn() {
    var num = 500;
    this.x = 100;
}
Fn.prototype.getX = function () {
    console.log(this.x);
}
Fn.aaa = 1000;

var f = new Fn;

f.num // undefined
f.aaa // undefined
var res = Fn(); // res是undefined  Fn中的this是window
```

- 角色一：普通函数，对于Fn而言，它本身是一个普通的函数，执行的时候会形成私有的作用域，然后进行形参赋值、预解析、代码执行、执行完成后内存销毁；

- 角色二：类，它有自己的实例，f就是Fn作为类而产生的一个实例，也有一个叫做prototype的属性是自己的原型，它的实例都可以指向自己的原型；

- 角色三：普通对象，Fn和 var obj = {} 中的obj一样，就是一个普通的对象（所有的函数都是Function的实例），它作为对象可以有一些自己的私有属性，也可以通过__proto__找到Function.prototype；


### 二、call深入

```js
var ary = [12, 23, 34];
ary.slice();
```

以上两行简单的代码的执行过程为：ary这个实例通过原型链的查找机制找到Array.prototype上的slice方法，让找到的slice方法执行，在执行slice方法的过程中才把ary数组进行了截取。

> slice方法执行之前有一个在原型上查找的过程（当前实例中没有找到，再根据原型链查找）。


当知道了一个对象调用方法会有一个查找过程之后，我们再看：

```js
var obj = {name:'iceman'};
function fn() {
    console.log(this);
    console.log(this.name);
}
fn(); // this --> window
// obj.fn(); // Uncaught TypeError: obj.fn is not a function
fn.call(obj);
```

call方法的作用：首先寻找call方法，最后通过原型链在Function的原型中找到call方法，然后让call方法执行，在执行call方法的时候，让fn方法中的this变为第一个参数值obj，最后再把fn这个函数执行。

#### 2.2、call方法原理


```js
    function fn1() {
    console.log(1);
}
function fn2() {
    console.log(2);
}
```

输出

fn1.call(fn2); // 1

首先fn1通过原型链查找机制找到Function.prototype上的call方法，并且让call方法执行，此时call这个方法中的this就是要操作的fn1。在call方法代码执行的过程过程中，首先让fn1中的“this关键字”变为fn2，然后再让fn1这个方法执行。

> 注意：在执行call方法的时候，fn1中的this的确会变为fn2，但是在fn1的方法体中输出的内容中并没有涉及到任何和this相关的内容，所以还是输出1。



### apply方法、bind方法和call方法

apply方法和call方法的作用是一模一样的，都是用来改变方法的this关键字，并且把方法执行，而且在严格模式下和非严格模式下，对于第一个参数是null/undefined这种情况规律也是一样的，只是传递函数的的参数的时候有区别。
```js
function fn(num1, num2) {
    console.log(num1 + num2);
    console.log(this);
}
fn.call(obj , 100 , 200);
fn.apply(obj , [100, 200]);
```

bind方法和apply、call稍有不同，bind方法是事先把fn的this改变为我们要想要的结果，并且把对应的参数值准备好，以后要用到了，直接的执行即可，也就是说bind同样可以改变this的指向，但和apply、call不同就是不会马上的执行。

```js
var tempFn = fn.bind(obj, 1, 2);
tempFn();
```
第一行代码只是改变了fn中的this为obj，并且给fn传递了两个参数值1、2，但是此时并没有把fn这个函数给执行，执行bind会有一个返回值，这个返回值tempFn就是把fn的this改变后的那个结果。
