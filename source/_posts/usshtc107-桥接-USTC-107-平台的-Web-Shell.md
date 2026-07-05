---
title: 'usshtc107: 桥接 USTC 107 平台的 Web Shell'
date: 2026-07-04 21:52:19
tags: life
categories: life
---

## 前言

USTC 为校内学生提供了 [107 算力平台](https://107.ustc.edu.cn/), 但是很不幸地, 登录该平台只能使用 Web Shell (使用 SSH 登录需要单独申请). 因此, 就有了 usshtc107 (use ssh to connect 107), usshtc107 可以在本地创建一个 ssh server, 并将请求转发至 107 平台.

项目地址: [https://github.com/Enthusjast/usshtc-107](https://github.com/Enthusjast/usshtc-107)

项目仍在开发中, 尚未稳定，欢迎大家进行测试，并反馈问题

## 架构原理

```
本地 SSH 客户端 (ssh / Terminal)
    │ TCP (127.0.0.1:3000)
    ▼
Electron 主进程 (proxy-server.js)
    │ SSH Server (ssh2)  ← 接收本地 SSH 连接
    │     │
    │     ▼ 双向桥接
    │ WebSocket Client
    │     │ JSON 协议 ({ "$case": "data", "data": { "data": "..." } })
    │     ▼
    ▼ 107 算力平台 WSS 终端
```

简单来说, 本软件在本地起一个 SSH 服务器, 把你的 SSH 请求通过 WebSocket 转发到 107 平台的 Web Shell. 对于你的终端来说, 它和连接一台普通的远程服务器没有区别.

## 使用方法

### 下载安装

项目采用 Electron 架构, 支持 Windows, MacOS, Linux 平台. 从 [GitHub Releases](https://github.com/Enthusjast/usshtc-107/releases/) 页面下载对应平台的安装包, 安装.

### 登录账号

首次进入软件, 在 Dashboard 页面点击 Login

![](https://img.enthusjast.cc/20260705121653451.png)

此时会跳转至 107 平台的登录页面, 登录后手动打开 Web Shell 页面, 窗口会读取 Cookie 并自动关闭.

登录成功后, Cookie 会自动保存到本地配置文件. 下次启动软件时, 无需重新登录, 直接自动连接.

### 使用连接

回到 Dashboard 页面, 可以发现软件自动读取了两个 Cookie, 并自动启动了服务.

![](https://img.enthusjast.cc/20260705122419650.png)

复制下方命令, 即可使用 SSH 连接:

```bash
ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -p 3000 user@127.0.0.1
```

也可以直接执行远程命令, 无需进入交互式 shell:

```bash
ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -p 3000 user@127.0.0.1 ls -la
```

### 仪表盘

Dashboard 页面提供实时运行状态:

- **Session 数量** — 当前活跃的 SSH 连接数
- **流量统计** — 已发送/接收的数据量
- **运行时间** — 服务启动至今的时长

所有数据每秒自动刷新.

### 会话管理

Sessions 页面列出所有活跃的 SSH 会话, 包括连接地址、连接时间、流量. 可以手动断开指定会话.

### 日志

Logs 页面显示实时运行日志, 包括 SSH 连接/断开、WebSocket 状态、错误信息等, 方便排查问题.

### 软件设置

软件提供了丰富的设置项:

| 设置 | 说明 |
|------|------|
| 监听端口 | 本地 SSH 服务器端口, 默认 3000 |
| 监听地址 | 默认 127.0.0.1 (仅本机访问) |
| 集群选择 | training / 分组 |
| 登录节点 | 默认 11.11.10.202 |
| 终端尺寸 | cols x rows, 默认 80x24 |
| 自动连接 | 启动后自动使用保存的 Cookie 连接 |
| 启动时最小化 | 开机自启时直接最小化到托盘 |
| SSH Config 别名 | 生成 SSH Config 片段, 一键复制 |
| 主题 | 深色 / 浅色 |
| 语言 | 中文 / English |

### 系统托盘

关闭窗口后, 软件不会退出, 而是最小化到系统托盘. 右键托盘图标可以打开窗口或退出.

## 已知限制

由于远程端是 107 平台的 Web Shell (而非真正的 SSH 服务器), 以下功能**无法使用**:

- **scp / sftp** — 文件传输不可用
- **VS Code Remote SSH** — IDE 远程开发不可用
- **X11 转发** — 图形应用转发不可用
- **端口转发** — TCP 端口映射不可用

这些限制是 Web Shell 协议本身决定的, 不是本软件的问题.

## 常见问题

### Q: Cookie 过期了怎么办?

重新登录即可. 打开软件, 点击 Login, 在弹出的窗口中登录 107 平台并打开 Web Shell. Cookie 会自动更新并保存.

### Q: 连接后终端没有响应?

1. 检查 Dashboard 是否显示 "Connected" 状态
2. 查看 Logs 页面是否有错误信息
3. 确认 Cookie 是否有效 (尝试重新登录)
4. 检查端口是否被占用: `lsof -i :3000`

### Q: 端口被占用怎么办?

在 Settings 页面修改端口, 保存后重启软件生效. 修改端口后, SSH 命令中的 `-p` 参数也要相应修改.

### Q: 重启后需要重新登录吗?

不需要. 登录一次后, Cookie 会保存到本地配置文件. 下次启动时, 软件会自动使用保存的 Cookie 连接. 如果 Cookie 过期, 需要重新登录.
