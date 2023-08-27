+++
title = "傅里叶分析（Fourier analysis）基础（1）——理论"
date = "2023-08-24"
author = "xy"
+++


傅里叶分析的主要功能是把时域（time domain）信号转换到频域（frequency domain）。翻开高等数学或信号处理的教科书，或者在维基百科搜索“Fourier transform”，很容易找到这样的公式：

$$
{\hat {f}}(\xi )=\int _{-\infty }^{\infty }f(x)\ e^{-i2\pi \xi x}\ dx.\label{eq:1}\tag{1}
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
    <img src="images/img87_2x.png" alt="text" width=65% />
</p>

表中左上角象限是适用于我们的需求的——时域和频域均为离散且有限。其中，$x(n)$对应 Eq.(1) 中的时域信号$f(x)$，$X(k)$对应频域表征$\hat{f}(\xi)$。这个公式和维基百科[“离散傅里叶变换”页面](https://en.wikipedia.org/wiki/Discrete_Fourier_transform#)给出的公式 Eq.1 也是一致的：


$$
X_{k}=\sum _{n=0}^{N-1}x_n\cdot e^{-\frac{i2\pi}{N}kn}\label{eq:2}\tag{2}
$$

所以，表中的 $\omega_k$ 即对应 Eq.(2) 中的 $\frac{i2\pi}{N}k$，亦即第 $k$ 个频率分量（$k\in [0,1,\dots,N-1]$）。从算法的角度，DFT是将长度为 $N$ 的序列 $\\{x_n\\}:=x_0,x_1,\dots,x_{N-1}$ 转换为**等长**的序列 $\\{X_k\\}:=X_0,X_1,\dots,X_{N-1}$。

注意，这里的 $x_n$ 和 $X_k$ 都是复数（complex number），由实部（Re）和虚部（Im）组成。$X_k$ 可以理解为输入序列 $\\{x_n\\}$ 与频率为 $\frac{k}{N}$ 的复正弦波（complex sinusoid）之间的互相关（cross-correlation），也就是滑动点积或内积（sliding dot-product/inner-product）。从所得的 N 个频率分量 $\\{X_k\\}$ ($k=0,1,\dots,N-1$)，我们可以重建出时域信号：

$$
x_{n}={\frac {1}{N}}\sum_{k=0}^{N-1}X_{k}\cdot e^{\frac{i2\pi}{N} kn}\label{eq:3}\tag{3}
$$

当 $n$ 的取值为无限，即 $n\in \mathbb {Z}$ 时，上式就是常说的傅里叶级数（Fourier series）。而当 $n$ 的取值有限，$n\in [0,N-1]$ 时，上式就是所谓的傅里叶逆变换（inverse transform）。Eq. (3) 的含义是，时域信号 $x_n$ 可以分解为 $N$ 个不同频率的正弦曲线（sinusoid）之加和，其中第 $k$ 个正弦曲线 $X_k$ 的振幅和相位分别为：

$$
|X_{k}|={\sqrt {\operatorname {Re} (X_{k})^{2}+\operatorname {Im} (X_{k})^{2}}}\\\arg(X_{k})=\operatorname {atan2} {\big (}\operatorname {Im} (X_{k}),\operatorname {Re} (X_{k}){\big )}
$$

所需要的理论基本就是这些，接下来只需找到相应的 Python 包（比如 [scipy.signal.fft](https://docs.scipy.org/doc/scipy/tutorial/fft.html#fast-fourier-transforms)）来开始我们的实验了。

