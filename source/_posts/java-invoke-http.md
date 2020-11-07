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

- Java 版本：8
- Dapr Java SKD 版本：0.9.2

Dapr Java-SDK [HTTP 调用文档](https://github.com/dapr/java-sdk/tree/master/examples/src/main/java/io/dapr/examples/invoke/http) 有个先决条件，内容如下：

- Dapr and Dapr CLI.
- Java JDK 11 (or greater): Oracle JDK or OpenJDK.
- Apache Maven version 3.x.

大家看到 Java JDK 版本最低要求是 11，但是本文显示使用的 JDK 8，这么做的原因是什么呢，可以[参考](https://github.com/dapr/java-sdk/issues/279) Java-SDK Issues，Issues 中回答如下：

>We want to validate that the SDK is built with Java 8 and apps can use it with Java 11.

意思是他们想通过 Java 11 写的应用程序验证 Java 8 写的 SDK 是否能正常使用。本文不需要验证 Java 11 能否使用 Java-SDK ，因此本文将使用 Java 8 构建应用程序。

## 工程结构

dapr run --app-id java-service-b --app-port 3000 --dapr-http-port 3005 -- java -jar target/dapr-java-service-exec.jar com.dapr.service.ServiceB -p 3000


## client-a

dapr run  --dapr-http-port 3006 -- java -jar target/dapr-java-client-exec.jar io.dapr.examples.invoke.http.InvokeClient "message one" "message two"

