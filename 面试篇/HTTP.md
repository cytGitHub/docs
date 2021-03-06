# HTTP

- 什么是 HTTP?
  - 应用层协议，基于 TCP/IP。
- 什么是 Http 事务?
  - 一次完整的请求加相应
- Http1.0 和 http1.1 的区别？
  - http1.0 不支持 host 域，它认为每台服务器都应该绑定一个 Ip 地址。
  - http1.1 默认开启 keep-alive，在一个 Tcp 链接上可以发送多个 http 请求，减少建立链接和关闭链接的消耗延迟。
  - http1.1 引入了更多的缓存策略，以及新增了一些错误状态码
- 什么是 Https，Https 和 Http 的区别是什么？
  - Https = Http + ssl
  - http 是明文传输，传输内容可以被窃取篡改
  - https 是在 http 的基础之上添加了一层加密协议。
- 什么是 keep-alive？keep-alive 断开的情况？
  - 在一次 Http 事务结束之后，可以继续保持 Tcp 连接处于打开状态，以便下一次请求能够复用当前的连接
  - keep-alive 并不会保证连接处于有效状态，如果设置了超时时间，那么连接也会断开
  - 如果服务端设置了 max 最大连接次数，那么也会断开
  
- 什么是 SSL？
  - SSL 是一个二进制协议，位于 TCP/IP 和应用层协议之间，为数据通信提供安全支持。在客户端发送加密数据之前，进行握手
- 什么是对称加密？什么是非对称加密？对称加密的缺点有哪些？
  - 对称加密就是客户端和服务端采用同一个秘钥进行加密解密
  - 非对称加密就是客户端和服务端采用不同秘钥进行加密解密
  - 对称加密的缺点是数据在传输之前，客户端和服务端要商定好秘钥，如果有一方泄露，也会造成安全隐患
- 介绍一下 HTTP 缓存？什么是强缓存？什么是协商缓存？
  - Http1.0 中，设置缓存的字段是 express
  - Http1.1 中，cache-control
  - 强缓存：如果在缓存数据未失效的情况下，那么就会直接使用浏览器的缓存数据，不会像服务器发送任何请求，强缓存生效的状态码 200
  - 协商缓存就是当请求头中没有强缓存属性的时候，浏览器第二次发起请求的情况下就会服务器进行协商，服务器判断资源是否进行了修改，如果没有被修改，返回 304 的状态码，浏览器就会用缓存中的数据，这样会减少服务器的传输压力。如果有更新，就会返回 200 状态码，并且将资源一并返回。
- Http 的三次握手和四次挥手讲一下？
- Http 和 Https 的默认端口是什么？
  - http 默认端口是 80
  - https 默认端口是 443
- Http Get 和 Post 的区别？
  - Get 请求参数可以被用户发现，是放在 url 上，Post 请求参数是在请求体中
  - Get 会发送一次数据包， Post 会发送两次数据包
- 什么是 TCP/IP 协议
  - Tcp，传输控制层协议。
  - 能够在不同网络间进行信息传输的协议簇！TCP/IP 协议不仅包含 TCP,IP,同时还包含其他协议！所以是一个协议簇
- 什么是 DNS?
  - 定义：域名服务系统，域名和 ip 地址相互映射的分布式数据库
- 地址栏中输入 url 发生了什么？
- Http 的特点有哪些？
- Http 请求的报文分为哪三个部分？
  - 请求行
    - 请求方法
    - 请求地址
    - 请求参数
  - 请求头
    - Accept：浏览器或者客户端能够接收的 MIME 文件类型
    - host：请求地址
    - Accept-Langeuage：浏览器能够接受的语言种类
    - connection：是否维持长链接
    - Referer：发送请求的 url 地址
    - user-agent：浏览器名称
    - content-type：请求的内容类型
    - Content-Length：数据长度
  - 请求体
- Http 的状态码？100-500 都是什么含义？
  - 100-199：信息状态码
  - 200-299：成功状态码
  - 300-399：重定向状态码
  - 400-499：客户端错误状态码
  - 500-599：服务端错误状态码
- DNS 解析的过程？
  - 从缓存中解析
  - 找本机的 hosts 文件
  - 从 Dns 服务器中寻找
- SSL4 次握手的过程？

- 什么是 webSocket?
  - websocket 是 h5 提出的新协议，是一种全双工通信协议，服务端可以进行推送的一种技术

* websocket 和 socket 的区别？
  - socket 是 TCP/IP 的抽象层，是一组接口，websocket 是应用层的完整协议，包含一套标准的 api
* http 和 websocket 的区别？
  - http 协议是短连接，每次请求完毕之后，都会断掉,而 webSocket 是长链接，在链接建立之后，所有的通信都会走该 TCP 通道 ，。

* HTTP1.0定义了三种请求方法： GET, POST 和 HEAD方法
* HTTP1.1新增了五种请求方法：OPTIONS, PUT, DELETE, TRACE 和 CONNECT
* 幂等
  * 在编程中一个幂等操作的特点是其任意多次执行所产生的影响均与一次执行的影响相同。

* https解决的问题
  * https://www.rrfed.com/2017/02/03/https/  