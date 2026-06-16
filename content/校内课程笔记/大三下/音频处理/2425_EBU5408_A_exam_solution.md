---
title: 2425_EBU5408_A Paper A 逐题解析
aliases:
  - EBU5408 Paper A 2024/25 逐题解析
  - Digital Audio Fundamentals Paper A 逐题答案
tags:
  - course/音频处理
  - EBU5408
  - exam-review
  - digital-audio
source:
  - "[[课程笔记/音频处理/附件/2425_EBU5408_A.pdf]]"
created: 2026-06-15
---

# 2425_EBU5408_A Paper A 逐题解析

> [!info] 使用说明
> 本文根据试卷 `2425_EBU5408_A.pdf` 整理。每一小题都包含：**原题**、**答案/解题过程**、**相关考点**、**复习提醒**。  
> 建议配合课程讲义阅读：Block 1 的 Sound Waves / Sound Perception / Digitisation，Block 2 的 MIDI / Sound Synthesis / Speech，Block 3 的 Compression、PCA/ICA，Block 4 的 applied audio processing 与 revision slides。

---

## 总体结构

| Question | 分值 | 主题 |
|---|---:|---|
| Q1 | 25 | 声波基础、采样与混叠、量化与 SQNR |
| Q2 | 25 | 掩蔽与临界频带、MIDI、ADSR、说话人识别 |
| Q3 | 25 | 噪声音频中的目标语音提取、ICA 源分离 |
| Q4 | 25 | WAV/MP3 文件大小、FLAC residual 的 Huffman 编码 |

---

# Question 1

## Q1(a) 弦的基频、波长、波速与长度变化

### 原题

> A bass guitar string of length 0.78 meters is fixed at both ends and vibrates at its fundamental frequency of 440 Hz (note A above middle C, also known as A4). Assuming the speed of the wave in the string is constant:  
> i) Calculate the wavelength of the fundamental frequency.  
> ii) Determine the speed of the wave traveling in the string.  
> iii) If the length of the string is increased to 0.86 meters, what will be the new fundamental frequency?

### 答案

#### i) 基频波长

两端固定的弦在**基频**振动时，弦长等于半个波长：

$$
L = \frac{\lambda}{2}
$$

所以：

$$
\lambda = 2L = 2 \times 0.78 = 1.56\ \text{m}
$$

**答案：**

$$
\boxed{\lambda = 1.56\ \text{m}}
$$

#### ii) 弦中波速

波速、频率、波长关系为：

$$
v = f\lambda
$$

代入：

$$
v = 440 \times 1.56 = 686.4\ \text{m/s}
$$

**答案：**

$$
\boxed{v = 686.4\ \text{m/s}}
$$

#### iii) 弦长增加到 0.86 m 后的新基频

波速保持不变，新的基频仍满足：

$$
f' = \frac{v}{\lambda'} = \frac{v}{2L'}
$$

其中：

$$
L' = 0.86\ \text{m}, \quad \lambda' = 2L' = 1.72\ \text{m}
$$

所以：

$$
f' = \frac{686.4}{1.72} \approx 399.07\ \text{Hz}
$$

也可以用比例关系：

$$
f' = f \frac{L}{L'} = 440 \times \frac{0.78}{0.86} \approx 399.07\ \text{Hz}
$$

**答案：**

$$
\boxed{f' \approx 399\ \text{Hz}}
$$

弦变长后，频率降低，因此音高会下降。

### 相关考点

- 两端固定弦的驻波：基频对应半个波长。
- 基频公式：

$$
f_1 = \frac{v}{2L}
$$

- 波速关系：

$$
v = f\lambda
$$

- 弦长与基频成反比：波速不变时，弦越长，基频越低。
- 课程联系：Block 1 Sound Waves 中的 frequency、wavelength、pitch、resonance、harmonics。

### 复习提醒

这类题最容易丢分的地方是把弦长直接当成波长。对于**两端固定弦的基频**，一定记住：

$$
\lambda = 2L
$$

---

## Q1(b) 采样、Nyquist 频率与 aliasing

### 原题

> A sound signal has frequency components at 500 Hz, 1500 Hz, and 2500 Hz. It is sampled at a frequency of 2000 Hz.  
> i) What is the Nyquist frequency for this system? Explain your answer.  
> ii) Which frequency components will alias? Explain why and calculate their aliased frequencies.  
> iii) Draw the frequency spectrum of the reconstructed signal. Clearly label the axes.

### 答案

#### i) Nyquist frequency

采样频率为：

$$
f_s = 2000\ \text{Hz}
$$

Nyquist frequency 是采样频率的一半：

$$
f_N = \frac{f_s}{2} = \frac{2000}{2} = 1000\ \text{Hz}
$$

**答案：**

$$
\boxed{f_N = 1000\ \text{Hz}}
$$

解释：如果一个连续信号要在采样后无混叠重建，信号中最高频率必须不超过采样频率的一半。

#### ii) 哪些频率会 alias？alias 后是多少？

原始频率成分：

$$
500\ \text{Hz},\quad 1500\ \text{Hz},\quad 2500\ \text{Hz}
$$

Nyquist frequency 是 1000 Hz，所以：

- 500 Hz 小于 1000 Hz，不会 alias；
- 1500 Hz 大于 1000 Hz，会 alias；
- 2500 Hz 大于 1000 Hz，会 alias。

alias 频率可用：

$$
f_{alias} = |f - kf_s|
$$

选择合适整数 $k$，让结果落在 $0$ 到 $f_N$ 之间。

对 1500 Hz：

$$
f_{alias} = |1500 - 1 \times 2000| = 500\ \text{Hz}
$$

对 2500 Hz：

$$
f_{alias} = |2500 - 1 \times 2000| = 500\ \text{Hz}
$$

**答案：**

$$
\boxed{1500\ \text{Hz} \rightarrow 500\ \text{Hz}}
$$

$$
\boxed{2500\ \text{Hz} \rightarrow 500\ \text{Hz}}
$$

因此重建后，三个成分都会落到 500 Hz 位置。实际重建信号中会表现为 500 Hz 处的一个频率分量，幅度取决于原始各分量的幅度和相位。

#### iii) 重建信号频谱

重建信号在 Nyquist 范围内只会看到 500 Hz 处的分量。

示意图：

```text
Magnitude
   ^
   |
   |             |
   |             |  500 Hz
   |             |  original 500 Hz + aliases from 1500 Hz and 2500 Hz
   |
   +-------------+----------------------------> Frequency (Hz)
   0            500                         1000
                                            Nyquist frequency
```

如果画双边频谱，也应在 $+500$ Hz 和 $-500$ Hz 处标出对应分量。

### 相关考点

- Sampling rate：每秒采样次数。
- Nyquist frequency：

$$
f_N = \frac{f_s}{2}
$$

- Aliasing：高于 Nyquist frequency 的频率会折叠到低频，产生错误频率成分。
- Anti-aliasing filter：采样前应滤掉高于 Nyquist frequency 的频率。
- 课程联系：Block 1 Digitisation 中的 sampling、Nyquist theorem、aliasing。

### 复习提醒

看到采样题时，固定步骤是：

1. 先算 $f_N = f_s/2$；
2. 把所有原始频率和 $f_N$ 比较；
3. 大于 $f_N$ 的频率用 $|f-kf_s|$ 折叠回 $0$ 到 $f_N$；
4. 最后画重建频谱。

---

## Q1(c) 量化步长、量化噪声与 SQNR

### 原题

> A sound signal is quantised using n=12 bits. The maximum voltage of the signal $(V_{max})$ is 5 Volts.  
> i) Calculate the quantisation step size (or quantisation interval) in Volts.  
> ii) Calculate the maximum quantisation noise in Volts.  
> iii) Calculate an approximation of the Signal-to-Quantisation Noise Ratio (SQNR) in decibels (dB), knowing that SQNR is defined by Eq. 1 below. Refer to the log chart shown in Table 1 for your calculations.  
> $SQNR = 20 \log_{10}(V_{max}/Quantisation\_noise)$  
> iv) Compare your result obtained using Eq. 1 above with the SQNR calculated using Eq. 2 below. Explain why an offset of 1.76 dB is used in Eq. 2.  
> $SQNR = 6.02n + 1.76\ \text{dB}$, where $n$ is the bit depth.

### 答案

#### i) Quantisation step size

12 bits 对应的量化级数为：

$$
2^{12} = 4096
$$

若信号电压范围为 $-V_{max}$ 到 $+V_{max}$，总范围为：

$$
2V_{max} = 10\ \text{V}
$$

量化间隔为：

$$
\Delta V = \frac{2V_{max}}{2^n}
$$

代入：

$$
\Delta V = \frac{2 \times 5}{4096} = \frac{10}{4096} \approx 0.002441\ \text{V}
$$

**答案：**

$$
\boxed{\Delta V \approx 0.00244\ \text{V} = 2.44\ \text{mV}}
$$

#### ii) Maximum quantisation noise

最大量化误差通常为半个量化间隔：

$$
Q_{max} = \frac{\Delta V}{2}
$$

所以：

$$
Q_{max} = \frac{0.002441}{2} \approx 0.001221\ \text{V}
$$

**答案：**

$$
\boxed{Q_{max} \approx 0.00122\ \text{V} = 1.22\ \text{mV}}
$$

#### iii) 用 Eq. 1 计算 SQNR

题目给出：

$$
SQNR = 20\log_{10}\left(\frac{V_{max}}{Quantisation\ noise}\right)
$$

代入：

$$
\frac{V_{max}}{Q_{max}} = \frac{5}{0.0012207} \approx 4096
$$

所以：

$$
SQNR = 20\log_{10}(4096)
$$

根据表中：

$$
\log_{10}(4000) \approx 3.60
$$

而 $4096$ 略大于 $4000$，所以：

$$
\log_{10}(4096) \approx 3.61
$$

$$
SQNR \approx 20 \times 3.61 = 72.2\ \text{dB}
$$

**答案：**

$$
\boxed{SQNR \approx 72.2\ \text{dB}}
$$

如果按表格粗略估算，也可以写为约 $72\ \text{dB}$。

#### iv) 与 Eq. 2 比较，并解释 1.76 dB

用 Eq. 2：

$$
SQNR = 6.02n + 1.76
$$

代入 $n=12$：

$$
SQNR = 6.02 \times 12 + 1.76 = 72.24 + 1.76 = 74.00\ \text{dB}
$$

**答案：**

$$
\boxed{SQNR \approx 74.0\ \text{dB}}
$$

比较：

| 方法 | SQNR |
|---|---:|
| Eq. 1，用最大量化噪声估算 | 约 72.2 dB |
| Eq. 2，理想 ADC / 满幅正弦模型 | 约 74.0 dB |

Eq. 2 比 Eq. 1 高约：

$$
74.0 - 72.2 \approx 1.8\ \text{dB}
$$

**1.76 dB 的原因：**

Eq. 2 是理想均匀量化器对满幅正弦信号的经典 SQNR 公式。它使用的是信号和量化噪声的 **RMS power / average power** 模型，而不是简单用最大量化误差作分母。量化噪声通常假设在 $-\Delta/2$ 到 $+\Delta/2$ 之间均匀分布，其 RMS 值与最大误差不同；满幅正弦信号的 RMS 值也与峰值不同。把这些常数项合并到 dB 公式中，就得到额外的 $1.76\ \text{dB}$。

### 相关考点

- Bit depth 决定量化级数：$2^n$。
- 量化间隔：

$$
\Delta V = \frac{2V_{max}}{2^n}
$$

- 最大量化噪声：

$$
Q_{max} = \frac{\Delta V}{2}
$$

- SQNR 越大，量化质量越好，动态范围越大。
- 每增加 1 bit，理想 SQNR 大约增加 6.02 dB。
- 课程联系：Block 1 Digitisation 中的 quantisation、quantisation noise、dynamic range、SQNR。

### 复习提醒

量化题要分清三个量：

1. 量化级数：$2^n$；
2. 量化间隔：总电压范围除以级数；
3. 最大量化误差：量化间隔的一半。

---

# Question 2

## Q2(a) 临界频带与频率掩蔽

### 原题

> Consider a sound signal with three frequencies: 1 kHz, 1.2 kHz, and 2 kHz. A loud tone at 1.2 kHz has a sound pressure level (SPL) of 50 dB.  
> i) Estimate the masking thresholds for the 1 kHz and 2 kHz quieter tones in the signal, assuming the masking effect decreases by 15 dB per critical band. Use Table 2 to determine the critical band width.  
> ii) Draw the hearing threshold between 0 and 5 kHz, including any masking thresholds for the above signal. Clearly label the axes.

### 答案

#### i) 估计 1 kHz 和 2 kHz 的 masking thresholds

强掩蔽音：

$$
f_m = 1.2\ \text{kHz},\quad SPL_m = 50\ \text{dB}
$$

根据 Table 2，1.2 kHz 最接近：

- Critical band 10；
- center frequency 1170 Hz；
- bandwidth 约 190 Hz。

1 kHz 最接近 critical band 9，2 kHz 接近 critical band 13 或 14。因为 2 kHz 在 1850 Hz 和 2150 Hz 两个中心频率之间，估算时允许有轻微差异。

**推荐写法：按 critical band 编号估算。**

- 1.2 kHz：约在第 10 个 critical band；
- 1 kHz：约在第 9 个 critical band；
- 2 kHz：约在第 14 个 critical band，或按近似也可写第 13 个 critical band。

对 1 kHz：

$$
\Delta Bark \approx 1
$$

掩蔽效应每隔一个 critical band 降低 15 dB：

$$
T_{mask}(1\ \text{kHz}) \approx 50 - 15 \times 1 = 35\ \text{dB}
$$

**1 kHz 答案：**

$$
\boxed{T_{mask}(1\ \text{kHz}) \approx 35\ \text{dB}}
$$

对 2 kHz：

如果把 2 kHz 视为第 14 个 critical band：

$$
\Delta Bark \approx 14 - 10 = 4
$$

$$
T_{mask}(2\ \text{kHz}) \approx 50 - 15 \times 4 = -10\ \text{dB}
$$

如果把 2 kHz 视为第 13 个 critical band：

$$
\Delta Bark \approx 13 - 10 = 3
$$

$$
T_{mask}(2\ \text{kHz}) \approx 50 - 15 \times 3 = 5\ \text{dB}
$$

**2 kHz 推荐答案：**

$$
\boxed{T_{mask}(2\ \text{kHz}) \approx -10\ \text{dB}\ \text{to}\ 5\ \text{dB}}
$$

在考试中可以选择一种一致的估算法。若使用第 14 个 critical band，则写：

$$
\boxed{T_{mask}(2\ \text{kHz}) \approx -10\ \text{dB}}
$$

但要说明：实际听阈不应低于 absolute threshold of hearing，所以图中可以把 2 kHz 处的有效听阈画在普通听阈附近，而不是无限降低。

#### 另一种用 bandwidth 的估算

也可以用 1.2 kHz 附近的 critical bandwidth 约 190 Hz：

对 1 kHz：

$$
\Delta f = |1200 - 1000| = 200\ \text{Hz}
$$

$$
\text{critical bands apart} \approx \frac{200}{190} \approx 1.05
$$

$$
T_{mask} \approx 50 - 15 \times 1.05 \approx 34.2\ \text{dB}
$$

约等于 35 dB。

对 2 kHz：

$$
\Delta f = |2000 - 1200| = 800\ \text{Hz}
$$

$$
\text{critical bands apart} \approx \frac{800}{190} \approx 4.21
$$

$$
T_{mask} \approx 50 - 15 \times 4.21 \approx -13\ \text{dB}
$$

这个结果与上面按 critical band 编号得到的 $-10$ dB 很接近。

#### ii) 听阈图应该怎么画

图中需要包含：

- x-axis：Frequency，范围 0 到 5 kHz；
- y-axis：SPL / Threshold，单位 dB；
- 普通 hearing threshold；
- 1.2 kHz 处的 loud masker，50 dB；
- 1 kHz 处被提高后的 masking threshold，约 35 dB；
- 2 kHz 处较低的 masking threshold，约 $-10$ 到 $5$ dB，实际可接近 absolute hearing threshold。

示意图：

```text
SPL / dB
  ^
50|                         * masker at 1.2 kHz, 50 dB
45|                       /   \
40|                      /     \
35|              *------/       \         threshold near 1 kHz ≈ 35 dB
30|                    /         \
20|                  /             \
10|                /                 \   threshold near 2 kHz ≈ 0-5 dB
 0|____absolute hearing threshold______*____________________
  |
  +--------------------------------------------------------> Frequency / kHz
  0       1.0     1.2       2.0                         5.0
```

### 相关考点

- Psychoacoustics：人耳感知不是线性的。
- Critical band：内耳把频率分成若干临界频带，低频临界带窄，高频临界带宽。
- Frequency masking：强声音会提高邻近频率的听阈，使弱声音听不见。
- Masking threshold：有 masker 时新的听阈。
- 课程联系：Block 1 Sound Perception 中的 critical bands、frequency masking、threshold of hearing；Block 3 lossy compression 中的 psychoacoustic model。

### 复习提醒

画掩蔽图时不要求艺术化，关键是要标清：

1. 横轴频率；
2. 纵轴 dB SPL；
3. masker 的位置和高度；
4. 被掩蔽频率的 threshold；
5. 掩蔽效果随距离增大而下降。

---

## Q2(b) MIDI Note-On 消息解析

### 原题

> You receive the following MIDI Note-On message: `0x94 0x2D 0x1E`  
> i) Explain the structure of this message.  
> ii) What MIDI channel is this message on?  
> iii) What is the note (in decimal)?  
> iv) What is the velocity of the note (in decimal)?

### 答案

MIDI channel voice message 通常由：

```text
status byte + data byte 1 + data byte 2
```

组成。

本题消息为：

```text
0x94 0x2D 0x1E
```

#### i) 消息结构

`0x94` 是 status byte。

十六进制 `0x94` 可拆成两个 nibble：

```text
0x9  0x4
```

- 高 4 位 `0x9`：表示 **Note On**；
- 低 4 位 `0x4`：表示 MIDI channel 编码值。

`0x2D` 是第一个 data byte，表示 note number。

`0x1E` 是第二个 data byte，表示 velocity。

所以结构为：

| Byte | 含义 |
|---|---|
| `0x94` | Note-On status byte，channel 编码为 4 |
| `0x2D` | Note number |
| `0x1E` | Velocity |

#### ii) MIDI channel

MIDI 的通道编码是 0 到 15，但通常显示为 channel 1 到 16。

`0x94` 的低 4 位是 `0x4`，因此：

- raw channel index = 4；
- human-readable MIDI channel = 4 + 1 = 5。

**答案：**

$$
\boxed{\text{MIDI channel 5}}
$$

> 如果题目按零基编号问，也可写 encoded channel value = 4。但常规 MIDI 频道编号应写 Channel 5。

#### iii) Note in decimal

`0x2D` 转十进制：

$$
2 \times 16 + 13 = 32 + 13 = 45
$$

**答案：**

$$
\boxed{45}
$$

#### iv) Velocity in decimal

`0x1E` 转十进制：

$$
1 \times 16 + 14 = 16 + 14 = 30
$$

**答案：**

$$
\boxed{30}
$$

### 相关考点

- MIDI 不是音频波形，而是控制事件。
- Note-On message：告诉合成器在某通道开始播放某个音符。
- Status byte 高 nibble 表示命令，低 nibble 表示通道。
- Data bytes 通常在 0 到 127 范围内。
- 课程联系：Block 2 MIDI and Sound Synthesis 中的 MIDI messages、Note On、channels、note number、velocity。

### 复习提醒

MIDI 十六进制题的固定做法：

1. 看 status byte 的高 nibble：`0x9` 是 Note On；
2. 看 status byte 的低 nibble：channel 编码；
3. 第二个 byte 是 note；
4. 第三个 byte 是 velocity；
5. 十六进制转十进制。

---

## Q2(c) ADSR envelope 填空

### 原题

> You are designing the envelope generator of a sound synthesis system. Complete the following sentences using the correct words from the list provided.  
> i) The *MISSING WORD* is the time it takes for the sound to reach its *MISSING WORD* level when a key is pressed. A fast *MISSING WORD* results in a *MISSING WORD* onset.  
> ii) The *MISSING WORD* is the period after the *MISSING WORD* where the sound *MISSING WORD* to the *MISSING WORD* level.  
> iii) *MISSING WORD* is the level at which the sound is held as long as the key remains pressed.  
> iv) Release is the time it takes for the sound to *MISSING WORD* after the key is released.  
> List of words: minimum, maximum, decay, sharp, soft, fade-in, fade-out, sustain, falls, rises, attack

### 答案

#### i)

完整句子：

> The **attack** is the time it takes for the sound to reach its **maximum** level when a key is pressed. A fast **attack** results in a **sharp** onset.

答案：

```text
attack, maximum, attack, sharp
```

#### ii)

完整句子：

> The **decay** is the period after the **attack** where the sound **falls** to the **sustain** level.

答案：

```text
decay, attack, falls, sustain
```

#### iii)

完整句子：

> **Sustain** is the level at which the sound is held as long as the key remains pressed.

答案：

```text
sustain
```

#### iv)

完整句子：

> Release is the time it takes for the sound to **fade-out** after the key is released.

答案：

```text
fade-out
```

### ADSR 总结图

```text
Amplitude
  ^
  |        /\
  |       /  \____ sustain level ______
  |      /        \                    \
  |     /          \                    \
  |____/            \____________________\____> Time
      Attack       Decay              Release
```

### 相关考点

- ADSR envelope：Attack, Decay, Sustain, Release。
- Attack：按键后从 0 到最大幅度的时间。
- Decay：从最大幅度下降到 sustain level 的时间。
- Sustain：按键保持时维持的幅度水平。
- Release：松键后声音衰减到 0 的时间。
- 课程联系：Block 2 Sound Synthesis 中的 envelope generator、ADSR、synthesiser architecture。

### 复习提醒

ADSR 中只有 Sustain 是 **level**，其他 Attack、Decay、Release 都主要是 **time**。

---

## Q2(d) Speaker verification 与 speaker identification

### 原题

> Explain the commonalities and the differences between a speaker verification system and a speaker identification system.

### 答案

Speaker verification 和 speaker identification 都属于 **speaker recognition**，即通过声音判断说话人身份。

#### 共同点

二者都：

1. 使用人的语音信号作为输入；
2. 从语音中提取说话人相关特征，例如 MFCC、pitch、formants、spectral envelope、timbre 等；
3. 需要 enrolment / registration 阶段，即先保存已知说话人的 voice model 或 voiceprint；
4. 在测试阶段把未知语音与已注册模型比较；
5. 会受到背景噪声、录音设备、房间混响、说话情绪、疾病、口音、语音伪造和重放攻击影响；
6. 常用于安全认证、取证、个性化服务、人机交互等场景。

#### 不同点

| 项目 | Speaker verification | Speaker identification |
|---|---|---|
| 核心问题 | “这个人是不是他声称的那个人？” | “这个未知说话人是谁？” |
| 比较方式 | 一对一比较 | 一对多搜索 |
| 输入 | 语音 + claimed identity | 语音，通常没有 claimed identity |
| 输出 | Accept / reject | 某个身份，或 unknown |
| 典型应用 | 声纹登录、银行电话认证、门禁 | 犯罪取证、会议说话人标注、数据库检索 |
| 难度特点 | 依赖阈值设置，关注 false accept / false reject | 注册人数越多越难，容易出现混淆 |

#### 一句话区分

- **Verification**：验证一个身份声明，判断真假。
- **Identification**：从候选人集合中找出最可能是谁。

### 相关考点

- Speaker recognition = verification + identification。
- Enrolment 阶段与 recognition 阶段。
- 一对一匹配与一对多匹配。
- 生物识别系统中的 threshold、false acceptance、false rejection。
- 课程联系：Block 2 Music and Speech 中的 speaker recognition；Block 4 Audio Forensics / ML 中的 speaker identification、verification、biometric security。

### 复习提醒

考试回答这类概念题时，不要只写定义。最好按下面结构：

1. 先说共同点；
2. 再说 verification 是 one-to-one；
3. 再说 identification 是 one-to-many；
4. 最后给应用例子。

---

# Question 3

## Q3(a) 城市场景噪声中的目标语音提取

### 原题

> Consider the scenario given below and answer questions related to it:  
> You are provided with a 60-second audio recording captured in a busy urban environment. The recording contains a mixture of multiple sound sources including vehicle noise, crowd chatter, and one speaker delivering an important message. The target speech is embedded within these overlapping noises. Your task is to design an audio processing pipeline to reduce the noise and extract the target voice.  
> i) Which algorithm do you think would be the most effective for this scenario? Justify your choice.  
> ii) Explain why extracting the target conversation is difficult given the nature of the background noise.  
> iii) Based on the given scenario, how would you determine the optimal number of components to use for audio separation using the selected algorithm?

### 答案

#### i) 最合适的算法及理由

本题最适合选择：

$$
\boxed{\text{ICA / FastICA, Independent Component Analysis}}
$$

理由：

1. 这个场景是典型的 **cocktail party problem**：多个声源混在一起，需要从混合信号中分离出目标说话人。
2. ICA 是一种 **blind source separation** 方法，可以在没有干净参考语音的情况下，把混合信号分解成统计上尽可能独立的成分。
3. 目标语音、车辆噪声、群体聊天声通常来自不同物理声源，具有不同的统计特征，因此可以尝试用 ICA 分离。
4. PCA 主要用于降维和去相关，能减少部分噪声，但不一定能真正把独立声源分开；ICA 更适合 source separation。
5. 如果有多麦克风录音，ICA 更直接适用；如果只有单通道录音，可以先做 STFT，把 time-frequency bins 构造成特征，再结合 ICA、NMF 或深度学习方法做近似分离。

**简洁考试版答案：**

> ICA is the most suitable because it separates statistically independent source components from mixed observations. In this urban recording, the target speaker, vehicle noise and crowd chatter can be treated as different sources. ICA is therefore more appropriate than PCA, which mainly decorrelates and reduces dimensionality but does not necessarily unmix sources.

#### ii) 为什么提取目标对话困难？

难点主要有：

1. **频率重叠**：人声、群体聊天和车辆噪声可能都覆盖低频到中频范围，无法用简单 band-pass filter 完全分开。
2. **语音之间相似**：crowd chatter 本身也是语音，与目标 speaker 的频谱、formants、节奏结构相似。
3. **非平稳噪声**：城市噪声随时间变化，例如车辆经过、喇叭、脚步、突发声等，不是稳定背景噪声。
4. **掩蔽效应**：强噪声会掩蔽较弱的目标语音，使某些音节或频率区域不可听。
5. **混响和传播路径**：城市环境可能有墙面反射，导致源信号在时间上叠加，增加分离难度。
6. **低 SNR**：如果目标说话人音量不够高，语音细节会被噪声覆盖。

**简洁考试版答案：**

> Extraction is difficult because the target speech overlaps in both time and frequency with vehicle noise and crowd chatter. Crowd chatter is especially difficult because it is speech-like. The background is non-stationary, so its spectrum and amplitude change over time, making simple filtering ineffective.

#### iii) 如何确定 ICA 的 optimal number of components？

可以按以下步骤确定：

1. **根据场景先验估计**：本题至少有三类主要声源：
   - vehicle noise；
   - crowd chatter；
   - target speaker。
   因此可以先尝试：

$$
n_{components} \approx 3
$$

2. **受观测通道数限制**：如果有 $M$ 个麦克风，标准 ICA 的可分离成分数通常不能超过 $M$。
3. **用 PCA / eigenvalue scree plot**：先做 PCA，观察多少个主成分能解释大部分方差，例如 95% 或 99%。
4. **实验调参**：尝试 2、3、4、5 个 components，比较分离效果。
5. **用客观指标评价**：例如 SNR、SDR、STOI、PESQ、SI-SDR。
6. **用听感和 spectrogram 检查**：目标 component 应该显示清晰的语音 formants、harmonics 和 syllable pattern；噪声 component 则应主要包含车辆或群体背景。
7. **避免过多或过少**：
   - components 太少：多个声源仍混在一起；
   - components 太多：可能把目标语音拆碎，产生 artifacts。

**推荐答案：**

$$
\boxed{\text{Start with }3\text{ components, then tune using PCA variance, objective metrics, spectrogram inspection and listening tests.}}
$$

### 相关考点

- Cocktail party problem。
- Blind source separation。
- ICA vs PCA。
- Non-stationary noise。
- Time-frequency representation / spectrogram。
- SNR、SDR、STOI、PESQ 等语音增强评价指标。
- 课程联系：Block 3 PCA and ICA；Block 4 Audio Processing / Revision Slides；Lab 2 Audio Source Separation。

### 复习提醒

遇到“多声源混合 + 要提取目标声源”的题，优先想到：

- ICA / FastICA；
- PCA whitening；
- source separation；
- cocktail party problem；
- limitations and assumptions。

---

## Q3(b) ICA 实现流程、局限与增强方法

### 原题

> Solve the questions below if ICA is selected for the scenario provided in Q3(a):  
> i) Provide a detailed, step-by-step approach for implementing the ICA algorithm. Clearly define each stage of the process. Coding is not required, but ensure that your explanation includes key considerations such as parameter selection and expected outcomes.  
> ii) Discuss the potential limitations of ICA in this scenario and propose additional techniques or algorithmic adjustments that could further enhance noise reduction performance.

### 答案

## Q3(b)(i) ICA step-by-step approach

下面给出一个适合考试作答的完整 pipeline。

### Step 1: Audio loading and inspection

读取 60 秒音频，检查：

- sampling rate；
- duration；
- number of channels；
- waveform；
- spectrogram；
- clipping 是否存在；
- 是否有明显 silent regions。

如果是多通道录音，形成观测矩阵：

$$
X \in \mathbb{R}^{M \times T}
$$

其中 $M$ 是麦克风通道数，$T$ 是时间样本数。

如果是单通道录音，可以先做 time-frequency representation，例如 STFT，再在频带或时频 patch 上做近似分解。

### Step 2: Pre-processing

预处理包括：

1. 转为统一格式，例如 WAV；
2. 统一采样率，例如 16 kHz、44.1 kHz 或题目给定采样率；
3. 转为 mono 或保留多通道，取决于算法设计；
4. 去除 DC offset；
5. normalisation，避免某个通道幅度过大；
6. 可选 voice activity detection，去掉长时间静音；
7. 可选 band-pass filtering，例如保留语音主要频段 300 Hz 到 3400 Hz，减少低频车辆 rumble 和高频 hiss。

### Step 3: Centering

ICA 通常要求数据零均值：

$$
X_c = X - \mu_X
$$

这样每个通道的均值为 0。

### Step 4: Whitening / PCA preprocessing

对中心化后的数据做 whitening，使不同观测维度去相关且方差归一：

$$
Z = V X_c
$$

Whitening 的作用：

- 降低数据相关性；
- 简化 ICA 的 unmixing 过程；
- 提高收敛稳定性；
- 可以顺便用 PCA 选择 components 数量。

### Step 5: Select number of components

选择 $n_{components}$ 时考虑：

- 主要声源数量：目标 speaker、vehicle noise、crowd chatter，初始可设为 3；
- 麦克风通道数量；
- PCA explained variance；
- 分离后 component 是否可解释；
- SNR / SDR / STOI / PESQ；
- 听感是否更清晰。

推荐调参策略：

```text
try n_components = 2, 3, 4, 5
compare objective metrics + spectrogram + listening
choose the smallest number that gives clear target speech without excessive artifacts
```

### Step 6: Apply ICA / FastICA

ICA 假设混合模型为：

$$
X = AS
$$

其中：

- $X$ 是观测到的混合信号；
- $S$ 是独立源信号；
- $A$ 是未知 mixing matrix。

ICA 的目标是找到 unmixing matrix $W$：

$$
\hat{S} = WX
$$

FastICA 会最大化 non-Gaussianity，例如通过 kurtosis 或 negentropy，使输出成分尽可能统计独立。

参数可包括：

| 参数 | 含义 | 选择建议 |
|---|---|---|
| `n_components` | 分离成分数 | 从 3 开始试 |
| `max_iter` | 最大迭代次数 | 设置较大，保证收敛 |
| `tol` | 收敛阈值 | 较小更精确，但更慢 |
| `random_state` | 随机种子 | 保证结果可重复 |
| contrast function | 非高斯性度量 | speech separation 常用 logcosh |

### Step 7: Identify the target voice component

ICA 输出的 components 没有固定顺序，需要判断哪一个是目标语音。

判断方法：

1. 听每个 component；
2. 看 spectrogram 是否有语音特征：
   - formants；
   - voiced harmonics；
   - syllable rhythm；
   - speech-like modulation；
3. 与目标说话人的已知 voiceprint 或 enrollment sample 比较；
4. 用 ASR intelligibility 或 speaker embedding 判断。

### Step 8: Reconstruct target audio

选择目标 component 后，重建目标语音。

如果是在 STFT 域处理，需要使用 inverse STFT：

$$
\hat{x}_{speech}(t) = ISTFT(\hat{S}_{speech})
$$

如果是时域多通道 ICA，直接取目标 component 并进行幅度恢复。

### Step 9: Post-processing

为了进一步提升质量，可以做：

- Wiener filtering；
- spectral subtraction；
- noise gate；
- speech band-pass filtering；
- de-click / de-rumble；
- dereverberation；
- loudness normalisation；
- artifact suppression。

### Step 10: Evaluation

评价包括客观和主观两类。

客观指标：

- SNR improvement；
- SDR / SI-SDR；
- PESQ；
- STOI；
- spectral distortion。

主观评价：

- 听起来是否更清晰；
- 目标语音是否更容易听懂；
- 是否出现 musical noise 或 pumping artifacts；
- 背景噪声是否明显降低。

### Expected outcomes

理想结果：

- 一个 component 主要包含目标 speaker；
- 其他 components 分别包含 vehicle noise、crowd chatter 或残余背景；
- 目标语音的 intelligibility 提升；
- spectrogram 中 speech formants 更清晰；
- 总体 SNR 提高。

但实际结果通常是 partial separation，不一定能完全干净地分离。

---

## Q3(b)(ii) ICA 的局限与改进方法

### ICA 的局限

1. **独立性假设不完全成立**  
   ICA 假设源信号统计独立。但 crowd chatter 和 target speech 都是语音，统计特征相似，独立性不一定强。

2. **线性瞬时混合假设过于理想**  
   城市环境有反射和混响，实际更像 convolutive mixing，而不是简单的瞬时线性混合。

3. **通道数限制**  
   标准 ICA 通常要求观测通道数不少于源数。如果只有一个 microphone，却有多个源，标准 ICA 很难直接分离。

4. **非平稳噪声**  
   车辆噪声、喇叭、人群声随时间变化，导致统计特性不稳定。

5. **尺度和顺序不确定**  
   ICA 输出的 component 顺序和幅度不固定，需要后续识别。

6. **可能产生 artifacts**  
   过度分离或参数不当可能导致语音断裂、musical noise 或失真。

7. **目标语音可能被拆散**  
   如果 components 过多，语音的不同频段或音节可能分散到多个 components。

### 改进方法

| 问题 | 可用改进 |
|---|---|
| 单通道或欠定分离 | 使用 NMF、deep learning speech separation、source-conditioned extraction |
| 混响严重 | dereverberation、convolutive ICA、beamforming |
| 车辆低频噪声强 | high-pass filter / band-pass filter |
| 人群聊天与目标语音相似 | speaker embedding、enrollment clue、target speaker extraction |
| 非平稳噪声 | adaptive noise reduction、Wiener filter、spectral gating |
| ICA artifacts | post-filtering、component selection、parameter tuning |
| 结果不稳定 | PCA whitening、固定 random seed、调整 tolerance 和 iteration |

### 推荐增强 pipeline

```text
Audio input
  -> format conversion and normalisation
  -> high-pass / band-pass filtering
  -> STFT spectrogram
  -> PCA whitening
  -> ICA / FastICA separation
  -> target component selection using speech features or speaker embedding
  -> Wiener filtering / spectral subtraction
  -> inverse STFT
  -> loudness normalisation
  -> evaluation by SNR, STOI, PESQ and listening tests
```

### 相关考点

- ICA 的假设：independence、linear mixture、non-Gaussianity。
- Whitening 和 PCA preprocessing。
- Components 数量选择。
- Source separation 的 evaluation。
- ICA 的局限：under-determined、reverberation、non-stationary noise、permutation/scale ambiguity。
- 课程联系：Block 3 Digital Audio PCA / ICA；Lab 2 Audio Source Separation；Block 4 Applied Digital Audio Processing。

### 复习提醒

Q3 是大题，阅卷通常看结构。建议按下面模板写：

1. Algorithm choice：ICA / FastICA；
2. Why：independent sources + cocktail party problem；
3. Difficulty：overlap + non-stationary + masking；
4. Pipeline：preprocess -> STFT -> whitening -> ICA -> select component -> postprocess -> evaluate；
5. Limitations：assumptions + channels + reverberation；
6. Improvements：filtering + Wiener + NMF/deep learning + beamforming。

---

# Question 4

## Q4(a) WAV 与 MP3 文件大小计算

### 原题

> Consider the scenario given below and answer questions related to it:  
> An AI-powered voice cloning system generates speech audio at 48 kHz sampling rate with 16-bit depth and stereo format. The generated speech is stored as uncompressed WAV files before being compressed for transmission.  
> i) Calculate the file size (in MB) of a 1-minute uncompressed AI-generated WAV file based on the given parameters. Show your steps for calculation.  
> ii) If the original file is compressed using MP3 at 128 kbps, calculate the new file size after compression. Show your steps for calculation.

### 答案

#### i) 1 分钟 uncompressed WAV 文件大小

已知：

| 参数 | 数值 |
|---|---:|
| Sampling rate | 48 kHz = 48,000 samples/s |
| Bit depth | 16 bits/sample |
| Channels | stereo = 2 channels |
| Duration | 60 s |

每个 sample 每个 channel 的字节数：

$$
16\ \text{bits} = 2\ \text{bytes}
$$

每个采样时刻的 stereo frame 字节数：

$$
2\ \text{bytes} \times 2\ \text{channels} = 4\ \text{bytes}
$$

每秒字节数：

$$
48000 \times 4 = 192000\ \text{bytes/s}
$$

60 秒字节数：

$$
192000 \times 60 = 11520000\ \text{bytes}
$$

转换为 MB：

如果用十进制 MB：

$$
\frac{11520000}{1000000} = 11.52\ \text{MB}
$$

如果用 $1\ \text{MiB} = 1024^2\ \text{bytes}$：

$$
\frac{11520000}{1024^2} \approx 10.99\ \text{MiB}
$$

**答案：**

$$
\boxed{\text{约 }11\ \text{MB}}
$$

更精确地说，是 **11.52 MB** 或 **10.99 MiB**。WAV header 约 44 bytes，可以忽略不计。

#### ii) MP3 128 kbps 压缩后的文件大小

MP3 bitrate：

$$
128\ \text{kbps} = 128000\ \text{bits/s}
$$

60 秒总 bit 数：

$$
128000 \times 60 = 7680000\ \text{bits}
$$

转换为 bytes：

$$
\frac{7680000}{8} = 960000\ \text{bytes}
$$

转换为 MB：

$$
\frac{960000}{1000000} = 0.96\ \text{MB}
$$

或：

$$
\frac{960000}{1024^2} \approx 0.916\ \text{MiB}
$$

**答案：**

$$
\boxed{\text{约 }0.96\ \text{MB}}
$$

压缩比大约为：

$$
\frac{11.52}{0.96} = 12
$$

即 MP3 文件约为原始 PCM WAV 的 $1/12$。

### 相关考点

- PCM audio bitrate：

$$
\text{bitrate} = sampling\ rate \times bit\ depth \times channels
$$

- 文件大小：

$$
\text{file size} = bitrate \times duration
$$

- bits 和 bytes 转换：

$$
8\ \text{bits} = 1\ \text{byte}
$$

- kHz、kbps、MB 的单位换算。
- Uncompressed WAV 与 compressed MP3 的区别。
- 课程联系：Block 1 Digitisation；Block 3 Compression and Decompression；Block 4 Revision Slides。

### 复习提醒

文件大小题最容易错在单位：

- 48 kHz 要写成 48,000 samples/s；
- 16 bit 要除以 8 变成 2 bytes；
- stereo 要乘 2；
- kbps 是 bits per second，不是 bytes per second。

---

## Q4(b) Huffman coding for FLAC residuals

### 原题

> A company is developing an audio compression system for high-fidelity lossless audio storage. They have decided to use Huffman coding to compress residual values. The company’s research team analysed the residual values from a FLAC-encoded audio file and found the frequency distribution of residuals shown in Table 3.  
> Residual Value / Frequency: -2: 5%, -1: 20%, 2: 10%, 1: 25%, 0: 40%.  
> i) Given the frequency distribution of residual values in a FLAC-encoded audio file, derive the Huffman codes for each residual.  
> ii) Calculate the average number of bits per residual using the weighted average formula.  
> iii) Compare the result to a fixed-length encoding approach using 3 bits per residual and determine the amount of compression achieved.  
> iv) Compare the result from part (iii) to the fixed-length encoding approach using 3 bits per residual and explain how much compression is achieved.  
> v) Construct the Huffman tree based on the given frequency distribution from part (i).

### 答案

给定频率：

| Residual | Frequency |
|---:|---:|
| -2 | 5% |
| -1 | 20% |
| 2 | 10% |
| 1 | 25% |
| 0 | 40% |

Huffman coding 的原则是：**频率越高，code 越短；频率越低，code 越长。**

---

### i) Derive Huffman codes

先按频率从小到大排序：

```text
-2 : 5%
 2 : 10%
-1 : 20%
 1 : 25%
 0 : 40%
```

逐步合并最小频率：

#### Step 1

合并 5% 和 10%：

```text
(-2, 5%) + (2, 10%) = 15%
```

#### Step 2

合并 15% 和 20%：

```text
15% + (-1, 20%) = 35%
```

#### Step 3

合并 25% 和 35%：

```text
(1, 25%) + 35% = 60%
```

#### Step 4

合并 40% 和 60%：

```text
(0, 40%) + 60% = 100%
```

给左分支分配 0，右分支分配 1，可以得到一组合法 Huffman codes：

| Residual | Frequency | Huffman code | Code length |
|---:|---:|---:|---:|
| 0 | 40% | `0` | 1 |
| 1 | 25% | `10` | 2 |
| -1 | 20% | `110` | 3 |
| -2 | 5% | `1110` | 4 |
| 2 | 10% | `1111` | 4 |

> 注意：Huffman code 不唯一。只要树结构满足 Huffman 合并规则，左右分支 0/1 互换也算正确，平均码长不变。

---

### ii) Weighted average bits per residual

平均码长：

$$
L_{avg} = \sum p_i l_i
$$

代入：

$$
L_{avg}
= 0.40 \times 1
+ 0.25 \times 2
+ 0.20 \times 3
+ 0.05 \times 4
+ 0.10 \times 4
$$

$$
L_{avg} = 0.40 + 0.50 + 0.60 + 0.20 + 0.40 = 2.10
$$

**答案：**

$$
\boxed{L_{avg} = 2.1\ \text{bits/residual}}
$$

---

### iii) 与 fixed-length 3 bits 比较，计算压缩量

Fixed-length encoding 使用：

$$
3\ \text{bits/residual}
$$

Huffman coding 平均使用：

$$
2.1\ \text{bits/residual}
$$

节省的 bit 数：

$$
3 - 2.1 = 0.9\ \text{bits/residual}
$$

节省比例：

$$
\frac{0.9}{3} = 0.30 = 30\%
$$

**答案：**

$$
\boxed{\text{每个 residual 平均节省 }0.9\ \text{bits，约节省 }30\%}
$$

压缩比也可写为：

$$
\frac{3}{2.1} \approx 1.43:1
$$

---

### iv) 解释压缩为什么发生

Huffman 相比固定长度编码的优势在于：

- fixed-length encoding 给每个 residual 都分配 3 bits，不管它出现频率高低；
- Huffman coding 给高频 residual 更短 code，例如 residual 0 的频率是 40%，只用 1 bit；
- 低频 residual 使用更长 code，例如 -2 和 2 使用 4 bits；
- 因为高频值出现得更多，所以总体平均 bit 数下降到 2.1 bits/residual。

所以 Huffman 编码使用固定长度编码的：

$$
\frac{2.1}{3} = 0.70 = 70\%
$$

也就是说压缩后平均 bit 数约为原来的 70%，减少约 30%。

**答案：**

$$
\boxed{\text{Huffman achieves about }30\%\text{ compression relative to 3-bit fixed-length coding.}}
$$

---

### v) Huffman tree

与上面 codes 对应的 Huffman tree 可以画成：

```text
                         [100%]
                        /      \
                    0  /        \ 1
                      /          \
                  0:40%          [60%]
                                /     \
                            0  /       \ 1
                              /         \
                          1:25%        [35%]
                                      /      \
                                  0  /        \ 1
                                    /          \
                                -1:20%        [15%]
                                             /      \
                                         0  /        \ 1
                                           /          \
                                      -2:5%          2:10%
```

由树读出 code：

| Residual | Path | Code |
|---:|---|---:|
| 0 | left | `0` |
| 1 | right-left | `10` |
| -1 | right-right-left | `110` |
| -2 | right-right-right-left | `1110` |
| 2 | right-right-right-right | `1111` |

### 相关考点

- Lossless compression：压缩后可完全恢复原始数据。
- FLAC：常用预测编码产生 residual，再对 residual 做 entropy coding。
- Residual：实际样本与预测样本之间的差。
- Huffman coding：高频符号短码，低频符号长码。
- Prefix-free code：没有任何 code 是另一个 code 的前缀。
- Average code length：

$$
L_{avg} = \sum p_i l_i
$$

- Compression ratio 与 percentage saving。
- 课程联系：Block 3 Compression and Decompression 中的 lossless compression、predictive coding、residuals、entropy coding、Huffman coding、FLAC。

### 复习提醒

Huffman 题固定步骤：

1. 按频率从小到大排序；
2. 每次合并两个最小的节点；
3. 重复直到总频率 100%；
4. 给左右分支分配 0 和 1；
5. 从根到叶读出 code；
6. 用 $\sum p_i l_i$ 算平均码长；
7. 与 fixed-length bit 数比较。

---

# 全卷考点总复习

## 1. Block 1: Sound waves and acoustics

必须掌握：

- 声音是介质中的压力波；
- frequency、wavelength、period、amplitude；
- $v=f\lambda$；
- pitch 与 frequency 的关系；
- resonance、standing wave、harmonics；
- 弦两端固定时：

$$
\lambda_1 = 2L, \quad f_1 = \frac{v}{2L}
$$

常见题型：

- 给弦长和频率，求波长、波速；
- 改变弦长，求新频率；
- 判断频率变高还是变低。

---

## 2. Block 1: Digitisation

必须掌握：

### Sampling

$$
f_N = \frac{f_s}{2}
$$

- $f_s$ 是 sampling rate；
- $f_N$ 是 Nyquist frequency；
- 超过 $f_N$ 的频率会 alias；
- 采样前使用 anti-aliasing filter。

### Quantisation

$$
2^n\ \text{levels}
$$

$$
\Delta V = \frac{2V_{max}}{2^n}
$$

$$
Q_{max}=\frac{\Delta V}{2}
$$

### SQNR

$$
SQNR \approx 6.02n + 1.76\ \text{dB}
$$

常见题型：

- 算 Nyquist frequency；
- 算 alias frequency；
- 算量化间隔；
- 算最大量化噪声；
- 算 SQNR。

---

## 3. Block 1: Sound perception

必须掌握：

- human hearing is nonlinear；
- threshold of hearing；
- critical bands；
- frequency masking；
- temporal masking；
- masking threshold。

考试高频表达：

> A loud tone raises the hearing threshold of nearby frequencies, making quieter tones inaudible.

要会解释为什么这和 compression 有关：

- lossy compression 会删除或粗量化被掩蔽的成分；
- 人耳听不到的部分可以用更少 bits 表示；
- MP3 等编码依赖 psychoacoustic model。

---

## 4. Block 2: MIDI and synthesis

必须掌握：

### MIDI

- MIDI is not audio；
- MIDI is event/control data；
- Note On：`0x9n note velocity`；
- Note Off：`0x8n note velocity`；
- channel 编码是 0 到 15，对应 channel 1 到 16。

十六进制转换要熟练：

| Hex | Decimal |
|---|---:|
| `0x2D` | 45 |
| `0x1E` | 30 |
| `0x94` | Note On, encoded channel 4, displayed channel 5 |

### ADSR

- Attack：到 peak / maximum 的时间；
- Decay：从 peak 降到 sustain 的时间；
- Sustain：按键保持时的 level；
- Release：松键后 fade out 的时间。

---

## 5. Block 2 / Block 4: Speech and speaker recognition

必须掌握：

- Speaker recognition 包括 verification 和 identification；
- verification：one-to-one，accept/reject；
- identification：one-to-many，find who；
- 常用特征：MFCC、pitch、formants、spectral features、speaker embeddings；
- 风险：noise、channel mismatch、spoofing、deepfake、replay attack。

---

## 6. Block 3: PCA and ICA

必须掌握：

### PCA

- 降维；
- 去相关；
- 保留最大方差方向；
- 可用于 denoising 或 whitening；
- 不保证分离独立声源。

### ICA

- Independent Component Analysis；
- blind source separation；
- 假设源信号统计独立；
- 常用于 cocktail party problem；
- 常见步骤：centering -> whitening -> ICA -> component selection -> reconstruction。

关键限制：

- 源数不能明显超过观测通道数；
- 混响会破坏 instantaneous mixing 假设；
- 相似语音源很难分；
- 输出顺序和尺度不确定；
- 需要后处理。

---

## 7. Block 3: Compression

必须掌握：

### 文件大小

$$
\text{bitrate} = sampling\ rate \times bit\ depth \times channels
$$

$$
\text{file size} = bitrate \times duration
$$

注意：

- bit 转 byte 要除以 8；
- stereo 要乘以 2；
- kbps 是 kilobits per second；
- WAV 是 uncompressed，MP3 是 compressed。

### Lossless compression

- predictive coding；
- residual；
- entropy coding；
- Huffman coding；
- FLAC / ALAC。

### Huffman coding

- 频率高，码短；
- 频率低，码长；
- 码是 prefix-free；
- 平均码长：

$$
L_{avg} = \sum p_i l_i
$$

---

# 最后复习建议

## A. 按题型复习，不要只按 PPT 顺序复习

这张卷子的题型非常明确，可以按下面 6 类训练。

### 1. 计算题

必须反复练：

- $v=f\lambda$；
- fixed string fundamental；
- Nyquist frequency；
- alias frequency；
- quantisation interval；
- quantisation noise；
- SQNR；
- WAV / MP3 file size；
- Huffman average code length。

建议自己做一张公式卡片，把所有公式集中写在一页。

---

### 2. 图像题

本卷需要画：

- reconstructed frequency spectrum；
- masking threshold / hearing threshold；
- Huffman tree。

画图题的得分关键不是好看，而是：

- 轴标清楚；
- 单位标清楚；
- 关键点位置正确；
- 图中有文字说明。

---

### 3. 概念对比题

高频对比：

| 对比 | 必须会说 |
|---|---|
| Nyquist rate vs Nyquist frequency | 前者是采样率要求，后者是给定采样率下最高可表示频率 |
| Sampling vs quantisation | 时间离散 vs 幅度离散 |
| MIDI vs audio | 控制事件 vs 波形采样数据 |
| Verification vs identification | one-to-one vs one-to-many |
| PCA vs ICA | 降维/去相关 vs 独立源分离 |
| Lossy vs lossless | 允许丢信息 vs 完全恢复 |
| WAV vs MP3 | 未压缩 PCM 容器 vs 有损压缩格式 |

---

### 4. Pipeline 设计题

Q3 这类题要练结构化回答。建议背一个通用模板：

```text
1. Inspect audio
2. Preprocess: resample, normalise, remove DC, filter
3. Transform: waveform / STFT / spectrogram
4. Apply algorithm: PCA / ICA / filter / compression
5. Tune parameters
6. Reconstruct output
7. Post-process
8. Evaluate with metrics and listening tests
9. Discuss limitations
```

如果题目要求 “justify”，一定写为什么不用简单方法。例如：

- 简单滤波不能解决频率重叠；
- PCA 不一定能分离独立声源；
- ICA 适合 cocktail party problem，但依赖独立性和多通道。

---

### 5. 英文答题句型

考试要求英文作答，建议背一些句子。

#### ICA

> ICA is suitable because it attempts to separate statistically independent source components from mixed observations.

> PCA mainly decorrelates data and reduces dimensionality, whereas ICA aims to recover independent sources.

#### Masking

> A loud tone raises the hearing threshold of nearby frequencies, causing quieter components to become inaudible.

#### Quantisation

> Increasing bit depth reduces the quantisation interval and therefore reduces quantisation noise.

#### Huffman coding

> Huffman coding assigns shorter codes to more frequent symbols and longer codes to less frequent symbols, reducing the average number of bits per symbol.

#### Speaker recognition

> Speaker verification checks whether a speaker matches a claimed identity, while speaker identification determines which enrolled speaker best matches the unknown voice.

---

## B. 推荐复习顺序

### 第 1 轮：公式与计算

优先复习：

1. Sound waves；
2. Sampling / aliasing；
3. Quantisation / SQNR；
4. File size；
5. Huffman coding。

目标：看到数字题能在 1 分钟内写出公式。

---

### 第 2 轮：概念与对比

重点复习：

1. MIDI message；
2. ADSR；
3. masking；
4. speaker verification / identification；
5. PCA / ICA；
6. lossy / lossless compression。

目标：每个概念都能用 2 到 4 句话解释。

---

### 第 3 轮：大题组织

重点练：

- Q3 audio processing pipeline；
- ICA limitations；
- improvements；
- evaluation metrics；
- AI audio / ethics / voice cloning 相关讨论题。

目标：形成固定答题框架，不要临场乱写。

---

## C. 考前一页速记

建议考前最后一天默写下面内容。

### 公式

$$
v=f\lambda
$$

$$
\lambda_1 = 2L
$$

$$
f_N = \frac{f_s}{2}
$$

$$
f_{alias}=|f-kf_s|
$$

$$
\Delta V = \frac{2V_{max}}{2^n}
$$

$$
Q_{max}=\frac{\Delta V}{2}
$$

$$
SQNR \approx 6.02n+1.76
$$

$$
\text{bitrate}=f_s \times bit\ depth \times channels
$$

$$
L_{avg}=\sum p_i l_i
$$

### 高频关键词

```text
Nyquist, aliasing, quantisation noise, SQNR,
critical band, masking threshold, MIDI Note-On,
ADSR, speaker verification, speaker identification,
PCA whitening, ICA, blind source separation,
WAV, MP3, FLAC, residual, entropy coding, Huffman tree
```

---

## D. 本卷最容易失分的地方

1. **Q1(a)** 把弦长误当成波长。基频时 $\lambda=2L$。
2. **Q1(b)** 忘记 1500 Hz 和 2500 Hz 都会 alias 到 500 Hz。
3. **Q1(c)** 量化范围要用 $2V_{max}$，最大量化噪声是 $\Delta/2$。
4. **Q2(a)** masking threshold 要和 critical band 距离联系，不是简单频率差。
5. **Q2(b)** MIDI channel 要注意 0-based encoding 和 1-based channel display。
6. **Q2(c)** Sustain 是 level，不是 time。
7. **Q2(d)** verification 和 identification 一定要写 one-to-one / one-to-many。
8. **Q3** 不要只写 “use ICA”，必须写 pipeline、参数、局限和评价。
9. **Q4(a)** kbps 是 bits per second，换 bytes 要除以 8。
10. **Q4(b)** Huffman code 不唯一，但平均码长必须算对。

---

## E. 最后建议

如果复习时间有限，优先级如下：

1. **最高优先级：** Q1 和 Q4 的计算题，因为步骤固定，容易拿满分。
2. **第二优先级：** Q3 的 ICA pipeline，因为分值高，结构化回答能拿很多分。
3. **第三优先级：** Q2 的概念题，尤其 MIDI、ADSR、speaker verification vs identification。
4. **补充优先级：** masking 图和 threshold 解释，注意图的轴和单位。

建议最终考前至少完整手写一遍：

- 一道 aliasing 题；
- 一道 SQNR 题；
- 一道 MIDI 解析题；
- 一道 ADSR 填空；
- 一道 ICA pipeline；
- 一道 file size；
- 一道 Huffman coding。

只要这些题型熟练，本卷大部分分数都可以稳定拿到。
