---
title: React-可复用组件
categories:
- 技术
- 可复用组件
tags:
- react
- 可复用组件
---

### Prop 验证

比如我们需要传入的是一种数字数据，我们可以用着用方法：
```js
BodyIndex.propTypes = {
    userid: React.PropTypes.number.isRequired
};
```

其中我们看到用到了react里面的PropTypes  这个属性   后面跟了isRequired  (这个数据类型是必须的)

### 默认 Prop 值

const defaultProps = { text:'Hello World' };

使用方法：BodyIndex.defaultProps = defaultProps;


### 传递所有参数的快捷方式


子页面代码：

<Component {...this.props} more="values" />

Component：代表的是子页面的子页面即孙页面的组件名。

 {...this.props}  这个是我们从父页面传递过来的，  后面的more="values" 就是我们新加的属性



 然后在孙页面输出  <p>{this.props.userid} {this.props.username} {this.props.id}</p>