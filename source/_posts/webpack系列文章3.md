---
title: webpack基础知识学习-出口
categories:
- 技术
- webpack系列文章
tags:
- webpack
---

>配置 output 选项可以控制 webpack 如何向硬盘写入编译文件。注意，即使可以存在多个入口起点，但只指定一个输出配置。




### 单个出口用法

在 webpack 中配置 output 属性的最低要求是，将它的值设置为一个对象，包括以下两点：

* filename 用于输出文件的文件名。
+ 目标输出目录 path 的绝对路径。


{% codeblock lang:javaScript %}
const config = {
  output: {
    filename: 'bundle.js',
    path: '/home/proj/public/assets'
  }
};

module.exports = config;
{% endcodeblock %}



-----
<!--more-->

### 多个出口

如果配置创建了多个单独的 "chunk"（例如，使用多个入口起点或使用像 CommonsChunkPlugin 这样的插件），则应该使用占位符(substitutions)来确保每个文件具有唯一的名称。

{% codeblock lang:javaScript %}
{
  entry: {
    app: './src/app.js',
    search: './src/search.js'
  },
  output: {
    filename: '[name].js',
    path: __dirname + '/dist'
  }
}

// 写入到硬盘：./dist/app.js, ./dist/search.js
{% endcodeblock %}
