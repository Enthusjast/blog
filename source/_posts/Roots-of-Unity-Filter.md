---
title: Roots-of-Unity-Filter
date: 2026-03-04 09:47:47
updated: 2026-03-04 09:47:47
tags:
  - maths
  - study
categories: maths
excerpt: 介绍单位根过滤器（Roots of Unity Filter）——利用单位根性质提取生成函数中下标为 n 的倍数的系数和，并附三道练习题。
---

## 单位根

> **定义**
> 
> 方程 $z^n - 1 = 0$ 的根称为 $n$ 次**单位根 (Roots of unity)**.

易知 $n$ 次单位根有互不相同的 $n$ 个,分别为 $\cos \frac{2k\pi}{n} + i \sin \frac{2k\pi}{n}, k = 0, 1, \cdots, n-1$.

> **命题** 
> 
> 设 $\xi = \cos \frac{2\pi}{n} + i \sin \frac{2\pi}{n}$ 为 $n$ 次单位根,则
> $$
> 1 + \xi^m + \xi^{2m} + \cdots + \xi^{(n-1)m} =
> \begin{cases}
>     n, & n \mid m; \\
>     0, & n \nmid m.
> \end{cases}
> $$

*证明*

当 $n \mid m$ 时,有 $\xi^m = 1$,故原式 $= n$.

当 $n \nmid m$ 时,有 $\xi^m \neq 1$,故原式为等比数列和：
$$
\text{原式} = \frac{1 - (\xi^m)^n}{1 - \xi^m} = 0
$$

## Filter

> **定理**
> 
> 设 $\xi = \cos \frac{2\pi}{n} + i \sin \frac{2\pi}{n}$ 为 $n$ 次单位根,多项式 $F(x) = a_0 + a_1x + a_2 x^2 + \cdots$ (有限多项),则
> $$
> a_0 + a_n + a_{2n} + \cdots = \frac{1}{n} \sum_{k=0}^{n-1} F(\xi^k)
> $$

*证明*

易知右端每个 $a_m$ 的系数为
$$
\frac{1}{n} \sum_{k=0}^{n-1} (\xi^k)^m =
\begin{cases}
    1, & n \mid m; \\
    0, & n \nmid m.
\end{cases}
$$
故右端即为左端.

这个定理可以帮我们 "filter" 出那些下标被 $n$ 整除的项的系数和,运用单位根的运算性质.
这个定理就被我们称为 "Roots of Unity Filter".
它也可以用于求解数列中相应项之和,只要运用生成函数 (Generating Function) 的技术.
有关生成函数的理解可以看这个[视频 (BV1QM411A73c)](https://www.bilibili.com/video/BV1QM411A73c/)

笔者没有找到 "Roots of Unity Filter" 的中文名称,直接翻译可能类似 "单位根过滤器",但中文互联网上没有查找到相应结果.
中文 OI(信息学竞赛) 社区中有 "单位根反演" 的说法,指代的算法类似于我们上面所说的定理.
[一篇文章](https://notes.sshwy.name/Math/Unit-Root-Inversion/)给出其英文名为 "unit root inversion",
但英文互联网中也没有相应结果. 那我们还是称其为 "Roots of Unity Filter" 吧.

> **推论**
> 
> 设 $r \in [1, n - 1]$, $G(x) = x^rF(x)$, 则
> $$
> a_{n - r} + a_{2n - r} + \cdots = \frac{1}{n} \sum_{k=0}^{n-1} G(\xi^k)
> $$

这个推论的证明十分简单,我们把它留给读者思考.

> **注记**
> 
> **用哪个单位根？** 上面我们只使用了 $n$ 个单位根中的一个 $\xi = \cos \frac{2\pi}{n} + i \sin \frac{2\pi}{n}$.
> 事实上,对于任何一个与 $n$ 互素的正整数 $k$, 使用 $\xi^k$ 也可行. 但我们仍推荐使用 $\xi$.
> 我从未见过任何一个问题,其中 $\xi^k$ 可行而 $\xi$ 不可行.
> 
> 更深入地讲,当 $(n, k) = 1$ 时,$\{ \xi^k, (\xi^k)^2, \cdots, (\xi^k)^{n - 1} \}$
> 为 $\{ \xi, \xi^2, \cdots, \xi^{n - 1} \}$ 的一个排列,因此我们可以说二者没有区别.

## 一些题目

> **练习 1**
> 
> 设 $\binom{n}{k}$ 为二项式系数,求 $\binom{2026}{0} + \binom{2026}{3} + \binom{2026}{6} + \cdots + \binom{2026}{2025}$.

**提示** 取 $F(x) = (1 + x)^{2026}$, 用三次单位根 filter.

> **练习 2**
> 
> 一个班级中有 $a$ 个男生,$b$ 个女生. 现在要在其中选出若干同学组成一个代表团,要求男生数与女生数之差为 4 的倍数,共有多少种满足条件的选法？

**解答** 设 $F(x) = (1 + x)^a (1 + y)^b$, 易知其展开式中 $x^my^n$ 项的系数 (记为 $c_{mn}$) 即为选取 $m$ 个男生与 $n$ 个女生的方法数.
我们要对满足 $4 \mid m - n$ 的 $c_{mn}$ 求和,但 $c_{00} = 1$ 除外.
令 $G(x) = F(x, \frac{1}{x})$, 则 $F(x, y)$ 中的 $x^my^n$ 项变为 $G(x)$ 中的 $x^{m - n}$ 项. 于是对 $G(x)$ 用四次单位根 filter 即可.

接下来这道题为刚结束的 2026 年中科大少年班入围考试数学测试倒数第 2 题.

> **练习 3**
> 
> 用 3 种颜色为 $n$ 边形染色,要求相邻顶点颜色不同,有多少种不同的染色方法？

**解答** 将三种颜色编号为 0, 1, 2, 则相邻顶点颜色编号之差 (模 3 取余) 只能为 1, 2.

设 $n$ 个顶点颜色分别为 $s_1, s_2, \cdots, s_n$, 相邻顶点颜色之差分别为 $d_1, d_2, \cdots, d_n$,  
其中 $s_{i + 1} \equiv s_i + d_i \pmod{3}, i = 1, 2, \cdots, n - 1$, 且 $s_1 \equiv s_n + d_n \pmod{3}$.

令 $F(x) = (x + x^2)^n$, 则其展开式中 $x^n$ 项的系数即为满足 $d_1 + d_2 + \cdots + d_n \equiv n \pmod{3}$ 的选法数.
由题意知 $3 \mid n$ (因为 $n$ 个顶点转一圈回到原处). 于是对$F(x)$ 用 3 次单位根 filter,
这样就得到了满足 $3 \mid d_1 + d_2 + \cdots + d_n$ 的方法数.

再给所得的系数和乘 3, 因为第一个顶点有 3 种颜色可选.