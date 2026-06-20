---
title: EBU5408 Block 3 - PPT 1：Compression and Decompression
aliases:
  - block3
  - Block 3 PPT 1
  - Compression and Decompression
  - Digital Audio Compression
tags:
  - course/音频处理
  - EBU5408
  - digital-audio
  - block3
  - audio-compression
source:
  - "[[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/1 Compression and DecompressionFolder/Digital Audio Compression_1.pdf]]"
  - "[[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/1 Compression and DecompressionFolder/Digital Audio Compression_2.pdf]]"
  - "[[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/1 Compression and DecompressionFolder/Digital Audio Compression_3.pdf]]"
created: 2026-06-17
---

# Block 3 - PPT 1：Compression and Decompression

> [!info] 课件来源
> 本笔记对应 Block 3 第 1 组课件：
> - [[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/1 Compression and DecompressionFolder/Digital Audio Compression_1.pdf]]
> - [[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/1 Compression and DecompressionFolder/Digital Audio Compression_2.pdf]]
> - [[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/1 Compression and DecompressionFolder/Digital Audio Compression_3.pdf]]

## 0. 这组 PPT 在讲什么

这组课件围绕 **digital audio compression and decompression** 展开，核心问题是：

1. 原始数字音频为什么这么大？
2. 采样率、位深、声道数如何决定文件大小？
3. 为什么能压缩？压缩到底利用了什么？
4. **lossless** 和 **lossy** 的本质差别是什么？
5. 无损压缩怎么靠冗余变小？
6. 有损压缩怎么靠人耳听觉特性变小？

> [!summary] 一句话理解
> **无损压缩** = 不删信息，只更聪明地表示信息。  
> **有损压缩** = 删掉人耳不敏感的信息，换取更小体积。

---

## 1. 数字音频基础回顾

### 1.1 ADC：把现实声音变成数据

现实中的声音是连续的模拟信号。电脑不能直接存“连续波”，所以要先做 **ADC (Analogue-to-Digital Conversion)**：

- **Sampling**：按时间间隔取样
- **Quantisation**：把幅度四舍五入到有限等级
- **Encoding**：把数值写成二进制

可以理解为：

```text
连续声波 → 离散采样 → 幅度取整 → 二进制保存
```

### 1.2 Sampling rate：时间细节

采样率表示每秒采多少次样。

- 44.1 kHz = 每秒 44,100 次
- 48 kHz = 每秒 48,000 次

采样率越高，时间细节越多；但文件也越大。根据 Nyquist 定理，理论可捕捉的最高频率约为采样率的一半。

### 1.3 Bit depth：幅度精度

位深表示每个 sample 用多少 bit 表示。

| Bit depth | Levels | 含义 |
|---|---:|---|
| 8-bit | 256 | 粗糙，量化噪声明显 |
| 16-bit | 65,536 | CD 常用，平衡质量和大小 |
| 24-bit | 16,777,216 | 更高精度，常用于录音/混音 |

位深越高，量化误差越小，声音更细腻，但数据量更大。

### 1.4 Dynamic range：位深和动态范围

动态范围近似公式：

$$
\text{Dynamic Range} \approx 6.02 \times \text{Bit Depth}
$$

所以：

- 8-bit ≈ 48 dB
- 16-bit ≈ 96 dB
- 24-bit ≈ 144 dB

这也是为什么 16-bit 足够应付很多播放场景，而 24-bit 更适合制作流程。

### 1.5 文件大小怎么算

未压缩 PCM 音频的 bitrate：

$$
\text{Bitrate} = \text{Sampling Rate} \times \text{Bit Depth} \times \text{Channels}
$$

课件例题：48 kHz、24-bit、stereo、3 分钟。

1. bitrate：

$$
48000 \times 24 \times 2 = 2{,}304{,}000\text{ bits/s}
$$

2. 转 bytes/s：

$$
2{,}304{,}000 / 8 = 288{,}000\text{ B/s}
$$

3. 乘 180 秒：

$$
288{,}000 \times 180 = 51{,}840{,}000\text{ bytes}
$$

4. 转 MB：

$$
51.84\text{ MB}
$$

如果压缩成 128 kbps AAC：

$$
128{,}000 \times 180 / 8 \approx 2.88\text{ MB}
$$

> [!important] 这个例子说明
> 同一段音频，未压缩约 51.84 MB，压缩后约 2.88 MB，差距非常大。

---

## 2. 为什么要压缩

数字音频每秒有很多 sample，每个 sample 又有多个 bit，所以未压缩文件会很快变大。

压缩的目的通常是：

- 节省存储
- 减少网络带宽
- 适合 streaming
- 减少传输延迟
- 降低系统成本

所以 Spotify、YouTube、Teams 之类服务都离不开压缩。

---

## 3. Lossless vs Lossy

### 3.1 无损压缩

无损压缩不会丢任何音频信息。解压后和原始数据完全一致。

常见格式：

- FLAC
- ALAC

适合：归档、母带、专业制作。

### 3.2 有损压缩

有损压缩会永久丢掉部分信息，但通常丢的是人耳不容易察觉的内容。

常见格式：

- MP3
- AAC
- OGG

适合：在线播放、移动端、普通听歌。

| 对比 | 无损 | 有损 |
|---|---|---|
| 是否丢信息 | 否 | 是 |
| 解压后是否等于原始 | 是 | 否 |
| 文件大小 | 中等 | 更小 |
| 典型用途 | 归档/制作 | 流媒体/分发 |

> [!warning] 重要区分
> “解压成 WAV”不代表恢复原始音质。只要中间经历过有损编码，信息就已经丢了。

---

## 4. WAV、RIFF 与 Python 读取

### 4.1 WAV 结构

WAV 通常使用 RIFF 容器，里面主要有：

- 文件标识
- 格式信息
- 声道数
- 采样率
- byte rate
- 数据区

公式：

$$
\text{Byte Rate} = \frac{\text{Sample Rate} \times \text{Channels} \times \text{Bits per Sample}}{8}
$$

### 4.2 Python 读取思路

课件展示了一个典型做法：先读前 44 bytes 作为 header，再把后面当作音频数据。

```python
with open('Clap.wav', 'rb') as audio_file:
    audiofile_data = audio_file.read()

wav_header = audiofile_data[:44]
audio_data = audiofile_data[44:]
```

然后用 `struct.unpack` 解析 `RIFF`、文件大小、`WAVE` 等字段。

### 4.3 为什么要转成数组

原始 bytes 不适合直接做 DSP。通常会转成 NumPy array，再做：

- filtering
- transform
- feature extraction
- ML input

再做归一化：

```python
data_array = data_array / np.max(np.abs(data_array))
```

这会把幅度拉到大约 `[-1, 1]`，便于后续处理。

---

## 5. 无损压缩为什么能变小

关键是：音频里有 **redundancy（冗余）**。

### 5.1 Temporal redundancy

相邻 sample 通常很接近：

$$
x_n \approx x_{n-1}
$$

所以没必要每次都存完整值，可以只存差值。

### 5.2 Statistical redundancy

某些数值出现得特别频繁，比如：

- 0
- ±1
- 静音附近的小值

如果频繁值用短编码，整体就能变小。

---

## 6. 无损压缩流水线

典型流程：

```text
PCM samples → Predictive coding → Residuals → Entropy coding → Compressed file
```

解压时反过来：

```text
Compressed file → Entropy decoding → Residuals → Predictive inversion → PCM samples
```

### 6.1 Predictive coding

先预测当前 sample，再存误差。

最简单的一阶差分：

$$
e_n = x_n - x_{n-1}
$$

如果波形平滑，`e_n` 就很小，容易压缩。

### 6.2 LPC

LPC 用多个历史 sample 预测当前 sample：

$$
\hat{x}_n = a_1x_{n-1} + a_2x_{n-2} + \cdots + a_px_{n-p}
$$

残差：

$$
e_n = x_n - \hat{x}_n
$$

LPC 比简单差分更强，特别适合语音和有谐波结构的音乐。

### 6.3 为什么 residual 越小越好

residual 越集中在 0 附近：

- dynamic range 更低
- 熵更低
- 编码更容易
- 压缩率更高

---

## 7. Entropy coding：把常见符号编码得更短

Entropy coding 的规则很简单：

- 高频符号 → 短码
- 低频符号 → 长码

常见方法：

- Huffman coding
- Rice coding
- Arithmetic coding

### 7.1 Huffman coding（重点：怎么建树、怎么算 bit）

> [!info] 对应 PDF
> 这部分主要补充自 [[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/1 Compression and DecompressionFolder/Digital Audio Compression_2.pdf]] 中 Huffman Coding、Example Audio Compression、Exercise Huffman Coding 和 Weighted Average Formula 相关页。

Huffman coding 是一种 **variable-length prefix coding（可变长度前缀编码）**。它不是改变原始数据，而是改变“每个符号怎么用 bit 表示”。

核心规则：

- 高频符号 -> 短码
- 低频符号 -> 长码
- 所有码字必须是 **prefix-free**：没有任何一个码字是另一个码字的开头
- 解码器只要知道 Huffman tree / codebook，就能无歧义地恢复原始符号

在音频无损压缩里，Huffman 通常不是直接编码 PCM sample，而是编码预测后的 **residual（残差）**：

```text
PCM samples -> predictive coding/LPC -> residuals -> Huffman coding -> compressed bitstream
```

因为 residual 往往集中在 `0, ±1, ±2` 附近，所以这些值会得到更短的码。

> [!summary] 一句话理解
> Huffman 不删除信息，只是让“常出现的东西写得短，少出现的东西写得长”，从而降低平均 bit 数。

#### 7.1.1 手算 Huffman 的步骤

给你一张频率表时，可以按下面步骤做：

1. **列出符号和频率**：频率可以是次数，也可以是百分比/概率。
2. **按频率从小到大排序**。
3. **取最小的两个节点合并**，新节点频率 = 两者频率之和。
4. **把新节点放回列表重新排序**。
5. 重复步骤 3-4，直到只剩一个根节点，频率总和为 100% 或总次数。
6. 从根节点开始给左右分支标 `0` 和 `1`。
7. 每个符号的码字 = 从根到该叶节点经过的 0/1 序列。

> [!tip] Huffman 码不唯一
> 左分支标 `0` 还是 `1` 可以互换；频率相同的节点也可能有不同合并顺序。因此具体码字可能不同，但只要树合法，**平均码长通常相同或等价**。

#### 7.1.2 怎么计算压缩效果

如果每个符号的概率是 $p_i$，Huffman 码长是 $L_i$，平均码长为：

$$
\bar{L} = \sum_i p_i L_i
$$

如果给的是出现次数 $f_i$，总符号数为 $N$，总 bit 数为：

$$
\text{Total Huffman Bits} = \sum_i f_i L_i
$$

固定长度编码需要的 bit 数通常是：

$$
L_{fixed} = \lceil \log_2 M \rceil
$$

其中 $M$ 是不同符号的数量。

压缩效率/节省比例：

$$
\text{Saving} = \frac{\text{Fixed Bits} - \text{Huffman Bits}}{\text{Fixed Bits}} \times 100\%
$$

也可以用平均 bit 数写成：

$$
\text{Saving} = \frac{L_{fixed} - \bar{L}}{L_{fixed}} \times 100\%
$$

> [!warning] 注意 baseline
> - 如果题目说“原本用 ASCII”，baseline 通常是 `8 bits/符号`。
> - 如果题目只给了 $M$ 个可能符号，baseline 通常是 $\lceil \log_2 M \rceil$ bits/符号。
> - 真实文件还要存 codebook/tree/header，课堂小题通常先忽略这些额外开销。

#### 7.1.3 例题 1：文字压缩 `AAAAAAABBBCC`

课件例子：

| Symbol | Frequency | Huffman code | Code length |
|---|---:|---:|---:|
| A | 7 | `0` | 1 |
| B | 3 | `10` | 2 |
| C | 2 | `11` | 2 |

原字符串：

```text
AAAAAAA BBB CC
```

编码后：

```text
A A A A A A A B  B  B  C  C
0 0 0 0 0 0 0 10 10 10 11 11
```

拼接为：

```text
00000001010101111
```

**Before：如果用 8-bit ASCII**

$$
7\times8 + 3\times8 + 2\times8 = 96\text{ bits}
$$

**After：Huffman 编码**

$$
7\times1 + 3\times2 + 2\times2 = 17\text{ bits}
$$

平均每个字母：

$$
17 / 12 \approx 1.42\text{ bits/symbol}
$$

节省比例：

$$
\frac{96-17}{96}\times100\% \approx 82.3\%
$$

> [!note] 如果不用 ASCII 作 baseline
> 这个例子只有 3 种符号，固定长度最少需要 $\lceil \log_2 3 \rceil = 2$ bits/符号，即 $12\times2=24$ bits。Huffman 的 17 bits 仍然更短。

#### 7.1.4 例题 2：音频 residual 的 Huffman 编码

课件给出 residual 的频率：

| Residual | Frequency | Huffman code | Length |
|---:|---:|---:|---:|
| 0 | 40% | `0` | 1 |
| 1 | 25% | `10` | 2 |
| -1 | 20% | `110` | 3 |
| 2 | 10% | `1110` | 4 |
| -2 | 5% | `1111` | 4 |

对应的树可以理解为：

```text
(100%)
├─ 0 -> residual 0 (40%)
└─ 1 -> (60%)
   ├─ 0 -> residual 1 (25%)
   └─ 1 -> (35%)
      ├─ 0 -> residual -1 (20%)
      └─ 1 -> (15%)
         ├─ 0 -> residual 2 (10%)
         └─ 1 -> residual -2 (5%)
```

所以：

```text
0   -> 0
1   -> 10
-1  -> 110
2   -> 1110
-2  -> 1111
```

平均码长：

$$
\bar{L}=0.40\times1+0.25\times2+0.20\times3+0.10\times4+0.05\times4
$$

$$
\bar{L}=0.40+0.50+0.60+0.40+0.20=2.10\text{ bits/residual}
$$

因为一共有 5 种 residual，固定长度编码需要：

$$
\lceil \log_2 5 \rceil = 3\text{ bits/residual}
$$

节省比例：

$$
\frac{3-2.10}{3}\times100\%=30\%
$$

也就是说，在忽略 codebook/header 的课堂模型下，Huffman 把平均 bit 数从 `3 bits/residual` 降到约 `2.10 bits/residual`。

##### 对一个 residual 序列实际编码

原 residual：

```text
0 0 0 1 0 -1 0 2 -2
```

固定长度编码：9 个 residual，每个 3 bits：

$$
9\times3=27\text{ bits}
$$

Huffman 编码：

```text
0 | 0 | 0 | 10 | 0 | 110 | 0 | 1110 | 1111
```

逐项数 bit：

$$
1+1+1+2+1+3+1+4+4=18\text{ bits}
$$

节省：

$$
\frac{27-18}{27}\times100\%\approx33.3\%
$$

> [!warning] 课件数值检查
> 课件这一页把该序列写成 `16 bits`，但按同页给出的码表逐项相加应为 `18 bits`。考试或作业中最稳妥的写法是把每个码字长度列出来再求和。

#### 7.1.5 例题 3：课件练习题完整计算

题目给出预测 residual 的分布：

| Residual value | Frequency |
|---:|---:|
| -5 | 7% |
| 5 | 11% |
| 2 | 20% |
| 0 | 40% |
| -2 | 22% |

**Step 1：从小到大排序**

```text
-5(7), 5(11), 2(20), -2(22), 0(40)
```

**Step 2：每次合并最小的两个**

```text
-5(7) + 5(11) = 18
18 + 2(20) = 38
38 + -2(22) = 60
60 + 0(40) = 100
```

**Step 3：按课件的 0/1 分支得到码表**

| Residual | Code | Length |
|---:|---:|---:|
| 0 | `0` | 1 |
| -2 | `10` | 2 |
| 2 | `110` | 3 |
| -5 | `1110` | 4 |
| 5 | `1111` | 4 |

**Step 4：算平均 bit 数**

$$
\bar{L}=0.40\times1+0.22\times2+0.20\times3+0.07\times4+0.11\times4
$$

$$
\bar{L}=0.40+0.44+0.60+0.28+0.44=2.16\text{ bits/residual}
$$

**Step 5：和固定长度比较**

5 个 residual 值，固定长度需要：

$$
\lceil\log_2 5\rceil=3\text{ bits/residual}
$$

节省比例：

$$
\frac{3-2.16}{3}\times100\%=28\%
$$

如果有 10,000 个 residual：

- 固定长度：$10{,}000\times3=30{,}000$ bits
- Huffman：$10{,}000\times2.16=21{,}600$ bits
- 节省：$8{,}400$ bits

> [!success] 结论
> 最高频的 `0(40%)` 只用 1 bit；最低频的 `-5(7%)` 和 `5(11%)` 用 4 bits。这样整体平均码长低于固定长度编码。

#### 7.1.6 解码怎么做

Huffman 解码是沿着树读 bit：

1. 从根节点开始。
2. 读到 `0` 走 0 分支，读到 `1` 走 1 分支。
3. 一旦到达叶节点，就输出该 residual。
4. 回到根节点继续读后面的 bit。

例如使用上面的码表：

```text
0 -> 0
10 -> 1
110 -> -1
1110 -> 2
1111 -> -2
```

bitstream：

```text
000100110011101111
```

可以切成：

```text
0 | 0 | 0 | 10 | 0 | 110 | 0 | 1110 | 1111
```

解码回：

```text
0 0 0 1 0 -1 0 2 -2
```

之所以能这样切，是因为 Huffman 码是 prefix-free。例如 `0` 是一个完整码字，所以不会再出现以 `0...` 开头的其他更长码字。

#### 7.1.7 和音频压缩的关系

Huffman 在音频里通常和 predictive coding 一起工作：

```text
原始 sample:       x_n
预测 sample:       x_hat_n
residual:          e_n = x_n - x_hat_n
entropy coding:    对 e_n 做 Huffman/Rice/Arithmetic coding
```

如果预测器很好，大多数 residual 会接近 0：

```text
0, 0, 1, 0, -1, 0, 0, 2, 0, ...
```

这正适合 Huffman：

- `0` 出现最多 -> 最短码
- `±1` 次之 -> 较短码
- 大 residual 很少出现 -> 较长码

解压时流程反过来：

```text
Huffman decoding -> residuals -> predictive inversion -> original PCM samples
```

只要码表和预测参数保存正确，恢复出的 PCM samples 和原始数据完全一致，所以这是 **lossless compression**。

#### 7.1.8 做题时最容易错的点

- 把百分比当成整数：`40%` 要用 `0.40` 参与平均码长计算。
- 忘记固定长度 baseline：5 种符号不是 5 bits，而是 $\lceil\log_2 5\rceil=3$ bits。
- 只写码表不算平均码长：题目通常还要问 compression efficiency。
- 看到不同答案就以为错了：Huffman 的左右 0/1 可以互换，码字可能不同，重点看码长和平均 bit 数。
- 忘记说明 codebook：真实压缩文件需要让解码器知道 Huffman tree/codebook。

### 7.2 Rice coding

Rice coding 特别适合 residual 集中在 0 附近的数据，也是 FLAC/ALAC 常见方案之一。

### 7.3 Arithmetic coding（重点：区间编码、怎么计算）

> [!info] 对应 PDF
> 这部分主要补充自 [[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/1 Compression and DecompressionFolder/Digital Audio Compression_2.pdf]] 中 Other Coding、Arithmetic Coding、Example Text/Audio Compression、Advantages of Arithmetic Coding 相关页。

Arithmetic coding 也是一种 **entropy coding**，可以看作 Huffman coding 的替代方案。它的核心思想不是“给每个符号单独分配一个码字”，而是：

> [!summary] 一句话理解
> Arithmetic coding 把**整段符号序列**编码成 $[0,1)$ 区间里的**一个小数**；序列越长、越不常见，最终区间越窄，需要的 bit 越多。

它可以用于：

- **lossless audio**：编码 predictive coding 后的 residuals
- **lossy audio**：编码 quantization 后的频域系数
- text/image/video 等其他非均匀分布数据

和 Huffman 的区别：

| 对比 | Huffman coding | Arithmetic coding |
|---|---|---|
| 编码单位 | 每个符号一个码字 | 整个序列一个区间/小数 |
| 每个符号码长 | 必须是整数 bit | 平均上可以接近“小数 bit” |
| 理论效率 | 接近 entropy，但受整数码长限制 | 通常更接近 Shannon entropy |
| 实现复杂度 | 较简单 | 较复杂，需要区间缩放/高精度处理 |
| 解码条件 | 需要 Huffman tree/codebook | 需要概率模型和最终编码值 |

#### 7.3.1 Arithmetic coding 的基本流程

假设符号集合为 $S=\{s_1,s_2,\ldots,s_M\}$，每个符号概率为 $p_i$。

第一步：概率必须满足：

$$
\sum_i p_i = 1
$$

第二步：把 $[0,1)$ 按概率切成若干子区间。例如：

```text
A: [0.00, 0.50)
B: [0.50, 0.80)
C: [0.80, 1.00)
```

第三步：从初始区间 $[low, high) = [0,1)$ 开始，每读一个符号，就把当前区间缩小到该符号对应的子区间。

如果当前区间宽度是：

$$
range = high - low
$$

某符号的累积分布区间是 $[c_{low}, c_{high})$，则更新为：

$$
new\_low = low + range \times c_{low}
$$

$$
new\_high = low + range \times c_{high}
$$

最后，只要选择最终区间里的任意一个二进制小数，就可以代表整段序列。

#### 7.3.2 小例子：把 `ABC` 编码成一个区间

为了看清步骤，先用一个简单概率模型：

| Symbol | Probability | Cumulative interval |
|---|---:|---:|
| A | 0.50 | `[0.00, 0.50)` |
| B | 0.30 | `[0.50, 0.80)` |
| C | 0.20 | `[0.80, 1.00)` |

要编码：

```text
ABC
```

**Step 0：初始区间**

$$
[0,1)
$$

**Step 1：读到 A**

A 对应 `[0.00, 0.50)`，所以新区间为：

$$
[0, 0.5)
$$

**Step 2：读到 B**

当前区间宽度：

$$
range = 0.5 - 0 = 0.5
$$

B 的累积区间是 `[0.50, 0.80)`：

$$
new\_low = 0 + 0.5\times0.50 = 0.25
$$

$$
new\_high = 0 + 0.5\times0.80 = 0.40
$$

所以区间变成：

$$
[0.25,0.40)
$$

**Step 3：读到 C**

当前区间宽度：

$$
range = 0.40 - 0.25 = 0.15
$$

C 的累积区间是 `[0.80, 1.00)`：

$$
new\_low = 0.25 + 0.15\times0.80 = 0.37
$$

$$
new\_high = 0.25 + 0.15\times1.00 = 0.40
$$

最终区间：

$$
[0.37,0.40)
$$

所以任何在这个区间里的小数，比如 `0.38`，都可以代表序列 `ABC`。

> [!note] 为什么一个小数能代表整个序列？
> 因为解码器知道同一套概率区间。它看到 `0.38` 后，会发现它先落在 A 的区间；把区间缩放后，又落在 B 的区间；再缩放后落在 C 的区间。这样就能一步步还原原序列。

#### 7.3.3 PDF 文字例子：`AAAAAAABBBCC`

课件给出的字符串：

```text
AAAAAAABBBCC
```

频率：

| Symbol | Frequency | Probability |
|---|---:|---:|
| A | 7 | $7/12 \approx 0.5833$ |
| B | 3 | $3/12 = 0.25$ |
| C | 2 | $2/12 \approx 0.1667$ |

累计区间可以设为：

| Symbol | Cumulative interval |
|---|---:|
| A | $[0,7/12)$ |
| B | $[7/12,10/12)$ |
| C | $[10/12,1)$ |

如果编码整段 `AAAAAAABBBCC`，最终区间宽度等于每个符号概率的乘积：

$$
width = \left(\frac{7}{12}\right)^7
\left(\frac{3}{12}\right)^3
\left(\frac{2}{12}\right)^2
$$

需要的 bit 数大约是：

$$
-\log_2(width) \approx 16.61\text{ bits}
$$

实际编码时 bit 数必须取整数，因此大约需要 17 bits（还未计入概率表/模型开销）。这和前面 Huffman 例子的 17 bits 非常接近，也远少于 8-bit ASCII 的 96 bits。

> [!tip] 重点
> Arithmetic coding 的优势不是每个小例子都一定比 Huffman 少很多，而是在长序列和复杂概率分布下，它通常能更接近 Shannon entropy。

#### 7.3.4 PDF 音频例子：residual 概率怎么进入 arithmetic coding

课件给出的 residual 频率可以换成概率：

| Residual | Frequency | Probability | Cumulative interval |
|---:|---:|---:|---:|
| 0 | 400 | 0.40 | `[0.00, 0.40)` |
| 1 | 250 | 0.25 | `[0.40, 0.65)` |
| -1 | 200 | 0.20 | `[0.65, 0.85)` |
| 2 | 100 | 0.10 | `[0.85, 0.95)` |
| -2 | 50 | 0.05 | `[0.95, 1.00)` |

概率检查：

$$
0.40+0.25+0.20+0.10+0.05=1.00
$$

这说明区间刚好覆盖 `[0,1)`。

如果 residual 序列开头是：

```text
0, 1, -1
```

编码过程：

1. 初始区间 `[0,1)`。
2. 读到 `0`，进入 `[0.00,0.40)`。
3. 读到 `1`：当前 range = 0.40，`1` 的累积区间是 `[0.40,0.65)`：

$$
new\_low=0+0.40\times0.40=0.16
$$

$$
new\_high=0+0.40\times0.65=0.26
$$

所以区间变成 `[0.16,0.26)`。

4. 读到 `-1`：当前 range = 0.10，`-1` 的累积区间是 `[0.65,0.85)`：

$$
new\_low=0.16+0.10\times0.65=0.225
$$

$$
new\_high=0.16+0.10\times0.85=0.245
$$

最终区间为：

$$
[0.225,0.245)
$$

任取其中一个小数，例如 `0.23`，就可以代表 `0, 1, -1` 这三个 residual。

#### 7.3.5 Arithmetic coding 的 bit 数怎么算

最终区间越窄，需要越多 bit 才能唯一落在该区间中。近似公式：

$$
\text{bits} \approx \lceil -\log_2(width) \rceil
$$

而最终区间宽度大约等于序列中每个符号概率的乘积：

$$
width = \prod_{k=1}^{N} p(x_k)
$$

所以：

$$
-\log_2(width)
= -\log_2\left(\prod_{k=1}^{N} p(x_k)\right)
= \sum_{k=1}^{N} -\log_2 p(x_k)
$$

这就是 Arithmetic coding 和 Shannon entropy 的连接：

- 高频符号概率大，$-\log_2 p$ 小，贡献 bit 少
- 低频符号概率小，$-\log_2 p$ 大，贡献 bit 多
- 长期平均下来，平均 bit 数会接近 entropy

#### 7.3.6 为什么 Arithmetic coding 常比 Huffman 更接近理论极限

Huffman 的每个符号码长必须是整数：1 bit、2 bits、3 bits……

但理想信息量可能是小数 bit。例如概率为 0.40 的符号，理论信息量是：

$$
-\log_2(0.40) \approx 1.32\text{ bits}
$$

Huffman 不能给它 `1.32 bits` 的单个码字，只能给 1 bit 或 2 bits。Arithmetic coding 不需要给每个符号单独整数码字，而是对整段序列统一编码，因此长期平均可以更接近这些“小数 bit”。

> [!important] 这就是课件说的 fractional bit efficiency
> Arithmetic coding 不是让单个 bit 变成小数，而是通过“整段序列一起编码”，让**平均每个符号的 bit 数**可以接近小数。

#### 7.3.7 优点和缺点

优点：

- 对非均匀分布很有效，频率越偏斜越有压缩空间。
- 更接近 Shannon entropy，通常比固定长度编码更省 bit。
- 适合 residual 这种集中在 0 附近的数据。
- 可用于 lossless residual，也可用于 lossy codec 中量化后的系数。

缺点：

- 实现比 Huffman 更复杂。
- 需要精确维护概率模型和区间。
- 实际系统要处理有限精度、归一化、溢出和模型传输问题。
- 对很短的数据，模型/header 开销可能抵消收益。

### 7.4 Shannon entropy（重点：理论下限、怎么算）

> [!info] 对应 PDF
> 这部分主要补充自 [[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/1 Compression and DecompressionFolder/Digital Audio Compression_2.pdf]] 中 Shannon Entropy 页。

Shannon entropy 衡量一个数据源平均有多少“不确定性”或“信息量”。它回答的问题是：

> 平均来说，表示这个数据源的一个符号，理论上至少需要多少 bit？

熵越高：

- 数据越随机
- 越难预测
- 越难压缩
- 需要的平均 bit 数越多

熵越低：

- 数据越可预测
- 分布越集中
- 越容易压缩
- 需要的平均 bit 数越少

#### 7.4.1 单个符号的信息量

一个符号 $x$ 的信息量定义为：

$$
I(x) = -\log_2 p(x)
$$

含义：

- $p(x)$ 越大，符号越常见，信息量越小
- $p(x)$ 越小，符号越罕见，信息量越大

例子：

$$
I(p=0.5)=-\log_2(0.5)=1\text{ bit}
$$

$$
I(p=0.25)=-\log_2(0.25)=2\text{ bits}
$$

$$
I(p=0.0625)=-\log_2(0.0625)=4\text{ bits}
$$

> [!summary] 越少见的事件，发生时带来的“惊讶”越大，所以信息量越高。

#### 7.4.2 Shannon entropy 公式

对一组符号 $x_i$，概率为 $p_i$，熵为：

$$
H(X) = -\sum_i p_i\log_2(p_i)
$$

也可以写成：

$$
H(X)=\sum_i p_i I(x_i)
$$

单位是：

```text
bits/symbol
```

也就是平均每个符号理论上至少需要多少 bit。

#### 7.4.3 计算步骤

做题时按这 4 步：

1. 把频率换成概率。
2. 检查概率总和是否为 1。
3. 对每个符号计算 $-p_i\log_2(p_i)$。
4. 把所有项相加。

> [!warning] 常见错误
> 如果题目给的是百分比，必须先转成小数。例如 `40%` 要写成 `0.40`。

#### 7.4.4 例题 1：文字 `AAAAAAABBBCC` 的 entropy

频率和概率：

| Symbol | Frequency | Probability |
|---|---:|---:|
| A | 7 | $7/12$ |
| B | 3 | $3/12$ |
| C | 2 | $2/12$ |

熵：

$$
H = -\frac{7}{12}\log_2\frac{7}{12}
-\frac{3}{12}\log_2\frac{3}{12}
-\frac{2}{12}\log_2\frac{2}{12}
$$

计算结果：

$$
H \approx 1.384\text{ bits/symbol}
$$

这段文本共有 12 个符号，所以理论最少 bit 数约为：

$$
12\times1.384\approx16.61\text{ bits}
$$

前面 Huffman 编码是 17 bits，已经非常接近理论下限；Arithmetic coding 也大约可以接近 17 bits。

#### 7.4.5 例题 2：音频 residual 分布的 entropy

课件 residual 分布：

| Residual | Probability | $-p\log_2p$ |
|---:|---:|---:|
| 0 | 0.40 | 0.5288 |
| 1 | 0.25 | 0.5000 |
| -1 | 0.20 | 0.4644 |
| 2 | 0.10 | 0.3322 |
| -2 | 0.05 | 0.2161 |

熵：

$$
H=0.5288+0.5000+0.4644+0.3322+0.2161
$$

$$
H\approx2.0415\text{ bits/residual}
$$

解释：

- 这个 residual 数据源理论上平均至少需要约 `2.04 bits/residual`。
- 前面 Huffman 平均码长约 `2.10 bits/residual`。
- 固定长度编码因为有 5 种 residual，需要 $\lceil\log_2 5\rceil=3$ bits/residual。

所以理论最大节省比例约为：

$$
\frac{3-2.0415}{3}\times100\%\approx31.95\%
$$

Huffman 的节省比例约为 30%，已经比较接近理论极限；Arithmetic coding 在长序列上通常还能更贴近 $2.0415$。

#### 7.4.6 例题 3：课件练习 residual 分布的 entropy

练习题分布：

| Residual | Probability | $-p\log_2p$ |
|---:|---:|---:|
| 0 | 0.40 | 0.5288 |
| -2 | 0.22 | 0.4806 |
| 2 | 0.20 | 0.4644 |
| -5 | 0.07 | 0.2686 |
| 5 | 0.11 | 0.3503 |

$$
H\approx0.5288+0.4806+0.4644+0.2686+0.3503
$$

$$
H\approx2.0926\text{ bits/residual}
$$

前面按课件码表算出的 Huffman 平均码长是：

$$
\bar{L}=2.16\text{ bits/residual}
$$

因此：

```text
Entropy lower bound: 约 2.09 bits/residual
Huffman average:     约 2.16 bits/residual
Fixed length:        3 bits/residual
```

这说明 Huffman 已经明显优于固定长度编码，但仍略高于 Shannon entropy。

#### 7.4.7 Entropy 的几个极端情况

**情况 1：完全可预测**

如果某个符号概率为 1：

```text
P(0)=1.0
```

那么：

$$
H=-1\times\log_2(1)=0
$$

说明没有不确定性，理论上不需要额外 bit 来区分符号。

**情况 2：均匀分布**

如果有 $M$ 个符号，而且每个符号概率都一样：

$$
p_i=\frac{1}{M}
$$

那么最大熵为：

$$
H_{max}=\log_2 M
$$

例如 5 个符号均匀出现：

$$
H_{max}=\log_2 5\approx2.322\text{ bits/symbol}
$$

均匀分布更随机，压缩空间比“0 特别多、其他很少”的分布小。

#### 7.4.8 Entropy 和音频压缩的关系

在无损音频压缩中，predictive coding 的目标可以理解为：

```text
让 residual 的分布更集中 -> 降低 entropy -> entropy coding 更省 bit
```

如果原始 sample 很难预测，residual 接近随机，entropy 高，Huffman/Rice/Arithmetic 都很难压缩。

如果预测器很好，residual 大量集中在 0 附近，entropy 低，就能明显压缩。

这也是为什么无损压缩流水线通常是：

```text
Predictive coding -> lower-entropy residuals -> entropy coding
```

#### 7.4.9 Shannon entropy、Huffman、Arithmetic 的关系

可以把三者关系记成：

```text
Shannon entropy = 理论下限
Huffman coding  = 简单实用，平均码长接近下限，但受整数码长限制
Arithmetic coding = 更复杂，通常更接近下限
```

更数学一点：

$$
H(X) \leq \text{Average code length}
$$

对 Huffman 来说，平均码长通常满足：

$$
H(X) \leq \bar{L}_{Huffman} < H(X)+1
$$

Arithmetic coding 对长序列通常可以比 Huffman 更接近 $H(X)$。

> [!important] 最重要的考试句
> Entropy is the theoretical minimum average number of bits per symbol for lossless compression. Compression algorithms try to get as close as possible to this limit.

---

## 8. 有损压缩：以 MP3 为例

有损压缩的核心不是“随便删”，而是 **按照人耳感知特性去删**。

MP3 典型流程：

```text
Frame splitting & windowing
→ MDCT
→ Psychoacoustic modelling
→ Quantisation & bit allocation
→ Entropy coding
→ Bitstream formatting
```

真正引入不可逆损失的主要阶段是：**quantisation**。

### 8.1 Frame splitting 和 windowing

音频先切成短帧，一般约 20-30 ms。这样短时间内信号更接近平稳。

如果直接硬切，会有边界突变，所以要加 window，例如 Hann window。

再用 overlap-add 把相邻帧平滑拼回去。

### 8.2 MDCT

> [!info] 对应 PDF
> 这一小节主要对应 [[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/1 Compression and DecompressionFolder/Digital Audio Compression_3.pdf#page=11|Digital Audio Compression_3.pdf 第 11-16 页]]，以及后面量化部分第 26、28、33、34 页中关于 MDCT 系数如何继续被心理声学模型和量化使用的内容。

MDCT 全称是 **Modified Discrete Cosine Transform（改进离散余弦变换）**。在 MP3 这类有损音频压缩里，它负责把一小段 **time-domain samples（时域采样点）** 转换成一组 **frequency-domain coefficients（频域系数）**。

可以把它理解成：

```text
一小段波形 samples
→ 加窗、与相邻帧重叠
→ MDCT
→ 一组表示不同频带能量的系数
```

也就是说，MDCT 并不是直接“压缩文件”的步骤，而是先把音频换到一个更适合压缩和听觉建模的表示空间。后面的 psychoacoustic modelling、quantisation、bit allocation 都是在 MDCT 系数的基础上做决策。

#### 8.2.1 MDCT 输入和输出是什么

输入是经过 **frame splitting + windowing** 的一帧音频。课件里强调 MP3 会先把音频切成短帧，一般约 20-30 ms，并且相邻帧会 overlap。原因是：

- 很长的真实音频通常是非平稳的；
- 但在很短时间内，可以近似看成 quasi-stationary；
- overlap 可以避免帧边界硬切带来的不连续。

MDCT 输出的是一串系数：

```text
X[0], X[1], X[2], ..., X[k]
```

其中每个 $X[k]$ 可以理解为某个频率 bin / frequency sub-band 上的能量或强度。系数越大，说明该频带在这一帧里越重要；系数越接近 0，说明该频带贡献较小，后续更容易被粗量化甚至丢弃。

课件给出的定义形式是：

$$
X[k] =
\sum_{n=0}^{N-1}
x[n]\cos\left[
\frac{\pi}{N}
\left(n+\frac{1}{2}+\frac{N}{2}\right)
\left(k+\frac{1}{2}\right)
\right]
$$

其中：

| 符号 | 含义 |
|---|---|
| $x[n]$ | 时域音频采样点 |
| $X[k]$ | 第 $k$ 个频域系数 |
| $N$ | window length / frame length |
| $k$ | frequency bin index |

> [!note] 公式记号说明
> 不同教材会把 MDCT 的长度记号写得不一样。常见写法是把 `2N` 个重叠输入样本变成 `N` 个系数；本课件用 $N$ 表示 window length。复习时不必纠结符号差异，重点记住：**MDCT 是对加窗、重叠帧做余弦变换，并输出可用于压缩的频带系数。**

不用死背公式，更重要的是理解它在做什么：**用一组余弦基函数去“解释”这一帧波形，然后记录每个余弦成分需要多少权重。**

#### 8.2.2 为什么要从时域转到频域

在时域里，音频是一串 sample：

```text
x[0], x[1], x[2], x[3], ...
```

它适合播放，却不适合回答这些压缩问题：

- 哪些频率成分最强？
- 哪些频率成分很弱？
- 哪些成分会被人耳听见？
- 哪些成分会被其他强声音 mask 掉？
- 哪些地方可以少分配 bit？

转到频域后，这些问题就容易得多。因为人耳的感知本来就和频率密切相关：我们会谈低频、中频、高频，会谈某个频率附近的 masking threshold。MDCT 把每帧拆成频带系数，使编码器可以按频带做心理声学分析和 bit allocation。

> [!summary] 一句话理解
> **时域波形适合播放，频域系数适合压缩决策。** MDCT 的作用就是把“波形长什么样”转换成“各个频带有多少能量”。

#### 8.2.3 Energy compaction：为什么 MDCT 有利于压缩

课件反复强调 MDCT 的一个好处是 **energy compaction（能量集中）**：

- 音乐和语音的能量通常不会平均分散在所有频率上；
- 做 MDCT 后，能量往往集中在少数几个较大的系数上；
- 很多其他系数会变得很小，甚至接近 0。

这对压缩非常关键。假设一帧有很多 MDCT 系数：

```text
大系数：真正重要，需要较多 bit 保留
小系数：贡献很弱，可以少给 bit、粗量化，甚至置零
```

所以 MDCT 本身还没有丢信息，但它让“哪些信息重要、哪些信息不重要”变得更明显。后面的 quantisation 才真正引入损失。

课件程序观察也对应这个结论：

- **After MDCT**：energy is concentrated in a few coefficients；most values are close to zero。
- **After psychoacoustic modelling**：低能量或被掩蔽的成分会被移除。
- **After quantization**：系数被 round，数值精度下降，信号变得近似。

#### 8.2.4 为什么 MDCT 要 overlap

如果把音频直接硬切成一帧一帧，再分别做变换，会在帧边界产生 discontinuities。听感上可能表现为：

- blocking artifacts；
- click / pop；
- 帧与帧之间不平滑；
- 重建后波形在边界处突变。

MDCT 的特点是 **lapped transform（重叠变换）**。它不是把每一帧孤立处理，而是处理加窗后的重叠帧。典型流程是：

```text
frame 1: samples 0      ... N-1
frame 2: samples N/2    ... 3N/2-1
frame 3: samples N      ... 2N-1
```

也就是相邻帧通常有 50% overlap。这样做的好处是：

- window 会让帧边缘逐渐变小，减少硬切；
- inverse MDCT 后可以 overlap-add；
- 相邻帧在重叠区域互相补偿；
- 重建波形更连续，blocking artifacts 更少。

> [!important] MDCT 与普通 frame-by-frame DCT 的关键区别
> 普通 DCT 通常是一帧一帧独立处理，不天然解决帧边界不连续；MDCT 的设计目标就是配合 overlap-add，让分帧处理后仍然可以平滑重建。

#### 8.2.5 为什么不用 FFT 或普通 DCT

课件用 “Why Use MDCT Instead of FFT or DCT?” 对比了三者。核心区别可以这样记：

| 方法 | 特点 | 对压缩的影响 |
|---|---|---|
| FFT | 使用复指数，输出幅度和相位；常用于频谱分析 | 信息表示更通用，但对 MP3 这种感知编码不如 MDCT 直接 |
| DCT | 只用 cosine basis，能量集中能力好 | 如果逐帧独立使用，仍容易有 frame boundary discontinuities |
| MDCT | cosine basis + overlapping / lapped transform | 既有能量集中，又能减少 blocking artifacts，适合 MP3 |

MDCT 可以看成“更适合音频编码的 DCT 变体”。它保留了 DCT 的能量集中优势，同时通过 overlap 处理帧边界。

#### 8.2.6 MDCT 和心理声学模型的关系

MDCT 输出的频域系数会进入 psychoacoustic modelling。心理声学模型会根据人耳特性判断：

- 哪些频率成分本身低于绝对听阈 ATH；
- 哪些弱成分被附近强成分 frequency masking；
- 哪些短时间内的弱声音被 temporal masking；
- 每个频带最多能容忍多少 quantisation noise。

这一步会产生类似 masking threshold 的判断。然后编码器用它指导 bit allocation：

```text
重要、容易听见的 MDCT 系数
→ 分配更多 bit
→ finer quantisation
→ 更低量化噪声

不重要、被掩蔽的 MDCT 系数
→ 分配更少 bit
→ coarser quantisation
→ 更高但听不明显的量化噪声
```

所以 MDCT 的频带表示是心理声学模型能发挥作用的前提。没有频域系数，编码器很难精确判断“这个频率附近的误差会不会被听见”。

#### 8.2.7 MDCT 在 MP3 pipeline 中的位置

把课件 pipeline 连起来看：

```text
Audio input
→ Frame splitting
→ Windowing
→ MDCT
→ Psychoacoustic model
→ Quantisation & bit allocation
→ Entropy coding
→ Bitstream formatting
→ Compressed output
```

其中：

- **MDCT**：把时域帧变成频域系数，本身主要是表示方式改变；
- **Psychoacoustic model**：决定哪些频带重要、哪些误差可被 mask；
- **Quantisation**：把连续系数映射到有限等级，真正引入 lossy approximation；
- **Entropy coding**：把量化后的符号进一步用较少 bit 表示。

> [!warning] 不要把 MDCT 和量化混在一起
> MDCT 只是变换域表示，理论上配合 inverse MDCT 和正确 overlap-add 可以重建；MP3 真正不可逆的主要损失来自后面的 **quantisation**，不是 MDCT 这个变换本身。

#### 8.2.8 考试/复习时的答题模板

如果题目问 “Why is MDCT used in MP3/audio compression?”，可以按下面结构答：

1. MDCT converts windowed time-domain frames into frequency-domain coefficients.
2. It uses overlapping/lapped frames, so inverse transform with overlap-add reduces blocking artifacts.
3. It provides energy compaction: most signal energy is concentrated in a small number of significant coefficients.
4. Many coefficients become small, so they can be coarsely quantized or discarded.
5. Its frequency-domain output matches psychoacoustic modelling, allowing bit allocation according to masking thresholds.
6. Therefore MDCT makes perceptual audio compression more efficient while keeping reconstruction smooth.

### 8.3 Psychoacoustic modelling

人耳并不是对所有频率都一样敏感。

核心概念：

- **ATH**：绝对听阈
- **frequency masking**：强声音会遮住附近弱声音
- **temporal masking**：强声音会遮住前后很短时间内的弱声音

所以编码器会算一个 masking threshold，然后尽量让量化噪声低于它。

### 8.4 Quantisation & bit allocation

这一步会把系数映射到有限等级。

- 更重要、耳朵更敏感的频段 → 更多 bit
- 被掩蔽的频段 → 更少 bit

也就是说，编码器不是平均分配 bit，而是“把 bit 花在耳朵更在意的地方”。

### 8.5 Bitstream formatting

最后把：

- header
- side information
- Huffman-coded data

打包成标准 MP3 bitstream，供解码器还原播放。

---

## 9. 这组课最值得记的 10 句话

1. ADC = sampling + quantisation + encoding
2. Sampling rate 决定时间细节和可表示的最高频率
3. Bit depth 决定幅度精度和动态范围
4. 未压缩音频文件大，是因为 sample 太多、每个 sample 又占 bit
5. 无损压缩利用冗余，不丢信息
6. 有损压缩利用人耳听不见或不敏感的信息
7. Predictive coding 先把相邻 sample 的相似性变成 residual
8. Entropy coding 让高频 residual 用短码
9. MP3 中真正不可逆的损失主要来自 quantisation
10. Psychoacoustics 决定哪些误差可以“藏”在人耳听不到的地方

---

## 10. 复习题

- ADC 具体做了哪三步？
- 为什么 16-bit 常比 8-bit 更常用？
- 48 kHz、24-bit、stereo、3 分钟音频有多大？
- 为什么 FLAC 是无损，而 MP3 是有损？
- predictive coding 为什么能压缩？
- Huffman 为什么能缩短平均编码长度？
- 给出 residual 频率表时，如何一步步合并节点建立 Huffman tree？
- 如何用 $\bar{L}=\sum p_iL_i$ 计算平均 bits/symbol？
- 固定长度编码和 Huffman 编码的压缩效率怎么算？
- 为什么 Huffman 码必须是 prefix-free？
- Arithmetic coding 为什么可以把整段序列表示成一个小数？
- Arithmetic coding 的区间更新公式是什么？
- 为什么 Arithmetic coding 通常比 Huffman 更接近 entropy？
- Shannon entropy 的公式是什么，单位是什么？
- 给定 residual 概率表时，如何计算理论最小 bits/residual？
- MDCT 为什么比直接硬切更适合 MP3？
- masking threshold 是怎么帮助 bit allocation 的？

---

## 11. 和后续内容的关系

这一组的压缩思想会继续影响后面的音频分析：

- 频域表示
- 噪声与失真
- 音质评价
- 特征提取
- 语音/音乐处理

如果你把这组内容吃透，后面的 Block 3 和 Block 4 会更容易理解。
