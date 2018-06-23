---
title: React2-React组件化
categories:
- 技术
- react系列文章
tags:
- react
- node
---



## React 机制##


![](https://ws1.sinaimg.cn/mw690/006c6oKBgy1fs4qn5ospjj30lv0duwgb.jpg)


<!--more-->


## React 组件##

> * 组件是 React 的一个主要特性
> * 组件对于模块化开发的重要性
> * 组件的 return 函数里返回的 HTML 节点必须是一个
> * 可以给外部使用的组件定义：export default class ComponentHeader extends React.Component{}
> * 入口的定义：ReactDOM.render(, document.getElementById('example'));
> * 组件return 函数返回Html的节点必须是一个



### index.js  里面代码示例:


``` JavaScript
import React from 'react';
import PCHeader from './pc_header';
import PCFooter from './pc_footer';
import PCNewsContainer from './pc_newscontainer';

export default class PCIndex extends React.Component {
	render() {
		return (
			<div>
				<PCHeader></PCHeader>
				<PCNewsContainer></PCNewsContainer>
				<PCFooter></PCFooter>
			</div>
		);
	};
}
```

### pc_header.js  里面代码示例:


{% codeblock lang:javaScript %}
import React from 'react';
import {Row, Col} from 'antd';
import {Router, Route, Link, browserHistory} from 'react-router'
class PCHeader extends React.Component {
render(){
    return(
        <h1>这是页头</h1>
    );
}
    
}
{% endcodeblock %}


### React 多组件嵌套

通过上面的示例我们可以看到：组件也可以通过参数的形式传递。把pc_header.js 组件作为一个参数传递到index.js里面。


> 这样我们可以分别开发页面不同的部分，非常方便。 需要注意的有两点：

 * 命名的规范化。
 * 项目搭建的规范化。



这里我们需要注意一个项目怎么去搭建项目的结构，下面是示例图片，可以参考下：

![](https://ws1.sinaimg.cn/mw690/006c6oKBgy1fs4uz6lhbdj30810fwgm5.jpg)







