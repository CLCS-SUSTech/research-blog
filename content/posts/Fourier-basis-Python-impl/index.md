+++
title = "傅里叶分析（Fourier analysis）基础（2）——Python实现"
date = "2023-08-27"
author = "xy"
draft = false
+++

接着上一篇[《傅里叶分析（Fourier analysis）基础（1）——理论》](../fourier-basis-theory)，我们选取[scipy.signal.fft](https://docs.scipy.org/doc/scipy/tutorial/fft.html#fast-fourier-transforms)）来进行傅里叶分析。

<!-- ## Python 实现 -->
为了统一符号，接下来我们在notebook中都使用小写变量 $x$ 表示时域信号（函数），大写变量 $X$ 表示频域表征。 

首先定义一段时域长度为 $N$ 的时域信号（$N=12$）：
```console
>>> import numpy as np
>>> N = 12
>>> x = np.arange(N)
>>> x
array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11])
```

接下来，使用`scipy.signal.fft`进行离散傅里叶转换：

```console
>>> from scipy.fft import fft
>>> X = fft(x)
>>> X
array([66. -0.j        , -6.+22.39230485j, -6.+10.39230485j,
       -6. +6.j        , -6. +3.46410162j, -6. +1.60769515j,
       -6. -0.j        , -6. -1.60769515j, -6. -3.46410162j,
       -6. -6.j        , -6.-10.39230485j, -6.-22.39230485j])
>>> len(X)
12
```

可见，离散傅里叶变换得到的频域表征 $X$ 与时域信号 $x$ 长度相等，$N=12$。每个频率分量 $X_k$ 都是复数，可表示成 $X_k=a+b\cdot j$ 的形式（$k=0,2\dots 11$）。例如，$X_1=-6+22.39j$。

其中 $\\{X_1,X_2,\dots,X_5\\}$ 这 5 个频率分量表示正频率，因其所对应的角频率 $\omega_k=2\pi \frac{k}{N}$ 均在 $[0,\pi)$ 之间：

$$
\omega_1=2\pi\frac{}{12},\ \omega_2=2\pi\frac{2}{12},\ \omega_3=2\pi\frac{3}{12},\ \omega_4=2\pi\frac{4}{12},\ \omega_5=2\pi\frac{5}{12}
$$

在坐标轴上表示如下：



与后 6 个分量 $\\{X_6,X_7,\dots,X_11\\}$ 成共轭（conjugate）关系，即：

$$
X_{k}={\overline {X_{N-k}}}\quad (k=1,2,\dots,N-1)
$$