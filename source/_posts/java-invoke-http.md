---
title: Dapr Java HTTP 调用
catalog: true
toc_nav_num: true
date: 2020-11-04 09:37:41
subtitle: java_invoke_http
header-img: /img/java/java.jpeg
tags: 
- Dapr
- Java
catagories:
- Java
---

## 版本介绍

- Java 版本：1.8
- Dapr Java SKD 版本：0.9.2

## 服务介绍

新建 3 个 Java 服务，分别为 ServiceA 作为 client 调用 ServiceB, ServiceB 调用 ServiceC。

```mermaid
graph LR;
    ServiceA-->ServiceB;
    ServiceB-->ServiceC;
    ServiceC-->ServiceB;
    ServiceB-->ServiceA;
```
