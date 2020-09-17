---
title: 入门
catalog: true
toc_nav_num: true
date: 2020-09-17 15:05:58
subtitle: docs/getting-started
header-img: /img/dapr/dapr.svg
tags: 
- Dapr
- 原文翻译
catagories:
- Dapr
---

## 入门

---

apr（Distributed Application Runtime） 是一个可移植的（portable）、事件驱动（event-driven）的运行时框架。开发者通过 Dapr 可以构建弹性、无状态、有状态的运行在云上和边缘的微服务。并且拥抱开发语言和开发框架的多样性。

### 核心概念

---

- **构建块**是一个实现分布式系统能力的组件集，比如：pub/sub，状态管理、资源绑定和分布式追踪。
- **组建**是构建块 API 的封装实现。例如状态构建块实现可能包含 Redis、Azure Storage、Azure Cosmos DB 和 AWS DynamoDB。很多组件都是可插拔的，所以一个实现可以替换为另一个。

查看 Dapr 概念 了解更多信息。

### 设置开发环境

---

Dapr 可以在本地或者 K8S 上运行。我们推荐从本地设置开始探索 Dapr 核心概念并且熟悉 Dapr CLI。跟随这些指令配置本地和 K8S Dapr。

## 下一步

---

1. 安装完 Dapr 后，查看[Hello World 开素开始]以继续。
2. 探索其它[快速开始]了解更多高级概念，比如：服务调用、发布/订阅、状态管理。
3. 跟随[如何引导]了解 Dapr 如何解决指定问题，比如创建一个[限速应用]。
