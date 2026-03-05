## 5.1 Basic concepts

**Self-information (自信息、单个事件的信息量)**

![image-20251108010000003](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108010000003.png)

![image-20251108010038110](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108010038110.png)

![image-20251108010106099](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108010106099.png)

![image-20251108010114576](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108010114576.png)

![image-20251108010142078](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108010142078.png)

![image-20251108010235791](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108010235791.png)

## 5.2 Digital pulse amplitude modulation（数字脉冲幅度调制）

### 1 PAM的概念

在数字通信中，我们可能需要用**M种不同波形**来表示不同的信息符号。

如果要表示 $k$ 个二进制位（bits），则：
$$
M = 2^k \quad \text{或} \quad k = \log_2 M
$$
比如：

- 2进制（M=2） → 每个符号1 bit
- 4进制（M=4） → 每个符号2 bits

**Pulse amplitude modulation (PAM, 脉冲幅度调制 )** ,所有波形形状 **相同**，但**幅度不同**。

数学表达：
$$
s_m(t) = A_m g(t)
$$
其中：

- $g(t)$：固定的脉冲形状（pulse shape）
- $A_m$：不同的幅度，对应不同符号

![image-20251108013659889](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108013659889.png)

**脉冲成形滤波器（pulse shaping filter，脉冲成形滤波器）**

- 时域函数：$g(t)$
- 决定信号的**脉冲形状**
- 控制信号的**带宽**和**码间干扰（ISI）**
- 例如矩形脉冲、升余弦（raised cosine）脉冲等都可以作为 $g(t)$

**频谱成形滤波器（spectrum shaping filter，频谱成形滤波器）**

- 频域函数：$G(f)$
- 决定信号的**功率谱分布**
- 通过选择合适的 $G(f)$，可以控制信号带宽，减少带外干扰。

![image-20251108013915307](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108013915307.png)



### 2 NRZcode(不归零码)和RZcode(归零码)

很简单，如下![image-20251108014414056](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108014414056.png)

![image-20251108014429401](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108014429401.png)

![image-20251108014443899](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108014443899.png)

![image-20251108014504462](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108014504462.png)

![image-20251108014511425](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108014511425.png)

### 3 差分编码

**差分编码的核心思想**：用“相邻符号是否变化”来表示 0 或 1。

- 如果当前符号和前一个相同 → 表示 0
- 如果当前符号和前一个不同 → 表示 1

![image-20251108014021562](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108014021562.png)

即$b_n$和$d_n$列往左上角连线，不同输出1，相同输出0。$d_n$第一个固定为0。

### 4 The PSD of baseband PAM signals 

### 1**PAM（脉冲幅度调制，Pulse Amplitude Modulation）信号的功率谱密度（Power Spectral Density, PSD）** 的一般形式：


$$
P_s(f) = P_d(f)|G_T(f)|^2 = \frac{1}{T_s} P_a(f)|G_T(f)|^2
$$


| 符号     | 含义                                                   |
| -------- | ------------------------------------------------------ |
| $s(t)$   | PAM信号（调制后的时间信号）                            |
| $P_s(f)$ | PAM信号的**功率谱密度（Power Spectral Density, PSD）** |
| $P_d(f)$ | 经过抽样后的**离散信号的功率谱密度**                   |
| $P_a(f)$ | 采样序列 $\{a_n\}$ 的功率谱密度（由符号序列决定）      |
| $G_T(f)$ | 传输脉冲 $g_T(t)$ 的频谱（即脉冲形状的傅里叶变换）     |
| $T_s$    | 采样周期（即相邻符号的间隔时间）                       |

这里，$P_a(f)$可以通过$R_a(m)$的傅里叶变换得到。

### 2 在{$a_n$}是不相关序列条件下信号的**功率谱密度**：

$$
P_s(f) = \frac{\sigma_a^2}{T_s} |G(f)|^2 + \frac{m_a^2}{T_s^2} \sum_{m=-\infty}^{\infty} \left| G_T\left( \frac{m}{T_s} \right) \right|^2 \delta \left( f - \frac{m}{T_s} \right)
$$

| 符号                          | 含义                                        |
| --------------------------- | ----------------------------------------- |
| $P_s(f)$                    | PAM信号 $s(t)$ 的**功率谱密度（PSD）**              |
| $\sigma_a^2$                | 码元序列 $\{a_n\}$ 的**方差**，即符号的随机波动能量         |
| $m_a$                       | 码元序列 $\{a_n\}$ 的**均值**，即平均值（若信号含直流分量）     |
| $T_s$                       | 码元持续时间（符号周期）                              |
| $G(f)$、$G_T(f)$             | 脉冲波形 $g_T(t)$ 的傅里叶变换（频谱）                  |
| $\delta(f - \frac{m}{T_s})$ | 狄拉克δ函数，表示在 $f = m/T_s$ 处的离散频谱线（周期抽样产生的谱线） |
| $m$                         | 整数，表示离散谱线的序号（对应频率倍数）                      |

### 3 常用脉冲波形的傅里叶变换

**sinc函数：**
$$
\mathrm{sinc}(x) = \frac{\sin(\pi x)}{\pi x}
$$
**不归零矩形脉冲（NRZ）：**
$$
\boxed{
\begin{cases}
g_{\text{NRZ}}(t)=A\,\mathrm{rect}\!\left(\dfrac{t}{T_s}-\dfrac12\right) \\[4pt]
G_{\text{NRZ}}(f)=A T_s\,\mathrm{sinc}(fT_s)\,e^{-j\pi fT_s}
\end{cases}}
$$
**归零矩形脉冲（RZ）：**
$$
\boxed{
\begin{cases}
g_{\text{RZ}}(t)=A\,\mathrm{rect}\!\left(\dfrac{t}{\tau}-\dfrac12\right) \\[4pt]
G_{\text{RZ}}(f)=A \tau\,\mathrm{sinc}(f\tau)\,e^{-j\pi f\tau}
\end{cases}}
$$

## 5.3 BER分析（还需研究）
BER指在分析中鉴别错误的概率。

发送端发出两种可能的信号 $s_1(t)$ 或 $s_2(t)$（对应 2PAM 的两个幅度 $A_1, A_2$）。

接收端的信号为：
$$
r(t) = s_i(t) + n_w(t)
$$
其中 $n_w(t)$ 是加性高斯白噪声（AGWN）。

接下来信号经过 **匹配滤波器**（matched filter），在符号末端 $t_0$ 取样得到一个随机变量：
$$
y = \text{matched filter output at } t_0
$$
加入 AWGN 后：
$$
y = A_i + n
$$
其中 $n \sim \mathcal{N}(0,\sigma^2)$

因此：

- 当发送 $s_1$ 时，$y$ 是以 $A_1$ 为均值的高斯分布
- 当发送 $s_2$ 时，$y$ 是以 $A_2$ 为均值的高斯分布

于是两种情况会有重叠 → **判决不能完全正确，会出现误码**。

为了根据 $y$ 判断发送的是 $s_1$ 还是 $s_2$，需要设一个门限：
$$
\begin{cases}
y > V_T \Rightarrow 判决为 s_1 \\
y < V_T \Rightarrow 判决为 s_2
\end{cases}
$$
等价于：

- 大信号 → 判为 $s_1$
- 小信号 → 判为 $s_2$

对于 2PAM，一般最佳门限是两个幅度的中点：
$$
V_T = \frac{A_1 + A_2}{2}
$$
**误码概率**定义为：
$$
P_e = P(\text{判决结果与实际发送的不一致})
$$
因为发送 $s_1$ 和 $s_2$ 的概率可能不一样，因此：
$$
P_e = P(s_1) P(e|s_1) + P(s_2) P(e|s_2)
$$


![image-20251209071618809](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251209071618809.png)

如图，$P(s_1)$即是门限左边的红色部分，$P(s_2)$即是门限右边的部分。

![image-20251209074207496](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251209074207496.png)



标准高斯分布 PDF：
$$
f(z)=\frac{1}{\sqrt{2\pi}} e^{-z^2/2}
$$
它的尾概率：
$$
P(Z>a)=\int_a^{\infty} \frac{1}{\sqrt{2\pi}}e^{-z^2/2}dz,
$$
这个积分 **没有初等函数** 的解析形式 ——
 数学界证明这是无法用多项式、指数、对数、三角函数等表示的。

因此定义了一个新函数来表示它：

误差函数：
$$
\operatorname{erf}(x)=\frac{2}{\sqrt{\pi}}\int_0^x e^{-t^2}dt
$$
互补误差函数：
$$
\operatorname{erfc}(x)=1-\operatorname{erf}(x)
=\frac{2}{\sqrt{\pi}}\int_x^\infty e^{-t^2}dt
$$
你看，erfc **直接就是高斯尾概率的定义形式**。

所以：

> **只要问题涉及高斯变量的尾概率，最终必然出现 erfc 或 Q 函数。**

**将 BPSK 的误码积分变换到 erfc 形式**时：

出错概率：
$$
P(e\mid s_1)
  = P\left(y<0\mid s_1\right)
$$
标准化为高斯变量：
$$
z=\frac{y-E_b}{\sigma}
$$
于是：
$$
P(e\mid s_1)=P\left(Z < -\sqrt{\frac{2E_b}{N_0}}\right)
$$
高斯对称性：
$$
P(Z<-a)=P(Z>a)=Q(a)
$$
利用
$$
Q(x)=\frac12\operatorname{erfc}\left(\frac{x}{\sqrt2}\right),
$$
得到：
$$
P_e=\frac12 \operatorname{erfc}\left(\sqrt{\frac{E_b}{N_0}}\right)
$$


## 5.4 带限信道上的PAM信号传输

我们要做到每个波形符号时域不交叠（The waveforms are non-overlapping in time），即互不干扰。但一般时域受限制则频域不受限，频域受限制则时域不受限。这里我们就需要奈奎斯特准则。

**接收滤波器输出采样值的构成分析如下：**

![image-20251121164836264](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251121164836264.png)

![image-20251121164856497](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251121164856497.png)

当我们发送整个序列时，在**特定采样点没有重叠，即没有下图红色部分，就是没有ISI。**

如果我们要做到没有ISI，就必须要符合**奈奎斯特准则**，即：

**在时域上：**![image-20251122202936845](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251122202936845.png)

**在频域上：![image-20251122203021169](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251122203021169.png)**

即频域上**所有以 $1/T_s$ 间隔搬移的 X(f) 加起来，在任意 f 的总和必须恒为 1。**

可以看出，在最理想的条件下，即用**理想低通滤波器**，也必须满足**奈奎斯特极限**。

**理想低通滤波器：![image-20251122203521047](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251122203521047.png)**

**奈奎斯特极限：**![image-20251122203550788](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251122203550788.png)

**但是**，奈奎斯特极限不可实现：![image-20251122203711354](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251122203711354.png)

![image-20251122203722390](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251122203722390.png)

所以我们一般使用的PAM是**滚降函数**：![image-20251122203818366](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251122203818366.png)

![image-20251122203850036](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251122203850036.png)

![image-20251122203904528](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251122203904528.png)

这里$R_s$和$W$计算中有"2"相关的是由**奈奎斯特极限**推出的

## 5.5 Optimal baseband systems（最佳基带系统）

![image-20251122205520678](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251122205520678.png)

我们需要，满足两个条件：

**条件一：采样点无ISI：**

我们希望采样点处：
$$
G_T(f)\, C(f)\, G_R(f) = X_{rcos}(f)
$$
其中：

- $X_{rcos}(f)$：满足 Nyquist 第一准则的 **Raised Cosine（RC）滤波器频响**

换句话说：

- **整个系统的等效脉冲响应必须是升余弦（RC）脉冲，才能保证采样无ISI。**

**条件二：采样点 SNR 最大（匹配滤波器）**

理论通信里，接收滤波器若要在白噪声下获得 **最大采样 SNR**，必须使用：
$$
g_R(t) = g_T(-t)
$$
即接收滤波器必须使用 **匹配滤波器**（Matched Filter）。

在频域即：
$$
G_R(f) = G_T^*(f)
$$
因此，我们要做到：
$$
\boxed{
G_T(f) = G_R(f) = \sqrt{X_{rcos}(f)}
}
$$
这就是我们需要的**Root Raised Cosine（RRC，根升余弦）滤波器**

当我们采用**根升余弦滚降**时：![image-20251122210249260](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251122210249260.png)

![image-20251122210312224](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251122210312224.png)

## 5.6 Eye pattern（眼图）

![屏幕截图 2025-11-22 202501](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-11-22%20202501.png)

## 5.7 信道均衡

![image-20251122210856509](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251122210856509.png)

![image-20251122210907096](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251122210907096.png)

