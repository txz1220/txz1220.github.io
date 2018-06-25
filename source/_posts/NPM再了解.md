---
title: npm 再了解
categories:
- 技术
- npm
tags:
- Rnpm
---

虽然之前已经学习并使用过npm了，这篇文章主要为了总结并学习的。

<!--more-->

### npm模块管理器

npm的出现则是为了在CommonJS规范的基础上，实现解决包的安装卸载，依赖管理，版本管理等问题,npm不需要单独安装。在安装Node的时候，会连带一起安装npm

允许用户从NPM服务器下载别人编写的第三方包到本地使用。
允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。
允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。


### npm包

一个符合CommonJS规范的包应该是如下这种结构：

- 一个package.json文件应该存在于包顶级目录下
- 二进制文件应该包含在bin目录下。
- JavaScript代码应该包含在lib目录下。
- 文档应该在doc目录下。
- 单元测试应该在test目录下

### package.json

- name：包名，需要在NPM上是唯一的，小写字母和数字组成可包含_ - .但不能有空格
- description：包简介。通常会显示在一些列表中
- version：版本号。一个语义化的版本号（http://semver.org/ ），通常为x.y.z。该版本号十分重要，常常用于一些版本控制的场合
- keywords：关键字数组。用于NPM中的分类搜索
- maintainers：包维护者的数组。数组元素是一个包含name、email、web三个属性的JSON对象
- contributors：包贡献者的数组。第一个就是包的作者本人。在开源社区，如果提交的patch被merge进master分支的话，就应当加上这    个贡献patch的人。格式包含name和email
- bugs：一个可以提交bug的URL地址。可以是邮件地址（mailto:mailxx@domain），也可以是网页地址
- licenses：包所使用的许可证
- repositories：托管源代码的地址数组
- dependencies：当前包需要的依赖。这个属性十分重要，NPM会通过这个属性，帮你自动加载依赖的包


### npm的使用

查看各种信息

```npm
# 查看 npm 命令列表
$ npm help

# 查看各个命令的简单用法
$ npm -l

# 查看 npm 的版本
$ npm -v

# 查看 npm 的配置
$ npm config list -l
```

### npm 命令安装模块

Node模块采用npm install命令安装。

每个模块可以“全局安装”，也可以“本地安装”。“全局安装”指的是将一个模块安装到系统目录中，各个项目都可以调用。一般来说，全局安装只适用于工具模块。“本地安装”指的是将一个模块下载到当前项目的node_modules子目录，然后只有在项目目录之中，才能调用这个模块。


#### 本地安装

$ npm install <package name>

#### 全局安装
$ sudo npm install -global <package name>
$ sudo npm install -g <package name>

指定所安装的模块属于哪一种性质的依赖关系

- –save：模块名将被添加到dependencies，可以简化为参数-S。
- –save-dev: 模块名将被添加到devDependencies，可以简化为参数-D。

$ npm install <package name> --save
$ npm install <package name> --save-dev


#### 卸载模块
我们可以使用以下命令来卸载 Node.js 模块

$ npm uninstall <package name>

#### 更新模块
我们可以使用以下命令来卸载 Node.js 模块

$ npm update <package name>


#### 创建模块

我们可以使用以下命令来创建 Node.js 模块

$ npm init


#### npm init创建模块会在交互命令行帮我们生产package.json文件


```npm
$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
name: (node_modules) test                   # 模块名
version: (1.0.0) 
description: Node.js 测试模块                # 描述
entry point: (index.js) 
test command: make test
git repository: https://github.com/test/test.git  # Github 地址
keywords: 
author: 
license: (ISC) 
About to write to ……/node_modules/package.json:      # 生成地址

{
  "name": "test",
  "version": "1.0.0",
  "description": "Node.js 测试模块",
  ……
}


Is this ok? (yes) yes
```


#### 模块发布

发布模块前首先要在npm注册用户

$ npm adduser
Username: liuxing
Password:
Email: (this IS public) ogilhinn@gmail.com

然后

$ npm publish
现在我们的npm包就成功发布了。