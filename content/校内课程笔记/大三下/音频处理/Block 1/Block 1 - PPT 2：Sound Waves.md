
> [!info] 课件来源
> 原始课件：[[课程笔记/音频处理/附件/Block 1 - Sound waves and elements of acoustics/2. Sound Waves.pdf]]  
> 本节接在 PPT 1 Introduction 之后，开始正式解释“声音是什么”以及声音如何用波、频率、频谱和数学模型表示。

## 0. 本节课的整体框架

本 PPT 的主题是 **Sound Waves**。它围绕六个问题展开：

1. **What is sound?** 声音的物理本质是什么？
2. **Properties of single frequency sound waves** 单频声波有哪些属性？
3. **Sound as a complex waveform** 自然声音为什么通常是复杂波形？
4. **Sound synthesis with Audacity** 如何用 Audacity 合成声音？
5. **Sound analysis with Audacity** 如何分析复杂声音的频率成分？
6. **Modeling sound waves in Matlab** 如何用 Matlab 建模正弦波和复合波？

> [!summary] 本节核心
> 声音不是“物体移动到耳朵里”，而是**介质中的压力变化向外传播**。单频声音可用正弦波描述；自然声音通常由多个频率成分叠加而成；频谱、傅里叶分析和声谱图是理解复杂声音的关键工具。

---

## 1. What is sound? 声音是什么？

### 1.1 声音来自物体振动

PPT 给出的定义是：声音是由物体振动产生的物理现象。例如：

- 小提琴弦振动；
- 木块被敲击后振动；
- 人的声带振动；
- 吉他的金属弦和木质琴体振动；
- 扬声器纸盆前后振动。

物体振动时，会推动周围空气分子，使空气局部出现：

- **compression 压缩区**：空气分子更密，压力更高；
- **rarefaction 稀疏区**：空气分子更疏，压力更低。

这些高压和低压的交替变化向外传播，我们就称它为声波。

### 1.2 声音是 pressure wave 压力波

声音更准确地说是空气压力的周期性变化，而不是空气分子整体从声源飞到耳朵。

可以这样理解：

```text
振动物体 → 推动附近空气分子 → 形成压缩/稀疏 → 压力变化逐层传递 → 到达耳朵
```

空气分子只是在平衡位置附近来回振动，真正向外传播的是“压力扰动”或“能量”。

> [!important] 容易误解的点
> 声波图里的正弦曲线通常表示**压力或振幅随时间/位置的变化**，不是空气分子真的沿着正弦曲线路径飞行。

### 1.3 声音是 longitudinal wave 纵波

PPT 特别强调：扬声器产生的是 **longitudinal pressure wave**。

纵波的特点：

- 介质粒子的振动方向与波传播方向**平行**；
- 声波向前传播时，空气分子也沿前后方向来回振动；
- 波形中出现交替的压缩区和稀疏区。

对比：绳子上下振动产生的横波中，粒子运动方向与传播方向垂直；空气中的普通声波主要是纵波。

---

## 2. 声音如何传播？

### 2.1 Sound wave propagation

声音传播可以类比“排队的人互相推一下”：

1. 声源推动最近的空气分子；
2. 最近的空气分子推动旁边的空气分子；
3. 压力变化继续传递；
4. 最终到达听者耳朵。

这就是 **sound wave propagation**。

声音从点声源向外传播时，理想情况下会向各个方向扩散，形成近似球面波。但真实声源通常有方向性。例如 PPT 中的扬声器水平扩散图显示：

- 扬声器正前方振幅最大；
- 侧面较弱；
- 后方更弱。

这就是 loudspeaker directivity，即扬声器指向性。

### 2.2 Frequency 和 speed of sound 的区别

PPT 区分了两个容易混淆的概念：

| 概念 | 中文 | 含义 | 单位 |
|---|---|---|---|
| Frequency $f$ | 频率 | 某一点空气压力每秒振动多少次 | Hz |
| Speed of sound $v$ | 声速 | 压力变化在介质中传播的速度 | m/s |

频率描述“振动有多快”，声速描述“波传播有多快”。

> [!example] 关键区别
> 一个 100 Hz 声音和一个 1000 Hz 声音在同一空气温度下传播速度几乎相同，但它们的频率和波长不同。

### 2.3 声速取决于介质

PPT 给出的典型声速：

| 介质 | 声速 |
|---|---:|
| Air, 20°C | 约 344 m/s |
| Water, just above 0°C | 约 1410 m/s |
| Steel | 约 5100 m/s |
| Glass | 约 4000 m/s，取决于玻璃类型 |

声速受介质的弹性、密度、温度影响。一般来说，声音在固体中传播更快，在液体中次之，在气体中较慢。

---

## 3. 人如何听到声音？

PPT 的听觉链路可以整理为：

```text
空气压力波 → 外耳/耳道 → 鼓膜振动 → 中耳传递 → 内耳毛细胞 → 听觉神经 → 大脑解释为声音
```

具体过程：

1. 声波进入耳道；
2. 压力变化使鼓膜振动；
3. 振动通过中耳结构传递到内耳；
4. 内耳中的毛细胞把机械振动转换成神经信号；
5. 听觉神经把信号传给大脑；
6. 大脑把这些信号解释成音高、响度、音色、方向等感知。

这也解释了为什么音频处理不仅是物理问题，也是感知问题：最终听到什么取决于耳朵和大脑的处理。

---

## 4. 声波的基本行为

PPT 提到声波具有普通波的行为：reflection、refraction、diffraction。

### 4.1 Reflection 反射

**Reflection** 是声波遇到固体或液体表面后反弹。

常见现象：

- **echo 回声**：反射声与原声间隔较长，能听出重复声音；
- **reverberation 混响**：大量密集反射叠加，形成空间感。

> [!example] 教室里的混响
> 空教室通常更“响”，因为墙面、地板、天花板反射明显；人多或有软材料时，吸收更多高频，混响变短。

### 4.2 Refraction 折射

**Refraction** 是声波进入不同介质或不同密度区域时，因为传播速度改变而发生弯折。

例子：

- 声音从冷空气进入热空气，传播速度变化，传播方向可能改变；
- 水下声波会因温度、盐度、压力变化而弯曲传播。

### 4.3 Diffraction 衍射

**Diffraction** 是声波绕过障碍物或通过开口后继续传播并扩散。

低频声波波长长，更容易绕过障碍物；高频声波波长短，更容易被遮挡。

> [!tip] 为什么隔壁低音更明显？
> 低频波长长，衍射能力强，也更容易穿过或绕过墙体；高频更容易被墙、门、家具吸收或阻挡。

---

## 5. Single-frequency sound 单频声音

### 5.1 单频声音可以用正弦波表示

单频声波可以表示为：

$$
y(t)=A\sin(2\pi f t+\theta)
$$

其中：

| 符号 | 含义 |
|---|---|
| $A$ | amplitude，振幅 |
| $f$ | frequency，频率，单位 Hz |
| $t$ | time，时间，单位秒 |
| $\theta$ | phase，相位，表示起始偏移 |

单频声听起来接近“纯音”。现实中纯单频声音很少自然出现，但可以由计算机或信号发生器人工生成。

### 5.2 Frequency and pitch 频率与音高

**Frequency** 是客观物理量：每秒完成多少个周期，单位 Hz。

**Pitch** 是主观感知量：人听起来音高有多高。

二者有关但不完全等同。PPT 的例子：

- 440 Hz 通常听作钢琴上的 A4；
- 频率越高，通常 pitch 越高；
- 单频声通常被感知为单一 pitch。

### 5.3 人耳听觉频率范围

PPT 给出：人类大约能听到 **20 Hz - 20,000 Hz**。

补充理解：

- 20 Hz 以下称为 **infrasound 次声**，人通常听不到但可能感觉到振动；
- 20 kHz 以上称为 **ultrasound 超声**；
- 年龄增长、听力损伤、暴露在高噪声环境中都会降低高频听力；
- 大多数乐器的主要频率范围大约在 50 Hz - 5000 Hz，但泛音可以更高。

---

## 6. 单频波的关键属性

### 6.1 Amplitude 振幅

振幅是波在某一时刻的 y 值。对于纯正弦波，通常把最高点的绝对值称为振幅 $A$。

振幅越大，压力变化越大，人通常听起来越响。

### 6.2 Intensity 强度

**Intensity** 是单位时间穿过单位面积的能量，常用 dB 相关尺度表示。

PPT 强调：

$$
I \propto A^2
$$

也就是说，强度与振幅平方成正比。

> [!important] 重要结论
> 如果振幅变成原来的 2 倍，强度变成原来的 $2^2=4$ 倍。对应的强度级变化约为：
> $$20\log_{10}(2)\approx 6.02\text{ dB}$$

### 6.3 Period 周期

周期 $T$ 是波完成一个完整 cycle 所需时间，单位秒。

频率和周期互为倒数：

$$
T=\frac{1}{f}
$$

例子：440 Hz 的声音每秒完成 440 个周期，所以：

$$
T=\frac{1}{440}\approx0.00227\text{ s}=2.27\text{ ms}
$$

### 6.4 Wavelength 波长

波长 $\lambda$ 是波在一个周期内传播的空间距离。

公式：

$$
\lambda=\frac{v}{f}
$$

其中 $v$ 是声速，$f$ 是频率。

PPT 的例子：空气中声速约 344 m/s，440 Hz 声音的波长：

$$
\lambda=\frac{344}{440}\approx0.78\text{ m}
$$

### 6.5 Phase 相位

相位 $\theta$ 描述波相对于某个起点的水平偏移。

常见相位差：

| 相位差 | 含义 |
|---|---|
| $0^\circ$ | 同相，峰值和谷值对齐 |
| $90^\circ$ | 相差四分之一个周期 |
| $180^\circ$ | 反相，一个波峰对应另一个波谷 |
| $360^\circ$ | 相差一个完整周期，形状重新对齐 |

相位在音频中非常重要，因为多个波叠加时，相位会影响它们是增强还是抵消。

> [!example] 反相抵消
> 两个频率、振幅完全相同但相位差 $180^\circ$ 的正弦波相加，理论上会完全抵消，结果为静音。

---

## 7. Exercise 1：理解声波计算

题目：扬声器在空气中产生频率 $f=500$ Hz 的声波，声速 $v=340$ m/s。

### 7.1 计算波长

$$
\lambda=\frac{v}{f}=\frac{340}{500}=0.68\text{ m}
$$

所以波长是 **0.68 m**。

### 7.2 计算周期

$$
T=\frac{1}{f}=\frac{1}{500}=0.002\text{ s}=2\text{ ms}
$$

所以周期是 **2 ms**。

### 7.3 振幅加倍，强度增加多少？

因为：

$$
I\propto A^2
$$

振幅变为 $2A$ 时：

$$
I'\propto(2A)^2=4A^2
$$

所以强度增加到原来的 **4 倍**，约等于增加 **6.02 dB**。

---

## 8. Complex sound waves 复杂声波

### 8.1 自然声音通常不是纯音

PPT 强调：自然界中几乎没有纯单频声音。真实声音通常是很多频率成分叠加的结果。

例如：

- 人声包含基频、共振峰、辅音噪声、气流声；
- 吉他声包含基频和许多泛音；
- 噪声包含大量不规则频率成分；
- 鼓声包含宽频瞬态成分。

### 8.2 Frequency components 与 spectrum

一个复杂声音可以拆成多个 frequency components。

所有频率成分放在一起，就构成该声音的 **frequency spectrum 频谱**。

```text
复杂声音 = 频率成分 1 + 频率成分 2 + 频率成分 3 + ...
```

听者不会分别听到每个单独频率，而是把它们综合感知为一个整体声音，比如某个乐器的音色。

### 8.3 Noise、Speech、Musical sound 的波形区别

PPT 用图展示了三类声音：

| 类型 | 波形特点 | 听感 / 含义 |
|---|---|---|
| Noise 噪声 | 不规则、随机、难以看出稳定周期 | 频率成分杂乱，例如白噪声、环境噪声 |
| Speech 语音 | 有时有周期性元音，有时有噪声性辅音，随时间变化大 | 信息承载强，频谱动态变化 |
| Musical sound 乐音 | 通常更周期、谐波结构明显 | 有较明确音高和音色 |

> [!note] 语音为什么复杂？
> 语音不是稳定的一条正弦波。元音通常有准周期结构，辅音可能像噪声，单词中的频率成分会随时间不断变化。

---

## 9. Resonance and harmonics 共振与谐波

### 9.1 Resonance 共振

**Resonance** 是物体倾向于在某些自然频率上振动的特性。

影响自然共振频率的因素：

- 形状；
- 材料；
- 长度；
- 张力；
- 空腔结构；
- 固定方式。

乐器之所以有独特音色，很大程度来自它们的共振结构。

### 9.2 Fundamental frequency 基频

**Fundamental frequency** 是振动系统最低、最基本的频率，通常决定感知 pitch。

例如一根吉他弦振动时，最低模式可能是 196 Hz，那么人通常把这个音感知为 G3 附近。

### 9.3 Harmonics 谐波

谐波是基频的整数倍：

$$
f_n=nf_0
$$

其中 $f_0$ 是基频，$n=1,2,3,\ldots$。

| 谐波 | 频率 |
|---|---|
| 1st harmonic | $f_0$，也就是基频 |
| 2nd harmonic | $2f_0$ |
| 3rd harmonic | $3f_0$ |
| nth harmonic | $nf_0$ |

### 9.4 Overtones 泛音

PPT 提到，如果允许非整数倍的基频，就会产生更复杂的 overtones。

一般理解：

- **harmonics** 通常指整数倍频率；
- **overtones** 可以泛指基频以上的频率成分，有时包括非整数倍；
- 谐波结构越强，声音越有明确音高；
- 非谐波成分越多，声音可能越像钟声、打击乐或噪声。

---

## 10. Pitch 作为主观听觉质量

PPT 说明：frequency 是绝对物理量，而 pitch 是相对、主观的声音质量。

### 10.1 A4 = 440 Hz

音乐中通常把 middle C 上方的 A 设置为 440 Hz，即 A4 = 440 Hz。

这提供了频率和音名之间的参考关系。

### 10.2 Octave 八度

八度关系对应频率加倍或减半：

$$
\text{one octave up}: f\rightarrow2f
$$

例如：

- A4 = 440 Hz；
- 高一个八度 A5 = 880 Hz；
- 低一个八度 A3 = 220 Hz。

> [!important] 记忆方式
> 同名音相差一个 octave 时，听起来“类似但更高/更低”，其频率关系是 2:1。

---

## 11. Exercise 2：基频与谐波计算

题目：吉他弦长度 $L=0.65$ m，两端固定，基频 $f_1=196$ Hz，波速保持不变。

### 11.1 基频波长

两端固定的弦在基频模式下，弦长等于半个波长：

$$
L=\frac{\lambda_1}{2}
$$

所以：

$$
\lambda_1=2L=2\times0.65=1.30\text{ m}
$$

### 11.2 弦上波速

$$
v=f_1\lambda_1=196\times1.30=254.8\text{ m/s}
$$

所以波速约为 **254.8 m/s**。

### 11.3 第二、第三谐波频率

$$
f_2=2f_1=392\text{ Hz}
$$

$$
f_3=3f_1=588\text{ Hz}
$$

### 11.4 弦长缩短到 0.50 m 后的新基频

波速不变，新的基频波长：

$$
\lambda'_1=2L'=2\times0.50=1.00\text{ m}
$$

新基频：

$$
f'_1=\frac{v}{\lambda'_1}=\frac{254.8}{1.00}=254.8\text{ Hz}
$$

所以新基频约为 **255 Hz**。

> [!tip] 物理直觉
> 弦越短，基频越高。这就是吉他按品改变音高的基本原理。

---

## 12. Dynamic range 动态范围

### 12.1 定义

**Dynamic range** 是音频中最安静和最响亮部分之间的差异，单位通常是 dB。

PPT 的定义：

> 它是一个 mix 或 audio file 中 quietest sound 与 loudest sound 的 dB 差值。

公式可写为：

$$
\text{Dynamic Range(dB)}=20\log_{10}\left(\frac{\text{Maximum Signal Level}}{\text{Minimum Detectable Signal Level}}\right)
$$

### 12.2 大动态范围与小动态范围

| 类型    | 特点            | 例子              |
| ----- | ------------- | --------------- |
| 大动态范围 | 安静和响亮部分差距大    | 古典音乐、电影原声、现场录音  |
| 小动态范围 | 整体响度较平均，峰谷差异小 | 被重度压缩的流行音乐、广告音频 |

动态范围过大时，小声部分可能听不清；动态范围过小时，声音可能失去起伏、听起来疲劳。

---

## 13. Signal-to-noise ratio 信噪比 SNR

### 13.1 定义

**SNR** 是正确信号功率与噪声功率之比，用来衡量信号质量。

$$
\text{SNR}=\frac{P_{signal}}{P_{noise}}
$$

以 dB 表示：

$$
\text{SNR}_{dB}=10\log_{10}\left(\frac{P_{signal}}{P_{noise}}\right)
$$

如果用同阻抗下的电压表示，因为功率与电压平方成正比：

$$
\text{SNR}_{dB}=20\log_{10}\left(\frac{V_{signal}}{V_{noise}}\right)
$$

### 13.2 PPT 例子

如果信号电压是噪声电压的 10 倍：

$$
\text{SNR}_{dB}=20\log_{10}(10)=20\text{ dB}
$$

### 13.3 SNR 的意义

| SNR | 含义 |
|---|---|
| 高 SNR | 信号远大于噪声，声音更清晰 |
| 低 SNR | 噪声接近或超过信号，声音更难辨认 |

> [!example] 录音中的 SNR
> 如果人声很小而空调噪声很大，SNR 就低。提高麦克风距离、减少环境噪声、正确设置增益，都能改善 SNR。

---

## 14. Sound synthesis 声音合成

### 14.1 合成的基本思想

PPT 中 synthesis 的定义：把多个元素组合成新的东西。

在声音中，最基本的合成就是把多个声波相加：

$$
y(t)=y_1(t)+y_2(t)+y_3(t)+\cdots
$$

如果两个声音同时在空气中传播，它们在每个时刻的压力变化会相加，形成 composite wave。

### 14.2 Audacity 合成例子：C major chord

PPT 用 Audacity 的 Generate Tone 功能生成三个单频声音：

| 音符 | 频率 |
|---|---:|
| Middle C | 262 Hz |
| E | 330 Hz |
| G | 393 Hz |

这三个频率叠加后形成一个 C major chord 的复合波形。

```text
262 Hz + 330 Hz + 393 Hz → 复合声音
```

这说明复合声音在时域中可能看起来很复杂，但它其实可以由几个简单正弦波叠加得到。

### 14.3 谐波合成例子

PPT 还展示了：

```text
100 Hz + 200 Hz + 300 Hz → 含前三个谐波的复合声
```

因为 200 Hz 和 300 Hz 分别是 100 Hz 的 2 倍和 3 倍，所以它们是 100 Hz 基频的谐波。

---

## 15. Sound analysis 声音分析

### 15.1 分析是合成的反过程

合成是“从频率成分得到复杂声音”；分析是“从复杂声音找出频率成分”。

```text
Sound synthesis: 频率成分 → 复杂波形
Sound analysis: 复杂波形 → 频率成分
```

### 15.2 Fourier 的核心思想

PPT 提到 Joseph Fourier 证明：任何周期性函数都可以表示为一系列正弦/余弦频率成分之和。

这就是傅里叶分析的基础，也是音频处理中频谱、滤波、均衡、压缩等技术的基础。

> [!important] 为什么傅里叶分析重要？
> 因为很多音频操作在频域更容易理解：
> - EQ：增强或削弱某些频率；
> - Filter：保留或去除某些频率范围；
> - Noise reduction：估计并降低噪声频段；
> - Compression codec：根据听觉特性保留更重要的频率信息。

### 15.3 Waveform view vs Frequency analysis view

| 视图 | x 轴 | y 轴 | 看什么 |
|---|---|---|---|
| Waveform view | 时间 | 振幅 | 声音随时间如何变化 |
| Frequency analysis view / Spectrum | 频率 | 频率成分大小 | 声音包含哪些频率 |
| Spectrogram | 时间 | 频率，颜色表示能量 | 频率成分如何随时间变化 |

### 15.4 Spectrum 与 Spectrogram 的区别

**Spectrum** 通常描述一段声音在整体或某一时间窗口中的频率分布。

**Spectrogram** 则显示频率随时间的变化，特别适合分析语音、音乐、动物叫声等非稳定信号。

PPT 的 speech sound analysis 例子中，单词 “Information” 的语音：

- waveform 显示时域振幅；
- spectrum 显示某一段频率成分；
- spectrogram 显示整段语音中频率能量如何随时间移动。

---

## 16. Matlab 建模声波

### 16.1 Angular frequency 角频率

PPT 先从正弦函数开始：

$$
y=A\sin(2\pi ft+\theta)
$$

也可以用角频率 $\omega$ 表示：

$$
\omega=2\pi f
$$

于是：

$$
y=A\sin(\omega t+\theta)
$$

其中 $\omega$ 的单位是 radians/second。

### 16.2 Matlab 中生成单频正弦波

PPT 示例代码：

```matlab
fs = 44100;          % Sampling frequency in Hz, standard for audio
f = 262;             % Frequency of the sine wave in Hz
duration = 0.03;     % Duration in seconds
t = 0:1/fs:duration; % Time vector with 1/fs spacing
y = sin(2 * pi * f * t);

figure;
plot(t, y);
xlabel('Time (seconds)');
ylabel('Amplitude');
title('262 Hz Sine Wave');
```

解释：

| 代码 | 含义 |
|---|---|
| `fs = 44100` | 每秒采样 44100 次，是常见音频采样率 |
| `f = 262` | 生成 262 Hz 的正弦波，接近 middle C |
| `duration = 0.03` | 只画 0.03 秒，方便看清波形周期 |
| `t = 0:1/fs:duration` | 构造时间轴，每两个样本间隔为 $1/fs$ |
| `sin(2*pi*f*t)` | Matlab 的 `sin` 输入是弧度，所以要乘 $2\pi$ |

### 16.3 Matlab 中生成复合波

PPT 示例：

```matlab
f1 = 262;
f2 = 330;
f3 = 393;

y = sin(2 * pi * f1 * t) + ...
    sin(2 * pi * f2 * t) + ...
    sin(2 * pi * f3 * t);
```

这对应 Audacity 中的三个音：C、E、G。三个正弦波相加后，时域波形不再是简单正弦，但频谱中仍能看到 262 Hz、330 Hz、393 Hz 三个成分。

> [!tip] 连接 Audacity 和 Matlab
> Audacity 更直观，适合听和看；Matlab 更适合写公式、控制参数、重复实验。二者背后的数学是一样的：声音可以表示为采样后的数值序列。

---

## 17. 本节公式总结

| 公式 | 含义 |
|---|---|
| $y(t)=A\sin(2\pi ft+\theta)$ | 单频正弦波 |
| $\omega=2\pi f$ | 频率与角频率关系 |
| $y(t)=A\sin(\omega t+\theta)$ | 用角频率表示正弦波 |
| $T=\frac{1}{f}$ | 周期与频率关系 |
| $\lambda=\frac{v}{f}$ | 波长、声速、频率关系 |
| $I\propto A^2$ | 强度与振幅平方成正比 |
| $\text{SNR}_{dB}=10\log_{10}(P_s/P_n)$ | 功率形式信噪比 |
| $\text{SNR}_{dB}=20\log_{10}(V_s/V_n)$ | 同阻抗电压形式信噪比 |
| $f_n=nf_0$ | 谐波频率 |

---

## 18. 本节关键词表

| 英文术语 | 中文理解 |
|---|---|
| Sound wave | 声波，介质中的压力扰动传播 |
| Pressure wave | 压力波，由高压和低压区域交替形成 |
| Compression | 压缩区，空气分子密集、压力较高 |
| Rarefaction | 稀疏区，空气分子较疏、压力较低 |
| Longitudinal wave | 纵波，粒子振动方向与传播方向平行 |
| Propagation | 波的传播 |
| Frequency | 频率，每秒周期数，单位 Hz |
| Speed of sound | 声速，压力扰动传播速度 |
| Amplitude | 振幅，波偏离平衡位置的大小 |
| Intensity | 强度，单位时间单位面积能量 |
| Period | 周期，完成一次振动所需时间 |
| Wavelength | 波长，一个周期对应的空间距离 |
| Phase | 相位，波形相对起点的偏移 |
| Spectrum | 频谱，声音频率成分的分布 |
| Spectrogram | 声谱图，频率成分随时间变化的图 |
| Resonance | 共振，物体倾向于在自然频率振动 |
| Fundamental frequency | 基频，最低且通常决定 pitch 的频率 |
| Harmonics | 谐波，基频的整数倍频率 |
| Dynamic range | 动态范围，最响与最静声音之间的 dB 差 |
| SNR | 信噪比，信号功率与噪声功率之比 |
| Fourier analysis | 傅里叶分析，把复杂波拆成频率成分 |

---

## 19. 复习自测题

1. 为什么说声音是 pressure wave，而不是空气分子从声源移动到耳朵？
2. Compression 和 rarefaction 分别是什么意思？
3. Frequency 和 speed of sound 有什么区别？
4. 为什么声音在钢铁中传播速度比空气中快？
5. Reflection、refraction、diffraction 分别对应哪些声音现象？
6. 写出单频正弦波公式，并解释 $A$、$f$、$t$、$\theta$。
7. 500 Hz 声音的周期是多少？如果声速 340 m/s，波长是多少？
8. 振幅加倍时，声音强度变为多少倍？对应约多少 dB？
9. 为什么自然声音通常是 complex sound wave？
10. Fundamental frequency、harmonic、overtone 有什么区别？
11. 为什么 octave 对应频率翻倍？
12. Dynamic range 和 SNR 分别衡量什么？
13. Spectrum 和 spectrogram 有什么区别？
14. 为什么傅里叶分析是音频处理的基础？
15. Matlab 里为什么要写 `sin(2*pi*f*t)` 而不是直接 `sin(f*t)`？

---

## 20. 一句话总结

本节课把声音从“听觉经验”转化为“可计算的波形”：声音是介质中的压力波，单频声音可由正弦函数描述，自然声音由多个频率成分叠加而成，而频谱、声谱图、傅里叶分析和 Matlab/Audacity 实验是理解数字音频处理的基础工具。

---

