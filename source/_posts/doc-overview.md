---
title: Dapr 概述
catalog: true
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

[官方文档地址](https://github.com/dapr/docs/tree/master/overview)

Dapr 是一个可移植的（portable）、事件驱动（event-driven）的运行时框架。企业开发者使用 Dapr 可以轻松构建弹性、无状态和有状态运行在云上和边缘的微服务。并且拥抱开发语言和开发框架的多样性。

### 任何开发语言、任何开发框架、运行在任何地方

我们正处于云应用浪潮中。开发者使用 Web + Database 架构（例如经典3层设计）会比较轻松，但当面对天生具备分布式属性的微服务应用架构来说可能就比较吃力了。要成为一个分布式系统专家是有难度的事情，你也没必要成为一个分布式系统专家。开发者应该专注于业务逻辑，同时依赖各种云平台以使应用程序拥有可伸缩性（scale）、容错性（resiliency）、可维护性（maintainability）、弹性（elasticity） 以及云原生架构的其它属性。

这就是 Dapr 切入点。Dapr 将构建微服务的最佳实践整理为开放、独立的构建块。因此，你可以选择开发语言和框架构建可移植的应用程序。每个构建块都是独立的，你可以在你的应用程序中使用它们中的一个、几个或者所有。

### 云和边缘微服务构建块

当架构微服务应用程序时有很多东西需要考虑。而当构建微服务应用程序时 Dapr 提供常用功能的最佳实践。开发者可以按标准在微服务中使用 Dapr 提供的常用功能并且部署到任何环境。Dapr 通过提供分布式系统构建块以支撑这种能力。

这些构建块中每一个块都是独立的，意味着你可以在你的应用程序中使用一个、几个或者全部构建块。在 Dapr 的首次发布中，提供以下构建块：

构建块|描述
--|--
服务调用（Service Invocation）|

> 引用：
> Resiliency is the ability to recover from failures and continue to function. It isn't about avoiding failures but accepting the fact that failures will happen and responding to them in a way that avoids downtime or data loss. The goal of resiliency is to return the application to a fully functioning state after a failure.
> Resiliency 是一种从失败中恢复并且继续的能力。