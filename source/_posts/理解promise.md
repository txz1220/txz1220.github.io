---
title: 理解Promise
categories:
- 技术
- 理解Promise
tags:
- 理解Promise
---


### Promise in js


>回调函数真正的问题在于他剥夺了我们使用 return 和 throw 这些关键字的能力。而 Promise 很好地解决了这一切。

另外解决回调地狱的问题。


所谓 Promise，就是一个对象，用来传递异步操作的消息。它代表了某个未来才会知道结果的事件（通常是一个异步操作），并且这个事件提供统一的 API，可供进一步处理。


#### Promise 对象有以下两个特点。

（1）对象的状态不受外界影响。Promise 对象代表一个异步操作，有三种状态：Pending（进行中）、Resolved（已完成，又称 Fulfilled）和 Rejected（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是 Promise 这个名字的由来，它的英语意思就是「承诺」，表示其他手段无法改变。

（2）一旦状态改变，就不会再变，任何时候都可以得到这个结果。Promise 对象的状态改变，只有两种可能：从 Pending 变为 Resolved 和从 Pending 变为 Rejected。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果。就算改变已经发生了，你再对 Promise 对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。

有了 Promise 对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，Promise 对象提供统一的接口，使得控制异步操作更加容易。

Promise 也有一些缺点。首先，无法取消 Promise，一旦新建它就会立即执行，无法中途取消。其次，如果不设置回调函数，Promise 内部抛出的错误，不会反应到外部。第三，当处于 Pending 状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。


```js
var promise = new Promise(function(resolve, reject) {
 if (/* 异步操作成功 */){
 resolve(value);
 } else {
 reject(error);
 }
});

promise.then(function(value) {
 // success
}, function(value) {
 // failure
});
```

Promise 构造函数接受一个函数作为参数，该函数的两个参数分别是 resolve 方法和 reject 方法。

如果异步操作成功，则用 resolve 方法将 Promise 对象的状态，从「未完成」变为「成功」（即从 pending 变为 resolved）；

如果异步操作失败，则用 reject 方法将 Promise 对象的状态，从「未完成」变为「失败」（即从 pending 变为 rejected）。


#### 基本的 api:

- Promise.resolve()
- 
- Promise.reject()
- 
- Promise.prototype.then()
- 
- Promise.prototype.catch()
- 
- Promise.all() // 所有的完成

```js
var p = Promise.all([p1,p2,p3]);
```

- Promise.race() // 竞速，完成一个即可



#### 进阶

promises 的奇妙在于给予我们以前的 return 与 throw，每个 Promise 都会提供一个 then() 函数，和一个 catch()，实际上是 then(null, ...) 函数，

```js
somePromise().then(functoin(){
        // do something
    });
```

我们可以做三件事，
1. return 另一个 promise
2. return 一个同步的值 (或者 undefined)
3. throw 一个同步异常 throw new Eror('');


1. 封装同步与异步代码

```js

```
new Promise(function (resolve, reject) {
resolve(someValue);
});
```
写成

```
Promise.resolve(someValue);
```

```