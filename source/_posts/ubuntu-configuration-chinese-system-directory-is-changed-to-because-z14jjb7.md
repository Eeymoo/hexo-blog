---
title: Ubuntu 系统切换中文目录配置指南
date: '2025-01-07 13:48:30'
updated: '2025-01-07 14:56:45'
excerpt: >-
  本文介绍了如何在Ubuntu系统中将中文系统目录修改为英文目录。主要步骤包括切换系统语言到英文、启动配置界面以更新目录设置、手动修改用户目录配置文件，以及在必要时转移现有的目录和内容。最后，重启系统完成更改，确保目录名称已成功转换为英文。
tags:
  - Ubuntu
  - 系统配置
categories:
  - Ubuntu
permalink: >-
  /post/ubuntu-configuration-chinese-system-directory-is-changed-to-because-z14jjb7.html
comments: true
toc: true
---

![image](https://raw.githubusercontent.com/eeymoo/Eeymoo.github.io/main/images/unsplash-3TBqWrOygfI-20250107135139-w6nbniv.jpg)

# Ubuntu 配置中文系统目录改为因为

## 切换系统语言

```bash
export LANG=en_US
```

## 启动配置页面

```bash
xdg-user-dirs-gtk-update
# 弹出提示框 勾选不再提示 后点击更新
```

## 修改系统配置

```bash
sudo vim ~/.config/user-dirs.dirs  
```

```bash
XDG_DESKTOP_DIR="$HOME/Desktop"
XDG_DOWNLOAD_DIR="$HOME/Downloads"
XDG_TEMPLATES_DIR="$HOME/Templates"
XDG_PUBLICSHARE_DIR="$HOME/Public"
XDG_DOCUMENTS_DIR="$HOME/Documents"
XDG_MUSIC_DIR="$HOME/Music"
XDG_PICTURES_DIR="$HOME/Pictures"
XDG_VIDEOS_DIR="$HOME/Videos"
```

## 转移目录

如果系统没有转移你的目录，你就需要手动转移目录以及内容，然后重新启动就可以了。

‍
