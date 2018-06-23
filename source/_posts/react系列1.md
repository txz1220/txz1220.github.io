---
title: React1-react简介及安装
categories:
- 技术
- react系列文章
tags:
- react
- node
---
本文主要讲述使用react创建一个新闻站点的技术教程，本文主要技术来源于：{% link 慕课网 http://coding.imooc.com/class/83.html [external] [慕课网] %}
。如果你感兴趣，可以跟着一起来完成。


## React的简介 ##

 - Facebook 内部用来开发Instagram   
 - JavaScript MVC框架
 - React 开源网址：[React github][1]
 - React 中文文档：[React中文文档][2]

<!-- more--> 
## 学习React需要掌握的知识 ##

 - JS
 - ES5/Es6   ——会使用babel  ——>  中文文档：[babel][3]
 - NodeJS
 - CSS
 - HTML

## React 安装及管理 ##

 - 确保先安装了node.js  ----最新的node.js包已经包含了npm  
 - 怎么查看是否安装？  node -v    npm -v
 - npm 换镜像源  （用淘宝的源就可以） 这样下载就比较快了
 - 最好采用npm 安装管理  （官方推荐方式）
 
### 用**npm** 安装React
 
 -  项目初始化
 
{% codeblock lang:npm %}
npm init 
{% endcodeblock %}
通过初始化就建立了一个react的配置文件，
下面再进行安装react需要的其他依赖包。

---

 - 安装依赖包
 可以有两种方式：
1、先在配置文件里加入需要安装的文件包名和版本，然后通过npm install 来进行安装
2、直接用npm来安装  方式如下：npm install babel-preset-es2015@版本号  --save
    这样你安装的包就可以把安装依赖的信息存储到配置文件里了

这里我们需要安装的依赖包有babel-preset-es2015 、babelify、babel-preset-react、react、react-dom  等  其他需要的依赖包可以在后续不断加入

>注： 如果要全局安装的话可以这样 npm install -g react

至此，我们还不能实现react的正常输出，我们还需要通过webpack来打包。


----------

 - **webpack** 的安装

   在安装webpack之前，先了解下react的写作流程：
   先在项目文件里建立一个src文件夹在里面建一个index.js文件 这个文件要传到外面的文件index.html。
   index.js里这样写：
   {% codeblock lang:JavaScript %}
var React = require("react");
var ReactDOM = require("react-dom");
class Index extends React.Component {
  render() {
    return(
     <h1>hello world</h1>
     document.getElementById('example')
    );
  }
}
{% endcodeblock %}

index.html里这样写：
{% codeblock lang:html %}
<div id="example">123</div>
<script src="./src/bundle.js"></script>
{% endcodeblock %}

>这里引入的bundle.js  就是webpack 生成的，他是把我们之前写的index.js生成了浏览器能识别的js文件，这样才能被浏览器识别。


**webpack**正式安装
首先定义一个webpack的配置文件：webpack config.js 通过官方文档来配置。
安装：
全局安装一下：
{% codeblock lang:npm %}
   npm install -g webpack
   npm install -g webpack-dev-server //服务器
{% endcodeblock %}

项目目录里安装一下：
{% codeblock lang:npm %}
   npm install webpack  --save
   npm install webpack-dev-server --save  //服务器
{% endcodeblock %}

>注： 一定要注意版本的问题，要和react等合适，如果都是最新的应该没问题。

下面来运行：

    webpack //在命令行执行就会把我们的index.js生成可识别的js文件了。

怎样自动加载呢：

    webpack-dev-server --contentbase  -src --inline //执行后就可以自动加载了

-----



   

  [1]: https://github.com/facebook/%20react
  [2]: http://www.css88.com/react/
  [3]: https://www.babeljs.cn/




