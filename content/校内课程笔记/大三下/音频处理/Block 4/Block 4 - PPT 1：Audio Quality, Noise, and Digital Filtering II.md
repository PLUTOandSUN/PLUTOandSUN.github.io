---
title: EBU5408 Block 4 - PPT 1：Audio Quality, Noise, and Digital Filtering II
aliases:
  - Block 4 PPT 1
  - Audio Quality Noise and Digital Filtering II
  - Digital Audio Quality Noise Filter
  - Audio Filter and Quality II
tags:
  - course/音频处理
  - EBU5408
  - digital-audio
  - block4
  - audio-quality
  - digital-filtering
  - noise
  - evaluation-metrics
source:
  - "[[../附件/Block 4 - Applied Digital Audio Processing/1 Audio Filter and Quality/Digital Audio Quality Noise Filter Part 2.pdf]]"
created: 2026-06-17
---

# Block 4 - PPT 1：Audio Quality, Noise, and Digital Filtering II

> [!info] 课件来源
> 本笔记对应 Block 4 第 1 组课件：
> - [[../附件/Block 4 - Applied Digital Audio Processing/1 Audio Filter and Quality/Digital Audio Quality Noise Filter Part 2.pdf]]
>
> 这节课延续了 Block 3 中的音频滤波基础，但重点更偏向 **Applied Digital Audio Processing**：不仅要知道滤波器如何改变声音，还要知道如何在复杂系统中使用滤波器，以及如何评价处理后的音频质量。

## 0. 这组 PPT 在课程中的作用

Block 3 第 3 组已经介绍了 low-pass、high-pass、notch、shelving、peaking、EQ 等基本滤波概念。Block 4 第 1 组是在这个基础上的进一步应用，主要讲三条主线：

1. **滤波与 EQ 的实际设计**
   - gain in dB；
   - cutoff frequency；
   - filter order；
   - tone control、parametric EQ、graphic EQ；
   - FIR 与 IIR 的选择。

2. **滤波在复杂音频系统中的作用**
   - 在 PCA / ICA 之前做预处理；
   - 在 PCA / ICA 之后做后处理；
   - 用滤波改善源分离、降噪和音色平衡。

3. **音频质量评价**
   - 主观评价：ABX、MOS、paired comparison；
   - 客观指标：SNR、THD、IMD、MSE/RMSE、PSNR、PEAQ、POLQA、ViSQOL、SDR、Amari Error；
   - 如何根据任务选择评价指标。

> [!summary] 一句话主线
> 这节课的核心不是“滤波器是什么”，而是：**如何安全地使用滤波器改善声音，以及如何判断改善是否真的有效。**

---

## 1. Shelving and Peaking Filter Composition：滤波器组合回顾

课件从 shelving 和 peaking filters 的组合开始。这部分可以看作 Block 3 末尾内容的复习和延伸。

### 1.1 为什么要组合 shelving 和 peaking filters？

单个滤波器通常只能完成一种简单任务：

- high-pass 去低频 rumble；
- low-pass 去高频 hiss；
- notch 去固定频率 hum；
- peaking cut 去某个共振；
- shelving boost 改变整体音色。

但真实音频的问题往往是混合的。例如，一段人声录音可能同时存在：

- 低频震动；
- 电源 hum；
- 某个房间共振；
- 高频 hiss；
- 人声不够清晰。

这时就需要多个滤波器组合。

### 1.2 Cascading filters

**Cascading filters（级联滤波器）**指把多个滤波器串联起来：

```text
input audio → filter 1 → filter 2 → filter 3 → output audio
```

例如一个常见语音清理链：

```text
High-pass → Notch → Peaking cut → Gentle high-shelf
```

它们分别负责：

| 滤波器 | 作用 |
|---|---|
| High-pass | 去低频 rumble 和 DC offset |
| Notch | 去 50/60 Hz 电源 hum |
| Peaking cut | 去房间共振或刺耳频段 |
| High-shelf | 轻微增加清晰度和空气感 |

### 1.3 Narrowband peaking filters 的作用

课件强调，narrowband peaking filters 常用于处理非常具体的频率问题，例如：

- resonances；
- microphone feedback；
- unwanted tones；
- 某个窄频率的电气噪声。

它们的优点是精准，但风险是容易过度处理。如果 Q 值太高或 cut 太深，声音可能变得不自然。

### 1.4 为什么要避免过大 boost 或 cut

课件提醒：超过 12 dB 的变化可能导致 distortion 或 amplifier overload。

这是因为大幅增益会显著提升某些频率的振幅。如果系统没有足够 headroom，就会出现：

- clipping；
- distortion；
- amplifier overload；
- loudspeaker overload；
- 噪声被一起放大；
- 声音频谱严重失衡。

> [!warning] 实用原则
> EQ 调整通常建议“小幅、多次、边听边改”。如果你需要对某个频段做非常大的提升，往往说明录音、麦克风位置、声源或前级处理本身可能存在问题。

---

## 2. Gain in dB：分贝增益如何换算？

### 2.1 dB 与线性幅度增益

课件给出公式：

$$
G = 10^{\frac{dB}{20}}
$$

其中：

- $G$ 是线性 amplitude gain；
- $dB$ 是分贝增益。

为什么分母是 20？因为这里讨论的是 amplitude ratio，而不是 power ratio。功率比常用 $10\log_{10}$，幅度比常用 $20\log_{10}$。

### 2.2 +6 dB 和 -6 dB

课件给出两个常用近似：

```text
+6 dB → G ≈ 2
-6 dB → G ≈ 0.5
```

也就是说：

- +6 dB 约等于振幅翻倍；
- -6 dB 约等于振幅减半。

### 2.3 例题 1：-6 dB cut

题目：A -6 dB cut is applied to a signal. Calculate the corresponding linear amplitude gain.

公式：

$$
G = 10^{\frac{-6}{20}}
$$

$$
G = 10^{-0.3} \approx 0.5
$$

所以 -6 dB cut 约等于把振幅变成原来的 0.5。

### 2.4 例题 2：+3 dB boost

题目：An audio signal is boosted by +3 dB. Estimate the corresponding linear gain.

$$
G = 10^{\frac{3}{20}}
$$

$$
G = 10^{0.15} \approx 1.41
$$

所以 +3 dB boost 约等于振幅乘以 1.41。

> [!note] 注意
> +3 dB 经常被理解为“功率大约翻倍”，但幅度不是翻倍，幅度约为 1.41 倍。

### 2.5 例题 3：+12 dB boost

题目：An engineer applies a +12 dB boost to a frequency band. Estimate the linear gain.

$$
G = 10^{\frac{12}{20}}
$$

$$
G = 10^{0.6} \approx 4
$$

所以 +12 dB 约等于振幅乘以 4。

### 2.6 +12 dB 为什么危险？

+12 dB 会让某个频段的振幅约变成 4 倍。这可能导致：

- 音频明显变大；
- 某些频段突出到不自然；
- clipping；
- distortion；
- amplifier overload；
- 音质下降。

> [!important] 记忆
> +12 dB 不是“小小增强”，它在线性幅度上约等于 4 倍，已经是非常大的处理。

---

## 3. Digital Filtering：数字滤波的用途

### 3.1 数字滤波能做什么？

课件指出，digital filtering 可以精确控制特定频率范围。

主要用途包括：

| 用途 | 说明 |
|---|---|
| Noise reduction | 去除 hum、hiss、rumble 等噪声 |
| Equalisation | 改变 tonal balance，塑造音色 |
| Audio effects | 创造特殊音效，如电话声、空间感、滤波扫频 |
| Artifact cleanup | 清理压缩、分离、降噪后残留的伪影 |

### 3.2 关键滤波器参数

课件列出两个核心参数：

1. **Cutoff frequency**
2. **Filter order**

#### Cutoff frequency

Cutoff frequency 是滤波器开始明显 attenuate signal 的频率点。

例如：

- high-pass cutoff = 80 Hz：80 Hz 以下逐渐被削弱；
- low-pass cutoff = 12 kHz：12 kHz 以上逐渐被削弱。

#### Filter order

Filter order 决定 transition 的 sharpness，也就是从 passband 到 stopband 的过渡有多陡。

一般来说：

- order 越高，过渡越陡；
- order 越低，过渡越平缓。

但高阶滤波器不一定总是更好，因为它可能增加计算复杂度、相位问题、延迟或不自然听感。

---

## 4. Tone Control、Parametric EQ 和 Graphic EQ

这一页是本组课件的重点之一，因为它把“滤波器理论”连接到实际 EQ 系统。

### 4.1 Equalisation 是什么？

**Equalisation（均衡）**是有意修改系统 frequency response 的过程。

它可以用于两类目的：

| 目的 | 例子 |
|---|---|
| Correction | 修正房间、麦克风、扬声器或录音问题 |
| Creative tone shaping | 让声音更亮、更暖、更厚、更有 presence |

### 4.2 Tone-control equalisers

Tone-control EQ 是最简单的均衡器，通常只有两到三个宽频段：

- bass；
- mid；
- treble。

优点：

- 简单直观；
- 操作容易；
- 适合普通播放设备。

缺点：

- 控制不精确；
- 频段很宽；
- 很难修复具体问题频率。

例如，调高 treble 会让整体高频变亮，但它不能精准处理某个 5 kHz 的刺耳共振。

### 4.3 Parametric equaliser

**Parametric EQ（参数均衡器）**使用可调 IIR filters，通常可以控制：

- centre frequency；
- bandwidth / Q；
- gain。

优点：

- 精准；
- 可以针对具体频点；
- 适合专业混音、修音和声学修正。

例如：

```text
Peaking filter: centre = 250 Hz, Q = 4, gain = -3 dB
```

这表示在 250 Hz 附近做一个相对窄的削弱。

### 4.4 Graphic equaliser

**Graphic EQ（图示均衡器）**由一排固定频率的 slider 构成。每个 slider 控制一个固定频带。

例如常见的 10-band graphic EQ 可能有：

```text
31 Hz, 63 Hz, 125 Hz, 250 Hz, 500 Hz, 1 kHz, 2 kHz, 4 kHz, 8 kHz, 16 kHz
```

用户看到的是一条“频率响应曲线”的形状，所以叫 graphic EQ。

### 4.5 Graphic EQ 的实现方式

课件提到 graphic EQ 可以用两种方式实现：

1. **Single FIR filter**
2. **Multiple IIR filters**

#### 用 FIR 实现

优点：

- 可以更接近 desired response；
- 可以实现 linear phase；
- 频谱塑形更精确。

缺点：

- 需要较长 tap length；
- delay 较大；
- 实时更新较困难。

#### 用多个 IIR filters 实现

优点：

- 低延迟；
- 计算效率高；
- 适合 real-time control。

缺点：

- 只能近似 target response；
- 会引入 phase distortion；
- 多个 band 之间会互相影响。

---

## 5. Multiple EQ Bands 的限制

### 5.1 频段重叠

课件特别提醒：EQ 中的 frequency bands often overlap。

这意味着：

```text
调整一个 band，不只影响这个 band，也会影响邻近频率。
```

### 5.2 为什么 band 不是独立的？

现实滤波器的频率响应不是一条垂直边界。每个 band 都有一定宽度和过渡区域。

所以当你提升 1 kHz band 时，可能也会影响：

- 800 Hz；
- 1.2 kHz；
- 甚至更宽区域。

### 5.3 这带来的问题

频段重叠会导致：

- 实际响应偏离理想响应；
- 调整一个 slider 后，邻近声音也变化；
- 多次调整后频谱变得复杂；
- 很难精确预测最终声音。

> [!tip] 实用方法
> 使用 EQ 时不要只看单个 band 的数值，要观察整体 frequency response，并反复听 A/B 对比。

---

## 6. Digital Audio Signal Equalisation：实时与离线均衡

### 6.1 数字均衡的优势

课件指出，digital audio equalisation 可以用于：

- real-time playback；
- post-production；
- pre-recorded signal processing。

与模拟滤波相比，数字滤波可以在录音之后继续处理，灵活性更高。

### 6.2 Real-time EQ 的要求

对于 real-time operation，每个 sample 都必须在一个 sampling period 内处理完成。

这意味着实时 EQ 必须满足：

| 要求 | 解释 |
|---|---|
| Causal | 只能用当前和过去 samples，不能依赖未来 samples |
| Low group delay | 延迟要低，否则用户会听到滞后 |
| Smooth parameter changes | 参数变化要平滑，避免 clicks 或 zipper noise |
| Stable | 滤波器不能发散或引起爆音 |

### 6.3 Real-time EQ 为什么常用 IIR？

课件指出，real-time equalisers 通常用 cascaded 或 parallel second-order IIR filters。

原因：

- IIR 计算效率高；
- 低延迟；
- 参数更新相对方便；
- 少量系数就能实现较陡响应。

常见形式是 biquad filters（二阶 IIR 滤波器），可以组合成多段 EQ。

### 6.4 Offline processing 的优势

如果音频已经录好，就不受实时延迟限制。

这时可以使用：

- non-causal filters；
- 更长 FIR filters；
- zero-phase filtering；
- 更复杂的优化算法；
- 更准确的频谱匹配。

因此：

```text
real-time systems → low latency and stability
offline processing → accuracy and flexibility
```

---

## 7. FIR 与 IIR 滤波器对比

### 7.1 FIR filter

**FIR（Finite Impulse Response）**滤波器的 impulse response 是有限长度的。

优点：

- 可以实现 linear phase；
- 稳定性好；
- 频谱塑形准确；
- 适合 offline 或 buffered applications。

缺点：

- 要实现锐利响应通常需要很多 taps；
- latency 较大；
- 实时参数更新不方便；
- computational cost 较高。

### 7.2 IIR filter

**IIR（Infinite Impulse Response）**滤波器有反馈结构，impulse response 理论上无限长。

优点：

- 低延迟；
- 计算效率高；
- 适合 real-time EQ；
- 少量阶数即可实现较强滤波效果。

缺点：

- 可能引入 phase distortion；
- 稳定性需要注意；
- 频率响应不一定完全符合目标曲线。

### 7.3 选择规则

| 场景 | 更适合 |
|---|---|
| 实时语音通话、直播、现场调音 | IIR |
| 离线母带处理、精确频响匹配、线性相位要求 | FIR |
| 低延迟优先 | IIR |
| 相位线性和准确性优先 | FIR |

### 7.4 FIR 的高级实现

课件提到 FIR filters 可用：

- windowing；
- inverse FFT methods。

但长 FIR 会带来计算和延迟压力，因此可能需要：

- multirate processing；
- FFT partitioning。

这些方法用于降低长滤波器的实时计算成本。

---

## 8. Filtering in Complex Audio Processing：滤波与 PCA/ICA

### 8.1 滤波不只是简单去噪

课件强调：filtering is not only used for simple noise removal，它也常出现在更高级的处理系统中。

例如：

- source separation；
- PCA denoising；
- ICA source extraction；
- speech enhancement；
- artifact removal。

### 8.2 PCA/ICA 前的 filtering

在 PCA 或 ICA 之前做 filtering 属于 **pre-processing filtering**。

目的：

- 改善输入信号质量；
- 去掉明显无用噪声；
- 避免噪声影响统计模型；
- 优化 PCA/ICA 的输入数据。

常见操作：

| 操作 | 作用 |
|---|---|
| Low-pass before downsampling | 防止 aliasing |
| High-pass | 去 DC offset 和超低频 rumble |
| Notch | 去电源 hum |
| Band-pass | 保留目标频率范围 |

### 8.3 为什么 downsampling 前要 low-pass？

如果降低采样率，新的 Nyquist frequency 会变低。原信号中高于新 Nyquist frequency 的频率会 alias 到低频，造成不可逆失真。

因此 downsampling 前要先 low-pass：

```text
remove high frequencies above new Nyquist limit → downsample safely
```

### 8.4 为什么 ICA/PCA 前要 high-pass？

低频 rumble 或 DC offset 可能占据大量能量，但它们不一定是有用信息。

如果不去除，它们可能：

- 主导 PCA 的方差方向；
- 干扰 ICA 的独立性估计；
- 降低源分离效果；
- 让后续模型关注错误结构。

---

## 9. PCA/ICA 后的 filtering

### 9.1 Post-processing filtering

在 PCA/ICA 之后，分离或重构出的信号可能仍然存在：

- residual noise；
- distortion；
- tonal imbalance；
- separation artifacts；
- periodic artifacts。

这时需要 post-processing filtering。

### 9.2 后处理滤波的目标

课件列出几个目标：

- remove remaining noise or distortion；
- refine frequency balance；
- avoid introducing new artifacts；
- prevent over-filtering。

### 9.3 常见后处理方法

| 方法 | 用途 |
|---|---|
| Low-pass filtering | 去高频噪声 |
| Band-stop / notch | 去固定 tones 或 hums |
| Wiener filtering | 动态估计噪声并抑制 |
| Spectral subtraction | 从频谱中减去噪声估计 |
| Band-pass filtering | 隔离目标频段 |
| Equalization | 调整 tonal balance |
| Comb filters | 去周期性 artifacts |
| Dynamic filters | 处理 time-varying noise |

### 9.4 Over-filtering 的风险

课件提醒：careful use avoids introducing new artifacts。

过度滤波可能导致：

- 声音不自然；
- 频率空洞；
- 语音发闷或发薄；
- music 失去空间感；
- 出现 phase artifacts；
- source separation 的残留伪影更加明显。

> [!important] 实用原则
> 后处理滤波的目标不是让频谱“看起来干净”，而是让最终声音在目标任务中更有用、更自然、更可听。

---

## 10. Audio Quality：什么是音频质量？

课件把 audio quality 定义为 sound reproduction 的 accuracy and fidelity。

可以从几个方面理解。

### 10.1 Frequency response

**Frequency response** 表示系统能再现哪些频率，以及不同频率是否被均匀再现。

人耳通常可听范围大约是：

```text
20 Hz - 20 kHz
```

但设备不一定能完整、平坦地再现这个范围。例如：

- 小扬声器低频不足；
- 廉价麦克风高频不平滑；
- 房间声学导致某些频率被增强或削弱。

### 10.2 Dynamic range

**Dynamic range** 是最响声音和最安静声音之间的范围。

动态范围不足会导致：

- 安静细节听不见；
- 大声部分容易失真；
- 音乐表现力下降；
- 语音细节损失。

### 10.3 Signal-to-Noise Ratio

**SNR** 表示有用信号相对于背景噪声的强度。

SNR 越高，通常说明声音越干净。

### 10.4 设备限制

不同设备会限制 audio quality：

- microphone self-noise；
- amplifier distortion；
- speaker frequency response；
- ADC/DAC quality；
- room acoustics；
- codec compression artifacts。

所以 audio quality 不只是文件本身的问题，也与整个 recording/playback chain 有关。

---

## 11. Understanding Noise：噪声来源与影响

### 11.1 噪声定义

课件定义 noise 为：

> unwanted sound interfering with the desired signal

也就是干扰目标声音的无用声音。

### 11.2 常见噪声来源

| 噪声类型 | 例子 |
|---|---|
| Environmental noise | traffic, conversations, machinery |
| Electrical noise | hum, hiss, static |
| Self-noise | equipment-generated noise |

### 11.3 噪声的影响

噪声会影响：

- clarity；
- intelligibility；
- analysis accuracy；
- source separation；
- feature extraction；
- ML model performance；
- perceived quality。

例如，在语音识别中，背景噪声可能导致识别错误；在 ICA 中，噪声可能影响独立成分估计；在音乐中，hiss 会降低听感质量。

---

## 12. Subjective Measurements：主观听感评价

### 12.1 为什么需要主观评价？

音频最终是给人听的。客观指标很重要，但它们不一定完全等同于人的听感。

例如：

- 两个音频的 MSE 差不多，但一个听起来更自然；
- SNR 提高了，但语音可能变得机械；
- 降噪很强，但音乐细节被抹掉。

因此需要 listening tests。

### 12.2 Double-blind tests

**Double-blind test（双盲测试）**中，听众和测试执行者都不知道样本身份，以减少偏见。

目的：

- 减少品牌、算法名称、预期心理影响；
- 提高评价可信度。

### 12.3 ABX tests

ABX test 中：

- A 是 reference；
- B 是另一个 sample；
- X 是 A 或 B 中的一个；
- 听众要判断 X 是 A 还是 B。

ABX 常用于判断两个音频是否能被听出差异，例如：

- 无损 vs 有损；
- 原始音频 vs 处理后音频；
- 不同 codec；
- 不同 bitrate。

### 12.4 Paired comparison tests

Paired comparison 中，听众比较两个样本，选择哪个更好。

它适合基于某个标准判断：

- 哪个更清晰；
- 哪个噪声更少；
- 哪个更自然；
- 哪个更接近 reference。

### 12.5 Mean Opinion Score（MOS）

**MOS** 是听众对质量打分的平均值，常见 1-5 分：

| 分数 | 含义 |
|---:|---|
| 1 | poor |
| 2 | bad / annoying |
| 3 | fair |
| 4 | good |
| 5 | excellent |

MOS 常用于语音质量、通信系统和主观音质评价。

### 12.6 Perceived loudness 与 LUFS

音频比较时必须控制 loudness，否则更响的样本往往会被误认为更好。

常用 loudness 单位包括 LUFS。

使用 loudness matching 可以避免响度差异干扰质量判断。

### 12.7 Timbral attributes

专家听众可能评价更细的 timbral attributes，例如：

- brightness；
- warmth；
- clarity；
- harshness；
- fullness；
- naturalness。

这类评价更接近音乐制作和声音设计中的真实需求。

---

## 13. Objective Metrics：为什么需要客观指标？

课件指出，listening tests 是 subjective and time-consuming。

客观指标的优势：

| 优势 | 解释 |
|---|---|
| Repeatability | 同样输入得到同样结果 |
| Consistency | 不受听众疲劳、偏好影响 |
| Automation | 可以批量评估大量音频 |
| Fast iteration | 方便调参和比较算法 |

但客观指标也有局限：它们不一定完全预测人的听感。因此实际研究常结合主观和客观评价。

---

## 14. SNR：Signal-to-Noise Ratio

### 14.1 定义

**SNR** 是 desired signal power 与 noise power 的比值。

公式：

$$
SNR(dB)=10\log_{10}\left(\frac{P_{signal}}{P_{noise}}\right)
$$

其中：

- $P_{signal}$：目标信号功率；
- $P_{noise}$：噪声功率。

### 14.2 如何理解 SNR

- SNR 高：信号远强于噪声，音频更干净；
- SNR 低：噪声接近或超过信号，质量差。

### 14.3 SNR 的用途

SNR 常用于评估：

- noise reduction effectiveness；
- processing 前后噪声改善；
- recording quality；
- enhancement algorithm performance。

### 14.4 前后对比

如果做降噪，可以比较：

```text
SNR before processing
SNR after processing
```

若 SNR 提高，说明噪声相对减少。但仍要听声音，因为过强降噪可能损伤有用信号。

---

## 15. THD：Total Harmonic Distortion

### 15.1 定义

**THD（总谐波失真）**衡量系统向原信号添加了多少不需要的 harmonics。

公式：

$$
THD(\%)=\frac{RMS\ value\ of\ harmonics}{RMS\ value\ of\ fundamental}\times100
$$

### 15.2 什么是 harmonic distortion？

如果输入是一个纯 1 kHz sine wave，理想系统输出仍应只有 1 kHz。

如果系统产生了：

```text
2 kHz, 3 kHz, 4 kHz...
```

这些就是 harmonics。

### 15.3 THD 的用途

THD 可用于判断：

- 滤波或增益是否引入失真；
- 放大器是否过载；
- speaker 是否在非线性工作；
- 处理算法是否破坏 fidelity。

THD 越低，通常表示保真度越好。

---

## 16. IMD：Intermodulation Distortion

### 16.1 定义

**IMD（互调失真）**衡量多个频率之间相互作用产生的新频率成分。

如果输入有两个频率 $f_1$ 和 $f_2$，非线性系统可能产生：

```text
f1 + f2
f1 - f2
2f1 - f2
2f2 - f1
...
```

这些都不是原始输入中的频率。

### 16.2 为什么 IMD 重要？

音乐和语音通常包含很多频率。如果系统非线性，频率之间会互相“制造”新成分，听起来可能：

- 浑浊；
- 刺耳；
- 不透明；
- 不自然。

### 16.3 IMD 的用途

IMD 可用于检查处理是否引入 unwanted frequency interactions。

IMD 越低，说明声音越干净。

---

## 17. MSE 和 RMSE

### 17.1 MSE 定义

**MSE（Mean Squared Error）**衡量 processed audio 与 reference audio 之间的平均平方差。

公式：

$$
MSE=\frac{1}{N}\sum_{i=1}^{N}(original[i]-processed[i])^2
$$

### 17.2 RMSE 定义

**RMSE（Root Mean Square Error）**是 MSE 的平方根：

$$
RMSE=\sqrt{MSE}
$$

### 17.3 如何理解

- MSE/RMSE 低：processed audio 更接近 reference；
- MSE/RMSE 高：差异更大。

### 17.4 使用条件

MSE/RMSE 需要 reference audio。如果没有干净原始信号，就无法直接计算。

### 17.5 局限

MSE/RMSE 是 sample-level error，不完全符合听感。

例如，一个很小的时间偏移可能导致 MSE 很大，但听起来差异不明显。因此音频评价中常结合 perceptual metrics。

---

## 18. PSNR：Peak Signal-to-Noise Ratio

### 18.1 定义

**PSNR** 衡量 maximum possible signal power 与 noise/error power 的比值。

公式：

$$
PSNR(dB)=20\log_{10}\left(\frac{MAX_{signal}}{RMS_{error}}\right)
$$

其中：

- $MAX_{signal}$：信号最大可能值；
- $RMS_{error}$：processed 与 original 之间的 RMS error。

### 18.2 用途

PSNR 常用于：

- degradation compared to clean reference；
- fidelity measurement；
- processed audio 与 reference 的接近程度。

PSNR 越高，通常表示 degradation 越小。

### 18.3 局限

和 MSE 一样，PSNR 也不完全等于人的听感质量。它适合有 reference 的误差评估，但不一定适合判断“好不好听”。

---

## 19. PEAQ：Perceptual Evaluation of Audio Quality

### 19.1 PEAQ 是什么？

**PEAQ** 是一种标准化算法，用 psychoacoustic model 预测音频感知质量。

它会比较 reference 和 degraded signal，并根据人耳听觉模型估计质量损伤。

### 19.2 ODG

PEAQ 常输出 ODG（Objective Difference Grade），范围通常为：

```text
0：imperceptible difference
-4：very annoying
```

越接近 0，说明感知差异越小。

### 19.3 用途

PEAQ 适合评价：

- codec transparency；
- processing artifacts；
- music/general audio quality；
- PCA/ICA 后处理对整体听感的影响。

### 19.4 注意

PEAQ 没有一个简单公式，它是复杂听觉模型的组合。

---

## 20. POLQA：语音质量评价

### 20.1 POLQA 是什么？

**POLQA（Perceptual Objective Listening Quality Assessment）** 是用于 speech quality 的客观评价算法。

它常用于通信系统，例如：

- telephone speech；
- VoIP；
- speech enhancement；
- mobile communication。

### 20.2 分数范围

POLQA 分数通常类似 MOS：

```text
1 = very poor
5 = excellent
```

分数越高，语音质量越好。

### 20.3 用途

在本课程语境中，POLQA 可用于评价：

- speech denoising；
- ICA/PCA 后语音清晰度；
- communication audio processing；
- intelligibility improvement。

---

## 21. ViSQOL

### 21.1 ViSQOL 是什么？

**ViSQOL（Virtual Speech Quality Objective Listener）** 是一种客观感知质量指标，用于预测 speech/audio quality。

课件强调它对 time misalignments 比较 robust。

### 21.2 分数范围

ViSQOL 分数通常在：

```text
0 - 1
```

越接近 1，质量越好。

### 21.3 用途

ViSQOL 适合在 timing 可能被处理改变时使用，例如：

- source separation；
- speech enhancement；
- time-domain processing；
- alignment 不完全精确的处理结果。

---

## 22. SDR：Signal-to-Distortion Ratio

### 22.1 定义

**SDR（Signal-to-Distortion Ratio）**衡量输出中真实目标信号相对于总 distortion 的比例。

这里的 distortion 可以包括：

- noise；
- artifacts；
- interference；
- separation errors。

### 22.2 为什么 SDR 重要？

课件指出 SDR 是 BSS Eval、source separation 和 denoising benchmarks 中常用的 headline score。

直观理解：

```text
SDR 越高 → 输出越干净，目标信号占比越高
```

例如：

- 0 dB：signal 和 distortion 能量相当；
- +20 dB：通常已经比较透明。

### 22.3 和 SIR/SAR 的关系

SDR 可以搭配：

- SIR：Signal-to-Interference Ratio；
- SAR：Signal-to-Artifacts Ratio；
- perceptual metrics：ViSQOL、PESQ 等。

这样可以知道错误来自哪里：

- 是其他 source 干扰？
- 是算法 artifacts？
- 是噪声残留？

---

## 23. Amari Error

### 23.1 为什么 ICA 需要 Amari Error？

ICA 的结果存在两个 ambiguity：

- scaling ambiguity；
- permutation ambiguity。

也就是说，即使 ICA 分离得很好，输出源的顺序和幅度也可能与原始源不同。

因此直接比较矩阵元素并不公平。

### 23.2 Amari Error 的作用

**Amari Error** 用来比较 estimated mixing/demixing matrix 与 true matrix，同时抵消 row scaling 和 permutation ambiguity。

它特别适合评价 ICA 或 BSS 算法。

### 23.3 如何解释数值

课件强调：

```text
Amari Error = 0 → perfect source separation
```

数值越接近 0，说明估计越接近理想分离。

---

## 24. 如何选择音频质量评价指标？

课件给出一个明确流程。

### Step 1：Define the purpose

先问：你到底要评价什么？

可能目标包括：

- codec transparency；
- equipment performance；
- loudspeaker design；
- noise reduction effectiveness；
- source separation quality；
- speech enhancement quality。

不同目标对应不同指标。

### Step 2：Choose the right tools

工具可以分为：

- subjective listening tests；
- objective metrics；
- audio analysis software/hardware；
- DAW plugins；
- research evaluation toolkits。

### Step 3：Set up controlled environment

主观测试和客观测量都需要稳定条件：

- consistent listening conditions；
- level matching；
- calibrated equipment；
- low external noise；
- acoustically treated room if possible。

### Step 4：Conduct tests

主观测试要注意：

- multiple listeners；
- unbiased setup；
- randomization；
- double-blind where possible。

客观测试要注意：

- consistent runs；
- averaged results；
- repeatability；
- same input/output alignment。

### Step 5：Analyze and interpret

不要只看一个指标。需要结合：

- subjective feedback；
- objective metrics；
- spectrogram；
- task performance；
- listening context。

如果出现矛盾，例如客观指标好但听起来差，就需要考虑 psychoacoustic effects 或 artifact 类型。

### Step 6：Iterate

音频处理通常是迭代过程：

```text
process → evaluate → adjust → retest
```

只有重新测试才能确认改动是否真的有效。

---

## 25. 不同任务应该选什么指标？

### 25.1 Noise reduction

推荐指标：

- SNR；
- PEAQ；
- MSE/RMSE if reference available；
- ViSQOL/POLQA if speech。

解释：SNR 直接衡量噪声减少，PEAQ/POLQA/ViSQOL 判断感知质量是否改善。

### 25.2 Artifact removal / source separation

推荐指标：

- SDR；
- SIR；
- SAR；
- THD；
- IMD；
- RMSE/MSE if reference available；
- Amari Error if true mixing matrix is known。

解释：source separation 不只是看噪声，还要看 interference 和 artifacts。

### 25.3 Speech enhancement

推荐指标：

- POLQA；
- ViSQOL；
- PESQ；
- intelligibility-related listening tests；
- SNR as auxiliary metric。

解释：语音任务更关注 intelligibility 和 naturalness。

### 25.4 Music / general audio

推荐指标：

- PEAQ；
- SNR；
- THD；
- IMD；
- subjective listening tests；
- ABX if comparing codecs。

### 25.5 有 reference 和无 reference 的区别

| 情况 | 可用指标 |
|---|---|
| Reference available | PSNR、RMSE/MSE、PEAQ、POLQA、ViSQOL、THD/IMD、SDR |
| No reference | SNR with noise estimation、THD、IMD、no-reference perceptual estimates、subjective tests |

> [!important] 选择指标的关键
> 先看任务目标，再看是否有 reference signal，最后看音频类型是 speech、music 还是 general audio。

---

## 26. 研究论文中常见指标

课件最后列出了一些研究中使用的指标，说明不同领域会采用不同评价方法。

### 26.1 Blind audio source separation

Vincent, Gribonval, Févotte 等关于 BSS performance measurement 的工作使用：

- PESQ；
- SNR；
- SIR；
- SAR。

这些指标分别关注语音感知质量、噪声、干扰和 artifacts。

### 26.2 ICA algorithms

在 crackle sounds 的 ICA 分析中，可能使用：

- Amari Error；
- SIR。

因为 ICA 评价常关心源分离矩阵是否正确，以及干扰抑制程度。

### 26.3 Target sound extraction

SoundBeam 等目标声音提取研究可能使用：

- SI-SDR；
- SDR improvement。

SI-SDR 是 scale-invariant SDR，更适合处理输出尺度不确定的任务。

### 26.4 Speech emotion recognition / dimensionality reduction

相关研究可能使用：

- accuracy；
- precision；
- recall；
- F-score；
- Cohen's Kappa；
- Matthews Correlation Coefficient。

这说明如果音频处理的最终目标是分类或识别，就要使用 machine learning evaluation metrics。

---

## 27. 课件逐页理解

### Page 1：标题页

主题是 Audio Quality, Noise, and Digital Filtering。说明本节延续滤波与噪声主题，但会进一步讨论质量评价。

### Page 2：Shelving and Peaking Filter Composition

复习 shelving 与 peaking filters 可以组合使用，并强调 cascading filters、narrowband correction 和避免大幅 boost/cut。

### Pages 3-8：Gain in dB 与练习

讲 dB 到线性 amplitude gain 的换算：

$$
G=10^{dB/20}
$$

重点例子：

- -6 dB → 0.5；
- +3 dB → 1.41；
- +12 dB → 4。

并说明大增益会导致 clipping、distortion 和 overload。

### Pages 9-10：Digital Filtering 与参数

数字滤波用于 noise reduction、EQ、audio effects 和 artifact cleanup。重要参数是 cutoff frequency 和 filter order。

### Pages 11-14：EQ、FIR 和 IIR

介绍 tone-control EQ、parametric EQ、graphic EQ，并比较 FIR 与 IIR 的实现差异。

重点：实时系统偏向 IIR，离线/高精度系统可偏向 FIR。

### Pages 16-21：Filtering in Complex Audio Processing

解释滤波可以用于 PCA/ICA 前后：

- 前处理改善输入；
- 后处理清理残余噪声和 artifacts；
- 与 source separation 和 denoising 系统结合。

### Pages 22-23：Audio Quality 与 Noise

定义音频质量、频率响应、动态范围、SNR、人耳范围和常见噪声来源。

### Pages 24-25：Subjective Measurements

讲 double-blind、ABX、paired comparison、MOS、loudness matching、timbral attributes。

### Pages 26-37：Objective Metrics

系统介绍 SNR、THD、IMD、MSE/RMSE、PSNR、PEAQ、POLQA、ViSQOL、SDR、Amari Error。

### Pages 38-41：测量流程与指标选择

说明应从目标出发，选择合适工具，设置受控环境，进行测试，分析结果，再迭代改进。

### Pages 42-44：Research metrics 与总结

通过论文例子说明真实研究会根据任务选择指标，例如 SIR/SAR、SI-SDR、accuracy、F1、MCC 等。

### Page 45：Reference

参考书：Digital Audio Processing Fundamentals - Aurelio Uncini。

---

## 28. 考试/复习重点

### 28.1 必须掌握的公式

#### dB 转线性幅度增益

$$
G=10^{\frac{dB}{20}}
$$

#### SNR

$$
SNR(dB)=10\log_{10}\left(\frac{P_{signal}}{P_{noise}}\right)
$$

#### THD

$$
THD(\%)=\frac{RMS\ harmonics}{RMS\ fundamental}\times100
$$

#### PSNR

$$
PSNR(dB)=20\log_{10}\left(\frac{MAX_{signal}}{RMS_{error}}\right)
$$

#### MSE / RMSE

$$
MSE=\frac{1}{N}\sum_{i=1}^{N}(original[i]-processed[i])^2
$$

$$
RMSE=\sqrt{MSE}
$$

### 28.2 必须会解释的概念

- shelving / peaking filter composition；
- gain in dB 与线性增益换算；
- cutoff frequency；
- filter order；
- tone-control EQ、parametric EQ、graphic EQ；
- multiple EQ bands overlap；
- real-time EQ 的限制；
- FIR vs IIR；
- PCA/ICA 前后 filtering；
- audio quality；
- noise sources；
- subjective vs objective measurements；
- SNR、THD、IMD、MSE/RMSE、PSNR；
- PEAQ、POLQA、ViSQOL；
- SDR、Amari Error；
- 如何根据任务选指标。

---

## 29. 常见问答

### Q1. +12 dB boost 对线性振幅意味着什么？

$$
G=10^{12/20}=10^{0.6}\approx4
$$

也就是振幅约变成 4 倍，因此容易造成 clipping、distortion 或 overload。

### Q2. Parametric EQ 和 graphic EQ 有什么区别？

Parametric EQ 可以调 centre frequency、bandwidth/Q 和 gain，更精准。Graphic EQ 使用固定频率的 sliders，更直观但控制灵活性较低。

### Q3. 为什么 graphic EQ 的 bands 不独立？

因为滤波器频率响应会重叠。调整一个 band 会影响邻近频率，所以最终响应可能偏离理想曲线。

### Q4. Real-time EQ 为什么常用 IIR？

IIR 计算效率高、延迟低、适合实时参数更新。FIR 虽然可线性相位且更准确，但长 FIR 会引入较大延迟和计算量。

### Q5. PCA/ICA 前为什么要滤波？

为了改善输入质量，去除明显噪声、DC offset、低频 rumble 或 aliasing 风险，使 PCA/ICA 更关注真正有用的信号结构。

### Q6. PCA/ICA 后为什么还要滤波？

分离后的信号可能仍有残余噪声、频谱不平衡或 artifacts。后处理滤波可以进一步改善听感和质量。

### Q7. SNR 高是否一定代表听起来好？

不一定。SNR 只衡量信号与噪声功率比，不一定反映失真、伪影、自然度或人耳感知质量。因此常需结合 PEAQ、POLQA、ViSQOL 或主观测试。

### Q8. 有 reference signal 时优先用哪些指标？

可以使用 PSNR、MSE/RMSE、PEAQ、POLQA、ViSQOL、SDR 等。是否选择 speech-specific 指标取决于音频类型。

### Q9. 没有 reference signal 怎么评价？

可以用噪声估计下的 SNR、THD、IMD、主观听感测试、no-reference 模型，或根据任务使用分类/识别指标。

### Q10. Amari Error 用来评价什么？

它主要用于 ICA/BSS，评价估计的 mixing/demixing matrix 与真实矩阵的接近程度，同时处理 scaling 和 permutation ambiguity。

---

## 30. 一页速记

> [!summary] Block 4 第 1 组 PPT 速记
> - dB 到线性幅度：$G=10^{dB/20}$。
> - -6 dB ≈ 0.5，+3 dB ≈ 1.41，+12 dB ≈ 4。
> - +12 dB 是大幅 boost，可能导致 clipping、distortion、overload。
> - Digital filtering 用于 noise reduction、EQ、effects、artifact cleanup。
> - Cutoff frequency 决定从哪里开始 attenuate。
> - Filter order 决定 transition 有多 sharp。
> - Tone-control EQ 简单但粗略；parametric EQ 精准；graphic EQ 直观但 bands 会重叠。
> - FIR：linear phase、准确，但延迟高；IIR：低延迟、实时友好，但有 phase distortion。
> - PCA/ICA 前滤波用于改善输入；PCA/ICA 后滤波用于清理残余噪声和 artifacts。
> - Audio quality 包括 frequency response、dynamic range、SNR、fidelity。
> - 主观评价：double-blind、ABX、paired comparison、MOS。
> - 客观评价：SNR、THD、IMD、MSE/RMSE、PSNR、PEAQ、POLQA、ViSQOL、SDR、Amari Error。
> - 指标选择要看：目标、是否有 reference、音频类型、算法任务。

---

## 31. 和后续课程的连接

- 与 Block 3 的连接：本节继续使用滤波、PCA、ICA、source separation 等概念，但更强调应用和评价。
- 与 Block 4 后续 ML 内容的连接：音频机器学习模型需要高质量输入，也需要合适指标评价输出。
- 与 ethics / forensic 内容的连接：音频处理不仅要“效果好”，还要知道处理是否引入伪影、是否影响真实性、是否可解释。
- 与实验/作业的连接：如果报告中使用降噪、分离或增强算法，需要说明选择了哪些质量指标以及为什么。
