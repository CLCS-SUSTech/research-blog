+++
title = "傅里叶分析（Fourier analysis）基础（2）——Python实现"
date = "2023-08-27"
author = "xy"
draft = true
+++

接着上一篇[《傅里叶分析（Fourier analysis）基础（1）——理论》]（），我们选取[scipy.signal.fft](https://docs.scipy.org/doc/scipy/tutorial/fft.html#fast-fourier-transforms)）来开始实验。

<!-- ## Python 实现 -->
为了统一符号，接下来我们在notebook中都使用小写变量 $x$ 表示时域信号（函数），大写变量 $X$ 表示频域表征。 