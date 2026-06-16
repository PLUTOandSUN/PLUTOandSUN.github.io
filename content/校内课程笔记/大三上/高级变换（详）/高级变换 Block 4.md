> 何威翰，编辑于2025/12/4
## 7 KLT变换

### 7.1 特征值变换

**特征值 λ 满足：**
$$
\det(A - \lambda I) = 0
$$
**特征向量 v 满足：**
$$
(A - \lambda I)v = 0
$$
意思是：
$$
Av = \lambda v
$$
即：
 **矩阵 A 作用在向量 v 上，只改变其长度（缩放 λ 倍），方向不变。**



### 7.2 线性变换编码

### 7.3 PCA

### 7.4 KLT

### 7.5 协方差矩阵，PCA（主成分分析）与 KLT 变换的计算

为什么 PCA 要用协方差矩阵？

因为协方差描述：

- 数据在各维度的方差
- 各维度之间的相关程度

**1D 方差：**
$$
Var(x)=\frac{1}{N-1}\sum(x_i - \bar{x})^2
$$
**2D 协方差：**
$$
Cov(x,y)=\frac{1}{N-1}\sum(x_i-\bar{x})(y_i-\bar{y})
$$
协方差矩阵表示为：
$$
\Sigma=
\begin{bmatrix}
Var(x) & Cov(x,y)\\
Cov(y,x) & Var(y)
\end{bmatrix}
$$
算出特征值后，对应的特征向量方向分别是：

- 主方向（最大 λ）：数据变化最大
- 次方向（小 λ）：变化小 → 可压缩

**特征向量提供了数据变化最大的方向（主成分），特征值表示该方向的方差大小（能量大小）**

在 KLT / PCA 中：

- 最大特征值方向 → 主成分（最重要，应保留）
- 最小特征值方向 → 次成分（可以丢弃 → 压缩）

这与 DCT、DWT 的思想一致，只是 PCA/KLT 是**数据驱动的最优变换**。



**具体KLT变换的步骤为：**

设
$$
\mathbf{X} = [\vec{x}_0, \vec{x}_1, \ldots, \vec{x}_{N-1}]
$$
**1. 求输入数据的均值向量**
$$
E(\mathbf{X}) = \frac{1}{N}\sum_{i=0}^{N-1} \vec{x}_i
$$
**2. 求协方差矩阵**
$$
R_{XX} = \frac{1}{N-1}\sum_{i=0}^{N-1} (\vec{x}_i - E(\vec{x}))(\vec{x}_i - E(\vec{x}))^{T}
$$
**3. 求协方差矩阵的特征值**
$$
|R_{XX} - \lambda I| = 0
$$
**4. 求协方差矩阵的特征向量**
$$
(R_{XX} - \lambda_i I)\vec{\phi}_i = 0
$$
**5. 归一化特征向量**
$$
\vec{\phi}^{*}_i = \frac{\vec{\phi}_i}{|\vec{\phi}_i|}
\quad \text{使得} \quad
\langle \vec{\phi}_i, \vec{\phi}_i^{*} \rangle = 1
$$
**6. 变换输入数据**
$$
\mathbf{Y} = \Phi^{T}\mathbf{X},
\quad \text{其中} \quad
\Phi^{T} = [\vec{\phi}^{*}_1,\ \vec{\phi}^{*}_2,\ \ldots]
$$


**例：**![image-20251204013737121](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251204013737121.png)

![image-20251204013750906](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251204013750906.png)

![image-20251204013801991](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251204013801991.png)

![image-20251204013827004](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251204013827004.png)

![image-20251204013900586](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251204013900586.png)



## 8 Wigner–Ville Distribution（WVD）

### 8.1 介绍

WVD 的核心来自“即时自相关函数”：
$$
R(t,\tau)=s(t+\tau/2)s^*(t-\tau/2)
$$
然后做傅里叶变换（对 τ）：
$$
W_s(t,\omega)=\int_{-\infty}^{\infty}s(t+\tau/2)s^*(t-\tau/2)e^{-j\omega\tau}d\tau
$$
 **解释：**

- s(t+τ/2) 和 s(t−τ/2) 是信号自身的“左右偏移版本”
- 乘在一起得到“瞬时相关性”
- 再做 Fourier → 得到“该时间点对应的频率能量”

**例子**

![image-20251204021716159](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251204021716159.png)

![image-20251204021725343](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251204021725343.png)



### 8.2 优势

1. **严格满足能量守恒**

   时间边缘条件：
   $$
   \frac{1}{2\pi}\int W(t,\omega)d\omega = |s(t)|^2
   $$
   频率边缘条件：
   $$
   \int W(t,\omega)dt = |S(\omega)|^2
   $$
   → **WVD 同时包含全部的时域能量与频域能量**。

2. **对时移与调频不变**

- 信号平移 → WVD 也平移
- 信号调频 → WVD 也平移



### 8.3 劣势

**最大的问题：交叉项（cross-terms）**

如果信号是：
$$
s(t)=s_1(t)+s_2(t)
$$
WVD 不是简单相加，而是：
$$
W_s = W_{s_1} + W_{s_2} + 2\Re(W_{s_1,s_2})
$$
第三项就是 **交叉项（cross-term）**，它：

- 出现在两个信号能量之间的位置
- 震荡得非常厉害
- 经常比真正的能量还强
- 会污染时频图

![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/20251230193343971.png)


**减少交叉项的方法：**

1. **Pseudo-WVD（PWVD）**

​	在 τ 上加窗口函数 h(τ)：
$$
PWVD=\int s(t+\tau/2)s^*(t-\tau/2)h(\tau)e^{-j\omega\tau}d\tau
$$
​	→ **在频率方向进行平滑**，减少震荡。

2. **Smoothed-WVD（SWVD）**

   用 2D 低通滤波器 φ(x,y) 对 WVD 做二维卷积：
   $$
   SWVD(t,\omega)=\iint \phi(x,y)WVD(t-x,\omega-y)\,dx\,dy
   $$
   → 更强平滑，减少更多交叉项
    → 但 **分辨率下降**

### 8.4 WVD 与 STFT、Wavelet 的关系

**STFT spectrogram = WVD 的平滑版**
$$
|STFT|^2 = WVD_s * WVD_{\text{window}}
$$
 **Wavelet scalogram 也是 WVD 的平滑版**
$$
SCAL(a,b)=\iint WVD_s WVD_\psi
$$
因此：

> **WVD 分辨率最高，是所有常见时频方法的“母方法”。
>  STFT 和 Wavelet 都是它平滑后的子版本。**

![image-20251204022204674](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251204022204674.png)



### 8.5 总结

**适合：**

- 单个、简单的信号
- 非平稳信号（chirp、Gaussian pulse）
- 需要精确时频变化的应用

**不适合：**

- 多分量信号
- 有大量频率成分
- 噪声环境
- 需要干净图像的应用

| 方法          | 优点                     | 缺点                 |
| ------------- | ------------------------ | -------------------- |
| **WVD**       | 时频分辨率最高、能量守恒 | 交叉项严重           |
| **STFT**      | 无交叉项、简单           | 分辨率差             |
| **Wavelet**   | 多尺度好、无交叉项       | 分辨率随尺度变化     |
| **PWVD/SWVD** | 平衡交叉项与分辨率       | 需要选择合适平滑函数 |



## 9 Z-transform 与 Perfect Reconstruction（PR）

### 9.1 Perfect Reconstruction

**Perfect Reconstruction（完美重构）就是：输出信号 = 输入信号 × 纯延时（不失真）。**

数学上写成：
$$
\hat X(z) = z^{-l} X(z)
$$
![image-20251205022152186](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251205022152186.png)



### 9.2 Z-transform

z-transform 的目的：

- 把序列写成函数 H(z) 或 X(z)
- 方便用多项式的方式表达滤波器位置和性质

例如 Haar 低通滤波器：
 h₀ = [1/√2, 1/√2] → H₀(z) = 1/√2 (1 + z⁻¹)

在滤波器组中（第 12–14 页），重构结果为：
$$
\hat X(z) = 
\frac{1}{2}\big(G_0(z)H_0(z)+G_1(z)H_1(z)\big)X(z)
+
\frac{1}{2}\big(G_0(z)H_0(-z)+G_1(z)H_1(-z)\big)X(-z)
$$
为了完美重构：

**条件 1（消混叠 alias cancellation）**
$$
G_0(z)H_0(-z)+G_1(z)H_1(-z)=0
$$
**条件 2（幅度条件）**
$$
G_0(z)H_0(z)+G_1(z)H_1(z)= 2z^{-l}
$$
这样最终信号 = 原信号 ×（延时）



## 10 Daubechies 小波

### 10.1 设计步骤

1. **设计一个 product filter（乘积滤波器）P₀(z）**

要求满足：
$$
P_0(z) - P_0(-z) = 2z^{-l}
$$
这是 **Perfect Reconstruction（PR）条件 2** 的要求（消除失真）。
 这个式子保证重构时：

- 系统的总响应是一个纯延时
- 没有额外的变形

P₀(z) 不是实际滤波器，只是一个**设计中间量**。



2. **把 P₀(z) 分解成两个低通滤波器**

## 

$$
P_0(z)=H_0(z)G_0(z)
$$

H₀(z) = 分析低通滤波器
 G₀(z) = 合成低通滤波器

> 小波的关键是：
>  **只要构造好 H₀(z)，其它 H₁(z)、G₀(z)、G₁(z) 都能自动得到。**

这就是小波滤波器组的重要特性。



3. **Daubechies 小波的 H₀(z) 和 G₀(z) 必须满足：**

- 正交性

- 完美重构

- k 个消失矩

- 滤波器长度最短（仅 2k taps）

- 最小相位条件（零点都在单位圆内）



4. **最终得到的形式是**
   $$
   H_0(z) = (1+z^{-1})^k \prod_{i=1}^{k-1}(z_i - z^{-1})
   $$

   $$
   G_0(z) = (1+z^{-1})^k \prod_{i=1}^{k-1}\left(\frac{1}{z_i} - z^{-1}\right)
   $$

   

   zᵢ 和 1/zᵢ 为某多项式的根，一定成对出现。



### 10.2 性质

- **k = 1时：**

$$
H_0(z)=G_0(z)=1+z^{-1}
$$

这就是 **Haar 小波的低通滤波器**（未归一化）。



- **k = 2 时：**

![image-20251205120705904](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251205120705904.png)



### 10.3 Orthogonal Filter Banks（正交滤波器组）

如下所示：
$$
\sum_n h_i[n-2k]\; h_i[n]=\delta(k)
$$

$$
\sum_n h_i[n-2k]\; h_l[n]=0, \quad i\neq l
$$

**即同一个滤波器与自身在 2k 移位之后是正交的**



**不同滤波器之间也是正交的**
$$
\langle h_i[n], h_l[n-2k] \rangle = 0,\; i \neq l.
$$
例如：

低通 h₀ 与高通 h₁ 正交。

这保证：

> **分解后的低频子带和高频子带互不干扰（energy decorrelation）。**



**应用：**
$$
H_1(z)=(-z)^{-N}H_0(-z^{-1})
$$
**也就是：**
$$
h_1[n] = (-1)^n\; h_0[N-n]
$$


