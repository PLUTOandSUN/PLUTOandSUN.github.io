---
title: EBU5408 Block 2 - MIDI and Sound Synthesis
aliases:
  - block2
  - Block 2 MIDI and Sound Synthesis
  - MIDI and Sound Synthesis
tags:
  - course/音频处理
  - EBU5408
  - digital-audio
  - block2
  - MIDI
  - synthesis
source:
  - "[[课程笔记/音频处理/附件/Block 2 - MIDI, Sound Synthesis, Music & Speech/5. MIDI and Sound Synthesis.pdf]]"
  - "[[课程笔记/音频处理/附件/Block 2 - MIDI, Sound Synthesis, Music & Speech/6. Music and Speech.pdf]]"
created: 2026-06-15
---

# Block 2 - PPT 1：MIDI and Sound Synthesis

> [!info] 课件来源
> 原始课件：[[课程笔记/音频处理/附件/Block 2 - MIDI, Sound Synthesis, Music & Speech/5. MIDI and Sound Synthesis.pdf]]  
> 本节从 Block 1 的数字声音基础，过渡到 **MIDI 控制信息** 和 **电子声音合成**。重点是理解：MIDI 本身不是声音，而是控制乐器或合成器发声的事件指令。

## 0. 本节课的整体框架

本 PPT 主要分成五个部分：

1. **Overview of MIDI and Sound Synthesis**：MIDI 是什么，声音合成是什么，它们在音乐制作中有什么作用。
2. **Understanding MIDI Messages**：MIDI message 的字节结构、十六进制表示、channel messages、system messages。
3. **Hardware Aspects of MIDI**：MIDI IN / OUT / THRU、sequencer、synthesiser 等硬件和系统结构。
4. **Basics of Sound Synthesis**：振荡器、滤波器、放大器、ADSR 包络、调制效果。
5. **Types of Synthesis**：subtractive、additive、FM、wavetable、granular synthesis。

> [!summary] 本节核心
> **MIDI 是“演奏指令”，不是音频波形。** 它告诉合成器“什么时候演奏哪个音、力度多大、用哪个通道和音色”。真正的声音由 synthesiser 根据这些指令生成。声音合成则是通过 oscillator、filter、amplifier、envelope、modulation 等模块创造和塑造声音。

---

## 1. What is MIDI？MIDI 是什么？

### 1.1 MIDI 的全称

**MIDI = Musical Instrument Digital Interface**，即“乐器数字接口”。

它是电子乐器、计算机、声卡、合成器、鼓机、灯光控制器等设备之间通信的标准协议。

### 1.2 MIDI 不是声音

MIDI 很容易和 audio 混淆。它们的区别非常重要：

| 项目 | MIDI | Audio |
|---|---|---|
| 本质 | 控制事件 / 指令 | 声波采样后的数字波形 |
| 内容 | note number、velocity、channel、controller 等 | waveform samples |
| 文件通常大小 | 很小 | 通常较大 |
| 可编辑性 | 可轻松改音高、节奏、力度、乐器 | 改音高和节奏可能影响音质 |
| 是否直接能听 | 不能，必须驱动合成器或音源 | 可以直接播放 |

例如 MIDI 事件可能表示：

```text
在 channel 1 上，以 velocity 100，按下 note number 60
```

这不是一段钢琴声音，而是“让某个音源播放 Middle C”的指令。

> [!important] 记忆
> MIDI 像乐谱或演奏脚本；Audio 像录下来的声音。

### 1.3 MIDI 的作用

MIDI 标准让不同厂商的电子乐器可以互相通信。比如：

```text
MIDI keyboard → computer / DAW → software synthesiser → audio output
```

或者：

```text
sequencer → hardware synthesiser → speakers
```

MIDI 的优势在于：

- 跨设备兼容；
- 数据量小；
- 便于编辑；
- 可以控制任意虚拟或硬件乐器；
- 可以自动化参数，例如音量、滤波器、pitch bend、modulation。

---

## 2. MIDI 简史

PPT 中给出 MIDI 的发展脉络：

| 时间 | 事件 | 意义 |
|---|---|---|
| MIDI 之前 | 不同厂商合成器接口互不兼容 | 设备之间难以通信 |
| 1981 | Dave Smith 和 Ikutaro Kakehashi 提出通用协议概念 | 为电子乐器建立统一语言 |
| 1983 | MIDI 1.0 正式发布 | 成为行业标准 |
| 1980s-1990s | Yamaha、Korg、Roland 等厂商采用 MIDI | sequencer、DAW、sampler 改变音乐制作 |
| 2020 | MIDI 2.0 发布 | 更高分辨率、双向通信、更强表达控制 |

今天 MIDI 不只用于音乐，还可用于：

- 舞台灯光；
- 机器人；
- 游戏；
- VR / AR 控制；
- 交互艺术装置。

---

## 3. MIDI 在音乐制作中的作用

### 3.1 Recording & Composition：录制与作曲

MIDI 可以记录：

- notes 音符；
- velocity 力度；
- timing 时间位置；
- duration 持续时间；
- expression 表情控制。

与录音不同，MIDI 录完后可以无损修改：

- 改错音；
- 改节奏；
- 改力度；
- 改乐器音色；
- 改整段旋律的调性。

### 3.2 Sound Design & Synthesis：声音设计与合成

MIDI 可以控制合成器参数，例如：

- pitch bend；
- modulation；
- filter sweep；
- envelope；
- volume；
- pan；
- effects parameters。

这使得 MIDI 不仅能“演奏音符”，还能控制声音随时间变化。

### 3.3 Editing & Arrangement：编辑与编曲

常见操作：

- **Quantisation**：把演奏时间吸附到节拍网格，使节奏更整齐；
- **Transpose**：整体升降调；
- **Duration editing**：改变音符长度；
- **Layering**：同一旋律叠加多个音色；
- **Automation**：自动改变参数。

### 3.4 Live Performance & Control：现场演出与控制

MIDI mapping 可以把实体控制器映射到 DAW、灯光和效果器。

例如：

- 推子控制音量；
- 旋钮控制滤波器 cutoff；
- pad 触发鼓声；
- 脚踏控制 sustain；
- MIDI Clock 同步鼓机和合成器。

### 3.5 Music Notation & Scoring：乐谱转换

MIDI 数据可以转换为五线谱，方便作曲、编曲和排练。

---

## 4. What is sound synthesis？声音合成是什么？

**Sound synthesis** 是用电子方式生成声音的过程，可以基于：

- mathematical models 数学模型；
- oscillators 振荡器；
- sampled audio 采样音频；
- physical models 物理模型；
- wavetable 波表；
- granular grains 音粒。

### 4.1 声音合成的应用

| 应用 | 说明 |
|---|---|
| Music production | 合成器、DAW、VST 插件 |
| Speech synthesis | Siri、Google Assistant 等 TTS 系统 |
| Game audio | 游戏中的交互式音效和环境声音 |
| Film sound design | 电影、动画中的特殊音效 |

### 4.2 MIDI 与 synthesis 的关系

MIDI 和 synthesis 的关系可以概括为：

```text
MIDI message = 演奏/控制指令
Synthesiser = 接收指令并生成声音的系统
Audio output = 合成器实际输出的声音波形
```

MIDI 不决定最终声音质量，最终音色取决于合成器或音源。

---

## 5. MIDI message 的基本结构

### 5.1 Status byte 与 data byte

PPT 说明：每个 MIDI message 通常由：

```text
1 status byte + 1 或 2 data bytes
```

组成。

| 字节 | 作用 |
|---|---|
| Status byte | 表示消息类型和 channel |
| Data byte 1 | 额外参数，例如 note number、controller number |
| Data byte 2 | 额外参数，例如 velocity、controller value |

### 5.2 Status byte 的两个半字节

一个 byte 有 8 bits，MIDI status byte 可以分成两个 nibble：

```text
高 4 bits：MIDI command
低 4 bits：MIDI channel
```

例如：

```text
0x90 = 1001 0000
```

- `1001` = Note On command；
- `0000` = MIDI channel 编码 0，即实际显示为 Channel 1。

> [!warning] Channel 编号容易错
> MIDI status byte 里 channel 用 0-15 编码，但人通常说 Channel 1-16。  
> 所以：Channel 1 = 0x0，Channel 5 = 0x4，Channel 16 = 0xF。

### 5.3 Data bytes 的范围

MIDI data byte 通常是 7-bit 数值，范围：

$$
0 \sim 127
$$

所以：

- note number：0-127；
- velocity：0-127；
- controller value：0-127。

---

## 6. MIDI message 示例解析

PPT 示例：

```text
Binary: 1001 0000 | 0011 1100 | 0111 1111
Hex:    0x90      | 0x3C      | 0x7F
```

逐字节解释：

| Byte | Hex | Binary | 含义 |
|---|---|---|---|
| Status | 0x90 | 1001 0000 | Note On，Channel 1 |
| Data 1 | 0x3C | 0011 1100 | note number 60，Middle C |
| Data 2 | 0x7F | 0111 1111 | velocity 127，最大力度 |

因此这条消息的意思是：

```text
在 MIDI Channel 1 上，以最大力度按下 Middle C。
```

---

## 7. Hexadecimal 十六进制复习

### 7.1 十六进制符号

十六进制使用 16 个符号：

```text
0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F
```

其中：

| Hex | Decimal |
|---|---:|
| A | 10 |
| B | 11 |
| C | 12 |
| D | 13 |
| E | 14 |
| F | 15 |

### 7.2 为什么 MIDI 常用 hex？

原因：

1. 比 binary 短；
2. 每 4 个 binary bits 正好对应 1 个 hex digit；
3. 适合表示 byte；
4. MIDI message、内存地址、颜色值等都常用 hex。

例如：

```text
Binary: 1101 1110 1001
Hex:    D    E    9
```

---

## 8. 进制转换练习答案

### 8.1 Exercise 1：Hex to Decimal

| Hex | Decimal 计算 | Decimal |
|---|---|---:|
| A3 | $10\times16+3$ | 163 |
| 1F4 | $1\times256+15\times16+4$ | 500 |
| 7D | $7\times16+13$ | 125 |
| B6 | $11\times16+6$ | 182 |

### 8.2 Exercise 2：Decimal to Hex

| Decimal | Hex |
|---:|---|
| 255 | FF |
| 450 | 1C2 |
| 123 | 7B |
| 999 | 3E7 |

### 8.3 Exercise 3：Binary to Hex

| Binary | 分组 | Hex |
|---|---|---|
| 0011 1100 | 3 C | 3C |
| 1111 0001 | F 1 | F1 |
| 1001 0110 | 9 6 | 96 |
| 1101 1011 | D B | DB |

---

## 9. Types of MIDI messages

MIDI messages 分为两大类：

| 类型               | 范围        | 是否针对 channel | 用途                       |
| ---------------- | --------- | ------------ | ------------------------ |
| Channel Messages | 0x80-0xEF | 是            | 控制某个 channel 的音符、控制器、音色等 |
| System Messages  | 0xF0-0xFF | 否            | 全局同步、定位、设备设置、系统专用信息      |

---

## 10. Channel Messages

### 10.1 常见 channel messages

| Message | Status range | 作用 |
|---|---|---|
| Note Off | 0x80-0x8F | 停止某个音符 |
| Note On | 0x90-0x9F | 开始播放某个音符 |
| Polyphonic Key Pressure | 0xA0-0xAF | 单个键的压力 |
| Control Change | 0xB0-0xBF | 控制参数，如 volume、modulation、sustain |
| Program Change | 0xC0-0xCF | 切换乐器音色 / patch |
| Channel Pressure | 0xD0-0xDF | 整个 channel 的压力 |
| Pitch Bend | 0xE0-0xEF | 弯音，改变音高 |

### 10.2 Note On

格式：

```text
0x9n key_number velocity
```

其中：

- `n` 是 channel 编码 0-15；
- `key_number` 是 MIDI note number；
- `velocity` 表示按键力度，通常影响响度或音色。

### 10.3 Note Off

格式：

```text
0x8n key_number release_velocity
```

也可以用：

```text
Note On with velocity 0
```

来表示关闭音符，这是很多 MIDI 系统中的常见写法。

### 10.4 Program Change

格式：

```text
0xCn program_number
```

它只需要 1 个 data byte，用来切换乐器音色。例如从 piano 切换到 violin。

### 10.5 Pitch Bend

格式：

```text
0xEn LSB MSB
```

Pitch Bend 使用两个 7-bit data bytes 合成更高分辨率的弯音控制。

---

## 11. MIDI channel

MIDI 有 16 个 channel，编号 1-16，但底层编码为 0-15。

| 实际 channel | 编码 nibble | Note On status |
|---:|---:|---:|
| Channel 1 | 0x0 | 0x90 |
| Channel 2 | 0x1 | 0x91 |
| Channel 5 | 0x4 | 0x94 |
| Channel 10 | 0x9 | 0x99 |
| Channel 16 | 0xF | 0x9F |

通常一个 channel 对应一个 instrument。例如：

- Channel 1：piano；
- Channel 2：strings；
- Channel 10：drums / percussion。

---

## 12. Channel message 练习答案

### 12.1 Exercise 1

题目：

```text
0x90 0x3C 0x64
```

问题：

1. What type of MIDI message is this?
2. What is the note number in decimal?
3. What is the velocity in decimal?
4. What MIDI channel is this message on?

答案：

| 项目 | 解释 |
|---|---|
| 0x90 | Note On，channel 编码 0，因此是 Channel 1 |
| 0x3C | $3\times16+12=60$，note number 60，Middle C |
| 0x64 | $6\times16+4=100$，velocity 100 |

完整解释：

```text
在 Channel 1 上，以 velocity 100 播放 MIDI note 60，也就是 Middle C。
```

### 12.2 Exercise 2

题目：

> Write the MIDI message in hexadecimal to turn off a D4, MIDI note 62, on Channel 5 with velocity 50.

步骤：

- Note Off command = 0x8n；
- Channel 5 的编码是 4；
- status byte = 0x84；
- note 62 转 hex = 0x3E；
- velocity 50 转 hex = 0x32。

答案：

```text
0x84 0x3E 0x32
```

补充：有些系统也允许用 Note On velocity 0 关闭音符：

```text
0x94 0x3E 0x00
```

但题目明确说 velocity 50，因此更标准的 Note Off 写法是 `0x84 0x3E 0x32`。

### 12.3 Exercise 3

题目：

```text
0x91 0x40 0x7F
0x92 0x45 0x64
0x93 0x48 0x50
```

逐条解析：

| Message | Command | Channel | Note | Velocity |
|---|---|---:|---:|---:|
| 0x91 0x40 0x7F | Note On | Channel 2 | 0x40 = 64 = E4 | 0x7F = 127 |
| 0x92 0x45 0x64 | Note On | Channel 3 | 0x45 = 69 = A4 | 0x64 = 100 |
| 0x93 0x48 0x50 | Note On | Channel 4 | 0x48 = 72 = C5 | 0x50 = 80 |

问题答案：

1. 差别在于 channel、note number、velocity 都不同。
2. Channel 2 播放 E4，Channel 3 播放 A4，Channel 4 播放 C5。
3. velocity 最高的是第一条，127。

### 12.4 Exercise 4

题目：

> Start playing G3, MIDI note 55, on Channel 7 with velocity 90. Hold the note. Stop it with velocity 0.

步骤：

- Channel 7 编码为 6；
- Note On status = 0x96；
- Note Off status = 0x86；
- note 55 = 0x37；
- velocity 90 = 0x5A；
- velocity 0 = 0x00。

答案：

```text
0x96 0x37 0x5A
... delta time / duration ...
0x86 0x37 0x00
```

也可用 Note On velocity 0 作为关闭：

```text
0x96 0x37 0x5A
... duration ...
0x96 0x37 0x00
```

注意：MIDI message 本身不直接写“持续多久”，在 MIDI file 中通常用 delta time 表示事件间隔。

### 12.5 Exercise 5

题目序列：

```text
0x90 0x3C 0x50
0x80 0x3C 0x00
0x90 0x40 0x64
0x90 0x43 0x64
```

逐条解释：

| Message | 含义 |
|---|---|
| 0x90 0x3C 0x50 | Channel 1 Note On，note 60 Middle C，velocity 80 |
| 0x80 0x3C 0x00 | Channel 1 Note Off，关闭 Middle C |
| 0x90 0x40 0x64 | Channel 1 Note On，note 64 E4，velocity 100 |
| 0x90 0x43 0x64 | Channel 1 Note On，note 67 G4，velocity 100 |

整体效果：

1. 先播放 C4，然后立即或稍后关闭 C4；
2. 然后播放 E4 和 G4；
3. 如果 E4 和 G4 没有 Note Off 且设备 polyphonic，它们会同时响，形成一个双音程。它们也是 C major chord 的两个音，但没有根音 C。

---

## 13. Channel Mode Messages

Channel Mode message 是 Control Change 的特殊情况，其第一个 data byte 在：

```text
121-127 = 0x79-0x7F
```

它们控制乐器如何处理 channel voice messages。

| 1st Data Byte | 功能 | 2nd Data Byte |
|---|---|---|
| 0x79 | Reset all controllers | 0 |
| 0x7A | Local control | 0 = off, 127 = on |
| 0x7B | All notes off | 0 |
| 0x7C | Omni mode off | 0 |
| 0x7D | Omni mode on | 0 |
| 0x7E | Mono mode on | controller number |
| 0x7F | Poly mode on | 0 |

---

## 14. System Messages

System messages 不针对某个 channel，status byte 以 `0xF` 开头。

分为三类：

1. **System Common Messages**：song position、time code、song select 等；
2. **System Real-time Messages**：clock、start、stop、active sensing 等；
3. **System Exclusive Messages，SysEx**：厂商自定义扩展。

### 14.1 System Common Messages

| Status | Name | Function |
|---|---|---|
| 0xF0 | SysEx Start | 开始 manufacturer-specific data |
| 0xF1 | MIDI Time Code Quarter Frame | 同步时间码 |
| 0xF2 | Song Position Pointer | 指示 MIDI sequence 中的位置 |
| 0xF3 | Song Select | 选择歌曲 |
| 0xF6 | Tune Request | 请求模拟合成器调音 |
| 0xF7 | End of SysEx | SysEx 结束 |

### 14.2 System Real-time Messages

| Status | Name | Function |
|---|---|---|
| 0xF8 | Timing Clock | 每四分音符发送 24 次，用于 tempo sync |
| 0xFA | Start | 开始播放 MIDI sequence |
| 0xFB | Continue | 从停止位置继续播放 |
| 0xFC | Stop | 停止播放 |
| 0xFE | Active Sensing | 检测连接是否仍然有效 |
| 0xFF | System Reset | 重置所有 MIDI devices |

### 14.3 System Exclusive Messages

SysEx 用于厂商扩展，比如某个合成器品牌自己的参数、音色库、设备设置。

基本结构：

```text
0xF0 ... manufacturer-specific data ... 0xF7
```

`0xF7` 是 terminator byte，但有些情况下也可以被下一个 status byte 结束。

---

## 15. System message 练习答案

### 15.1 Question 1

题目：判断以下 MIDI messages 是 System Common 还是 System Real-time，并解释功能。

```text
0xF8
0xF2
0xFA
0xFE
```

答案：

| Message | 类型 | 功能 |
|---|---|---|
| 0xF8 | System Real-time | Timing Clock，用于同步 tempo |
| 0xF2 | System Common | Song Position Pointer，指示 sequence 位置 |
| 0xFA | System Real-time | Start，开始播放 sequence |
| 0xFE | System Real-time | Active Sensing，检测连接是否有效 |

### 15.2 Question 2

题目：

```text
0xFA → 0xF8 → 0xF8 → 0xF8 → 0xFC
```

解释：

- `0xFA`：Start，开始播放；
- `0xF8`：Timing Clock pulse，用于保持设备同步；
- 连续三个 `0xF8`：表示播放过程中持续发送时钟同步信号；
- `0xFC`：Stop，停止播放。

完整答案：

```text
一个 MIDI sequence 开始播放，期间收到若干 timing clock 信号用于同步节奏，最后收到 stop message 停止播放。
```

### 15.3 Question 3

题目：MIDI keyboard 每 300 ms 发送一次 `0xFE`。

答案：

1. `0xFE` 是 Active Sensing，用于告诉接收设备连接仍然有效。
2. 如果接收设备停止收到该消息，它可能认为 MIDI connection 断开或设备失联。为了避免 stuck notes，接收设备通常会停止当前音符、执行 all notes off，或进入安全状态。

---

## 16. Responding to MIDI channel messages

合成器通常只响应发给自己 channel 的 message。

例如某个合成器设置为 Channel 2：

- 收到 Channel 1 的 Note On：忽略；
- 收到 Channel 2 的 Note On：播放；
- 收到多个 Channel 2 的 Note On：如果它是 multi-voice / polyphonic，就能同时播放多个音。

---

## 17. Voice、Timbre、Patch、Bank

### 17.1 Timbre 音色

在 MIDI 语境中，**timbre** 指模拟的乐器或声音质量，例如：

- piano；
- violin；
- brass；
- drums；
- synth bass。

### 17.2 Multi-timbral

一个 multi-timbral 设备可以同时播放多个不同 timbres。

例如：

```text
Channel 1 = piano
Channel 2 = strings
Channel 10 = drums
```

### 17.3 Voice

在 MIDI 中，voice 指 tone module 能同时产生的不同音高和音色组合。

如果一个设备有 24 voices，就意味着它最多能同时发出 24 个独立音符/声音。

### 17.4 Patch 与 Bank

**Patch** 是定义某种 timbre 的参数集合。比如一个 piano patch 包含音源、滤波、包络、效果等设置。

**Bank** 是 patch 的集合，相当于音色库。

---

## 18. General MIDI

General MIDI 是为了标准化 patch number 和 instrument assignment。

### 18.1 关键规则

- 有 16 个 MIDI channels；
- Channel 10 保留给 percussion；
- 有 128 个标准 instrument patches；
- percussion 使用标准 percussion map；
- 对鼓来说，note number 不代表 pitch，而代表哪种 drum。

例如在 Channel 10：

```text
note number 可能表示 kick、snare、hi-hat、cymbal 等
```

### 18.2 General MIDI 兼容要求

PPT 提到设备需要：

- 支持全部 16 channels；
- multitimbral：每个 channel 可以播放不同 instrument / program；
- polyphonic：每个 channel 可以同时播放多个 voices；
- 至少 24 dynamically allocated voices。

### 18.3 Note On 与 Note Off

一个 Note On message 包含：

```text
status byte + pitch / note number + velocity
```

随后通常会有 Note Off message，说明哪一个 note 停止。

---

## 19. ADSR envelope：音量包络

MIDI device 可以改变声音随时间的幅度变化，常用模型是 ADSR。

| 阶段 | 含义 |
|---|---|
| Attack | 按键后声音从 0 增长到峰值所需时间 |
| Decay | 从峰值下降到 sustain level 的时间 |
| Sustain | 按键保持时维持的音量水平 |
| Release | 松开按键后声音衰减到 0 的时间 |

图像上可以理解为：

```text
按键 → Attack 上升 → Decay 回落 → Sustain 保持 → 松键 → Release 衰减
```

不同乐器的 ADSR 很不一样：

- 钢琴：attack 快，release 随踏板和琴弦衰减；
- 小提琴：attack 可慢可快，sustain 明显；
- 打击乐：attack 极快，decay 快，sustain 很低或没有。

---

## 20. MIDI hardware：MIDI IN / OUT / THRU

### 20.1 MIDI ports

传统 MIDI 使用 5-pin connectors，有三个常见接口：

| Port | 作用 |
|---|---|
| MIDI IN | 接收 MIDI data |
| MIDI OUT | 发送设备自己生成的 MIDI data |
| MIDI THRU | 转发从 MIDI IN 收到的数据 |

### 20.2 Half-duplex

PPT 说 MIDI communication 是 **half-duplex**：数据可以双向流动，但不能同时双向传输。

也就是说，同一时刻设备要么发送，要么接收。

### 20.3 MIDI THRU 的重要区别

MIDI THRU 只转发从 MIDI IN 收到的数据，不发送设备自己生成的数据。

设备自己生成的数据通过 MIDI OUT 发送。

### 20.4 Practical example

设置：

1. MIDI keyboard；
2. synthesiser；
3. drum machine。

连接：

```text
Keyboard MIDI OUT → Synthesiser MIDI IN
Synthesiser MIDI THRU → Drum Machine MIDI IN
```

结果：

- keyboard 发送 MIDI data；
- synthesiser 接收并播放；
- 同样的数据通过 THRU 转发给 drum machine；
- drum machine 也可根据对应 channel 做出响应。

---

## 21. MIDI sequencer

**MIDI sequencer** 是记录、编辑和回放 MIDI data 的设备或软件。

### 21.1 常见 sequencer

软件：

- Ableton Live；
- FL Studio；
- Logic Pro；
- Cubase。

硬件：

- Akai MPC series；
- Roland MC-707。

### 21.2 Sequencer 功能

| 功能 | 说明 |
|---|---|
| Recording | 从 keyboard、drum pad、controller 捕获 MIDI messages |
| Editing | 修改 timing、pitch、duration、velocity |
| Looping & Layering | 循环 patterns，叠加多个 tracks |
| Playback & Integration | 把 MIDI data 发送到 software synth 或 hardware module |
| Automation | 控制 volume、modulation、pitch bend 等参数随时间变化 |

---

## 22. MIDI synthesiser

**MIDI synthesiser** 是使用 MIDI protocol 生成声音的乐器。

它把 MIDI data 转换成 audio signal。

### 22.1 工作流程

```text
MIDI data input → sound engine → generated sound → audio output
```

具体：

1. **MIDI Data Input**：接收来自 keyboard、drum pad、controller 的 MIDI signals。
2. **Sound Generation**：根据 MIDI 指令控制 analog 或 digital sound engine。
3. **Audio Output**：输出音频到 speakers 或 audio interface。

---

## 23. 合成器的基本模块

一个 sound synthesiser system 通常包括：

| 模块 | 作用 |
|---|---|
| Oscillator | 产生原始周期波形 |
| Filter | 改变频率内容 |
| Amplifier | 控制声音响度 |
| Envelope Generator | 控制声音随时间变化 |
| Modulator | 调制 pitch、filter、volume 等参数 |
| MIDI Interface | 接收外部控制信息 |
| Output Stage | 输出干净、合适电平的音频 |

---

## 24. Oscillator 振荡器

Oscillator 产生持续重复的信号，是合成器的原始声源。

常见波形：

| Waveform | 特点 |
|---|---|
| Sine | 最纯净，只含一个频率 |
| Square | 富含奇次谐波，声音空心、电子感强 |
| Sawtooth | 谐波丰富，声音明亮，适合 bass/lead |
| Triangle | 比 square 柔和，谐波较少 |
| Noise | 随机信号，用于 percussion、wind、effects |

Oscillator 决定：

- pitch；
- raw timbre；
- 谐波基础。

多个 oscillators 可叠加，产生更厚、更复杂的声音。

---

## 25. Filters 滤波器

Filter 改变声音的 frequency content。

常见类型：

| Filter | 作用 |
|---|---|
| Low-pass filter | 让低频通过，削弱高频 |
| High-pass filter | 让高频通过，削弱低频 |
| Band-pass filter | 只保留某一频段 |

在 subtractive synthesis 中，filter 是核心模块。比如从 sawtooth wave 开始，用 low-pass filter 去掉高频，可得到更温暖柔和的声音。

---

## 26. Amplifier 放大器

Amplifier 控制声音的 amplitude，即响度。

在合成器中，amplifier 通常和 envelope generator 一起工作：

```text
oscillator → filter → amplifier controlled by ADSR → output
```

它决定声音何时响、响多久、如何衰减。

---

## 27. Modulation effects 调制效果

Modulation 是让某个参数随时间变化。

常见调制对象：

- pitch；
- filter cutoff；
- volume；
- wavetable position；
- pan。

### 27.1 Vibrato vs Tremolo

| 效果 | 调制对象 | 听感 |
|---|---|---|
| Vibrato | pitch | 音高上下波动 |
| Tremolo | amplitude | 音量周期性忽大忽小 |

记忆：

```text
Vibrato = pitch modulation
Tremolo = amplitude modulation
```

---

## 28. Sound synthesis practical example：制作 bass sound

PPT 示例：Creating a Bass Sound。

步骤：

1. **Oscillator**：选择 sawtooth wave，因为它谐波丰富、明亮。
2. **Filter**：加 low-pass filter，去掉部分高频，让声音更温暖。
3. **Envelope**：设置 short attack、medium decay、low sustain、short release，得到 punchy bass。
4. **Modulation**：加入轻微 vibrato，提高表现力。

这说明合成器音色设计不是单一模块决定，而是多个模块组合的结果。


## 29. Types of synthesis：合成方法总览

PPT 介绍了五种合成方法：

1. Subtractive synthesis；
2. Additive synthesis；
3. Frequency Modulation synthesis；
4. Wavetable synthesis；
5. Granular synthesis。

---

## 30. Subtractive synthesis 减法合成

### 30.1 概念

Subtractive synthesis 从一个谐波丰富的波形开始，然后用 filter 去掉不需要的频率。

```text
rich waveform → filter removes frequencies → shaped sound
```

### 30.2 关键模块

| 模块 | 作用 |
|---|---|
| VCO / oscillator | 产生 saw、square、noise 等原始波形 |
| VCF / filter | 改变 harmonic content |
| VCA / amplifier | 控制 loudness |
| ADSR envelope | 控制 volume、filter cutoff 等随时间变化 |

### 30.3 例子

从 sawtooth wave 开始，使用 low-pass filter 去掉高频，得到 warm、mellow 的声音。

### 30.4 优缺点

| 优点 | 缺点 |
|---|---|
| 直观、简单、适合经典 analog sounds | timbre 复杂度有限 |

---

## 31. Additive synthesis 加法合成

### 31.1 概念

Additive synthesis 通过叠加多个 sine waves 来构建复杂声音。

它基于 Fourier synthesis：任何周期声音都可以表示为一系列正弦波之和。

```text
complex sound = sine1 + sine2 + sine3 + ...
```

### 31.2 例子

合成一个含谐波的声音：

| 成分 | 频率 |
|---|---:|
| Fundamental | 440 Hz |
| 2nd harmonic | 880 Hz |
| 3rd harmonic | 1320 Hz |

通过改变每个 sine wave 的 amplitude 和 phase，可以控制音色。

### 31.3 优缺点

| 优点 | 缺点 |
|---|---|
| 可创造非常复杂、真实的声音 | 计算量大，参数多，难以编程 |

---

## 32. Frequency Modulation synthesis：FM 合成

### 32.1 概念

FM synthesis 使用一个 oscillator 调制另一个 oscillator 的频率。

| 术语 | 含义 |
|---|---|
| Carrier oscillator | 基础频率，主要决定 pitch |
| Modulator oscillator | 改变 carrier frequency |
| Modulation index | 调制深度，决定谐波复杂度 |

简化公式可理解为：

$$
y(t)=\sin(2\pi f_c t + I\sin(2\pi f_m t))
$$

其中：

- $f_c$ 是 carrier frequency；
- $f_m$ 是 modulator frequency；
- $I$ 是 modulation index。

### 32.2 听感

FM 可产生：

- bright sounds；
- metallic sounds；
- bell-like timbres；
- electric piano；
- evolving digital textures。

### 32.3 优缺点

| 优点 | 缺点 |
|---|---|
| 能产生明亮、金属感、复杂音色 | 参数变化结果不直观，较难预测 |

---

## 33. Wavetable synthesis 波表合成

### 33.1 概念

Wavetable synthesis 使用一组预先存储的 waveforms，而不是只用简单 oscillator。

合成器可以在这些 waveforms 之间移动或插值，形成动态变化的声音。

```text
sine wave → intermediate waves → sawtooth wave
```

### 33.2 关键元素

| 元素 | 作用 |
|---|---|
| Wavetable oscillator | 从表中选择 waveform |
| Interpolation | 在波形之间平滑过渡 |
| Modulation | 用 LFO、envelope、MIDI 控制 wavetable position |

### 33.3 优缺点

| 优点 | 缺点 |
|---|---|
| 适合现代电子音乐，声音动态丰富 | 受 wavetable 质量和内容限制 |

---

## 34. Granular synthesis 颗粒合成

### 34.1 概念

Granular synthesis 把声音样本切成很多极短的 grains，然后重新排列、重叠、变速、变调。

```text
sample → grains → rearrange / overlap / stretch → new texture
```

### 34.2 关键参数

| 参数 | 含义 |
|---|---|
| Grain size | 每个 grain 的长度 |
| Playback speed | 控制 time-stretching 和 pitch |
| Randomisation | 改变 grain 位置、包络、音高等 |

### 34.3 应用

可用于：

- time-stretch；
- pitch-shift；
- ambient texture；
- glitch sound；
- experimental sound design。

### 34.4 优缺点

| 优点 | 缺点 |
|---|---|
| 极其灵活，适合实验性声音 | 如果使用不当，声音可能不自然 |

---

## 35. Synthesis methods comparison

| Type | Approach | Strengths | Weaknesses |
|---|---|---|---|
| Subtractive | 从 rich waveform 开始，用 filter 去掉频率 | 简单、直观、适合经典 analog sounds | timbre 复杂度有限 |
| Additive | 叠加多个 sine waves | 可创造复杂和真实声音 | 计算量大，难编程 |
| FM | 一个 oscillator 调制另一个 oscillator | 明亮、金属感、复杂音色 | 难控制、难预测 |
| Wavetable | 在预存波形之间 morph | 动态、现代、适合 evolving sounds | 受 wavetable 限制 |
| Granular | 把 sample 切成 grains 后重组 | 灵活、实验性强 | 可能不自然 |

---

## 36. 本节与考试的连接

### 36.1 MIDI message 解析题

考试很可能给出：

```text
0x94 0x2D 0x1E
```

要求解释结构、channel、note、velocity。

答题步骤：

1. 看第一个 byte 的高 nibble：判断 command；
2. 看第一个 byte 的低 nibble：判断 channel，注意 +1；
3. 第二个 byte 转十进制：note number；
4. 第三个 byte 转十进制：velocity。

例如：

```text
0x94 = Note On, channel nibble 4 → Channel 5
0x2D = 45
0x1E = 30
```

所以：Channel 5 上 Note On，note 45，velocity 30。

### 36.2 常考概念

| 考点 | 需要会说什么 |
|---|---|
| MIDI vs audio | MIDI 是事件指令，audio 是波形数据 |
| Status byte | 高 4 bits command，低 4 bits channel |
| Data byte | 0-127，用于 note、velocity、controller value |
| Channel messages | 针对某个 channel，如 Note On、Note Off、Program Change |
| System messages | 不针对 channel，如 clock、start、stop、SysEx |
| General MIDI | Channel 10 percussion，128 patches，16 channels |
| ADSR | Attack、Decay、Sustain、Release |
| Vibrato vs Tremolo | pitch modulation vs amplitude modulation |
| Synthesis types | subtractive、additive、FM、wavetable、granular 的区别 |

### 36.3 答题模板：解释 MIDI message

```text
The first byte is the status byte. Its upper nibble indicates the MIDI command, and its lower nibble indicates the channel. The following data bytes represent the note number and velocity. Since MIDI channels are encoded from 0 to 15, the displayed channel number is the encoded value plus one.
```

中文理解：

```text
第一个字节是状态字节。高四位表示 MIDI 命令，低四位表示通道。后面的数据字节表示音符编号和力度。由于 MIDI 通道底层按 0-15 编码，实际显示通道要加 1。
```

---

## 37. 本节关键词表

| 英文术语 | 中文理解 |
|---|---|
| MIDI | Musical Instrument Digital Interface，乐器数字接口 |
| MIDI message | MIDI 消息，表示演奏或控制事件 |
| Status byte | 状态字节，表示 command 和 channel |
| Data byte | 数据字节，表示 note、velocity、controller value 等 |
| Channel message | 针对特定 channel 的消息 |
| System message | 不针对特定 channel 的系统消息 |
| Note On | 开始播放音符 |
| Note Off | 停止播放音符 |
| Velocity | 力度，通常影响响度和音色 |
| Program Change | 切换乐器音色或 patch |
| Control Change | 控制参数，如 volume、sustain、modulation |
| Pitch Bend | 弯音控制 |
| SysEx | System Exclusive，厂商专用消息 |
| Active Sensing | 检测 MIDI 连接是否有效 |
| Timbre | 音色 |
| Voice | 可同时产生的独立声音 |
| Patch | 音色参数集合 |
| Bank | patch 集合 |
| General MIDI | 标准化 patch 和 channel 分配的规范 |
| ADSR | Attack、Decay、Sustain、Release 包络 |
| Oscillator | 振荡器，产生原始波形 |
| Filter | 滤波器，改变频率内容 |
| Amplifier | 放大器，控制响度 |
| Modulation | 调制，让参数随时间变化 |
| Vibrato | 音高调制 |
| Tremolo | 音量调制 |
| Subtractive synthesis | 减法合成 |
| Additive synthesis | 加法合成 |
| FM synthesis | 频率调制合成 |
| Wavetable synthesis | 波表合成 |
| Granular synthesis | 颗粒合成 |

---

## 38. 复习自测题

1. MIDI 和 audio 的根本区别是什么？
2. 为什么说 MIDI 是一种 scripting language？
3. 一个 MIDI message 通常由哪些 byte 构成？
4. Status byte 的高 4 bits 和低 4 bits 分别表示什么？
5. 为什么 0x90 表示 Channel 1，而不是 Channel 0？
6. 解析 `0x90 0x3C 0x64` 的 command、channel、note、velocity。
7. 写出 Channel 5 上关闭 note 62、velocity 50 的 MIDI message。
8. Channel messages 和 system messages 的区别是什么？
9. 0xF8、0xFA、0xFC、0xFE 分别是什么？
10. Active Sensing 的作用是什么？
11. General MIDI 中 Channel 10 为什么特殊？
12. Timbre、voice、patch、bank 分别是什么意思？
13. 什么是 multi-timbral？什么是 polyphonic？
14. MIDI IN、OUT、THRU 的区别是什么？
15. MIDI sequencer 的作用是什么？
16. Synthesiser 如何把 MIDI data 转换成声音？
17. Oscillator、filter、amplifier、envelope generator 分别做什么？
18. ADSR 四个阶段分别是什么？
19. Vibrato 和 tremolo 的区别是什么？
20. Subtractive synthesis 和 additive synthesis 的核心区别是什么？
21. FM synthesis 中 carrier、modulator、modulation index 分别是什么？
22. Wavetable synthesis 为什么适合 evolving sounds？
23. Granular synthesis 如何进行 time-stretch 或 texture 设计？
24. 如果考试要求比较五种 synthesis type，应从 approach、strength、weakness 三方面回答。

---

## 39. 一句话总结

本节课说明：**MIDI 负责描述“如何演奏”，synthesiser 负责生成“实际声音”**。理解 MIDI message 的字节结构可以让我们读懂 note、channel、velocity 等控制信息；理解 oscillator、filter、ADSR、modulation 和各种 synthesis methods，则可以解释电子音乐和数字声音设计是如何产生丰富音色的。

---

# Block 2 - PPT 2：Music and Speech

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
