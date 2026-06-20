
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
