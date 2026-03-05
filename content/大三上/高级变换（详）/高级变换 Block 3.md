> 何威翰，编辑于2025/12/4
## 6 小波变换
### 6.1 介绍

小波是“小的波”，是一种 **短时、局部、振荡的函数**。

通过**缩放 (scale)** 与 **平移 (shift)** 一个母小波（mother wavelet），可以得到一族子小波（daughter wavelets）。

大尺度（a 大）：对应 **低频**、宽窗；小尺度（a 小）：对应 **高频**、窄窗。

![image-20251203220858342](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203220858342.png)

### 6.2 连续小波变换（CWT）

CWT 是一个依赖 *两个变量（a，b）* 的变换：

- **a：尺度**
- **b：平移**

公式：

![image-20251203220958540](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203220958540.png)

- 同时给出 **时间 + 频率** 信息
- 可以画 **Scalogram（尺度图）**

| STFT                           | CWT                             |
| ------------------------------ | ------------------------------- |
| 窗宽固定 → 时间/频率分辨率固定 | 窗宽随尺度改变 → **可变分辨率** |
| 难以同时兼顾低频与高频         | 更自然地处理非平稳信号          |

为了从 CWT 重建原信号，需要满足 **可容许条件（Admissibility Condition）**（p.15–16）：
$$
C_\psi=\int\frac{|\Psi(\omega)|^2}{|\omega|}\,d\omega < \infty
$$
这意味着：

- 小波的 **平均值为 0**（零均值）
- Fourier 能量在低频必须快速衰减

### 6.3 多分辨率分析 MRA

MRA 解决了 CWT 的冗余与效率问题。

它把信号分成两个部分：

（1）**逼近部分（Approximation）——低频**：平滑趋势

（2）**细节部分（Detail）——高频**：局部快速变化

![image-20251203221515582](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203221515582.png)

任何信号 s(t) 都可以写成（p.4 图示）：
$$
s(t)=\sum_n c_{m,n}\phi_{m,n}(t)+\sum_{k=0}^{m-m_0-1}\sum_n d_{k,n}\psi_{k,n}(t)
$$
这意味着：

- 求 **逼近系数 $c_{m,n}$** 其实就是信号投影到 scaling function φ
- 求 **细节系数 $d_{m,n}$** 其实就是信号投影到 wavelet function ψ

y因此我们可以通过递归公式（两尺度方程）算系数：
$$
\phi(t)=\sum_k p_k\phi(2t-k)
$$
这意味着 φ 可以通过**卷积 + 下采样**计算。

于是定义：

- **低通滤波器 $h_0[n]$** ← 来自 φ 的系数
- **高通滤波器 $h_1[n]$** ← 来自 ψ 的系数

利用这些滤波器，就能算出下一层的系数：

- **逼近系数：**

$$
c_{m-1,n}= \sqrt{2}\sum_i h_0[i-2n]c_{m,i}
$$

- **细节系数：**

$$
d_{m-1,n}= \sqrt{2}\sum_i h_1[i-2n]c_{m,i}
$$

**子空间结构**


$$
\cdots \subset V_{2}\subset V_1\subset V_0 \subset V_{-1}\subset \cdots
$$
且：
$$
V_{j+1}=V_j\oplus W_j
$$
含义：

- 每一层逼近空间 + 该层细节空间 = 上一层更精细的空间
- 逐层分解最终可以完全重建信号

![image-20251203221554449](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203221554449.png)

所以，我们这样来算**Mallat 小波分解：**

- 每一层先通过 **H0（低通）** 产生新的 c
- 再通过 **H1（高通）** 产生 d
- 然后对新 c 再重复下一层分解

![image-20251203222230881](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203222230881.png)

![image-20251203222239062](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203222239062.png)



**例：**![image-20251203222328724](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203222328724.png)

![image-20251203222335434](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203222335434.png)

### 6.4 信号重建（逆小波变换）

如下步骤：

- 对 c、d 分别 **上采样 ×2**
- 通过逆低通 $H_0(\omega)$ 或逆高通 $H_1(\omega)$
- 再相加

![image-20251203222520823](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203222520823.png)

**例：**

![image-20251203222544191](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203222544191.png)

![image-20251203222554627](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203222554627.png)

![image-20251203222600727](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203222600727.png)

### 6.5 三种变换的区别

傅里叶变换（Fourier Transforms）：用于获得一个随时间变化的函数的**频率谱（frequency spectrum）**。

余弦变换（Cosine Transforms）：用于识别输入数据的**变化速率（rate-of-change）**。

小波变换（Wavelet Transforms）：用于识别输入数据中的**整体趋势（approximations）**，以及识别输入数据中出现的**短时特征或瞬时异常（short-duration features or artifacts）**。

| 变换          | 输出 | 假设输入   | 能否时频分析 | 特点                     |
| ------------- | ---- | ---------- | ------------ | ------------------------ |
| **DFT**       | 复数 | 周期       | ❌            | 频率准确，相位可得       |
| **DCT**       | 实数 | 周期 + 偶  | ❌            | 能量集中、压缩好（JPEG） |
| **DHT / DWT** | 实数 | 无需周期性 | ✔            | 时间 + 频率，多尺度分析  |
