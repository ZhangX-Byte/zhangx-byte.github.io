---
title: 设置 Azure K8S 服务集群
catalog: true
toc_nav_num: true
date: 2020-09-29 20:54:50
subtitle: docs/getting-started/cluster/setup-aks.md
header-img: /img/dapr/dapr.svg
tags: 
- Dapr
- 原文翻译
catagories:
- Dapr
---

## 设置 Azure K8S 服务集群

---

### 前置条件

---

- [Docker](https://docs.docker.com/get-docker/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)

### 部署 Azure K8S 服务集群

---

这个指南向你介绍安装 Azure K8S 服务集群。如果你需要了解更多信息，参考[快速开始：使用 Azure CLI 部署 Azure K8S 服务（AKS）集群](https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough)

1. 登录 Azure

``` cmd
az login
```

2. 设置默认订阅

``` cmd
az account set -s [your_subscription_id]
```

3. 创建资源组

``` cmd
az group create --name [your_resource_group] --location [region]
```

4. 创建一个 Azure K8S 服务集群

K8S 通过 `--kubernetes-version` 使用 1.13.x 或者更新的版本

``` cmd
az aks create --resource-group [your_resource_group] --name [your_aks_cluster_name] --node-count 2 --kubernetes-version 1.14.7 --enable-addons http_application_routing --enable-rbac --generate-ssh-keys
```

5. 从 Azure K8S 集群中获取访问凭证

``` cmd
az aks get-credentials -n [your_aks_cluster_name] -g [your_resource_group]
```

### （可选）安装 Helm v3

---

1. [安装 Helm v3 客户端](https://helm.sh/docs/intro/install/)

> 注意： 最新的 Dapr helm 图表不在支持 Helm v2。请从 heml v2 迁移至 heml v3，[迁移指南](https://helm.sh/blog/migrate-from-helm-v2-to-helm-v3/)

2. 如果你需要 K8S 仪表盘权限执行此命令

``` cmd
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```