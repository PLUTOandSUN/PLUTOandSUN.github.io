> [!info] 课件来源
> 原始课件：[[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/2 EBU6230_L2_imagerep.pdf]]  
> 本节是 Part 1 的第 2 个正式课件，主题是 **Image Representation 图像表示**。核心内容包括：数字图像如何由连续图像变成离散矩阵、sampling 采样、quantization 量化、sub-sampling 下采样、pixel interpolation 像素插值。

---

## 0. 本节课的整体框架

这一讲回答的是一个基础问题：

> **一幅图像在计算机里到底是什么？**

上一讲已经给出数字图像的定义：图像可以看成二维函数 $f(x,y)$。这一讲进一步解释：

1. 现实世界中的图像本来是连续的；
2. 计算机不能直接存储连续函数；
3. 所以要通过 **sampling 采样** 把连续空间变成离散网格；
4. 再通过 **quantization 量化** 把连续强度变成有限整数；
5. 最终数字图像就变成一个二维或三维数组；
6. 如果改变图像大小，还需要 **sub-sampling** 或 **interpolation**。

可以用一条主线理解本讲：

```text
Real world scene
→ continuous image f(x,y)
→ sampling in space
→ quantization in intensity
→ digital image g(i,j)
→ storage / display / processing
```

本讲的五个关键词：

| 关键词 | 中文 | 作用 |
|---|---|---|
| Image representation | 图像表示 | 说明图像在数学和计算机中的形式 |
| Sampling | 采样 | 决定空间分辨率 |
| Quantization | 量化 | 决定灰度/强度分辨率 |
| Sub-sampling | 下采样 | 缩小图像，但可能损失细节 |
| Interpolation | 插值 | 放大图像或几何变换时估计新像素 |

---

## 1. 图像处理与信号处理的关系

PPT 一开始强调：image and video processing 与 signal processing 有密切关系。

### 1.1 图像和视频也是信号

在信号处理里，信号不一定只是一维声音波形。图像和视频也可以看成信号：

| 类型 | 数学表示 | 自变量 | 函数值 |
|---|---|---|---|
| 音频 | $f(t)$ | 时间 $t$ | 声压/电压/幅度 |
| 灰度图像 | $f(x,y)$ | 空间坐标 $x,y$ | 灰度/亮度 |
| 彩色图像 | $[R(x,y),G(x,y),B(x,y)]$ | 空间坐标 $x,y$ | 颜色通道值 |
| 视频 | $f(x,y,t)$ | 空间 + 时间 | 每帧图像强度 |

所以图像处理其实是二维信号处理，视频处理可以看作三维信号处理。

### 1.2 完整图像处理流程

PPT 给出的流程可以理解为：

```text
Real world
→ Capture system
→ Image and video processing
→ Display
→ Human visual system
```

每一步都可能影响最终图像质量：

- **real world**：真实场景中的光照、物体、颜色、运动；
- **capture system**：相机、扫描仪、传感器；
- **processing**：增强、去噪、压缩、插值、识别；
- **display**：屏幕、打印机、投影设备；
- **human visual system, HVS**：人眼和大脑对亮度、颜色、边缘、纹理的感知。

> [!important] 关键思想
> 图像质量不只由图像文件本身决定，也由采集、处理、显示和人类视觉感知共同决定。

---

## 2. Analogue to digital：从模拟到数字

### 2.1 为什么要数字化？

现实世界中的光、颜色和亮度是连续变化的。相机、扫描仪等设备最初采集到的信号也可以看成连续或模拟信号。

但计算机只能存储和处理 bit：

```text
0 和 1
```

因此必须把模拟信号转换成数字表示。

PPT 用 1D 信号说明：

- microphones 麦克风产生连续电压信号；
- video cameras 摄像机产生连续或模拟视觉信号；
- 要输入计算机处理，必须转换为 bit stream。

图像数字化同样需要两个基本步骤：

1. **Sampling 采样**：把连续坐标离散化；
2. **Quantization 量化**：把连续强度离散化。

### 2.2 采样和量化的直观区别

| 操作 | 作用对象 | 问题 | 决定什么 |
|---|---|---|---|
| Sampling | 横轴/空间位置 | 在哪里取样？ | 空间分辨率 |
| Quantization | 纵轴/强度值 | 每个样本用多少等级表示？ | 灰度/亮度分辨率 |

对于图像来说：

```text
Sampling 决定有多少 pixel
Quantization 决定每个 pixel 可以取多少种值
```

---

## 3. Continuous image representation：连续图像表示

### 3.1 连续图像是二维函数

PPT 中说：一幅图像可以表示为两个连续变量的函数：

$$
f(x,y)
$$

其中：

- $x$：水平空间坐标；
- $y$：垂直空间坐标；
- $f(x,y)$：位置 $(x,y)$ 处的强度值。

对于灰度图像：

$$
f(x,y)=\text{grey level at }(x,y)
$$

也就是说，图像不是单纯的“图片文件”，而是一个空间位置到亮度值的映射：

$$
(x,y) \rightarrow f(x,y)
$$

### 3.2 坐标和强度的含义

坐标 $(x,y)$ 决定位置，函数值 $f(x,y)$ 决定亮度。

例如：

- $f(10,20)=0$：该点接近黑色；
- $f(10,20)=255$：该点接近白色；
- 中间值表示不同灰度。

如果是彩色图像，则每个点可能有三个函数值：

$$
R(x,y),\quad G(x,y),\quad B(x,y)
$$

合起来写作：

$$
I(x,y) = [R(x,y),G(x,y),B(x,y)]
$$

---

## 4. Discrete image representation：离散图像表示

### 4.1 从 $f(x,y)$ 到 $g(i,j)$

连续图像是：

$$
f(x,y)
$$

数字图像是采样和量化后的离散版本，可以写成：

$$
g(i,j)
$$

其中：

- $i$：row index 行索引；
- $j$：column index 列索引；
- $g(i,j)$：第 $i$ 行、第 $j$ 列的像素值。

如果图像大小是 $M\times N$，则通常表示有：

- $M$ 行；
- $N$ 列；
- 总像素数：

$$
M\times N
$$

### 4.2 图像就是一个矩阵

灰度图像可以看成一个二维矩阵：

$$
g(i,j)=
\begin{bmatrix}
g(0,0) & g(0,1) & \cdots & g(0,N-1)\\
g(1,0) & g(1,1) & \cdots & g(1,N-1)\\
\vdots & \vdots & \ddots & \vdots\\
g(M-1,0) & g(M-1,1) & \cdots & g(M-1,N-1)
\end{bmatrix}
$$

这就是为什么在程序里图像常用 array 或 matrix 存储。

### 4.3 灰度图像和彩色图像的数组形式

灰度图像：

```text
M × N matrix
```

RGB 彩色图像：

```text
M × N × 3 array
```

其中第三个维度分别表示：

```text
R channel, G channel, B channel
```

---

## 5. 坐标系统与索引：Be careful!

PPT 特别提醒：不同数学表示和编程语言中，图像索引方式可能不同。

### 5.1 Cartesian coordinates

在数学里的笛卡尔坐标系中，常见约定是：

- $x$ 向右增加；
- $y$ 向上增加；
- 原点可能在左下角。

### 5.2 图像数组坐标

在图像矩阵中，通常使用：

- 行 index $i$；
- 列 index $j$。

很多图像处理系统中：

- $i$ 向下增加；
- $j$ 向右增加；
- 原点在左上角。

这和数学笛卡尔坐标的方向不同。

### 5.3 C/C++/Java 与 MATLAB 的差异

| 环境 | 索引起点 | 常见表示 |
|---|---:|---|
| C/C++/Java | 0 | `g[0][0]` 到 `g[M-1][N-1]` |
| MATLAB | 1 | `g(1,1)` 到 `g(M,N)` |
| 数学坐标 | 不固定 | 常用 $(x,y)$ |

> [!warning] 易错点
> 图像中的 $x,y$ 坐标和矩阵中的 $i,j$ 行列索引不是完全一样的概念。写代码或做题时要先确认原点、方向和索引起点。

---

## 6. Pictorial intensity representation：灰度图像表示

### 6.1 灰度图像是什么？

PPT 中说：

> A grey level image is one in which the value of each pixel is a single sample representing only an amount of light.

也就是说，灰度图像中每个像素只有一个数值，用来表示该位置的亮度。

例如 8-bit 灰度图：

| 像素值 | 显示效果 |
|---:|---|
| 0 | 黑色 |
| 127 或 128 | 中灰 |
| 255 | 白色 |

通常约定：

> 数值越大，像素越亮。

### 6.2 灰度表格示例

一个很小的灰度图可以写成：

$$
\begin{bmatrix}
0 & 128 & 255\\
60 & 128 & 200\\
30 & 90 & 255
\end{bmatrix}
$$

每个数值对应屏幕上的一个像素亮度。

---

## 7. Pictorial colour representation：彩色图像表示

### 7.1 RGB 分量

彩色图像可以拆成多个分量。最常见的是 RGB：

```text
Red component
Green component
Blue component
```

一幅 RGB 图像可以看作三幅灰度图的组合：

$$
I(x,y)=\{R(x,y),G(x,y),B(x,y)\}
$$

每个通道本身都是一幅灰度图，只不过它表示的是红、绿、蓝光的强度。

### 7.2 为什么彩色图像更占空间？

如果灰度图每个像素 8 bit，那么一个像素只需要 1 byte。

RGB 图像每个像素有 3 个通道：

$$
8+8+8=24\text{ bits}
$$

所以 RGB 8-bit 图像通常是：

$$
24\text{ bits/pixel}=3\text{ bytes/pixel}
$$

---

## 8. What is a pixel？像素到底是什么？

PPT 中有一句非常重要的话：

> A pixel is not a little square. It is a sample from a continuous 2D function.

### 8.1 常见误解

很多人以为 pixel 是屏幕上的小方块。显示时它确实经常被画成一个小方块，但在图像表示理论中，pixel 的本质是：

> 连续图像函数在某个空间位置上的一个样本。

也就是说：

```text
pixel = sampling position + sampled value
```

### 8.2 pixel 的两个核心属性

每个 pixel 至少包含：

1. **location 位置**  
   它位于第几行、第几列，或坐标 $(x,y)$ 附近。

2. **value 数值**  
   它的灰度值、颜色值、深度值或其他测量值。

因此数字图像由有限个 pixel 组成，每个 pixel 有特定位置和数值。

---

## 9. What is an image？什么才算图像？

PPT 提出一个有意思的问题：不是所有二维数组都一定直观上是“图像”。

### 9.1 一维时间序列不是图像

例如温度随时间变化：

$$
f(t)
$$

这是一个 1D time series，不是图像。

如果把它切成很多段再堆成二维表格，形式上可以得到一个二维数组，但它的两个轴可能是“month”和“year”，不一定是空间坐标。

### 9.2 Spectrogram 是图像吗？

PPT 给了 audio spectrogram 的例子：

```text
time × frequency → energy
```

它是二维函数，但两个坐标是 time 和 frequency，不是两个空间坐标。

所以它可以被显示成图像，也可以用图像处理方法分析，但严格来说它不是普通意义上的空间图像。

### 9.3 直观定义

PPT 给出的直观判断标准：

- $x$ 和 $y$ 应该是 spatial coordinates；
- 两个坐标最好有相同单位；
- 2D rotation 和 translation 应该有意义；
- 不应该有特殊坐标，比如 time 或 temperature。

换句话说，典型图像应该像从上往下拍摄桌面物体：没有特殊方向，旋转和平移都有自然意义。

### 9.4 例外：white noise

PPT 提到一个例外：white-noise time series 切开堆成二维表后，也可以被看作图像。

原因是白噪声没有结构，旋转和平移不会破坏其统计特性。因此在某些情况下，它可以被看作图像。

---

## 10. Sampling：采样

### 10.1 1D 采样回顾

在一维信号中，采样就是按固定时间间隔记录信号值。

采样率 sampling rate 表示每秒采多少个样本，单位是 Hz：

$$
f_s = \text{samples per second}
$$

例如音频采样率 44.1 kHz 表示每秒采样 44100 次。

### 10.2 图像中的采样

图像采样不是沿时间轴，而是沿空间坐标轴。

连续图像：

$$
f(x,y)
$$

采样后得到离散位置：

$$
(i,j)
$$

所以 pixel position 就是 image 的 sampling position。

### 10.3 采样决定 spatial resolution

图像的 spatial resolution 空间分辨率由采样密度决定。

PPT 中的说法：

> Resolution = number of pixels per unit area.

也就是说，单位面积内采样点越多，空间分辨率越高。

---

## 11. Nyquist theorem：奈奎斯特定理

### 11.1 1D Nyquist theorem

PPT 中写到：

> The sampling rate should be at least twice the maximum frequency response.

公式为：

$$
f_s \ge 2f_{max}
$$

其中：

- $f_s$ 是 sampling frequency；
- $f_{max}$ 是信号中最高频率。

这表示：要无损地表示最高频率为 $f_{max}$ 的信号，采样率至少要是它的两倍。

### 11.2 采样不足会发生什么？

如果采样太少，会出现 aliasing 混叠。

PPT 中举例：

- 每个周期只采样 1 次，可能被误认为 constant signal；
- 每个周期采样 1.5 次，可能被误认为 lower frequency signal。

也就是说，采样不足会让高频信号伪装成低频信号。

### 11.3 图像中的 aliasing

在图像中，aliasing 常表现为：

- 锯齿边缘 jagged edges；
- 摩尔纹 moiré patterns；
- 细线条断裂或变形；
- 下采样后纹理变得奇怪。

解决思路通常是：

1. 提高采样率；
2. 下采样前先做 low-pass filtering；
3. 使用 anti-aliasing 技术。

---

## 12. Image digitization：图像数字化

### 12.1 Digitizer

PPT 中的图像数字化流程：

```text
Scene → digitizer/scanner → g(i,j)
```

digitizer 的作用是把真实场景变成数字图像矩阵。

常见 digitizer 包括：

- scanner；
- digital camera；
- microscope camera；
- satellite sensor；
- medical imaging sensor。

### 12.2 Sampler

连续图像域被扫描，在离散位置测量亮度值，形成 intensity array。

即：

```text
continuous domain → sampler → array of sampling positions → g(i,j)
```

### 12.3 Scanline

PPT 提到 scanline：

> Converting the continuous 2D signal into a digital image by sampling per scanline.

scanline 可以理解为一行像素。图像采集时可以按行扫描：

```text
row 0 → row 1 → row 2 → ... → row M-1
```

每一行包含多个采样位置。

---

## 13. Cameras and colour sampling：相机如何采集颜色？

### 13.1 CCD/CMOS 元件测量的是强度

PPT 中说：

> Each CCD-element measures scalar intensity.

也就是说，单个传感器元件本身通常只能测量光强，而不能直接知道完整颜色。

要得到彩色图像，需要测量不同光谱波段，例如红、绿、蓝。

### 13.2 Bayer filter

标准相机常使用 Bayer filter。它在传感器上覆盖不同颜色滤镜，使不同位置分别测量 R、G、B 光强。

典型 Bayer pattern 中绿色像素更多，因为人眼对亮度和绿色更敏感。

直观表示：

```text
G R G R ...
B G B G ...
G R G R ...
B G B G ...
```

相机之后会通过 demosaicing 算法估计每个像素完整的 RGB 值。

### 13.3 Fuji EXR 和人眼 cone mosaic

PPT 还提到 Fuji EXR 和人眼视网膜 cone mosaic。

人眼有不同类型的 cone cells：

- L cones：偏红/长波；
- M cones：偏绿/中波；
- S cones：偏蓝/短波。

PPT 指出蓝锥细胞较少，fovea 中甚至没有蓝锥细胞。这说明视觉系统本身也不是简单均匀采样 RGB。

---

## 14. Image resolution：图像分辨率

### 14.1 分辨率与采样

这一讲中的 resolution 特指 sampling resolution。

即：

> Resolution = number of pixels per unit area.

如果同一场景用更多采样点表示，图像细节更丰富。

PPT 展示了同一图像在不同采样尺寸下的效果，例如：

```text
512 → 256 → 128 → 64 → 32
```

采样数越低，图像越模糊、越 blocky。

### 14.2 低分辨率为什么 blocky？

低分辨率图像中，单个 pixel 代表更大的真实区域。

当放大显示时，每个 pixel 会变成明显的大块，因此看起来 blocky。

### 14.3 线性分辨率和数据量

如果图像宽高都加倍：

```text
M × N → 2M × 2N
```

总像素数变为：

$$
(2M)(2N)=4MN
$$

所以线性分辨率加倍，数据量大约增加 4 倍。

如果宽高都减半：

```text
M × N → M/2 × N/2
```

总像素数变为：

$$
\frac{MN}{4}
$$

---

## 15. Image sampling methods：图像采样方法

PPT 中提到两类采样方式。

### 15.1 Uniform sampling：均匀采样

Uniform sampling 指在所有区域使用相同采样频率。

优点：

- 简单；
- 容易存储成规则矩阵；
- 符合大多数图像文件格式。

缺点：

- 平坦区域可能采样过多；
- 复杂细节区域可能采样不够。

### 15.2 Adaptive sampling：自适应采样

Adaptive sampling 指在细节更多的区域使用更高采样频率，在平坦区域使用较低采样频率。

优点：

- 更有效利用存储；
- 可作为压缩策略；
- 在重要区域保留更多细节。

例子：

- 人脸区域比背景采样更密；
- 边缘和纹理区域保留更多像素；
- 平坦天空区域减少采样。

---

## 16. Sampling effects：采样误差与锯齿

### 16.1 斜线的离散表示

PPT 提问：如何用离散像素值表示一条连续直线？

连续世界中的斜线是平滑的，但在像素网格上只能用有限像素近似。

结果可能出现：

- stair-step effect 阶梯状；
- jagged edges 锯齿边缘；
- loss of information 信息损失。

### 16.2 提高分辨率是否能完全解决？

PPT 明确说：

> Doubling resolution does not solve the problem.

提高分辨率可以减轻锯齿，但不能从理论上完全消除采样误差。

而且代价很高：

- memory 增加；
- bandwidth 增加；
- scan conversion time 增加；
- 宽高各加倍会导致数据量约 4 倍。

### 16.3 用更多 grey levels 缓解问题

PPT 说问题可以通过更多灰度级缓解。

直观理解：

- binary image 中像素只能黑或白，边缘非常硬；
- 多灰度图中边缘附近可以用中间灰度表示部分覆盖；
- 这就是 anti-aliasing 的思想。

例如斜线边缘像素可以不是纯黑或纯白，而是灰色，从视觉上更平滑。

---

## 17. Relationship between pixels：像素邻域关系

图像中的像素不是孤立的。很多算法需要考虑一个像素和周围像素的关系。

### 17.1 4-neighbourhood

4-neighbourhood 指一个像素上下左右四个邻居：

```text
  N
W P E
  S
```

这些邻居与中心像素共享一条 edge。

### 17.2 8-neighbourhood

8-neighbourhood 包括上下左右和四个对角邻居：

```text
NW N NE
 W P E
SW S SE
```

这些邻居与中心像素共享 edge 或 corner。

### 17.3 为什么邻域重要？

邻域关系用于：

- edge detection；
- segmentation；
- connected component labeling；
- morphology；
- shape representation；
- region growing。

### 17.4 形状表示中的内外边界

PPT 提到 shape representation，可用像素之间的关系表示形状：

- internal boundary 内边界；
- external boundary 外边界；
- inter-pixel boundary 像素间边界。

不同邻域定义会影响一个区域是否连通、边界怎样被描述。

---

## 18. Quantization：量化

### 18.1 量化定义

PPT 定义：

> Image quantization represents measured value at the sampled point by an integer.

也就是说，采样得到的是某个位置的真实亮度，但真实亮度可能是连续值；量化把这个连续值替换成有限整数。

例如：

```text
真实亮度 0.532 → 8-bit 灰度值 136
```

量化后的数值称为 grey levels。

### 18.2 量化级数

如果用 $B$ bit 表示一个像素，则可用灰度级数为：

$$
L=2^B
$$

最大整数值为：

$$
L-1=2^B-1
$$

例子：

| bit depth $B$ | grey levels $L$ | 值范围 |
|---:|---:|---|
| 1 bit | 2 | 0-1 |
| 3 bit | 8 | 0-7 |
| 4 bit | 16 | 0-15 |
| 8 bit | 256 | 0-255 |
| 16 bit | 65536 | 0-65535 |

### 18.3 Digital image visualization

对于 $L=256$ 的 8-bit 灰度图：

- 0 映射为 black；
- 255 映射为 white；
- 中间值线性映射为不同灰度。

例如：

$$
0 \rightarrow \text{black}
$$

$$
127 \rightarrow \text{middle grey}
$$

$$
255 \rightarrow \text{white}
$$

---

## 19. Intensity resolution：强度分辨率

### 19.1 定义

PPT 中说 intensity resolution 指：

> How accurately a pixel's grey level represents the brightness of the corresponding point in the original scene.

也就是：像素灰度值能多精细地表示真实场景亮度。

它由量化 bit 数决定。

### 19.2 bit 数越多，亮度越细腻

如果 bit 数多，则可用灰度等级多，亮度变化更平滑。

例如：

- 8 bit：256 levels，看起来较连续；
- 4 bit：16 levels，可能出现明显亮度跳变；
- 1 bit：只有黑白，细节大量丢失。

### 19.3 bit 数和存储的 trade-off

更多 bit 提高质量，但也增加存储。

对于灰度图：

$$
\text{Size(bits)}=M\times N\times B
$$

对于 RGB 图像：

$$
\text{Size(bits)}=M\times N\times 3\times B
$$

所以：

```text
more bits → better intensity resolution → larger file size
```

---

## 20. False contours：伪轮廓

### 20.1 什么是 false contours？

当量化级数太少时，原本平滑变化的亮度会变成一层一层的区域。

这种不真实的亮度边界叫：

> false contours 伪轮廓

例如天空从亮到暗本应平滑渐变，但如果只有 16 个灰度级，可能出现明显条带。

### 20.2 为什么会产生？

因为一大段连续亮度范围被映射到同一个灰度级。

PPT 中解释：

> With fewer bits, a wider range of intensities in the original scene is mapped into a single grey level.

也就是：量化太粗，很多不同亮度被迫变成同一个整数。

---

## 21. Dithering and halftoning

### 21.1 为什么需要 dithering 和 halftoning？

PPT 说 coarse quantization 容易导致 abrupt discontinuities，也就是 false contours。

Dithering 和 halftoning 利用了人类视觉系统的空间平均特性：

> 当 HVS 面对大面积高频颜色或亮度变化时，会把局部像素混合感知成一个均匀区域。

所以即使设备只能显示有限颜色，也可以通过空间排列产生更多“感知颜色”。

### 21.2 Dithering：抖动

PPT 定义：

> Dithering adds a small amount of random noise to the signal before quantizing.

直观理解：

```text
量化前加入少量噪声
→ 避免大面积像素全被量化成同一等级
→ 打散 false contours
→ 人眼感知更自然
```

它会随机把某些像素分配到更高或更低量化等级，从而制造中间亮度的视觉幻觉。

> [!important] 重要结论
> Dithering 会降低客观 SNR，但可能提高主观视觉质量。

### 21.3 Halftoning：半色调

Halftoning 指用黑白像素组合产生灰度感。

典型例子：报纸和杂志印刷。

如果一个区域中黑点多，视觉上更暗；白点多，视觉上更亮。

```text
更多黑点 → darker grey
更多白点 → lighter grey
```

### 21.4 Classical halftoning

Classical halftoning 使用不同大小的点表示不同强度。

- 小黑点：浅灰；
- 大黑点：深灰；
- 密集黑点：接近黑色。

### 21.5 Mach banding

PPT 提到 Mach-banding：人眼会放大相邻亮度带之间的差异。

当显示设备只有很少颜色或灰度级时，人眼可能更容易看到条带边界，因此需要 dithering。

---

## 22. Quantization methods：量化方法

### 22.1 Uniform or linear quantization

Uniform quantization 指强度值线性映射到灰度级。

例如把 $[0,1]$ 均匀分成 256 份：

$$
0 \rightarrow 0,\quad 1 \rightarrow 255
$$

优点：

- 简单；
- 易实现；
- 适合均匀分布或一般显示。

缺点：

- 不考虑人眼对不同亮度区域的敏感程度；
- 不考虑输入信号概率分布。

### 22.2 Logarithmic quantization

Logarithmic quantization 在暗部提供更高强度分辨率。

PPT 说明原因：

> The human eye is logarithmic.

也就是说，人眼对亮度的感知不是线性的。在暗区域，人眼可能对相对变化更敏感，因此可以给暗部更多量化级。

### 22.3 Non-uniform quantization

Non-uniform quantization 适合信号概率分布不均匀的情况。

核心思想：

- 常出现或重要的强度范围分配更多量化级；
- 不常出现或不重要的范围分配较少量化级。

它也可以考虑 HVS 特性。

---

## 23. Gamma transformation：伽马变换

### 23.1 公式

PPT 给出 gamma transformation：

$$
f' = f^\gamma
$$

通常假设输入强度已经归一化：

$$
0\le f\le 1
$$

### 23.2 gamma 的效果

| gamma | 效果 | 直观解释 |
|---:|---|---|
| $\gamma<1$ | 强调/拉开暗部 | 暗区域被提亮，阴影细节更明显 |
| $\gamma=1$ | 不变 | 线性映射 |
| $\gamma>1$ | 强调亮部、压暗暗部 | 高亮区域差异更突出 |

例如：

$$
0.25^{0.5}=0.5
$$

所以当 $\gamma<1$ 时，低强度值会变大，图像暗部被提亮。

### 23.3 为什么 gamma 重要？

Gamma transformation 可以：

- 建模 human perception；
- 做 gamma correction；
- 改善显示效果；
- 增强暗部或亮部细节。

---

## 24. Common quantization levels：常见量化等级

PPT 总结了常见 bit depth：

| $n$ | 最大值 $2^n-1$ | 类型/用途 |
|---:|---:|---|
| 1 | 1 | binary image，只有黑白 |
| 8 | 255 | 1 byte，非常常见的灰度图 |
| 16 | 65535 | research、医学或科学图像常见 |
| 24 | RGB 每通道 8 bit | 常见 true colour image |

注意：24-bit colour 通常表示：

$$
8\text{ bits Red}+8\text{ bits Green}+8\text{ bits Blue}
$$

即：

$$
3\times 8=24\text{ bits/pixel}
$$

---

## 25. Colour quantization：颜色量化

### 25.1 每个颜色通道可以分别量化

RGB 图像可以分别量化：

```text
R channel
G channel
B channel
```

这很简单，但 PPT 指出不一定令人满意。

原因是：

- 人眼对不同颜色通道敏感度不同；
- RGB 中的距离不一定对应人眼感知距离；
- 有些颜色组合比单独通道更重要。

### 25.2 不同通道可以不同采样/量化

PPT 提到：一些 colour components 可以：

- quantized with different steps；
- sampled with different steps。

例如视频压缩中常见 chroma subsampling，就是利用人眼对亮度比色度更敏感。

### 25.3 Colour quantization 的思想

PPT 图中提到在 Red/Green plane 中选择一些 colours sites，并形成 Voronoi regions。

直观理解：

1. 原始图像可能有很多颜色；
2. 算法选择有限个代表颜色；
3. 每个原始颜色映射到最近的代表颜色；
4. 最终图像颜色数减少，文件更小。

---

## 26. Look-up table, LUT

### 26.1 LUT 是什么？

Look-up table 是一个颜色索引表。

它用较小的 index 存储像素，再用表查出真实 RGB 值。

例如：

| index | R | G | B |
|---:|---:|---:|---:|
| 0 | 10 | 10 | 10 |
| 1 | 10 | 20 | 30 |
| 2 | 30 | 100 | 20 |

图像矩阵中存的不是完整 RGB，而是 index：

```text
0, 1, 2, 2, 0, ...
```

显示时再通过 LUT 转成 RGB。

### 26.2 LUT 的好处

- 减少存储；
- 易于改变颜色映射；
- 适合 palette image；
- 可用于科学可视化。

### 26.3 False colour images 是特殊 LUT

PPT 说 false colour image 是一种 special look-up table。

例如把灰度值映射到颜色：

```text
low value → blue
middle value → green/yellow
high value → red
```

这在医学图像、热成像、遥感图像中非常常见。

---

## 27. Choice of sampling and quantization：如何选择采样和量化？

PPT 给出几个判断问题。

### 27.1 图像内容是什么？

如果图像有大量细节，例如文字、边缘、纹理，就需要更高 spatial resolution。

如果图像大部分是平滑区域，可以使用较低采样或更强压缩。

### 27.2 图像用途是什么？

不同用途需要不同质量：

| 用途 | 需求 |
|---|---|
| 视觉展示 | 人眼看起来清楚即可 |
| 医学诊断 | 不能丢失关键细节 |
| 机器分析 | 特征必须保留 |
| 网络预览图 | 可以牺牲部分质量换速度 |
| 打印出版 | 需要高空间分辨率 |

### 27.3 内存和速度限制

更高分辨率和更高 bit depth 会增加：

- memory；
- storage；
- bandwidth；
- processing time；
- display time。

### 27.4 需要哪些信息？

要根据任务决定保留什么信息：

- color resolution；
- spatial resolution；
- grey-level resolution；
- texture；
- shape；
- edges。

---

## 28. Digital image quality factors：图像质量因素

PPT 总结了两个主要因素。

### 28.1 Spatial resolution

Spatial resolution 由 spatial sampling 控制。

决定：

- 图像能表示多少空间细节；
- 边缘是否清晰；
- 小物体是否可见；
- 放大后是否 blocky。

### 28.2 Intensity resolution

Intensity resolution 由 quantization levels 控制。

决定：

- 亮度变化是否平滑；
- 是否出现 false contours；
- 暗部和亮部细节是否可分辨。

### 28.3 trade-off

提高任一因素都会增加文件大小和计算成本。

```text
higher spatial resolution → more pixels
higher intensity resolution → more bits per pixel
both → larger image file
```

---

## 29. Zooming and shrinking：放大与缩小

### 29.1 Zooming

PPT 说 zooming 可以看作 oversampling。

放大图像需要：

1. 创建新的 pixel locations；
2. 给这些新位置分配 grey level；
3. 这个分配过程需要 interpolation。

常见方法：

- pixel replication；
- nearest neighbour interpolation；
- bilinear interpolation。

### 29.2 Shrinking

Shrinking 可以看作 undersampling。

如果图像太大，会带来：

- 需要太多 memory；
- processing time 太长；
- 图像太大无法完整显示。

因此可以通过 sub-sampling 得到更小图像。

---

## 30. Sub-sampling：下采样

### 30.1 基本方法

Sub-sampling 指按照某种模式移除像素。

最简单方法：

> skipping pixels 跳过像素。

例如 2:1 subsampling：

```text
保留每隔一个像素
丢弃其余像素
```

如果每隔一行一列保留，宽高各减半。

### 30.2 尺寸变化

如果原图是：

$$
M\times N
$$

宽高各减半后：

$$
\frac{M}{2}\times \frac{N}{2}
$$

总像素数变为：

$$
\frac{MN}{4}
$$

所以 1/2 linear size 对应 1/4 pixel count。

### 30.3 为什么 sub-sampled images 质量低？

PPT 提问：The sub-sampled images are of low quality. Why?

原因包括：

- 细节被丢弃；
- 高频信息没有先过滤；
- 产生 aliasing；
- 纹理和边缘被错误表示；
- 放大查看时 blocky。

更好的做法通常是：

```text
low-pass filtering → sub-sampling
```

先去掉会混叠的高频成分，再降低采样率。

---

## 31. Up-sampling：上采样

### 31.1 目标

Up-sampling 的目标是增加图像分辨率。

但新像素不是凭空知道的，需要从已有像素估计。

PPT 说：

> Requires generation of additional pixels from available ones.

### 31.2 插值的必要性

几何变换通常会产生非整数位置。例如旋转、缩放后，一个输出像素可能对应输入图像中的：

$$
(10.3, 25.7)
$$

但原图只有整数网格位置：

$$
(10,25), (10,26), (11,25), (11,26)
$$

所以必须使用 interpolation 来估计非整数位置的像素值。

---

## 32. Nearest neighbour interpolation：最近邻插值

### 32.1 插值定义

PPT 定义：

> Interpolation is the process of using known data to estimate values at unknown locations.

也就是说，插值是用已知像素估计未知位置的像素值。

### 32.2 最近邻方法

Nearest neighbour interpolation 的规则非常简单：

> 新像素复制距离它最近的已知像素值。

例如未知点离左上角像素最近，就直接复制左上角像素。

### 32.3 优缺点

| 方法 | 优点 | 缺点 |
|---|---|---|
| Nearest neighbour | 快、简单、保留原始像素值 | 放大后 blocky、边缘锯齿明显 |

最近邻适合：

- label map；
- segmentation mask；
- binary image；
- 不希望产生新类别值的图像。

不太适合自然图像高质量放大。

---

## 33. General interpolation：一般插值与映射方向

PPT 介绍了 forward mapping 和 backward interpolation。

### 33.1 Forward mapping

Forward mapping 指：

```text
input grid → output image positions
```

也就是把输入图像中的每个像素映射到输出图像。

问题：

- 输出位置可能是非整数；
- 需要再插值到输出网格；
- 可能出现 holes，即某些输出像素没人填；
- 也可能出现 redundant conversions。

### 33.2 Backward interpolation

Backward interpolation 指：

```text
for each output pixel
→ inverse map to input coordinate
→ interpolate input image value
```

即对输出图像中的每个整数网格点，反向找它在输入图像中的位置。

优点：

- 每个输出像素都会被计算；
- 不容易出现 holes；
- 只计算输出图像需要的数据；
- 因此通常更 preferred。

---

## 34. Bilinear interpolation：双线性插值

### 34.1 基本思想

Bilinear interpolation 使用一个规则网格上的 4 个已知像素估计内部点。

假设局部坐标为 $(u,v)$，其中：

$$
0\le u\le 1,\quad 0\le v\le 1
$$

四个角点为：

| 点 | 值 |
|---|---|
| 左上/左下附近 | $f_{00}$ |
| 右侧 | $f_{10}$ |
| 下/上侧 | $f_{01}$ |
| 对角 | $f_{11}$ |

常见公式为：

$$
f(u,v)=(1-u)(1-v)f_{00}+u(1-v)f_{10}+(1-u)vf_{01}+uvf_{11}
$$

### 34.2 与 PPT 公式的关系

PPT 给出：

$$
f(x,y)=ax+by+cxy+d
$$

这就是 bilinear 的一般形式。

它不是简单的一条直线，而是在 $x$ 和 $y$ 两个方向上分别做线性插值，并带有 $xy$ 项。

### 34.3 操作步骤

PPT 的解释：

1. 在水平方向对上边两个点做 linear interpolation；
2. 在水平方向对下边两个点做 linear interpolation；
3. 再在垂直方向对这两个中间结果做 linear interpolation。

### 34.4 优缺点

| 方法 | 优点 | 缺点 |
|---|---|---|
| Bilinear interpolation | 比 nearest neighbour 平滑，计算仍较简单 | 会产生一定模糊，不如更高阶方法锐利 |

---

## 35. Fourier information：幅度谱与相位谱

PPT 最后提到 Fourier transform。

### 35.1 Fourier transform 的作用

Fourier transform 可以把图像分解成：

- Amplitude spectrum 幅度谱；
- Phase spectrum 相位谱。

幅度谱表示不同频率成分有多强；相位谱表示这些频率成分在空间中的对齐方式。

### 35.2 相位比幅度更重要

PPT 提到一个实验：

1. 对两幅图像分别计算 $(A_1,P_1)$ 和 $(A_2,P_2)$；
2. 用第一幅图的 amplitude 和第二幅图的 phase 重建；
3. 用第二幅图的 amplitude 和第一幅图的 phase 重建。

结论：

> Phase is perceptually more important than amplitude.

也就是说，人眼对图像结构、边缘、空间位置更敏感，而这些信息主要由 phase 控制。

### 35.3 为什么 phase 重要？

图像中物体的形状、边缘和位置都依赖频率成分之间的相对相位。

如果只有 amplitude，没有正确 phase，图像结构可能难以识别。

---

## 36. 本节与考试的连接

### 36.1 可能考点 1：解释数字图像表示

可以这样答：

> A digital image is a sampled and quantized version of a continuous image function $f(x,y)$. It can be represented as a numerical array $g(i,j)$, where $i$ and $j$ are row and column indices and $g(i,j)$ is the pixel value.

中文：

> 数字图像是连续图像函数 $f(x,y)$ 经过空间采样和强度量化后的离散表示，可写成数值矩阵 $g(i,j)$。

### 36.2 可能考点 2：sampling 与 quantization 的区别

| 概念 | 中文 | 处理对象 | 决定 |
|---|---|---|---|
| Sampling | 采样 | 空间位置 | spatial resolution |
| Quantization | 量化 | 强度/灰度值 | intensity resolution |

答题关键词：

```text
Sampling discretizes coordinates.
Quantization discretizes intensity values.
```

### 36.3 可能考点 3：Nyquist theorem

公式：

$$
f_s\ge 2f_{max}
$$

说明：采样率至少应为信号最高频率的两倍，否则会产生 aliasing。

图像中可以联系：

- jagged edges；
- moiré patterns；
- sub-sampling artifacts。

### 36.4 可能考点 4：bit depth 与 grey levels

公式：

$$
L=2^B
$$

最大灰度值：

$$
L-1=2^B-1
$$

例子：

- 3 bit → 8 levels；
- 8 bit → 256 levels；
- 16 bit → 65536 levels。

### 36.5 可能考点 5：图像大小计算

灰度图：

$$
\text{Size(bits)}=M\times N\times B
$$

RGB 图：

$$
\text{Size(bits)}=M\times N\times 3\times B
$$

如果 $B=8$，RGB 图像每像素 3 bytes。

### 36.6 可能考点 6：4-neighbourhood vs 8-neighbourhood

| 邻域 | 包含像素 | 共享关系 |
|---|---|---|
| 4-neighbourhood | 上、下、左、右 | shared edge |
| 8-neighbourhood | 上、下、左、右 + 四个对角 | shared edge or corner |

### 36.7 可能考点 7：dithering 与 halftoning

Dithering：

> Add noise before quantization to break false contours and improve perceived quality.

Halftoning：

> Use black and white dot patterns to create the perception of grey levels.

### 36.8 可能考点 8：gamma transformation

公式：

$$
f'=f^\gamma
$$

- $\gamma<1$：提亮/拉开暗部；
- $\gamma>1$：强调亮部、压暗暗部；
- 用于建模和补偿人眼/显示设备的非线性感知。

### 36.9 可能考点 9：nearest neighbour vs bilinear interpolation

| 方法 | 使用像素 | 效果 | 特点 |
|---|---|---|---|
| Nearest neighbour | 最近的 1 个像素 | blocky | 快、简单 |
| Bilinear | 周围 4 个像素 | smoother | 更自然但可能模糊 |

### 36.10 可能考点 10：为什么下采样前要低通滤波？

因为下采样降低了采样率。如果高频信息仍存在，就可能违反 Nyquist theorem，导致 aliasing。

所以常见流程是：

```text
low-pass filtering → sub-sampling
```

---

## 37. 本节关键词表

| 英文 | 中文 | 解释 |
|---|---|---|
| Image representation | 图像表示 | 图像在数学和计算机中的表达方式 |
| Continuous image | 连续图像 | 定义在连续坐标上的 $f(x,y)$ |
| Discrete image | 离散图像 | 采样量化后的 $g(i,j)$ |
| Sampling | 采样 | 将连续空间坐标离散化 |
| Quantization | 量化 | 将连续强度值离散成整数 |
| Pixel | 像素 | 连续 2D 函数在某位置的样本 |
| Grey level | 灰度级 | 量化后的亮度整数值 |
| Spatial resolution | 空间分辨率 | 单位面积内像素数量 |
| Intensity resolution | 强度分辨率 | 灰度/亮度量化精细程度 |
| Bit depth | 位深 | 每个像素或通道使用的 bit 数 |
| Nyquist theorem | 奈奎斯特定理 | 采样率至少为最高频率两倍 |
| Aliasing | 混叠 | 采样不足导致高频伪装成低频 |
| Scanline | 扫描线 | 图像中的一行采样像素 |
| Bayer filter | 拜耳滤镜 | 相机常用 RGB 颜色采样阵列 |
| 4-neighbourhood | 4 邻域 | 与中心像素共享边的四个邻居 |
| 8-neighbourhood | 8 邻域 | 共享边或角的八个邻居 |
| False contours | 伪轮廓 | 量化级数不足导致的条带边界 |
| Dithering | 抖动 | 加噪打散量化伪轮廓 |
| Halftoning | 半色调 | 用黑白点模式产生灰度感 |
| Uniform quantization | 均匀量化 | 等间隔量化强度值 |
| Logarithmic quantization | 对数量化 | 暗部给予更高分辨率 |
| Gamma transformation | 伽马变换 | $f'=f^\gamma$ 的非线性强度变换 |
| LUT | 查找表 | 用 index 映射到 RGB 或颜色值 |
| False colour | 假彩色 | 用颜色映射显示非真实颜色信息 |
| Sub-sampling | 下采样 | 删除像素以缩小图像 |
| Up-sampling | 上采样 | 增加像素以放大图像 |
| Interpolation | 插值 | 用已知像素估计未知位置值 |
| Nearest neighbour | 最近邻 | 复制最近像素值 |
| Bilinear interpolation | 双线性插值 | 用周围 4 个像素做线性估计 |
| Fourier phase | 傅里叶相位 | 对图像结构和感知非常重要 |

---

## 38. 复习自测题

1. 连续图像 $f(x,y)$ 和数字图像 $g(i,j)$ 有什么区别？
2. 为什么说 pixel 不是 little square，而是 sample？
3. Sampling 和 quantization 分别离散化什么？
4. Spatial resolution 和 intensity resolution 分别由什么控制？
5. 8-bit 灰度图有多少 grey levels？最大值是多少？
6. 一张 $512\times512$ 的 8-bit 灰度图需要多少 bits 和 bytes？
7. 一张 $512\times512$ 的 RGB 8-bit 图像需要多少 bytes？
8. Nyquist theorem 的公式是什么？采样不足会造成什么？
9. 为什么下采样可能导致 aliasing？
10. 宽高都加倍时，图像像素数和存储量大约增加多少倍？
11. 4-neighbourhood 和 8-neighbourhood 的区别是什么？
12. False contours 是如何产生的？
13. Dithering 为什么能改善主观视觉质量？为什么它又会降低 SNR？
14. Halftoning 如何用黑白像素产生灰度感？
15. Uniform quantization 和 logarithmic quantization 有什么区别？
16. Gamma transformation 中 $\gamma<1$ 和 $\gamma>1$ 分别有什么效果？
17. LUT 如何用于 colour quantization？
18. 为什么 false colour image 可以看作一种特殊 LUT？
19. Nearest neighbour interpolation 为什么会 blocky？
20. Bilinear interpolation 使用几个像素？公式中的 $xy$ 项说明了什么？
21. Forward mapping 和 backward interpolation 哪个更常用？为什么？
22. Fourier transform 中 amplitude 和 phase 哪个对感知更重要？为什么？

---

## 39. 一句话总结

本节课的核心是：**数字图像是连续图像 $f(x,y)$ 经过空间采样和强度量化得到的数值矩阵 $g(i,j)$；sampling 决定空间分辨率，quantization 决定强度分辨率，sub-sampling 会缩小图像但可能造成混叠，interpolation 用于放大和几何变换时估计新像素。**
---

