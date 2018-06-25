---
title: React-Router
categories:
- 技术
- Router
tags:
- react
- Router
---

主要用来管理页面跳转

### 首先是安装Router：

直接npm 安装即可。

### 1、代码的逻辑结构：

 - 首页      详情页、主题部分共享于首页
 - 列表页面
 - 其他平级页面


### 2、控制页面的层级结构


<!--more-->

### 3、单页面构建Root控制


```js
import React from 'react';

import ReactDom from 'react-dom';

import Index from './index';

import ComponentList from './components/list';

import {Router,Route,hashHistory} from 'react-router';

export default class Root extends React.Component{

  render(){
      return(
        //这里替换了之前的Index,变成了程序的入口
        <Router history={hashHistory}>
           <Route component={Index}  path="/"></Route>
           <Route component={ComponentList}  path="list"></Route>
        </Router>

      );
  };
}


//入口文件   

ReactDOM.render(<Root/>, document.getElementById('example'));

```


>在package.json里面改下配置   "main":"root.js"
在webpack.config.js 里面改下配置   entry: "./src/js/root.js"


#### 另外root可以在不同的入口进行嵌套： 

比如在Index里面嵌套一个详情页可以着用写：

 <Route component={Index}  path="/">
    <Route component={ComponentDetails} path="details"></Route>
 </Route>


在Index页面里写入：

<div>
   {this.props.children}
</div>



### 4、页面间的跳转：

首先导入必要的包：

import {Link}  from 'react-router'


加链接:

在Header 页  导航加入：

<ul>
  <li><Link to = {'/'}>首页</Link><li>
  <li><Link to = {'/details'}>详情页</Link><li>
  <li><Link to = {'/list'}>列表页</Link><li>
</ul>


### 5、Router 参数传递

首先在router加入Id

path="list/:id"

然后在相对应的页面来接收：

Id:{this.props.params.id}