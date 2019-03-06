---
title: Date
layout: page
---

**2019-2-25 ~ 2019-2-26**

学习 **Auxy** 师傅的 [Webkit Exploitation Tutorial](https://www.auxy.xyz/tutorial/Webkit-Exp-Tutorial/#)
，非常棒的一篇文章！简直太厉害了！

这篇 **Tutorial** 从环境搭建开始，举例介绍了 webkit 中各种漏洞类型，每种类型的洞都列了个历史漏洞。

然后从结构层次介绍了 webkit 包含的内容，着重解释了 **JSC 编译优化过程的阶段性机制**，对 JSC 的一些重要特性，

**JSC Object Model** 机制的介绍非常详细。

**2019-2-27 ~ 2019-2-28**

以 35c3 CTF 的 webkid 为例学习了 webkit 漏洞的利用的一般形式，接着是历史漏洞 **cve-2018-4416** 的调试分析到利用的过程。

记录 **Auxy** 师傅说过的一个学习方式：先看 pj0 的洞 然后再去盲看 commit 联系找 1day patch。

**2019-3-1**

看 "Attacking Client-Side JIT Compilers" 讲 jit 相关的。从 js engine 的组成部分讲起，一些基本的概念。

然后细讲了编译优化部分对代码的处理，优化解释执行的代码生成跟快速的机器码，消除冗余代码。内容很棒！还没完全消化。

结尾放的是用来打 pwn2own 2018 的洞的 demo。

**2019-3-2**

看了点 fuzz 相关的，搭建 libfuzz 环境，一边看 jit 相关的。。。

**2019-3-4 ~ 2019-3-6**

看了一天的 js，然后再来看 saleo 的教程感觉稍微流畅了点？接着看 4441 的洞，试着审计。。。