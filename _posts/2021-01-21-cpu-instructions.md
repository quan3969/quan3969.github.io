---
layout: post
title:  "CPU 指令集"
# date:  2021-01-19 13:24:54 +0800  
categories: blog
---

> CPU 有一项非常重要，却没什么人关注的参数：CPU 指令集。它对我们的 CPU 性能到底有什么影响呢？这里是我的一些见解。

先来看两个 CPUID 的图：

![10genCPU](/assets/img/cpu-instructions/10genCPU.gif)
![11genCPU](/assets/img/cpu-instructions/11genCPU.gif)

这分别是 10 代 和 11 代低压 CPU 的参数信息，11 代 CPU 明显比 10 代多支持了一项指令集 AVX-512 的指令集。

但业界对这套指令集众说纷纭，有人觉得这是 CPU 的未来，有人却认为这没什么作用，甚至会拖慢电脑的运行速度（参考这篇[知乎文章](https://www.zhihu.com/question/406517759)）。

同主频下，要想提高 CPU 性能，即 IPC，由以下三条路可走：
1. 更多的 ALU 计算单元。
2. 更强的 SIMD 指令集。
3. 优化告诉缓存和分支预测等 CPU 微结构。

本篇我们主要讲述 CPU 的指令集

### CPU 指令集
对于台式机或传统 x86-64 的 PC，Instructions Set 主要包括以下几种：
1. CPU instructions
2. FPU instructions
3. SIMD instructions
4. AES instructions
5. MPX instructions
6. SMX instructions
7. TSX instructions
8. VMX instructions


在我以前做微机实验，用汇编写程序驱动 8086 时，首次接触到 mov, pop, push 等低级语言的语句。这是能被机器直接翻译并执行的代码，也是最底层，反汇编后能看到的代码。其实当时就应该知道，这就是 x86 的指令集，当然这是指一套指令集，其他也一样。

图中，CPU 指令集有 x86, x86-64, MMX, SSE, SSE2, SSE3, SSE4.2, AVX, AVX2, [AVX-512](https://www.intel.com/content/www/us/en/support/articles/000005779/processors.html), FMA, AES, SHA.

其中 x86 是主要架构，x86-64 是 64 位的 x86，微软管它叫 AMD64. 这其中有很长的一段故事可讲，简单的来说就是 Intel 想搞一套独立的 IA64，不向前兼容，但失败了；而 AMD 也做了一套 64 位的，但可以向前兼容，成功了。

MMX 是 [SMID](http://linasm.sourceforge.net/docs/instructions/index.php)(single-instruction multiple-data) 的原型，SSE, SSE2, SSE3, SSE4.2, AVX, AVX2, AVX-512 是在这个基础上拓展出来的，当然性能也越来约好了，直到 [AVX-512](https://www.intel.com/content/www/us/en/support/articles/000005779/processors.html).

这些指令集都大大提高了机器处理语音、图像等需要矢量计算的能力。

剩下的 FMA, AES, SHA 指令集有它们特定的处理情景。如 AES 就是对软件加密和解密的指令集，有了这套指令能大大加速处理速度。

那么机器是怎么利用这些指令集的呢？这里就牵扯到编译了，微软家的最强 IDE-Visual Studio 它能指定所运用的编译语言和编译优化。

依我的理解，同样用 c 语言写的一段计算，通过不同的编译工具，就能转换成不同的指令集构成的，能让电脑执行的语句。计算机执行这些语句得到所需的计算结果。

利用这些编译工具进行编译，编译出来的成品进行同等运算量的计算，从所需时间来对比，我们便能得知这些指令集哪一套比较好了。

**一句话总结指令集是什么**：指令集就是汇编的语句，能被机器所直接翻译并执行。CPU 要能执行这些指令，晶体管就要做成那样的结构。

对于程序设计：根据指令集所能承载的数据量，对程序需要处理的数据进行最大分割并优化，通过编译工具编译成这样的语句，随后由机器运行，这就能发挥 CPU 的最大效能。
