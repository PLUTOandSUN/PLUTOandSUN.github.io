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

