---
title: EBU5408 Block 4 - PPT 2：Real-Time Audio Processing, Machine Learning, Ethics and Forensics
aliases:
  - Block 4 PPT 2
  - Real-Time Audio Processing and ML
  - Audio ML Ethics Forensics
  - Digital Audio ML
  - AI and Ethics
  - Audio Forensic
tags:
  - course/音频处理
  - EBU5408
  - digital-audio
  - block4
  - real-time-audio
  - machine-learning
  - MFCC
  - AI-ethics
  - audio-forensics
source:
  - "[[../附件/Block 4 - Applied Digital Audio Processing/2 ML, Ethics and other/Audio Processing.pdf]]"
  - "[[../附件/Block 4 - Applied Digital Audio Processing/2 ML, Ethics and other/Digital Audio ML_1.pdf]]"
  - "[[../附件/Block 4 - Applied Digital Audio Processing/2 ML, Ethics and other/MFCC.pdf]]"
  - "[[../附件/Block 4 - Applied Digital Audio Processing/2 ML, Ethics and other/Digital Audio AI and Ethics.pdf]]"
  - "[[../附件/Block 4 - Applied Digital Audio Processing/2 ML, Ethics and other/Digital Audio Forensic.pdf]]"
created: 2026-06-17
---

# Block 4 - PPT 2：Real-Time Audio Processing, Machine Learning, Ethics and Forensics

> [!info] 课件来源
> 本笔记对应 Block 4 第 2 组课件，位于：`Block 4 - Applied Digital Audio Processing/2 ML, Ethics and other`。
>
> 包含以下主课件：
> - [[../附件/Block 4 - Applied Digital Audio Processing/2 ML, Ethics and other/Audio Processing.pdf]]
> - [[../附件/Block 4 - Applied Digital Audio Processing/2 ML, Ethics and other/Digital Audio ML_1.pdf]]
> - [[../附件/Block 4 - Applied Digital Audio Processing/2 ML, Ethics and other/MFCC.pdf]]
> - [[../附件/Block 4 - Applied Digital Audio Processing/2 ML, Ethics and other/Digital Audio AI and Ethics.pdf]]
> - [[../附件/Block 4 - Applied Digital Audio Processing/2 ML, Ethics and other/Digital Audio Forensic.pdf]]

## 0. 本组课件的整体逻辑

Block 4 的主题是 **Applied Digital Audio Processing（应用型数字音频处理）**。第 1 组课件已经讲了音频滤波、音质评价和客观指标。第 2 组课件继续往应用方向展开，主要包含五个模块：

1. **Real-time audio processing**：实时音频系统如何在极低延迟下运行。
2. **Machine learning in audio**：机器如何从声音中学习模式。
3. **MFCC**：音频机器学习中最常用的语音/音色特征之一。
4. **AI audio generation and ethics**：AI 生成声音、TTS、语音克隆、deepfake 及伦理问题。
5. **Audio forensics**：音频修复、认证、取证、证据链和法律可靠性。

> [!summary] 一句话主线
> 本组课件从“如何实时处理声音”讲到“机器如何理解与生成声音”，再讲到“这些技术如何被负责任地使用、评估和作为证据处理”。

---

# A. Real-Time Audio Processing

## 1. 什么是实时音频处理？

**Real-time audio processing（实时音频处理）**指音频在进入系统的同时被处理，并且必须在极短时间内输出。

典型场景包括：

- 现场演出监听；
- 麦克风实时降噪；
- 直播效果器；
- 电子乐器合成器；
- DAW 中的实时插件；
- 游戏音频引擎；
- 视频会议语音处理。

课件的核心定义是：

```text
Audio is processed as it arrives.
Processing must be completed before the next block arrives.
```

也就是说，系统不能“慢慢算”。如果下一块音频已经来了，而上一块还没处理完，就会出现 glitch 或 dropout。

---

## 2. 实时系统的三个核心约束

实时音频系统必须平衡：

1. **Speed**：处理速度要够快；
2. **Quality**：处理质量要尽可能好；
3. **Stability**：系统要稳定，不能爆音、卡顿或崩溃。

### 2.1 Performance requirements

课件列出的 performance requirements 包括：

- low latency；
- consistent processing times；
- handling concurrent operations。

也就是说，不只是平均速度要快，还要每一块 buffer 都稳定按时完成。

### 2.2 System resources

系统资源包括：

- CPU load；
- RAM usage；
- audio interface capabilities。

如果 CPU 太忙、内存不足，或者 audio interface driver 不够低延迟，都可能导致实时处理失败。

### 2.3 Trade-offs

实时系统最重要的是 trade-off：

| Trade-off | 解释 |
|---|---|
| Quality vs Speed | 高质量算法通常更复杂、更慢 |
| Complexity vs Real-time | 算法越复杂，越难按时处理完 buffer |
| Latency vs Stability | buffer 越小延迟越低，但越容易 glitch |

例如：

- high-fidelity convolution reverb 听起来真实，但计算重；
- simpler reverb 更适合实时演出；
- mastering 可以 offline rendering，不需要实时；
- live performance 必须实时稳定。

---

## 3. Latency：延迟

### 3.1 Latency 的定义

**Latency（延迟）**是输入和输出之间的时间差。

在音频中，latency 通常以 ms 表示。

```text
Latency = delay between input and output
```

延迟越低，系统响应越自然；延迟越高，演奏者或说话者越容易感觉到“不跟手”。

### 3.2 Latency 类型

课件列出：

| 类型 | 含义 |
|---|---|
| Input latency | 麦克风/乐器进入系统的延迟 |
| Output latency | 系统输出到耳机/扬声器的延迟 |
| Round-trip latency | input + processing + output 总延迟 |

在现场演出中，round-trip latency 最重要，因为演奏者关心的是“我发出的声音多久之后从监听里回来”。

### 3.3 为什么 latency 重要？

高 latency 会导致：

- 演奏 timing 变差；
- 歌手耳机监听不舒服；
- 说话反馈不自然；
- 乐器响应不跟手；
- 游戏或 VR 音频沉浸感下降。

课件中给出的 live performance 可接受范围大约是：

```text
10-12 ms：通常可接受
< 6 ms：非常低，理想
```

---

## 4. Audio buffers：缓冲区

### 4.1 为什么要用 buffer？

计算机通常不是一个 sample 一个 sample 地处理音频，而是把音频分成小块，也就是 buffers。

```text
continuous audio stream → small blocks / buffers → process each buffer
```

每个 buffer 包含短时间的 audio samples。

### 4.2 Buffer size 的影响

| Buffer size | 优点 | 缺点 |
|---|---|---|
| Large buffer | 更稳定，CPU 有更多时间处理 | 延迟更高 |
| Small buffer | 延迟低，响应快 | CPU 压力大，容易 glitch/dropout |

因此，buffer size 是实时音频系统中最关键的参数之一。

### 4.3 Buffer underrun

如果系统无法在下一块 buffer 到来之前完成当前处理，就会出现 buffer underrun。

结果可能是：

- click；
- pop；
- dropout；
- glitch；
- audio stream interruption。

---

## 5. Latency 计算

### 5.1 基本公式

单向 buffer latency：

$$
Latency(ms)=\frac{BufferSize}{SampleRate}\times1000
$$

如果计算 round-trip latency，课件中使用乘以 2：

$$
RoundTripLatency(ms)=\frac{BufferSize}{SampleRate}\times1000\times2
$$

### 5.2 例题：256 samples, 48 kHz

题目：buffer size = 256 samples，sample rate = 48 kHz，求 round-trip latency。

$$
Latency=\frac{256}{48000}\times1000\times2
$$

先算单向：

$$
\frac{256}{48000}=0.00533s
$$

$$
0.00533\times1000=5.33ms
$$

round-trip：

$$
5.33\times2=10.66ms
$$

所以约为：

```text
10.7 ms
```

这在现场演出中通常属于可接受范围，但不是超低延迟。

### 5.3 例题：128 samples, 48 kHz

$$
Latency=\frac{128}{48000}\times1000\times2
$$

单向：

$$
\frac{128}{48000}\times1000=2.67ms
$$

round-trip：

$$
2.67\times2=5.33ms
$$

所以约为：

```text
5.3 ms
```

这更适合实时演出，但 CPU 压力更大。

### 5.4 采样率对 latency 的影响

在 buffer size 固定时：

```text
sample rate 越高，每个 sample 对应的时间越短，buffer 时间越短
```

因此更高 sample rate 可以降低 buffer latency，但也会增加每秒处理的 sample 数，使 CPU 负担增加。

---

## 6. 管理 latency 的策略

课件列出三类策略。

### 6.1 Low-latency audio drivers

常见低延迟音频驱动：

- ASIO；
- Core Audio；
- WASAPI。

这些驱动能减少软件与硬件之间的通信延迟。

### 6.2 System optimization

可以通过系统优化降低 glitch 风险：

- 使用高性能电源模式；
- 关闭无关后台进程；
- 减少 CPU load；
- 避免实时处理时运行重负载程序。

### 6.3 Direct hardware monitoring

Direct monitoring 指从 audio interface 直接监听输入信号，而不是经过 DAW 或软件处理后再听。

优点：

- 几乎零延迟；
- 适合录音监听。

缺点：

- 听不到软件效果器处理后的声音，除非硬件本身支持 DSP 效果。

---

## 7. Online vs Batch Processing

课件区分：

| 类型 | 处理方式 | 特点 |
|---|---|---|
| Online processing | sample by sample 或实时 buffer | 低延迟，适合 live systems |
| Batch processing | 一次处理一块或整段音频 | 延迟更高，但可用复杂算法 |

### 7.1 Online processing

适用于：

- live performance；
- voice chat；
- real-time effects；
- instrument processing。

要求：

- causal；
- low latency；
- stable；
- predictable computation time。

### 7.2 Batch processing

适用于：

- mastering；
- offline restoration；
- dataset feature extraction；
- training ML models；
- high-quality rendering。

优势：

- 可以使用更复杂算法；
- 可以重复处理；
- 可以查看未来 samples；
- 更灵活。

---

## 8. 实时音频系统的核心模块

课件列出四个 core building blocks。

### 8.1 Oscillators

Oscillators 生成基本波形：

- sine；
- square；
- saw；
- triangle；
- noise。

它们是合成器和音频测试信号的基础。

### 8.2 Filters

Filters 改变频率内容：

- remove unwanted frequencies；
- enhance useful frequencies；
- shape tone；
- create effects。

### 8.3 Envelopes

Envelopes 控制声音如何随时间变化，常见 ADSR：

- Attack；
- Decay；
- Sustain；
- Release。

例如钢琴音的快速 attack 和逐渐 decay，与管风琴持续音非常不同。

### 8.4 Effects

Effects 对声音进行变换：

- reverb；
- delay；
- distortion；
- chorus；
- flanger；
- compression。

效果越复杂，CPU 负担越高，也越难满足实时约束。

---

## 9. Real-time audio patch 的运行方式

实时系统通常按如下流程运行：

```text
continuous input
→ divide into buffers
→ process each buffer
→ playback/output
```

每个 buffer 的处理可能包括：

- signal generation；
- filtering；
- effects；
- mixing；
- parameter updates。

处理必须在下一块 buffer 到来前完成。

### 9.1 系统参数

| 参数 | 作用 |
|---|---|
| Sample rate | 每秒 sample 数，如 48 kHz |
| Buffer size | 决定 latency 与 CPU load |
| Dynamic control | 参数可实时变化，如 frequency、gain |
| System stability | start/stop、资源释放、异常处理必须稳定 |

### 9.2 实时代码中的 callback

课件 Python 示例使用 `sounddevice` 的 callback。callback 的作用是：每当系统需要下一块输出 buffer 时，就调用函数生成或处理音频。

核心逻辑：

```python
def audio_callback(outdata, frames, time, status):
    # generate/process frames samples
    # write output into outdata
```

如果 callback 运行太慢，就会出现声音中断。

### 9.3 实时参数更新

课件示例中，另一个 thread 允许用户输入新的 frequency。这样 oscillator 的频率可以在运行中改变。

这体现了 real-time parameter updates 的挑战：

- 参数改变不能打断音频流；
- 多线程可能有并发问题；
- 参数变化最好平滑，避免 clicks。

---

## 10. Real-time audio effects：delay 示例

课件展示了 delay effect 的基本实现。

### 10.1 Delay 的原理

Delay 效果就是把过去的声音延迟一段时间后再混回当前输出。

```text
output = dry signal + delayed signal
```

### 10.2 Circular buffer

实时 delay 常用 circular buffer 保存过去的 samples。

步骤：

1. 当前输入 sample 进入 buffer；
2. 从 buffer 中读出延迟位置的 sample；
3. 把当前 sample 和 delayed sample 相加；
4. 更新 buffer index；
5. 如果有 feedback，把 delayed sample 的一部分写回 buffer。

### 10.3 Feedback

课件中 feedback = 0.5，表示延迟声有 50% 被反馈回延迟线。

feedback 越高，echo 重复越久；太高可能导致失控或过载。

---

# B. Machine Learning in Audio

## 11. 音频机器学习是什么？

**Machine learning in audio** 指让机器从声音数据中学习模式。

课件把应用分为三类。

### 11.1 Audio classification

Audio classification 把声音分类。

例子：

- speech vs music；
- guitar vs piano；
- speaker identification；
- car horn；
- dog bark；
- environmental sound classification。

### 11.2 Audio generation

Audio generation 生成新的声音。

例子：

- AI music composition；
- text-to-speech；
- sound effect generation。

### 11.3 Audio transformation

Audio transformation 修改已有声音。

例子：

- music style transfer；
- source separation；
- noise reduction；
- voice conversion。

---

## 12. Raw audio 的挑战

### 12.1 Raw waveform 高维

CD quality audio 每秒 44,100 samples。如果输入 10 秒音频，就已经有 441,000 个样本。

这会导致：

- dimensionality high；
- computation expensive；
- temporal dependencies complex；
- redundancy large；
- model hard to train。

### 12.2 为什么需要 feature extraction？

大多数传统 ML 模型不适合直接处理 raw waveform。因此需要把音频转换成 compact and informative numerical representation。

Feature extraction 的目标：

```text
raw audio → compact features → ML model
```

好的特征应该：

- 保留任务相关信息；
- 去除不必要冗余；
- 降低维度；
- 更适合模型学习。

---

## 13. Time-domain features

Time-domain features 直接从 waveform samples 中计算，通常在短帧内计算。

### 13.1 Zero-Crossing Rate（ZCR）

**ZCR** 是信号穿过零轴的次数。

直观意义：

- 高频或噪声多的信号通常 ZCR 高；
- 平滑、低频信号通常 ZCR 低。

用途：

- speech/music 区分；
- voiced/unvoiced detection；
- noisiness estimation；
- percussive sound detection。

### 13.2 Energy / RMS Energy

RMS energy 衡量一帧内信号的平均幅度或响度。

公式直观为：

$$
RMS = \sqrt{\frac{1}{N}\sum_{n=1}^{N}x[n]^2}
$$

用途：

- loudness estimation；
- silence detection；
- onset detection；
- sound event detection。

---

## 14. Frequency-domain features

Frequency-domain features 基于 spectrum，通常通过 Fourier Transform 或 STFT 获得。

### 14.1 Spectral centroid

**Spectral centroid** 是频谱的“重心”。

它表示大部分频率能量集中在哪里。

直观解释：

- centroid 高 → 声音更 bright；
- centroid 低 → 声音更 dark / dull。

例如镲片的 spectral centroid 通常高于低音鼓。

### 14.2 Spectral roll-off

**Spectral roll-off** 是某个频率阈值，低于该频率的能量占总能量的某个比例，例如 85% 或 95%。

用途：

- 判断频谱带宽；
- 区分明亮和低沉声音；
- 检测高频含量。

### 14.3 MFCC

**MFCC（Mel-Frequency Cepstral Coefficients）** 是语音和音乐处理中非常常见的特征。

它的特点：

- 使用 Mel scale，接近人耳 pitch perception；
- 压缩 spectral shape；
- 捕捉 timbral characteristics；
- 在 speech recognition、speaker recognition、music classification 中很常用。

### 14.4 Chroma features

Chroma features 把频谱能量映射到 12 个西方音级：

```text
C, C#, D, D#, E, F, F#, G, G#, A, A#, B
```

适合：

- harmony analysis；
- chord recognition；
- melody analysis；
- music similarity。

### 14.5 Spectral contrast

Spectral contrast 衡量不同频带中 peaks 和 valleys 的差异。

它与声音 texture、clarity 有关。

---

## 15. Audio ML pipeline

课件给出标准 pipeline：

```text
Data collection & labelling
→ Preprocessing
→ Feature extraction
→ Model selection & training
→ Evaluation
→ Deployment / inference
```

### 15.1 Data collection & labelling

收集音频文件并标注标签。

例如：

- genre；
- word spoken；
- speaker identity；
- sound type。

监督学习中，标签质量非常关键。

### 15.2 Preprocessing

常见预处理包括：

- resampling；
- normalization；
- trimming silence；
- segmentation into frames；
- noise reduction；
- balancing dataset。

### 15.3 Feature extraction

从每段音频中提取特征，例如：

- MFCCs；
- ZCR；
- RMS；
- spectral centroid；
- chroma；
- spectrogram。

### 15.4 Model selection and training

传统模型：

- KNN；
- SVM；
- Random Forest；
- Logistic Regression。

深度学习模型：

- CNN；
- RNN；
- Transformers；
- raw audio models。

### 15.5 Evaluation

用 validation/test data 评估模型。

常见指标：

- accuracy；
- precision；
- recall；
- F1-score；
- confusion matrix。

### 15.6 Deployment

把训练好的模型用于新音频：

- classification；
- generation；
- transformation；
- real-time inference。

> [!important] 课件提醒
> Most errors come from data and feature extraction. 也就是说，模型表现不好不一定是算法太弱，可能是数据和特征出了问题。

---

## 16. 模型评价指标

### 16.1 Confusion matrix 基础

| 名称 | 含义 |
|---|---|
| TP | 正类预测为正类 |
| TN | 负类预测为负类 |
| FP | 负类错误预测为正类，Type I error |
| FN | 正类错误预测为负类，Type II error |

### 16.2 Accuracy

$$
Accuracy=\frac{TP+TN}{TP+TN+FP+FN}
$$

表示总体预测正确率。

### 16.3 Precision

$$
Precision=\frac{TP}{TP+FP}
$$

表示模型预测为正类时，有多少是真的正类。

适合关注误报成本的任务，例如枪声检测中误报可能导致不必要警报。

### 16.4 Recall

$$
Recall=\frac{TP}{TP+FN}
$$

表示真实正类中有多少被找出来。

适合关注漏报成本的任务，例如安全警报检测中漏掉真实警报非常危险。

### 16.5 F1-score

$$
F1=2\times\frac{Precision\times Recall}{Precision+Recall}
$$

F1 平衡 precision 和 recall，适合类别不平衡或同时关心误报与漏报的任务。

---

## 17. 音乐流派分类例子

课件示例：自动把短音乐片段分类为：

- Blues；
- Classical；
- Jazz；
- Metal；
- Pop；
- Rock。

基本步骤：

1. Load audio；
2. Extract MFCCs；
3. Prepare train/test split；
4. Train classifier，例如 KNN 或 SVM；
5. Evaluate accuracy、confusion matrix 等。

GTZAN 是常用 benchmark，但课件也提醒它存在 label issues。

---

## 18. Python 工具

课件列出常用工具：

| 工具 | 用途 |
|---|---|
| librosa | audio analysis and feature extraction |
| scikit-learn | classical ML algorithms and evaluation |
| TensorFlow | deep learning |
| PyTorch | deep learning |

---

## 19. 应用与研究方向

### 19.1 Speech recognition

用于：

- Siri；
- Alexa；
- Google Assistant；
- dictation；
- automatic captioning。

### 19.2 Music recommendation and analysis

用于：

- Spotify；
- Apple Music；
- similar songs；
- user preference modelling。

### 19.3 Speaker identification / verification

用于：

- security；
- personalization；
- forensic comparison。

### 19.4 Acoustic scene classification

识别环境：

- office；
- street；
- restaurant；
- train station。

### 19.5 Deep learning

CNN/RNN/Transformers 可以直接处理 spectrogram，甚至 raw audio，通常在大数据下表现更强。

### 19.6 Source separation

用深度学习分离：

- vocals；
- drums；
- instruments；
- target sound。

### 19.7 Generative models

生成：

- realistic speech；
- music；
- sound effects。

### 19.8 Edge devices

在 smartphones、IoT 等低功耗设备上实时运行模型，要求模型高效、低延迟。

---

# C. MFCC

## 20. MFCC 在本组课件中的作用

MFCC 是音频机器学习中最经典的特征之一。虽然课件页数较少，但它连接了前面的 feature extraction 和后面的 speaker recognition、speech classification。

MFCC 的目标是：

```text
把一帧音频的频谱形状压缩成少量数字，用来描述 timbre / speech characteristics
```

---

## 21. Frame length 和 hop size

### 21.1 为什么要分帧？

语音和音乐是随时间变化的，但在很短时间内可以近似认为相对稳定。因此通常将音频分成短帧。

常见 frame length：

```text
20-40 ms
```

常见 hop size：

```text
10-20 ms
```

### 21.2 frame length 转 samples

公式：

$$
Number\ of\ samples = sampling\ rate\times time(seconds)
$$

课件例子：25 ms，48 kHz。

$$
25ms=0.025s
$$

$$
48000\times0.025=1200\ samples
$$

### 21.3 hop size 例题

题目：sampling rate = 32 kHz，hop size = 15 ms。

$$
15ms=0.015s
$$

$$
32000\times0.015=480\ samples
$$

所以 hop size 是 480 samples。

---

## 22. Time resolution vs frequency resolution

课件强调：frame 长度会影响时间分辨率和频率分辨率。

| Frame | 优点 | 缺点 |
|---|---|---|
| Short frame | 好的 time resolution，能捕捉快速变化 | samples 少，frequency resolution 差 |
| Long frame | 好的 frequency resolution，频率更精细 | 平均时间更长，快速变化不清楚 |

这是 STFT、MFCC、spectrogram 中非常重要的 trade-off。

### 22.1 直观例子

如果要检测鼓点或爆破音，需要较短 frame，因为事件变化快。

如果要精确分析稳定音高或谐波，需要较长 frame，因为频率分辨率更好。

---

## 23. MFCC 的常见计算流程

虽然课件没有完整列出全部步骤，但为了理解 MFCC，应掌握以下流程：

```text
audio waveform
→ framing
→ windowing
→ FFT / power spectrum
→ Mel filterbank
→ log energies
→ DCT
→ MFCC coefficients
```

### 23.1 Framing

把音频切成短帧，例如 25 ms。

### 23.2 Windowing

每帧乘以 window function，例如 Hamming window，减少边界突变。

### 23.3 FFT

把每帧从时域变到频域，得到 spectrum。

### 23.4 Mel filterbank

用 Mel scale 模拟人耳对 pitch 的非线性感知。

人耳对低频更敏感，对高频分辨率较低。因此 Mel scale 在低频更密、高频更疏。

### 23.5 Log energies

对每个 Mel filter 输出取 log，模拟人耳对 loudness 的近似对数感知。

### 23.6 DCT

用 DCT 压缩 log Mel spectrum，得到少量 cepstral coefficients。

常用前 12 或 13 个 MFCC。

---

# D. AI Audio Generation and Ethics

## 24. AI 如何学习生成声音？

AI 音频生成模型通常训练在大规模音频库上，例如：

- speech data；
- music；
- sound effects；
- ambient noise。

模型通过深度学习寻找声音中的 patterns and structures。

例如：

- frequency relationships；
- rhythm；
- melody structure；
- speech prosody；
- timbre；
- ambient texture。

课件称之为 massive pattern recognition。

---

## 25. 常见生成模型

### 25.1 GANs

**GANs（Generative Adversarial Networks）**由 generator 和 discriminator 组成。

- generator 尝试生成逼真音频；
- discriminator 判断音频是真实还是生成；
- 两者竞争，生成器逐渐变强。

### 25.2 VAEs

**VAEs（Variational Autoencoders）**把音频编码到 latent space，再从 latent representation 解码生成新音频。

适合学习连续的潜在表示和生成变体。

### 25.3 Transformers

Transformers 最初用于语言，现在也用于 audio/music generation。

优点是能建模长距离依赖，例如音乐结构、句子节奏、上下文连贯性。

### 25.4 Diffusion models

Diffusion models 通过逐步 denoise 生成数据。

它们在图像生成中非常成功，也越来越多用于 audio generation。

---

## 26. Modern TTS

### 26.1 早期 TTS vs neural TTS

早期 TTS 包括 concatenative 和 parametric systems，听起来往往机械、不自然。

现代 neural TTS 可以生成高度真实的语音。

### 26.2 Modern TTS 能建模什么？

课件列出：

- prosody；
- intonation；
- emotion；
- voice styles。

也就是说，现代 TTS 不只是读字，还能模拟：

- 语速；
- 重音；
- 停顿；
- 情绪；
- 说话风格。

### 26.3 TTS 应用

| 应用 | 例子 |
|---|---|
| Accessibility | screen readers |
| Communication aids | voice banking |
| Virtual assistants | Siri, Alexa, chatbots |
| Content creation | video voiceover, audiobooks |
| Gaming | dynamic NPC dialogue |

---

## 27. AI music and sound generation

AI 可以用于：

- style imitation；
- prompt-based music generation；
- interactive co-creation；
- stem separation；
- infinite soundtracks；
- sound effect synthesis。

### 27.1 Positive uses

- 帮助音乐人快速构思；
- 为广告、电影、游戏快速原型；
- 生成 royalty-free content；
- 个性化音乐流；
- relaxation/focus/sleep therapeutic music；
- 降低音乐创作门槛。

### 27.2 风险

- 版权争议；
- 模仿特定艺术家；
- 未经授权使用训练数据；
- 生成内容归属不清；
- 大量低成本内容冲击创作者生态。

---

## 28. Voice cloning and audio deepfakes

### 28.1 Voice cloning

Voice cloning 是构建能模仿某个人声音的 AI 模型。

通常需要目标声音样本。过去可能需要数小时高质量录音，现在 few-shot 或 zero-shot 方法可能只需要几分钟甚至几秒。

### 28.2 Audio deepfake

Audio deepfake 是让某个人“听起来像说了他没有说过的话”。

它常带有欺骗或恶意语境。

### 28.3 Voice conversion

Voice conversion 是把已有 speech 转换成另一个 target speaker 的声音。

与 TTS 不同，voice conversion 通常保留源语音内容和节奏，但改变说话人音色。

---

## 29. Voice cloning 的工作流程

### Step 1：Data collection

收集目标声音样本。

来源可能是：

- 公开视频；
- podcast；
- 电话录音；
- 社交媒体；
- studio recordings。

伦理风险在于：很多样本可能未经授权。

### Step 2：Model training

模型学习 speaker identity，例如：

- timbre；
- pitch；
- accent；
- speaking style。

它会形成 voice embedding 或 digital voiceprint。

### Step 3：Synthesis / conversion

可以通过：

- text + voiceprint → cloned speech；
- source audio + target voice → converted speech；
- real-time conversion → 即时变声。

---

## 30. Voice cloning 的评价

### 30.1 Objective evaluation

可比较：

- MFCCs；
- spectral characteristics；
- speaker embeddings；
- pitch contour；
- formants。

### 30.2 Subjective evaluation

使用 MOS 测试评价：

- speech quality；
- naturalness；
- speaker similarity。

### 30.3 性能差异原因

课件提到 female voice clones 比 male voice clones 表现更好，可能原因包括：

- spectral characteristics differences；
- feature extraction limitations；
- dataset imbalance。

其中 dataset imbalance 很重要：如果训练集中某类声音样本少，模型往往表现更差。

### 30.4 中文语音克隆挑战

课件指出 Chinese speech cloning 比 English 更难，可能因为：

- 中文训练数据更稀缺；
- 中文 prosody 更复杂；
- 声调语言对 pitch contour 更敏感；
- 模型结构仍需改进。

---

## 31. AI audio 的伦理问题

### 31.1 正面应用

| 场景 | 好处 |
|---|---|
| Medical/accessibility | voice banking for patients losing speech |
| Entertainment | ethical recreation with consent |
| Dubbing | actor consent-based multilingual dubbing |
| Education/content | faster production |

### 31.2 负面应用

| 风险 | 例子 |
|---|---|
| Scams | 冒充家人紧急求助 |
| Corporate fraud | 假 CEO 电话要求转账 |
| Political manipulation | 伪造政客录音影响选举 |
| Blackmail | 伪造语音进行威胁 |
| Misinformation | 虚假音频传播谣言 |

### 31.3 Consent and permission

克隆真实人物声音时，最重要的问题是 consent。

应明确：

- 谁允许使用声音；
- 用于什么目的；
- 是否可撤回；
- 是否可商业化；
- 是否可用于训练模型；
- 是否可生成新内容。

### 31.4 Technical countermeasures

课件提到：

- detection algorithms；
- watermarking；
- digital fingerprints。

此外，还需要公众教育和政策监管。

### 31.5 Policy and regulation

监管挑战包括：

- 跨国数据；
- 匿名在线传播；
- 取证难度；
- 合法创作和恶意伪造之间界限复杂。

---

# E. Audio  Forensics

## 32. Audio restoration vs forensic audio

### 32.1 Audio restoration

Audio restoration 是改善录音质量的过程。

目标通常是：

- remove noise；
- reduce clicks/pops；
- reduce distortion；
- improve listenability；
- preserve original content。

常见于：

- old recordings；
- poor recording environments；
- damaged audio files。

### 32.2 Forensic audio

Forensic audio 用于法律和调查目的。

目标不是简单“让声音好听”，而是：

- authenticate recordings；
- enhance intelligibility；
- identify speakers；
- analyze recording conditions；
- preserve evidence integrity。

### 32.3 核心区别

| 对比 | Restoration | Forensics |
|---|---|---|
| 目标 | 感知质量更好 | 真实性、可懂度、法律可靠性 |
| 处理方式 | 可较积极 | 保守、可追溯、最小改动 |
| 输出要求 | 好听/清晰 | 可作为证据、可复现 |
| 风险 | artifacts | 改变证据含义 |

---

## 33. 常见音频问题

### 33.1 Noise

- broadband noise：hiss，宽频噪声；
- tonal noise：hum，50/60 Hz 及 harmonics。

### 33.2 Clipping / distortion

录音电平太高导致 waveform peaks flattened。

问题：信息已经丢失，很难完全修复。

### 33.3 Clicks and pops

短促 impulsive sounds，常见于：

- vinyl defects；
- digital errors；
- packet glitches。

### 33.4 Speed / pitch irregularities

模拟录音中常见：

- wow：慢速 pitch variations；
- flutter：快速 pitch variations。

这些会影响 pitch 和 timing。

---

## 34. Digital restoration techniques

### 34.1 Noise reduction

目标是减少背景噪声，同时保留原始信号。

### 34.2 Spectral subtraction

流程：

```text
estimate noise profile → subtract from signal spectrum
```

风险：过度处理会产生 watery 或 robotic artifacts。

### 34.3 Adaptive filtering

Adaptive filtering 动态调整滤波器，以适应变化的噪声。

适合非静态噪声。

### 34.4 De-clicking / de-crackling

检测 sharp transients，然后用 interpolation 或 replacement 修复。

### 34.5 De-reverb

De-reverb 减少房间反射和 echo。

为什么难？

- reverb 与原始信号深度混合；
- aggressive processing 会损伤语音；
- 仍是活跃研究方向。

### 34.6 Tools

常用工具：

- iZotope RX；
- Audacity；
- MATLAB；
- Python librosa/scipy。

---

## 35. Audio forensics 的关键原则

### 35.1 Authenticity

必须确认录音是否原始、是否被篡改。

### 35.2 Intelligibility

取证增强常关注 speech intelligibility，而不是音乐音质。

### 35.3 Minimal processing

处理应尽量 minimal and precise：

- careful EQ；
- selective filtering；
- avoid artifacts；
- avoid changing meaning。

### 35.4 Chain of custody

证据链记录音频证据从获取到分析的全过程。

包括：

- 谁接触过文件；
- 何时复制；
- 使用了什么工具；
- 是否生成 hash；
- 原始文件是否保持不变。

---

## 36. Evidence acquisition

### 36.1 Forensic copying

使用 write-blockers 和 forensic imaging tools 创建精确副本，避免改变原始数据。

### 36.2 Integrity verification

使用 hash 作为数字指纹：

- MD5；
- SHA-1；
- SHA-256。

如果文件被修改，hash 会变化。

### 36.3 Metadata inspection

检查：

- timestamps；
- software tags；
- sample rate；
- bit depth；
- codec；
- editing traces。

---

## 37. Authentication and tamper detection

### 37.1 ENF analysis

**ENF（Electrical Network Frequency）**分析利用电网频率微小波动来验证录音时间和连续性。

如果录音中包含 50/60 Hz hum，可以与电网频率数据库比较。

### 37.2 Spectrogram analysis

用 STFT 可视化频率随时间变化。

可发现：

- abrupt edits；
- duplicated segments；
- unnatural gaps；
- inconsistent noise floor。

### 37.3 Phase analysis

剪辑点可能破坏 phase continuity。

Phase analysis 可帮助发现 splicing。

### 37.4 Feature-based detection

从滑动窗口中提取 features，并用 ML 检测异常模式。

---

## 38. Forensic enhancement

### 38.1 Noise reduction

可以使用：

- spectral subtraction；
- Wiener filtering；
- MMSE filtering。

目标是提高 intelligibility，但不能改变证据含义。

### 38.2 De-reverberation

方法包括：

- Room Impulse Response modelling；
- inverse filtering；
- blind deconvolution。

### 38.3 Transcoding and resampling

格式转换可能导致 timing inconsistencies。取证中需要谨慎 resampling，例如使用 polyphase filters。

---

## 39. Speaker recognition

### 39.1 Feature extraction

提取 speaker-specific voice features，例如：

- MFCCs；
- Constant-Q cepstral features。

### 39.2 Speaker modeling

方法包括：

- GMM-UBM；
- i-vectors；
- x-vectors。

### 39.3 Speaker comparison

比较 unknown voice 和 known speaker database。

方法包括：

- PLDA；
- deep neural network classifiers。

### 39.4 Evaluation metrics

常见指标：

- EER（Equal Error Rate）；
- DCF（Detection Cost Function）。

EER 是 false acceptance 与 false rejection 相等时的错误率。

---

## 40. Reporting and software

取证报告必须记录：

- processing steps；
- software versions；
- parameter settings；
- file hashes；
- outputs；
- limitations。

常见输出：

- spectrograms；
- ENF correlation plots；
- speaker classifier scores。

常见工具：

- Amped FIVE；
- iZotope RX；
- Audacity + forensic plugins；
- MATLAB / Python workflows。

---

## 41. 本组课件的综合理解

这一组课件看似内容很杂，但其实有一条清晰链条：

```text
Real-time audio processing
→ audio features and ML
→ AI generation and transformation
→ ethical risks
→ forensic analysis and legal reliability
```

它说明数字音频处理不只是技术问题，还包括：

- 系统性能；
- 数据表示；
- 模型评价；
- 伦理边界；
- 法律证据标准。

---

## 42. 考试/复习重点

### 42.1 Real-time audio

必须会：

- latency 定义；
- buffer size 对 latency 和 stability 的影响；
- round-trip latency 计算；
- online vs batch processing；
- oscillator/filter/envelope/effect；
- callback 和 buffer processing 的基本思想。

### 42.2 Audio ML

必须会：

- raw audio 为什么难直接用于 ML；
- feature extraction 的目的；
- ZCR、RMS、spectral centroid、roll-off、MFCC、chroma、spectral contrast；
- audio ML pipeline；
- accuracy、precision、recall、F1；
- confusion matrix。

### 42.3 MFCC

必须会：

- frame length / hop size 转 samples；
- time vs frequency resolution trade-off；
- MFCC 大致流程；
- Mel scale 为什么接近人耳感知。

### 42.4 AI ethics

必须会：

- TTS、voice cloning、voice conversion、audio deepfake 区别；
- 生成模型类型：GAN、VAE、Transformer、Diffusion；
- 正面应用与风险；
- consent、watermarking、detection、regulation。

### 42.5 Audio forensics

必须会：

- restoration vs forensics；
- chain of custody；
- forensic copying and hashing；
- metadata inspection；
- ENF、spectrogram、phase analysis；
- speaker recognition pipeline；
- reporting and reproducibility。

---

## 43. 常见问答

### Q1. 为什么小 buffer 会降低 latency？

因为系统每次处理的音频块更短，输入到输出之间等待的时间减少。但 CPU 必须更频繁地处理 buffer，所以更容易 glitch。

### Q2. 256 samples at 48 kHz 的 round-trip latency 是多少？

$$
\frac{256}{48000}\times1000\times2\approx10.7ms
$$

### Q3. 128 samples at 48 kHz 的 round-trip latency 是多少？

$$
\frac{128}{48000}\times1000\times2\approx5.3ms
$$

### Q4. 为什么 raw audio 通常需要 feature extraction？

因为 raw waveform 高维、冗余多、时间依赖复杂。特征提取可以把声音转换成更紧凑、有信息量、适合模型学习的数值表示。

### Q5. Precision 和 recall 有什么区别？

Precision 关注“预测为正的样本中有多少是真的”；recall 关注“真实正样本中有多少被找出来”。安全警报检测通常更重视 recall，因为漏报危险。

### Q6. MFCC 为什么常用于语音？

因为它基于 Mel scale，接近人耳对频率的感知，并能压缩频谱形状，捕捉 timbre 和 speech characteristics。

### Q7. Voice cloning 和 audio deepfake 有什么区别？

Voice cloning 是技术过程，指复制某人声音；audio deepfake 是合成结果，常指让某人听起来像说了没说过的话，通常带欺骗风险。

### Q8. AI 生成声音的核心伦理问题是什么？

包括 consent、身份冒充、欺诈、版权、误导公众、数据来源、监管和检测。

### Q9. Audio restoration 和 forensic audio 有什么区别？

Restoration 主要追求听起来更好；forensics 追求真实性、证据可靠性和可复现，处理必须保守。

### Q10. 为什么取证中要保留原始文件不变？

因为原始文件是证据基础。所有处理应在副本上进行，并用 hash 和记录证明证据没有被篡改。

---

## 44. 一页速记

> [!summary] Block 4 第 2 组 PPT 速记
> - Real-time audio 必须在下一个 buffer 到达前完成处理。
> - Latency 与 buffer size 成正比，与 sample rate 成反比。
> - Round-trip latency：$BufferSize/SampleRate\times1000\times2$。
> - 小 buffer 低延迟但 CPU 压力大；大 buffer 稳定但延迟高。
> - Audio ML 需要 feature extraction，因为 raw waveform 高维且复杂。
> - 常见特征：ZCR、RMS、spectral centroid、roll-off、MFCC、chroma。
> - ML pipeline：data/labelling → preprocessing → features → training → evaluation → deployment。
> - 评价分类模型：accuracy、precision、recall、F1、confusion matrix。
> - MFCC 依赖 framing、windowing、FFT、Mel filterbank、log、DCT。
> - AI audio generation 包括 TTS、music generation、voice cloning、deepfake。
> - 伦理核心：consent、misuse、fraud、watermarking、detection、regulation。
> - Audio forensics 重视 authenticity、chain of custody、minimal enhancement。
> - 取证分析包括 ENF、spectrogram、phase、metadata、hash、speaker recognition。

---

## 45. 和 Block 4 其他内容的连接

- 与 [[课程笔记/音频处理/Block 4/Block 4 - PPT 1：Audio Quality, Noise, and Digital Filtering II|Block 4 PPT 1]] 的连接：PPT 1 讲质量评价和滤波，PPT 2 进一步讲实时系统、ML、伦理和取证。
- 与 Block 3 的连接：PCA/ICA、filtering、source separation 都在这里变成应用系统中的组成部分。
- 与课程实验/作业的连接：如果做音频分类、源分离、降噪或 deepfake 分析，需要明确数据、特征、模型、评价指标和伦理边界。

- 🥤 (pomodoro::BREAK) (duration:: 5m) (begin:: 2026-06-17 15:50) - (end:: 2026-06-17 15:55)