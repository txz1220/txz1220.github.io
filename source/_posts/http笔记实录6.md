---
title: HTTP笔记实录6
categories:
- 技术
- HTTP      
tags:
- HTTP
---

### 第 6 章　HTTP 首部

#### 6.1　HTTP 报文首部

HTTP 协议的请求和响应报文中必定包含 HTTP 首部。首部内容为客户端和服务器分别处理请求和响应提供所需要的信息。对于客户端户来说，这些信息中的大部分内容都无须亲自查看。报文首部由几个字段构成。

<!--more-->

##### HTTP 请求报文
在请求中，HTTP 报文由方法、URI、HTTP 版本、HTTP 首部字段等部分构成。


##### HTTP 响应报文

在响应中，HTTP 报文由 HTTP 版本、状态码（数字和原因短语）、 HTTP 首部字段 3 部分构成。

#### 6.2　HTTP 首部字段

##### 6.2.1　HTTP 首部字段传递重要信息


HTTP 首部字段是构成 HTTP 报文的要素之一。在客户端与服务器之 间以 HTTP 协议进行通信的过程中，无论是请求还是响应都会使用首 部字段，它能起到传递额外重要信息的作用。

使用首部字段是为了给浏览器和服务器提供报文主体大小、所使用的 语言、认证信息等内容。

![](https://ws1.sinaimg.cn/large/006c6oKBgy1ftl99jyp7oj30no0b9gq4.jpg)


##### 6.2.2　HTTP 首部字段结构

HTTP 首部字段是由首部字段名和字段值构成的，中间用冒号“:” 分 隔。

Content-Type: text/html



##### 6.2.3　4 种 HTTP 首部字段类型

HTTP 首部字段根据实际用途被分为以下 4 种类型。

- 通用首部字段（General Header Fields）

请求报文和响应报文两方都会使用的首部。

- 请求首部字段（Request Header Fields）

从客户端向服务器端发送请求报文时使用的首部。补充了请求的附加 内容、客户端信息、响应内容相关优先级等信息。

- 响应首部字段（Response Header Fields）

从服务器端向客户端返回响应报文时使用的首部。补充了响应的附加 内容，也会要求客户端附加额外的内容信息。

- 实体首部字段（Entity Header Fields）

针对请求报文和响应报文的实体部分使用的首部。补充了资源内容更 新时间等与实体有关的信息。


##### 6.2.4　HTTP/1.1 首部字段一览

![](https://ws1.sinaimg.cn/large/006c6oKBgy1ftl9lyf6jcj30k30bwn3h.jpg)

###### 请求首部字段

![](https://ws1.sinaimg.cn/large/006c6oKBgy1ftl9mieukej30hm0kf177.jpg)

![](https://ws1.sinaimg.cn/large/006c6oKBgy1ftl9mtbl8rj30k00buahb.jpg)

![](https://ws1.sinaimg.cn/large/006c6oKBgy1ftl9n4mys9j30jn0d1qa9.jpg)

#### 6.3　HTTP/1.1 通用首部字段

通用首部字段是指，请求报文和响应报文双方都会使用的首部。

##### 6.3.1　Cache-Control

通过指定首部字段 Cache-Control 的指令，就能操作缓存的工作机 制。

![](https://ws1.sinaimg.cn/large/006c6oKBgy1ftl9pko8g3j30mw0a877h.jpg)

指令的参数是可选的，多个指令之间通过“,”分隔。首部字段 CacheControl 的指令可用于请求及响应时。

Cache-Control: private, max-age=0, no-cache

![](https://ws1.sinaimg.cn/large/006c6oKBgy1ftl9qs4wcej30kf0b745x.jpg)

![](https://ws1.sinaimg.cn/large/006c6oKBgy1ftl9rn86k2j30n30ean7o.jpg)


表示是否能缓存的指令

public 指令

Cache-Control: public

当指定使用 public 指令时，则明确表明其他用户也可利用缓存。 private 指令


Cache-Control: private

当指定 private 指令后，响应只以特定的用户作为对象，这与 public 指令的行为相反。 缓存服务器会对该特定用户提供资源缓存的服务，对于其他用户发送 过来的请求，代理服务器则不会返回缓存。


no-cache 指令
https://ws1.sinaimg.cn/large/006c6oKBgy1ftl9tzf3bzj30jh09kmzu.jpg


Cache-Control: no-cache

使用 no-cache 指令的目的是为了防止从缓存中返回过期的资源。

客户端发送的请求中如果包含 no-cache 指令，则表示客户端将不会接 收缓存过的响应。于是，“中间”的缓存服务器必须把客户端请求转发 给源服务器。

如果服务器返回的响应中包含 no-cache 指令，那么缓存服务器不能对 资源进行缓存。源服务器以后也将不再对缓存服务器请求中提出的资 源有效性进行确认，且禁止其对响应资源进行缓存操作。

Cache-Control: no-cache=Location

由服务器返回的响应中，若报文首部字段 Cache-Control 中对 no-cache 字段名具体指定参数值，那么客户端在接收到这个被指定参数值的首 部字段对应的响应报文后，就不能使用缓存。换言之，无参数值的首 部字段可以使用缓存。只能在响应指令中指定该参数。


控制可执行缓存的对象的指令

no-store 指令

Cache-Control: no-store

当使用 no-store 指令机密信息时，暗示请求（和对应的响应）或响应中包含机密信息。

>从字面意思上很容易把 no-cache 误解成为不缓存，但事实上 no-cache 代表不缓 存过期的资源，缓存会向源服务器进行有效期确认后处理资源，也许称为 do-notserve-from-cache-without-revalidation 更合适。no-store 才是真正地不进行缓存。



指定缓存期限和认证的指令

s-maxage 指令

Cache-Control: s-maxage=604800（单位 ：秒）


s-maxage 指令的功能和 max-age 指令的相同，它们的不同点是 smaxage 指令只适用于供多位用户使用的公共缓存服务器。也就是说，对于向同一用户重复返回响应的服务器来说，这个指令没有任何作用。


当客户端发送的请求中包含 max-age 指令时，如果判定缓存资源的缓 存时间数值比指定时间的数值更小，那么客户端就接收缓存的资源。 另外，当指定 max-age 值为 0，那么缓存服务器通常需要将请求转发给源服务器。

当服务器返回的响应中包含 max-age 指令时，缓存服务器将不对资源的有效性再作确认，而 max-age 数值代表资源保存为缓存的最长时间。


max-stale 指令

Cache-Control: max-stale=3600（单位：秒）

使用 max-stale 可指示缓存资源，即使过期也照常接收。

如果指令未指定参数值，那么无论经过多久，客户端都会接收响应； 如果指令中指定了具体数值，那么即使过期，只要仍处于 max-stale 指定的时间内，仍旧会被客户端接收。


only-if-cached 指令

Cache-Control: only-if-cached

使用 only-if-cached 指令表示客户端仅在缓存服务器本地缓存目标资 源的情况下才会要求其返回。换言之，该指令要求缓存服务器不重新 加载响应，也不会再次确认资源有效性。若发生请求缓存服务器的本 地缓存无响应，则返回状态码 504 Gateway Timeout。


must-revalidate 指令

Cache-Control: must-revalidate

使用 must-revalidate 指令，代理会向源服务器再次验证即将返回的响 应缓存目前是否仍然有效。

若代理无法连通源服务器再次获取有效资源的话，缓存必须给客户端 一条 504（Gateway Timeout）状态码。

另外，使用 must-revalidate 指令会忽略请求的 max-stale 指令（即使已 经在首部使用了 max-stale，也不会再有效果）。


proxy-revalidate 指令

Cache-Control: proxy-revalidate

proxy-revalidate 指令要求所有的缓存服务器在接收到客户端带有该指 令的请求返回响应之前，必须再次验证缓存的有效性。

no-transform 指令

Cache-Control: no-transform

使用 no-transform 指令规定无论是在请求还是响应中，缓存都不能改 变实体主体的媒体类型。

这样做可防止缓存或代理压缩图片等类似操作。


##### 6.3.2　Connection

Connection 首部字段具备如下两个作用。

- 控制不再转发给代理的首部字段 
- 管理持久连接


![](https://ws1.sinaimg.cn/large/006c6oKBgy1ftla7tr9o6j30ma0afaez.jpg)


Connection: 不再转发的首部字段名

在客户端发送请求和服务器返回响应内，使用 Connection 首部字 段，可控制不再转发给代理的首部字段（即 Hop-by-hop 首 部）。


![](https://ws1.sinaimg.cn/large/006c6oKBgy1ftla97ti96j30j808vq53.jpg)


Connection: close

HTTP/1.1 版本的默认连接都是持久连接。为此，客户端会在持 久连接上连续发送请求。当服务器端想明确断开连接时，则指定 Connection 首部字段的值为 Close。


Connection: Keep-Alive

HTTP/1.1 之前的 HTTP 版本的默认连接都是非持久连接。为 此，如果想在旧版本的 HTTP 协议上维持持续连接，则需要指定 Connection 首部字段的值为 Keep-Alive。


##### 6.3.3　Date

首部字段 Date 表明创建 HTTP 报文的日期和时间。


##### 6.3.4　Pragma

Pragma 是 HTTP/1.1 之前版本的历史遗留字段，仅作为与 HTTP/1.0 的向后兼容而定义。

规范定义的形式唯一，如下所示。

Pragma: no-cache

该首部字段属于通用首部字段，但只用在客户端发送的请求中。客户 端会要求所有的中间服务器不返回缓存的资源。


所有的中间服务器如果都能以 HTTP/1.1 为基准，那直接采用 CacheControl: no-cache 指定缓存的处理方式是最为理想的。但要整体掌握 全部中间服务器使用的 HTTP 协议版本却是不现实的。因此，发送的 请求会同时含有下面两个首部字段。

Cache-Control: no-cache Pragma: no-cache


##### 6.3.5　Trailer

首部字段 Trailer 会事先说明在报文主体后记录了哪些首部字段。该 首部字段可应用在 HTTP/1.1 版本分块传输编码时。


##### 6.3.6　Transfer-Encoding

首部字段 Transfer-Encoding 规定了传输报文主体时采用的编码方式。

##### 6.3.7　Upgrade

首部字段 Upgrade 用于检测 HTTP 协议及其他协议是否可使用更高的 版本进行通信，其参数值可以用来指定一个完全不同的通信协议。

![](https://ws1.sinaimg.cn/large/006c6oKBgy1ftlah3ynz9j30mn09u79a.jpg)

上图用例中，首部字段 Upgrade 指定的值为 TLS/1.0。请注意此处两 个字段首部字段的对应关系，Connection 的值被指定为 Upgrade。 Upgrade 首部字段产生作用的 Upgrade 对象仅限于客户端和邻接服务 器之间。因此，使用首部字段 Upgrade 时，还需要额外指定 Connection:Upgrade。

对于附有首部字段 Upgrade 的请求，服务器可用 101 Switching Protocols 状态码作为响应返回。


##### 6.3.8　Via

使用首部字段 Via 是为了追踪客户端与服务器之间的请求和响应报文 的传输路径。

报文经过代理或网关时，会先在首部字段 Via 中附加该服务器的信 息，然后再进行转发。这个做法和 traceroute 及电子邮件的 Received 首部的工作机制很类似。

首部字段 Via 不仅用于追踪报文的转发，还可避免请求回环的发生。 所以必须在经过代理时附加该首部字段内容。


![](https://ws1.sinaimg.cn/large/006c6oKBgy1ftlaiou300j30ng0efn2o.jpg)


##### 6.3.9　Warning

HTTP/1.1 的 Warning 首部是从 HTTP/1.0 的响应首部（Retry-After）演 变过来的。该首部通常会告知用户一些与缓存相关的问题的警告。

Warning: 113 gw.hackr.jp:8080 "Heuristic expiration" Tue, 03 Jul 2012

Warning 首部的格式如下。最后的日期时间部分可省略。

Warning: `[警告码][警告的主机:端口号]`“[警告内容]”([日期时间])

HTTP/1.1 中定义了 7 种警告。警告码对应的警告内容仅推荐参考。 另外，警告码具备扩展性，今后有可能追加新的警告码。

![](https://ws1.sinaimg.cn/large/006c6oKBgy1ftlakqs9q8j30mo0d8tjz.jpg)


#### 6.4　请求首部字段

<待续>