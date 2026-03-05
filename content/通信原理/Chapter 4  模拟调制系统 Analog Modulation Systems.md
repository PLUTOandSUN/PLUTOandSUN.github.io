
## 4.1 基本概念

### 1 介绍

基带（低频）信号无法直接通过无线电波传输。它们需要先从基带信号转换为带通信号（调制），再通过天线发射。在接收端，接收到的带通信号会被转换回基带信号（解调）。![image-20251106230954212](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106230954212.png)

### 2  I/Q modulation and I/Q demodulation

![image-20251106231440891](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106231440891.png)

这里**复包络**信号（$s_L(t) = I(t) + j Q(t)$）通过调制过程转变成**带通信号**（$s(t)$）。**复包络**信号 $s_L(t) = I(t) + j Q(t)$ 是由同相分量 $I(t)$ 和正交分量 $Q(t)$ 组成的。这个复数信号是基带信号的简化表示。

上述过程的**复信号表示**如下：![image-20251106232812357](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251106232812357.png)

## 4.2 Amplitude Modulation 幅度调制

### 1 Double-sideband suppressed carrier modulation（DSB-SC）（双边带抑制载波调幅）

简单地说，就是假设**基带信号$m(t)$**是一个复包络信号$s_L(t)$的实部，把它调制成**带通信号**$s(t)$，即复包络信号的原信号。

![image-20251107005358441](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107005358441.png)

这里相位怎么取都可以。

**性质：**

- 时域性质：![image-20251107005600578](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107005600578.png)

- 频域性质：![image-20251107005736160](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107005736160.png)
- **带通信号**$s(t)$的PSD：![image-20251107005859058](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107005859058.png)

**DSB-SC**如果调制和解调的载波信号有相位差，那么最后的带通信号也会有相位差。所以，调制和解调的载波信号相位必须一样，即必须是**Coherent detection（相干解调）**，即必须要是**carrier synchronization（载波同步）的。

如果要实现**载波同步**，我们可以通过**Pilot assisted carrier synchronization (导频辅助的载波同步）**，即一个**导频信号**（一个常数乘载波信号）与调制信号一同传输。

**调制过程如下：**![image-20251107010516455](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107010516455.png)

在**频域**表现如下：![image-20251107010548976](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107010548976.png)

**解调过程如下：**![image-20251107010632102](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107010632102.png)

我们可以通过**锁相环**生成解调的载波信号![image-20251107010746309](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107010746309.png)

这里通过调制特性可以看出，解调信号为2倍才能恢复原信号的幅度

### 2 Amplitude Modulation（幅度调制）与包络解调

AM，即**DSB-SC**用**Pilot assisted carrier synchronization (导频辅助的载波同步）**，插入幅度足够大的载波，使包络和$m(t)$呈现出线性关系，其最大的特点是不仅可以**相干解调**，而且可以**非相干解调（包络解调）**

**调制过程**：![image-20251107012833332](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107012833332.png)

**频谱特征：**![image-20251107012858673](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107012858673.png)

**解调过程：**

- 相干解调，跟上述的一样：![image-20251107013121103](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107013121103.png)
- **非相干解调：**![image-20251107013230847](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107013230847.png)

通过**插入调幅系数大于0小于等于1的插入载波**，我们可以发现**带通信号**的**复包络=包络**，这样，我们就可以用包络检波器直接输出**直流信号+基带信号**，隔直流后即可得出基带信号。

在其中，有几个参数非常重要，具体如下：![image-20251107012938558](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107012938558.png)

其中，a等于a乘以$m_n(t)$的最大值

a的取值影响**调制的深浅**![image-20251107013749531](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107013749531.png)

![image-20251107013645323](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107013645323.png)

### 3 Single Sideband Modulation（SSB）（单边带调制）

**介绍：**

双边带信号在$f_c$左右有两个对称边带，保留其中一个就是单边带信号。因为只保留了一个，所以单边带信号的带宽为$W$。

![image-20251107112530841](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107112530841.png)

有两种形式，一种是取正半轴，一种是取负半轴。

上单边带信号的复包络是$m(t)$的解析信号（通过希尔伯特变换去求），下单边带信号的复包络是$m(t)$的解析信号的共轭

**复包络和复包络的原信号（带通信号）具体如下：**![image-20251107113100116](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107113100116.png)

![image-20251107113116454](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107113116454.png)

**具体调制过程如下：**![image-20251107113303378](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107113303378.png)

后面是负为上边带，正为下边带。

**解调过程如下：**![image-20251107113615236](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107113615236.png)



## 4.3 Angle Modulation 角度调制

### 1 基础知识

前面两种方式我们用载波的幅度携带信息，现在我们尝试用载波的**相位**携带信息![image-20251105194420813](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251105194420813.png)

根据**包络相位表示**，我们可以用包络相位的$\varphi(t)$携带信息。

关于相位的一些表示：![image-20251107143312667](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107143312667.png)

### 2 **调相**和**调频**

我们可以看出，可以使$m(t)$和相位有对应关系，也可以使$m(t)$和频率有对应关系，分别是**调相**和**调频**。![image-20251107144353978](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107144353978.png)

任何角度调制信号，即可以看作**调频信号**，也可 以看作**调相信号**，两者没有本质区别，可以互相转化，所以在下面我们主要讨论**调频**

![image-20251107144539118](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107144539118.png)

![image-20251107144550112](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107144550112.png)

### 3 重要参数

关于角度调制信号的**重要参数**：

![image-20251107144805167](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107144805167.png)



**FM的频谱特性：**

**FM信号的绝对带宽是无穷大，FM信号的有效带宽有一定范围**

具体来说,带通信号$s_(t)$和$s_L(t)$可以表现为以下形式：![image-20251107160120547](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107160120547.png)

鉴于频谱分析非常复杂，我们一般应用**卡松公式**来计算**频谱宽度**![image-20251107160458556](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251107160458556.png)

为**最大频偏**和**原信号的频率**之和的两倍。

## 4.4 Analysis of Noise Immunity （抗噪性能分析）

![image-20251108000246815](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108000246815.png)

| 调制方式   | 带宽              | 输出信噪比 ($(S/N)_o$)                          | 相对抗噪声性能     |
| ------ | --------------- | ------------------------------------------ | ----------- |
| DSB-SC | $2W$            | $\frac{P_R}{N_0 W}$                        | 基准          |
| SSB    | $W$             | $\frac{P_R}{N_0 W}$                        | 与 DSB-SC 相同 |
| AM     | $2W$            | $\eta \frac{P_R}{N_0 W}$                   | 差（因效率低）     |
| FM     | $2(\beta + 1)W$ | $\frac{3\beta_f^2}{C_m} \frac{P_R}{N_0 W}$ | 最好          |

**dB（分贝, decibel）** 不是一种“物理量”，而是一种**相对比值的对数表示单位**。

如果我们有两个功率 $P_1$ 和 $P_2$，
 那么它们的分贝差定义为：
$$
L_{dB} = 10 \log_{10}\left(\frac{P_1}{P_2}\right)
$$

> 单位是 **dB（分贝）**

## 4.5 Frequency division multiplexing (FDM) 频分复用

![image-20251108005230318](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108005230318.png)

![image-20251108005332707](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251108005332707.png)

## 4.5 补充
- 余弦函数 $\cos(2\pi f_0 t)$:
    
    $$\mathcal{F}\{\cos(2\pi f_0 t)\} = \frac{1}{2} [\delta(f - f_0) + \delta(f + f_0)]$$
    
- 正弦函数 $\sin(2\pi f_0 t)$:
    
    $$\mathcal{F}\{\sin(2\pi f_0 t)\} = \frac{1}{2j} [\delta(f - f_0) - \delta(f + f_0)]$$

- $\cos(\omega_0 t) = \frac{1}{2}(e^{j\omega_0 t} + e^{-j\omega_0 t})$
- $\sin(\omega_0 t) = \frac{1}{2j}(e^{j\omega_0 t} - e^{-j\omega_0 t})$

