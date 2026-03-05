

## 3.1 Random signals

### 1 Probability Distribution Function (PDF，概率分布函数)

概率密度函数（PDF）是描述随机变量 $X$ 在某个特定值 $x$ 附近取值的可能性的函数，记作 $p_X(x)$。![image-20251106141047402](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106141047402.png)

### 2 Cumulative Distribution Function (CDF，累积分布函数)

积分布函数 $F_X(x)$ 定义为随机变量 $X$ 小于或等于某个特定值 $x$ 的概率：
$$
F_X(x) = P(X \leq x)
$$
即累积概率，是随机变量 $X$ 小于或等于 $x$ 的事件发生的概率。

![image-20251106141131150](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106141131150.png)

### 2 期望和期望相关

![image-20251106141710877](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106141710877.png)



### 3 随机变量的例子

**离散随机变量**

![image-20251106141844726](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106141844726.png)

**连续随机变量**

![image-20251106141900554](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106141900554.png)

![image-20251106141909966](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106141909966.png)

![image-20251106141925224](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106141925224.png)



高斯公式具有**缩放性质**：

如果 $X \sim \mathcal{N}(\mu, \sigma^2)$ 且 $a$ 是一个常数，则 $Y = aX$ 也服从高斯分布，且：
$$
Y \sim \mathcal{N}(a\mu, a^2\sigma^2)
$$
这意味着缩放高斯分布会改变其均值和方差，但它仍然保持高斯分布。

### 4 **零均值随机变量**（Zero-mean random variable）

任意随机变量都可以表示成一个零均值随机变量加上一个常数项 $m_X$，其中 $m_X = E[X]$ 为随机变量 $X$ 的期望值。通过对随机变量 $X(e)$ 进行平移操作，我们可以得到一个新的随机变量 $\tilde{X}(e)$，使得其均值为零：
$$
\tilde{X}(e) = X(e) - m_X
$$
显然，$E[\tilde{X}] = 0$，即新的随机变量 $\tilde{X}(e)$ 的期望值为零。

方差：扣除均值后的二阶矩：
$$
\sigma_X^2 = E\left[ (X - E[X])^2 \right]
$$

### 5 随机变量的函数

如果 $X$ 是一个随机变量，它是一个从样本空间 $\Omega$ 到实数域 $R$ 的映射函数（即 $X: \Omega \to R$），那么 $Y$ 也是一个从 $\Omega$ 到 $R$ 的函数。通常，我们通过函数 $g(X)$ 来定义新的随机变量 $Y$，即：
$$
Y = g(X)
$$
这里，$g(X)$ 是作用于随机变量 $X$ 的一个函数。

对随机变量 $Y = g(X)$ 的期望值可以通过下式计算：
$$
E[g(X)] = \int_{-\infty}^{\infty} g(x) f_X(x) dx
$$
其中，$f_X(x)$ 是随机变量 $X$ 的概率密度函数（PDF），通过这个积分可以得到新随机变量 $Y$ 的期望值。

### 6 两个随机变量的统计特性

**Joint distribution functions of a pair of random variables （两个随机变量的联合分布）**

![image-20251106142348062](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106142348062.png)

![image-20251106142411129](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106142411129.png)



![image-20251106143412126](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106143412126.png)

### 7 随机信号之间的关系

**Orthogonal, uncorrelated and independent（正交、不相关、独立）**

![image-20251106193743807](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106193743807.png)

**公式** $(Y - E[Y]) = a(X - E[X]) + Z$：
 该公式表示，随机变量 $Y$ 可以通过与 $X$ 的线性关系以及一个独立的随机噪声项 $Z$ 来表示。这里，$a$ 是常数，$E[Y]$ 和 $E[X]$ 是它们的期望值，$Z$ 是与 $X$ 无关的噪声项。

#### **无相关性（Uncorrelated）**

**定义**：如果两个随机变量 $X$ 和 $Y$ 无相关，表示它们的协方差为零：
$$
\text{cov}(X, Y) = E[(X - E[X])(Y - E[Y])] = 0
$$
**解释**：无相关性意味着 $X$ 和 $Y$ 之间没有线性关系，协方差为零。但这并不意味着它们没有任何关系，可能存在非线性的关系。

**性质**：
$$
\text{Var}(X + Y) = \text{Var}(X) + \text{Var}(Y), \quad \text{if} \quad \text{cov}(X, Y) = 0
$$
如果两个无相关的随机变量之和，它们的方差是各自方差的和。

#### **正交性（Orthogonal）**

- **定义**：如果两个随机变量 $X$ 和 $Y$ 是正交的，表示它们之间的内积为零：
  $$
  E[XY] = 0
  $$

- **解释**：正交性是一个比无相关性更强的条件，通常用于向量空间中，表示两个随机变量之间没有线性关系。它通常用于描述信号或向量的关系。

#### **独立性（Independent）**

- **定义**：两个随机变量 $X$ 和 $Y$ 独立，表示它们的联合概率分布等于它们的边际概率分布的乘积：
  $$
  f_{XY}(x, y) = f_X(x) f_Y(y)
  $$

- **解释**：独立性是一个更强的条件，表示两个随机变量完全不相关，即一个变量的发生与另一个变量无关。独立性通常意味着它们之间没有任何形式的依赖关系，不仅仅是线性关系。

**三者之间的关系：**

![image-20251106194124905](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106194124905.png)

### 8 复数随机变量 Complex random variable

复数随机变量 $Z(e)$ 将一个复数 $Z$ 分配给样本空间 $\Omega$ 中的每个样本 $e$。简而言之，复数随机变量是由两个实值随机变量组成的，分别表示复数的实部和虚部。

复数随机变量 $Z$ 可以表示为：
$$
Z = X + j \cdot Y
$$
其中，$X$ 和 $Y$ 是实值随机变量，$j$ 是虚数单位（即 $j = \sqrt{-1}$）。

**复数随机变量 $Z$ 的分布是 $X$ 和 $Y$ 的联合分布。**

**部分性质：**

![image-20251106204242830](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106204242830.png)

### 9 随机过程

 **1. 随机过程的定义**

- **随机过程**是一个**二维函数**，它将样本空间 $\Omega$ 映射到函数空间。具体来说，随机过程 $X(e,t)$ 是由样本 $e \in \Omega$ 和时间 $t \in \mathbb{R}$ 共同决定的函数，$e$ 表示实验结果，$t$ 表示时间或其他相关变量。

- 数学表达式为：
  $$
  X(e,t) \in \mathbb{R}, \quad e \in \Omega, \quad t \in \mathbb{R}
  $$

2. **随机过程的组成**

- 随机过程是所有样本函数的集合，表示为：
  $$
  X(t) = \{ x_i(t) \}
  $$
  其中 $x_i(t)$ 是每个样本 $e_i$ 对应的函数。

- **给定实验结果 $e$**，$X(e,t)$ 是一个确定性的函数。这意味着，知道了实验结果 $e$ 后，随机过程 $X(e,t)$ 的值是确定的。

3. **随机过程的性质**

- **随机过程是一个无限数量的随机变量**，它们在时间上分布。具体来说：
  - **给定时间 $t$**，$X(e,t)$ 是一个随机变量。
  - **给定时间 $t$ 和实验结果 $e$**，$X(e,t)$ 是一个确定的实数。

### ![image-20251106205307293](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106205307293.png)

![image-20251106205335392](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106205335392.png)

![image-20251106205422268](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106205422268.png)

## 3.2  随机过程的统计特性 Statistical Characteristics of Random Process

### 1 Probability distribution (随机过程的概率分布)

![image-20251106205611063](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106205611063.png)

![image-20251106210006257](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106210006257.png)



### 2 Mathematical expectation （随机过程的均值）

#### **随机过程的期望（统计平均）**

- **$m_X(t)$** 是一个**确定性函数**，表示随机过程 $X(e, t)$ 的期望。换句话说，它描述了在给定时间 $t$ 时，所有样本的期望值（即随机过程的均值）。

- **$m_X(t)$** 的定义为：
  $$
  E[X(e,t)] = m_X(t)
  $$
  这表示在给定实验结果 $e$ 的情况下，随机过程 $X(e, t)$ 的期望值是一个确定的函数，与 $e$ 无关，但与时间 $t$ 有关。

#### **时间平均（Time Average）**

- **时间平均** $X(e, t)$ 是对每个具体样本的时间上的平均值。对于一个样本 $e$，它表示该样本在不同时间 $t$ 上的平均值。结果依赖于样本 $e$（是随机的），但与时间 $t$ 无关（时间不变的）。

- 公式表示为：

  ![image-20251106211246663](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106211246663.png)

  这表明，**时间平均**是对每个样本在整个时间范围内的平均值进行计算。

#### Zero-mean random process（零均值随机过程）

![image-20251106211715830](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106211715830.png)

### 3 功率（Power）

#### ![image-20251106212731556](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106212731556.png)

### 4 自相关函数

**自相关函数定义**：

- 自相关函数用于衡量一个随机信号在不同时间点之间的相关性。
- 公式 $R_X(t_1, t_2) = E[X(t_1) X^*(t_2)]$ 表示了在时间 $t_1$ 和 $t_2$ 上信号的相关性，其中 $X^*(t_2)$ 是信号的复共轭（如果信号是复数的情况下）。

**平稳过程的自相关**：

- 当 $t_1 = t + \tau$ 和 $t_2 = t$ 时，公式可以简化为 $R_X(t + \tau, t) = E[X(t + \tau) X(t)]$，即信号在不同时间点之间的自相关，$\tau$ 是时间偏移量。

**平均自相关函数**：

- 计算信号的平均自相关函数 $\overline{R_X(\tau)}$ 作为 $R_X(t + \tau, t)$ 的期望值，意味着它是信号在所有时间点上的自相关的统计平均。

**统计平均**：

- $\overline{R_X(\tau)}$ 也是 $R_X^S(e, \tau)$ 的统计平均，即 $\overline{R_X(\tau)} = E[X(e, t) X(e, t+\tau)]$，表示对信号的自相关进行平均处理。

![image-20251106224526428](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106224526428.png)

### 5 Power spectral density（PSD，功率谱密度）

给定样本𝑒，随机过程𝑋(𝑒,𝑡)是一个确定性功率信号，其功率谱密度为：
$$
P_X^S(e,f) = \lim_{T \to \infty} \left( \frac{1}{T} \left| \mathcal{F}[X_T(e,t)] \right|^2 \right)
$$
其中， $\mathcal{F}[X_T(e,t)]$ 是信号 $X(e,t)$ 在时间窗 $T$ 内的傅里叶变换，计算的是傅里叶变换的幅度的平方。

**随机过程的功率谱密度**是所有样本功率谱密度的统计平均值，**即：**
$$
P_X(f) = E \left[ \lim_{T \to \infty} \left( \frac{1}{T} \left| \mathcal{F}[X_T(e,t)] \right|^2 \right) \right] = \lim_{T \to \infty} \left( \frac{1}{T} E \left[ \left| \mathcal{F}[X_T(e,t)] \right|^2 \right] \right)
$$
该公式可以解释为：

- $\mathcal{F}[X_T(e,t)]$ 是信号 $X(e,t)$ 在时间窗 $T$ 内的傅里叶变换。
- 通过对傅里叶变换的幅度平方取期望 $E$，然后再取极限，得到随机过程的功率谱密度。

### 6 维纳-辛钦定理（Wiener-Khinchin Theorem）

**自相关函数与功率谱密度的关系**：
 该定理表明，随机信号的功率谱密度（$P_X(f)$）是自相关函数（$\overline{R}_X(\tau)$）的傅里叶变换。公式为：
$$
\overline{R}_X(\tau) \iff P_X(f)
$$
其中，$\overline{R}_X(\tau)$ 是自相关函数，表示信号自身在不同时间延迟（$\tau$）下的相关性。

**功率谱密度的积分关系**：
 功率谱密度的总功率（$P_X$）等于其频谱的积分：
$$
P_X = \int_{-\infty}^{\infty} P_X(f) df = \overline{R}_X(0)
$$
其中 $P_X(f)$ 是频域上的功率谱密度，$\overline{R}_X(0)$ 是自相关函数在 $\tau = 0$ 时的值，代表信号的平均功率。

### 7 Cross-correlation function（互相关函数）

![image-20251106230152318](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106230152318.png)![image-20251106230204244](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106230204244.png)

![image-20251106230220811](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106230220811.png)

![image-20251106230243409](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106230243409.png)

## 3.3 宽平稳（WSS, Wide-Sense Stationary）

一个随机过程 $x(t)$ 是**宽平稳的**，当且仅当满足以下两个条件：

1. **均值不随时间变化：**
   $$
   E[x(t)] = \text{常数} = \mu_x
   $$
   即平均值在任意时刻都相同。

2. **自相关函数只与时间差有关，而不依赖于绝对时间：**
   $$
   R_x(t_1, t_2) = E[x(t_1)x^*(t_2)] = R_x(t_1 - t_2) = R_x(\tau)
   $$
   即只与 $\tau = t_1 - t_2$ 有关。

如果系统是**线性时不变（LTI）**的，并且输入 $x(t)$ 是 WSS，则输出 $y(t)$ 也是 WSS，且：
$$
R_y(\tau) = R_x(\tau) * |h(\tau)|^2
$$
其中 $h(t)$ 是系统的冲激响应。

## 3.4 Complex random process（复随机过程）

![image-20251107234238732](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107234238732.png)

![image-20251107234255525](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107234255525.png)

![image-20251107234310537](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107234310537.png)

## 3.5 GaussianNoise（高斯噪声）（过一遍）

### 1 介绍

设有一个噪声随机变量 $N$，如果它的概率密度是
$$
p_N(n) = \frac{1}{\sqrt{2\pi}\sigma}\exp\left(-\frac{(n-\mu)^2}{2\sigma^2}\right)
$$
那么我们就说这个噪声是**高斯噪声**，记作
$$
N \sim \mathcal N(\mu,\sigma^2)
$$

- $\mu$：噪声的**均值**（“平均偏移量”）
- $\sigma^2$：噪声的**方差**（“抖动的强度”）



![image-20251107234738435](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107234738435.png)

### 2 Additive white Gaussian noise (AWGN) 加性白高斯噪声

白噪声指具有极宽带宽且功率谱密度恒定的噪声。

![image-20251108194953044](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108194953044.png)

**AWGN通过滤波器：**

在通信原理和信号处理中，**$N_0$** 是一个非常基础且关键的参数，它被称为**噪声功率谱密度（Noise Power Spectral Density）**。

简单来说，$N_0$ 衡量的是“单位带宽内的噪声功率有多大”。

---

1. 物理意义

$N_0$ 代表噪声在 **1 Hz（赫兹）** 带宽内的平均功率。

- **单位**：瓦特/赫兹 ($W/Hz$)，在物理上等同于焦耳 ($J$)。
    
- 计算公式：对于热噪声（一种典型的高斯白噪声），$N_0$ 可以表示为：
    
    $$N_0 = k \cdot T$$
    
    其中，$k$ 是玻尔兹曼常数（$1.38 \times 10^{-23} \ J/K$），$T$ 是系统的等效噪声温度（开尔文）。这意味着温度越高，噪声越强。
    

2. 为什么常看到 $\frac{N_0}{2}$？

这是初学者最容易困惑的地方。在公式中，噪声功率谱密度通常写成 $S_n(f) = \frac{N_0}{2}$。这是因为：

- **双边功率谱（Double-sided PSD）**：在数学推导中，我们通常考虑负频率（从 $-\infty$ 到 $+\infty$）。为了让总功率保持不变，能量被平分到了正负频率两侧，所以每一侧的高度是 $\frac{N_0}{2}$。
    
- **单边功率谱（Single-sided PSD）**：在实际工程测量中，我们只关注正频率。此时，整个 $N_0$ 的能量都集中在正频率上，所以高度就是 $N_0$。
    

3. $N_0$ 与总噪声功率 $P_n$ 的关系

如果你有一个带宽为 $B$ 的系统（例如一个滤波器），那么通过这个系统的总噪声功率 $P_n$ 就是：

$$P_n = N_0 \cdot B$$

（注：如果是使用双边带宽，公式则为 $\frac{N_0}{2} \cdot 2B$ = $N_0 B$）

4. 常见应用：$E_b/N_0$

在评估数字通信系统性能时，你会经常看到 $E_b/N_0$（每比特能量与噪声功率谱密度之比）。

- **$E_b$**：传输一个比特（bit）所消耗的能量。
    
- **$E_b/N_0$**：它相当于数字通信中的“信噪比（SNR）”。它比普通 SNR 更有用，因为它排除了带宽和数据速率的影响，能直观反映不同调制方式（如 QPSK vs 16QAM）的效率。

![屏幕截图 2025-11-08 200204](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-11-08%20200204.png)

### 3 高斯白噪声和确定信号的内积

![屏幕截图 2025-11-08 200738](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-11-08%20200738.png)

![屏幕截图 2025-11-08 200922](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-11-08%20200922.png)

### 4 窄带高斯噪声的解析信号和复包络

![屏幕截图 2025-11-08 202059](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-11-08%20202059.png)

![屏幕截图 2025-11-08 202113](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-11-08%20202113.png)

![屏幕截图 2025-11-08 202320](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-11-08%20202320.png)

![屏幕截图 2025-11-08 202808](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-11-08%20202808.png)![](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-11-08%20202808.png)

### 5 窄带高斯信号的同相分量和正交分量

![image-20251108203626916](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108203626916.png)

一个随机变量 $R$ 若只取非负值 $r\ge 0$，并且概率密度函数是
$$
f_R(r) = 
\begin{cases}
\displaystyle \frac{r}{\sigma^2} e^{-\frac{r^2}{2\sigma^2}}, & r \ge 0 \\
0, & r < 0
\end{cases}
$$
就说 $R$ 服从**瑞利分布**，记作 $R \sim \text{Rayleigh}(\sigma)$。

## 3.6 Matched Filter（匹配滤波器）（过一遍）

![屏幕截图 2025-11-08 204033](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-11-08%20204033.png)

![屏幕截图 2025-11-08 204715](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-11-08%20204715.png)

![屏幕截图 2025-11-08 204836](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-11-08%20204836.png)
