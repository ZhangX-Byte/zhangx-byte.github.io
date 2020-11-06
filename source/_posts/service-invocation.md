---
title: 服务调用
catalog: true
toc_nav_num: true
date: 2020-09-15 19:49:52
subtitle: docs/concepts/service-invocation/
header-img: /img/dapr/dapr.svg
tags:
- Dapr
- 原文翻译
catagories:
- Dapr
---

## 服务调用

[Service Invocation](https://github.com/dapr/docs/tree/master/concepts/service-invocation)

---

使用服务调用 API,你的微服务可以找到其它微服务，并且在你的系统中使用标准协议（当前支持 gRPC 或者 HTTP）进行可靠通讯。

以下是一个 Dapr 服务调用如何工作的高度概括。

![](/img/dapr/service-invocation.png)

1. 服务 A 对服务 B 发起一个 http/gRPC 请求。请求进入到本地 Dapr 边车。
2. Dapr 发现服务 B 的位置并且转发消息到服务 B 的 Dapr 边车。
3. 服务 B 的 Dapr 边车转发请求到服务 B 。服务 B 执行它的业务逻辑响应。
4. 服务 B 发送一个响应到服务 A 。这个响应进入到服务 B 的边车。
5. Dapr 转发响应到服务 A 的 Dapr 边车。
6. 服务 A 接收响应。

作为上面的内容描述的例子，假设我们有以下示例描述的应用程序集合，一个 python 应用程序调用一个 Noed.js 应用程序：https://github.com/dapr/quickstarts/blob/master/hello-kubernetes/README.md

在这样的情景下，python 应用程序作为上面提到的“Service A”，Node.js 应用程序作为"Service B"。

在例子的上下文中，以下1-6项再一次描述：

1. 假设 Node.js 应用程序有一个 Dapr 应用程序 id “nodeapp”，如示例所示。python 应用程序通过 http://localhost:3500/v1.0/invoke/nodeapp/method/neworder 调用 Node.js 应用程序的 neworder 方法，它首先进入 python 应用程序的本地 Dapr 边车。
2. Dapr 发现 Node.js 应用程序的位置并且转发请求到 Node.js 应用程序的边车。
3. Node.js 应用程序的边车转发请求到 Node.js 应用程序。Node.js 应用程序执行它的业务逻辑（就像在示例中描述的一样）记录进入的消息然后持久化订单 ID 到 Redis 中（上面的图中未显示）。

第 4-5 步和上面列表一样。

## 下一步

---

如果你已经准备好开始了，跟着这个指引概述[如何开始一个服务调用]()

如果你想要知道更多关于服务调用如何工作的技术细节，异步到[API 规范]()
