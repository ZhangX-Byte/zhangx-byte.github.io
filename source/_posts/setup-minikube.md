---
title: 设置 Minikube 集群
catalog: true
toc_nav_num: true
date: 2020-09-27 21:47:14
subtitle: docs/getting-started/cluster/setup-minikube.md
header-img: /img/dapr/dapr.svg
tags: 
- Dapr
- 原文翻译
catagories:
- Dapr
---

## 设置 Minikube 集群

---

### 前置条件

---

- Docker
- kubectl
- Minikube

> 注意：对于 Windows ，在 BIOS 中启用 Virtualization 并且安装 [Hyper-V](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)

### 开始 Minikube 集群

1. （可选）设置默认 VM 驱动

``` cmd
minikube config set vm-driver [driver_name]
```

2. 通过 `--kubernetes-version` 指定 K8S 版本（使用 1.13.x 或者更新的版本）开始集群。

``` cmd
minikube start --cpus=4 --memory=4096 --kubernetes-version=1.16.2 --extra-config=apiserver.authorization-mode=RBAC
```

3. 启用仪表盘和入口插件

``` cmd
# Enable dashboard
minikube addons enable dashboard

# Enable ingress
minikube addons enable ingress
```

### (可选)安装 Helm v3

---

1. [安装 Helm v3 客户端](https://helm.sh/docs/intro/install/)

> 注意： 最新的 Dapr helm 图表不在支持 Helm v2。请从 heml v2 迁移至 heml v3，[迁移指南](https://helm.sh/blog/migrate-from-helm-v2-to-helm-v3/)

#### 疑难解答

1. 负载均衡器的外部 IP 地址不从 `kubectl get svc` 中显示

在 Minikube 中，你的服务 EXTERNAL-IP 在 `kubectl get svc` 中显示 `<pending>` 状态。在这种情况下，你可以运行 `minikube service [service_name]` 以打开你的服务并且不显示外部 IP 地址。

``` cmd
$ kubectl get svc
NAME                        TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)            AGE
...
calculator-front-end        LoadBalancer   10.103.98.37     <pending>     80:30534/TCP       25h
calculator-front-end-dapr   ClusterIP      10.107.128.226   <none>        80/TCP,50001/TCP   25h
...

$ minikube service calculator-front-end
|-----------|----------------------|-------------|---------------------------|
| NAMESPACE |         NAME         | TARGET PORT |            URL            |
|-----------|----------------------|-------------|---------------------------|
| default   | calculator-front-end |             | http://192.168.64.7:30534 |
|-----------|----------------------|-------------|---------------------------|
🎉  Opening kubernetes service  default/calculator-front-end in default browser...
```
