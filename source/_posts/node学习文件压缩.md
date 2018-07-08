---
title: node 文件压缩
categories:
- 技术
- node.js
- 文件压缩
tags:
- node.js
- 文件压缩
---

## 简单的压/解压缩


### 压缩

在nodejs里，是如何对资源进行压缩的呢------Zlib模块。

```js
var fs = require ('fs');

var zlib = require('zlib');

var gzip = zlib.createGzip();

var inFile = fs.createReadStream('./extra/fileForCompress.txt')

var out = fs.createWriteStream(./extra/fileForCompress.txt.gz;)

inFile.pipe(gzip).pipe(out);
```
<!--more-->

### 解压的例子

反向操作：

```js
var fs = require('fs');
var zlib = require('zlib');

var gunzip = zlib.createGunzip();

var inFile = fs.createReadStream('./extra/fileForCompress.txt.gz');
var outFile = fs.createWriteStream('./extra/fileForCompress1.txt');

inFile.pipe(gunzip).pipe(outFile);
```


### 服务端gzip压缩

首先判断 是否包含 accept-encoding 首部，且值为gzip。

- 否：返回未压缩的文件。
- 是：返回gzip压缩后的文件。

```js
var http = require('http');
var zlib = require('zlib');
var fs = require('fs');

var filepath = './extra/fileForGzip.html'

var server = http.createServer(function(req,res){
    var acceptEncoding = req.headers['accept-encoding'];
    var gzip;
    if(acceptEncoding.indexOf('gzip')!=-1){
        gzip = zlib.createGzip();
        res.writeHead(200,{
            'Content-Encoding' : 'gzip'
        });
        fs.createReadStream(filepath).pipe(gzip).pipe(res);
    }else{
        fs.createReadStream(filepath).pipe(res);
    }
})

server.listen('3000');

```

### 服务端字符串gzip压缩

代码跟前面例子大同小异。这里采用了**slib.gzipSync(str)**对字符串进行gzip压缩。

```js
var http = require('http');
var zlib = require('zlib');

var responseText = 'hello world';

var server = http.createServer(function(req, res){
    var acceptEncoding = req.headers['accept-encoding'];
    if(acceptEncoding.indexOf('gzip')!=-1){
        res.writeHead(200, {
            'content-encoding': 'gzip'
        });
        res.end( zlib.gzipSync(responseText) );
    }else{
        res.end(responseText);
    }

});

server.listen('3000');
```


[学习来源](https://github.com/chyingp/nodejs-learning-guide)