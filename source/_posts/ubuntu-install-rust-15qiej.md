---
title: Ubuntu 系统上安装 Rust 编程语言及设置国内镜像指南
date: '2025-01-07 20:43:13'
updated: '2025-01-07 20:47:22'
excerpt: >-
  本文介绍了在 Ubuntu 系统上安装 Rust 的步骤。首先，需要设置 Rust 的镜像源，以便于更快下载所需文件。通过配置环境变量
  `RUSTUP_DIST_SERVER` 和 `RUSTUP_UPDATE_ROOT`，将下载地址指向国内的代理服务器。接着，通过运行一个 cURL
  命令来执行 Rust 的安装脚本。最后，文章还提供了可选步骤，指导用户如何配置 crates.io 的镜像，这样可以在使用 Rust
  包管理时更加高效，确保依赖库和索引的快速访问。
tags:
  - 配置记录
  - rust
categories:
  - Ubuntu
  - Rust
permalink: /post/ubuntu-install-rust-15qiej.html
comments: true
toc: true
---

![image](https://raw.githubusercontent.com/eeymoo/Eeymoo.github.io/main/images/unsplash-ntcf0lU5d38-20250107204339-m79x2af.jpg)

# Ubuntu 安装 Rust

## 1. 设置镜像

```bash
export RUSTUP\_DIST\_SERVER\="https://rsproxy.cn"
export RUSTUP\_UPDATE\_ROOT\="https://rsproxy.cn/rustup"
```

## 2. 安装 Rust

```bash
curl --proto '\=https' --tlsv1.2 -sSf https://rsproxy.cn/rustup-init.sh | sh
```

## 3. 设置 crates.io 镜像 (可选)

```toml
# ~/.cargo/config.toml Unix
# %USERPROFILE%\.cargo\config.toml window
[source.crates-io]
replace-with = 'rsproxy-sparse'
[source.rsproxy]
registry = "https://rsproxy.cn/crates.io-index"
[source.rsproxy-sparse]
registry = "sparse+https://rsproxy.cn/index/"
[registries.rsproxy]
index = "https://rsproxy.cn/crates.io-index"
[net]
git-fetch-with-cli = true
```
