---
title: EBU5408 Block 3 - PPT 2：PCA and ICA
aliases:
  - Block 3 PPT 2
  - PCA and ICA
  - Digital Audio PCA
  - Digital Audio ICA
tags:
  - course/音频处理
  - EBU5408
  - digital-audio
  - block3
  - PCA
  - ICA
  - source-separation
source:
  - "[[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/2 PCA and ICA/Digital Audio PCA.pdf]]"
  - "[[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/2 PCA and ICA/Digital Audio ICA.pdf]]"
created: 2026-06-17
---

# Block 3 - PPT 2：PCA and ICA

> [!info] 课件来源
> 本笔记对应 Block 3 第 2 组课件：
> - [[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/2 PCA and ICA/Digital Audio PCA.pdf]]
> - [[课程笔记/音频处理/附件/Block 3- Core Signal Processing Techniques for Digital Audio/2 PCA and ICA/Digital Audio ICA.pdf]]
>
> 这一组课件围绕 **PCA（Principal Component Analysis）** 和 **ICA（Independent Component Analysis）** 展开，是从“音频压缩”过渡到“音频信号分析、降噪与源分离”的关键内容。

## 0. 本组 PPT 的核心问题

第 1 组课件讲的是 **compression and decompression**，主要关心如何让音频文件变小。第 2 组课件的重点不同：它关心的是如何从复杂音频数据中提取有用结构。

本组课件主要回答：

1. 音频数据为什么是高维的？
2. 如何用 **PCA** 降维、去冗余、降噪？
3. PCA 为什么不能可靠地分离多个独立声源？
4. 什么是 **cocktail party problem（鸡尾酒会问题）**？
5. 什么是 **BSS（Blind Source Separation，盲源分离）**？
6. 如何用 **ICA** 从混合录音中恢复独立声源？
7. PCA 和 ICA 的相似点与根本区别是什么？

> [!summary] 一句话主线
> **PCA** 主要找“最大方差方向”，适合降维、去冗余、初步降噪；  
> **ICA** 主要找“统计独立成分”，适合从多个混合录音中做盲源分离。

---

## 1. Dimensionality Reduction：音频为什么需要降维？

### 1.1 什么是高维音频数据

音频信号看起来是一条一维波形，但在实际处理中经常会变成高维数据。例如：

- 把音频切成很多 frame，每一帧有 1024 个 samples；
- 提取频谱，每一帧有很多 frequency bins；
- 提取 MFCC、spectrogram、chroma 等特征；
- 多个麦克风同时录音，每个麦克风都是一个 observation；
- 一段长音频包含大量时间点、频率点和通道。

因此，音频处理常常面对的是：

```text
many variables → complex data
```

降维的目标是：

```text
many variables → fewer components → simplified representation
```

### 1.2 降维的目的

课件中对 dimensionality reduction 的解释是：把高维音频特征转换成低维表示，同时尽量保留最重要的信息。

在音频处理中，降维有几个重要作用：

| 作用 | 解释 |
|---|---|
| 减少计算量 | 低维数据更容易处理，模型训练更快 |
| 降低存储需求 | 保留少量关键成分，减少数据规模 |
| 去除冗余 | 高相关变量携带重复信息 |
| 降噪 | 噪声常分布在低重要性成分中 |
| 特征提取 | 把复杂波形转成更有代表性的特征 |
| 可视化 | 高维音频特征可投影到 2D/3D 中观察 |

常见方法包括：

- **PCA**：Principal Component Analysis
- **ICA**：Independent Component Analysis

---

# A. PCA：Principal Component Analysis

## 2. PCA 的基本思想

### 2.1 PCA 是什么

**PCA（主成分分析）**是一种线性降维方法。它会寻找一组新的坐标轴，使数据投影到这些坐标轴上后，能够尽可能保留原始数据中的主要变化。

课件中的关键描述包括：

- finds new orthogonal directions that maximize variance；
- computes eigenvectors and eigenvalues from the covariance matrix；
- projects data onto eigenvectors for dimensionality reduction；
- captures most variability while reducing redundancy。

翻译成中文就是：

> PCA 寻找一组彼此正交的新方向，这些方向按“能解释的数据方差多少”排序。前几个方向通常包含最多信息，因此保留前几个主成分就可以降低维度。

### 2.2 PCA 中的“方差”为什么重要

在 PCA 中，方差可以理解为数据变化的强度。

如果一个方向上的方差很大，说明数据在这个方向上变化明显，很可能包含重要结构；如果一个方向上的方差很小，可能只是噪声或细小扰动。

所以 PCA 的策略是：

```text
保留高方差方向，丢弃低方差方向
```

在音频降噪中，这通常意味着：

- 主成分：更可能代表音乐、语音、鼓点等主要结构；
- 小成分：更可能包含随机噪声或不重要细节。

### 2.3 正交投影

PCA 会把数据投影到一个低维线性空间。这里有两个关键词：

- **orthogonal**：主成分之间互相垂直；
- **projection**：把原始数据映射到新坐标轴上。

如果原始数据是二维点云，PCA 会找出一条最能解释数据伸展方向的直线，把所有点投影到这条直线上。这样二维数据就变成了一维数据，同时尽量保留主要变化。

### 2.4 PCA 的两个等价目标

PCA 可以从两个角度理解：

1. 最大化投影后的方差；
2. 最小化重构误差。

也就是说，PCA 找到的低维空间既能让数据投影后尽量分散，又能让从低维空间重构回原空间时误差尽量小。

---

## 3. PCA 如何减少 redundancy

### 3.1 Correlation：变量相关导致冗余

如果两个音频特征高度相关，它们就包含大量重叠信息。例如：

- 相邻频率 bin 的能量可能一起变化；
- 相邻时间帧可能很相似；
- 多个麦克风录到的声音可能高度相关。

这种 overlapping information 就是 redundancy。

### 3.2 PCA 用新坐标轴去相关

PCA 会把原始相关变量转换成一组新的主成分。主成分之间是正交的，并且在 PCA 的二阶统计意义下是 uncorrelated（不相关）的。

这意味着 PCA 可以减少由高相关变量带来的重复信息。

> [!note] PCA 去的是“相关性”，不是“独立性”
> PCA 可以让成分不相关，但不相关不等于统计独立。后面的 ICA 才以统计独立为目标。

---

## 4. PCA 使用的统计量：Second-Order Statistics

PCA 使用的是 **second-order statistics（二阶统计量）**，包括：

| 统计量 | 含义 |
|---|---|
| Variance | 单个变量自身的变化程度 |
| Covariance | 两个变量如何一起变化 |
| Correlation | 标准化后的共同变化关系 |

PCA 依赖 covariance matrix（协方差矩阵）。协方差矩阵描述不同变量之间的共同变化结构。

PCA 对协方差矩阵做 eigen decomposition：

- eigenvectors：主成分方向；
- eigenvalues：每个方向解释的方差大小。

可以理解为：

```text
协方差矩阵 → 特征值/特征向量 → 主成分方向与重要性
```

---

## 5. Data centering：为什么 PCA 前要中心化？

### 5.1 中心化公式

PCA 前需要把数据减去均值：

$$
x_{centered} = x - E\{x\}
$$

其中：

- $x$ 是原始数据；
- $E\{x\}$ 是均值；
- $x_{centered}$ 是中心化后的数据。

### 5.2 为什么要中心化

如果不减均值，协方差矩阵会受到整体偏移影响。PCA 想分析的是“数据围绕均值如何变化”，而不是数据本身离原点多远。

课件例子：北京一周温度

```text
原始数据：[26, 27, 28, 29, 30, 31, 32]
均值：29
中心化：[-3, -2, -1, 0, 1, 2, 3]
```

中心化后，数据平均值在 0 附近，PCA 分析的就是相对于平均水平的变化。

### 5.3 音频中的中心化

在音频帧处理中，常见做法是对每一帧减去均值：

```python
frame_means = noisy_frames.mean(axis=1, keepdims=True)
noisy_frames_centered = noisy_frames - frame_means
```

这样做能减少 DC offset 或 frame-level bias，让 PCA 更关注波形变化结构。

---

## 6. PCA 用于音频降噪

### 6.1 课件中的真实问题

假设一个麦克风录到的是混合信号：

$$
x(t) = a_1x_1(t) + a_2x_2(t) + n(t)
$$

其中：

- $x_1(t)$：目标声音，例如 speech；
- $x_2(t)$：背景声音，例如 music 或环境噪声；
- $a_1, a_2$：混合权重；
- $n(t)$：additive noise；
- $x(t)$：我们实际观测到的混合录音。

目标是改善录音，降低噪声，并保留最重要的信号结构。

### 6.2 PCA 降噪的直观逻辑

PCA 降噪假设：

- 主要信号结构通常解释较大方差；
- 随机噪声通常分散在很多小成分中；
- 保留前 $k$ 个主成分并重构，可以保留主要结构，抑制噪声。

流程如下：

```text
Noisy audio
→ framing
→ centering
→ PCA fit
→ keep k components
→ inverse transform
→ reconstruct audio
```

### 6.3 为什么要分帧

音频是一长串 sample，直接对整段做 PCA 不方便。课件代码把音频切成 frame：

```python
frame_size = 1024
noisy_frames = frame_audio(noisy_signal, frame_size)
```

这样会得到一个二维矩阵：

```text
shape = (num_frames, frame_size)
```

每一帧是一条 sample，每个 sample 位置是一个 feature。

### 6.4 PCA 降噪代码流程解释

课件代码大致分为六步。

#### Step 1：读取音频并转单声道

```python
signal, sr = sf.read(input_wav)
if signal.ndim > 1:
    signal = signal[:, 0]
```

如果音频是 stereo，只取一个 channel，方便演示。

#### Step 2：添加人工噪声

```python
np.random.seed(0)
noise_power = 0.02
noiseOnly = noise_power * np.random.randn(len(signal))
noisy_signal = signal + noiseOnly
```

这里用随机噪声生成 noisy signal，方便比较原始、加噪和降噪结果。

`np.random.seed(0)` 的作用是保证每次运行生成同样的噪声，便于测试和对比。

#### Step 3：切帧

```python
frame_size = 1024
noisy_frames = frame_audio(noisy_signal, frame_size)
```

`frame_audio` 会把一维信号 reshape 成二维矩阵。

#### Step 4：中心化

```python
frame_means = noisy_frames.mean(axis=1, keepdims=True)
noisy_frames_centered = noisy_frames - frame_means
```

每一帧减去自己的均值。

#### Step 5：PCA 变换与重构

```python
n_components = 10
pca = PCA(n_components=n_components)
pca.fit(noisy_frames_centered)
frames_pca = pca.transform(noisy_frames_centered)
frames_reconstructed = pca.inverse_transform(frames_pca)
frames_reconstructed += frame_means
```

这里的核心是：只保留 `n_components` 个主成分。主成分数量越少，降维越强，但也更容易损失声音细节。

#### Step 6：拼回完整音频

```python
denoised_signal = overlap_add(frames_reconstructed)
sf.write('denoised_signal_pca.wav', denoised_signal, sr)
```

课件代码中的 `overlap_add` 实际上没有做重叠加窗，只是把 frame 展平还原成一维信号。

---

## 7. 如何选择 PCA component 数量

### 7.1 Explained variance ratio

每个主成分都会解释一部分总方差。`explained variance ratio` 表示某个主成分解释了总方差的比例。

如果累计 explained variance 达到 95% 或 99%，通常说明保留了大部分信息。

常见选择方式：

- 画 explained variance ratio 曲线；
- 画 cumulative explained variance 曲线；
- 使用 elbow method；
- 保留达到某个阈值的 component 数量。

### 7.2 Elbow method 的局限

课件指出，elbow method 可能找到一个最大曲率点，例如约 23 个 components。但音频比较复杂：

- 太少 components 会导致失真；
- 太多 components 会保留噪声；
- elbow point 只基于方差，不直接基于听感质量。

所以在音频降噪中，光看方差不一定够。

### 7.3 MSE-based optimisation

如果有 clean signal，可以尝试不同 component 数量，并计算重构误差：

$$
MSE = \frac{1}{N}\sum_{n=1}^{N}(x_n - \hat{x}_n)^2
$$

选择 MSE 最小的 component 数量。

课件中的 sample results 显示：

| Components | Residual Noise Power | Noise Reduction |
|---:|---:|---:|
| 12 | 0.001918 | Worse than noisy |
| 42 | 0.000229 | 42.60% |
| 52 | 0.000188 | 52.7% |
| 68 | 0.000171 | 57.10% |
| 144 | 0.199+ | High distortion |

这个表说明：component 数量不是越多越好，也不是越少越好。需要在“保留信号”和“去除噪声”之间平衡。

> [!question] 如果没有 clean signal 怎么办？
> 可以结合听感评价、spectrogram 观察、SNR 估计、noise floor 分析、任务指标，或使用交叉验证式的无参考质量评价方法。

---

## 8. VMD：Variational Mode Decomposition

### 8.1 为什么引入 VMD

真实音频往往是 **non-stationary（非平稳）** 的，也就是频率内容会随时间变化。

传统 Fourier analysis 更适合 stationary signal，因此面对快速变化的音频事件时可能不够理想。

EMD（Empirical Mode Decomposition）适合非平稳信号，但有问题：

- mode mixing；
- 对噪声敏感；
- 稳定性不足。

VMD 是更稳健的替代方法。

### 8.2 VMD 的核心思想

**VMD（Variational Mode Decomposition）**会把信号分解成若干个 band-limited modes，也就是不同频带内的 intrinsic mode functions。

每个 mode 有：

- 自己的 center frequency；
- 自己的 bandwidth；
- 相对紧凑的频率范围。

可以理解为：

```text
复杂非平稳信号 → 多个频带受限的 mode
```

### 8.3 VMD 的优点

课件强调：

- 比 EMD 更鲁棒；
- 减少 mode mixing；
- 有更强的数学优化框架；
- 适合音频、图像、生物医学信号和振动分析。

### 8.4 PCA + Wiener + VMD 多阶段降噪

课件提出一个 multi-stage approach：

1. **PCA initial denoising**：先按 frame 做 PCA，去掉被噪声主导的维度。
2. **Oracle Wiener Filter**：在频域中按 clean power / total power 计算增益，抑制残余噪声。
3. **VMD**：把滤波后的信号分解成多个 band-limited modes，稳定非平稳瞬态。

这个 pipeline 结合了：

- PCA 的统计方差分析；
- Wiener filter 的功率谱密度思想；
- VMD 的自适应子频带分解。

课件中给出的结果是：集成 pipeline 可以达到约 70.2% 的 noise power reduction，优于单独 PCA。

---

# B. ICA：Independent Component Analysis

## 9. Cocktail Party Problem

### 9.1 问题描述

鸡尾酒会问题是音频源分离的经典例子：

- 房间里有多个人同时说话；
- 多个麦克风从不同位置录音；
- 每个麦克风都录到所有人声音的混合；
- 不同麦克风中的混合比例不同；
- 目标是从混合录音中恢复每个人的原始声音。

也就是：

```text
mixed microphone recordings → separate independent sources
```

### 9.2 为什么 PCA 不够

课件先问：PCA 能不能分离音频信号？

结论是：

> PCA cannot reliably separate independent audio sources.

原因是 PCA 主要寻找最大方差方向和不相关成分，但源分离需要的是统计独立成分。

不相关只是独立的弱条件：

```text
independent ⇒ uncorrelated
uncorrelated ⇏ independent
```

所以 PCA 可以用于降维、去冗余和预处理，但不能可靠完成盲源分离。

---

## 10. Blind Source Separation（BSS）

### 10.1 BSS 是什么

**BSS（Blind Source Separation，盲源分离）**是从混合信号中恢复原始信号的任务。

之所以叫 blind，是因为我们通常不知道：

- 原始源信号是什么；
- 源信号有几个；
- 它们如何混合；
- mixing matrix 是什么。

我们只观察到混合后的数据。

### 10.2 BSS 的应用

| 领域 | 应用 |
|---|---|
| 音频处理 | 从噪声中分离语音，分离乐器，人声提取 |
| 生物医学 | EEG 脑电信号分离，胎儿心跳提取 |
| 图像处理 | 分离重叠图像，去除伪影 |
| 通信 | 分离无线传输中的混合信号 |
| 金融 | 找出影响市场的独立因素 |

---

## 11. BSS 数学模型

课件给出的基本模型：

$$
x(t) = A s(t)
$$

其中：

- $s(t)$：原始 source signals；
- $x(t)$：observed mixture signals；
- $A$：unknown mixing matrix。

我们的目标是：只根据 $x(t)$ 估计 $s(t)$。

### 11.1 两个源、两个麦克风例子

如果有两个 source 和两个 sensor，则：

$$
A = \begin{bmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22}
\end{bmatrix}
$$

观测信号为：

$$
x_1(t)=a_{11}s_1(t)+a_{12}s_2(t)
$$

$$
x_2(t)=a_{21}s_1(t)+a_{22}s_2(t)
$$

这里 $A$ 是未知的，所以问题是 blind。

---

## 12. ICA 的基本思想

### 12.1 ICA 是什么

**ICA（Independent Component Analysis）**是 BSS 中常用方法。它利用一个关键假设：

> 原始 source signals 是 statistically independent 的。

ICA 要找一个 demixing matrix $W$，使得：

$$
y(t)=Wx(t)
$$

其中 $y(t)$ 是估计出的 source signals。理想情况下：

$$
y(t) \approx s(t)
$$

如果完美反转混合过程，那么：

$$
W = A^{-1}
$$

但因为 $A$ 不知道，ICA 要从 observed mixtures 中估计 $W$。

### 12.2 ICA 的核心目标

ICA 不追求最大方差，而是追求最大统计独立性。

算法大致过程：

```text
observe x(t)
→ initialize W
→ compute y(t)=Wx(t)
→ measure independence of y components
→ adjust W to increase independence
→ repeat until convergence
```

常用算法：

- FastICA
- JADE
- RADICAL

---

## 13. Statistical Independence

### 13.1 独立性的概率定义

两个信号 $s_1$ 和 $s_2$ 独立意味着：

$$
p(s_1, s_2) = p(s_1)p(s_2)
$$

也就是联合概率可以分解成边缘概率乘积。

### 13.2 Mutual information

如果两个信号独立，它们之间的 mutual information 为 0。

ICA 可以被理解为：寻找一个变换，使输出成分之间的 mutual information 尽可能低。

### 13.3 ICA 可能失败的情况

ICA 依赖独立性假设。如果源信号不独立，ICA 可能效果不好。例如：

- 两个源非常相似；
- 源信号高度相关；
- 多个源都是 Gaussian；
- 混合过程不是线性的；
- 观测通道数量少于源数量太多。

---

## 14. ICA 的 ambiguity 不确定性

ICA 分离出的信号存在两个常见不确定性。

### 14.1 Scaling ambiguity

恢复出的信号可能被放大或缩小：

$$
y(t)=c\cdot s(t)
$$

原因是如果 source 放大，mixing coefficient 可以相应缩小，混合结果仍然一样。

所以 ICA 无法确定原始 source 的绝对幅度。通常会假设 source 有 unit variance。

### 14.2 Permutation ambiguity

恢复出的 source 顺序不确定。

例如真实顺序是：

```text
[speech, music]
```

ICA 可能输出：

```text
[music, speech]
```

这不是错误，因为 ICA 只负责分离独立成分，不知道每个成分的语义标签。

---

## 15. Unmixing matrix W

### 15.1 W 的意义

$W$ 是 unmixing matrix，也叫 demixing matrix。它把观测混合信号变成估计源信号：

$$
\hat{y}(t)=W x(t)
$$

每一行 $w_i$ 都会生成一个 estimated independent component：

$$
y_i(t)=w_{i1}x_1(t)+w_{i2}x_2(t)+\cdots+w_{in}x_n(t)
$$

### 15.2 W 和 A 的关系

混合过程：

$$
x(t)=A s(t)
$$

分离过程：

$$
y(t)=W x(t)
$$

如果分离完美：

$$
W \approx A^{-1}
$$

但实际中 $A$ 未知，所以 ICA 通过统计独立性来估计 $W$。

---

## 16. ICA Python 实现流程

课件代码用 `FastICA` 分离两个 mixed signals。

### 16.1 读取两个混合录音

```python
import librosa
import numpy as np
import soundfile as sf
import matplotlib.pyplot as plt
from sklearn.decomposition import FastICA

file_path_1 = 'mixed_signal_1.wav'
file_path_2 = 'mixed_signal_2.wav'

audio_mixed_1, sr = librosa.load(file_path_1, sr=None, mono=False)
audio_mixed_2, sr2 = librosa.load(file_path_2, sr=None, mono=False)
```

这里 `sr=None` 表示保持原始采样率。

### 16.2 堆叠成观测矩阵

```python
X = np.vstack([audio_mixed_1, audio_mixed_2])
```

此时：

```text
X shape = (2, N_samples)
```

每一行是一个麦克风或一个混合观测。

### 16.3 转置给 sklearn

`sklearn` 的 `FastICA` 期望输入形状是：

```text
(n_samples, n_features)
```

所以要转置：

```python
X_transposed = X.T
```

变成：

```text
(N_samples, 2)
```

### 16.4 应用 FastICA

```python
ica = FastICA(n_components=2, random_state=0)
S_est = ica.fit_transform(X_transposed)
```

`S_est` 中的两列就是估计出来的两个 source。

### 16.5 保存分离结果

```python
estimated_source1 = S_est[:, 0]
estimated_source2 = S_est[:, 1]

sf.write('separated_source1.wav', estimated_source1, sr)
sf.write('separated_source2.wav', estimated_source2, sr)
```

注意：输出顺序可能与真实 source 顺序不同，音量也可能不同，这是 ICA 的 ambiguity。

---

## 17. 源数量未知时怎么办？

真实场景中经常不知道有几个 source。

课件建议：先用 PCA，再用 ICA。

流程：

```text
Observed mixtures
→ PCA estimate important components
→ choose components explaining ~99% variance
→ use that number in ICA
→ source separation
```

原因：

- 真实信号通常贡献大部分方差；
- 噪声往往贡献较低方差；
- PCA 可先保留高方差成分，丢弃部分低方差噪声；
- ICA 再对保留成分做独立源分离。

这说明 PCA 和 ICA 不是互相替代，而是可以串联使用。

---

## 18. PCA 和 ICA 的对比

### 18.1 相似点

PCA 和 ICA 都可以用于：

- feature extraction；
- dimension reduction；
- finding hidden structure；
- preprocessing audio data。

### 18.2 根本区别

| 对比 | PCA | ICA |
|---|---|---|
| 目标 | 最大化方差 | 最大化统计独立性 |
| 统计依据 | 二阶统计量：variance/covariance | 更高阶统计性质/非高斯性/独立性 |
| 输出成分关系 | 正交、不相关 | 不一定正交，但尽量独立 |
| 典型用途 | 降维、去冗余、降噪、可视化 | 盲源分离、语音/乐器分离 |
| 是否能分离独立声源 | 不可靠 | 更适合 |
| 结果不确定性 | 主成分方向符号可能变 | scale 和 permutation ambiguity |

> [!important] 核心区别
> PCA 问的是：“哪些方向保留最多变化？”  
> ICA 问的是：“哪些变换能让输出成分彼此最独立？”

---

## 19. 工业安全警报场景：如何设计 pipeline

课件练习给出一个场景：

> 90 秒工业设施录音，里面有重型机械持续嗡鸣、间歇性语音广播、偶发警报声。目标是提取关键 safety alarm。

### 19.1 为什么这个问题难

难点包括：

- machinery hum 是持续低频或窄带噪声；
- verbal announcements 和 alarm 可能频率重叠；
- siren/alarm 可能是短时、非平稳、强瞬态；
- 背景噪声复杂且变化；
- 如果只有单通道录音，源分离更困难。

### 19.2 可能的算法选择

如果有多个麦克风录音，优先考虑：

```text
PCA preprocessing + ICA source separation + filtering/VMD refinement
```

如果只有单通道，可以考虑：

- STFT/spectrogram filtering；
- band-pass filter 针对 alarm 频段；
- VMD 分解非平稳成分；
- supervised ML / classifier 检测 alarm；
- template matching 或 spectral peak tracking。

### 19.3 推荐 pipeline

一个合理 pipeline：

1. **Preprocessing**
   - resampling；
   - mono/multichannel alignment；
   - normalization；
   - remove DC offset。

2. **Time-frequency analysis**
   - STFT 或 spectrogram；
   - 找 alarm 主要频率范围和时间模式。

3. **PCA 降噪或估计 component 数量**
   - 保留解释 95%-99% 方差的成分；
   - 去掉低方差噪声。

4. **ICA 源分离**
   - 如果有多通道，使用 FastICA；
   - 分离 machinery、speech、alarm 相关成分。

5. **Post-filtering / VMD**
   - 对 alarm 成分做 band-pass；
   - 用 VMD 分离非平稳模式；
   - 抑制残余噪声。

6. **Evaluation**
   - 听感检查；
   - spectrogram 对比；
   - SNR 或 residual noise power；
   - alarm detection accuracy。

### 19.4 方法局限

| 方法 | 局限 |
|---|---|
| PCA | 基于方差，不保证分离 source；可能丢掉低能但重要的 alarm |
| ICA | 需要独立性假设；多源数量可能超过观测通道；输出顺序和幅度不确定 |
| VMD | 参数如 mode 数 K 需要选择；结果依赖频带结构 |
| Filtering | 如果 alarm 与噪声频段重叠，简单滤波效果有限 |

---

## 20. 本组课的考试重点

### 20.1 PCA 必须会

- PCA 是什么；
- 为什么 PCA 能降维；
- 什么是 principal component；
- 为什么要 center data；
- covariance matrix、eigenvectors、eigenvalues 的意义；
- explained variance ratio 如何选择 components；
- PCA 降噪流程；
- PCA 的限制。

### 20.2 ICA 必须会

- cocktail party problem；
- BSS 的定义；
- BSS 数学模型 $x(t)=As(t)$；
- ICA 的目标 $y(t)=Wx(t)$；
- $W \approx A^{-1}$ 的含义；
- statistical independence；
- scaling ambiguity 和 permutation ambiguity；
- FastICA 的基本使用流程；
- PCA 与 ICA 的区别。

---

## 21. 常见问答

### Q1. PCA 能不能做源分离？

不能可靠地做。PCA 找最大方差方向和不相关成分，而真正的源分离需要独立性。PCA 可作为预处理，但不是完整 BSS 解决方案。

### Q2. PCA 为什么能降噪？

因为主要信号结构通常集中在高方差主成分中，而随机噪声常分布在较小成分中。保留前几个主成分并重构，可以保留主结构并抑制部分噪声。

### Q3. PCA component 数量怎么选？

可以用 explained variance threshold，比如 95% 或 99%；也可以用 elbow method；如果有 clean reference，可以用 MSE 或 residual noise power 找最优值。

### Q4. ICA 为什么适合 cocktail party problem？

因为不同说话人的语音源通常可近似认为统计独立。ICA 通过寻找 demixing matrix，让输出成分尽可能独立，从而恢复不同声源。

### Q5. ICA 的结果为什么顺序会乱？

因为 ICA 只关心分离独立成分，不知道哪个成分应该排第一。输出 `[s2, s1]` 和 `[s1, s2]` 在数学上都合理。

### Q6. ICA 为什么会有音量不确定？

因为源信号的缩放可以和 mixing matrix 的缩放互相抵消。仅凭混合信号无法确定真实绝对幅度。

---

## 22. 一页速记

> [!summary] Block 3 第 2 组 PPT 速记
> - PCA：找最大方差方向，用于降维、去冗余、降噪。
> - PCA 基于 covariance matrix、eigenvectors、eigenvalues。
> - PCA 前要 center data，否则均值偏移会干扰协方差分析。
> - Explained variance ratio 用于选择主成分数量。
> - PCA 降噪：切帧 → 中心化 → PCA → 保留 k 个成分 → 重构。
> - PCA 不可靠地分离独立声源，因为它只去相关，不保证独立。
> - BSS：只根据混合观测恢复未知源信号。
> - ICA：找 demixing matrix $W$，使 $y(t)=Wx(t)$ 的成分尽可能独立。
> - BSS 模型：$x(t)=As(t)$；理想分离：$W \approx A^{-1}$。
> - ICA 有 scale ambiguity 和 permutation ambiguity。
> - 源数量未知时，可以先 PCA 估计重要 component 数，再 ICA。

---

## 23. 和前后课程的连接

- 与第 1 组压缩课件的连接：PCA 和 ICA 都依赖“数据中存在结构和冗余”这一思想。
- 与后续 filtering/noise quality 的连接：PCA、VMD、Wiener filtering 都是降噪和质量提升方法。
- 与机器学习的连接：PCA 常用于特征降维，ICA 可作为源分离和预处理步骤。
- 与实验的连接：Lab 中可能会用 Python、NumPy、SoundFile、librosa、scikit-learn 处理真实音频。
