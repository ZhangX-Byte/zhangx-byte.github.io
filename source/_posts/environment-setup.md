---
title: 环境设置
catalog: true
toc_nav_num: true
date: 2020-09-19 16:27:14
subtitle: docs/getting-started/environment-setup
header-img: /img/dapr/dapr.svg
tags: 
- Dapr
- 原文翻译
catagories:
- Dapr
---

## 环境设置

---

Dapr 既可以使用自托管模式运行也可以运行在 K8S 模式下。通过自托管模式运行 Dapr 运行时使你可以在本地开发环境开发 Dapr 应用程序，然后部署到其它支持 Dapr 运行的环境。例如：你可以在自托管模式下开发 Dapr 应用程序然后把应用程序部署到任何 K8S 集群。

### 内容

---

- [环境设置](#环境设置)
  - [内容](#内容)
  - [先决条件](#先决条件)
  - [安装 Dapr 命令行](#安装-dapr-命令行)
    - [Windows](#windows)
    - [Linux](#linux)
    - [MacOS](#macos)
    - [通过二进制版本](#通过二进制版本)
  - [自托管模式安装 Dapr](#自托管模式安装-dapr)
    - [使用命令行界面初始化 Dapr](#使用命令行界面初始化-dapr)
    - [安装指定运行时版本](#安装指定运行时版本)
    - [自托管模式卸载 Dapr](#自托管模式卸载-dapr)
  - [在 K8S 集群下安装 Dapr](#在-k8s-集群下安装-dapr)
    - [设置集群](#设置集群)
    - [使用 Dapr 命令行界面](#使用-dapr-命令行界面)
      - [安装 Dapr 到 K8S](#安装-dapr-到-k8s)
    - [使用 Helm （高级）](#使用-helm-高级)
      - [在 K8S 中安装 Dapr](#在-k8s-中安装-dapr)
      - [验证安装](#验证安装)
      - [边车注释](#边车注释)
      - [从 K8S 中卸载 Dapr](#从-k8s-中卸载-dapr)

### 先决条件

---

默认情况下，Dapr 使用 Docker 容器安装开发环境以便你轻松上手。然而，Dapr 不依赖 Docker 运行（查看【这里】介绍使用 Docker 轻量化初始本地安装 Dapr）。这个入门指南假设 Dapr 是和开发人员环境一起安装的。

- 安装 [Docker](https://docs.docker.com/get-docker/)

> Windows 用户，确保 `Docker Desktop For Windows` 使用 Linux 容器。

### 安装 Dapr 命令行

---

使用脚本安装最新版本

#### Windows

安装最新的 windows Dapr 命令行界面到  `c:\dapr` 并添加这个文件夹到 User Path 环境变量中。

``` powershell
powershell -Command "iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1 | iex"
```

#### Linux

安装最新的 linux Dapr 命令行界面到 `/usr/local/bin`

``` bash
wget -q https://raw.githubusercontent.com/dapr/cli/master/install/install.sh -O - | /bin/bash
```

#### MacOS

安装最新的 darwin Dapr 命令行界面到 `/usr/local/bin`

``` bash
curl -fsSL https://raw.githubusercontent.com/dapr/cli/master/install/install.sh | /bin/bash
```

或者使用 Homebrew 安装

``` bash
brew install dapr/tap/dapr-cli
```

#### 通过二进制版本

Dapr 命令行界面每个发布版本都包含各种系统和架构。这些二进制版本可以手动下载和安装。

1. 下载[Dapr 命令行界面](https://github.com/dapr/cli/releases)
2. 解压（例如：dapr_linux_amd64.tar.gz, dapr_windows_amd64.zip）
3. 把解压后文件移动到你希望的位置。
   - Linux/MacOS - /usr/local/bin
   - Windows，创建一个文件夹并添加文件夹路径到系统路径中。例如：创建一个文件夹 `c:\dapr` 并把文件夹路径加入到系统环境变量中。

### 自托管模式安装 Dapr

---

#### 使用命令行界面初始化 Dapr

默认情况下，初始化 Dapr 命令行界面过程中会安装 Dapr 二进制文件，同时设置一个开发者环境以帮助你轻松上手 Dapr。这个环境使用 Docker 容器，因此 Docker 列入到先决条件中。

>如果你不想使用这个环境并且不依赖 Docker 运行 Dapr，查看命令行界面[文档](https://github.com/dapr/cli/blob/master/README.md)，当使用 init 命令时同时使用 `--slim` 命令。注意，如果你时一个新手，强烈推荐安装 Docker 并且使用常规初始化（init）命令。
>对于 Linux 用户，如果你运行 docker 命令使用 sudo 或者安装路径时 `/usr/local/bin` （默认安装路径），你需要使用“sudo dapr init”。对于 Windows 用户，确保你使用管理员模式运行命令行终端。注意：查看[Dapr 命令行界面]以了解使用 Dapr 命令行界面的细节。

``` cmd
$ dapr init
⌛  Making the jump to hyperspace...
Downloading binaries and setting up components
✅  Success! Dapr is up and running. To get started, go here: https://aka.ms/dapr-getting-started
```

查看 Dapr 安装成功，从命令提示符中运行 `docker ps` 命令并检查 `daprio/dapr:latest` 和 `redis` 容器镜像同时在运行。

#### 安装指定运行时版本

你可以安装或升级到指定版本的 Dapr 运行时，通过使用 `dapr init --runtime-version` 。在 [Dapr 发布版本](https://github.com/dapr/dapr/releases)列表中查找。

``` cmd
# Install v0.1.0 runtime
$ dapr init --runtime-version 0.1.0

# Check the versions of cli and runtime
$ dapr --version
cli version: v0.1.0
runtime version: v0.1.0
```

#### 自托管模式卸载 Dapr

卸载将移除放置服务的容器或放置服务的二进制文件。

``` cmd
$dapr uninstall
```

>对于 Linux 用户，如果你运行你的 docker 命令通过 sudo 或者安装路径为 `/usr/local/bin`（默认路径），你需要使用 `sudo dapr uninstall` 移除 dapr 二进制文件或者容器。

默认它不会移除 Redis 或者 Zipkin 容器以防你对它们有其它用途。要移除 Redis、Zipkin 和 actor 部署容器和移除位于 `$HOME/.dapr` 或者 `%USERPROFILE%\.dapr\` 的默认 Dapr 目录， ，运行：

``` cmd
$dapr uninstall --all
```

你应该总在运行 `dapr init` 之前运行 `dapr uninstall` 。

### 在 K8S 集群下安装 Dapr

---

当设置 K8S 时，你可以通过 Dapr 命令行界面或者 Helm 。

Dapr 安装以下 pods：

- dapr-operator：管理组件更新和 Dapr K8S 服务终端（状态存储、发布-订阅、等等）
- dapr-sidecar-injector：注入 Dapr 到已注释的部署 pods 中
- dapr-placement：仅用于 actors ，创建映射表以映射 actor 实例到 pods 中
- dapr-sentry：管理服务之间的 mTLS 并充当证书颁发机构

#### 设置集群

你可以在任何 K8S 集群安装 Dapr 。以下是一些有用的链接：

- {% post_link setup-minikube Setup Minikube Cluster %}
- [Setup Azure Kubernetes Service Cluster](https://github.com/dapr/docs/blob/master/getting-started/cluster/setup-aks.md)
- [Setup Google Cloud Kubernetes Engine](https://cloud.google.com/kubernetes-engine/docs/quickstart)
- [Setup Amazon Elastic Kubernetes Service](https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html)

> 注意：Dapr 命令行界面和 Dapr Helm 图表都会自动部署具有 `kubernetes.io/os=linux` 标签关联的节点。你可以部署 Dapr 到 Windows 节点，但大多数用户应该不需要。更多信息查看 [Deploying to a Hybrid Linux/Windows K8s Cluster](https://github.com/dapr/docs/tree/master/howto/windows-k8s)

#### 使用 Dapr 命令行界面

你可以使用命令行界面安装 Dapr 到 K8S 集群。

##### 安装 Dapr 到 K8S

>注意：默认命名空间是 dapr-system

``` cmd
$ dapr init -k

⌛  Making the jump to hyperspace...
ℹ️  Note: To install Dapr using Helm, see here:  https://github.com/dapr/docs/blob/master/getting-started/environment-setup.md#using-helm-advanced

✅  Deploying the Dapr control plane to your cluster...
✅  Success! Dapr has been installed to namespace dapr-system. To verify, run "dapr status -k" in your terminal. To get started, go here: https://aka.ms/dapr-getting-started
```

安装到自定义命名空间：

``` cmd
dapr init -k -n mynamespace
```

高可用模式安装：

``` cmd
dapr init -k --enable-ha=true
```

禁用 mTLS：

``` cmd
dapr init -k --enable-mtls=false
```

从 K8S 中卸载 Dapr

``` cmd
$dapr uninstall --kubernetes
```

#### 使用 Helm （高级）

你可以使用 Helm 3 图表安装 K8S 集群。

>注意：最新的 Darp helm 图表不在支持 Helm v2。请跟随[指南](https://helm.sh/blog/migrate-from-helm-v2-to-helm-v3/)迁移 helm v2 到 helm v3。

##### 在 K8S 中安装 Dapr

1. 确认 Helm 3 已经安装到你的机器上
2. 添加 Azure 容器注册表做为 Helm 仓库

  ``` cmd
  helm repo add dapr https://dapr.github.io/helm-charts/
  helm repo update
  ```

3. 在你的 K8S 集群中创建 `dapr-system` 命名空间

  ``` cmd
  kubectl create namespace dapr-system
  ```

4. 在你的集群 `dapr-system` 命名空间中安装 Dapr 图表。

``` cmd
helm install dapr dapr/dapr --namespace dapr-system
```

##### 验证安装

一旦图表完成安装，验证 dapr-operator, dapr-placement, dapr-sidecar-injector 和 dapr-sentry pods 在 `dapr-system` 命名空间中运行。

``` cmd
$ kubectl get pods -n dapr-system -w

NAME                                     READY     STATUS    RESTARTS   AGE
dapr-operator-7bd6cbf5bf-xglsr           1/1       Running   0          40s
dapr-placement-7f8f76778f-6vhl2          1/1       Running   0          40s
dapr-sidecar-injector-8555576b6f-29cqm   1/1       Running   0          40s
dapr-sentry-9435776c7f-8f7yd             1/1       Running   0          40s
```

##### 边车注释

要查看在 K8S 中所有 Dapr 边车支持的注释，访问[这里](https://github.com/dapr/docs/blob/master/howto/configure-k8s/README.md)查看。

##### 从 K8S 中卸载 Dapr

Helm3

``` cmd
helm uninstall dapr -n dapr-system
```

> 注意：点击[这里](https://github.com/dapr/dapr/blob/master/charts/dapr/README.md)查看 Dapr helm 图表细节。