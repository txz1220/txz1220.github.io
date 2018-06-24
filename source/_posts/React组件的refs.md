---
title: React-组件的Refs
categories:
- 技术
- 组件的Refs
tags:
- react
- 组件的Refs
---

### 操作DOM

两种方法：

1、JS的原生写法：

var myDiv =document.getElementById('myDiv');

ReactDOM.findDOMNode(myDiv).style.color ='green';  // 这里用到了ReactDOM  在头部先引入 import ReactDOM from 'react-dom'


2、在元素上定义ref="submitButton"   然后直接可以调用了： this.refs.submitButton.style.color="red";

Refs 是访问到组件内部 DOM 节点唯一可靠的方法

Refs 会自动销毁对子组件的引用

不要在 render 或 render 之前对 Refs 进行调用    //在事件内调用  或者render后面调用。

不要滥用 Refs