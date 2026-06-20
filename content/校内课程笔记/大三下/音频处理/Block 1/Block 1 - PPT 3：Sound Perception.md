
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

