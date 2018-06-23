---
title: webpack基础知识学习-入口起点
categories:
- 技术
- webpack系列文章
tags:
- webpack
---



### 单个入口

单个入口在上一章其实已经看到了，下面，我们主要学习下多个入口怎样创建。

<!--more-->

### 多个入口

#### 1、分离 应用程序(app) 和 第三方库(vendor) 入口

{% codeblock lang:javaScript %}
const config = {
  entry: {
    app: './src/app.js',
    vendors: './src/vendors.js'
  }
};
{% endcodeblock %}

>从表面上看，这告诉我们 webpack 从 app.js 和 vendors.js 开始创建依赖图(dependency graph)。这些依赖图是彼此完全分离、互相独立的（每个 bundle 中都有一个 webpack 引导(bootstrap)）。这种方式比较常见于，只有一个入口起点（不包括 vendor）的单页应用程序(single page application)中。

-------

#### 2、多页面应用程序

{% codeblock lang:javaScript %}
const config = {
  entry: {
    pageOne: './src/pageOne/index.js',
    pageTwo: './src/pageTwo/index.js',
    pageThree: './src/pageThree/index.js'
  }
};
{% endcodeblock %}

>webpack 需要 3 个独立分离的依赖图（如上面的示例）。
在多页应用中，（译注：每当页面跳转时）服务器将为你获取一个新的 HTML 文档。页面重新加载新文档，并且资源被重新下载。然而，这给了我们特殊的机会去做很多事：


+ 使用 CommonsChunkPlugin 为每个页面间的应用程序共享代码创建 bundle。由于入口起点增多，多页应用能够复用入口起点之间的大量代码/模块，从而可以极大地从这些技术中受益。

--------