## 2.1 Commonly used signals
### 1狄拉克冲激函数及其性质
![84c04352744a724291deec109c588bce](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/84c04352744a724291deec109c588bce.png)

![07356bd68545ce69745fd27bf7d5c4b8](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/07356bd68545ce69745fd27bf7d5c4b8.png)

### 2 rec函数性质

其中，rect 是 **矩形函数**（rectangular function）的缩写

矩形函数通常使用如下符号表示：
$$
\text{rect}(t) = 
\begin{cases}
1, & \text{if } |t| \leq \frac{1}{2} \\
0, & \text{if } |t| > \frac{1}{2}
\end{cases}
$$
$\text{rect}\left(\frac{t}{T}\right)$ 表示一个宽度为 $T$，中心在 0 处的矩形函数。其值为 1 当 $-\frac{T}{2} \leq t \leq \frac{T}{2}$，否则为 0。

同时，矩形冲激信号（Rectangle Impulse Signal）是一个在特定时间区间内具有常数幅度的信号，并且在其他时间点为零。它通常在时域中表示为一个矩形脉冲，并且可以用**单位矩形函数**来描述。

矩形冲激信号可以通过如下函数表示：
$$
\text{rect}(t/T) = 
\begin{cases} 
1, & |t| \leq \frac{T}{2} \\
0, & |t| > \frac{T}{2}
\end{cases}
$$
其中：

- $T$ 是矩形信号的宽度。
- $t$ 是时间变量。
- 矩形信号在时间 $t \in \left[-\frac{T}{2}, \frac{T}{2}\right]$ 范围内的幅度为 1，在其余时间范围内为 0。

### 3 sinc函数性质

**sinc 函数**在通信原理中如下：
$$
\text{sinc}(x) = \frac{\sin(x)}{x}
$$
sinc 函数与矩形函数之间有着密切的关系。矩形函数在时域的傅里叶变换结果就是 sinc 函数。例如，一个宽度为 $T$ 的矩形函数的傅里叶变换是：
$$
\mathcal{F}\left[\text{rect}\left(\frac{t}{T}\right)\right] = T \cdot \text{sinc}(fT)
$$

### 4 复函数性质

![89247dd3a57455c412bf6f9f2f46edb4](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/89247dd3a57455c412bf6f9f2f46edb4.png)

## 2.2 Energy and power

### 1 信号的功率

**瞬时功率 (Instantaneous Power)**：

- 电压信号 $s(t)$ 的瞬时功率是 $s^2(t)$，即信号幅度的平方。

- 公式：
  $$
  \text{瞬时功率} = s^2(t)
  $$

这表示在某一时刻 $t$，信号 $s(t)$ 的功率是该信号幅度的平方。

**时间平均功率 (Time Average Power)**：

- 时间平均功率 $P_s$ 是信号 $s(t)$ 在一段时间内的平均功率，定义为：
  $$
  P_s = \lim_{T \to \infty} \frac{1}{T} \int_{-T/2}^{T/2} s^2(t) \, dt
  $$

这是对信号 $s(t)$ 在时间区间 $[-T/2, T/2]$ 内平方的积分的平均值。随着 $T$ 趋向无穷大，计算得出时间平均功率。

**信号 $y(t)$ 是信号 $s(t)$ 的缩放版本**：
$$
y(t) = K \cdot s(t)
$$
则其功率变为：
$$
P_y = K^2 \cdot P_s
$$
这意味着信号幅度的平方比例决定了功率的变化。

**信号 $y(t)$ 是信号 $s(t)$ 的延迟版本**：
$$
y(t) = s(t - t_0)
$$
则其功率与原信号相同：
$$
P_y = P_s
$$
延迟不会影响信号的功率。

### 2 信号的总能量

**在一个足够小的时间间隔内的能量**：

- 如果我们考虑一个信号 $s(t)$ 在一个足够小的时间间隔 $[t, t + \Delta]$ 内的能量，这个能量可以通过信号幅度的平方与时间间隔的乘积来表示：

$$
\text{能量} = s^2(t) \Delta
$$

这表示在时间 $t$ 处，信号的能量是 $s^2(t)$ 与时间间隔 $\Delta$ 的乘积。

- 对于整个时间范围内的能量，信号的总能量 $E_s$ 是其幅度平方的积分，即：

$$
E_s = \int_{-\infty}^{\infty} s^2(t) \, dt
$$

或者通过极限的方式表示为：
$$
E_s = \lim_{T \to \infty} \int_{-T/2}^{T/2} s^2(t) \, dt
$$
这表示对信号 $s(t)$ 在整个时间范围内的能量进行计算，即对 $s(t)$ 的平方进行积分，得到信号的总能量。

**如果信号 $y(t)$ 是信号 $s(t)$ 的缩放版本：**
$$
y(t) = K \cdot s(t), \quad E_y = K^2 \cdot E_s
$$
这意味着缩放系数 $K$ 会影响信号的能量，信号的能量与 $K^2$ 成正比。

**如果信号 $y(t)$ 是信号 $s(t)$ 的延迟版本：**
$$
y(t) = s(t - t_0), \quad E_y = E_s
$$
延迟 $t_0$ 不会改变信号的总能量，能量保持不变。

### 3 复信号的功率和能量

![image-20251104211840272](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251104211840272.png)

### 4 Energy limited signal & power limited signal

![image-20251104211901655](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251104211901655.png)

## 2.3 Spectral density and correlation function

### 1 傅里叶级数（略）

![image-20251104234607741](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251104234607741.png)

### 2 傅里叶变换的定义

![image-20251104234702021](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251104234702021.png)

### 3 傅里叶变换的性质

![image-20251104234717869](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251104234717869.png)

![image-20251104234726585](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251104234726585.png)

![image-20251104235535612](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251104235535612.png)

**关于位移**：“频反时同”

### 4 常用函数的傅里叶变换

![image-20251104234938863](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251104234938863.png)

### 5 帕塞瓦尔定理

帕尔塞瓦尔定理指出，时间域信号的能量等于其频率域信号的能量。也就是：
$$
E_x = \int_{-\infty}^{\infty} |x(t)|^2 \, dt = \int_{-\infty}^{\infty} |X(f)|^2 \, df
$$
这表明信号的能量可以从时间域转化为频率域。

### 6 能量谱密度 (Energy Spectral Density, ESD)

**能量谱密度** $E_x(f)$ 描述了信号 $x(t)$ 在不同频率 $f$ 上的能量分布。它可以通过信号的频域表示 $X(f)$ 的幅度的平方得到：
$$
E_x(f) = |X(f)|^2
$$
这表示信号在频域中每个频率分量的能量密度。

信号的**总能量** $E_x$ 可以通过对频域上各频率分量的能量谱密度 $E_x(f)$ 进行积分来计算：
$$
E_x = \int_{-\infty}^{\infty} E_x(f) \, df
$$
这表明总能量是频域中所有频率分量能量的总和。

**自相关函数定义**：
 对于一个能量信号 $x(t)$，自相关函数 $R_x(\tau)$ 描述了信号与其自身在不同时间延迟 $\tau$ 下的相关性。其数学表达式为：
$$
R_x(\tau) = \langle x(t + \tau), x(t) \rangle = \int_{-\infty}^{\infty} x(t + \tau) x^*(t) \, dt
$$
其中，$\tau$ 是时间延迟，$x^*(t)$ 是信号 $x(t)$ 的复共轭。

![image-20251105004653372](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105004653372.png)

**能量信号的自相关函数$R_x(\tau)$和能量谱密度 $E_x(f)$ 是一对傅立叶变换**



**信号之和的能量**：

![image-20251105011944042](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105011944042.png)

**Exy 是 x(t) 和 y(t) 的互能量**:

- 互能量 $E_{xy}$ 定义为：
  $$
  E_{xy} = \int_{-\infty}^{\infty} x(t) y^*(t) dt = \int_{-\infty}^{\infty} X(f) Y^*(f) df
  $$

这里 $x(t)$ 和 $y(t)$ 是时间域信号，而 $X(f)$ 和 $Y(f)$ 是它们对应的频域信号。

**Exy(f) 是 Exy 在频域上的分布密度**:

- 互能量的频谱密度表示为 $E_{xy}(f) = X(f) Y^*(f)$，它反映了信号在频域上的能量分布。

同理：![image-20251105144338788](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105144338788.png)

**互相关函数的定义和性质：**

![image-20251105144450168](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105144450168.png)

**11 归一化相关系数(Normalized correlation coefficient)：**

![image-20251105144618272](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105144618272.png)

### 7 功率谱密度（Power spectral density ，PSD)）

**考虑功率信号时，唯一的差别是多了个时间平均：**$\lim_{T \to \infty} \frac{1}{T}$

**具体计算类似能量谱密度**

![image-20251105145822454](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105145822454.png)

![image-20251105145831667](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105145831667.png)

![image-20251105145945382](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105145945382.png)

### 8 单边谱密度（Single-side spectral density）

**复数表示的旋转运动**：v

- 图左侧给出了复数 $z = x + iy$ 的表示，描述了平面上旋转运动的参数化。
- 其中 $x = r \cos \varphi$ 和 $y = r \sin \varphi$， $\varphi = \omega t$ 是角度，$r$ 是幅值。
- 这部分展示了 $x$ 和 $y$ 如何随着时间变化，形成圆形的轨迹。

**单边 PSD（Single-side PSD）**：

- 右边的公式表示了单边谱密度：
  $$
  P_x^{SS}(f) = P_x(f) + P_x(-f)
  $$

- 这个公式的意思是，单边谱密度是双边谱密度 $P_x(f)$ 和 $P_x(-f)$ 的和。

**实信号的 PSD**：

- 对于实信号，谱密度在 $f > 0$ 时是双倍的，即 $P_x^{SS}(f) = 2P_x(f)$。

- 对于负频率 $f < 0$，谱密度为 0。

- 因此，单边谱密度为：
  $$
  P_x = \int_{-\infty}^{\infty} P_x(f) df = \int_0^\infty P_x^{SS}(f) df
  $$

**图示**：

下图展示了双边 PSD 和单边 PSD 的示意图。

- 双边 PSD：具有正频率和负频率两个部分，频谱对称。
- 单边 PSD：只展示正频率部分，能量集中在正频率上。



### 9 带宽

**常用的五种[[带宽]]如下图：**

![image-20251105151520887](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105151520887.png)

![image-20251105151528410](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105151528410.png)

其中，**3dB 带宽** $B_{3dB}$ 定义为信号功率下降到最大功率一半时的频率范围。具体来说，当功率谱密度 $P_x(f)$ 的值下降至最大值的一半时，对应的频率点即为 3dB 带宽。

**等效矩形带宽 $B_{Eq}$** 是通过矩形形状的频谱来近似描述实际信号的带宽。其满足以下关系：
$$
B_{Eq} \times |P_x(f)|_{\text{max}} = P_x
$$
这里，$P_x$ 是信号的总功率，$B_{Eq}$ 是与其匹配的矩形频谱的带宽

![image-20251105151539322](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105151539322.png)

**x% 能量占比带宽** $B_{x\%}$ 是一个频率范围，其中信号的能量总量占信号总能量的 x%。

该带宽满足以下关系：
$$
\int_0^{B_{x\%}} P_x(f) \, df = x\% \cdot P_x
$$
其中 $P_x(f)$ 是信号在频域的功率谱密度，$P_x$ 是信号的总功率。

在带宽的常见计算中，我们通常只关心 **正频率部分**，因为它代表了信号的实际能量分布。

## 2.4 线性时不变系统

### 1 介绍

满足以下两个条件：

![image-20251105153549433](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105153549433.png)

 

### 2 传递函数（Transfer Function）

![image-20251105170242030](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105170242030.png)

当输入信号为单位脉冲信号 $\delta(t)$ 时，系统的输出为 **脉冲响应** $h(t)$。脉冲响应表示了系统对单位脉冲输入的响应。对于一个 LTI 系统，脉冲响应和传递函数 $H(f)$ 之间的关系为：

### 3 脉冲响应

$$
h(t) \xleftrightarrow{\mathcal{F}} H(f)
$$

这里，$h(t)$ 是时域上的脉冲响应，$H(f)$ 是频域上的传递函数。

![image-20251105170457591](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105170457591.png)





### 4 系统的频域响应的输出信号

输入信号 $x(t)$ 经过系统的传递函数 $H(f)$ 后，输出信号 $y(t)$ 的频域表示为：
$$
Y(f) = X(f) H(f)
$$
其中，$X(f)$ 是输入信号 $x(t)$ 的频域表示，$H(f)$ 是系统的频域传递函数。

从频域转换到时域，输出信号 $y(t)$ 可以表示为：
$$
y(t) = \int_{-\infty}^{\infty} X(f) H(f) e^{j 2 \pi f t} df
$$
这是 **卷积** 形式的表达式。实际信号的输出是输入信号与系统脉冲响应的卷积：
$$
y(t) = \int_{-\infty}^{\infty} x(t + \tau) h(-\tau) d\tau
$$
这说明，输出信号 $y(t)$ 是输入信号 $x(t)$ 和系统脉冲响应 $h(t)$ 的 **卷积**。换句话说，系统对输入信号的响应是通过卷积计算的：
$$
y(t) = x(t) * h(t)
$$
其中，$*$ 表示卷积操作。

![image-20251105173549789](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105173549789.png)

### 5 The ESD/PSD of output $y(t)$ 

![image-20251105173649325](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105173649325.png)

### 6 Some special cases of inputs

![image-20251105173750727](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105173750727.png)

### 7 部分理想基带滤波器（Ideal baseband filter）

![image-20251105173944811](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105173944811.png)

![image-20251105174015150](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105174015150.png)

## 2.5 带通信号与带通系统 Bandpass signal and bandpass system

### 1 介绍

在通信系统中，信号通常在载波频率 $f_c$ 周围进行调制。这时，信号的频谱是围绕 $f_c$ 的高频带宽，直接处理这样的信号比较复杂。**等效基带表示**通过对信号进行频移，使其将频谱平移到以零为中心的频带，即**复包络信号**，从而简化分析和处理。

![image-20251105174704292](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105174704292.png)

### 2 希尔伯特变换 Hilbert transform

希尔伯特变换（Hilbert Transform）是一种信号处理技术，用来构造一个信号的**解析信号（analytic signal）**。它的作用是将一个实信号 $x(t)$ 转换为一个复数信号，即**解析信号**，其中实部是原始信号，虚部是其希尔伯特变换的结果。**其专门用于处理实数信号。**

![image-20251105175351818](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105175351818.png)

**其中，$\hat{x}(t)$ 和 $\hat{X}(f)$ 上的符号（“$\hat{}$”）表示信号经过希尔伯特变换之后的结果。**

**sgn(f)** 是**符号函数**（sign function），通常用于表示一个数的符号。它的数学定义如下：
$$
\text{sgn}(f) =
\begin{cases} 
1 & \text{如果 } f > 0 \\
0 & \text{如果 } f = 0 \\
-1 & \text{如果 } f < 0 
\end{cases}
$$
**有以下性质：**

![image-20251105175707099](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105175707099.png)

### 3 解析信号

**定义如下**：![image-20251105175912427](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105175912427.png)

z(t) 是一个滤波器的输出，该滤波器的传递函数为 $1 + \text{sgn}(f)$，当输入信号为 $x(t)$ 时，该滤波器的作用是生成解析信号。

**解析信号的性质：**

![image-20251105180220641](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105180220641.png)

解析信号的自相关函数：![image-20251105180323087](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105180323087.png)

**一些常用的解析信号：**

![image-20251105180756271](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105180756271.png)

假设**m(t)** 是一个带宽为 **$W$** 的基带信号，假设 **$f_c > W$**。

### 4 复包络

对于一个实数的带通信号 $x(t)$，其复包络信号 $x_L(t)$ 定义为：
$$
x_L(t) = z(t) e^{-j2\pi f_c t}
$$
其中：

- $z(t)$ 是信号的解析信号（由信号 $x(t)$ 和其希尔伯特变换构成）。
- $e^{-j2\pi f_c t}$ 是一个复指数项，用来进行频移，$f_c$ 是中心载波频率。

![image-20251105194219116](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105194219116.png)

****

**$x_L(t)$和$x(t)$之间的转换**

![image-20251105194355541](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105194355541.png)

**三种表示**

![image-20251105194420813](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105194420813.png)

**等效基带表示**：

- $x(t) = \text{Re} \{ x_L(t) e^{j 2 \pi f_c t} \}$
- 这是将带通信号转换为基带信号的一般表达式，其中：
  - $x_L(t)$ 是复包络信号。
  - $f_c$ 是中心频率。
  - $e^{j 2 \pi f_c t}$ 是频移因子。

2. **同相正交表示 (In-phase Quadrature Representation)**：

- **表达式**：$x(t) = x_c(t) \cos 2 \pi f_c t - x_s(t) \sin 2 \pi f_c t$
  - 这里，$x_c(t)$ 和 $x_s(t)$ 分别是复包络信号的同相分量和正交分量。
  - **同相分量** $x_c(t) = \text{Re}\{ x_L(t) \}$：是复包络信号的实部。
  - **正交分量** $x_s(t) = \text{Im}\{ x_L(t) \}$：是复包络信号的虚部。

3. **包络相位表示 (Envelope Phase Representation)**：

- **表达式**：$x(t) = A(t) \cos[ 2 \pi f_c t + \varphi(t) ]$
  - 这里，$A(t)$ 是包络函数，表示信号的幅度。
  - $\varphi(t)$ 是相位函数，表示信号的相位。
  - 包络函数 $A(t) = |x_L(t)|$ 和相位函数 $\varphi(t) = \angle x_L(t)$ 是通过复包络的幅度和相位得到的。

**可以通过这几种表示互相求$x(t)$ 和$x_L(t)$。**

### 5 **带通系统的等效基带表示**（Equivalent Baseband Representation of Bandpass System）

通过频域和时域的表示形式，展示了如何将带通信号在处理系统中转换为等效的基带信号。

![image-20251105195155011](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105195155011.png)

带通信号有正负频两侧（$±f_c$），而低通等效只保留正频部分，所以功率、幅度都要“减半”，这就是那个 $1/2$ 系数的来源。

