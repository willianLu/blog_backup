---
title: HTTP 与 HTTPS的区别
date: 2021-02-28 10:00
comments: true
---

#### HTTP协议是什么

>HTTP 协议是超文本传输协议的缩写，英文是Hyper Text Transfer Protocol。它是一个基于请求与响应，无状态的，应用层的协议，常基于TCP/IP协议传输数据，互联网上应用最为广泛的一种网络协议。设计 HTTP 的初衷是为了提供一种发布和接收 HTML 页面的方法。

HTTP 有多个版本，目前广泛使用的是HTTP/1.1版本。
<!-- more -->

#### HTTP特点
- [请求和响应]：基本的特性，由客户端发起请求，服务端响应。
- [简单快速]：客户端向服务器请求服务时，只需传送请求方法和路径，请求方法常用的有get、post。
- [灵活]：HTTP允许传输任意类型的数据对象，传输的类型由Content-Type标记。
- [无连接]：限制每次连接只处理一个请求。服务器处理完请求，并收到客户端的应答后，即断开连接，但是却不利于客户端与服务器保持会话连接，为了弥补这种不足，产生了两项记录HTTP状态的技术，Cookie和Session。
- [无状态]：无状态是指协议对于事务处理没有记忆，后续处理需要前面的信息，则必须重传。

#### HTTP的缺点
- [明文传输]：数据完全肉眼可见，容易被劫持，缺乏安全性
- HTTP是不安全的，无法验证通信双方的身份，也不能判断报文是否被修改

#### 为什么要用HTTPS
HTTP 协议以明文方式传递信息，不提供任何方式的数据加密，不适合传输一些敏感信息，比如：各种账号、密码等信息，使用 HTTP 协议传输隐私信息非常不安全。为了解决上述 HTTP 存在的问题，就出现了 HTTPS。

#### 什么是HTTPS
>HTTPS （全称：Hyper Text Transfer Protocol over SecureSocket Layer），是以安全为目标的 HTTP 通道，在HTTP的基础上通过传输加密和身份认证保证了传输过程的安全性。HTTPS 在HTTP 的基础下加入SSL，HTTPS 的安全基础是 SSL，因此加密的详细内容就需要 SSL。 HTTPS 存在不同于 HTTP 的默认端口及一个加密/身份验证层（在 HTTP与 TCP 之间）。这个系统提供了身份验证与加密通讯方法。

HTTPS协议的主要作用可以分为两种：一种是建立一个信息安全通道，来保证数据传输的安全；另一种就是确认网站的真实性。

#### HTTPS传输数据的流程
- 首先客户端通过 URL 访问服务器建立 SSL 连接。
- 服务端收到客户端请求后，会将网站支持的证书信息（证书中包含公钥）传送一份给客户端。
- 客户端的服务器开始协商 SSL 连接的安全等级，也就是信息加密的等级。
- 客户端的浏览器根据双方同意的安全等级，建立会话密钥，然后利用网站的公钥将会话密钥加密，并传送给网站。
- 服务器利用自己的私钥解密出会话密钥。
- 服务器利用会话密钥加密与客户端之间的通信。

#### HTTPS的特点
- [内容加密]：采用混合加密技术，中间者无法直接查看明文内容
- [验证身份]：通过证书认证客户端访问的是自己的服务器（确认网站的真实性）
- [保护数据完整性]：防止传输的内容被中间人冒充或者篡改

#### HTTPS的缺点
- 相同网络环境下，HTTPS 协议会使页面的加载时间延长近 50%，增加 10%到 20%的耗电。此外，HTTPS 协议还会影响缓存，增加数据开销和功耗。
- HTTPS 协议的安全是有范围的，在黑客攻击、拒绝服务攻击和服务器劫持等方面几乎起不到什么作用。
- 最关键的是，SSL 证书的信用链体系并不安全。特别是在某些国家可以控制 CA 根证书的情况下，中间人攻击一样可行。
- 成本增加。部署 HTTPS 后，因为 HTTPS 协议的工作要增加额外的计算资源消耗，例如 SSL 协议加密算法和 SSL 交互次数将占用一定的计算资源和服务器成本。在大规模用户访问应用的场景下，服务器需要频繁地做加密和解密操作，几乎每一个字节都需要做加解密，这就产生了服务器成本。

#### HTTP与HTTPS的区别

- 安全性：HTTP 的连接很简单，是无状态的；HTTPS 协议是由 SSL+HTTP 协议构建的可进行加密传输、身份认证的网络协议，比 HTTP 协议安全。
- 连接端口：HTTP 标准端口是 80，而 HTTPS 的标准端口是 443。
- 费用：HTTPS 协议需要到 CA 申请证书，一般免费证书较少，因而需要一定费用
- 传输方式：HTTP 是超文本传输协议，信息是明文传输，而 HTTPS 是 SSL 加密传输协议。
- 工作层：在 OSI 网络模型中，HTTP 工作于应用层，而 HTTPS 工作在传输层。
- 工作耗时：HTTP 耗时=TCP 握手，而 HTTPS 耗时=TCP 握手+SSL 握手。
- 显示形式：HTTP 的 URL 以http://开头，而 HTTPS 的 URL 以https://开头。