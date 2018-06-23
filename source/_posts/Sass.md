---
title: Sass学习
categories:
- 技术
- Sass
tags:
- Sass
---

### 一、安装

由于Sass是基于ruby的，所以先安装ruby。

Ruby 安装完成后，在开始菜单中找到新安装的 Ruby，并启动 Ruby 的 Command 控制面板：Start Command Prompt with Ruby

1、通过命令安装 Sass

```
gem install sass
```

##### 使用国内淘宝镜像gem。 
第一步：gem sources –remove https://rubygems.org/ 删除自带gem 
第二步：gem sources -a https://ruby.taobao.org/ 添加国内淘宝镜像gem 
第三步：gem sources 显示下载的gem信息 

##### 查看版本
`sass -v`

#### 更新：
`gem update sass`

#### 删除
`gem uninstall sass `

<!--more-->
后缀sass 和scss 的区别：

sass 不用{} 包裹， 而scss可以包裹。建议使用scss。

示例：

```scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```


### 二、Sass编译

- 命令编译
- GUI工具编译
- 自动化编译

#### 1、命令编译

单文件编译：

> sass <要编译的Sass文件路径>/style.scss:<要输出CSS文件路径>/style.css
 
 多文件编译：

 sass sass/:css/

 上面的命令表示将项目中“sass”文件夹中所有“.scss”(“.sass”)文件编译成“.css”文件，并且将这些 CSS 文件都放在项目中“css”文件夹中。

####  2、GUI 界面工具编译

就推荐[Koala](http://koala-app.com/)

其他就不介绍了。

#### 3、自动化编译

> * Grunt 
> * Gulp

具体配置自行查看文档


### 三、常见错误：

>最为常见的一个错误就是字符编译引起的。在Sass的编译的过程中，是不是支持“GBK”编码的。所以在创建 Sass 文件时，就需要将文件编码设置为“utf-8”。

>另外一个错误就是路径中的中文字符引起的。建议在项目中文件命名或者文件目录命名不要使用中文字符。而至于人为失误造成的编译失败，在编译过程中都会有具体的说明，大家可以根据编译器提供的错误信息进行对应的修改。

### 四、不同样式风格的输出方法

- 嵌套输出方式 nested
- 展开输出方式 expanded  
- 紧凑输出方式 compact 
- 压缩输出方式 compressed

#### 4.1嵌套输出方式 nested

语法：
```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

在编译的时候带上参数“ --style nested”:
sass --watch test.scss:test.css --style nested

编译出来的 CSS 样式风格：
```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none; }
nav li {
  display: inline-block; }
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none; }
  ```

#### 4.2 展开输出方式 expanded

语法：
```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```
在编译的时候带上参数“ --style expanded”:

sass --watch test.scss:test.css --style expanded

这个输出的 CSS 样式风格和 nested 类似，只是大括号在另起一行，同样上面的代码，编译出来：
```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```
#### 4.3 紧凑输出方式 compact

语法：
```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```
在编译的时候带上参数“ --style compact”:

sass --watch test.scss:test.css --style compact

该方式适合那些喜欢单行 CSS 样式格式的朋友，编译后的代码如下：

```css
nav ul { margin: 0; padding: 0; list-style: none; }
nav li { display: inline-block; }
nav a { display: block; padding: 6px 12px; text-decoration: none; }
```

#### 4.4 压缩输出方式 compressed

在编译的时候带上参数“ --style compressed”:

sass --watch test.scss:test.css --style compressed

压缩输出方式会去掉标准的 Sass 和 CSS 注释及空格。也就是压缩好的 CSS 代码样式风格：


