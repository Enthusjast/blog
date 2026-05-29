---
title: 在 USTC Vlab 中配置 TeX Live
date: 2026-03-25 10:39:01
updated: 2026-04-11 22:07:37
tags:
    - life
categories: life
excerpt: 在科大 Vlab 平台在线安装 TeX Live 并配置 VSCode 远程 LaTeX 开发的完整教程，含中文支持和格式化配置。
---

**我是 Joker!** 刚得知 Vlab 内置了 TeX Live 2026, 那我这篇文章白写了(

---

Windows 下的 TeX Live 性能远远不如 Linux 中的 TeX Live, 且在 Windows 下配置和使用都较为复杂. 我曾尝试过将 TeX Live 配置在 WSL 中, 但是反而出现了更多问题. 前几日听说了[科大 Vlab 项目](https://Vlab.ustc.edu.cn/)提供了免费的 Linux 平台, 于是我决定在上面配置 TeX Live 及尝试远程开发.

有关 Vlab 平台的注册与使用, 参见 [Vlab 文档](https://Vlab.ustc.edu.cn/docs/).

## 安装 TeX Live

使用科大 Vlab 平台可以方便快捷调用科大开源软件镜像, 所以下文使用在线安装 TeX Live 的方式.

### 1. 下载安装程序

```bash
cd /tmp
wget http://mirrors.ustc.edu.cn/CTAN/systems/texlive/tlnet/install-tl-unx.tar.gz # 使用科大镜像源
tar -xzf install-tl-unx.tar.gz
```

### 2. 运行安装程序

```bash
cd install-tl-*/
sudo ./install-tl --repository https://mirrors.ustc.edu.cn/CTAN/systems/texlive/tlnet/ # 指定科大镜像源
```

接下来会看到类似如下的文字

{% fold info @安装页面 %}

```text
======================> TeX Live installation procedure <=====================

======>   Letters/digits in <angle brackets> indicate   <=======
======>   menu items for actions or customizations      <=======
= help>   https://tug.org/texlive/doc/install-tl.html   <=======

 Detected platform: GNU/Linux on x86_64

 <B> set binary platforms: 1 out of 15

 <S> set installation scheme: scheme-full

 <C> set installation collections:
     40 collections out of 41, disk space required: 9404 MB (free: 9841 MB)

 <D> set directories:
   TEXDIR (the main TeX directory):
     /usr/local/texlive/2026
   TEXMFLOCAL (directory for site-wide local files):
     /usr/local/texlive/texmf-local
   TEXMFSYSVAR (directory for variable and automatically generated data):
     /usr/local/texlive/2026/texmf-var
   TEXMFSYSCONFIG (directory for local config):
     /usr/local/texlive/2026/texmf-config
   TEXMFVAR (personal directory for variable and automatically generated data):
     ~/.texlive2026/texmf-var
   TEXMFCONFIG (personal directory for local config):
     ~/.texlive2026/texmf-config
   TEXMFHOME (directory for user-specific files):
     ~/texmf

 <O> options:
   [ ] use letter size instead of A4 by default
   [X] allow execution of restricted list of programs via \write18
   [X] create all format files
   [X] install macro/font doc tree
   [X] install macro/font source tree
   [ ] create symlinks to standard directories

 <V> set up for portable installation

Actions:
 <I> start installation to hard disk
 <P> save installation profile to 'texlive.profile' and exit
 <Q> quit

Enter command:
```

{% endfold %}

输入 `I` 开始安装. 这会耗费较长时间(取决于网速), 因为它会从镜像站下载数千个文件.

{% note warning %}
**Attention**

TeX Live 安装可能占用 10GB+ 的存储空间.
{% endnote %}

安装过程中会显示如下若干文字

{% fold info @安装提示 %}

```text
Installing to: /usr/local/texlive/2026
Installing [1/4, time/total: ??:??/??:??]: hyphen-base [23k]
Installing [2/4, time/total: 00:00/00:00]: kpathsea [1291k]
Installing [3/4, time/total: 00:01/00:01]: texlive-scripts [563k]
Installing [4/4, time/total: 00:01/00:01]: texlive.infra [671k]
Time used for installing the packages: 00:01
Installing [0001/5016, time/total: ??:??/??:??]: 12many [376k]
......
Installing [5016/5016, time/total: 01:21:49/01:21:49]: zztex [147k]
Time used for installing the packages: 1:21:51
[20:13:54] running mktexlsr /usr/local/texlive/2026/texmf-dist ...
mktexlsr: Updating /usr/local/texlive/2026/texmf-dist/ls-R...
mktexlsr: Done.
writing fmtutil.cnf to /usr/local/texlive/2026/texmf-dist/web2c/fmtutil.cnf
writing updmap.cfg to /usr/local/texlive/2026/texmf-dist/web2c/updmap.cfg
writing language.dat to /usr/local/texlive/2026/texmf-var/tex/generic/config/language.dat
writing language.def to /usr/local/texlive/2026/texmf-var/tex/generic/config/language.def
writing language.dat.lua to /usr/local/texlive/2026/texmf-var/tex/generic/config/language.dat.lua
[20:14:37] running mktexlsr /usr/local/texlive/2026/texmf-var /usr/local/texlive/2026/texmf-config /usr/local/texlive/2026/texmf-dist ...
mktexlsr: Updating /usr/local/texlive/2026/texmf-config/ls-R...
mktexlsr: Updating /usr/local/texlive/2026/texmf-dist/ls-R...
mktexlsr: Updating /usr/local/texlive/2026/texmf-var/ls-R...
mktexlsr: Done.
[20:14:38] running updmap-sys --nohash ...done
[20:15:00] re-running mktexlsr /usr/local/texlive/2026/texmf-var /usr/local/texlive/2026/texmf-config ...
mktexlsr: Updating /usr/local/texlive/2026/texmf-config/ls-R...
mktexlsr: Updating /usr/local/texlive/2026/texmf-var/ls-R...
mktexlsr: Done.
setting up ConTeXt caches: [20:15:02] running mtxrun --generate ...done
[20:15:08] running context --generate --luatex ...done
pre-generating all format files, be patient...
[20:15:13] running fmtutil-sys --no-error-if-no-engine=luametatex,luajithbtex,luajittex,mfluajit --no-strict --all ...failed
./install-tl: fmtutil-sys --no-error-if-no-engine=luametatex,luajithbtex,luajittex,mfluajit --no-strict --all failed (status 28):
[20:18:47] running package-specific postactions
[20:18:49] finished with package-specific postactions

Summary of warnings:
./install-tl: fmtutil-sys --no-error-if-no-engine=luametatex,luajithbtex,luajittex,mfluajit --no-strict --all failed (status 28):

 ----------------------------------------------------------------------
 The following environment variables contain the string "tex"
 (case-independent).  If you're doing anything but adding personal
 directories to the system paths, they may well cause trouble somewhere
 while running TeX.  If you encounter problems, try unsetting them.

 Please ignore spurious matches unrelated to TeX. (To omit this check,
 set the environment variable TEXLIVE_INSTALL_ENV_NOCHECK.)

    SUDO_COMMAND=./install-tl --repository https://mirrors.ustc.edu.cn/CTAN/systems/texlive/tlnet/
    TEXLIVE_INSTALL_NO_DISKCHECK=1
 ----------------------------------------------------------------------
欢迎进入 TeX Live 的世界！
请参阅 /usr/local/texlive/2026/index.html 获取文档链接。

TeX Live 网站 (https://tug.org/texlive/) 提供所有更新
和更正。TeX Live 是世界各地 TeX 用户组的联合项目；
请考虑加入最适合您的群组来支持它。群组列表可在
https://tug.org/usergroups.html 上找到。

将 /usr/local/texlive/2026/texmf-dist/doc/man 添加到 MANPATH。
将 /usr/local/texlive/2026/texmf-dist/doc/info 添加到 INFOPATH。
最重要的是，将  /usr/local/texlive/2026/bin/x86_64-linux
添加到当前和未来会话的 PATH。

Logfile: /usr/local/texlive/2026/install-tl.log
```

{% endfold %}

### 3. 配置环境变量

安装完成后, 需要将 TeX Live 的路径添加到 `~/.bashrc` 文件中

```bash
# 查看当前安装的版本
ls /usr/local/texlive
```

```bash
# 创建一个不带版本号的软连接
sudo ln -s /usr/local/texlive/20XX /usr/local/texlive/latest
# Attention: 这里需要将 20XX 替换为你实际安装的版本号.
```

```bash
# 打开配置文件
nano ~/.bashrc
```

在文件末尾添加以下行

```bash
export PATH=/usr/local/texlive/latest/bin/x86_64-linux:$PATH
export MANPATH=/usr/local/texlive/latest/texmf-dist/doc/man:$MANPATH
export INFOPATH=/usr/local/texlive/latest/texmf-dist/doc/info:$INFOPATH
```

```bash
# 生效配置
source ~/.bashrc
```

### 4. 验证安装

运行下列命令来检查是否成功

```bash
tex -v
latex -v
xelatex -v
```

输出应当形如

- `tex -v` 的输出

```text
TeX 3.141592653 (TeX Live 2026)
kpathsea version 6.4.2
Copyright 2026 D.E. Knuth.
...
```

- `latex -v` 的输出

```text
pdfTeX 3.141592653-2.6-1.40.29 (TeX Live 2026)
kpathsea version 6.4.2
Copyright 2026 Han The Thanh (pdfTeX) et al.
...
```

- `xelatex -v` 的输出

```text
XeTeX 3.141592653-2.6-0.999998 (TeX Live 2026)
kpathsea version 6.4.2
Copyright 2026 SIL International, Jonathan Kew and Khaled Hosny.
...
```

## 远程开发

参照 [Vlab 文档](https://Vlab.ustc.edu.cn/docs/) 配置 Vlab 平台的 SSH 连接, 以及通过 VSCode 连接 Vlab.

### 1. 配置 VSCode

在 VSCode 中安装 LaTeX 开发扩展: LaTeX Workshop

为了让 VSCode 能够正确调用服务器上的工具链(特别是处理中文时常用的 `xelatex`), 需要修改 VSCode 的 `settings.json`.

在远程窗口中, 按 `Ctrl + Shift + P`, 输入并选择 `Preferences: Open Remote Settings (JSON)`

添加或修改如下配置

{% fold info @配置 %}

```json
{
    "latex-workshop.latex.autoBuild.run": "onSave",
    "latex-workshop.showContextMenu": true,
    "latex-workshop.intellisense.package.enabled": true,
    "latex-workshop.latex.tools": [
        {
            "name": "XeLaTeX",
            "command": "xelatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        },
        {
            "name": "PDFLaTeX",
            "command": "pdflatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOCFILE%"
            ]
        },
        {
            "name": "LaTeXmk",
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "-outdir=%OUTDIR%",
                "%DOCFILE%"
            ]
        },
        {
            "name": "Biber",
            "command": "biber",
            "args": [
                "%DOCFILE%"
            ]
        },
        {
            "name": "BibTeX",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ]
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "PDFLaTeX",
            "tools": [
                "PDFLaTeX"
            ]
        },
        {
            "name": "PDFLaTeX * 2",
            "tools": [
                "PDFLaTeX",
                "PDFLaTeX"
            ]
        },
        {
            "name": "XeLaTeX",
            "tools": [
                "XeLaTeX"
            ]
        },
        {
            "name": "XeLaTeX * 2",
            "tools": [
                "XeLaTeX",
                "XeLaTeX"
            ]
        },
        {
            "name": "BibTeX",
            "tools": [
                "BibTeX"
            ]
        },
        {
            "name": "LaTeXmk",
            "tools": [
                "LaTeXmk"
            ]
        },
        {
            "name": "XeLaTeX->BibTeX->XeLaTeX*2",
            "tools": [
                "XeLaTeX",
                "BibTeX",
                "XeLaTeX",
                "XeLaTeX"
            ]
        },
        {
            "name": "PDFLaTeX->BibTeX->PDFLaTeX*2",
            "tools": [
                "PDFLaTeX",
                "BibTeX",
                "PDFLaTeX",
                "PDFLaTeX"
            ]
        },
        {
            "name": "XeLaTeX->Biber->XeLaTeX*2",
            "tools": [
                "XeLaTeX",
                "Biber",
                "XeLaTeX",
                "XeLaTeX"
            ]
        },
    ],
    "latex-workshop.latex.recipe.default": "lastUsed",
    "latex-workshop.latex.clean.fileTypes": [
        "*.aux",
        "*.bbl",
        "*.blg",
        "*.idx",
        "*.ind",
        "*.lof",
        "*.lot",
        "*.out",
        "*.toc",
        "*.acn",
        "*.acr",
        "*.alg",
        "*.glg",
        "*.glo",
        "*.gls",
        "*.ist",
        "*.fls",
        "*.log",
        "*.fdb_latexmk",
    ],
    "latex-workshop.latex.autoClean.run": "onBuilt",
    "latex-workshop.view.pdf.internal.synctex.keybinding": "double-click",
    "latex-workshop.view.pdf.viewer": "tab",
}
```

{% endfold %}

配置好 LaTeX Workshop 后, 就可以进行 LaTeX 远程开发了.

如果您在 Windows 下已经配置好了 LaTeX Workshop, 一般可以直接将其迁移至这里, 只需要注意路径的设置.

{% note warning %}
**Attention**

如果直接将项目文件移动至 Ubuntu 中, 建议先清除一遍临时文件 (`.aux`, `.log`, `.fls` 等), 以免 Windows 下的路径缓存干扰 Linux 下的编译.
{% endnote %}

### 2. 验证配置

随便写个小文档, 例如

```latex
\documentclass{article}

\begin{document}

He110, w0r1d!

\end{document}
```

## 补充

### 1. 安装或更新宏包

安装完 TeX Live 后, 如果发现缺少某个新的宏包, 可以使用 `tlmgr` (TeX Live Manager) 进行在线更新或安装.

```bash
# 添加 tlmgr 路径
sudo /usr/local/texlive/latest/bin/x86_64-linux/tlmgr path add
```

```bash
# 更新宏包索引
sudo tlmgr option repository https://mirrors.ustc.edu.cn/CTAN/systems/texlive/tlnet/
```

```bash
# 安装宏包
sudo tlmgr install <packagename>
```

```bash
# 移除宏包
sudo tlmgr remove <packagename>
```

```bash
# 查看所有更新的宏包
sudo tlmgr update --list
```

```bash
# 更新所有需要更新的宏包
sudo tlmgr update --self --all
```

### 2. 配置 LaTeX 格式化

在 Ubuntu 环境下, 通过 VSCode 远程配置 LaTeX 格式化，最核心的工具是 `latexindent`. 它是 TeX Live 的自带脚本, 支持自动缩进, 对齐和换行等处理.

安装 `latexindent` 相关依赖

```bash
# 安装 Perl 包管理器
sudo apt update
sudo apt install perl cpanminus

# 安装 latexindent 运行所需的 4 个核心模块
sudo cpanm YAML::Tiny
sudo cpanm File::HomeDir
sudo cpanm Log::Log4perl
sudo cpanm Log::Dispatch
sudo cpanm Unicode::GCString
```

在终端输入命令 `latexindent -v`, 若安装成功, 输出应当形如

```text
4.0, 2026-03-15
```

参照上文打开 VSCode 配置文件, 添加或修改如下配置

{% fold info @配置 %}

```json
{
    // 添加 latexindent 路径
    "latex-workshop.formatting.latexindent.path": "latexindent",

    // 指定格式化引擎
    "latex-workshop.formatting.latex": "latexindent",
    
    // 传递给 latexindent 的参数
    "latex-workshop.formatting.latexindent.args": [
        "-m",                // 允许修改行尾（重排文本）
        "-w",                // Overwrite，直接修改原文件
        "-y=indentPreamble:1", // 同时也缩进导言区（\documentclass 到 \begin{document} 之间）
    ],

    // 开启自动格式化（按需开启）
    "editor.formatOnSave": true,    // 保存时自动美化
    "editor.formatOnType": true,    // 输入时自动美化
    
    // 指定默认格式化器
    "[latex]": {
        "editor.defaultFormatter": "James-Yu.latex-workshop",
        "editor.formatOnPaste": true,
    },
}
```

{% endfold %}

### 3. 配置中文字体

Ubuntu 所使用的字体与 Windows 不同, 我们需要安装开源字体, 并在 LaTeX 文档中指定使用.

```bash
# 安装开源中文字体(思源系列)
sudo apt install fonts-noto

# 刷新字体缓存
fc-cache -fv
```

在 LaTeX 文档导言区中指定字体

```latex
\usepackage{fontspec}
\setmainfont{Noto Serif CJK SC}
\setsansfont{Noto Sans CJK SC}
```
