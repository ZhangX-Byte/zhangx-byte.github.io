---
title: Dapr 概述
catalog: true
toc_nav_num: true
date: 2020-09-11 13:47:55
subtitle: docs/overview
header-img: /img/dapr/dapr.svg
tags: 
- Dapr
- 原文翻译
catagories:
- Dapr
---

## Dapr 概述

---

[Dapr overview](https://github.com/dapr/docs/tree/master/overview)

Dapr 是一个可移植的（portable）、事件驱动（event-driven）的运行时框架。企业开发者使用 Dapr 可以轻松构建弹性、无状态和有状态运行在云上和边缘的微服务。并且拥抱开发语言和开发框架的多样性。

### 任何开发语言、任何开发框架、运行在任何地方

---

我们正处于云应用浪潮中。开发者使用 Web + Database 架构（例如经典3层设计）会比较轻松，但当面对天生具备分布式属性的微服务应用架构来说可能就比较吃力了。要成为一个分布式系统专家是有难度的事情，你也没必要成为一个分布式系统专家。开发者应该专注于业务逻辑，同时依赖各种云平台以使应用程序拥有可伸缩性（scale）、容错性（resiliency）、可维护性（maintainability）、弹性（elasticity） 以及云原生架构的其它属性。

这就是 Dapr 切入点。Dapr 将构建微服务的最佳实践整理为开放、独立的构建块。因此，你可以选择开发语言和框架构建可移植的应用程序。每个构建块都是独立的，你可以在你的应用程序中使用它们中的一个、几个或者所有。

### 云和边缘微服务构建块

---

当架构微服务应用程序时有很多东西需要考虑。而当构建微服务应用程序时 Dapr 提供常用功能的最佳实践。开发者可以按标准在微服务中使用 Dapr 提供的常用功能并且部署到任何环境。Dapr 通过提供分布式系统构建块以支撑这种能力。

这些构建块中每一个块都是独立的，意味着你可以在你的应用程序中使用一个、几个或者全部构建块。在 Dapr 的首次发布中，提供以下构建块：

构建块|描述
--|--
服务调用（Service Invocation）| 容错 service-to-service invocation 使方法调用（包括重试调用）远程服务，无论这些服务位于任何被支持的托管环境。
状态管理（State Management）| 通过状态管理存储键/值对，可以同时在你的应用程序中实现长时间运行、高可用、有状态服务和无状态服务。状态存储是可插拔的并且可以使用 Azure CosmosDB， Azure SQL Server， PostgreSQL， AWS DynamoDB 或者 Redis。
发布和订阅消息（Publish and Subscribe Messaging）| 发布事件和订阅主题。
资源绑定（Resource Bindings）| 带有触发器的资源绑定进一步构建在事件驱动的架构之上，通过从任何外部源(如数据库、队列、文件系统等)接收和发送事件来实现伸缩性和容错性。
Actor 模式（Actors）| 有状态和无状态对象的模式，通过方法和状态封装使并发变得简单。Dapr 在它的 actor 运行时中提供很多能力，包括并发、状态、actor 激活/停用生命周期管理、定时器和唤醒 actor 的提醒。
可观察性（Observability）| Dapr 发出指标、日志和根据以调试和监控 Dapr 和用户应用程序。Dapr支持分布式跟踪，以使用 W3C 跟踪上下文标准和 Open Telemetry 发送到不同的监视工具轻松地诊断和服务生产中的服务间调用。
信息安全（Secrets）| Dapr 提供信息安全管理并且集成到公共云和本地，以供应用程序代码检索使用。

### 边车架构

---

Dapr 通过边车架构以暴露它的 APIs （要么通过程序要么通过一个进程），不需要应用程序代码嵌入任何 Dapr 运行时代码。这使得其它运行时集成 Dapr 变得简单，就像提供隔离的应用程序逻辑以改善可支持性。

### 托管环境

---

Dapr 可以在多个环境上托管，包括为本地开发环境自托管，或者部署到一组虚拟机、K8S和边缘（如Azure IoT edge）。

#### 自托管

自托管模式下，Dapr 作为一个隔离的边车进程运行，你的服务可以通过 HTTP 或者 gRPC 调用。自托管模式下，你也可以把 Dapr 部署到一组虚拟机下。

#### K8S 托管

在容器托管环境比如 K8s，Dapr 以一个边车容器的方式和应用程序容器运行在同一个 pod 中。

### 开发语言 SDKs 和框架

为了使 Dapr 在不同的语言中运用更加自然，Dapr 对 Go、Java、JavaScript、.NET 和 Python 提供特定的 SDK。Dapr 构建块中的功能通过这些 SDKs 暴露，比如：通过一个类型化的语言而不是调用 http/gRPC 接口以保存状态、发布一个事件或者创建一个 actor。这使你能够使用自己选择的语言编写无状态和有状态函数以及 actor 的组合。并且由于这些 SDKs 共享 Dapr 运行时，你可以获得跨语言的 actor 和函数支持。

#### SDKs

- C++ SDK
- Go SDK
- Java SDK
- JavaScript SDK
- Python SDK
- .NET SDK

> 注意： Dapr 是语言无关的提供 REST HTTTP API 除了 protobuf 客户端外。

#### 开发框架

Dapr 可以用于任何开发框架。这里有一些已经集成到 Dapr 的。

##### Web

在 Dapr .NET SDK 中集成了 `ASP.NET Core`，`ASP.NET Core` 带来了状态路由控制器，该控制器响应来自其他服务的发布/订阅事件。

在 Dapr Java SDK 你可以找到 Spring Boot 集成。

Dapr 很容易与 Python Flask 和 node Express 集成，您可以在入门示例中找到它们。

##### Actors

Dapr SKDs 支持虚拟 actors ，虚拟 actors 是使并发简单的有状态对象，具有方法和状态封装，并且是为可扩展的分布式应用程序设计的。

##### Azure Functions

Dapr 通过扩展与 Azure 函数运行时集成，扩展允许函数与 Dapr 无缝交互。Azual 函数提供一个事件驱动编程模式并且 Dapr 提供云原生构建块。通过这个扩展，你可以同时提供 serverless 和事件驱动应用。更多信息请阅读[用于 Dapr 的Azure 函数扩展](https://cloudblogs.microsoft.com/opensource/2020/07/01/announcing-azure-functions-extension-for-dapr/) 和访问[Azure 函数扩展](https://github.com/dapr/azure-functions-extension)以试用示例。

##### Dapr 工作流

为了使开发人员能够轻松构建使用 Dapr 功能（包括诊断和多语言支持）的工作流应用程序，可以使用Dapr工作流。Dapr 集成了工作流引擎比如 Logic Apps，更多信息阅读[使用 Dapr 和 Logic Apps 的云原生工作流](https://cloudblogs.microsoft.com/opensource/2020/05/26/announcing-cloud-native-workflows-dapr-logic-apps/)和访问[Dapr 工作流](https://github.com/dapr/workflows)试用示例。

### 为运维而设计

---

Dapr 是为运维而设计的。[Dapr 仪表板](https://github.com/dapr/dashboard)（通过 Dapr CLI 安装），提供一个以网页为基础的 UI 使你能看信息、看日志和 Dapr 边车更多的信息。

监视仪表板提供了对 Dapr 系统服务和边车的更深层次的可见性，而 Dapr 的可观察性功能提供了对应用程序的深入了解，如跟踪和指标。

### 运行与任何地方

---

#### 本地开发机器以自托管模式运行 Dapr

Dapr 可以配置为自托管模式以运行在你本地机器上。每一个运行的服务有一个 Dapr 运行时进程（或者边车），这个进程（或边车）通过配置以使用状态存储、发布/订阅、绑定组件和其它构建块。

你可以使用 Dapr CLI 在你本地机器上运行 Dapr 启用应用程序。通过入门示例试用。

#### 以 K8S 模式运行 Dapr 

Dapr 可以配置以运行在任何 K8S 集群上。在 K8S 上 `dapr-sidecar-injector` 和 `dapr-operator` 服务提供了一流的集成，以将 Dapr 作为 sidecar 容器启动与服务容器在同一 pod 中，并提供了已配置到集群中的 Dapr 组件更新的通知。

`dapr-sentry` 服务是一个证书颁发机构，可启用 Dapr 边车实例之间的相互 TLS 进行安全数据加密。有关Sentry服务的更多信息，请阅读[安全概述](https://github.com/dapr/docs/blob/master/concepts/security/README.md#dapr-to-dapr-communication)。

在 Kubernetes 集群中部署并运行启用了 Dapr 的应用程序非常简单，只需在部署方案中添加一些注释即可。您可以在Kubernetes入门示例中看到一些示例。使用 Kubernetes [入门示例](https://github.com/dapr/quickstarts/tree/master/hello-kubernetes)进行尝试。

---

## 参考

- [1] [Implement resilient applications](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/implement-resilient-applications/)

    > Resiliency is the ability to recover from failures and continue to function. It isn't about avoiding failures but accepting the fact that failures will happen and responding to them in a way that avoids downtime or data loss. The goal of resiliency is to return the application to a fully functioning state after a failure.
    > 翻译：Resiliency 是一种从故障中恢复并且继续工作的能力。并不是避开故障而是接受可能会故障的事实并且以某种方式回应它们以避免停机或者数据丢失。Resiliency 的目标是在发生故障后将应用程序返回到完全正常的状态。
