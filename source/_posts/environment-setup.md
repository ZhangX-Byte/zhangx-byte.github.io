---
title: 环境设置
catalog: true
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
