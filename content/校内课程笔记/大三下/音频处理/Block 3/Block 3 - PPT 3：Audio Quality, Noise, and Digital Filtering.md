---
title: EBU5408 Block 3 - PPT 3：Audio Quality, Noise, and Digital Filtering
aliases:
  - Block 3 PPT 3
  - Audio Quality Noise and Digital Filtering
  - Digital Audio Filter Noise Introduction
  - Audio Filter and Quality
tags:
  - course/音频处理
  - EBU5408
  - digital-audio
  - block3
  - audio-filter
  - noise
  - equaliser
source:
  - "[[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/3 Audio Filter and Quality/Digital Audio Filter Noise Introduction.pdf]]"
created: 2026-06-17
---

# Block 3 - PPT 3：Audio Quality, Noise, and Digital Filtering

> [!info] 课件来源
> 本笔记对应 Block 3 第 3 组课件：
> - [[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/3 Audio Filter and Quality/Digital Audio Filter Noise Introduction.pdf]]
>
> 这组 PPT 是 Block 3 中从“压缩、PCA/ICA 分析”过渡到“音频质量、噪声与滤波”的部分。它重点讲：为什么要修改音频频谱、不同滤波器如何影响声音、以及实际调音/降噪时应该如何选择滤波器。

## 0. 本组 PPT 的核心作用

前两组课件分别讲了：

- [[课程笔记/音频处理/Block 3/Block 3 - PPT 1：Compression and Decompression|PPT 1：音频压缩与解压缩]]：如何减少数据量；
- [[课程笔记/音频处理/Block 3/Block 3 - PPT 2：PCA and ICA|PPT 2：PCA 与 ICA]]：如何从复杂音频中提取结构、降噪或分离声源。

第 3 组课件则开始进入更直接的 **audio quality enhancement（音频质量提升）**：

1. 声音为什么需要滤波？
2. 噪声通常在哪些频段出现？
3. low-pass、high-pass、notch filter 分别解决什么问题？
4. shelving filter 和 peaking filter 如何用于均衡器？
5. 实际调音时为什么不能随意大幅 boost/cut？

> [!summary] 一句话主线
> **Filtering** 就是对声音的频谱进行选择性修改：保留、增强或削弱某些频率成分，从而达到降噪、改善清晰度、修正音色或增强听感的目的。

---

## 1. 为什么音频处理中要修改频谱？

### 1.1 声音可以看成不同频率成分的组合

一个音频信号在时域中表现为 waveform，也就是振幅随时间变化的曲线。但从频域角度看，它可以理解成许多不同频率成分的叠加。

例如：

- 低频可能对应鼓声、低音、空调震动、脚步声；
- 中频可能对应人声主体、乐器主体；
- 高频可能对应齿音、空气感、噪声 hiss、细节和瞬态。

因此，改变某些频率的强弱，就能改变声音听起来的特征。

### 1.2 Signal spectrum modification 的意义

课件第一部分强调：**signal spectrum modification** 在数字音频信号处理中非常重要。

它常用于：

| 应用 | 解释 |
|---|---|
| Real-time audio effects | 直播、演出、通话中的即时音效处理 |
| Acoustic correction | 修正房间、扬声器、麦克风造成的频响问题 |
| Spatial sound | 空间音频、方向感、房间感模拟 |
| Noise reduction | 去除 hiss、rumble、hum 等噪声 |
| Sound enhancement | 增强清晰度、存在感、温暖度或低频冲击力 |

滤波的本质是：

```text
输入声音 → 按频率选择性增强/削弱 → 输出声音
```

---

## 2. Real-time 与 Offline 音频处理

课件指出音频处理可以分为两种方式：

1. **Real-time / online processing**
2. **Offline / batch processing**

### 2.1 Real-time processing

Real-time processing 指声音一边进入系统，一边被处理并立即输出。

典型场景：

- 语音通话降噪；
- 直播麦克风 EQ；
- 现场演唱调音；
- 数字乐器实时效果器；
- 游戏语音处理。

特点：

| 特点 | 说明 |
|---|---|
| 低延迟 | 输入和输出之间不能等待太久 |
| 即时反馈 | 用户能立刻听到效果 |
| 计算受限 | 算法不能太慢，否则会卡顿 |
| 更重视稳定性 | 不能因为复杂处理导致实时系统崩溃 |

> [!example] 例子
> 如果你在视频会议中说话，降噪系统必须马上处理你的声音。如果算法延迟太大，对方会听到明显的声音滞后。

### 2.2 Offline processing

Offline processing 指声音先录下来，之后再处理。

典型场景：

- 录音后期处理；
- 播客降噪；
- 音乐混音；
- 电影声音修复；
- 实验数据分析。

特点：

| 特点 | 说明 |
|---|---|
| 更灵活 | 可以反复试听、调整参数 |
| 可用更复杂算法 | 不必严格满足实时延迟 |
| 可追求更高质量 | 可以多次迭代优化 |
| 适合批处理 | 可一次处理整段音频 |

### 2.3 两者对滤波设计的影响

同一个滤波目标，在 real-time 和 offline 中的策略可能不同。

- real-time：滤波器应简单、稳定、低延迟；
- offline：可以使用更高阶、更复杂、更精细的处理。

例如，实时会议降噪可能使用较轻量的高通滤波和噪声抑制；而录音后期可以对每个频段精细 EQ、手动修复噪声、使用更复杂的频谱处理。

---

## 3. Audio filter 是什么？

### 3.1 基本定义

**Audio filter（音频滤波器）**是用来修改音频频率响应的工具。

它可以：

- boost 某些频率；
- attenuate 某些频率；
- remove 某些频率；
- reshape overall tone。

课件提到 audio filters 常用作：

- tone controls；
- equalisers；
- acoustic correction tools；
- sound enhancement tools。

### 3.2 Frequency response

一个滤波器最重要的特征是 **frequency response（频率响应）**，也就是它对不同频率的影响。

可以这样理解：

| 频率区域 | 滤波器可能做的事 |
|---|---|
| 低频 | 保留、削弱或增强 bass / rumble |
| 中频 | 调整人声主体、乐器存在感 |
| 高频 | 控制 hiss、air、brightness、sibilance |
| 某个窄频点 | 去除 hum、feedback、resonance |

频率响应不是只决定“音量变大或变小”，而是决定不同频率如何分别变化。

### 3.3 H(z) 与 H(s)

课件提到：

- 在数字系统中，滤波器常表示为 $H(z)$；
- 它们常由连续时间滤波器 $H(s)$ 推导而来。

可以简单理解为：

| 表示 | 含义 |
|---|---|
| $H(s)$ | 模拟/连续时间系统中的传递函数 |
| $H(z)$ | 数字/离散时间系统中的传递函数 |

数字音频是离散采样数据，所以数字滤波器通常在 z-domain 中描述。

> [!note] 不必在这节课深挖复变函数
> 这里需要掌握的核心不是复杂数学推导，而是知道 $H(z)$ 描述数字滤波器如何改变输入信号的频率成分。

---

## 4. Filtering 对声音做了什么？

课件列出三个最基本且最常用的滤波器：

1. Low-pass filter
2. High-pass filter
3. Notch filter

这三个滤波器可以理解为音频清理的基础工具。

---

## 5. Low-pass filter：低通滤波器

### 5.1 低通滤波器的作用

**Low-pass filter（低通滤波器）**允许低频通过，削弱或移除高频。

也就是：

```text
low frequencies pass
high frequencies attenuated
```

### 5.2 用途：去除高频 hiss

课件中给出的例子是：

> Low-pass filter → removes high-frequency noise (hiss)

**Hiss** 通常是高频噪声，听起来像“嘶嘶声”。它可能来自：

- 麦克风底噪；
- 前置放大器噪声；
- 老录音带噪声；
- 过度压缩或编码引起的高频噪声。

低通滤波器可以削弱这些高频噪声。

### 5.3 使用低通滤波要小心

低通滤波不是越强越好。如果 cutoff frequency 太低，可能会同时削弱有用的高频细节。

可能损失：

- 人声的空气感；
- 清晰的齿音和辅音；
- 鼓镲和瞬态细节；
- 空间感和亮度。

> [!warning] 风险
> 低通滤波过度会让声音变得闷、暗、缺少清晰度。

---

## 6. High-pass filter：高通滤波器

### 6.1 高通滤波器的作用

**High-pass filter（高通滤波器）**允许高频通过，削弱或移除低频。

也就是：

```text
high frequencies pass
low frequencies attenuated
```

### 6.2 用途：去除低频 rumble

课件强调：

> High-pass filter → removes low-frequency noise (rumble)

**Rumble** 是低频噪声，可能来自：

- 空调或机器震动；
- 麦克风架震动；
- 手持麦克风 handling noise；
- 风声；
- 地板脚步震动；
- 城市交通低频背景。

这些低频噪声可能本身不明显，但会占用 headroom，甚至 mask important speech frequencies。

### 6.3 为什么高通能改善 speech clarity

人声中有大量重要信息在中频范围，尤其是语音可懂度相关的频率区域。如果低频 rumble 很强，它可能掩盖 speech 的清晰度。

去除不必要的低频后：

- 背景轰鸣减少；
- 语音主体更干净；
- 混音中低频拥挤减少；
- 系统有更多 headroom；
- speech intelligibility 提升。

> [!example] 常见实践
> 对普通讲话录音，常会使用 gentle high-pass filter 去掉非常低的频率，例如麦克风震动和房间低频噪声。但 cutoff 不能设得太高，否则人声会变薄。

---

## 7. Notch filter：陷波滤波器

### 7.1 Notch filter 的作用

**Notch filter（陷波滤波器）**用于削弱一个非常窄的频率范围。

它不像 low-pass 或 high-pass 那样处理一大片频段，而是针对某个具体频率。

可以理解为：

```text
只挖掉一个窄频点或窄频带
```

### 7.2 用途：去除 50/60 Hz hum

课件中的例子是：

> Notch filter → removes specific unwanted frequencies, e.g. 50/60 Hz hum

50 Hz 或 60 Hz hum 通常来自电源干扰：

- 欧洲/中国等地区常见 50 Hz；
- 美国等地区常见 60 Hz。

电源 hum 有时还会带有 harmonics，例如：

```text
50 Hz, 100 Hz, 150 Hz, 200 Hz...
60 Hz, 120 Hz, 180 Hz, 240 Hz...
```

如果只是不想破坏整段低频，就可以用 notch filter 精准削弱这些频点。

### 7.3 Notch 的优点和风险

优点：

- 精准；
- 对其他频率影响较小；
- 适合去 hum、feedback、resonance。

风险：

- 如果 notch 太宽，会削弱有用音色；
- 如果 notch 太深，声音可能出现空洞感；
- 如果目标频率随时间变化，固定 notch 可能不够。

---

## 8. Types of Audio Filters：音频滤波器类型

课件第 5 页开始从更实用的音色调整角度介绍滤波器：

- shelving filters；
- peaking filters；
- equalisers；
- tone controls。

这些是混音、调音和声音修复中经常遇到的概念。

---

## 9. Shelving filter：搁架滤波器

### 9.1 Shelving filter 是什么

**Shelving filter（搁架滤波器）**用于提升或削弱某个 cutoff frequency 以上或以下的一大片频率。

它像一个“架子”：频率响应在某个范围之后整体抬高或压低。

常见类型：

| 类型 | 作用 |
|---|---|
| Low-shelf | 提升或削弱低频区域 |
| High-shelf | 提升或削弱高频区域 |

### 9.2 和 low-pass / high-pass 的关系

课件说 shelving filters behave like low-pass or high-pass filters with adjustable gain。

意思是：

- low-pass/high-pass 常用于“通过或削弱”；
- shelving filter 更像“整体调高或调低某个频段”。

例如：

- low-shelf boost：让 bass 更厚；
- low-shelf cut：减少低频浑浊；
- high-shelf boost：增加亮度和空气感；
- high-shelf cut：让声音更柔和，减少刺耳。

### 9.3 课件例子

课件给出的例子包括：

- low-frequency boost at 250 Hz；
- high-frequency boost at 2 kHz。

这里要理解的是：shelving filter 可以改变声音整体 tonal balance，而不是只处理一个极窄频点。

### 9.4 Shelving filter 的参数

关键参数包括：

| 参数 | 含义 |
|---|---|
| Gain | boost 或 cut 的幅度 |
| Cutoff frequency | 从哪里开始进入 shelving 行为 |
| Filter order / slope | 过渡区域有多陡 |

---

## 10. Peaking filter：峰值滤波器 / Presence filter

### 10.1 Peaking filter 是什么

**Peaking filter** 用来提升或削弱某个中心频率附近的一段频率。

它不像 shelving filter 那样影响一大片高频或低频，而是围绕一个 **centre frequency** 做局部调整。

常用于：

- 提升人声 presence；
- 削弱刺耳频段；
- 去除房间共振；
- 控制乐器某个问题频段；
- 抑制 microphone feedback。

### 10.2 Peaking filter 的参数

课件提到 peaking filters 使用以下参数：

| 参数 | 含义 |
|---|---|
| Gain | 提升或削弱多少 dB |
| Centre frequency | 处理的目标中心频率 |
| Bandwidth / Q | 影响范围有多宽 |

### 10.3 Q 与 bandwidth

在音频 EQ 中，Q 常用来控制滤波器的“宽窄”。

一般可以这样理解：

| Q / bandwidth | 效果 |
|---|---|
| 高 Q / 窄 bandwidth | 精准处理一个窄频段 |
| 低 Q / 宽 bandwidth | 宽范围地塑造音色 |

课件也强调：

- narrow bandwidth gives precise adjustment；
- wide bandwidth gives broader shaping。

### 10.4 Practical examples

| 目标 | 可能用法 |
|---|---|
| 去除嗡嗡共振 | narrow peaking cut |
| 增强人声清晰度 | moderate peaking boost in presence area |
| 减少刺耳感 | peaking cut around harsh frequency |
| 去 feedback | narrow notch-like peaking cut |

> [!tip] 记忆方法
> Shelving 像“调一片区域的整体高度”；Peaking 像“在某个频点附近挖或抬一个山峰”。

---

## 11. Equalisers：均衡器

### 11.1 EQ 是多个滤波器的组合

**Equaliser（EQ，均衡器）**不是单个滤波器，而是多个滤波器组合起来，用来塑造整体 frequency response。

课件中说：

> Equalisers combine multiple filters to shape the sound.

也就是说，一个 EQ 可能包含：

- high-pass filter；
- low-pass filter；
- low-shelf；
- high-shelf；
- 多个 peaking bands；
- notch bands。

### 11.2 Tone control

Tone control 是更简单的 EQ，通常调整：

- bass；
- mid；
- treble。

它不一定像 parametric EQ 那样精细，但足够用于很多普通播放设备或简单调音场景。

### 11.3 EQ 的用途

| 用途 | 解释 |
|---|---|
| Acoustic correction | 修正房间或设备频响问题 |
| Sound enhancement | 让声音更清晰、更亮、更厚或更自然 |
| Noise reduction | 减少不需要的频段 |
| Creative effects | 制造电话声、低保真、空间感等风格 |
| Mix balancing | 让不同乐器在频谱中互不遮挡 |

---

## 12. Filter order：滤波器阶数

课件提到：

> Filter order controls how sharp the transition is.

### 12.1 什么是 transition

滤波器通常不会在 cutoff frequency 处突然从“完全通过”变成“完全移除”。它有一个过渡区域。

例如 high-pass filter：

```text
低频被削弱 → 过渡带 → 高频保留
```

### 12.2 阶数越高，过渡越陡

一般来说，filter order 越高，transition 越 sharp。

优点：

- 可以更精准地保留/去除频段；
- 对目标频段以外的影响更小。

可能的问题：

- 计算复杂度更高；
- 实时系统中可能引入更多延迟或相位问题；
- 过陡的滤波听起来可能不自然。

> [!note] 课程层面需要记住
> Filter order 控制频率响应的陡峭程度。不是阶数越高就一定越好，而是要根据声音目标选择。

---

## 13. Shelving 与 Peaking filter 的实际行为

课件第 6-8 页强调了几个实际调音中容易忽略的点。

### 13.1 Boost 和 cut 不一定完全对称

课件说：

> Boost and cut responses are not perfectly symmetrical.

这意味着：同一个频点上 +6 dB 和 -6 dB 不一定在听感或曲线形状上完全互为镜像。

原因可能包括：

- 滤波器实现方式；
- gain 对滤波形状的影响；
- Q 和 bandwidth 的变化；
- 多个滤波器叠加后的相互作用。

所以实际调音时不能只看数值，还要听声音、看频谱。

### 13.2 滤波器形状取决于多个参数

课件强调：filter shape depends on：

- gain；
- frequency；
- bandwidth。

这三个参数会共同决定最终音色。

例如：

- 同样 +6 dB，宽 Q 会让声音整体变亮；
- 同样 +6 dB，窄 Q 只会突出某个频点，可能听起来尖锐；
- 同样 centre frequency，不同 bandwidth 会改变影响范围。

### 13.3 Narrow bandwidth vs wide bandwidth

| Bandwidth | 适合用途 | 听感 |
|---|---|---|
| Narrow | 去共振、去 feedback、修问题频点 | 精准，但过度会不自然 |
| Wide | 塑造整体音色、轻微增强/削弱 | 自然，但不够精准 |

---

## 14. 实际使用中的注意事项

### 14.1 用于修正 resonances

**Resonance（共振）**是某些频率异常突出，听起来可能“嗡”“刺”“箱体感强”或“不自然”。

常见处理：

```text
找到问题频率 → 用 narrow peaking cut 削弱
```

### 14.2 用于去除 problematic frequencies

Problematic frequencies 可能包括：

- 机器 hum；
- 麦克风 feedback；
- 房间 resonances；
- 过强鼻音；
- 刺耳高频；
- 低频 rumble。

不同问题对应不同滤波策略。

### 14.3 大幅 boost 的风险

课件提醒：

> Large boosts can cause distortion.

第 8 页进一步强调：

> Changes above 12 dB can cause distortion or amplifier overload.

原因包括：

- 信号幅度变大，容易 clipping；
- 放大器或扬声器可能超负荷；
- 噪声也会被一起放大；
- 频段不平衡会让听感不自然。

> [!warning] 实用原则
> 小幅、渐进、反复试听通常比一次性大幅 boost/cut 更安全。很多情况下，先 cut 问题频率比盲目 boost 想要的频段更有效。

---

## 15. Filter composition：滤波器组合

### 15.1 为什么要组合滤波器

单个滤波器通常只能解决一个问题。真实音频往往同时有多个问题：

- 低频 rumble；
- 高频 hiss；
- 50 Hz hum；
- 某个房间共振；
- 人声不够清晰。

因此需要把多个滤波器组合起来。

### 15.2 Cascading filters

课件提到：

> Cascading filters gives more precise control.

**Cascading** 指把多个滤波器串联：

```text
input → filter 1 → filter 2 → filter 3 → output
```

例如，一个语音清理 chain 可以是：

```text
high-pass filter → notch filter → peaking cut → gentle high-shelf
```

这可以分别处理：

- 低频 rumble；
- 50/60 Hz hum；
- 共振；
- 清晰度。

### 15.3 Narrowband peaking filters 的用途

课件指出 narrowband peaking filters 可用于：

- correct specific frequency issues；
- remove resonances；
- eliminate microphone feedback；
- eliminate unwanted tones。

它们的特点是精准，但也容易过度处理。

---

## 16. 常见噪声与滤波器选择表

> [!tip] 快速选择
> 先判断噪声在哪个频段，再选择滤波器。

| 问题声音 | 典型频率特征 | 适合滤波器 | 说明 |
|---|---|---|---|
| Hiss 嘶声 | 高频宽带噪声 | Low-pass / high-shelf cut | 小心不要削掉空气感 |
| Rumble 轰鸣 | 低频噪声 | High-pass | 常用于语音清理 |
| Handling noise | 很低频、突发震动 | High-pass | 麦克风手持噪声常见 |
| 50/60 Hz hum | 固定窄频率 | Notch | 可能还要处理 harmonics |
| Feedback 啸叫 | 窄频峰值 | Narrow peaking cut / notch | 找到频点后精准削弱 |
| Room resonance | 某些频段突出 | Peaking cut | 宽窄取决于共振范围 |
| 声音太暗 | 高频不足 | High-shelf boost | 避免过度导致刺耳 |
| 声音太薄 | 低频/低中频不足 | Low-shelf boost 或 peaking boost | 注意不要增加浑浊 |

---

## 17. 一个实际音频清理 workflow

如果拿到一段有噪声的人声录音，可以按下面思路处理。

### Step 1：先听问题

不要直接套滤波器。先判断：

- 是低频轰鸣？
- 高频 hiss？
- 电流 hum？
- 某个频点刺耳？
- 整体不清晰？

### Step 2：看频谱

用 spectrogram 或 spectrum analyser 辅助判断。

- 水平线常可能是 hum；
- 高频持续能量可能是 hiss；
- 低频大片能量可能是 rumble；
- 突出的窄峰可能是 resonance 或 feedback。

### Step 3：选择滤波器

- 低频噪声 → high-pass；
- 高频噪声 → low-pass 或 high-shelf cut；
- 固定频率 hum → notch；
- 局部共振 → peaking cut；
- 整体音色调整 → shelving / broad peaking。

### Step 4：小幅调整

先用较小 gain 调整，例如 2-6 dB，而不是直接 12 dB 以上。

### Step 5：A/B 对比

反复比较：

```text
处理前 vs 处理后
```

判断是否真的变好，而不是只是变大声或变亮。

### Step 6：避免过度处理

如果滤波后出现：

- 声音变薄；
- 声音变闷；
- 人声不自然；
- 细节消失；
- clipping；
- 相位感奇怪；

说明可能处理过度。

---

## 18. 本组课件中的关键概念解释

### 18.1 Boost

Boost 指提升某个频段的 gain。

例子：

```text
High-shelf +3 dB → 高频更亮
Peaking +4 dB at 3 kHz → 人声 presence 更突出
```

### 18.2 Attenuate / Cut

Attenuate 或 cut 指削弱某个频段。

例子：

```text
High-pass at low frequencies → 去低频 rumble
Notch at 50 Hz → 去电源 hum
Peaking -5 dB at resonance → 去共振
```

### 18.3 Cutoff frequency

Cutoff frequency 是滤波器开始明显改变频率响应的位置。

常用于：

- low-pass；
- high-pass；
- shelving filter。

### 18.4 Centre frequency

Centre frequency 是 peaking filter 或 notch filter 的目标中心频率。

例如 notch at 60 Hz，就是以 60 Hz 为中心做窄带削弱。

### 18.5 Bandwidth / Q

Bandwidth 或 Q 控制作用范围。

- 窄：精准；
- 宽：自然、整体。

### 18.6 Gain

Gain 控制 boost 或 cut 的幅度，通常用 dB 表示。

---

## 19. 课件内容逐页理解

### Page 1：标题页

主题是 **Audio Quality, Noise, and Digital Filtering**。说明这节课关注的是如何通过数字滤波改善音频质量，并处理噪声问题。

### Page 2：Introduction

这一页说明 spectrum modification 的重要性，并区分 real-time 和 offline processing。

重点：滤波不是只用于“降噪”，也用于 audio effects、acoustic correction 和 spatial sound。

### Page 3：Audio Filters

这一页定义 audio filters：它们可以作为 tone controls 和 equalisers，通过 boost 或 attenuate 频段来改变 frequency response。

重点：数字系统用 $H(z)$ 表示滤波器，通常可从模拟滤波器 $H(s)$ 推导。

### Page 4：What does filtering do to sound?

这一页列出三种基础滤波器：

- low-pass：去高频 hiss；
- high-pass：去低频 rumble；
- notch：去固定频率 hum。

这是最重要的应用页之一。

### Page 5：Types of Audio Filters

这一页进入更实用的 EQ 类型：

- shelving filters；
- peaking filters；
- equalisers；
- tone control。

重点：滤波器不仅能去噪，也能塑造音色。

### Page 6：Shelving and Peaking Filters

这一页讲参数：

- gain；
- cutoff frequency；
- centre frequency；
- bandwidth / Q。

重点：shelving 影响 cutoff 以上或以下，peaking 影响 centre frequency 周围。

### Page 7：Practical Behaviour

这一页强调实际滤波和理论曲线不总是简单对称。

重点：滤波器形状受 gain、frequency、bandwidth 影响；小幅调整通常更安全。

### Page 8：Filter Composition

这一页讲滤波器组合：多个 shelving 和 peaking filters 可以 cascade，形成更精确的 frequency response。

重点：不要过度 boost/cut，超过 12 dB 可能导致 distortion 或 amplifier overload。

---

## 20. 考试/复习重点

### 20.1 必须会解释

- 为什么频谱修改在数字音频处理中重要；
- real-time 与 offline processing 的区别；
- audio filter 如何通过 frequency response 改变声音；
- $H(z)$ 与 $H(s)$ 的基本含义；
- low-pass、high-pass、notch filter 的用途；
- shelving filter 和 peaking filter 的区别；
- gain、cutoff frequency、centre frequency、bandwidth/Q 的含义；
- filter order 与 transition sharpness 的关系；
- 为什么大幅 boost/cut 可能导致 distortion；
- 如何组合多个滤波器形成 EQ。

### 20.2 常见问答

#### Q1. Low-pass filter 用来解决什么问题？

它削弱高频，常用于减少高频 hiss。但过度使用会让声音变暗、变闷。

#### Q2. High-pass filter 为什么能改善语音清晰度？

它可以去除低频 rumble、handling noise 等无用低频，减少低频对语音主体的 masking，从而提升 speech clarity 和 intelligibility。

#### Q3. Notch filter 和 peaking filter 有什么关系？

Notch filter 可以看作非常窄、用于强削弱的 peaking-style filter。它适合去除固定频率噪声，例如 50/60 Hz hum。

#### Q4. Shelving filter 和 peaking filter 有什么区别？

Shelving filter 影响 cutoff 以上或以下的一大片频段；peaking filter 影响 centre frequency 周围的一段频率。

#### Q5. 为什么不要大幅 boost？

大幅 boost 会增加 clipping、distortion、amplifier overload 的风险，也可能把噪声一起放大。课件特别提醒，超过 12 dB 的变化可能造成问题。

#### Q6. Filter order 越高越好吗？

不一定。高阶滤波器过渡更陡，控制更精准，但可能增加计算复杂度、延迟、相位问题或不自然听感。

---

## 21. 一页速记

> [!summary] Block 3 第 3 组 PPT 速记
> - Filtering = 修改声音的 frequency response。
> - Real-time processing 要低延迟；offline processing 更灵活、可更精细。
> - 数字滤波器常表示为 $H(z)$，模拟滤波器常表示为 $H(s)$。
> - Low-pass：保留低频，削弱高频，用于减少 hiss。
> - High-pass：保留高频，削弱低频，用于减少 rumble、handling noise。
> - Notch：削弱窄频点，用于去 50/60 Hz hum、feedback、resonance。
> - Shelving：整体提升/削弱低频或高频区域。
> - Peaking：围绕 centre frequency 提升/削弱一段频率。
> - EQ = 多个滤波器组合，用于塑造整体音色。
> - Gain、cutoff、centre frequency、bandwidth/Q 是重要参数。
> - Filter order 控制 transition 的 sharpness。
> - 大幅 boost/cut，尤其超过 12 dB，可能导致 distortion 或 overload。

---

## 22. 和前后课程的连接

- 与 [[课程笔记/音频处理/Block 3/Block 3 - PPT 1：Compression and Decompression|Block 3 PPT 1]] 的连接：压缩前后的音频质量会受到噪声和频谱分布影响，滤波可作为预处理或后处理。
- 与 [[课程笔记/音频处理/Block 3/Block 3 - PPT 2：PCA and ICA|Block 3 PPT 2]] 的连接：PCA/ICA 更偏统计分解和源分离，filtering 更偏频率选择性处理；两者都可用于降噪。
- 与后续 Block 4 的连接：音频质量评价、噪声滤除、机器学习特征提取都会依赖频域理解和滤波思想。
