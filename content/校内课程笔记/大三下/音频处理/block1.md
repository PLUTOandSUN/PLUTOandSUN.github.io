---
title: EBU5408 Block 1 - Introduction
aliases:
  - block1
  - Block 1 Introduction
  - Digital Audio Fundamentals Introduction
tags:
  - course/音频处理
  - EBU5408
  - digital-audio
  - block1
source:
  - "[[课程笔记/音频处理/附件/Block 1 - Sound waves and elements of acoustics/1. Introduction.pdf]]"
  - "[[课程笔记/音频处理/附件/Block 1 - Sound waves and elements of acoustics/2. Sound Waves.pdf]]"
  - "[[课程笔记/音频处理/附件/Block 1 - Sound waves and elements of acoustics/3. Sound Perception.pdf]]"
  - "[[课程笔记/音频处理/附件/Block 1 - Sound waves and elements of acoustics/4. Digitisation.pdf]]"
created: 2026-06-15
---

# Block 1 - PPT 1：Introduction

> [!info] 课件来源
> 原始课件：[[课程笔记/音频处理/附件/Block 1 - Sound waves and elements of acoustics/1. Introduction.pdf]]  
> 相关课程总览：[[课程笔记/音频处理/附件/2425_EBU5408_A.pdf]]

## 0. 这份 PPT 在课程中的作用

这份 PPT 是 EBU5408 **Digital Audio Fundamentals** 的课程导入。它本身不是在推导声学公式，而是在回答几个基础问题：

1. 这门课研究什么？
2. 课程结束后应该掌握什么能力？
3. 数字音频为什么重要，它从哪里发展而来？
4. 数字音频有哪些典型应用场景？
5. 这门课怎么上、怎么考、需要准备什么工具？

可以把本 PPT 理解成整门课的“地图”。后续 Block 1 的 Sound Waves、Sound Perception、Digitisation 会在这张地图上深入展开。

> [!summary] 核心主线
> **现实世界声波** → 麦克风采集 → **模拟电信号** → ADC 数字化 → **数字音频数据** → 存储 / 传输 / 编辑 / 压缩 / 分析 → DAC 还原 → 扬声器播放 → 人耳感知。

---

## 1. Agenda：本讲结构

PPT 的议程分成四部分：

- **What is this module about?** 这门课研究数字声音的哪些方面。
- **How to study for this module?** 如何通过 lecture、tutorial、lab 学好这门课。
- **Assessment** 评分方式，包括 coursework 和 final exam。
- **Audio tools** Block 1 和 Block 2 需要用到的音频工具，例如 Audacity 和 Matlab。

---

## 2. 这门课研究什么？

课件给出的定义是：本课程关注 **digital sound 的 creation、representation、modification 和 evaluation**。

### 2.1 Creation：声音如何被创造或采集

Creation 可以理解为“声音从哪里来”。主要有两类：

- **录音采集**：真实世界中的声音被麦克风转换成电信号，再通过 ADC 变成数字音频。
- **合成生成**：计算机或电子乐器直接生成声音，例如 synthesiser、virtual instrument、text-to-speech。

例子：

- 用麦克风录一段人声。
- 在 DAW 中用 MIDI 键盘触发钢琴音色。
- 用 AI TTS 系统把文字转换成语音。

### 2.2 Representation：声音如何被表示

数字音频不能直接保存“空气振动”，它需要被转换成数据。常见表示包括：

- **Waveform**：随时间变化的振幅序列。
- **PCM samples**：等时间间隔采样得到的一串数字。
- **Audio file formats**：例如 WAV、MP3、AAC、FLAC。
- **Frequency-domain representation**：例如频谱、声谱图 spectrogram。

后续 Digitisation 会重点讲：

- sampling rate 采样率；
- bit depth 位深；
- quantisation 量化；
- aliasing 混叠；
- audio format 文件格式。

### 2.3 Modification：声音如何被修改

Modification 指数字音频处理。典型操作包括：

- 剪辑、拼接、淡入淡出；
- 音量调整、均衡 EQ、压缩 compression、混响 reverb；
- 降噪、语音增强、自动调音 auto-tune；
- 编码压缩，例如 MP3；
- 分离音源、识别说话人、语音识别。

本质上，这些操作都是对数字信号进行计算处理。

### 2.4 Evaluation：如何评价声音

声音处理之后需要判断“好不好”。评价可以分为：

- **客观评价**：信噪比 SNR、失真、频谱差异、压缩率、延迟等。
- **主观评价**：人听起来是否自然、清晰、刺耳、失真、疲劳。
- **任务评价**：语音识别准确率、说话人识别准确率、通信是否可懂等。

> [!note] 重要理解
> 数字音频不是只看“波形长什么样”，还要考虑人的听觉系统。两个波形在数学上不同，不一定听起来差很多；两个波形看起来相似，也可能在关键频段上听感差异明显。

---

## 3. 本课程覆盖的主要主题

课件列出的主题包括：

| 主题 | 中文解释 | 为什么重要 |
|---|---|---|
| Basics of sound and acoustics | 声音与声学基础 | 理解声音是压力波，掌握强度、频率、音高等概念 |
| Sound perception | 声音感知 | 人耳如何感知响度、音高、音色，决定很多音频处理策略 |
| Digital representations and audio formats | 数字表示与音频格式 | 理解 WAV、MP3、采样率、位深等基础 |
| MIDI and music | MIDI 与音乐 | 区分“控制信息”和“音频信号” |
| Speech | 语音 | 语音信号有特殊结构，可用于识别、合成和增强 |
| Sound compression | 声音压缩 | MP3 等格式如何减少数据量，同时尽量保持听感 |
| Evaluation of sound | 声音评价 | 判断处理结果是否有效 |
| Audio processing applications | 音频处理应用 | 从降噪、增强、识别到医学和 VR |
| Ethical issues | 伦理问题 | 深度伪造、隐私、语音认证安全、音频取证可靠性 |

---

## 4. Learning Objectives：学习目标解释

### 4.1 理解声学与声音基础

课程要求理解 sound 和 acoustics 的 fundamentals，特别是：

- **Intensity 强度**：物理上与单位面积通过的声功率有关；听觉上常与 loudness 响度相关，但二者不是线性关系。
- **Frequency 频率**：每秒周期数，单位 Hz。频率越高，通常听起来音越高。
- **Pitch 音高**：人耳对频率的主观感知。Pitch 不完全等于 frequency，例如复杂音的基频、泛音结构也会影响音高感。

> [!example] 频率与音高
> 440 Hz 的纯音通常被听作 A4。若一个复杂音含有 440 Hz 的基频以及 880 Hz、1320 Hz 等泛音，人耳仍可能感知其 pitch 为 440 Hz。

### 4.2 理解数字音频的创建、表示、修改和评价

这要求你能从完整信号链路理解数字音频：

```text
声波 → 麦克风 → 模拟信号 → ADC → 数字样本 → 文件/流/处理 → DAC → 扬声器 → 听觉感知
```

要能解释每一步可能产生的问题：

- 麦克风噪声、环境噪声；
- ADC 采样率不足导致 aliasing；
- 量化导致 quantisation noise；
- 压缩导致 artifacts；
- 播放设备和房间声学影响听感。

### 4.3 创建、编辑、录制并辨别声音

这部分强调实践能力。不是只背概念，还要能用工具处理音频：

- 用 Audacity 录音、剪辑、查看波形和 spectrogram；
- 用 Matlab 读取音频、绘制波形、做频谱分析；
- 能听出常见问题，例如 clipping、background noise、distortion、compression artifacts。

### 4.4 分析频率并听出隐藏失真

“隐藏失真”是音频课程很重要的能力，因为某些问题在时域波形中不明显，但在频域或听感中很明显。

常见隐藏问题：

- **Clipping**：音量超过范围后波形顶部被削平，听起来刺耳。
- **Aliasing**：采样不充分导致高频折叠到低频，产生不真实频率成分。
- **Quantisation noise**：位深不足导致细节粗糙。
- **Compression artifacts**：MP3 等有损压缩造成水声、金属感、瞬态模糊。
- **Background noise**：背景噪声掩盖语音细节。

---

## 5. 数字声音简史

### 5.1 从想法到技术

| 时间 | 事件 | 意义 |
|---|---|---|
| 1842 | Ada Lovelace 提出计算机器可用于音乐创作的想法 | 早期意识到计算机不只是算术工具，也可处理音乐结构 |
| 1877 | Thomas Edison 发明 phonograph 留声机 | 首个能录制和播放声音的设备，仍是模拟机械方式 |
| 1920s-1930s | 电录音与扩音技术发展 | 改善录音质量，让声音记录更可靠 |
| 1937 | Alec Reeves 发明 PCM | PCM 成为数字音频的基础表示方式 |
| 1957 | Max Mathews 在 Bell Labs 用计算机录制 / 生成数字声音 | 标志计算机声音实验的开始 |
| 1960s-1970s | ADC 和 DAC 技术进步 | 模拟世界与数字世界之间的转换变得实用 |

### 5.2 数字音频革命

| 时间 | 事件 | 意义 |
|---|---|---|
| 1971 | Denon 发行商业数字录音 | 数字录音开始进入商业领域 |
| 1979 | Sony Walkman 推出 | 个人便携音频流行，但仍主要是模拟磁带 |
| 1982 | CD 由 Sony 和 Philips 推出 | 第一种大规模普及的数字音频格式，使用 16-bit PCM 和 44.1 kHz 采样率 |
| 1983 | MIDI 推出 | 乐器、合成器和计算机之间可以交换标准化控制信息 |
| 1991 | MP3 开发 | 有损压缩让音频文件显著变小，便于存储和传输 |
| 1999 | 便携 MP3 播放器出现；Napster 流行 | 数字音乐分发兴起，同时带来版权问题 |
| 2001 | iPod 发布 | 改变个人数字音乐消费方式 |
| 2003 | iTunes Store 开放 | 合法数字音乐购买平台成熟 |
| 2008 | Spotify 推出 | 音乐产业从下载转向流媒体订阅模式 |
| 2010s 至今 | FLAC、ALAC、lossless、spatial audio、AI audio | 数字音频走向高保真、沉浸式和智能化 |

> [!tip] 如何记忆这段历史
> 可以按“瓶颈被解决”的逻辑记：
> 1. 先解决 **能否记录声音**；
> 2. 再解决 **能否电气化与放大**；
> 3. 再解决 **能否数字表示**；
> 4. 再解决 **能否便携和压缩**；
> 5. 最后进入 **流媒体、空间音频和 AI 音频**。

### 5.3 音频记录媒介演变

PPT 中还有一页音频记录历史时间线，重点是记录媒介的变化：

| 阶段 | 典型媒介 / 技术 | 特点 |
|---|---|---|
| 1870s-1880s | 早期录音与播放设备 | 声音记录开始出现 |
| 1880s-1890s | Cylinder recordings 圆筒录音 | 开始商业化 |
| 1900s-1910s | Disc records 唱片 | 逐渐取代圆筒，成为更流行的格式 |
| 1920s-1930s | Magnetic recording 磁录音 | 德国等地发展，录音质量和可编辑性提升 |
| 1940s-1950s | Wire / tape recording 钢丝与磁带 | 磁带因灵活性更高而流行 |
| 1960s-1970s | Cassette 卡带 | 开放式卷带的便携替代品，广泛用于家庭和个人录音 |
| 1980s-1990s | CD、DAT、cassette | CD 引入数字音频，模拟卡带仍常见 |
| 2000s 至今 | Digital audio files | 文件化、网络化、流媒体化 |

---

## 6. 数字音频的应用领域

PPT 强调数字音频被用于娱乐、通信、医学、科学等大量场景。理解这些应用时，可以问三个问题：

1. 输入是什么声音？
2. 系统要对声音做什么处理？
3. 输出结果服务于什么任务？

### 6.1 Music Production & Recording：音乐制作与录音

主要关键词：**DAW、MIDI、virtual instruments、auto-tuning、effects、streaming formats**。

#### 6.1.1 DAW 是什么？

DAW 是 **Digital Audio Workstation**，即数字音频工作站。它是录音、编辑、混音和母带处理的核心软件环境。

常见 DAW 功能：

- 多轨录音；
- 波形编辑；
- 音量、声像、EQ、压缩、混响；
- 插件效果器；
- MIDI 编曲；
- 导出 WAV、MP3、AAC 等格式。

#### 6.1.2 DAW 的基本信号流

课件中的 DAW 图可以解释为：

```text
麦克风/乐器
  ↓ 模拟音频信号
Preamp 前置放大
  ↓
ADC 模数转换
  ↓ 数字音频信号
Audio Interface / Controller
  ↓ USB/FireWire 等数据连接
Driver + RAM Buffer
  ↓
CPU / Software 做 DSP 处理
  ↓
Hard Drive 存储 + Display 显示波形
  ↓
DAC 数模转换
  ↓ 模拟音频信号
耳机 / 音箱监听
```

每个环节的作用：

| 环节 | 作用 | 常见问题 |
|---|---|---|
| Microphone | 把空气压力变化转换成电信号 | 噪声、指向性、房间反射 |
| Preamp | 把很弱的麦克风信号放大到可用电平 | 增益过高会噪声或 clipping |
| ADC | 把模拟电压转换成数字样本 | 采样率、位深、量化误差 |
| Buffer | 临时存放音频数据，保证连续处理 | buffer 太大延迟高，太小可能爆音 |
| CPU / DSP | 执行 EQ、reverb、compression 等处理 | 算力不足会卡顿 |
| Hard Drive | 保存音频文件和工程 | 读写速度影响大型工程 |
| DAC | 把数字样本转换回模拟电信号 | 转换质量影响播放效果 |
| Monitor | 耳机或音箱播放 | 设备频响影响判断 |

#### 6.1.3 MIDI 与 virtual instruments

MIDI 不是声音本身，而是**控制信息**。

例如按下 MIDI 键盘的一个键，它记录的不是钢琴声音，而是类似这样的信息：

- 哪个音符；
- 什么时候按下；
- 按下力度 velocity；
- 持续多久；
- 是否使用踏板或控制旋钮。

Virtual instrument 再根据这些 MIDI 信息生成实际声音。

> [!important] MIDI vs Audio
> - **Audio**：真实声波被采样后的数字波形。
> - **MIDI**：告诉乐器或软件“演奏什么”的控制指令。

#### 6.1.4 Auto-tuning 与 effects processing

- **Auto-tune**：检测人声 pitch，并把它移动到目标音高附近。
- **Effects processing**：改变声音特性，例如 EQ 改频谱，reverb 模拟空间，compression 控制动态范围。

这些都是数字音频处理的直接应用。

---

### 6.2 Film, TV, and Video Game Audio：影视与游戏音频

PPT 提到的内容包括：

- soundtracks 背景音乐；
- dialogue 对白；
- Foley 拟音；
- surround sound 与 3D audio；
- game audio engines，例如 FMOD；
- ADR 自动对白替换。

#### 6.2.1 Foley 是什么？

Foley 是为影视画面重新制作或补充声音效果。例如：

- 脚步声；
- 衣服摩擦声；
- 开门声；
- 物体碰撞声。

这些声音未必来自拍摄现场，而是后期在录音棚中根据画面同步录制。

#### 6.2.2 游戏音频为什么特殊？

电影音频是线性时间轴；游戏音频是交互式的。

游戏中声音可能取决于：

- 玩家位置；
- 角色动作；
- 环境材质；
- 敌人距离；
- 剧情状态。

所以游戏音频引擎需要实时决定播放什么声音、从哪个方向来、音量多大、混响多少。

#### 6.2.3 Surround / Spatial Audio

Spatial audio 的目标是让听者感觉声音来自三维空间中的某个位置。

常见技术思路：

- 多声道扬声器系统，例如 5.1、7.1、Dolby Atmos；
- 双耳 binaural 渲染，用耳机模拟方向感；
- HRTF，即头相关传输函数，模拟头部、耳廓对声音方向的影响；
- VR / AR 中结合头部追踪，让声源方向随头部转动而稳定。

---

### 6.3 Telecommunication & Voice Processing：通信与语音处理

PPT 中的关键词包括：

- VoIP；
- noise cancellation；
- speech enhancement；
- text-to-speech；
- speech recognition；
- teleconferencing and podcasting。

#### 6.3.1 VoIP

VoIP 是 **Voice over IP**，即通过互联网协议传输语音。Zoom、Skype、WhatsApp 语音通话都属于这一类。

VoIP 系统需要处理：

- 音频压缩，减少网络带宽；
- packet loss 丢包；
- latency 延迟；
- jitter 网络抖动；
- echo cancellation 回声消除；
- noise suppression 降噪。

#### 6.3.2 Speech enhancement

课件中的 speech enhancement 图可以理解为：

```text
原始语音 → 通道 / 环境加入噪声 → 带噪语音 → 增强算法 → 更清晰的语音
```

目标不是让声音“完全还原”，而是在可接受失真下提高：

- intelligibility 可懂度；
- clarity 清晰度；
- SNR 信噪比；
- listening comfort 听感舒适度。

#### 6.3.3 ASR、NLP 与 TTS

课件用图表示：

```text
语音 → Automatic Speech Recognition → 文本 → Natural Language Processing → Text to Speech → 语音
```

三个模块分别是：

- **ASR**：把语音转文字。
- **NLP**：理解、处理、生成语言内容。
- **TTS**：把文字合成为语音。

这条链路在语音助手、字幕生成、客服系统、无障碍辅助中非常常见。

---

### 6.4 Broadcasting & Streaming Media：广播与流媒体

PPT 提到：

- FM 与 digital radio；
- live streaming；
- podcasting；
- internet radio。

这些应用的核心是：**在带宽和实时性限制下传输可接受质量的音频**。

关键权衡：

| 目标 | 可能的代价 |
|---|---|
| 更高音质 | 更高 bitrate，更大文件，更高带宽 |
| 更低延迟 | buffer 更小，更容易卡顿或丢包 |
| 更强压缩 | 可能出现压缩 artifacts |
| 更稳定传输 | 可能增加缓存和延迟 |

常见格式：MP3、AAC、Opus、FLAC 等。流媒体通常会根据网络情况动态调整码率。

---

### 6.5 Hearing Aids & Medical Applications：助听器与医学应用

PPT 提到：

- digital hearing aids；
- cochlear implants；
- medical imaging and ultrasound；
- speech therapy and assistive technology。

#### 6.5.1 Digital hearing aids

数字助听器使用 DSP 对声音进行个性化处理：

- 放大特定频段；
- 抑制背景噪声；
- 降低反馈啸叫；
- 增强语音；
- 根据环境自动切换模式。

它不是简单“把所有声音变大”，而是根据使用者听力损失曲线进行频率相关处理。

#### 6.5.2 Cochlear implant

人工耳蜗把声音转成电刺激信号，直接刺激听觉神经相关结构。

基本链路：

```text
外部麦克风 → 声音处理器 → 发射器 → 植入接收器 → 电极阵列 → 听觉神经
```

它体现了音频处理、医学工程和神经感知之间的联系。

---

### 6.6 Forensics & Law Enforcement：音频取证与执法

PPT 提到：

- audio forensics and enhancement；
- voice identification and biometric security；
- lie detection and speech analysis；
- surveillance and wiretapping。

#### 6.6.1 Audio forensics

音频取证可能包括：

- 降噪，让语音更清楚；
- 分析录音是否被剪辑或篡改；
- 判断录音环境；
- 提取说话人特征；
- 增强被背景声掩盖的信息。

#### 6.6.2 Speaker recognition

课件中的 speaker recognition 图可以解释为两阶段：

1. **Enrolment 注册阶段**：采集某人的声音，提取 voice signature。
2. **Recognition 识别阶段**：对新的声音提取 voice characteristics，与注册特征和 claimed identity 比较，最后 accept / reject。

需要注意：说话人识别不是绝对可靠，可能受噪声、录音设备、情绪、疾病、伪造语音、重放攻击影响。

> [!warning] 伦理与安全
> 语音识别和声纹认证涉及隐私、安全和公平性问题。深度伪造语音会让“听起来像某人”不再等于“确实是某人”。

---

### 6.7 Scientific Research & Environmental Monitoring：科学研究与环境监测

PPT 提到：

- seismology and acoustic analysis；
- animal communication and bioacoustics；
- astronomy and radio waves；
- underwater sound and SONAR。

这些例子说明：音频处理的核心思想不限于“人能听到的声音”，而是广义的 **time-varying signals**。

#### 6.7.1 Seismology and acoustic analysis

地震信号也是随时间变化的波。可以用类似音频分析的方法研究：

- 频率成分；
- 能量变化；
- 噪声模型；
- 事件检测。

#### 6.7.2 Bioacoustics

生物声学研究动物声音，例如鲸歌、鸟鸣、昆虫叫声。常见任务：

- 物种识别；
- 行为分析；
- 迁徙监测；
- 生态环境变化检测。

#### 6.7.3 SONAR

SONAR 利用声波在水下传播，用于测距、定位、海洋研究和潜艇探测。

---

### 6.8 VR & AR Audio：虚拟现实与增强现实音频

PPT 提到：

- spatial audio；
- binaural sound；
- immersive experiences；
- augmented audio reality。

VR / AR 中，音频不只是背景声，而是空间感和沉浸感的一部分。

重要能力：

- 判断声源方向；
- 判断距离；
- 感知房间大小和材质；
- 头部转动时保持声源位置稳定；
- 把虚拟声音和真实环境融合。

---

## 7. 如何学习这门课

### 7.1 课程组织

课程由 lectures、tutorials 和 labs 混合组成。课件中说明：

- **Blocks 1 & 2**：Marie-Luce Bourguet；
- **Blocks 3 & 4**：Pireh Pirzada。

学习方式不是只听课，还要结合工具实践。

### 7.2 推荐书

推荐教材：

- Richard G. Lyons, *Understanding Digital Signal Processing*, 3rd edition, Pearson, 2010.

这本书偏数字信号处理基础，适合补充理解 frequency analysis、filtering、sampling 等内容。

### 7.3 学习建议

> [!tip] 建议的学习流程
> 1. 课前浏览 PPT，先知道术语。  
> 2. 课上重点听概念之间的关系，而不是只抄定义。  
> 3. 课后用 Audacity 或 Matlab 复现实验：看 waveform、spectrogram、FFT。  
> 4. 建立词汇表：ADC、DAC、PCM、MIDI、DAW、DSP、codec 等。  
> 5. 对每个应用场景都练习回答：输入是什么、处理什么、输出是什么、评价指标是什么。

---

## 8. Labs and Coursework

课程有两个 lab：

| Lab | 主题 | 重点能力 |
|---|---|---|
| Lab 1 | Speech signals and Spectrograms | 观察语音波形和声谱图，理解语音频率结构 |
| Lab 2 | Audio Signal Processing Application | 应用音频处理算法解决实际任务 |

课件提醒：

- lab sheets 会提前给出，需要提前准备；
- lab deliverables 必须在 lab session 前提交；
- lab 中会进行 assessment，参与是 mandatory；
- 最终 coursework report 在第二次 lab 后不久提交；
- 具体时间和地点看 QM+。

---

## 9. Assessment：评分方式

### 9.1 总评构成

| 部分 | 占比 |
|---|---:|
| Continuous Assessment / Coursework | 25% |
| Final Exam | 75% |

总评公式：

$$
\text{Final Mark} = 0.25 \times \text{Coursework Mark} + 0.75 \times \text{Exam Mark}
$$

通过要求：

- overall total mark 至少 **40%**；
- coursework total mark 至少 **30%**。

### 9.2 Final Exam

课件说明 final exam：

- written；
- closed book；
- 2 hours；
- 4 questions；
- each question carries 25 marks；
- all topics are covered。

这意味着复习不能只押某一章，需要覆盖全部 blocks。

### 9.3 Coursework 内部构成

| Coursework 部分 | 占 coursework 比例 |
|---|---:|
| Lab 1 deliverables + in-lab assessment | 25% |
| Lab 2 deliverables + in-lab assessment | 25% |
| Coursework report | 50% |

> [!important] 实用提醒
> Lab 前提交 deliverables 很关键，因为 lab 现场 assessment 会基于准备情况进行。不要等到 lab 当天才开始做。

---

## 10. Audio Tools：需要准备的软件

### 10.1 Audacity

官网：<https://www.audacityteam.org/>

Audacity 是免费开源音频编辑工具，适合：

- 录音；
- 剪辑；
- 查看 waveform；
- 查看 spectrogram；
- 做简单降噪、放大、淡入淡出；
- 导出不同音频格式。

在本课中，Audacity 适合用来直观理解声音：你可以看到一段语音在时间轴上的波形，也可以看到它的频谱随时间如何变化。

### 10.2 Matlab

QMUL Matlab 页面：<https://www.qmul.ac.uk/its/support/self-help/software/free-and-discounted-software/matlab/>

Matlab 更适合算法和分析，例如：

- 读取音频文件；
- 绘制 waveform；
- 计算 FFT；
- 绘制 spectrogram；
- 设计滤波器；
- 实现音频处理实验。

---

## 11. 本讲关键词表

| 英文术语 | 中文理解 |
|---|---|
| Digital audio | 用数字样本表示、存储、处理和传输的声音 |
| Acoustics | 声学，研究声音产生、传播和接收 |
| Waveform | 波形，振幅随时间变化的图像或数据 |
| PCM | Pulse Code Modulation，数字音频基础编码方式 |
| ADC | Analog-to-Digital Converter，把模拟信号转为数字信号 |
| DAC | Digital-to-Analog Converter，把数字信号转回模拟信号 |
| DAW | Digital Audio Workstation，数字音频工作站 |
| MIDI | 乐器和软件之间传递的控制信息，不是音频本身 |
| DSP | Digital Signal Processing，数字信号处理 |
| Codec | 编码 / 解码器，用于压缩和解压音频 |
| Spectrogram | 声谱图，显示频率随时间变化的能量分布 |
| VoIP | Voice over IP，互联网语音通信 |
| ASR | Automatic Speech Recognition，自动语音识别 |
| TTS | Text to Speech，文本转语音 |
| SNR | Signal-to-Noise Ratio，信噪比 |
| Spatial audio | 空间音频，模拟声音的方向和距离 |

---

## 12. 可以用于复习的自测问题

1. 本课程中 creation、representation、modification、evaluation 分别是什么意思？
2. 为什么 PCM 是数字音频的重要基础？
3. CD 的典型参数是什么？为什么 1982 年 CD 的出现很重要？
4. MIDI 和 audio 的本质区别是什么？
5. DAW 中 ADC、DAC、preamp、buffer 分别起什么作用？
6. Speech enhancement 的输入和输出是什么？
7. VoIP 系统为什么需要压缩、降噪和延迟控制？
8. 数字助听器为什么不是简单地把所有声音放大？
9. Speaker recognition 的 enrolment 和 recognition 阶段分别做什么？
10. Coursework 和 final exam 各占总评多少？通过要求是什么？

---

## 13. 一句话总结

这节课告诉我们：**数字音频是一条从物理声波到数字数据、再到处理、传输、播放和人耳感知的完整链路**。后续课程会围绕这条链路逐步深入：先理解声音本身，再理解人如何听声音，然后学习如何把声音数字化并进行实际处理。

---

# Block 1 - PPT 2：Sound Waves

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

# Block 1 - PPT 3：Sound Perception

> [!info] 课件来源
> 原始课件：[[课程笔记/音频处理/附件/Block 1 - Sound waves and elements of acoustics/3. Sound Perception.pdf]]  
> 本节接在 [[#Block 1 - PPT 2：Sound Waves]] 之后，从“声音作为物理波”转向“人耳和大脑如何感知声音”，并说明这些听觉规律如何被用于音频压缩。

## 0. 本节课的整体框架

本 PPT 的主题是 **Sound Perception**，也就是声音感知。它主要回答三个问题：

1. **Objective measures of sound**：怎样客观测量声音？例如 intensity、pressure、dB SPL。
2. **What is psychoacoustics?**：心理声学研究什么？为什么人耳听觉不是线性的？
3. **Application to audio compression**：为什么 MP3 等有损压缩可以丢掉一部分声音数据，但听起来仍然可以接受？

> [!summary] 本节核心
> 声音的物理强度和人感受到的响度不是线性对应关系。人耳对不同频率的敏感度不同，也会出现频率掩蔽和时间掩蔽。音频压缩正是利用这些听觉限制，把人耳不容易察觉的部分减少或丢弃。

---

## 1. Objective measures of sound：声音的客观测量

PPT 首先区分两个层面：

- **Objective measurements 客观测量**：可以用仪器测量的物理量，例如 sound intensity、sound pressure。
- **Subjective experience 主观体验**：人感受到的响度 loudness、刺耳程度、清晰度等。

两者相关，但不完全相同。比如两个声音的 SPL 都是 60 dB，人耳感受到的响度仍可能因为频率不同而不同。

---

## 2. Sound intensity 声强

### 2.1 定义

**Sound intensity** 是声波携带的功率除以传播面积，即单位面积上通过的声功率。

$$
I=\frac{P}{A}
$$

其中：

| 符号 | 含义 |
|---|---|
| $I$ | intensity，声强 |
| $P$ | power，功率 |
| $A$ | area，面积 |

单位是：

$$
\text{W/m}^2
$$

### 2.2 Power 功率

PPT 中说明：**power** 是单位时间内传递的能量，单位是 watt，记作 W。

在音频设备中，watt 常用于：

- 功率放大器输出能力；
- 扬声器能够承受的功率；
- 音响系统的功率规格。

### 2.3 声强的直观理解

如果声源向外辐射声能，离声源越远，同样的声能分布到更大的球面面积上，因此单位面积接收到的声强会减小。

在理想自由场中，距离加倍，面积变成 4 倍，声强大约变成原来的 1/4。这就是为什么离声源越远声音越弱。

---

## 3. Sound pressure 声压

### 3.1 Pressure 的定义

**Pressure 压强** 是力除以受力面积：

$$
p=\frac{F}{A}
$$

单位是：

$$
\text{N/m}^2 = \text{Pa}
$$

Pa 是 pascal，帕斯卡。

### 3.2 声压是什么？

对于声音，我们关心的是空气压力相对于平衡大气压的微小变化。

也就是说，声压不是大气压本身，而是声波造成的：

```text
高于平衡气压的部分 + 低于平衡气压的部分
```

PPT 中称为 **air pressure amplitude**，单位是 Pa。

### 3.3 Pressure、power、intensity 的单位与参考值

PPT 的表格表达了三种测量量：

| 测量对象 | 单位 | 常见 dB 参考值 |
|---|---|---|
| Sound Pressure | Pa | $20\times10^{-6}$ Pa |
| Sound Power | W | $10^{-12}$ W |
| Sound Intensity | W/m² | $10^{-12}$ W/m² |

> [!important] 注意
> dB 本身不是绝对单位，必须说明参考值。dB SPL 的参考声压是 $20\ \mu\text{Pa}=0.00002\text{ Pa}$，大约对应正常年轻人在 1 kHz 附近的听阈。

---

## 4. Measuring sound in decibels：用分贝测量声音

### 4.1 dB 不是绝对单位

PPT 强调：**decibel 不是绝对测量单位**。它表达的是某个量相对于参考量的比例。

所以说“60 dB”时，要知道它是什么 dB：

- dB SPL：相对于听阈声压；
- dBFS：数字音频中相对于满刻度 full scale；
- dBV：相对于 1 V；
- dBW：相对于 1 W。

本节讲的是 **dB SPL**。

### 4.2 dB SPL 公式

PPT 给出的关键公式：

$$
dB_{SPL}=20\log_{10}\left(\frac{E}{E_0}\right)
$$

其中：

| 符号 | 含义 |
|---|---|
| $E$ | measured sound pressure amplitude，测得的声压幅度 |
| $E_0$ | reference pressure，参考声压 |
| $E_0$ | $0.00002\text{ Pa}=20\ \mu\text{Pa}$ |

为什么是 20 而不是 10？因为声压是幅度量，而声功率/声强与声压平方成正比：

$$
I\propto p^2
$$

所以：

$$
10\log_{10}\left(\frac{p^2}{p_0^2}\right)=20\log_{10}\left(\frac{p}{p_0}\right)
$$

### 4.3 为什么用 log scale？

人耳能听到的声压范围非常大，从大约 $20\ \mu\text{Pa}$ 到会造成疼痛或损伤的巨大声压。用线性尺度会很不方便。

此外，人的响度感知也更接近对数关系。PPT 提到：

- 声音增加 **10 dB**，听起来大约是 **两倍响**；
- 对多数人来说，**3 dB** 左右是能感知到的较小响度变化。

> [!note] 物理变化 vs 听觉变化
> - 声强增加 10 倍，对应 +10 dB。
> - 声压幅度增加 10 倍，对应 +20 dB。
> - 声压幅度增加 2 倍，对应约 +6 dB。
> - 人主观觉得“约两倍响”通常约需 +10 dB。

---

## 5. Exercise：dB SPL 计算

PPT 给了两个练习。

### 5.1 痛阈 30 Pa 对应多少 dB SPL？

题目：

> What would be the amplitude in decibels of the audio threshold of pain, given as 30 Pa?

使用公式：

$$
dB_{SPL}=20\log_{10}\left(\frac{E}{E_0}\right)
$$

代入：

$$
E=30\text{ Pa},\quad E_0=0.00002\text{ Pa}
$$

$$
\frac{E}{E_0}=\frac{30}{0.00002}=1,500,000
$$

$$
dB_{SPL}=20\log_{10}(1,500,000)
$$

$$
\log_{10}(1,500,000)=\log_{10}(1.5\times10^6)\approx6.176
$$

$$
dB_{SPL}\approx20\times6.176=123.5\text{ dB SPL}
$$

所以答案约为：

$$
\boxed{123.5\text{ dB SPL}}
$$

### 5.2 60 dB 的正常对话对应多少 Pa？

题目：

> What would be the pressure amplitude of normal conversation, given as 60 dB?

从公式反推：

$$
dB_{SPL}=20\log_{10}\left(\frac{E}{E_0}\right)
$$

$$
\frac{E}{E_0}=10^{dB/20}
$$

$$
E=E_0\times10^{dB/20}
$$

代入：

$$
E=0.00002\times10^{60/20}
$$

$$
E=0.00002\times10^3=0.02\text{ Pa}
$$

所以答案是：

$$
\boxed{0.02\text{ Pa}}
$$

---

## 6. 常见声音的近似 dB SPL

PPT 给出了常见声音的近似声压级：

| 声音 | 近似 dB SPL |
|---|---:|
| Threshold of hearing 听阈 | 0 dB |
| Rustle of leaves 树叶沙沙声 | 10 dB |
| Very quiet room 很安静房间 | 20 dB |
| Average room 普通房间 | 40 dB |
| Conversation 正常谈话 | 60 dB |
| Busy street 繁忙街道 | 70 dB |
| Loud radio 很响的收音机 | 80 dB |
| Train through station 火车经过车站 | 90 dB |
| Riveter 铆钉机 | 100 dB |
| Threshold of discomfort 不适阈 | 120 dB |
| Threshold of pain 痛阈 | 140 dB |
| Damage to ear drum 鼓膜损伤 | 160 dB |

> [!warning] 安全提醒
> 长时间暴露在高 SPL 环境中会造成听力损伤。即使没有立即疼痛，持续高音量耳机也可能损害高频听力。

---

## 7. Psychoacoustics：心理声学

### 7.1 定义

**Psychoacoustics 心理声学** 研究声音引发的心理和生理反应，也就是：

```text
声音物理信号 → 耳朵接收 → 神经系统处理 → 大脑感知
```

它研究的对象包括：

- noise 噪声；
- speech 语音；
- music 音乐；
- loudness 响度；
- pitch 音高；
- timbre 音色；
- masking 掩蔽；
- localization 声源定位。

### 7.2 人耳听觉是非线性的

PPT 强调，心理声学实验表明人耳听觉在很多方面都是非线性的，包括：

- loudness perception 响度感知非线性；
- frequency resolution 频率分辨率非线性；
- 不同频率的听阈不同；
- 同一声音在不同背景下可能听得到或听不到。

> [!example] 非线性听觉
> 100 Hz 和 1000 Hz 都是 60 dB SPL，但人可能觉得 1000 Hz 更明显，因为人耳在 1-5 kHz 范围更敏感。

---

## 8. Threshold of hearing：听阈

### 8.1 定义

**Threshold of hearing** 是人刚刚能够听到某个声音所需的最低声压级。

PPT 中说明：人耳对大约 **1000 Hz - 5000 Hz** 的声音最敏感，这接近人类语音的重要频率范围。

### 8.2 听阈随频率变化

人耳不是对所有频率同样敏感：

- 低频需要更高 SPL 才能听到；
- 1-5 kHz 左右最容易听到；
- 很高频也需要更高 SPL，且年龄增长后高频听力下降明显。

这解释了 PPT 的问题：

> Which is louder: a 1,000 Hz sound at 60 dB or a 100 Hz sound at 60 dB?

如果两者都是 60 dB SPL，物理声压级相同，但通常 **1000 Hz 听起来更响/更明显**，因为人耳对 1000 Hz 比对 100 Hz 更敏感。

### 8.3 Equal-loudness curves 等响曲线

PPT 的图显示了“某频率的声音要多大 SPL，才会被感知为某个响度”。这类曲线通常称为 equal-loudness contours。

它告诉我们：

- 同样的 SPL 不等于同样的 loudness；
- 低频要达到同样响度通常需要更高 SPL；
- 人耳在中频范围最敏感。

### 8.4 听阈随年龄变化

PPT 还说明听阈会随年龄变化。常见趋势：

- 年龄越大，高频听阈越高；
- 也就是说老年人通常更难听到高频；
- 噪声暴露、耳机音量过高、疾病也会影响听阈。

---

## 9. Critical bands：临界频带

### 9.1 为什么需要临界频带？

PPT 说明：人耳区分频率的能力不是线性的。

在低频区域，人耳可以分辨相差几 Hz 的两个音；但在高频区域，两个音可能要相差超过 100 Hz，人耳才明显察觉差异。

这是因为内耳可以近似看作一组频率选择性滤波器，每个滤波器对应一个 **critical band 临界频带**。

### 9.2 临界频带的特点

PPT 关键点：

- 人耳听觉范围大约有 **24 个 critical bands**；
- 每个 band 对一段频率范围敏感，类似 bandpass filter；
- 低频 critical band 更窄；
- 高频 critical band 更宽。

因此，两个频率是否容易被分辨，不仅取决于它们相差多少 Hz，也取决于它们落在哪个频带。

### 9.3 同一 critical band 内的两个音

PPT 给了几个现象：

- 如果两个 tones 在同一 critical band 内，不容易被听成两个独立音；
- 相差约 4 Hz 时，耳朵听到一个带有低频起伏的 tone，即 beating 拍频；
- 相差约 70 Hz 时，听到快速 modulation 或 beating；
- 相差约 350 Hz 时，两个音可能落入不同 critical bands，人耳能区分它们。

> [!tip] 直观理解
> 临界频带就像耳朵里的“频率分辨窗口”。同一个窗口里的声音容易互相混在一起；不同窗口里的声音更容易分开听。

---

## 10. Frequency masking：频率掩蔽

### 10.1 定义

**Frequency masking** 指一个较响的声音让另一个较弱、频率相近或更高的声音变得听不见。

PPT 的定义可以整理为：

- 两个频率在接近同一时间到达；
- 它们落在同一个或相近 critical band；
- 其中一个明显更响；
- 较弱的声音被较响的声音遮盖。

术语：

| 术语 | 含义 |
|---|---|
| masking tone | 掩蔽音，较响的声音 |
| masked frequency | 被掩蔽频率，较弱且听不见的声音 |
| masking threshold | 掩蔽阈值，有掩蔽音存在时新的听阈 |

### 10.2 频率掩蔽如何改变听阈？

PPT 的问题：

> How does frequency masking affect the threshold of hearing?

答案：

频率掩蔽会在 masking tone 附近提高听阈。也就是说，原本安静环境中可以听到的弱声音，在强声音存在时必须变得更大，超过新的 masking threshold，才能被听见。

```text
安静环境听阈 → 加入强掩蔽音 → 附近频率听阈升高 → 弱声音被盖住
```

### 10.3 掩蔽的方向性

PPT 图中强调：

- loud sounds 会 mask similar or higher frequency 的声音；
- soft sounds 也可能 mask other soft sounds of similar frequency；
- 低频强声常常更容易向高频方向扩展掩蔽，这叫 upward spread of masking。

### 10.4 频率掩蔽与音频处理

频率掩蔽说明：如果某个弱频率成分本来就被强频率成分遮住，人耳听不到或很难听到它，那么压缩算法可以减少这个弱成分的精度，甚至丢弃它。

这就是 MP3、AAC 等 perceptual audio coding 的核心依据之一。

---

## 11. Temporal masking：时间掩蔽

### 11.1 定义

**Temporal masking** 指一个响亮声音停止后，耳朵需要一点时间恢复，因此紧接着出现的较弱声音可能听不见。

PPT 的定义：

> After a loud sound stops, there is a small delay before we can hear a softer tone.

### 11.2 影响时间掩蔽的因素

PPT 说明时间掩蔽持续时间取决于：

- masker 的持续时间；
- masker 的 amplitude；
- masker 的 frequency。

通常：

- 掩蔽音越响，后续掩蔽越明显；
- 掩蔽音越长，恢复时间可能越长；
- 不同频率范围的恢复特性不同。

### 11.3 频率掩蔽与时间掩蔽的关系

频率掩蔽主要发生在“同时存在”的频率成分之间；时间掩蔽关注“前后相邻”的声音之间。

| 掩蔽类型 | 发生条件 | 例子 |
|---|---|---|
| Frequency masking | 同一时间，频率接近，强声盖住弱声 | 大鼓声盖住附近频率的小声音 |
| Temporal masking | 强声停止后不久，弱声出现 | 爆破音之后的细小噪声听不见 |

---

## 12. Psychoacoustics 为什么对音频处理重要？

PPT 中有一组问题：

1. 为什么 critical bands 对音频处理重要？
2. frequency masking 什么时候发生？
3. temporal masking 什么时候发生？
4. psychoacoustics 如何让音频压缩更有效？

可以这样回答：

### 12.1 Critical bands 的作用

临界频带告诉我们人耳如何分辨频率。音频算法可以按临界频带分析声音，而不是简单按线性 Hz 平均处理。

例如：

- 在同一 critical band 内，人耳分辨率较低；
- 频率掩蔽通常发生在同一或相邻 critical band；
- 压缩算法可以在每个 band 内估计 masking threshold。

### 12.2 Frequency masking 的发生条件

频率掩蔽发生在：

- 两个声音几乎同时出现；
- 频率相近，通常处在同一或相邻 critical band；
- 一个声音明显更响；
- 较弱声音低于 masking threshold。

### 12.3 Temporal masking 的发生条件

时间掩蔽发生在：

- 一个强声音出现后；
- 紧接着出现较弱声音；
- 人耳还没有从强声音刺激中恢复；
- 弱声音暂时听不见或不明显。

### 12.4 心理声学如何帮助压缩

心理声学让压缩算法知道哪些信息“物理存在但听觉上不重要”。

因此算法可以：

- 丢弃低于听阈的频率成分；
- 减少被强声掩蔽的弱成分精度；
- 在人耳不敏感的频段使用更粗略的编码；
- 在关键频段保留更多信息。

---

## 13. Audio compression：音频压缩

### 13.1 为什么需要压缩？

PPT 举例：一个 3 分钟 stereo 未压缩歌曲约为 25 MB。未压缩音频文件较大，不利于：

- 网络传输；
- 流媒体播放；
- 移动设备存储；
- 大规模音乐库管理。

### 13.2 Lossless compression 无损压缩

**Lossless compression** 的目标是压缩后还能完全恢复原始数据。

PPT 说明无损音频压缩常用于：

- 编辑；
- 进一步压缩前的中间格式；
- 档案保存；
- master copies 母版。

常见无损音频格式：

- FLAC；
- ALAC；
- MPEG-4 ALS；
- WMA Lossless；
- Monkey's Audio；
- TTA；
- WavPack。

压缩率通常约为原始大小的 **50-60%**。

### 13.3 为什么无损压缩对音频不总是特别强？

PPT 提到，sound waveforms 复杂且不可预测，因此无损压缩效果有限。

原因是：

- 音频波形变化连续且复杂；
- 音乐、语音、噪声中包含大量细节；
- 完全保留每个 sample 会限制压缩空间。

### 13.4 Silence compression 静音压缩

PPT 提到一种直观压缩方法：silence compression。

流程：

1. 设置阈值 threshold；
2. 检测低于阈值的 samples；
3. 把这些 samples 当作 0；
4. 用 RLE，Run Length Encoding，记录连续 0 的长度。

问题：

- 真实录音中的 silence 很少绝对为 0；
- 低于阈值的背景声可能仍可被听见；
- 如果把它们当作 0，就不是严格无损。

---

## 14. Psychoacoustics and lossy audio compression：心理声学与有损压缩

### 14.1 有损压缩的核心思想

PPT 的关键句：

> Effective lossy compression identifies data that doesn't matter and throws it away.

也就是说，有损压缩不是随机丢数据，而是尽量丢掉不会明显影响听感的数据。

### 14.2 哪些声音“存在但听不到”？

PPT 总结了两种情况：

1. 声音低于 threshold of hearing，太小，听不到；
2. 声音被其他声音 masking，即被遮盖。

所以压缩算法可以重点分析：

- 当前频率成分是否低于听阈；
- 是否被同一 critical band 的更强频率掩蔽；
- 是否发生 temporal masking；
- 这段时间窗口里哪些成分必须保留。

### 14.3 Perceptual encoding 感知编码

**Perceptual encoding** 是基于心理声学的编码方式。

PPT 中说明：它的目标是确定人耳不太能感知或完全不能感知的声音成分，并减少这些成分的数据量。

典型步骤：

```text
音频分帧 → 频域分析 → 按 critical bands 建模 → 计算听阈和 masking threshold → 分配 bits → 量化/编码 → 输出压缩音频
```

其中最关键的是 bit allocation：

- 人耳敏感、未被掩蔽的成分：分配更多 bits，减少失真；
- 人耳不敏感或被掩蔽的成分：分配更少 bits，允许更多误差；
- 完全听不到的成分：可以丢弃。

### 14.4 Frequency masking and encoding

PPT 的最后图示表达了：

- 输入频谱中有很多频率成分；
- masking threshold 以下的成分属于 imperceptible frequency components；
- 编码后输出频谱保留重要成分，去掉或弱化不重要成分。

这就是 MP3 等有损压缩能大幅减小文件大小的原因。

---

## 15. 本节与考试的连接

本 PPT 内容非常容易出现在计算题和解释题中。

### 15.1 可能考 dB SPL 计算

你需要会：

$$
dB_{SPL}=20\log_{10}\left(\frac{p}{p_0}\right)
$$

以及反推：

$$
p=p_0\times10^{dB/20}
$$

其中：

$$
p_0=20\ \mu\text{Pa}=0.00002\text{ Pa}
$$

### 15.2 可能考 masking threshold

类似试卷中的题型可能会问：

- 某个 loud tone 会不会 mask 附近 quiet tone；
- critical band 宽度如何影响频率分辨；
- masking threshold 如何画在听阈图上。

答题时要写出：

```text
同一/相邻 critical band + 同时出现 + 一个声音明显更强 → 弱声音可能被 mask → 听阈升高
```

### 15.3 可能考音频压缩原理

如果问为什么 MP3 可以压缩音频，要答：

- 人耳听阈随频率变化；
- 有 frequency masking；
- 有 temporal masking；
- perceptual encoder 根据 critical bands 和 masking threshold 决定丢弃或粗量化哪些成分；
- 因此减少数据量，同时尽量保持主观听感。

---

## 16. 本节公式总结

| 公式 | 含义 |
|---|---|
| $I=\frac{P}{A}$ | 声强 = 声功率 / 面积 |
| $p=\frac{F}{A}$ | 压强 = 力 / 面积 |
| $dB_{SPL}=20\log_{10}\left(\frac{p}{p_0}\right)$ | 声压级公式 |
| $p_0=0.00002\text{ Pa}$ | dB SPL 参考声压 |
| $p=p_0\times10^{dB/20}$ | 由 dB SPL 反推声压 |
| $L_I=10\log_{10}\left(\frac{I}{I_0}\right)$ | 声强级形式，功率/强度量用 10 log |
| $I\propto p^2$ | 声强与声压平方成正比 |

---

## 17. 本节关键词表

| 英文术语 | 中文理解 |
|---|---|
| Sound intensity | 声强，单位面积通过的声功率 |
| Sound pressure | 声压，声波造成的空气压力变化 |
| Pascal | 帕斯卡，压强单位 Pa |
| Decibel | 分贝，相对参考值的对数尺度 |
| dB SPL | 声压级，相对于 $20\ \mu\text{Pa}$ 的 dB |
| Threshold of hearing | 听阈，刚能听到声音的最低水平 |
| Threshold of pain | 痛阈，声音强到引起疼痛的水平 |
| Psychoacoustics | 心理声学，研究人如何感知声音 |
| Equal-loudness curve | 等响曲线，描述不同频率达到同样响度所需 SPL |
| Critical band | 临界频带，人耳频率分辨的基本带宽 |
| Frequency masking | 频率掩蔽，强声盖住相近频率弱声 |
| Masking tone | 掩蔽音，造成遮盖的强声音 |
| Masked frequency | 被掩蔽频率，被遮盖的弱成分 |
| Masking threshold | 掩蔽阈值，有掩蔽音时升高后的听阈 |
| Temporal masking | 时间掩蔽，强声后短时间内弱声听不见 |
| Lossless compression | 无损压缩，可完全恢复原始数据 |
| Lossy compression | 有损压缩，丢弃部分听觉不重要数据 |
| Perceptual encoding | 感知编码，基于人耳模型的音频编码 |
| FLAC | 常见无损音频压缩格式 |
| MP3 | 常见有损音频压缩格式 |
| RLE | Run Length Encoding，游程编码 |

---

## 18. 复习自测题

1. Sound intensity 和 sound pressure 的定义分别是什么？单位是什么？
2. 为什么 dB 不是绝对单位？dB SPL 的参考值是多少？
3. 写出 dB SPL 的公式，并解释为什么使用 $20\log_{10}$。
4. 30 Pa 对应多少 dB SPL？60 dB SPL 对应多少 Pa？
5. 为什么 1000 Hz、60 dB 的声音通常比 100 Hz、60 dB 的声音听起来更明显？
6. 什么是 threshold of hearing？它如何随频率变化？
7. 年龄增长通常如何影响听阈？
8. 什么是 psychoacoustics？为什么说人耳听觉是非线性的？
9. Critical band 是什么？为什么低频 critical band 更窄、高频更宽很重要？
10. 两个频率相差很小的时候，人耳可能听到什么现象？
11. Frequency masking 发生的条件是什么？
12. Masking threshold 与安静环境下的 threshold of hearing 有什么区别？
13. Temporal masking 发生在什么时候？受哪些因素影响？
14. 为什么 lossless audio compression 通常只能压到原大小的 50-60% 左右？
15. Silence compression 为什么不一定严格无损？
16. Perceptual encoding 如何利用 threshold of hearing、critical bands 和 masking？
17. MP3 为什么可以比 WAV 小很多，但听起来仍然可接受？
18. 如果考试要求解释 psychoacoustics 对 audio compression 的作用，应该提到哪些关键词？

---

## 19. 一句话总结

本节课说明：**声音能否被听到，不只取决于它物理上是否存在，还取决于人耳对频率、响度和时间的非线性感知**。听阈、临界频带、频率掩蔽和时间掩蔽共同构成心理声学模型，而这些模型正是 MP3 等有损音频压缩能够有效工作的基础。

---

# Block 1 - PPT 4：Digitisation of Sound

> [!info] 课件来源
> 原始课件：[[课程笔记/音频处理/附件/Block 1 - Sound waves and elements of acoustics/4. Digitisation.pdf]]  
> 本节接在 [[#Block 1 - PPT 3：Sound Perception]] 之后，解释如何把连续的模拟声音转换成计算机可以保存、处理和传输的数字音频。

## 0. 本节课的整体框架

本 PPT 的主题是 **Digitisation of Sound**，也就是声音数字化。它把前面学过的声波、频率、强度、听觉感知，连接到实际的数字音频文件与 Matlab 操作。

主要内容：

1. **Sampling and aliasing**：时间维度如何采样，以及采样率不足会产生什么错误。
2. **Quantisation and dynamic range**：幅度维度如何量化，位深如何影响噪声和动态范围。
3. **Companding**：为什么降低位深时需要非线性量化，例如 A-law。
4. **Audio file formats**：WAV、AIFF、MP3、AAC、FLAC、OGG 等格式的区别。
5. **Matlab simulation**：如何在 Matlab 中模拟采样、量化，并读取 WAV 文件。

> [!summary] 本节核心
> 数字音频的两个核心步骤是：**sampling 在时间轴上取样**，以及 **quantisation 在振幅轴上取有限精度的数值**。采样率不足会产生 aliasing；位深不足会产生 quantisation noise。文件大小则由采样率、位深、声道数和时长共同决定。

---

## 1. 声音如何被计算机表示？

真实世界中的声音是连续变化的空气压力波，属于 **analog signal 模拟信号**。计算机不能直接存储连续无限精度的波形，所以必须把它变成一串数字。

完整链路可以写成：

```text
连续声波 → 麦克风转换为连续电压 → ADC → 采样 samples → 量化数字值 → 数字音频文件
```

其中 ADC 是 **Analog-to-Digital Converter**，模数转换器。

数字化主要包含两个维度：

| 步骤 | 处理维度 | 问题 |
|---|---|---|
| Sampling | 时间维度 | 多久测一次？采样率是多少？ |
| Quantisation | 振幅维度 | 每个样本用多少 bit 表示？可用多少幅度等级？ |

> [!important] 一句话区别
> **Sampling 决定横轴时间有多密；Quantisation 决定纵轴振幅有多细。**

---

## 2. Sampling：采样

### 2.1 采样的定义

PPT 给出的定义是：计算机在规则的时间间隔上测量波形的振幅，得到一系列数字，这个过程叫 **sampling**。

例如 CD 标准采样率：

$$
44100\text{ Hz}=44100\text{ samples/second}
$$

意思是：每秒对声音波形测量 44100 次。

### 2.2 Sampling rate 采样率

**Sampling rate** 是单位时间内采样的次数，单位是 Hz。

常见采样率：

| 场景 | 常见采样率 |
|---|---:|
| 电话语音 | 8 kHz |
| AM radio | 11.025 kHz |
| FM radio / 低质量数字音频 | 22.05 kHz |
| CD audio | 44.1 kHz |
| 专业音频 / 视频 | 48 kHz |
| DVD / 高解析音频 | 96 kHz / 192 kHz |

采样率越高，理论上可以记录越高的频率，但数据量也越大。

---

## 3. Nyquist theorem：奈奎斯特定理

### 3.1 核心结论

PPT 的表述是：

> Sample twice as often as the highest frequency you want to capture.

也就是说，如果想准确捕捉最高频率 $f_{max}$，采样率至少需要：

$$
f_s \ge 2f_{max}
$$

其中：

| 符号 | 含义 |
|---|---|
| $f_s$ | sampling rate，采样率 |
| $f_{max}$ | 要捕捉的最高频率 |

最低可用采样率称为 **Nyquist rate**。

### 3.2 Nyquist rate 和 Nyquist frequency

这两个概念很容易混淆：

| 概念 | 中文 | 给定什么？ | 表示什么？ |
|---|---|---|---|
| Nyquist rate | 奈奎斯特采样率 | 给定最高信号频率 $f_{max}$ | 至少需要的采样率 $2f_{max}$ |
| Nyquist frequency | 奈奎斯特频率 | 给定采样率 $f_s$ | 可无混叠采样的最高频率 $f_s/2$ |

公式：

$$
\text{Nyquist rate}=2f_{max}
$$

$$
\text{Nyquist frequency}=\frac{f_s}{2}
$$

### 3.3 例子：为什么 CD 是 44.1 kHz？

人耳大致能听到：

$$
20\text{ Hz} \sim 20\text{ kHz}
$$

如果希望覆盖 20 kHz，理论上采样率至少需要：

$$
2\times20\text{ kHz}=40\text{ kHz}
$$

CD 使用 44.1 kHz，因此 Nyquist frequency 是：

$$
\frac{44100}{2}=22050\text{ Hz}=22.05\text{ kHz}
$$

它略高于 20 kHz，给 anti-aliasing filter 留出过渡空间。

---

## 4. Aliasing：混叠

### 4.1 Aliasing 的定义

**Aliasing** 是采样率不足时产生的采样错误。高频成分不能被正确表示，反而会在数字信号中表现为错误的低频成分。

PPT 中说它像 folded 或 mirrored frequencies，也就是频率被“折叠”或“镜像”回来。

### 4.2 为什么会混叠？

如果每个周期的采样点太少，就无法判断原始波形到底是什么样。

特别是当：

$$
f > \frac{f_s}{2}
$$

高于 Nyquist frequency 的频率成分会折叠到低频区域，形成假频率。

> [!warning] 重要
> 混叠一旦发生，很难从采样后的数字信号中恢复原始高频，因为错误频率已经混进了有效频段。

### 4.3 Alias frequency 计算

PPT 给出公式：

$$
f_{alias}=|f-nf_s|
$$

选择整数 $n$，使结果落在：

$$
0 \le f_{alias} \le \frac{f_s}{2}
$$

例子：

$$
f=1000\text{ Hz},\quad f_s=1500\text{ Hz}
$$

Nyquist frequency：

$$
\frac{1500}{2}=750\text{ Hz}
$$

1000 Hz 高于 750 Hz，所以会混叠。取 $n=1$：

$$
f_{alias}=|1000-1500|=500\text{ Hz}
$$

所以 1000 Hz 会被错误地表现为 500 Hz。

### 4.4 与考试的典型连接

如果题目给出信号频率成分：500 Hz、1500 Hz、2500 Hz，采样率 2000 Hz：

Nyquist frequency：

$$
\frac{2000}{2}=1000\text{ Hz}
$$

因此：

- 500 Hz 不混叠；
- 1500 Hz 高于 1000 Hz，会混叠到 $|1500-2000|=500$ Hz；
- 2500 Hz 可取 $n=1$，混叠到 $|2500-2000|=500$ Hz。

这说明多个不同高频可能折叠到同一个低频位置，导致频谱严重失真。

### 4.5 Antialiasing filtering 抗混叠滤波

因为超过 Nyquist frequency 的成分无法正确恢复，所以采样前通常要使用 **anti-aliasing filter**。

作用：

```text
模拟输入信号 → 低通滤波，去除 Nyquist 以上频率 → ADC 采样
```

它本质上是一个 low-pass filter，把输入频率限制在 Nyquist frequency 以下。

---

## 5. Quantisation：量化

### 5.1 量化的定义

采样决定“什么时候测”，量化决定“测得的振幅用多精细的数字表示”。

PPT 定义：样本值的 resolution 取决于用于测量波形高度的 bits 数，常见为 8-bit 或 16-bit。

如果位深为 $N$ bit，则可表示的幅度等级数为：

$$
2^N
$$

例子：

| Bit depth | Quantisation levels |
|---:|---:|
| 3-bit | 8 levels |
| 8-bit | 256 levels |
| 16-bit | 65,536 levels |
| 24-bit | 16,777,216 levels |

### 5.2 Sampling vs Quantisation

| 概念 | 维度 | 影响 |
|---|---|---|
| Sampling | time dimension 时间维度 | 高频能否被捕捉；采样不足会 aliasing |
| Quantisation | amplitude dimension 振幅维度 | 振幅精度；位深不足会 quantisation noise |

### 5.3 课堂问题：8-bit 音频更可能是什么？

题目：

> A sound file encoded with 8 bits is likely to be: music / natural sound / speech / song

较合理答案是：**speech 语音**。

原因：

- 8-bit 只有 256 个幅度等级，动态范围较低；
- 音乐、歌曲、自然声通常需要更高保真度和更大动态范围；
- 语音通信对音质要求较低，更关注可懂度 intelligibility，因此 8-bit 更常见于电话语音等场景。

---

## 6. Quantisation error and quantisation noise：量化误差与量化噪声

### 6.1 量化误差是什么？

量化误差本质上是 rounding error。连续模拟值必须被四舍五入或映射到有限的量化等级上，因此原始值和量化值之间会有差异。

$$
\text{quantisation error}=\text{actual analog value}-\text{nearest quantised value}
$$

### 6.2 最大量化误差

若量化间隔为 $\Delta V$，最大误差通常不超过半个间隔：

$$
|e_{max}|=\frac{\Delta V}{2}
$$

如果信号范围是 $[-V_{max},V_{max}]$，位深为 $N$，则总范围为 $2V_{max}$，量化间隔约为：

$$
\Delta V=\frac{2V_{max}}{2^N}
$$

最大量化噪声幅度：

$$
\frac{\Delta V}{2}=\frac{V_{max}}{2^N}
$$

### 6.3 为什么位深不足会有噪声？

如果位深太低，很多不同的模拟振幅会被映射到同一个数字值上，波形会变成阶梯状。这个误差在人耳中表现为噪声或失真。

位深越高：

- 量化间隔越小；
- 量化误差越小；
- 可表示的弱声音越多；
- 动态范围越大。

---

## 7. SQNR 与动态范围

### 7.1 SQNR 定义

**SQNR** 是 Signal-to-Quantisation-Noise Ratio，信号与量化噪声比。

它衡量最大可表示信号与量化噪声之间的相对大小。

位深越高，SQNR 越大，音频系统越能捕捉安静声音而不被噪声淹没。

### 7.2 近似公式

PPT 给出：

$$
SQNR \approx 6.02N\text{ dB}
$$

更常见的正弦波满幅输入近似：

$$
SQNR \approx 6.02N+1.76\text{ dB}
$$

其中 $N$ 是 bit depth。

### 7.3 为什么每增加 1 bit 约增加 6 dB？

每增加 1 bit，量化等级翻倍，量化间隔减半，最大可区分的幅度范围相对于噪声提高约：

$$
20\log_{10}(2)\approx6.02\text{ dB}
$$

所以可以记住：

> [!important] 每多 1 bit，动态范围大约增加 6 dB。

### 7.4 Exercise：8-bit、16-bit、24-bit 动态范围

使用保守近似：

$$
DR\approx6.02N\text{ dB}
$$

| Bit depth | 近似动态范围 |
|---:|---:|
| 8-bit | $6.02\times8=48.16$ dB |
| 16-bit | $6.02\times16=96.32$ dB |
| 24-bit | $6.02\times24=144.48$ dB |

如果使用 $6.02N+1.76$：

| Bit depth | SQNR 近似 |
|---:|---:|
| 8-bit | 49.92 dB |
| 16-bit | 98.08 dB |
| 24-bit | 146.24 dB |

考试中如果问 approximate dynamic range，通常写 **8-bit ≈ 48 dB，16-bit ≈ 96 dB，24-bit ≈ 144 dB** 最稳。

---

## 8. Audio dithering 与 noise shaping

### 8.1 Dithering

当位深不足时，会产生量化噪声。**Dithering** 是在量化前向样本加入很小的随机噪声，让量化误差不再以明显失真的形式出现。

直觉：

```text
不加 dither：量化误差可能和信号相关 → 失真明显
加 dither：误差随机化 → 听起来更像平滑噪声
```

Dither 并不是消除噪声，而是把不自然的量化失真变成更容易接受的随机噪声。

### 8.2 Noise shaping

**Noise shaping** 会重新分布量化噪声，把更多噪声推到人耳不敏感的频率区域，尤其是较高频区域。

它利用了前面 Sound Perception 中的心理声学知识：人耳对不同频率的敏感度不同。

---

## 9. Audio quality vs data rate：音质与数据率

### 9.1 未压缩音频码率公式

未压缩 PCM 音频的数据率由三项决定：

$$
\text{bitrate}=f_s\times N\times C
$$

其中：

| 符号 | 含义 |
|---|---|
| $f_s$ | sampling rate，采样率 |
| $N$ | bit depth，每个样本 bits |
| $C$ | number of channels，声道数 |

若要转换为 bytes/second：

$$
\text{bytes/s}=\frac{f_s\times N\times C}{8}
$$

### 9.2 Stereo 会使码率翻倍

PPT 强调：**Stereo: double the bitrate.**

因为 stereo 有左右两个声道，同一时间需要存储两条 sample 序列。

### 9.3 常见音频应用的码率

PPT 表格中给出：

| Quality | Sampling rate | Bits/sample | Mono/Stereo | Uncompressed data rate |
|---|---:|---:|---|---:|
| Telephone | 8 kHz | 8 | Mono | 8 kB/s |
| AM radio | 11.025 kHz | 8 | Mono | 11.0 kB/s |
| FM radio | 22.05 kHz | 16 | Stereo | 88.2 kB/s |
| CD | 44.1 kHz | 16 | Stereo | 176.4 kB/s |
| DVD audio | 192 kHz max | 24 max | up to 6 channels | 1200 kB/s max |

注意这里表格的单位是 **kB/sec**，不是 kbps。CD 的 176.4 kB/s 等于：

$$
176.4\times8=1411.2\text{ kbps}
$$

---

## 10. Exercise：音乐信号码率与存储空间

题目：音乐信号带宽为 15 Hz 到 20 kHz，使用 Nyquist sampling rate，16 bits per sample。

### 10.1 采样率

最高频率约为：

$$
f_{max}=20\text{ kHz}
$$

Nyquist sampling rate：

$$
f_s=2f_{max}=40\text{ kHz}
$$

### 10.2 单声道 bit rate

若是 mono：

$$
\text{bitrate}=40000\times16=640000\text{ bits/s}=640\text{ kbps}
$$

### 10.3 立体声 bit rate

stereophonic music 有 2 channels：

$$
\text{bitrate}=40000\times16\times2=1,280,000\text{ bits/s}=1.28\text{ Mbps}
$$

### 10.4 10 分钟立体声音频需要多少 MB？

10 分钟：

$$
10\times60=600\text{ s}
$$

总 bits：

$$
1,280,000\times600=768,000,000\text{ bits}
$$

转 bytes：

$$
\frac{768,000,000}{8}=96,000,000\text{ bytes}
$$

按十进制 MB：

$$
96,000,000\text{ bytes}\approx96\text{ MB}
$$

所以答案约为：

$$
\boxed{96\text{ MB}}
$$

如果用 MiB：

$$
\frac{96,000,000}{1024^2}\approx91.6\text{ MiB}
$$

---

## 11. Exercise：CD 音频通过 ISDN 传输

题目：CD 标准音频，44.1 kHz，2 channels，16-bit samples，通过 64 kbps ISDN 传输。

### 11.1 一秒 CD 音频有多少 bits？

$$
44100\times2\times16=1,411,200\text{ bits}
$$

也就是：

$$
1.4112\text{ Mbps}
$$

### 11.2 通过 64 kbps 传输 1 秒音频需要多久？

$$
\text{time}=\frac{1,411,200}{64,000}=22.05\text{ s}
$$

所以传 1 秒未压缩 CD 音频需要约 **22.05 秒**。

### 11.3 实时传输需要多少压缩比？

实时传输要求 1 秒音频在 1 秒内传完，所以需要把码率从 1,411.2 kbps 降到 64 kbps：

$$
\text{compression ratio}=\frac{1,411.2}{64}\approx22.05:1
$$

也就是说，需要约 **22:1** 的压缩比，或者压缩到原始大小的约：

$$
\frac{64}{1411.2}\approx4.54\%
$$

---

## 12. Companding：压扩

### 12.1 Companding 是什么？

**Companding = compressing + expanding**。

它常用于降低 bit depth，但尽量减少低幅度信号的量化损失。

### 12.2 为什么线性降低位深有问题？

PPT 例子：从 16-bit 转 8-bit，如果简单除以 256 并向下取整：

```text
8-bit value = floor(16-bit value / 256)
```

那么 0 到 255 之间的所有小幅度值都会变成 0。

这对低幅度信号影响巨大，因为安静声音会直接消失。

### 12.3 Exercise：32767 和 255 转 8-bit

题目：考虑两个 16-bit 样本幅度：32767 和 255。将它们转换为 8-bit，并比较舍入误差。

使用除以 256 并向下取整：

$$
32767/256=127.996\rightarrow127
$$

$$
255/256=0.996\rightarrow0
$$

如果再换算回 16-bit 尺度：

$$
127\times256=32512
$$

第一个误差：

$$
32767-32512=255
$$

第二个误差：

$$
255-0=255
$$

绝对误差都是 255，但相对误差完全不同：

$$
\frac{255}{32767}\approx0.78\%
$$

$$
\frac{255}{255}=100\%
$$

所以低幅度样本被完全丢失，而高幅度样本只受到很小比例的影响。

> [!important] 结论
> 线性降低 bit depth 时，低幅度声音受到的相对损伤更大。这正是 companding 要解决的问题。

---

## 13. A-law 编码

### 13.1 A-law 是什么？

**A-law** 是一种非均匀量化方法，常用于语音通信中。

它的核心思想：

- 小幅度信号使用更细的量化间隔；
- 大幅度信号使用较粗的量化间隔；
- 这样在降低位深时，保留更多人耳更敏感的弱信号细节。

PPT 中说：human auditory system is believed to be a logarithmic process。也就是说，人耳对响度变化的感知近似对数型。

### 13.2 A-law 的效果

A-law 函数会把低幅度区域“拉开”，让低幅度信号获得更多表示精度。

直观表示：

```text
线性量化：每个幅度区间一样宽
A-law：低幅度区间更细，高幅度区间更宽
```

### 13.3 A-law 使用了人耳的什么性质？

PPT 问题：

> Which property of the human auditory system is used in A-law encoding?

答案：利用了人耳的**对数响度感知**和 **Weber's Law**。

Weber's Law 说：刚可察觉差异 JND 与原始刺激强度有关。原始刺激越大，需要更大的变化才容易被察觉。

因此：

- 小声音中的小误差更容易被听到；
- 大声音中的同等绝对误差不那么明显；
- A-law 把更多精度分配给小幅度信号。

---

## 14. Audio file formats：音频文件格式

PPT 从多个维度区分音频文件格式：

| 维度 | 问题 |
|---|---|
| Free or proprietary | 是开放格式还是公司控制格式？ |
| Platform-restricted or cross-platform | 是否只能在某些操作系统使用？ |
| Compressed or uncompressed | 是否压缩？有损还是无损？ |
| Container or simple audio file | 是否含 header、metadata、chunks？ |
| Copy-protected or unprotected | 是否包含 DRM？ |

---

## 15. Proprietary and platform-restricted formats

### 15.1 Proprietary file formats

**Proprietary formats** 由公司或组织控制，格式细节可能不完全公开，使用可能受专利或许可限制。

例子：

- Adobe Audition 的 SES；
- Audacity 的 AUP project；
- Pro Tools 的 PTF；
- MP3 曾有专利授权问题，但标准公开且跨平台广泛使用。

开放替代格式包括：

- OGG；
- FLAC。

### 15.2 Platform-restricted files

有些格式与平台关系更强：

| 格式 | 典型平台 |
|---|---|
| WMA | Windows |
| AIFF | Apple / Mac |
| AU | Unix / Linux |
| MP3 | Cross-platform |
| AAC | Cross-platform，手机、数字广播、游戏机等广泛使用 |

---

## 16. Container file formats：容器文件格式

### 16.1 Container 是什么？

Container file 不只是保存音频样本，还会用 header 和 chunks 包装音频数据，并记录 metadata。

Metadata 可以包括：

- song name；
- artist；
- genre；
- album；
- copyright；
- annotations；
- codec 信息；
- 数据块位置和大小。

### 16.2 常见容器

| 格式 | 容器基础 |
|---|---|
| AIFF | IFF |
| WAV | RIFF |
| MP3 | MPEG 标准的一部分 |
| WMA | Windows container format |
| OGG | open-source cross-platform container |

> [!note] 文件扩展名不一定告诉你全部信息
> 例如 WAV 通常是未压缩 PCM，但 WAV 也可以包含压缩数据。判断编码方式时要查看文件 header 或使用 `audioinfo` 等工具。

---

## 17. Compressed / uncompressed files

### 17.1 PCM

未压缩音频的基本格式是 **PCM，Pulse Code Modulation**。

PCM 本质上就是按采样率和位深保存样本值。

可存储未压缩音频的格式包括：

- WAV；
- AIFF；
- AU；
- RAW；
- PCM。

RAW 文件甚至没有 header，只包含原始音频数据，因此读取时必须额外知道采样率、位深、声道数等参数。

### 17.2 Lossy vs lossless compression

| 类型 | 特点 | 例子 |
|---|---|---|
| Lossy compression | 丢弃部分数据，不能完全恢复，但体积小 | MP3、AAC、Ogg Vorbis、A-law、μ-law |
| Lossless compression | 可完全恢复原始数据，压缩率较低 | FLAC、ALAC、MPEG-4 ALS、Monkey's Audio、TTA |

### 17.3 DRM / Copy protection

Copy protection 通常嵌入在 container formats 中。WMA 基于 ASF，支持 DRM。

DRM 用于限制复制、播放或分发权限。

---

## 18. Common audio file types 总结

| File type | Platform | Extension | Compression | Container | Proprietary / DRM |
|---|---|---|---|---|---|
| PCM | cross | `.pcm` | no | no | no DRM |
| RAW | cross | `.raw` | no | no | no DRM |
| WAV | cross | `.wav` | optional | yes, RIFF | usually open, no DRM |
| AIFF | Mac | `.aif`, `.aiff` | no | yes, IFF | no DRM |
| AIFF-C | Mac | `.aifc` | yes, various codecs | yes, IFF | no DRM |
| CAF | Mac | `.caf` | yes | yes | no DRM |
| AU | Unix/Linux | `.au`, `.snd` | optional μ-law | yes | no DRM |
| MP3 | cross | `.mp3` | MPEG lossy | yes | license historically, DRM optional |
| AAC | cross | `.m4a`, `.m4b`, `.mp4`, `.aac` 等 | AAC lossy | depends on container | license historically |
| WMA | Windows | `.wma` | WMA lossy | yes | proprietary, DRM optional |
| OGG Vorbis | cross | `.ogg`, `.oga` | Vorbis lossy | yes | open source |
| FLAC | cross | `.flac` | FLAC lossless | yes | open source |

---

## 19. Matlab：模拟采样

PPT 用 Matlab 生成正弦波，并用不同采样率采样。

核心步骤：

```matlab
signalFrequency = 90;      % signal frequency in Hz
numberOfCycles = 3;
SR1 = 200;                 % first sampling rate
SR2 = 1500;                % second sampling rate
signalPeriod = 1 / signalFrequency;
timeSpan = numberOfCycles * signalPeriod;

t1 = 0:1/SR1:timeSpan;
t2 = 0:1/SR2:timeSpan;

x1 = sin(2 * pi * signalFrequency * t1);
x2 = sin(2 * pi * signalFrequency * t2);

plot(t1, x1, 'bo-', t2, x2, 'rx-');
legend('SR=200', 'SR=1500');
```

解释：

- `SR1=200` 对 90 Hz 信号来说高于 Nyquist rate $2\times90=180$，刚刚足够；
- `SR2=1500` 采样更密，波形显示更平滑；
- 采样率越低，采样点越稀疏，越容易看错波形。

另一个例子中：

```matlab
x = sin(180*pi*t)
```

因为：

$$
180\pi=2\pi f
$$

所以：

$$
f=90\text{ Hz}
$$

如果采样率只有 100 Hz，Nyquist frequency 只有 50 Hz，无法正确采样 90 Hz，因此会发生 aliasing。

---

## 20. Matlab：模拟量化

PPT 中的 Matlab 量化实验步骤：

### 20.1 生成正弦波

```matlab
fs = 1000;
t = 0:1/fs:1;
f = 5;
A = 1;
x = A * sin(2 * pi * f * t);
```

这生成一个 5 Hz，幅度为 1，持续 1 秒的正弦波。

### 20.2 设置量化等级

```matlab
numLevels = 8;  % 3-bit quantisation
x_min = min(x);
x_max = max(x);
quantised_values = linspace(x_min, x_max, numLevels);
```

`numLevels=8` 表示 3-bit 量化，因为：

$$
2^3=8
$$

### 20.3 找最近的量化等级

```matlab
[~, idx] = min(abs(x - quantised_values'), [], 1);
x_quantised = quantised_values(idx);
```

这一步把每个原始样本映射到最近的量化值。

### 20.4 画原始波形、量化波形和误差

```matlab
stairs(t, x_quantised, 'r')
plot(t, x - x_quantised, 'k')
```

量化后的波形呈阶梯状；误差图显示原始波形和量化波形之间的差。

---

## 21. Matlab：读取 WAV 文件

### 21.1 查看文件信息

```matlab
info = audioinfo("music.wav");
```

可能输出：

```text
CompressionMethod: 'Uncompressed'
NumChannels: 1
SampleRate: 44100
TotalSamples: 109568
Duration: 2.4845
BitsPerSample: 16
```

这些信息对应文件格式中的关键参数：

- 是否压缩；
- 声道数；
- 采样率；
- 样本总数；
- 时长；
- 位深。

### 21.2 读取、播放和绘制音频

```matlab
[y, Fs] = audioread('music.wav');
sound(y, Fs);

t = 0:seconds(1/Fs):seconds(info.Duration);
t = t(1:end-1);
plot(t, y)
xlabel('Time')
ylabel('Audio Signal')
```

解释：

| 代码 | 作用 |
|---|---|
| `audioread` | 读取音频样本和采样率 |
| `sound(y, Fs)` | 按采样率播放音频 |
| `t = ...` | 创建时间轴 |
| `plot(t, y)` | 绘制 waveform |

---

## 22. 本节与考试的连接

### 22.1 高频考点 1：Nyquist 与 aliasing

你需要会：

1. 根据最高频率求 Nyquist rate；
2. 根据采样率求 Nyquist frequency；
3. 判断哪些频率会 alias；
4. 计算 alias frequency；
5. 解释 anti-aliasing filter 的作用。

常用句式：

```text
The Nyquist frequency is half the sampling rate. Any component above this frequency will be aliased and appear as a lower folded frequency in the sampled signal.
```

### 22.2 高频考点 2：bit depth、SQNR、dynamic range

你需要会：

- $2^N$ levels；
- quantisation interval；
- maximum quantisation noise；
- $SQNR\approx6.02N$；
- $SQNR\approx6.02N+1.76$；
- 每增加 1 bit，动态范围增加约 6 dB。

### 22.3 高频考点 3：文件大小与码率

一定要记住：

$$
\text{file size} = f_s \times N \times C \times T
$$

单位是 bits。如果要 bytes，除以 8。

例如 48 kHz、16-bit、stereo、60 s：

$$
48000\times16\times2\times60=92,160,000\text{ bits}
$$

$$
\frac{92,160,000}{8}=11,520,000\text{ bytes}\approx11.52\text{ MB}
$$

这类题很像试卷中的 WAV 文件大小计算。

### 22.4 高频考点 4：A-law 与心理声学

答题关键词：

- companding；
- non-uniform quantisation；
- logarithmic perception；
- Weber's law；
- low-amplitude signals need finer resolution；
- reduces bit depth while preserving perceptual quality.

### 22.5 高频考点 5：音频格式分类

可能会要求你解释：

- WAV 与 MP3 的区别；
- PCM 是什么；
- lossy vs lossless；
- container 与 codec 的区别；
- FLAC 为什么无损；
- RAW 为什么需要额外参数才能读取。

---

## 23. 本节公式总结

| 公式 | 含义 |
|---|---|
| $f_s\ge2f_{max}$ | Nyquist theorem |
| $\text{Nyquist frequency}=f_s/2$ | 给定采样率可表示的最高频率 |
| $f_{alias}=|f-nf_s|$ | 混叠频率，选择 $n$ 使结果落入 $0$ 到 $f_s/2$ |
| $\text{levels}=2^N$ | $N$ bit 可表示的量化等级数 |
| $\Delta V=\frac{2V_{max}}{2^N}$ | 量化间隔 |
| $e_{max}=\Delta V/2$ | 最大量化误差 |
| $SQNR\approx6.02N$ dB | 位深与 SQNR 的近似关系 |
| $SQNR\approx6.02N+1.76$ dB | 满幅正弦波常用 SQNR 公式 |
| $\text{bitrate}=f_s\times N\times C$ | 未压缩 PCM 码率 |
| $\text{file size}=f_s\times N\times C\times T/8$ | 文件大小，单位 bytes |

---

## 24. 本节关键词表

| 英文术语 | 中文理解 |
|---|---|
| Digitisation | 数字化，把模拟信号转换为数字信号 |
| ADC | 模数转换器，Analog-to-Digital Converter |
| Sampling | 采样，在时间轴上按固定间隔取值 |
| Sampling rate | 采样率，每秒采样次数 |
| Nyquist rate | 奈奎斯特采样率，捕捉最高频率所需最低采样率 |
| Nyquist frequency | 奈奎斯特频率，采样率一半 |
| Aliasing | 混叠，高频被错误表示成低频 |
| Anti-aliasing filter | 抗混叠滤波器，采样前去除过高频率 |
| Quantisation | 量化，把连续振幅映射到有限等级 |
| Bit depth | 位深，每个样本使用的 bits 数 |
| Quantisation error | 量化误差，真实值与量化值之差 |
| Quantisation noise | 量化噪声，量化误差造成的噪声 |
| SQNR | 信号与量化噪声比 |
| Dynamic range | 动态范围，最大与最小可用信号之比 |
| Dithering | 抖动，通过加入微小随机噪声掩盖量化失真 |
| Noise shaping | 噪声整形，把噪声推向人耳不敏感频段 |
| Companding | 压扩，先压缩动态范围再扩展 |
| A-law | A 律压扩，非均匀量化方法 |
| Weber's Law | 韦伯定律，刚可察觉差异与刺激强度有关 |
| PCM | 脉冲编码调制，未压缩数字音频基础格式 |
| Codec | 编码/解码算法 |
| Container | 容器格式，包装音频数据和元数据 |
| DRM | 数字版权管理 |

---

## 25. 复习自测题

1. Sampling 和 quantisation 分别在什么维度上操作？
2. CD 44.1 kHz 的 Nyquist frequency 是多少？为什么它能覆盖人耳听觉范围？
3. 如果最高频率是 20 kHz，Nyquist rate 是多少？
4. 什么是 aliasing？为什么采样率不足会导致高频折叠成低频？
5. 已知 $f=1000$ Hz，$f_s=1500$ Hz，alias frequency 是多少？
6. Anti-aliasing filter 应该放在 ADC 前还是后？为什么？
7. 8-bit、16-bit、24-bit 分别有多少量化等级？
8. Quantisation error 为什么最多是半个量化间隔？
9. 为什么每增加 1 bit，动态范围大约增加 6 dB？
10. 8-bit、16-bit、24-bit 的近似动态范围分别是多少？
11. Dithering 是消除噪声还是改变噪声性质？
12. 44.1 kHz、16-bit、stereo 的 CD 音频码率是多少？
13. 48 kHz、16-bit、stereo、1 分钟 WAV 文件约多大？
14. 为什么线性地从 16-bit 降到 8-bit 会严重损害低幅度信号？
15. A-law 使用了人耳的哪种听觉性质？
16. WAV、MP3、FLAC、RAW 的关键区别是什么？
17. Container 和 codec 的区别是什么？
18. Matlab 中 `audioinfo` 和 `audioread` 分别用于什么？

---

## 26. 一句话总结

本节课说明：**声音数字化就是在时间上采样、在振幅上量化**。采样率决定能否正确表示高频，位深决定振幅精度和动态范围；采样率不足会混叠，位深不足会产生量化噪声。理解这些概念后，才能正确计算音频文件大小、判断音频质量，并理解 WAV、MP3、FLAC 等格式背后的技术差异。
