> 何威翰，编辑于2025/12/4
## 5 从STFT到Haar
### 5.1 时间-频率分析

传统 **傅里叶变换（FT）** 能告诉你：“信号里包含哪些频率”， 但 **不能告诉你这些频率在什么时候出现**。

给信号加一个“时间窗口”，对窗口内的信号做傅里叶变换，移动窗口，就能得到：

- 某一段时间内**有哪些频率**（频率局部化）
- 一个整体的**时频图（spectrogram）**

即为**短时傅里叶变换（STFT）**。

给信号加一个“时间窗口”，对窗口内的信号做傅里叶变换，移动窗口，就能得到：

- 某一段时间内**有哪些频率**（频率局部化）
- 一个整体的**时频图（spectrogram）**

但窗口的宽度会产生影响：

● **窗口宽 → 时间分辨率差 / 频率分辨率好**

因为窗口长，可以看到很多周期，频率估计准，但不知道它发生的具体时间。

● **窗口窄 → 时间分辨率好 / 频率分辨率差**

因为窗口短，只能看到信号的一小段，不足以准确分辨频率。

所以，时间不确定度 Δt 与频率不确定度 Δω 的乘积不能任意小：

![image-20251203180739668](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203180739668.png)

**只有高斯函数同时达到最小的不确定性（等号成立）**



### 5.2 短时傅里叶变换

将信号分成若干小时间片（通过窗口函数实现），认为在这一小段时间内信号“近似平稳”，然后对这段做傅里叶变换。即为STFT。

 **STFT 的数学表达式：**
$$
STFT(t,\omega) = \int_{-\infty}^{\infty} s(\tau)\, \gamma^*(\tau - t)\, e^{-j\omega \tau}\, d\tau
$$
含义：

- $\gamma(\tau-t)$：以 t 为中心的窗口

- STFT 先用窗口截取信号、再对其做 FT

- 结果是 **一个二维函数**：
  - 时间 t
  - 频率 ω

    

通常我们绘制：
$$
|STFT(t,\omega)|^2
$$
——这称为 **Spectrogram**（谱图）

这是一个**时间 × 频率**二维图，每个点表示该时间该频率处的能量

![image-20251203181110357](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203181110357.png)

在实际运算中，我们必须要**符合COLA（Constant Overlap-Add）条件：**各窗口叠加后必须得到常数（不会有空洞或过度叠加造成失真）



### 5.3 Gabor变换

**Gabor Transform 是 STFT 的离散版本，并且使用 Gaussian（高斯）作为窗口函数。**

Gabor 变换的结果是把信号表示成：

- 时间
- 频率

两个维度的函数，就像一张时间–频谱图。

并且它将信号展开成一系列“基本函数”的和：
$$
s(t)=\sum_{m=-\infty}^{\infty}\sum_{n=-\infty}^{\infty}
c_{m,n}\,h_{m,n}(t)
$$
其中：

- $h_{m,n}(t)$：Gabor 基函数
   = **高斯窗口** $h(t-mT)$ → 时间平移
   × **复指数** $e^{jn\Omega t}$ → 频率平移
- $c_{m,n}$：系数（类似傅里叶系数）

所有 Gabor 基都是一个高斯信号 h(t) 的：

- 时间平移：0, T, 2T, …
- 频率调制：0, Ω, 2Ω, …

![image-20251203181603858](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203181603858.png)

每个基函数 $h_{m,n}$ 对应在(t, ω) 平面中的一个小圆（一个区域），其中心在：
$$
(t = mT,\ \omega = n\Omega)
$$
![image-20251203181626303](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203181626303.png)

采样里我们必须要满足关键约束：
$$
T\Omega \le 2\pi
$$
有三种采样情况：

- Oversampling（过采样）：TΩ < 2π

  - 基函数更密集

  - 可以构成 Gabor Frame（完备，可重构）

  - 有很好时间–频率定位

  - 高斯窗口效果最佳

- Critical sampling（临界采样）：TΩ = 2π
  - 基函数数量 = 信号采样点数
  - 可以做到正交（或接近）
  - 但时间–频率定位变差
  - 重构变得困难

- Undersampling（欠采样）：TΩ > 2π
  - 无法构成 frame
  - 信息不足以重建信号
  - 类似于“低于奈奎斯特频率采样”



Gabor 系数计算方法：
$$
c_{m,n}=\int s(t)\gamma^*(t-mT)e^{-jn\Omega t} dt
$$
也就是说，它等价于对信号做 **STFT 在点 (mT, nΩ) 的采样**：
$$
c_{m,n} = STFT(mT, n\Omega)
$$
重构时需要一个“合成窗口” γ(t)，它与分析窗口 h(t) 一般不相同，需要满足“对偶基”（biorthogonality），如：
$$
\langle \gamma_{m,n}, h_{m',n'} \rangle = \delta_{mm'}\delta_{nn'}
$$


### 5.4 Haar函数

每个小波系统包含两类核心函数：

**✔（1）Scaling function（尺度函数） φ**

定义于区间 $[0,1]$ 为矩形脉冲：
$$
\phi(x)=
\begin{cases}
1, & 0\le x<1 \\
0, & \text{otherwise}
\end{cases}
$$
它的缩放和平移形式：
$$
\phi_{j,k}(x)=\phi(2^j x - k)
$$
代表“低频”或“平均值”。

------

**✔（2）Wavelet function（小波函数） ψ**

母小波（mother wavelet）ψ₀₀ 是“+1 → –1”的阶梯矩形函数：
$$
\psi(x)=
\begin{cases}
1, & 0\le x<\frac12 \\
-1, & \frac12\le x<1 \\
0, & \text{otherwise}
\end{cases}
$$
缩放和平移得到 daughter wavelets：
$$
\psi_{j,k}(x)=\psi(2^j x - k)
$$
![image-20251203182710835](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203182710835.png)

![image-20251203182717667](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203182717667.png)

随着 j 变大，函数变得更“窄”，频率更高；随着 k 变化，窗口在时间上移动

![image-20251203182746407](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203182746407.png)

**所有 Haar 函数之间都正交**。



**Haar 函数的两个性质：**

1. **Two-scale Relation（双尺度关系）**

**尺度函数 φ 和小波 ψ 都可以用更细尺度的 φ 表示**：
$$
\phi(x)=\phi(2x)+\phi(2x-1)
$$
![image-20251203183042780](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203183042780.png)

2. **线性分段逼近（piecewise linear approximation）**

Haar 函数能近似任何连续函数：

- φ 系列用于“平均值”
- ψ 系列用于“细节 / 差分”

![image-20251203183127813](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203183127813.png)



### 5.5 Haar变换

Haar 变换就是：**用 Haar 小波作为基，将信号展开为低频 + 多级高频分量**

最小 **标准化**Haar 2×2 变换矩阵：
$$
H_2=\frac{1}{\sqrt{2}}
\begin{bmatrix}
1 & 1 \\
1 & -1
\end{bmatrix}
$$
它的两行分别代表：

- 平均值（low frequency）
- 差值（high frequency）

对应图中的 φ₀₀ 和 ψ₀₀。

![image-20251203184053255](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203184053255.png)

同理，4×4：![image-20251203184242354](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203184242354.png)

8×8：![image-20251203184304026](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203184304026.png)

![image-20251203184316705](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203184316705.png)

- 第 1 行：全 1（求平均值）
- 第 2 行：半正半负（低频）
- 第 3–4 行：中频
- 第 5–8 行：高频



**Haar 变换与 DCT 的比较**

- DCT 每一行是不同频率的余弦波
- Haar 行也代表不同频率，但**同时具有“时间局部性”（translation）**因而 Haar 能捕捉：不同时间发生的短时事件（time-localized features），这是 DCT 无法做到的。



**Haar的作用**

1. **特征提取 Feature Extraction** Haar 能在非平稳信号中找到 **什么时候** 出现特定特征（短脉冲）。

2. **压缩 Image/Signal Compression**Haar 是**有损压缩**，但压缩率高且计算简单，高频系数通常代表“细节/噪声”，可以阈值切除。

3. **去噪 Denoising**Haar 是“差值型”的基，对噪声敏感，适合用 thresholding 消除噪声。

   

**Haar 变换的逆变换**

因为 Haar 矩阵是 **正交矩阵**（归一化后）：
$$
H^{-1}=H^T
$$
![image-20251203184543405](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203184543405.png)



**总结**

- 我们已经看到，可以通过构造Haar矩阵来直接执行Haar变换。
- Haar变换速度快，因为该矩阵包含大量零项且为实数矩阵（不含复数项）。
- 它可用于识别待分析信号中的**频率分量 frequency components** （精细细节）。
- 它可用于识别**输入数据中的趋势 the trends in the input data**（近似值）。
- 可通过削减或消除信号中高频对应**系数 compression**，再逆变换来实现压缩。

![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/20251230160627218.png)
