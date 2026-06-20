
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

