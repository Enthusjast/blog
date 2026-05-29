---
title: 使用 PicGo 与 GitHub 配置图床
date: 2026-04-11 19:58:09
updated: 2026-04-11 19:58:09
tags:
    - life
categories: life
excerpt: 使用 PicGo + GitHub Pages 搭建免费图床的完整教程，含自定义域名配置。
---

## Github

### 创建仓库

在 GitHub 上创建一个 Public Repository, 命名为 "my-pics" (其实随意命名)

### 创建 Token

进入设置页, 在边栏底部找到 "Developer Settings", 进入这一项.

![](https://img.enthusjast.cc/20260411203532995.png)

进入后在边栏中展开 "Personal access tokens", 选择 "Tokens (classic)".
右侧点击 "Generate new token", 在下拉菜单中选择 "Generate new token (classic)".

![](https://img.enthusjast.cc/20260411204737979.png)

在 Note 中填入该 Token 的名称(例如 PicGo-Token, 随意填写); Expiration 选择 No expiration (不过期);
下方列表中勾选 repo; 最后在页面底部点击 Generate token.

![](https://img.enthusjast.cc/20260411205142408.png)

复制出现的 Token, 并将其保存至一个安全的地方, 该 Token 只会出现一次.

![](https://img.enthusjast.cc/20260311205153758.png)

### 发布 GitHub Pages

转至仓库页面, 进入仓库设置. 在边栏中转至 "Pages", 右侧 "Source" 下选择 "Deploy from a branch", "Branch" 下分别选择 "main", "/(root)".

![](https://img.enthusjast.cc/20260412215519551.png)

这样, 可以通过访问 `https://username.github.io/my-pics` 来访问你的 图床. 例如, 若你有一张图片名为 `img.png`, 则链接 `https://username.github.io/my-pics/img.png` 可以访问到该图片.

## PicGo

### PicGo 软件的配置

前往 [PicGo 的 GitHub Releases 页面](https://github.com/Molunerfinn/PicGo/releases) 下载 PicGo.

边栏选择图床设置下的 GitHub, 添加配置. 配置中需要填写如下配置项

- **图床配置名**: 这项随意填写, 例如 "GitHub".
- **设定仓库名**: 填写你在 GitHub 上创建的仓库名, 例如 "username/my-pics".
- **设定分支名**: 一般为 "main".
- **设定 Token**: 填写你在 GitHub 上创建的 Personal Access Token.
- **设定存储路径**: 非必填, 留空则默认将图片存储至仓库根目录.
- **设定自定义域名**: 非必填, 若你有自己的域名, 我们后面的章节介绍相关配置.

接下来在边栏选择进入上传区, 在这里你可以上传图片至你的图床.
在边栏选择进入相册, 可以看到你上传至图床的全部图片, 也可以复制相关图片的图床链接.

### 自定义域名

如果你有一个自己的域名(例如 `yourdomain.com`), 那么你可以考虑通过自定义域名访问图床.

进入你的图床仓库 "username/my-pics", 在顶栏转到 "Settings", 下面的侧边栏中转到 "Pages". 在大页面中的 "source" 下选择 "Deploy from a branch", "Branch" 下分别选择 "main", "/(root)".

![](https://img.enthusjast.cc/20260418210445717.png)

点击 "Save" 后, 在下面 "Custom domain" 中填入你的自定义域名, 例如 `img.yourdomain.com`.

![](https://img.enthusjast.cc/20260418210645206.png)

接下来配置 DNS, 例如使用 Cloudflare, 添加一条 CNAME 记录, 名称为 `img`, 目标为 `username.github.io`.

![](https://img.enthusjast.cc/20260418211143581.png)

回到 PicGo 中, 在"设定自定义域名"中填入 `img.yourdomain.com` 即可.
