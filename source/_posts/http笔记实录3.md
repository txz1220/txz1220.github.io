---
title: HTTP笔记实录3
categories:
- 技术
- HTTP      
tags:
- HTTP
---

### 第 3 章 HTTP 报文内的 HTTP信息

HTTP 通信过程包括从客户端发往服务器端的请求及从服务器端返回客户端的响应。 本章就让我们来了解一下请求和响应是怎样运作的。

#### 3.1 HTTP 报文

用于 HTTP 协议交互的信息被称为 HTTP 报文。 请求端（客户端） 的HTTP 报文叫做请求报文， 响应端（服务器端） 的叫做响应报文。
HTTP 报文本身是由多行（用 CR+LF 作换行符） 数据构成的字符串文本。


HTTP 报文大致可分为报文首部和报文主体两块。 两者由最初出现的空行（CR+LF） 来划分。 通常， 并不一定要有报文主体。

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsoptyegsjj30hj07egnq.jpg)

<!--more-->
#### 3.2 请求报文及响应报文的结构

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsoputzk8kj30hv09ddiv.jpg)

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsopvpcnktj30hk0glgu8.jpg)


请求行
包含用于请求的方法， 请求 URI 和 HTTP 版本。
状态行
包含表明响应结果的状态码， 原因短语和 HTTP 版本。
首部字段
包含表示请求和响应的各种条件和属性的各类首部。

一般有 4 种首部， 分别是： 通用首部、 请求首部、 响应首部和实体首部


#### 3.3 编码提升传输速率
HTTP 在传输数据时可以按照数据原貌直接传输， 但也可以在传输过程中通过编码提升传输速率。 通过在传输时编码， 能有效地处理大量
的访问请求。 但是， 编码的操作需要计算机来完成， 因此会消耗更多的 CPU 等资源。


##### 3.3.1 报文主体和实体主体的差异

- 报文（ message）
是 HTTP 通信中的基本单位， 由 8 位组字节流（octet sequence，其中 octet 为 8 个比特） 组成， 通过 HTTP 通信传输。

- 实体（entity）

作为请求或响应的有效载荷数据（补充项） 被传输， 其内容由实体首部和实体主体组成。



HTTP 报文的主体用于传输请求或响应的实体主体。

通常， 报文主体等于实体主体。 只有当传输中进行编码操作时， 实体主体的内容发生变化， 才导致它和报文主体产生差异


##### 3.3.2 压缩传输的内容编码

向待发送邮件内增加附件时， 为了使邮件容量变小， 我们会先用 ZIP压缩文件之后再添加附件发送。 HTTP 协议中有一种被称为内容编码
的功能也能进行类似的操作。

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsow8kk24bj30hj0h0adk.jpg)

##### 3.3.3 分割发送的分块传输编码


在 HTTP 通信过程中， 请求的编码实体资源尚未全部传输完成之前，浏览器无法显示请求页面。 在传输大容量数据时， 通过把数据分割成
多块， 能够让浏览器逐步显示页面。这种把实体主体分块的功能称为分块传输编码（Chunked Transfer Coding） 。


#### 3.4 发送多种数据的多部分对象集合

多部分对象集合包含的对象如下。
- multipart/form-data

在 Web 表单文件上传时使用。

- multipart/byteranges

状态码 206（Partial Content， 部分内容） 响应报文包含了多个范
围的内容时使用。



在 HTTP 报文中使用多部分对象集合时， 需要在首部字段里加上
Content-type。 有关这个首部字段， 我们稍后讲解。


#### 3.5 获取部分内容的范围请求

以前， 用户不能使用现在这种高速的带宽访问互联网， 当时， 下载一个尺寸稍大的图片或文件就已经很吃力了。 如果下载过程中遇到网络
中断的情况， 那就必须重头开始。 为了解决上述问题， 需要一种可恢复的机制。 所谓恢复是指能从之前下载中断处恢复下载。

要实现该功能需要指定下载的实体范围。 像这样， 指定范围发送的请求叫做范围请求（ Range Request） 。

执行范围请求时， 会用到首部字段 Range 来指定资源的 byte 范围。

byte 范围的指定形式如下。

![](https://ws1.sinaimg.cn/large/006c6oKBgy1fsowgv71dnj30ha07bdgf.jpg)


#### 3.6 内容协商返回最合适的内容

同一个 Web 网站有可能存在着多份相同内容的页面。 比如英语版和中文版的 Web 页面， 它们内容上虽相同， 但使用的语言却不同。

当浏览器的默认语言为英语或中文， 访问相同 URI 的 Web 页面时，则会显示对应的英语版或中文版的 Web 页面。 这样的机制称为内容
协商（Content Negotiation） 。

包含在请求报文中的某些首部字段（如下） 就是判断的基准。 这些首部字段的详细说明请参考下一章。

Accept
Accept-Charset
Accept-Encoding
Accept-Language
Content-Languag


内容协商技术有以下 3 种类型：

服务器驱动协商（ Server-driven Negotiation）

服务器驱动协商（ Server-driven Negotiation）

透明协商（ Transparent Negotiation）