---
title: 服务调用 API 规范
catalog: true
toc_nav_num: true
date: 2020-09-15 22:21:27
subtitle: docs/reference/api/
header-img: /img/dapr/dapr.svg
tags:
- Dapr
- 原文翻译
catagories:
- Dapr
---

## 服务调用 API 规范

---

Dapr 给用户提供使用唯一 ID 调用其它应用程序的能力。这个功能允许应用程序通过名称标识符和其它应用程序交互，把服务发现的重担交给 Dapr 运行时。

### 内容

- 在远程 Dapr 应用程序上调用一个方法

### 在远程 Dapr 应用程序上调用一个方法

---

这个终端使你能够调用另一个 Dapr 应用程序启用的方法。

#### HTTP 请求

``` cmd
POST/GET/PUT/DELETE http://localhost:<daprPort>/v1.0/invoke/<appId>/method/<method-name>
```

#### HTTP 应答编码

当一个服务通过 Dapr 调用另一个服务时，被调用的服务状态码会返回给调用方。如果有网络错误或者其它瞬态错误， Dapr 将会返回 `500` 错误并带着详细错误信息。

如果用户通过HTTP调用Dapr来与启用了gRPC的服务对话，被调用的 gRPC 服务错误返回 `500` ，成功返回 `200OK`。

代码|描述
--|--
500|请求失败

#### URL 参数

参数|描述
--|--
daprPort｜Dapr 端口
appId｜远程应用程序 ID
method-name｜调用远程应用程序的方法名称或者 url

#### 请求内容

在请求中，你可以传递请求头：

``` json
{
  "Content-Type": "application/json"
}
```

在请求消息体中放置你想发送到服务的数据：

``` json
{
  "arg1": 10,
  "arg2": 23,
  "operator": "+"
}
```

#### 通过调用服务接收请求

一旦你的服务代码通过 Dapr 调用另一个服务启用的方法，Dapr 将会发送请求（伴随着请求头和消息体）到应用的 `<method-name>` 终端。

被调用的 Dapr 应用程序监听并且在那个终端应答请求。

#### 跨命名空间调用

在支持命名空间的托管平台，Dapr 应用程序 ID 遵循有效的 FQDN（Fully Qualified Domain Name，全限定域名）转换，包含目标命名空间。例如，以下字符串包含应用程序 ID（myApp），此外应用程序运行的命名空间（production）。

``` cmd
myApp.production
```

支持命名空间平台

- K8S

#### 示例

调用 `mathService` 中的 `add` 方法：

``` curl
curl http://localhost:3500/v1.0/invoke/mathService/method/add \
  -H "Content-Type: application/json"
  -d '{ "arg1": 10, "arg2": 23}'
```

`mathService` 服务需要监听 `/add` 终端以接收和处理请求。

Node 应用程序像这样：

``` nodejs
app.post('/add', (req, res) => {
  let args = req.body;
  const [operandOne, operandTwo] = [Number(args['arg1']), Number(args['arg2'])];
  
  let result = operandOne + operandTwo;
  res.send(result.toString());
});

app.listen(port, () => console.log(`Listening on port ${port}!`));
```

> 远程终端应答将在应答消息体中返回。

如果你的服务监听路径嵌套较多（比如：`/api/v1/add`），Dapr 实现了完整的反向代理，所以你可以追加所有需要的路径分段到你的请求 URL 里，例如：

``` url
http://localhost:3500/v1.0/invoke/mathService/method/api/v1/add
```

如果你调用的 `mathService` 在不同的命名空间中，你可以使用下列 URL：

``` url
http://localhost:3500/v1.0/invoke/mathService.testing/method/api/v1/add
```

在这个 URL 中，`testing` 是 `mathService` 运行的命名空间。
