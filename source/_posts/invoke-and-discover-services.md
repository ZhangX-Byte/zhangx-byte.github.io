---
title: 调用远程服务
catalog: true
toc_nav_num: true
date: 2020-09-15 20:57:09
subtitle: docs/howto/invoke-and-discover-services/
header-img: /img/dapr/dapr.svg
tags:
- Dapr
- 原文翻译
catagories:
- Dapr
---

## 调用远程服务

---

在很多环境中，多个服务需要互相通讯，开发者常常会问自己以下问题：

- 如何发现和调用不同的服务？
- 如何处理重试和瞬态错误？
- 如何正确使用分布式跟踪来查看调用图？

Dapr 通过提供一个端点，将反向代理与内置服务发现结合起来，同时利用内置分布式跟踪和错误处理，可以使开发人员克服这些挑战。

更多关于服务调用的信息，阅读{% post_link service-invocation 概念文档 %}

### 为你的服务选择 ID

Dapr 允许你为应用程序分配一个全局、唯一的 ID。

这个 ID 封装你的应用程序状态，不管有多少个实例。

#### 使用 Dapr 命令行界面设置 ID

在标准模式下，设置 --app-id 标记：

``` CMD
dapr run --app-id cart --app-port 5000 python app.py
```

#### 使用 K8S 设置 ID

在 K8S 中，在 pod 中设置 dapr.io/app-id ：

``` yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: python-app
  namespace: default
  labels:
    app: python-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: python-app
  template:
    metadata:
      labels:
        app: python-app
      annotations:
        dapr.io/enabled: "true"
        dapr.io/app-id: "cart"
        dapr.io/app-port: "5000"
...

```

#### 在代码中调用服务

Dapr 使用边车、去中心化架构。使用 Dapr 调用应用程序，你可以在你的集群/环境使用 `invoke` 端点。

边车编程模式鼓励每个应用程序和它自己的 Dapr 实例沟通。Dapr 实例相互发现并通讯。

*注意：以下是一个 Python cart 应用程序实例。它可以使用任何编程语言实现*

``` python
from flask import Flask
app = Flask(__name__)

@app.route('/add', methods=['POST'])
def add():
    return "Added!"

if __name__ == '__main__':
    app.run()
```

这个 Python 应用程序通过 `/add` 终端暴露了一个 `add()` 方法。

#### 使用 curl 调用

``` curl
curl http://localhost:3500/v1.0/invoke/cart/method/add -X POST
```

由于 add 端点是一个 'POST' 方法，我们在 curl 命令中使用 `-X POST` 。

调用 'GET' 端点：

``` curl
curl http://localhost:3500/v1.0/invoke/cart/method/add
```

调用 'DELETE' 端点：

``` curl
curl http://localhost:3500/v1.0/invoke/cart/method/add -X DELETE
```

Dapr 在调用的服务 HTTP 应答消息体中放任何负载。

#### 命名空间

当运行在[支持命名空间的平台]上时，你应该把目标应用程序的命名空间包含在应用程序 ID 中：

``` cmd
myApp.production
```

查看[跨命名空间 API 规范]了解更多关于命名空间的信息。

## 概述

---

上面的示例为你展示了如何直接调用不同的服务（运行在本地或者 K8S），Dapr 输出指标和追踪信息允许你可视化服务间的调用图、错误日志和可选地记录有效负载主体。

## 相关主题

- {% post_link service-invocation 服务调用概念 %}
- {% post_link service-invocation-api 服务调用-API-规范 %}
