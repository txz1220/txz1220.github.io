---
title: webpack使用技术详情
categories:
- 技术
- webpack系列文章
tags:
- webpack
---

###  本文主要步骤：

1、创建文件 mkdir mywebpack
2、npm init -y  // 用来创建webpack的配置文件
3、安装webpack  npm install webpack --save-dev
4、安装组件 npm install html-webpack-plugin --save-dev  //具体的index等文件自己创建就好了
5、webpack.config.js 的使用   //这个之前基础都学习过了

<!--more-->

5、处理js文件需要用的依赖包：

```npm
npm install --save-dev babel-loader babel-core 
npm install --save-dev babel-preset-env  //转义ES6
```
为防止浏览器不支持 Promise/Object.assign/Array.from等还有性能问题,我们引入两个包: 

> * babel-polyfill 
> + babel-plugin-transform-runtime


```npm
npm install --save-dev babel-polyfill babel-plugin-transform-runtime 
```
引入生产版本依赖 npm install --save babel-runtime 通过 .babelrc 添加配置:

{% codeblock lang:javaScript %}
{
    "presets": [
        "env"
    ],
    "plugins": [
       "transform-runtime"
    ]
}
{% endcodeblock %}

将 babel-polyfill 加到你的 entry 数组中使用，配置js文件要经过babel转义：

{% codeblock lang:javaScript %}
const path = require('path');
module.exports = {
    //entry为入口,webpack从这里开始编译
    entry: [
        "babel-polyfill",
        path.join(__dirname, './src/index.js')
    ],
    //output为输出 path代表路径 filename代表文件名称
    output: {
        path: path.join(__dirname, './bundle'),
        filename: 'bundle.js'
    },
    //module是配置所有模块要经过什么处理
    //test:处理什么类型的文件,use:用什么,include:处理这里的,exclude:不处理这里的
    module: {
        rules: [
            {
                test: /\.js$/,
                use: ['babel-loader'],
                include: path.join(__dirname , 'src'),
                exclude: /node_modules/
            }
        ]
    },
};
{% endcodeblock %}


-----



6、打包： 直接执行命令webpack 
7、看看日志说明：
8、使用快捷方式进行编译： 可以在项目package.json里面来配置 ： 

{% codeblock lang:javaScript %}
{
  "name": "05-01",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
    "build":"webpack"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "babel-preset-es2015": "^6.14.0",
    "babel-preset-react": "^6.11.1",
    "babelify": "^7.3.0",
    "react": "^15.3.2",
    "react-dom": "^15.3.2",
    "webpack": "^1.13.2",
    "webpack-dev-server": "^1.16.1"
  }
}
{% endcodeblock %}

下面你可以使用命令：

{% codeblock lang:npm %}
  npm run build
{% endcodeblock %}
-----
<!--more-->

9、怎样自动加载：
>首先安装webpack-dev-server  执行命令：
```npm
npm install webpack-dev-serve --save-dev
```
下面就可以执行如下命令了
```npm
webpack-dev-server --contentbase  -src --inline  
```
>注意： 这里版本很重要，要匹配。 如果安装其他版本，可以在名称后面加@跟上版本号就可以了。

10、配置端口号 

webpakc.config.js 里面配置

{% codeblock lang:javaScript %}
  devServer: {
  contentBase: path.join(__dirname, "dist"),
  compress: true,
  port: 9000
}
{% endcodeblock %}

接下来以管理员身份执行命令

```npm
npm run start
```


11、配置ESLint 实现代码规范化自动化测试

> * 安装：

```npm
npm install eslint --save-dev
``` 

> * 配置：

package.json 里面的配置：

```js
{
  "name": "05-01",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
    "build":"webpack"
    "lintjs":"eslint app/ webpack.*.js --cache"   //这是我们需要配置的
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "babel-preset-es2015": "^6.14.0",
    "babel-preset-react": "^6.11.1",
    "babelify": "^7.3.0",
    "react": "^15.3.2",
    "react-dom": "^15.3.2",
    "webpack": "^1.13.2",
    "webpack-dev-server": "^1.16.1"
  }
}
``` 
eslintrc.js 里面的配置：

具体的规则可以去官网查看。


> * 执行如下命令即可：

```npm
npm run lintjs
``` 


如果有错误：会相应的提示。

怎样修复呢：
执行命令：

```npm
npm run lintjs -- --fix
``` 



##### 如何自动测试  在webpack 中集成：

> 首先进行安装：  npm install eslint-loader  --save-dev

> 然后在webpack.config.js 里面进行配置： 具体配置可以查看官方文档。


12、webpack中加载CSS的相关配置

需要安装两个插件：

```npm
npm insatall css-loader style-loader  --save-dev
``` 
webpack.config.js进行配置：

```js
const ExtractTextPlugin = require('extract-text-webpack-plugin');
...
module: {
    rules: [
        ...
        {
            test: /\.less$/,
            use: ExtractTextPlugin.extract({
                fallback: "style-loader",
                use: ['css-loader', 'style-loader','postcss-loader', 'less-loader']  //进行配置
            })
        }
    ]
},
plugins: [
    ...
    new ExtractTextPlugin({
        filename: 'index.css'
    }),
],
``` 

13、webpack中加载图片

在 webpack 里，负责图片翻译的是 file-loader：

```npm
npm install  file-loader --save-dev
``` 

在webpack.config.js里面进行配置：

```js
      },
      {
       test: /\.(png|jpg|gif)$/,
       use: [
          {
            loader: 'file-loader',
            options: {}
          }
        ]
       }
     ]
``` 

>至于我们怎样在js文件里配置：  我们需要一张图片，我从 unsplash 找来了一张玫瑰，放到 src/img/rose.jpg 位置。

我们在 src/index.js 中 import 它：

```js
    import ReactDOM from 'react-dom'
    import Rose from './img/rose.jpg'
  class App extends React.Component {
  render () {
    return (
      <div><img src={Rose} alt='玫瑰' /></div>
    )
  }
}
ReactDOM.render(<App />, document.body)
``` 
14、打包：

在完成项目开发后，我们需要输出文件给生产环境部署，只要执行：
```npm
  npx webpack --mode production
``` 

14、部署：

>部署时，拷贝 dist 目录即可。

15、清理 dist

>随着某些文件的增删，我们的 dist 目录下会产生一些不再使用的文件，我们不想这些文件也部署到生产环境上占用空间，所以 webpack 在打包前最好能删除 dist 目录。

我们来试试 clean-webpack-plugin。

首先是安装：

```npm
  npm i -D clean-webpack-plugin
``` 

然后在 webpack.config.js 中调用：

```js
  const path = require('path')
  const CleanWebpackPlugin = require('clean-webpack-plugin')
 module.exports = {
   mode: 'development',
   devServer: {
     contentBase: path.resolve(__dirname, 'dist')
   },
   plugins: [
     new CleanWebpackPlugin(['dist'])   //需要实例化
   ],
   module: {
``` 

再执行 npx webpack --mode production，webpack 确实会在打包前清空 dist 目录，但我们的 index.html 也一起被清空了。


下面我们使用 html-webpack-plugin 来自动生成 index.html：

首先是安装：
```npm
  npm i --save-dev html-webpack-plugin
``` 
调整 webpack.config.js：


```js
  const CleanWebpackPlugin = require('clean-webpack-plugin')
  const HtmlWebpackPlugin = require('html-webpack-plugin')
 module.exports = {
   mode: 'development',
   devServer: {
     contentBase: path.resolve(__dirname, 'dist')
   },
   plugins: [
    new CleanWebpackPlugin(['dist'])
    new CleanWebpackPlugin(['dist']),
    new HtmlWebpackPlugin()
   ],
``` 

再运行 npx webpack --mode production，dist 下已经自动生成 index.html，再 title 却是 Webpack App，我们需要再调整一下 webpack.config.js：

```js
   plugins: [
    new CleanWebpackPlugin(['dist']),
    new HtmlWebpackPlugin()
    new HtmlWebpackPlugin({
      title: 'webpack 教程'
    })
   ],
``` 


至此，我们大致的教程算是完结了，但是这样比较麻烦，如果开发一个特定类型的项目，我们可以采用脚手架的方式直接生成：

比较有名的有：

> * [create-react-app](https://github.com/facebook/create-react-app)  react 官方出品的一套，只适用开发 react.js 项目；
> + [neutrino.js](https://neutrinojs.org/)  这是 Mozilla 出品的一套解决方案，Web、React、Node.js 等方案均有；



