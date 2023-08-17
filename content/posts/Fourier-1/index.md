+++
title = "傅里叶分析（Fourier analysis）基础（1）"
date = "2023-08-17"
author = "xy"
draft = true
+++

傅里叶分析的主要功能是把时域（time domain）信号转换到频域（frequency domain）。翻开高等数学或信号处理的教科书，或者在wikipedia搜索“Fourier transform”，很容易找到这样的公式：

$$
{\hat {f}}(\xi )=\int _{-\infty }^{\infty }f(x)\ e^{-i2\pi \xi x}\ dx.
$$

$f(x)$ 是时域信号，$\hat f(\xi)$描述对应的频域分量。$x$表示时间，$\xi$表示频率；若前者单位为秒 sec，则后者单位为赫兹 Hz。

但是这里 $f(x)$ 的定义域是无限的连续域，我们很难直接上手研究它。在全民 Jupyter Notebook 的时代，我们希望 $f(x)$是长成这样的：

```
f = [1.2, 1.3, 2.0, ..., 0.8, 0.9]
```

这样我们就可以把段有限长度的数组作为时域信号，输入给某个实现了傅里叶转换的软件包，就能得到想要的频率分量了——简单而美好。但是为了实现这个美好的愿望，我们必须把问题定义得更明确：用有限领取代 $(-\infty,\infty)$；用加和$\Sigma$取代积分$\int$；… 所以最终我们要采用的方法，并非原本的傅里叶变换，而是其离散模式 Descrete Fourier Transform (DFT)。

关于为何选取DFT，斯坦福大学音乐与声学计算研究中心 Julius O. Smith III 教授编写的《频谱音频信号处理》（SPECTRAL AUDIO SIGNAL PROCESSING）在线教科书中，提供了非常清晰的指导（[原文链接](https://ccrma.stanford.edu/~jos/sasp/Fourier_Transforms_Continuous_Discrete_Time_Frequency.html)）：

<!-- ![Resize](images/img87_2x.png) -->
<!-- <img src="images/img87_2x.png" alt="text" width=60% /> -->

<p align="center">
    <img src="images/img87_2x.png" alt="text" width=75% />
</p>

