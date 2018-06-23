---
title: React4-React生命周期
categories:
- 技术
- react系列文章
tags:
- react
- node
---

### [React生命周期官方文档](https://facebook.github.io/react/docs/component-specs.html#lifecyclemethods)



### React生命周期图例：


![](https://ws1.sinaimg.cn/large/006c6oKBgy1fs838d4rxlj30lp0eywfw.jpg)

<!--more-->
### React生命周期代码示例：
{% codeblock lang:javaScript %}
import React from 'react';
export default class BodyIndex extends React.Component{
//定义页面将要加载
  componentWillMount(){
    //定义你的逻辑即可
    console.log("BodyIndex - componentWillMount");
  }
//定义页面加载完成
  componentDidMount(){
    console.log("BodyIndex - componentDidMount");
  }

  render(){
    var userName = '';
    var boolInput = false;

    var html = "IMOOC&nbsp;LESSON";

    //comments

    return (
      <div>
        <h2>页面的主体内容</h2>
        <p>{userName=='' ? '用户还没有登录' : '用户名：' + userName}</p>
        <p><input type='button' value = {userName} disabled={boolInput}/></p>
        {/*注释*/}
        <p>{html}</p> {/*需要进行 Unicode 的转码*/}
      </div>
    )
  }
}
{% endcodeblock %}