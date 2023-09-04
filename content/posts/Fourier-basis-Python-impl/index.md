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

可见，离散傅里叶变换得到的频域表征 $X$ 与时域信号 $x$ 长度相等，$N=12$。每个频率分量 $X_k$ 都是复数，可表示成 $X_k=a+b\cdot j$ （$k=1,2\dots 12$）的形式。比如，$X_2=-6+22.39j$。