---
title: Lean 的安装与配置
date: 2026-04-11 18:27:38
updated: 2026-04-11 18:27:38
tags: 
    - Lean
categories: Lean
published: false
---

笔者发现 Lean 社区的[安装指南](https://leanprover.cn/install)有若干问题, 接下来给出来我的安装与配置过程.

## 安装 elan

如果网络没有问题, 用一行命令安装:

```bash
wget -q https://raw.githubusercontent.com/leanprover-community/mathlib4/master/scripts/install_debian.sh && bash install_debian.sh ; rm -f install_debian.sh && source ~/.profile
```

脚本内容包括: 检查并安装 VSCode, Lean 插件, 并安装 elan.

完成后, 在 `~/.bashrc` 中修改环境变量:

```bash
export PATH="$HOME/.elan/bin:$PATH"
```

## 检查安装

在终端输入以下命令检查 `elan` 版本和默认安装的 `Lean` 版本:

```bash
elan --version
```

输出应当形如:

```text
elan 4.2.1 (3d5138e15 2026-03-18)
```

输入以下命令检查默认安装的 Lean 版本:

```bash
lean --version
```

输出应当形如:

```text
Lean (version 4.30.0-rc1, x86_64-unknown-linux-gnu, commit 714601baf118066cbf3f282361339c6d06665b2a, Release)
```

有关 `elan` 的用法, 可查阅其官方文档.

## 创建 Lean 项目

在终端中运行:

```bash
lake new your_project_name # 将 you_project_name 替换为项目名称

# 或者创建一个新文件夹并在此处建立项目
mkdir your_project_name
cd your_project_name
lake init your_project_name
```

项目的结构形如:

```
your_project_name
├── YourProjectName
│   └── Basic.lean
├── lakefile.toml
├── lean-toolchain
├── Main.lean
├── YourProjectName.lean
└── ...
```

欲在该项目中使用 Mathlib, 需向 `lakefile.toml` 中添加如下内容:

```toml
[[require]]
name = "mathlib"
git = "https://github.com/leanprover-community/mathlib4"
rev = "master"
```

这里 `master` 代表使用 Mathlib 的版本, 也可以是 `v4.20.0` 等(如果你想手动指定版本).

接下来下载 Mathlib, 如果你的网络环境好, 在终端运行以下命令:

```bash
curl -L https://raw.githubusercontent.com/leanprover-community/mathlib4/master/lean-toolchain -o lean-toolchain
```

接下来你将会看到下载进度, 形如:

```text
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100    29  100    29    0     0     20      0  0:00:01  0:00:01 --:--:--    20
```

随后执行命令:

```bash
lake update
```

该命令有一大堆输出, 形如:

{% fold info @安装页面 %}

```text
info: your_project_name: no previous manifest, creating one from scratch
info: mathlib: cloning https://github.com/leanprover-community/mathlib4
info: mathlib: checking out revision 'ab4925322b50d479724a6632ee0d7a5653728e99'
info: toolchain not updated; already up-to-date
info: plausible: cloning https://github.com/leanprover-community/plausible
info: plausible: checking out revision 'a3b459a8312125758e51c354b93d54ba620efda6'
info: LeanSearchClient: cloning https://github.com/leanprover-community/LeanSearchClient
info: LeanSearchClient: checking out revision 'c5d5b8fe6e5158def25cd28eb94e4141ad97c843'
info: importGraph: cloning https://github.com/leanprover-community/import-graph
info: importGraph: checking out revision '4411c5f89c797401c609b3a946c8874569e69731'
info: proofwidgets: cloning https://github.com/leanprover-community/ProofWidgets4
info: proofwidgets: checking out revision '82d457fb3bdd9efadbae06608ff337d689efdddf'
info: aesop: cloning https://github.com/leanprover-community/aesop
info: aesop: checking out revision 'f74c7555aaa94eadd7b7bff9170f7983f92aac21'
info: Qq: cloning https://github.com/leanprover-community/quote4
info: Qq: checking out revision '7aa86cb20b8458748dc24d55dab2d7ea01161057'
info: batteries: cloning https://github.com/leanprover-community/batteries
info: batteries: checking out revision 'bf597c77bf9b8e66720d724928207f5911533113'
info: Cli: cloning https://github.com/leanprover/lean4-cli
info: Cli: checking out revision 'f7d0ca7c926cdde0562af20394dd25d028b839a5'
info: mathlib: running post-update hooks
Current branch: HEAD
Using cache (Azure) from origin: leanprover-community/mathlib4
Attempting to download 7564 file(s) from leanprover-community/mathlib4 cache
Downloaded: 7564 file(s) [attempted 7564/7564 = 100%, 130 KB/s], Decompressed: 3189
Decompressed 7564 file(s)
Decompressing 706 file(s) (7567 already decompressed)
Decompressed in 6744 ms
Completed successfully!
```

{% endfold %}

接下来保存缓存(但不是必须的), 运行以下命令:

```bash
lake exe cache get
```

输出形如:

```text
Current branch: HEAD
Using cache (Azure) from origin: leanprover-community/mathlib4
No files to download
Already decompressed 8273 file(s)
```

## 配置 VSCode

在 VSCode 中安装插件 [Lean 4](https://marketplace.visualstudio.com/items?itemName=leanprover.lean4) (作者为 leanprover)

接下来重启 VSCode, 在 VSCode 中打开你的项目文件夹, 打开其中的 Lean 文件 `main.lean`.
这样会在编辑其右边出现执行窗口. 你可以尝试如下测试代码:

```lean
import Mathlib.Data.Real.Basic
example (a b : ℝ) : a * b = b * a := by
  rw [mul_comm a b]
```

将光标移到最后一行, 若右侧如下图所示, 则表明你的 Mathlib 已成功安装了.

![](https://cdn.jsdelivr.net/gh/Enthusjast/my-pics@main/20260411195133376.png)

若你想更新 Mathlib, 在终端中运行:

```bash
curl -L https://raw.githubusercontent.com/leanprover-community/mathlib4/master/lean-toolchain -o lean-toolchain
lake update
lake exe cache get
```
