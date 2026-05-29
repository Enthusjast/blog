---
title: Hello World
date: 2026-02-23 22:28:47
updated: 2026-02-23 22:28:47
tags: 
  - life
categories: life
---

Hello world!

---

临近寒假末尾, 才发现自己还有一个"搭建个人博客"的 flag. 但是我对于这方面一点也不了解, 于是决定在 Qwen 的帮助下完成这件事
(别问我为什么是 Qwen, 问就是我瞎选的)

问过 Qwen 后, 决定使用 Hexo 框架以及 Fluid 主题. 接下来的部分或许算是一份配置教程🤔也可能只是简单地记录一下.

---

## 准备

### 安装必要工具

Hexo 用 JavaScript(Node.js) 编写, 要使用该框架, 首先要在电脑上安装 [Node.js](https://nodejs.org/) 环境以及配置 npm 包管理器(主要是配置使其使用国内镜像源).

博客托管在 GitHub 上, 因此要在电脑上安装 [Git](https://git-scm.com/), 以及 [GitHub](https://github.com) 账户.

安装完成后, 在终端验证:
```bash
node -v
npm -v
git -v
```

博客的配置涉及到对 YAML 配置文件的编辑, 编写博客使用 Markdown 标记语言, 因此使用 [VSCode](https://code.visualstudio.com/) 编辑器.

### 创建 GitHub 仓库

创建名为`用户名.github.io`的 Public repository.

启用"Add README"(可选), 可以在 README 中介绍你的博客.

## 下载 Hexo 并初始化博客

通过命令用 npm 安装 Hexo 并初始化博客目录.

```bash
npm install -g hexo-cli
hexo init my-blog
cd my-blog
npm install
```

完成后, 可以通过以下命令运行并预览你的博客网站.

```bash
hexo clean
hexo generate
hexo server
```

访问 https://localhost:4000 可以看到初始博客.

## 配置 GitHub Pages 部署

通过命令安装以下部署插件:

```bash
npm install hexo-deployer-git --save
```

在博客根目录的 `_config.yml` 文件(以后称为博客配置文件)的末尾添加:

```yaml
deploy:
  type: git
  repo: https://github.com/用户名/用户名.github.io
  branch: main
```

通过以下命令即可将博客部署至 GitHub Pages:

```bash
hexo clean
hexo generate
hexo deploy
```

部署成功后, 访问 https://用户名.github.io/ 即可看到部署的博客.

## 常用 Hexo 命令

| 命令 | 功能 |
| --- | --- |
| `hexo new post 标题` | 创建一篇新文章 |
| `hexo clean` | 清除生成的文件 |
| `hexo generate` | 生成静态文件 |
| `hexo server` | 启动本地服务器预览博客 |
| `hexo deploy` | 部署博客到 GitHub Pages |

## 下载及配置 Fluid 主题

在博客根目录(`my-blog`)下运行以下命令:

```bash
git clone -b master https://github.com/fluid-dev/hexo-theme-fluid.git themes/fluid
```

Fluid 需要一些特定的渲染器支持, 运行以下命令:

```bash
npm install hexo-renderer-pug hexo-renderer-stylus --save
```

完成后, 将博客配置文件中的`theme`字段修改为`fluid`:

```yaml
theme: fluid
```

将文件 `my-blog/themes/fluid/_config.yml` 复制至根目录 `my-blog`, 并重命名为 `_config.fluid.yml`, 今后对主题的配置均在该文件(以后称为主题配置文件)中进行.

有关主题的配置, 参见[Fluid 用户手册](https://hexo.fluid-dev.com/docs/)

Fulid 主题需要一个页面来展示个人信息.

通过以下命令创建页面:

```bash
hexo new page about
```

编辑 `source/about/index.md` 文件, 添加以下内容:
```markdown
---
title: 关于
layout: about
---

这里写个人介绍.
```