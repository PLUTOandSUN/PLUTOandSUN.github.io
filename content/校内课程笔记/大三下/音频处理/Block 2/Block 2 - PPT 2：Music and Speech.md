> [!info] 课件来源
> 原始课件：[[课程笔记/音频处理/附件/Block 2 - MIDI, Sound Synthesis, Music & Speech/6. Music and Speech.pdf]]  
> 本节接在 [[#Block 2 - PPT 1：MIDI and Sound Synthesis]] 之后，重点比较 **music** 与 **speech** 的声学特征、认知处理方式，以及语音处理技术在 ASR、TTS、说话人识别等领域的应用。

## 0. 本节课的整体框架

这份 PPT 的标题是 **Music and Speech**。它把前面学过的频率、频谱、声谱图、谐波、音色、MIDI 与声音合成知识，连接到“人类声音通信”和“语音技术”。

主要分为四部分：

1. **Comparing Music and Speech**：比较音乐和语音在 pitch、rhythm、timbre、frequency content 上的相似与差异。
2. **Cognitive and Perceptual Processing**：大脑如何处理语音和音乐，它们在记忆、情绪、意义表达上的区别。
3. **Speech Characteristics**：语音产生机制、voiced/voiceless、fricatives、plosives、formants、spectrogram。
4. **Applications in Technology and Research**：speech processing、ASR、speaker verification/identification，以及现代应用和挑战。

> [!summary] 本节核心
> 音乐和语音都是听觉通信形式，都依赖 pitch、rhythm、timbre 和 frequency content。但语音主要传递明确语义，音乐更偏情感和艺术表达。语音处理技术的关键是从音频信号中提取可用于识别、合成、增强或验证身份的特征。

---

## 1. 为什么要比较 Music 和 Speech？

音乐和语音看起来是不同领域，但从音频处理角度看，它们有很多共同点：

- 都是随时间变化的声波；
- 都可以用 waveform、spectrum、spectrogram 表示；
- 都包含 pitch、rhythm、timbre、loudness 等特征；
- 都会被人耳和大脑解释成有意义的听觉对象；
- 都可以通过数字信号处理、机器学习和感知模型进行分析。

但二者的主要目的不同：

| 方面 | Speech | Music |
|---|---|---|
| 主要目的 | 传递语言信息 | 表达情绪、结构、艺术想法 |
| 基本单位 | phoneme、syllable、word、sentence | note、chord、rhythm、phrase |
| 结构约束 | 受语言语法和语义约束 | 受调式、和声、节拍、风格约束 |
| 可理解性 | 重点是 intelligibility 和 meaning | 重点是 expression、aesthetics、emotion |

PPT 的两个关键问题是：

1. 大脑如何分别处理音乐和语音？
2. 什么使声音听起来像“音乐”，什么使声音听起来像“语言”？

---

## 2. Pitch and Frequency Content：音高与频率内容

### 2.1 Speech 中的 pitch

语音中的 pitch 主要由 **fundamental frequency, F0** 决定。

F0 会受到多种因素影响：

- speaker：不同说话人的声带长度和张力不同；
- language：不同语言对声调、重音、语调的使用不同；
- emotion：兴奋、悲伤、疑问等会改变 pitch pattern；
- gender / age：声带结构和生理条件不同。

语音里的 pitch 不只是“高低”，它还参与表达意义。例如：

- 英语中句末升调常表示 question；
- 句子重音可以突出信息焦点；
- 语调变化可以表达情绪；
- 声调语言中 pitch contour 可以改变词义。

### 2.2 Music 中的 pitch

音乐通常使用更固定的 pitch system：

- scales 音阶；
- tones 音级；
- intervals 音程；
- harmony 和声；
- tuning system 调律系统。

音乐 note 通常有明确的 fundamental frequency。例如：

$$
A4=440\text{ Hz}
$$

高一个八度：

$$
A5=880\text{ Hz}
$$

### 2.3 Speech vs Music 的 pitch 差异

| 方面        | Speech                          | Music                           |
| --------- | ------------------------------- | ------------------------------- |
| pitch 稳定性 | 更连续、更可变                         | 更离散、更稳定                         |
| 主要功能      | intonation、prosody、emotion、tone | melody、harmony、scale            |
| 频率关系      | 不一定遵循固定比例                       | 常遵循音阶和和声关系                      |
| 例子        | 疑问句升调                           | C major scale、chord progression |

> [!note] 重要理解
> 语音的 pitch 是“动态表达工具”，音乐的 pitch 更常是“结构化音高系统”。

---

## 3. Temporal and Frequency Domains：时域与频域

声音可以在两个主要域中表示：

| 表示域 | 关注点 | 图像 |
|---|---|---|
| Temporal domain | 振幅如何随时间变化 | waveform |
| Frequency domain | 声音包含哪些频率成分 | spectrum |
| Time-frequency domain | 频率成分如何随时间变化 | spectrogram |

### 3.1 Fourier transform 的作用

PPT 回顾了 Fourier transform：复杂波形可以看作许多简单正弦波的叠加。

对于周期性复杂声音：

```text
complex waveform = fundamental + harmonics + other components
```

其中整数倍频率称为 **harmonic frequencies**。

在频域中，数据通常表示为不同 frequency components 的 amplitude。

### 3.2 为什么语音和音乐都需要频域分析？

因为很多重要信息在 waveform 中不直观，但在 spectrum / spectrogram 中很明显：

- 音乐中的 harmonic structure；
- 乐器 timbre；
- 语音中的 formants；
- 元音和辅音差异；
- 噪声和清音成分；
- pitch contour；
- 音频事件的起止时间。

---

## 4. Audio histogram、spectrum、spectrogram

### 4.1 Audio histogram

Audio histogram 是对 time-domain samples 的统计分析。

它显示：

> 在一个音频片段中，每个 amplitude level 上有多少 samples。

用途：

- 判断音频是否 clipping；
- 看音量分布；
- 判断是否存在 DC offset；
- 粗略评估动态范围。

但 histogram 不告诉我们频率信息。

### 4.2 Power / Frequency Spectrum

Power spectrum 或 frequency spectrum 是二维表示：

| 轴 | 含义 |
|---|---|
| x-axis | frequency |
| y-axis | amplitude / power |

它回答的问题是：

```text
这一段声音包含哪些频率？每个频率有多强？
```

### 4.3 Spectrogram

Spectrogram 是三维信息的二维图像：

| 维度 | 含义 |
|---|---|
| x-axis | time |
| y-axis | frequency |
| colour / brightness | amplitude / energy |

它回答的问题是：

```text
声音中的频率成分如何随时间变化？
```

### 4.4 Speech 和 music 的 spectrogram 差异

一般来说：

| 特征 | Speech spectrogram | Music spectrogram |
|---|---|---|
| 时间变化 | 很快，音素变化明显 | 更依赖音符和节拍结构 |
| harmonic lines | voiced sounds 中可见 | 乐器音通常清晰 |
| formants | 元音中明显 | 不以 formants 为核心 |
| noise components | 辅音中明显 | 鼓、擦弦、噪声乐器中明显 |
| rhythm | 语言自然节奏 | 更规则的拍点和重复结构 |

---

## 5. Pitch changing 的意义

Pitch 变化在动物叫声、人类语言和音乐中都有意义，但表达内容不同。

### 5.1 Animal calls

动物叫声中的 pitch change 可能表达：

- dominance；
- threat；
- fear；
- alarm；
- submission；
- mating signal。

### 5.2 Human speech

人类语言中 pitch change 主要体现为：

- intonation 语调；
- emotion 情绪；
- question vs statement；
- focus / emphasis；
- tonal language 中的词义区分。

### 5.3 Music

音乐中的 pitch change 表示：

- melody；
- harmony；
- tension and release；
- positive / negative affect；
- stylistic expression。

### 5.4 Pitch and emotion

PPT 展示了单词在不同情绪下的 pitch distribution。通常：

- excited speech 可能 F0 更高、变化更大；
- subdued / sad speech 可能 F0 更低、变化更小；
- anger 可能伴随更高 energy 和更大 pitch variation。

---

## 6. Tonal language：声调语言中的 pitch

在声调语言中，pitch contour 可以改变词义。

例如普通话中同一个音节，如果声调不同，含义可能完全不同。

从音频处理角度看，tonal language 要求系统不仅识别 phoneme，还要识别 F0 contour。

这对 ASR 很重要：

- 英语 ASR 更重视 phoneme sequence、stress、context；
- 汉语等声调语言 ASR 还需要准确建模 tone / pitch contour。

> [!important] 语音 pitch 不只是情绪
> 在非声调语言中 pitch 常用于语调和情绪；在声调语言中 pitch 还能直接区分词义。

---

## 7. Rhythm and Timing：节奏与时间结构

### 7.1 Speech 中的 rhythm

语音节奏受语言结构影响：

- syllable timing；
- stress timing；
- pauses；
- speech rate；
- phrase boundary；
- emphasis。

这些因素会影响意义和听感。

例如 pause 的位置不同，句子理解可能不同。

### 7.2 Music 中的 rhythm

音乐节奏通常更规则：

- beats；
- tempo；
- meter；
- bar；
- repeated rhythmic patterns。

音乐中的 timing 更容易被网格化，例如 4/4 拍、120 BPM。

### 7.3 Speech vs Music timing

| 方面 | Speech | Music |
|---|---|---|
| rhythm | irregular，受 stress 和 meaning 影响 | regular，基于 beat 和 meter |
| timing | flexible，adaptive | precise，quantised 或 metered |
| pauses | 影响语义和语气 | 用于 phrasing 和 dramatic effect |
| repetition | 不一定重复 | 常有循环和 pattern |

### 7.4 Stress-timed vs syllable-timed languages

PPT 提到：

- **Stress-timed languages**：重读音节之间的时间趋于稳定，非重读音节会被压缩，例如英语。
- **Syllable-timed languages**：每个音节长度更接近，例如许多罗曼语族语言。

这说明不同语言的 rhythm 结构不同，ASR 和语音合成系统需要考虑语言差异。

---

## 8. Timbre and Harmonics：音色与谐波

### 8.1 Speech 中的 timbre

语音 timbre 主要由：

- vocal tract shape；
- vocal fold vibration；
- formants；
- nasal/oral cavity resonance；
- individual anatomy；
- speaking style。

每个人的声道形状不同，因此声音具有个人特征。这也是 speaker recognition 的基础。

### 8.2 Music 中的 timbre

音乐 timbre 主要由：

- harmonic structure；
- attack / sustain / decay；
- instrument body resonance；
- playing technique；
- synthesis parameters。

例如小提琴和小号即使演奏同一个音高，也能被区分，是因为它们的谐波分布和 envelope 不同。

### 8.3 Formants 与 harmonics 的区别

| 概念 | 含义 | 主要用于 |
|---|---|---|
| Harmonics | 基频的整数倍频率 | 乐器音色、voiced speech |
| Formants | 声道共振峰，增强某些频率区域 | 元音识别、语音 timbre |

在语音中，F0 决定声音 pitch，而 formants 更决定 vowel quality。

---

## 9. Cognitive and Perceptual Processing：认知与感知处理

### 9.1 Speech processing in brain

PPT 中提到语音处理通常有 left hemisphere dominance，特别是：

- Broca's area：与语言产生、语法处理相关；
- Wernicke's area：与语言理解相关；
- auditory cortex：处理声音输入。

语音处理重点包括：

- phonemes；
- syntax；
- semantics；
- speaker identity；
- prosody。

### 9.2 Music processing in brain

音乐处理常涉及更多右半球活动，尤其是：

- melody；
- harmony；
- emotional response；
- musical memory。

但这不是绝对划分。音乐和语音都使用 auditory cortex，也存在重叠脑区。

### 9.3 Music or Speech?

PPT 中的 “Music or Speech?” 说明：当一句话被唱出来时，它同时包含：

- speech 的 linguistic information；
- music 的 pitch、rhythm、melodic information。

如果保留 time information，可能更像 speech；如果强调 spectral / pitch structure，可能更像 music。这说明音乐和语音之间存在连续谱，而不是完全分离。

---

## 10. Memory and Learning Differences

### 10.1 Speech memory

语音记忆常依赖：

- short-term phonological memory；
- semantic associations；
- sentence structure；
- context。

例如记住一句话，不只是记声音，还会依赖语义理解。

### 10.2 Music memory

音乐记忆可能非常持久。PPT 提到：某些 dementia 患者仍能回忆歌曲。

原因可能包括：

- melody cues；
- rhythm cues；
- emotional memory；
- repetition；
- long-term procedural memory。

### 10.3 学习中的音乐线索

把内容编成歌更容易记忆，是因为 melody 和 rhythm 提供额外 retrieval cues。

---

## 11. Emotion and Communication

### 11.1 Speech conveys explicit meaning

语音通过 words 传递明确语义，同时 prosody 传递情绪。

**Prosody** 包括：

- intonation；
- stress；
- rhythm；
- pitch contour；
- speaking rate；
- pauses。

### 11.2 Music conveys implicit emotion

音乐通常没有明确词义，但能通过：

- harmony；
- melody；
- rhythm；
- tempo；
- timbre；
- dynamics；

引发强烈情绪反应。

### 11.3 对比

| 方面 | Speech | Music |
|---|---|---|
| meaning | explicit semantic meaning | implicit affective meaning |
| emotion | prosody + words | melody/harmony/rhythm/timbre |
| communication | 信息传递为主 | 情绪和审美体验为主 |

---

## 12. Speech Production：语音产生机制

语音产生可以分为几个系统：

| System | Role | Key components |
|---|---|---|
| Respiratory system | 提供气流 | lungs、diaphragm、intercostal muscles |
| Phonatory system | 通过声带产生 voicing | larynx、vocal folds、glottis |
| Articulatory system | 塑造具体语音 | pharynx、oral cavity、nasal cavity、tongue、lips、teeth |
| Nervous system | 控制和协调 | brain、cranial nerves |

简单流程：

```text
肺部气流 → 喉部声带振动/不振动 → 口腔/鼻腔/舌/唇塑形 → 形成语音
```

---

## 13. Types of Speech Sounds：语音声音类型

### 13.1 Voiced sounds 浊音

**Voiced sounds** 产生时 vocal folds 振动。你可以把手放在喉咙上感受到振动。

特点：

- 有明显 F0；
- 波形常呈准周期；
- 所有 vowels 都是 voiced；
- 频谱中有 harmonics 和 formants。

### 13.2 Voiceless sounds 清音

**Voiceless sounds** 产生时 vocal folds 不振动。

例如：

- /p/；
- /t/；
- /k/；
- /f/；
- /s/。

它们通常更像噪声或瞬态爆破。

### 13.3 Fricatives 擦音

Fricative 是空气通过狭窄通道产生湍流。

例子：

| Type | Voiced examples | Voiceless examples |
|---|---|---|
| Fricative | /v/, /z/, /ʒ/ | /f/, /s/, /ʃ/, /h/ |

声谱图中 fricatives 往往表现为高频噪声带。

### 13.4 Plosives 爆破音

Plosive 是口腔通道完全闭合后突然释放气流。

| Type | Voiced examples | Voiceless examples |
|---|---|---|
| Plosive | /b/, /d/, /g/ | /p/, /t/, /k/ |

波形中常表现为短暂 silence / closure 后出现 burst。

---

## 14. Voiced Speech Sounds：浊音语音特征

PPT 中强调 voiced speech 有两个可用于 speech processing 的重要性质：

1. 某些时间段内近似周期性；
2. voiced sounds 的 spectrum 中有 formants。

### 14.1 Quasi-stationary 20-30 ms

语音整体变化很快，但在很短窗口内可以近似稳定。

通常：

$$
20\text{ ms} \sim 30\text{ ms}
$$

内语音信号近似 quasi-stationary。

这就是为什么 ASR 常用 25 ms 左右的 frame 做 STFT / MFCC。

### 14.2 Voiced speech characteristics

| Characteristic | 说明 |
|---|---|
| Fundamental Frequency F0 | 声带振动决定 voice pitch |
| Harmonics | F0 的整数倍，被 vocal tract 放大 |
| Formants | 声道共振频率，决定 vowel quality |
| Spectral Envelope | 频谱整体形状，受 formants 和 harmonics 影响 |
| Periodicity | 声带振动造成规则重复波形 |
| Amplitude / Intensity | 受气流和声带张力影响 |
| Duration | 受 stress、context、speaking rate 影响 |

### 14.3 Formant examples

PPT 给出一些元音的 F1/F2 例子：

| Vowel | Example | F1 | F2 | Description |
|---|---|---:|---:|---|
| /i/ | see | 300 Hz | 2300 Hz | high front vowel |
| /e/ | bet | 500 Hz | 1900 Hz | mid front vowel |
| /æ/ | cat | 700 Hz | 1800 Hz | low front vowel |
| /u/ | boot | 300 Hz | 800 Hz | high back vowel |
| /o/ | boat | 500 Hz | 900 Hz | mid back vowel |
| /a/ | father | 700 Hz | 1100 Hz | low back vowel |

> [!important] 记忆
> F0 更多决定 pitch，F1/F2 等 formants 更多决定 vowel identity。

---

## 15. Speech in temporal and frequency domains

PPT 以单词 “phonetician” 的 waveform 和 spectrogram 为例：

- waveform 展示时间域振幅；
- spectrogram 展示频率随时间变化；
- voiced segments 中能看到 formant bands；
- consonants 可能表现为 noise burst 或高频噪声；
- silence / closure 在 waveform 和 spectrogram 中都能看到。

对于语音分析，spectrogram 通常比单纯 waveform 更有信息量，因为它能同时展示时间和频率结构。

---

## 16. Introduction to Speech Processing

**Speech processing** 是研究和应用人类语音信号分析、合成和处理技术的领域。

它结合：

- signal processing；
- machine learning；
- linguistics；
- acoustics；
- cognitive science。

目标是让系统能够：

- 分析语音；
- 识别语音内容；
- 生成语音；
- 增强语音；
- 压缩语音；
- 识别说话人。

---

## 17. Speech Processing Applications

PPT 列出五类主要应用：

| Application | 目标 |
|---|---|
| Speech Recognition | spoken language → text |
| Speech Synthesis | text → artificial speech |
| Speech Coding | 压缩语音以便存储或传输 |
| Speech Enhancement | 降噪、去混响、提高 intelligibility |
| Speaker Recognition | 根据声音识别或验证说话人身份 |

### 17.1 Speech analysis: Who? What? How?

PPT 用 “Who? What? How?” 概括 speech analysis：

| 问题 | 对应任务 |
|---|---|
| Who? | speaker identification / verification |
| What? | speech recognition，识别说了什么 |
| How? | emotion、prosody、speaking style、understanding |

---

## 18. Automatic Speech Recognition, ASR

ASR 的目标是：

```text
speech audio → text transcription
```

机器识别语音需要结合：

- signal processing；
- machine learning；
- linguistic modeling。

---

## 19. ASR pipeline：关键技术步骤

一个传统 ASR 系统通常包含：

```text
Audio input → preprocessing → feature extraction → acoustic model → language model → decoding → text output
```

### 19.1 Audio input and preprocessing

包括：

- audio capture；
- digitisation；
- noise reduction；
- normalization；
- silence removal；
- framing。

### 19.2 Feature extraction

ASR 不直接使用原始 waveform，而是提取特征。

常见特征：

| Feature | 作用 |
|---|---|
| STFT | 把信号分成短帧，提取 time-frequency 信息 |
| MFCC | 模拟人耳 mel scale，表示短时功率谱 |
| Pitch | F0、intonation、speaker cues |
| Energy | 音量、stress、endpoint detection |
| Spectral features | spectral centroid、bandwidth、formants 等 |

#### STFT

PPT 提到音频被分成小时间帧，例如：

$$
25\text{ ms}
$$

原因是语音在短时间内近似 quasi-stationary。

#### MFCC

MFCC 是 ASR 中非常经典的语音特征。

它大致流程：

```text
speech signal → pre-emphasis → framing → windowing → FFT → Mel filter bank → log → DCT → MFCC vector
```

MFCC 的意义：

- 保留短时频谱包络；
- 强调人耳重要频率；
- 对 phoneme 和 vowel 识别有用；
- 比原始 waveform 更稳定、更低维。

---

## 20. Acoustic Modeling

**Acoustic model** 把声学特征映射到语音基本单位，例如 phoneme。

### 20.1 Phoneme recognition

Phoneme 是语言中最小的可区分声音单位。

例如 cat 中的 /k/、/æ/、/t/。

ASR 需要从 MFCC 或 spectrogram 特征中判断当前声音更像哪个 phoneme。

### 20.2 Traditional models: HMM

传统 ASR 常用 **Hidden Markov Models, HMMs**。

HMM 适合语音，因为语音是时间序列，并且 phoneme 状态随时间转移。

### 20.3 Modern models: DNN/CNN/RNN/Transformers

现代 ASR 更多使用 deep learning：

| Model | 作用 |
|---|---|
| CNN | 从 spectrogram 中提取局部时频模式 |
| RNN / LSTM / GRU | 建模时间依赖 |
| Transformer | 建模长距离上下文，适合大规模语音识别 |
| End-to-end models | 直接从 audio/features 映射到 text |

---

## 21. Language Modeling

Acoustic model 只告诉系统“声音像什么 phoneme/word”，但语言模型告诉系统“什么词序列更合理”。

### 21.1 Word prediction

例子：

```text
I am ____
```

后面接 “going” 的概率比 “banana” 更高。

### 21.2 N-grams

传统语言模型常用 n-grams：

- unigram：看单个词；
- bigram：看前一个词；
- trigram：看前两个词。

缺点是上下文范围有限。

### 21.3 Transformers

现代系统使用 Transformers，例如 GPT、BERT 类架构，能够捕捉长距离上下文关系。

优点：

- 更强的语义建模；
- 能处理长文本依赖；
- 对上下文和歧义更敏感。

---

## 22. Decoding

**Decoding** 是把 acoustic model 和 language model 结合起来，寻找最可能的 word sequence。

常见算法：

| Algorithm | 常见场景 |
|---|---|
| Viterbi algorithm | HMM-based ASR |
| Beam search | neural ASR / seq2seq models |

输出是最终 transcription。

可以把 decoding 理解为：

```text
声学证据 + 语言合理性 → 最可能的文字结果
```

---

## 23. Modern ASR key technologies

PPT 总结了现代 ASR 的关键技术：

### 23.1 Deep learning

- CNN：从 spectrogram 中提取局部模式；
- RNN：建模语音时间依赖；
- Transformers：建模长程上下文。

### 23.2 End-to-end models

例如 Wave2Vec、DeepSpeech 等系统可以直接把音频映射到文字，减少传统 pipeline 中手工分离 acoustic model 和 language model 的步骤。

### 23.3 Transfer learning

先在大规模数据上预训练，再针对特定语言、口音、领域或任务 fine-tune。

优点：

- 降低标注数据需求；
- 提升小语种或专业领域表现；
- 提高鲁棒性。

---

## 24. Speaker Verification and Identification

### 24.1 Speaker verification 说话人验证

Speaker verification 回答的问题是：

> Is this person who they claim to be?

它是 **one-to-one comparison**。

流程：

```text
claimed identity + voice sample → compare with enrolled model → accept / reject
```

例子：

- 银行电话认证；
- 手机声纹登录；
- 安全门禁。

### 24.2 Speaker identification 说话人识别

Speaker identification 回答的问题是：

> Who is speaking?

它是 **one-to-many comparison**。

流程：

```text
unknown voice sample → compare against speaker database → identify best match
```

例子：

- 会议中自动标注谁在说话；
- 法庭音频分析；
- 监控系统中的说话人查找。

### 24.3 Verification vs Identification 对比

| 方面 | Speaker Verification | Speaker Identification |
|---|---|---|
| 问题 | 是不是这个人？ | 这个人是谁？ |
| 比较方式 | one-to-one | one-to-many |
| 输入 | claimed identity + voice sample | unknown voice sample |
| 输出 | accept / reject | speaker identity / unknown |
| 难度 | 较低 | 较高，数据库越大越难 |
| 应用 | 登录、银行、门禁 | 取证、监控、会议分析 |

> [!warning] 安全注意
> 声纹系统可能受到 replay attack、voice cloning、background noise、microphone mismatch 等影响，因此实际应用需要反欺骗和鲁棒性设计。

---

## 25. Speech processing 的重要应用

PPT 列出了很多 speech processing 的实际应用领域。

### 25.1 Human-Computer Interaction

例如：

- Siri；
- Alexa；
- Google Assistant；
- voice commands；
- smart home voice control。

语音让人机交互更自然，尤其适合 hands-free 场景。

### 25.2 Accessibility

包括：

- speech-to-text：帮助听障人士或需要字幕的人；
- text-to-speech：帮助视障人士或阅读困难者；
- real-time translation：跨语言交流。

### 25.3 Communication

语音处理改善通信质量：

- noise reduction；
- echo cancellation；
- speech enhancement；
- VoIP；
- teleconferencing。

### 25.4 Healthcare

语音分析可用于辅助检测：

- speech disorders；
- Parkinson's disease；
- depression；
- neurological conditions。

也可帮助开发 speech-generating devices。

### 25.5 Automation and Efficiency

例如：

- customer service bots；
- meeting transcription；
- lecture captioning；
- voice search。

### 25.6 Security and Surveillance

包括：

- speaker identification；
- forensic audio analysis；
- keyword spotting；
- compliance monitoring。

### 25.7 Natural Language Understanding

NLU 不只是把语音转文字，还要理解：

- intent；
- sentiment；
- emotion；
- context；
- sarcasm / humor；
- dialogue state。

### 25.8 Education and Multimodal Applications

教育场景：

- pronunciation feedback；
- language learning apps；
- real-time captions。

多模态场景：

```text
speech + text + vision + gesture → richer interaction
```

例如 AR / VR 中，用语音和手势共同控制对象。

---

## 26. Challenges in Speech Processing

尽管语音处理发展很快，仍然有很多挑战。

| Challenge | 说明 |
|---|---|
| Accents and dialects | 口音和方言差异影响识别准确率 |
| Noise and distortion | 背景噪声、混响、设备差异会干扰识别 |
| Contextual understanding | 讽刺、幽默、文化背景难以理解 |
| Variability in speech | 语速、情绪、说话风格、录音质量变化大 |
| Ambiguity | homophones、homonyms、上下文歧义 |
| Real-time processing | 需要低延迟和足够算力 |
| Multilingual issues | 多语言、code-switching 复杂 |
| Data limitations | 标注数据不足、隐私限制 |
| Robustness | 新环境、新说话人、新设备适应困难 |
| Ethics | bias、fairness、voice privacy、voice cloning 风险 |
| Multimodal integration | 多模态同步和融合困难 |

---

## 27. 本节与考试的连接

### 27.1 可能考 Music vs Speech 比较

答题可从以下维度组织：

| 维度 | Speech | Music |
|---|---|---|
| Intent | informational | expressive/artistic |
| Pitch | variable F0, prosody, tone | structured notes, scales, harmony |
| Rhythm | natural, language-dependent | metered, tempo-based |
| Timbre | speaker-specific, formants | instrument-specific, harmonics/envelope |
| Meaning | explicit semantic meaning | implicit emotional meaning |
| Brain | left-dominant for language | right more active for melody/harmony, but overlaps |

### 27.2 可能考 Spectrogram / Spectrum

需要会解释：

- waveform：time vs amplitude；
- spectrum：frequency vs amplitude；
- spectrogram：time vs frequency，颜色表示 amplitude；
- speech spectrogram 可显示 formants、voiced/unvoiced、plosives/fricatives。

### 27.3 可能考 Speech sounds

关键词：

- voiced：vocal folds vibrate；
- voiceless：vocal folds do not vibrate；
- fricative：air through narrow constriction；
- plosive：complete closure then release；
- formants：vocal tract resonances；
- voiced speech quasi-stationary around 20-30 ms。

### 27.4 可能考 ASR pipeline

答题模板：

```text
ASR converts speech audio into text. A typical pipeline includes audio capture and preprocessing, feature extraction such as STFT or MFCCs, acoustic modeling to map features to phonemes, language modeling to predict likely word sequences, and decoding using algorithms such as Viterbi or beam search to output the final transcription.
```

中文结构：

```text
输入语音 → 预处理 → 特征提取 MFCC/STFT → 声学模型 → 语言模型 → 解码 → 文本
```

### 27.5 可能考 Speaker verification vs identification

最重要区别：

```text
Verification = one-to-one, “Is this claimed person?”
Identification = one-to-many, “Who is speaking?”
```

---

## 28. 本节关键词表

| 英文术语 | 中文理解 |
|---|---|
| Speech | 语音，主要用于语言信息传递 |
| Music | 音乐，主要用于艺术与情绪表达 |
| Fundamental frequency, F0 | 基频，语音中常对应 voice pitch |
| Prosody | 韵律，包括语调、重音、节奏、停顿等 |
| Intonation | 语调，pitch contour 变化 |
| Tonal language | 声调语言，pitch contour 可改变词义 |
| Temporal domain | 时域，振幅随时间变化 |
| Frequency domain | 频域，频率成分及其强度 |
| Spectrum | 频谱，frequency vs amplitude |
| Spectrogram | 声谱图，time vs frequency，颜色表示能量 |
| Audio histogram | 样本振幅分布统计图 |
| Timbre | 音色 |
| Harmonics | 谐波，基频整数倍 |
| Formants | 共振峰，声道共振频率 |
| Voiced sound | 浊音，声带振动 |
| Voiceless sound | 清音，声带不振动 |
| Fricative | 擦音，窄通道湍流产生 |
| Plosive | 爆破音，闭塞后释放气流 |
| Speech processing | 语音处理 |
| ASR | 自动语音识别，speech-to-text |
| TTS | 文本转语音，text-to-speech |
| Speech coding | 语音编码/压缩 |
| Speech enhancement | 语音增强，如降噪 |
| Speaker recognition | 说话人识别总称 |
| Speaker verification | 说话人验证，一对一 |
| Speaker identification | 说话人识别，一对多 |
| STFT | 短时傅里叶变换 |
| MFCC | 梅尔频率倒谱系数 |
| Acoustic model | 声学模型，特征到音素/声学单位 |
| Language model | 语言模型，预测词序列概率 |
| Decoding | 解码，寻找最可能文字序列 |
| HMM | 隐马尔可夫模型 |
| DNN | 深度神经网络 |
| Transformer | 基于注意力的序列建模架构 |
| NLU | 自然语言理解 |

---

## 29. 复习自测题

1. 为什么音乐和语音都可以被看作 auditory communication？
2. Speech 和 music 的主要 intent 有什么不同？
3. Speech pitch 和 music pitch 的区别是什么？
4. 为什么声调语言对 pitch contour 更敏感？
5. Waveform、spectrum、spectrogram 分别展示什么？
6. Speech spectrogram 中 formants 通常说明什么？
7. Stress-timed 和 syllable-timed languages 有什么区别？
8. Timbre 在语音和音乐中的来源分别是什么？
9. F0、harmonics、formants 分别代表什么？
10. 为什么 voiced speech 可以在 20-30 ms 内近似 quasi-stationary？
11. Voiced、voiceless、fricative、plosive 的区别是什么？
12. ASR 的完整 pipeline 是什么？
13. MFCC 为什么适合语音识别？
14. Acoustic model 和 language model 的作用分别是什么？
15. HMM、DNN、Transformer 在 ASR 中分别用于什么？
16. Speaker verification 和 speaker identification 的本质区别是什么？
17. Speech enhancement 和 speech coding 的目标有什么不同？
18. Speech processing 在 accessibility 中有哪些应用？
19. 语音处理面临哪些主要挑战？
20. 如果考试要求比较 music and speech，你会从哪些维度回答？

---

## 30. 一句话总结

本节课说明：**音乐和语音共享相同的声学基础，却服务于不同的沟通目的**。音乐更强调结构化音高、节奏和情感表达；语音更强调语言意义、韵律和说话人特征。理解 pitch、rhythm、timbre、formants、spectrogram 和 ASR pipeline，是学习语音处理和现代音频智能应用的基础。
