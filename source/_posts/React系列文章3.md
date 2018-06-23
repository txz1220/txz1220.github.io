---
title: React3-React内置表达式
categories:
- 技术
- react系列文章
tags:
- react
- node
---


### 三元表达式：

{% codeblock lang:javaScript %}
import React from 'react';
export default class BodyIndex extends React.Component{
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

<!--more-->
### React 三元表达式

* {window.userName == '' ? '默认用户名' : '用户名： ' + userName}
> 注意是**==**   ， 而不是"="  

### React 传参
*  disabled={boolInput}  不要用""  而是用{};


### React注释如何来写


 *  如果在代码块里面： {/*注释*/}
 *  在代码块外面： //comments


### React如果要显示html里面的空格

*  HTML 要显示可以进行 Unicode 转码










