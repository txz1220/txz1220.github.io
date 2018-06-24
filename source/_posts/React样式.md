---
title: React-样式
categories:
- 技术
- 样式
tags:
- react
- 样式
---

### 1、内联样式：

#### 1.1内部书写：

##### a、首先在render里面定义变量：

变量的形式：

```js
const styleComponentHeader = {
  header: {
    backgroundColor: '#333333',
    color: '#FFFFFF',
    'padding-top': '15px',
    paddingBottom: '15px',
  },
};
```
<!--more-->
注意上面的命名规范： 

- 驼峰命名  paddingBottom: '15px'
 
- 引号写法  'padding-top': '15px'

> 另外是属性值用引号括起来

##### b、然后在元素上进行引用：

style={styleComponentHeader.header} 


#### 1.2 外部引用：

在外部引用css文件：

在index.html里面全局应用：和正常的引用一样。

>注意 class 需要更改成 className



**上面两种方法的缺点： 动画、伪类 (hover) 等不能使用**



#### 1.3 内联样式的表达式

首先在元素上绑定一个点击事件：onClick={this.switchHeader.bind(this)}  绑定一个函数 switchHeader   这个函数在render外面来定义：

```js
//先初始化
constrcutor(){
    super();
    this.state = {
        miniHeader: false
    }
}

switchHeader(){
    this.setState({
        miniHeader: !this.state.miniHeader;
    })
}
```
##### 那我们怎么定义miniHeader的样式状态呢：

可以吧他绑在我们刚才定义的样式里面

paddingBottom: (this.state.miniHeader) ? "3px" : "15px"

>这里用到了三元表达式的写法




### 2、CSS模块化：

首先安装三个模块，在配置文件先定义好，然后用npm安装即可。

这个三个模块分别是：
- babel-plugin-react-html-attrs   解决在react写类class不必非得用calssName

- style-loader

- css-loader


下面是配置webpack.config.js     具体配置可以看看相关的文档或者看我之前写的webpack教程。


下面是把你写的css文件导入到你制定的js文件页，  比如你写好了footer.css的样式文件，你可以把他引入到footer.js页面

引入方式：

var footerCss  = require("../../css/footer.css");


在footer.js使用它：

在你的元素上加上<footer class={footerCss.miniFooter}>  这是footer页面 </footer>

这里footerCSS是我们上面定义的  miniFooter是我们在footer.css里面写的。





### 2、jsx样式和css样式互转：

css to react  [在线转换](http://staxmanade.com/CssToReact/)




