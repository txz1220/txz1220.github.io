---
title: React4-React 属性与事件
categories:
- 技术
- react系列文章
tags:
- react
- node
---

### State属性

> * 表示页面状态的值
> * state 对于模块属于自身的属性
> * 首先需要进行初始化 this.state = {username: "Parry"};
> * 初始化可以放置在构造函数 constructor 里
> * 修改 state：this.setState({username:"IMOOC"});
> * state 的作用域只属于当前的类，不污染其他模块



### 代码示例:


{% codeblock lang:javaScript %}
import React from 'react';
export default class BodyIndex extends React.Component {
	constructor() {
		super(); //调用基类的所有的初始化方法
		this.state = {
			username: "Parry",
			age: 20
		}; //初始化赋值
	}
	render() {
		setTimeout(() => {
			//更改 state 的时候
			this.setState({username: "IMOOC", age: 30});
		}, 4000);
		return (
			<div>
				<h2>页面的主体内容</h2>
				<p>{this.state.username} {this.state.age}</p>
			</div>
		)
	}
}
{% endcodeblock %}

<!--more-->

### Props 属性：


> * props 对于模块属于外来属性
> * 传递参数： 在被引入模块中添加{this.props.userid} 这里面的userid就是你引用的一个参数，然后你就可以在引入该模块的文件中给这个userid进行赋值了：<'被引入的模块' userid={1220}/>，这样就可以顺利的传递参数了。
> * 模块中接受参数：this.props.username

### 被引入模块的示例代码：

{% codeblock lang:javaScript %}
import React from 'react';
export default class BodyIndex extends React.Component {
  constructor(){
      super(); //调用基类的所有的初始化方法
      this.state =  {
        username : "Parry",
        age : 20
      }; //初始化赋值
  }

	render() {
    setTimeout(()=>{
      //更改 state 的时候
      this.setState({username: "IMOOC",age : 30});
    },4000);

		return (
			<div>
				<h2>页面的主体内容</h2>
				<p>{this.state.username} {this.state.age} {this.props.userid} {this.props.username}</p>
			</div>
		)
	}
}
{% endcodeblock %}

### 引入模块文件的示例代码：

{% codeblock lang:javaScript %}
var React = require('react');
var ReactDOM = require('react-dom');
import BodyIndex from './components/bodyindex';
class Index extends React.Component {	
	render() {
		return (
			<div>
				<ComponentHeader/>
				<BodyIndex userid={123456} username={"nick"}/>
				<ComponentFooter/>
			</div>
		);
	}
}
ReactDOM.render(
	<Index/>, document.getElementById('example'));

{% endcodeblock %}