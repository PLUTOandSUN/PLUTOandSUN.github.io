---
title: EBU5408 Block 4 - PPT 3：Course Revision and Exam Preparation
aliases:
  - Block 4 PPT 3
  - Course Revision
  - EBU5408 Revision Slides
  - Audio Processing Exam Preparation
tags:
  - course/音频处理
  - EBU5408
  - digital-audio
  - block4
  - revision
  - exam-preparation
  - audio-ethics
  - ICA
  - audio-compression
source:
  - "[[../附件/Block 4 - Applied Digital Audio Processing/3 Revision Slides/EBU5408_CourseRevision.pdf]]"
created: 2026-06-19
---

# Block 4 - PPT 3：Course Revision and Exam Preparation

> [!info] 课件来源
> 本笔记对应 Block 4 第 3 组课件：
> - [[../附件/Block 4 - Applied Digital Audio Processing/3 Revision Slides/EBU5408_CourseRevision.pdf]]
>
> 这组 slides 不是单独讲一个新技术点，而是 **Course revision**：它把 EBU5408 / Digital Audio Fundamentals 中 TB3 和 TB4 的核心主题、考试形式、样题、评分标准和答题方式集中串起来。复习时要把它当成“考试地图”和“答题模板”。

## 0. 这组 PPT 在课程中的作用

前两组 Block 4 课件分别偏向：

- [[Block 4 - PPT 1：Audio Quality, Noise, and Digital Filtering II|PPT 1：音频质量、噪声、滤波、EQ 与评价指标]]
- [[Block 4 - PPT 2：Real-Time Audio Processing, Machine Learning, Ethics and Forensics|PPT 2：实时音频处理、机器学习、AI 伦理与取证]]

第 3 组则是复习课，核心问题不是“再学一个新算法”，而是：

1. 课程到底覆盖了哪些主题？
2. 考试会怎样考这些主题？
3. 算法题、计算题、场景分析题、伦理题分别应该怎样组织答案？
4. 什么样的答案能拿到分？

> [!summary] 一句话主线
> 本组 PPT 的重点是：**把课程知识转化成考试可用的解释、计算、选择、论证和评价能力。**

---

## 1. 课程主题总览：你需要复习的知识地图

Slides 第 3-5 页给出全课程主题 outline。它可以理解为考试范围清单。复习时不要只背单个定义，而要能说明每个主题“为什么重要、用于什么场景、有什么限制”。

### 1.1 Digital Audio Fundamentals：数字音频基础

这一部分是所有后续内容的底层语言。需要掌握：

| 主题 | 需要理解什么 |
|---|---|
| Analogue vs Digital Audio | 模拟信号连续，数字信号离散；数字化需要采样和量化。 |
| Sampling | 采样率决定每秒记录多少个样本；与 Nyquist 频率、带宽和 aliasing 有关。 |
| Quantisation | 把连续幅度映射到有限等级；会产生量化误差。 |
| Encoding | 把音频样本以某种格式编码存储或传输。 |
| WAV File Structure | WAV 通常包含 header、format chunk、data chunk；适合未压缩 PCM。 |
| Bit Depth | 决定每个 sample 的位数，影响动态范围和量化噪声。 |
| Sample Rate | 决定最高可表示频率范围。 |
| Audio Bandwidth | 音频信号频率范围；与采样率和滤波有关。 |
| PCM Audio | Pulse-Code Modulation，是未压缩数字音频的常见表示。 |
| Audio Metadata | 文件中描述采样率、声道数、编码方式、时长等信息的数据。 |
| Audio Representation in Python | 音频可作为数组/矩阵处理，常见维度为 samples 或 samples × channels。 |

> [!important] 考试理解方式
> 如果题目问“为什么 44.1 kHz 可以覆盖大多数人耳听觉范围”，你不能只写“因为 CD 用 44.1 kHz”，而要说明 Nyquist：采样率的一半约为 22.05 kHz，高于人耳常见上限约 20 kHz，因此可以覆盖大多数 audible bandwidth。

### 1.2 Audio Compression & Processing：压缩与处理

这一部分常用于计算题或解释题。需要理解：

| 主题 | 核心点 |
|---|---|
| Lossless Compression | 解压后与原始信号完全一致；压缩率通常低于有损压缩。 |
| Lossy Compression | 允许丢弃人耳不敏感信息，压缩率高，但不可完全恢复。 |
| MP3 Compression Pipeline | 分帧、窗口、变换、心理声学模型、量化、熵编码。 |
| Frame Splitting & Windowing | 把长音频切成短帧，减少边界突变，便于频域分析。 |
| MDCT | MP3/AAC 等常用的重叠变换，有利于频域压缩。 |
| Psychoacoustic Modelling | 利用 masking 等人耳特性决定哪些信息可被丢弃。 |
| Entropy Coding | 利用统计冗余进一步压缩码流。 |
| Audio Normalisation | 调整整体音量或峰值/RMS，避免过低或过载。 |
| Audio Reconstruction | 从压缩或处理后的表示恢复为可播放音频。 |

> [!tip] 复习重点
> 压缩题常见考法不是让你完整推导 MP3，而是让你说明“为什么有损压缩能大幅减少文件大小”以及“为什么它可能产生 artifacts”。

### 1.3 Audio Quality, Noise & Filtering：音质、噪声与滤波

这一部分连接 Block 3 和 Block 4，是很多应用题的基础。

| 主题 | 需要会解释 |
|---|---|
| Noise and Distortion | 噪声是额外无关成分，失真是信号形态被改变。 |
| Audio Restoration | 通过降噪、去点击、去混响等改善旧录音或低质量录音。 |
| Digital Filtering | 通过频率选择性处理增强或削弱某些频段。 |
| Notch Filters | 去除很窄频率范围，例如 50/60 Hz hum。 |
| Equalisation | 调整频率响应，改变 tonal balance。 |
| Shelving / Peaking Filters | 常用于 EQ；shelving 改变某一侧频段，peaking 改变中心频率附近。 |
| FIR and IIR Filters | FIR 稳定、可线性相位；IIR 高效、低延迟但可能有相位失真。 |
| Real-Time Filtering | 需要低延迟、稳定、因果、计算量可控。 |

### 1.4 Dimensionality Reduction & Source Separation：降维与源分离

这一部分是样题 Q3 的核心。

| 主题 | 核心理解 |
|---|---|
| PCA | 找到最大方差方向，用于降维、去噪、压缩表示。 |
| Data Centering | PCA 前通常要减去均值，使数据以零均值为中心。 |
| Variance & Covariance | PCA 依赖协方差结构，找出数据变化最大的方向。 |
| PCA Noise Reduction | 保留主要成分，丢弃小方差噪声成分。 |
| BSS | Blind Source Separation，在缺少源信号先验的情况下分离混合信号。 |
| ICA | 假设源信号统计独立，寻找独立成分。 |
| Cocktail Party Problem | 多人同时说话时从混合声音中分离目标说话人。 |

> [!warning] PCA vs ICA 的考试区别
> - **PCA** 更像“找最大方差方向”，适合降维和去噪，但不一定能把不同声源真正拆开。
> - **ICA** 更像“找统计独立的源”，更适合语音/噪声/背景源的分离。

### 1.5 Audio Features & Machine Learning：音频特征与机器学习

这一部分常见考法是：给一个任务，让你选择合适 features、模型和评价指标。

| 特征/概念 | 解释 |
|---|---|
| Feature Extraction | 把 raw waveform 转成更紧凑、可学习的数值表示。 |
| Time-Domain Features | 直接从时域波形计算，例如 ZCR、RMS。 |
| Frequency-Domain Features | 从频谱或时频图中提取，例如 centroid、roll-off、MFCC。 |
| ZCR | 过零率，常反映高频/噪声/清浊音特征。 |
| RMS Energy | 表示短帧能量或响度。 |
| Spectral Centroid | 频谱“重心”，反映声音明亮度。 |
| STFT | 短时傅里叶变换，用于观察频率随时间变化。 |
| MFCC | 模拟人耳 Mel 感知的 cepstral 特征，常用于语音和音色任务。 |
| Audio Classification | 根据音频特征判断类别，例如 speech/music、speaker ID、环境声。 |

### 1.6 Real-Time Audio Processing：实时音频处理

需要掌握 latency、buffer 和系统约束。

| 概念 | 解释 |
|---|---|
| Audio Buffers | 音频通常按小块处理，而不是一个 sample 一个 sample 地手动处理。 |
| Latency | 输入到输出之间的延迟。 |
| Buffer Size Calculation | buffer 越大越稳定但延迟越高；越小延迟越低但更容易 glitch。 |
| CPU/System Constraints | 实时处理必须在下一块 buffer 到来前完成。 |
| Low-Latency Systems | 依赖合适驱动、优化系统、低复杂度算法和稳定处理时间。 |

常用公式：

$$
Latency(ms)=\frac{BufferSize}{SampleRate}\times1000
$$

如果题目问 round-trip latency，通常再乘以 2：

$$
RoundTripLatency(ms)=\frac{BufferSize}{SampleRate}\times1000\times2
$$

### 1.7 Audio Forensics & Restoration：音频取证与修复

这一部分强调“技术处理”和“证据可靠性”的区别。

| 主题 | 核心点 |
|---|---|
| Audio Authentication | 判断录音是否真实、连续、未篡改。 |
| Metadata Inspection | 查看采样率、编码器、时间戳、软件痕迹等。 |
| ENF Analysis | 利用电网频率波动验证录音时间和连续性。 |
| Speech Intelligibility Enhancement | 提高语音可懂度，但不能改变证据含义。 |
| Noise Reduction | 降低噪声，但需避免引入误导性 artifacts。 |
| De-clicking / De-reverb | 去除点击声或混响，改善可懂度。 |
| Restoration vs Forensics | restoration 追求好听；forensics 追求真实、可追溯、可复现。 |

### 1.8 AI Audio & Ethics：AI 音频与伦理

这部分是样题 Q4 伦理题的核心。

| 主题 | 需要会答 |
|---|---|
| AI Audio Generation | AI 生成语音、音乐、音效等。 |
| Voice Cloning | 用少量样本模仿某人声音。 |
| Audio Deepfakes | 让某人听起来像说了没说过的话。 |
| TTS | Text-to-Speech，从文本生成语音。 |
| AI Music Generation | 生成音乐、伴奏、风格化声音。 |
| Ethical Challenges | consent、版权、冒充、欺诈、误导公众。 |
| Misuse of AI Audio | 诈骗、政治操纵、黑mail、企业欺诈。 |
| Detection and Mitigation | 水印、检测器、访问控制、身份验证、政策监管。 |

---

## 2. 考试形式与作答要求

Slides 第 6 页说明考试形式：

- 需要回答全部 4 道题。
- 考试时长 2 小时。
- 开始作答某一道题前，应该先快速浏览所有题目。
- 计算题要展示清晰步骤。
- 场景题要解释选择理由。
- 合适时可以画图或示意流程。
- 大多数题目的骨架答案都能从 lecture notes、tutorial exercises 和课堂 examples 中找到。

### 2.1 为什么要先浏览全部题目？

因为考试不是只考记忆，而是考你能否快速判断：

- 哪道题是计算题？
- 哪道题是概念解释？
- 哪道题需要算法 pipeline？
- 哪道题是伦理/取证/场景讨论？
- 哪些题最容易先拿分？

如果一开始就卡在某一小问，很容易浪费时间。更好的策略是先建立整卷地图，再分配时间。

### 2.2 计算题的基本要求

计算题通常按步骤给分。不要只写最后答案。

正确格式应包括：

1. 写公式。
2. 代入已知量。
3. 注意单位转换。
4. 得出中间量。
5. 给最终答案和单位。
6. 如果有二进制 MB / 十进制 MB 差异，说明假设。

### 2.3 场景题的基本要求

场景题通常不是问“某算法定义是什么”，而是问：

- 这个场景有什么问题？
- 哪种方法更适合？为什么？
- 有哪些限制？
- 如何改进 pipeline？
- 如何评价结果？

> [!tip] 场景题答题模板
> **Task → Problem characteristics → Method choice → Pipeline → Limitations → Improvements → Evaluation**

---

## 3. 考试考察什么能力？

Slides 第 7 页列出 expected demonstration。可以分成六类能力。

### 3.1 理解数字音频基础

你需要能解释采样、量化、bit depth、sample rate、WAV/PCM 等基础概念，而不是只背定义。

例如：

- 为什么 bit depth 越高，动态范围越大？
- 为什么采样率太低会产生 aliasing？
- 为什么 stereo 文件大小通常是 mono 的两倍？

### 3.2 进行 DSP 相关计算

常见计算包括：

- 文件大小。
- bitrate 与时长换算。
- buffer latency。
- SNR / PSNR / MSE / RMSE。
- dB 与线性幅度增益换算。

### 3.3 清晰解释音频处理概念

答题要避免只堆术语。应该解释“概念 + 作用 + 使用场景 + 局限”。

例如，不要只写：

> ICA separates independent components.

更完整的答案应该写：

> ICA 假设混合信号由统计独立的源组成，通过寻找独立成分来恢复源信号。它适合语音与背景噪声/其他说话人混合的场景，但依赖独立性假设，并可能受到频率重叠、混响、非平稳噪声和成分数量选择的影响。

### 3.4 理解压缩和滤波技术

需要会比较：

- lossless vs lossy；
- FIR vs IIR；
- low-pass / high-pass / notch / band-pass；
- compression ratio 与 audio quality trade-off；
- psychoacoustic model 为什么能减少数据量。

### 3.5 把 lecture concepts 应用于真实音频场景

样题中的 noisy urban recording 就是典型场景题。它要求你把：

- noise type；
- overlapping speech；
- PCA/ICA；
- spectrogram；
- post-processing；
- SNR/SDR/PESQ/STOI；

组织成完整处理流程。

### 3.6 理解 AI 音频系统、限制和权衡

AI audio 题目通常需要你同时谈：

- 技术能力；
- 误用风险；
- 伦理治理；
- 检测和水印；
- 对抗攻击；
- 社会影响。

---

## 4. Study Hints：复习时应该关注什么

Slides 第 8 页给出复习建议。逐条解释如下。

### 4.1 理解 lecture examples 和 tutorial exercises

考试题目的骨架往往来自课件例子或 tutorial。复习时要把例题改写成自己的模板。

例如文件大小题，不要只背某个例子的结果，而要掌握通用公式：

$$
FileSize(bytes)=SampleRate\times BitDepthBytes\times Channels\times DurationSeconds
$$

### 4.2 关注 WHY，不只背定义

考试喜欢问“为什么选择这个方法”。例如：

- 为什么 ICA 比 PCA 更适合分离重叠语音？
- 为什么 MP3 可以丢弃部分频率信息？
- 为什么小 buffer 会降低 latency 但提高 CPU 风险？
- 为什么 forensic audio 不能过度处理？

### 4.3 理解算法优点、限制和 trade-offs

很多高分答案都来自 trade-off 分析。

| 主题 | 常见 trade-off |
|---|---|
| Lossy compression | 文件更小 vs 音质损失/artifacts |
| Buffer size | 低延迟 vs 稳定性 |
| FIR/IIR | 线性相位/精确性 vs 低延迟/高效率 |
| PCA/ICA | 降维去噪 vs 源分离能力 |
| AI voice cloning | 可访问性/医疗用途 vs fraud/deepfake 风险 |
| Forensic enhancement | 可懂度提高 vs 证据真实性风险 |

### 4.4 熟悉真实场景解释

题目可能不会直接说“解释 ICA”，而是给一个 messy audio scenario。你需要从场景中识别：

- 噪声是否平稳？
- 是否有多个源？
- 是否有语音重叠？
- 是否需要实时处理？
- 是否有 reference signal？
- 是否涉及伦理或法律证据？

### 4.5 同时复习计算和概念

不要只复习数学，也不要只复习文字解释。考试会同时考：

- 文件大小/bitrate/latency 等数值计算；
- PCA/ICA、滤波、压缩、AI ethics 等概念解释；
- 真实场景中的选择与论证。

---

## 5. 样题 Q3：Noisy Urban Audio Recording

Slides 第 9-12 页围绕一个 noisy urban audio recording 场景展开。

题目场景包含：

- vehicle noise；
- crowd chatter；
- overlapping speech。

可能任务包括：

- 选择合适算法；
- 解释为什么适合；
- 讨论限制和假设；
- 提出改进 pipeline。

评分标准关注：

- 方法选择是否正确；
- 是否有 DSP reasoning；
- 是否理解 ICA/PCA；
- 是否能说明 realistic limitations 和 trade-offs。

### 5.1 为什么这个场景适合考 ICA/PCA？

因为 noisy urban recording 同时具有：

1. **多个声音源**：车辆、人群、目标语音。
2. **频率重叠**：车辆低频、人声中频、人群语音频段互相覆盖。
3. **非平稳噪声**：车流和人群不是固定噪声，音量和频率会随时间变化。
4. **目标源不一定最响**：目标语音可能被背景遮盖。

这使得简单滤波不一定够用。例如只用 band-pass 保留 300 Hz-3.4 kHz 会保留语音，但也会保留很多 crowd chatter。

### 5.2 Q3(a)(i)：ICA vs PCA，为什么 ICA 更适合？

课件示例答案核心是：

- ICA 更有效，因为它尝试分离 statistically independent components。
- PCA 主要用于 dimensionality reduction 和 noise reduction。
- PCA 不一定能真正 unmix sources。
- 因此在 isolating voices 的场景中，ICA 通常比 PCA 更适合。

更完整的解释可以写成：

> 在城市噪声录音中，目标语音、车辆噪声和人群说话可以看作多个混合源。如果假设这些源在统计上相对独立，ICA 可以尝试从混合信号中恢复独立成分，因此更适合 source separation。PCA 通过方差最大方向进行降维和去噪，但其主成分只保证 uncorrelated，不保证独立；而且高方差成分可能是车辆噪声而不是目标语音。因此 PCA 可以作为预处理或降噪工具，但单独用于分离目标说话人通常不如 ICA。

### 5.3 Q3(a)(ii)：为什么重叠频率和非平稳噪声是难点？

课件给出两个要点。

#### 频率重叠

车辆噪声、人群聊天和目标语音可能共享相似频段。例如：

- 人声主要信息在中频；
- 人群 chatter 也是人声；
- 车辆低频噪声可能掩盖语音基频；
- 高频环境噪声可能影响辅音清晰度。

因此，单纯按频率切割会遇到问题：滤掉噪声的同时可能也滤掉目标语音。

#### 非平稳噪声

Non-stationary noise 指噪声随时间变化，例如：

- 汽车突然经过；
- 人群声音忽大忽小；
- 背景说话人突然接近麦克风；
- 短时警笛、刹车、脚步声。

这类噪声让固定滤波器或简单 noise profile 方法效果变差，因为噪声统计特性不是恒定的。

### 5.4 Q3(b)(i)：ICA 处理 pipeline 的标准答案

Slides 第 11-12 页要求：如果选择 ICA，给出 detailed step-by-step approach，不要求写代码，但要定义每个阶段，并包含 parameter selection 和 expected outcomes。

课件示例 pipeline 是：

1. Data Pre-processing
2. Time-Frequency transform
3. ICA-Based Separation
4. Inverse Transformation
5. Parameter Selection
6. Post-Processing
7. Evaluation

下面是详细解释。

#### Step 1：Data Pre-processing

目标是把输入音频整理成适合算法处理的形式。

可包括：

- 转成 WAV 或统一采样格式；
- resampling 到合适 sample rate；
- 转 mono 或保留 multi-channel；
- normalise volume；
- remove silent segments；
- high-pass 去除 rumble / DC offset；
- 对齐多通道输入；
- 检查 clipping 和异常片段。

> [!note] 为什么预处理重要？
> ICA 对输入数据质量敏感。如果输入有严重 clipping、极低频 rumble、过多 silence 或通道不同步，分离结果会明显下降。

#### Step 2：Time-Frequency Representation

将音频转换为 spectrogram，例如通过 STFT。

目的：

- 显示声音能量如何随时间和频率变化；
- 让语音和噪声结构更容易分离；
- 为后续 source separation 提供可操作表示。

常见参数：

- frame length；
- hop size；
- window type；
- FFT size。

> [!warning] 参数 trade-off
> 长窗口频率分辨率更好，但时间定位更差；短窗口时间定位更好，但频率分辨率更差。

#### Step 3：ICA-Based Separation

对混合表示应用 ICA，提取 statistically independent components。

关键点：

- ICA 假设源之间相互独立；
- 输出的 components 需要判断哪个对应目标语音；
- 可能需要比较每个 component 的频谱、能量、语音清晰度或听感；
- 如果是多通道录音，ICA 更自然；如果只有单通道，可能需要额外构造特征或使用其他方法辅助。

#### Step 4：Inverse Transformation

将分离后的 component 转回 time domain。

如果前面用了 STFT，则需要 inverse STFT。需要注意：

- 相位信息如何处理；
- overlap-add 是否正确；
- 输出是否有 musical noise 或 artifacts；
- 音量是否需要重新归一化。

#### Step 5：Parameter Selection

课件特别强调参数选择。可以讨论：

| 参数 | 影响 |
|---|---|
| Number of components | 太少会分不出源；太多会产生冗余或不稳定成分。 |
| Learning rate | 太大可能不收敛，太小收敛慢。 |
| Convergence threshold | 控制何时停止迭代。 |
| Max iterations | 防止无限运行，但过小可能未收敛。 |
| Pre-whitening | 常用于 ICA 前提高稳定性。 |
| STFT window/hop | 影响时频分辨率和重构质量。 |

Expected outcome：

- 一个或多个 component 更接近目标说话人；
- 背景车辆和 crowd chatter 被降低；
- 语音 intelligibility 提高；
- 但仍可能有残余噪声和 artifacts。

#### Step 6：Post-Processing

ICA 后的结果通常不完美，需要后处理。

可用方法包括：

- Wiener filtering；
- spectral subtraction；
- notch filter 去 hum；
- band-pass 强调语音频段；
- de-reverb；
- smoothing 降低 musical noise；
- normalisation；
- manual spectrogram cleanup。

注意不要 over-process，否则会让语音变薄、机械或产生伪影。

#### Step 7：Evaluation

课件提到可用：

- SNR；
- SDR；
- PESQ；
- STOI；
- listening tests。

解释如下：

| 指标 | 适合评价什么 |
|---|---|
| SNR | 噪声相对信号是否减少。 |
| SDR | 分离结果中目标信号相对失真/干扰的比例。 |
| PESQ | 语音感知质量，常用于通信语音。 |
| STOI | 语音可懂度，适合判断 speech intelligibility。 |
| Listening tests | 人耳确认是否真的更清楚、更自然。 |

### 5.5 Q3(b)(ii)：ICA 的限制与改进方案

题目还要求讨论 ICA 在该场景的 limitations，并提出 additional techniques 或 algorithmic adjustments。

#### ICA 的潜在限制

1. **独立性假设不完全成立**
   - 人群聊天和目标语音都属于 speech，统计结构可能相似。

2. **源数量和混合通道数限制**
   - 如果声源数量多于麦克风通道，ICA 分离会更困难。

3. **频率重叠严重**
   - 目标语音和背景说话人频段重叠，无法只靠频率分离。

4. **非平稳噪声**
   - 车辆、人群和突发声音随时间变化，固定模型不稳定。

5. **混响影响独立性和混合模型**
   - 房间反射会让同一源以延迟形式出现，破坏简单线性瞬时混合假设。

6. **成分解释困难**
   - ICA 输出有 permutation ambiguity 和 scaling ambiguity，需要人工或规则判断哪个 component 是目标语音。

7. **可能产生 artifacts**
   - 分离后的声音可能有 musical noise、断续、相位问题或语音变形。

#### 可提出的改进

| 改进方法 | 为什么有用 |
|---|---|
| Pre-filtering | 先用 high-pass/notch/band-pass 去除明显无关噪声。 |
| Voice Activity Detection | 只在语音活跃片段重点处理，减少噪声干扰。 |
| Wiener filtering | 后处理残余噪声，减少 artifacts。 |
| Spectral subtraction | 在有噪声 profile 时减少背景噪声。 |
| NMF | 对非负 spectrogram 分解，适合音乐/语音结构分离。 |
| Beamforming | 如果有多麦克风，利用空间方向增强目标说话人。 |
| Deep speech enhancement | 用训练模型处理复杂非平稳噪声。 |
| De-reverberation | 减少混响，提高 ICA 或后续语音清晰度。 |
| Parameter tuning | 调整 component 数、learning rate、window size，提高稳定性。 |
| Hybrid pipeline | ICA + post-filtering + perceptual evaluation，通常比单一算法更可靠。 |

> [!summary] Q3 高分结构
> 先明确场景困难，再解释为什么 ICA 比 PCA 更适合，然后给出完整 pipeline，最后讨论限制、改进和评价指标。

---

## 6. 样题 Q4：数字音频存储与压缩计算

Slides 第 13-15 页给出一个 AI voice cloning 系统生成音频的存储/压缩计算题。

题干条件：

- Sampling rate = 48 kHz
- Bit depth = 16-bit
- Stereo
- Duration = 1 minute
- Uncompressed WAV
- Then compressed using MP3 at 128 kbps

### 6.1 未压缩 WAV 文件大小公式

通用公式：

$$
FileSize(bytes)=SampleRate\times Duration\times Channels\times \frac{BitDepth}{8}
$$

也可以写成：

$$
BytesPerSecond=SampleRate\times Channels\times BytesPerSample
$$

### 6.2 示例计算：1 分钟 48 kHz / 16-bit / stereo WAV

#### Step 1：bit depth 转 bytes

16-bit 表示每个 sample 需要：

$$
16\ bits = 2\ bytes
$$

#### Step 2：考虑 stereo 双声道

Stereo 有 2 个 channels：

$$
2\ bytes/sample \times 2\ channels = 4\ bytes\ per\ frame
$$

这里可以理解为同一采样时刻包含左右两个声道，所以每个采样帧 4 bytes。

#### Step 3：每秒字节数

采样率为 48,000 samples/second：

$$
48000\times4=192000\ bytes/second
$$

#### Step 4：1 分钟字节数

1 minute = 60 seconds：

$$
192000\times60=11520000\ bytes
$$

#### Step 5：转换为 MB / MiB

如果用二进制 MiB：

$$
\frac{11520000}{1024\times1024}\approx10.98\ MiB
$$

所以约为：

```text
10.98 MiB ≈ 11 MB
```

如果用十进制 MB：

$$
\frac{11520000}{1000\times1000}=11.52\ MB
$$

> [!important] 单位提醒
> 课件答案使用 $1024\times1024$，所以结果约为 10.98 MB。严格说这是 MiB，但考试中通常写 roughly 11 MB 即可，关键是步骤清楚。

### 6.3 MP3 128 kbps 压缩后文件大小

bitrate = 128 kbps，表示每秒 128,000 bits。

#### Step 1：计算总 bits

$$
128000\ bits/second \times 60\ seconds=7680000\ bits
$$

#### Step 2：bits 转 bytes

$$
\frac{7680000}{8}=960000\ bytes
$$

#### Step 3：转换为 MB / MiB

二进制：

$$
\frac{960000}{1024\times1024}\approx0.916\ MiB
$$

十进制：

$$
\frac{960000}{1000\times1000}=0.96\ MB
$$

所以压缩后约为：

```text
0.92 MiB 或约 0.96 MB
```

### 6.4 压缩比例

用二进制近似：

$$
CompressionRatio=\frac{10.98}{0.916}\approx12.0
$$

也就是说，128 kbps MP3 大约比原始 WAV 小 12 倍。

### 6.5 这类题的评分点

Slides 强调 marks allocated for：

- correct calculations；
- correct unit conversions；
- understanding bitrate relationships。

因此作答时要避免：

- 忘记 stereo 乘以 2；
- 16-bit 没有除以 8；
- kbps 当成 kB/s；
- 忘记乘以 duration；
- MB/MiB 换算混乱；
- 只写最后答案不写步骤。

> [!tip] 计算题答题模板
> **Known values → Formula → Convert units → Substitute → Intermediate result → Final answer with units**

---

## 7. 样题 Q4：AI Voice Cloning 的伦理、安全与鲁棒性

Slides 第 16-19 页给出一个 12 分场景题：某 startup 开发 AI voice cloning 技术，可以用短音频样本生成非常接近某人声音的语音。公司宣传正面用途，例如 personalized voice assistants、medical voice restoration、accessibility；但记者发现该技术被用于 deepfake audio、impersonation、fraud 和 misinformation。

题目分三问：

1. 这种技术如何被利用来造成伤害或操纵个人/组织？3 marks
2. 公司应采取什么措施防止滥用？4 marks
3. 对抗攻击可让 AI 生成声音逃避 deepfake detection，如何提高模型鲁棒性？5 marks

### 7.1 Q4(i)：可能造成哪些伤害？

课件答案给出三类。

#### 1. Impersonation and fraud

攻击者可以用克隆声音冒充某人，例如：

- 冒充家人打电话求助转账；
- 冒充公司 CEO 要求财务汇款；
- 冒充银行/客服骗取验证码；
- 冒充员工获取机密信息。

伤害：经济损失、身份盗用、机密泄露。

#### 2. Misinformation and disinformation

Deepfake audio 可以伪造某人讲话：

- 伪造政治人物发言；
- 伪造公司高管声明；
- 伪造公众人物争议言论；
- 制造假新闻和舆论操纵。

伤害：破坏声誉、削弱公众信任、操纵选举或市场。

#### 3. Blackmail and social engineering

克隆声音可以用于威胁或操纵：

- 伪造私人语音进行勒索；
- 用熟人声音诱导受害者行动；
- 对组织进行 social engineering；
- 伪造内部指令绕过安全流程。

> [!important] 答伦理题不能太抽象
> 不要只写“it can be misused”。要给具体、现实的 misuse scenario，并说明对个人和组织的影响。

### 7.2 Q4(ii)：公司应该采取什么防滥用措施？

课件答案强调两类：usage policies / verification，以及 watermarking / identifiers。

更完整可以写成：

#### 1. Strict usage policies

公司应制定明确政策：

- 禁止冒充、欺诈、骚扰、政治操纵；
- 明确允许用途和禁止用途；
- 对商业使用设定更严格审查；
- 对违规账户暂停或封禁。

#### 2. Identity verification

要求用户身份验证：

- KYC 或实名验证；
- 企业账户审核；
- 高风险用途人工审批；
- 防止匿名大规模生成。

#### 3. Consent from voice owners

克隆某人声音前必须取得 consent：

- 声音所有者明确授权；
- 授权范围清楚；
- 可撤销；
- 记录 consent evidence；
- 对已故人物或公众人物需额外伦理审查。

#### 4. Watermarking / unique identifiers

在生成音频中嵌入数字水印或不可感知标记：

- 帮助检测是否由系统生成；
- 便于追踪滥用来源；
- 提高平台审核效率。

#### 5. Monitoring and abuse response

实际系统还需要：

- logging；
- rate limits；
- anomaly detection；
- abuse reporting channel；
- 与平台/执法机构合作；
- 定期 transparency reports。

### 7.3 Q4(iii)：如何应对 adversarial attacks？

题目说 security researchers 发现 adversarial attacks 可以修改 AI-generated voices，使其逃避 deepfake detection。需要提出 technical approach 让 voice cloning / detection 系统更 robust。

课件给出五点，每点 1 mark。

#### 1. Adversarial training

把对抗样本加入训练过程，让模型学会识别轻微扰动后的 deepfake。

解释：

- 攻击者可能加入人耳不明显的噪声或频谱扰动；
- 如果检测器只见过干净 deepfake，就容易被绕过；
- adversarial training 能提高对扰动的鲁棒性。

#### 2. Model regularisation

使用：

- weight decay；
- dropout；
- noise injection；
- data augmentation。

目的：降低模型对某些脆弱特征的过度依赖，使模型不容易被微小扰动欺骗。

#### 3. Multi-modal or hybrid detection

不要只看一种 acoustic feature，而是结合多种线索：

- pitch contour；
- timbre；
- formants；
- MFCC / spectral features；
- prosody；
- linguistic style；
- metadata；
- watermark signal。

这样攻击者需要同时绕过多个检测通道，难度更高。

#### 4. Watermarking and integrity checks

在生成音频中嵌入隐藏信号或完整性标记：

- 正常生成音频应包含水印；
- 如果对抗扰动破坏水印，系统可以发出警报；
- integrity check 可验证音频是否被篡改。

#### 5. Continuous monitoring and updates

攻击方法会不断变化，因此检测系统需要：

- 收集新攻击样本；
- 定期 retrain；
- 更新检测特征；
- 监控误报/漏报；
- 与安全社区共享发现。

> [!summary] Q4 伦理题高分结构
> 先写现实危害，再写公司治理措施，最后写技术防御。每一点都要和 voice cloning / deepfake 直接相关，不要泛泛而谈。

---

## 8. 三类题型的答题模板

### 8.1 算法选择/场景分析题模板

适用于 ICA/PCA、滤波、降噪、source separation、forensics 等题。

```text
1. Identify the task:
   The goal is to ...

2. Describe the audio challenges:
   The recording contains ..., which causes ...

3. Choose the method:
   I would choose ... because ...

4. Explain the processing pipeline:
   preprocessing → feature/time-frequency representation → algorithm → reconstruction → post-processing → evaluation

5. Discuss limitations:
   The method assumes ..., but in this scenario ...

6. Propose improvements:
   Additional techniques include ...

7. Evaluation:
   Use metrics such as ..., plus listening tests.
```

### 8.2 计算题模板

适用于 file size、bitrate、latency、dB gain 等。

```text
Given:
- sample rate = ...
- bit depth = ...
- channels = ...
- duration = ...

Formula:
FileSize = SampleRate × Duration × Channels × BitDepth/8

Substitution:
...

Final answer:
... MB
```

### 8.3 伦理/AI 风险题模板

```text
1. Positive use cases:
   The technology can support ...

2. Misuse scenarios:
   It can be misused for impersonation, fraud, misinformation, blackmail, etc.

3. Harm analysis:
   These harms affect individuals by ..., and organisations by ...

4. Governance measures:
   Require consent, identity verification, strict policies, logging, auditing.

5. Technical safeguards:
   Watermarking, deepfake detection, adversarial training, hybrid detection.

6. Limitations:
   Detection is imperfect; attackers adapt; policy and public education are also needed.
```

---

## 9. 常见失分点

### 9.1 概念题失分

- 只写定义，不写用途。
- 只写算法优点，不写限制。
- PCA 和 ICA 混淆。
- 把 uncorrelated 当成 independent。
- 不解释为什么某方法适合该场景。
- 场景题没有引用题干中的 vehicle noise / crowd chatter / overlapping speech。

### 9.2 计算题失分

- 忘记 bit 到 byte 的转换。
- 忘记 stereo 两个声道。
- 把 kbps 当成 kB/s。
- 忘记时长从分钟转秒。
- MB 换算中 1000 和 1024 混用但不说明。
- 只有答案，没有步骤。

### 9.3 伦理题失分

- 只说“有风险”，没有具体例子。
- 没有区分个人伤害和组织伤害。
- 只谈政策，不谈技术 safeguards。
- 只谈检测，不谈 consent 和治理。
- 没有回答 adversarial manipulation 的鲁棒性问题。

---

## 10. 逐页理解

### Page 1：标题页

主题是 Digital Audio Fundamentals - Course revision。说明这是全课程复习，不是新内容讲义。

### Page 2：Agenda

本次复习包括三件事：

1. EBU5408 考试形式；
2. TB3 和 TB4 主题 outline；
3. 样题、答题方式和 final advice。

### Pages 3-5：Course Topics Outline

列出考试范围，包括：

- 数字音频基础；
- 压缩与处理；
- 音质、噪声、滤波；
- PCA/ICA/source separation；
- 音频特征与机器学习；
- 实时音频；
- 音频取证与修复；
- AI audio 与 ethics。

这三页应该作为复习 checklist。

### Page 6：Exam Format

考试 2 小时，答全部 4 题。计算要展示步骤，场景题要解释理由，必要时画图。课件强调 lecture notes、tutorial exercises 和课堂 examples 中能找到 skeletal solution。

### Page 7：What the Exam Assesses

考察理解、计算、解释、压缩/滤波、真实场景应用、AI audio limitations 和 trade-offs。

### Page 8：Study Hints

复习时要理解 why、advantages、limitations、trade-offs，同时复习计算和概念解释。

### Page 9：Past Exam Q3 场景

给出 noisy urban audio recording：vehicle noise、crowd chatter、overlapping speech。要求选择算法、解释理由、讨论限制、提出改进。

### Page 10：Q3(a) 示例答案

核心：ICA 比 PCA 更适合 isolating voices，因为 ICA 分离 independent components；PCA 主要降维/去噪，不能保证 unmix sources。还要讨论频率重叠和非平稳噪声。

### Page 11：Q3(b) 题干

如果选择 ICA，需要给出详细 step-by-step approach，定义每个阶段，包含 parameter selection 和 expected outcomes；还要讨论 ICA 的限制并提出增强降噪表现的技术。

### Page 12：Q3(b) 示例答案

标准 pipeline：预处理、时频表示、ICA 分离、逆变换、参数选择、后处理、评价。

### Page 13：Past Exam Q4 计算题方向

数字音频存储/压缩场景：计算未压缩文件大小和压缩后文件大小。评分看计算、单位换算和 bitrate 理解。

### Page 14：Q4(a) 题干

AI voice cloning 系统生成 48 kHz、16-bit、stereo、1 分钟 WAV，然后用 128 kbps MP3 压缩。要求计算两个文件大小。

### Page 15：Q4(a)(i) 示例答案

计算未压缩 WAV：16-bit = 2 bytes，stereo = 4 bytes per sample frame，48,000 × 4 = 192,000 bytes/s，乘 60 秒 = 11,520,000 bytes，除以 1024² ≈ 10.98 MB。

### Page 16：Q4 AI voice cloning 场景题

给出正面用途和滥用风险，要求回答 harms、公司防滥用措施、对抗攻击下的技术鲁棒性。

### Page 17：伦理题评分提醒

要识别 realistic misuse scenarios，把 harms 直接连接到 AI voice cloning，同时说明个人和组织影响、技术/伦理/社会后果，表达简洁清楚。

### Page 18：Q4(i)(ii) 示例答案

伤害包括 impersonation/fraud、misinformation/disinformation、blackmail/social engineering。防滥用措施包括 usage policies、verification、consent、watermarking/identifiers。

### Page 19：Q4(iii) 示例答案

提升鲁棒性的方法：adversarial training、regularisation、multi-modal/hybrid detection、watermarking/integrity checks、continuous monitoring and updates。

---

## 11. 考试/复习重点清单

### 11.1 必须会的公式

#### WAV 文件大小

$$
FileSize(bytes)=SampleRate\times Duration\times Channels\times \frac{BitDepth}{8}
$$

#### 压缩文件大小

$$
CompressedSize(bytes)=\frac{Bitrate(bits/s)\times Duration(s)}{8}
$$

#### Buffer latency

$$
Latency(ms)=\frac{BufferSize}{SampleRate}\times1000
$$

#### Round-trip latency

$$
RoundTripLatency(ms)=\frac{BufferSize}{SampleRate}\times1000\times2
$$

#### dB 到线性幅度增益

$$
G=10^{\frac{dB}{20}}
$$

#### SNR

$$
SNR(dB)=10\log_{10}\left(\frac{P_{signal}}{P_{noise}}\right)
$$

### 11.2 必须会比较的概念

| 对比 | 重点 |
|---|---|
| Analog vs Digital | 连续 vs 离散；采样和量化。 |
| Lossless vs Lossy | 完全恢复 vs 更高压缩但有损。 |
| PCA vs ICA | 方差/降维/去噪 vs 独立成分/source separation。 |
| FIR vs IIR | 稳定/线性相位 vs 高效/低延迟。 |
| Online vs Batch | 实时低延迟 vs 离线高质量/复杂算法。 |
| Restoration vs Forensics | 好听/清晰 vs 真实/可追溯/可作为证据。 |
| Voice cloning vs Deepfake | 技术能力 vs 常带欺骗语境的伪造内容。 |

### 11.3 必须会解释的 pipelines

#### Audio compression pipeline

```text
frame splitting → windowing → transform/MDCT → psychoacoustic model → quantisation → entropy coding → bitstream
```

#### ICA speech separation pipeline

```text
preprocessing → STFT/spectrogram → ICA → inverse transform → post-processing → evaluation
```

#### Audio ML pipeline

```text
data collection/labelling → preprocessing → feature extraction → model training → evaluation → deployment
```

#### Forensic audio workflow

```text
preserve original → forensic copy → hash/integrity check → metadata/spectrogram/ENF analysis → minimal enhancement → documented report
```

#### AI voice cloning risk mitigation

```text
consent → identity verification → usage policy → watermarking → monitoring → detection → updates
```

---

## 12. 一页速记

> [!summary] Block 4 第 3 组 PPT 速记
> - 这组课件是 course revision：复习范围、考试形式、样题和评分标准。
> - 考试 2 小时，答全部 4 题；先浏览全卷，计算题写步骤，场景题写理由。
> - 复习重点不是背定义，而是解释 why、trade-off、limitations 和 real-world application。
> - 全课程主题包括数字音频基础、压缩、滤波、PCA/ICA、音频特征、ML、实时音频、取证、AI ethics。
> - Noisy urban recording 题：ICA 更适合 source separation；PCA 更偏降维/去噪。
> - ICA pipeline：预处理 → STFT/spectrogram → ICA → inverse transform → 参数选择 → 后处理 → SNR/SDR/PESQ/STOI/听感评价。
> - ICA 限制：频率重叠、非平稳噪声、混响、独立性假设、成分数量、artifacts。
> - WAV 大小：`SampleRate × Duration × Channels × BitDepth/8`。
> - 48 kHz / 16-bit / stereo / 60s WAV：约 11 MB。
> - 128 kbps MP3 / 60s：约 0.92 MiB 或 0.96 MB。
> - Voice cloning 风险：impersonation、fraud、misinformation、blackmail、social engineering。
> - 防滥用：consent、identity verification、usage policy、watermarking、logging、monitoring。
> - 对抗鲁棒性：adversarial training、regularisation、hybrid detection、watermark/integrity checks、continuous updates。

---

## 13. 和 Block 4 其他内容的连接

- 与 [[Block 4 - PPT 1：Audio Quality, Noise, and Digital Filtering II|PPT 1]] 的连接：样题 Q3 的 post-processing、SNR/SDR/PESQ/STOI、滤波和降噪都依赖 PPT 1 中的音质评价与滤波知识。
- 与 [[Block 4 - PPT 2：Real-Time Audio Processing, Machine Learning, Ethics and Forensics|PPT 2]] 的连接：样题 Q4 的 voice cloning ethics、deepfake detection、forensics、实时系统和 ML features 都来自 PPT 2。
- 与 Block 3 的连接：PCA/ICA、source separation、filtering 是样题 Q3 的核心基础。
- 与实验/作业的连接：如果实验涉及降噪、分类、分离或 AI 音频，需要在报告中明确 pipeline、参数、评价指标和局限。
