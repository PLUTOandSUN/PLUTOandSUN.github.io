---
title: EBU6230 Paper B 2023-24 逐题答案与考点
tags:
  - 图像与视频处理
  - EBU6230
  - 复习
  - 考点整理
aliases:
  - EBU6230 Solutions B 2023-24 逐题整理
source: "[[课程笔记/图像与视频处理/附件/Solutions_2324_EBU6230B_.pdf]]"
created: 2026-06-15
---

# EBU6230 Paper B 2023/24 逐题答案与考点

> [!info] 使用说明
> 本笔记根据 [[课程笔记/图像与视频处理/附件/Solutions_2324_EBU6230B_.pdf|Solutions_2324_EBU6230B_.pdf]] 整理。每一小题都包含：**原题**、**参考答案**、**相关考点**、**课程内容关联**和**易错提醒**。答案以 PDF 标答为主，并补充考试时可写出的解释。

## 课程资料对应关系

- Part 1：图像表示、采样、量化、直方图
  - [[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/1 EBU6230_L1_introduction_to_image_processing.pdf|L1 Introduction to Image Processing]]
  - [[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/2 EBU6230_L2_imagerep.pdf|L2 Image Representation]]
  - [[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/3 EBU6230_L3_histograms_updated.pdf|L3 Histograms]]
- Part 2：图像变换、颜色图像、滤波
  - [[课程笔记/图像与视频处理/附件/Part 2 - Image Transformation, Colour Images and Image Filtering/4 EBU6230_image_transformations.pdf|Image Transformations]]
  - [[课程笔记/图像与视频处理/附件/Part 2 - Image Transformation, Colour Images and Image Filtering/5 EBU6230_colour_image.pdf|Colour Image]]
  - [[课程笔记/图像与视频处理/附件/Part 2 - Image Transformation, Colour Images and Image Filtering/6 EBU6230_image_filtering.pdf|Image Filtering]]
- Part 3：边缘、兴趣点、形态学
  - [[课程笔记/图像与视频处理/附件/Part 3 - Edges, Interest points, and Morphology/3-3_Interest points.pdf|Interest Points]]
  - [[课程笔记/图像与视频处理/附件/Part 3 - Edges, Interest points, and Morphology/3-4_Morphology.pdf|Morphology]]
- Part 4：压缩、序列、MPEG-7
  - [[课程笔记/图像与视频处理/附件/Part 4 - Image Compression (JPEG2000), Image Sequences, MPEG7/4-1_Image Compression_updated.pdf|Image Compression / JPEG2000]]
  - [[课程笔记/图像与视频处理/附件/Part 4 - Image Compression (JPEG2000), Image Sequences, MPEG7/4-2_Sequences_updated.pdf|Image Sequences / Motion Estimation]]

## 试卷结构总览

| 题号 | 主题 | 主要考点 | 对应课程 |
|---|---|---|---|
| Q1(a) | True / False | false colour、dithering、HVS logarithmic、median filter | L1, L2, Image Filtering |
| Q1(b)(c) | Histograms | 直方图定义、低对比度、彩色图像 intensity histogram、曝光问题、几何不变性 | L3 Histograms |
| Q1(d) | Upsampling | 上采样、插值、分辨率、伪影 | L2 Image Representation |
| Q2(a) | Image Transformation | algebraic operation、background subtraction、normalization、shear、scaling | Image Transformations |
| Q2(b) | Colour Images | RGB-CMY、加色/减色模型、三色理论、对立过程理论 | Colour Image |
| Q2(c) | Image Formats | PGM header、P5、width/height、maximum value、comment | Colour Image |
| Q3(a) | Morphology | dilation、structuring element、opening、noise removal | Morphology |
| Q3(b) | Interest Points | Moravec operator、SAD/SSD、Harris detector | Interest Points |
| Q4(a) | Motion Estimation | Taylor expansion、gradient method、block matching、SSD/MSE | Image Sequences |
| Q4(b) | JPEG2000 | ROI coding、static ROI、dynamic ROI | Image Compression |

---

# Question 1

## Q1(a) True or False

### 原题

> State TRUE or FALSE for the following statements:  
> i) “False colour images are usually created to reduce the image file size.”  
> ii) “Dithering decreases the SNR yet improves the perceived quality of the output.”  
> iii) “Human eye perceives brightness on a logarithmic scale, not linear.”  
> iv) “Median filters are used to reduce noises while preserving edges.”

### 参考答案

| 小题  | 答案        | 解释                                                                                          |
| --- | --------- | ------------------------------------------------------------------------------------------- |
| i   | **False** | False colour 主要用于把灰度或不可见信息映射成颜色，从而突出组织边界、边缘、血流、温度、遥感类别等信息；它不是为了减小文件大小。                      |
| ii  | **True**  | Dithering 会向量化前信号加入噪声或空间扰动，因此客观 SNR 会下降；但它能打散 false contours / banding，让人眼感觉更平滑，所以主观质量可能提高。 |
| iii | **True**  | 人眼对亮度的感知近似是对数式而非线性式；因此暗部需要更高强度分辨率，gamma / logarithmic quantization 都与此相关。                   |
| iv  | **True**  | Median filter 是非线性滤波器，用邻域中值替换像素，对 salt-and-pepper noise 很有效，同时比均值滤波更能保留边缘。                  |

### 相关考点

- **False colour images**：用 LUT 或颜色映射突出重要结构，不等于压缩。
- **Dithering / halftoning**：加入噪声或图案，使有限灰度/颜色产生更连续的视觉效果。
- **SNR 与 perceived quality 的区别**：客观误差增加不一定代表人眼感知更差。
- **HVS brightness perception**：人眼对亮度敏感度非线性，暗部更敏感。
- **Median filter**：非线性排序统计滤波，常用于椒盐噪声，并能较好保护边缘。

### 课程内容关联

- False colour：[[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/1 EBU6230_L1_introduction_to_image_processing.pdf|L1]] false colour medical example；[[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/2 EBU6230_L2_imagerep.pdf|L2]] LUT / false colour。
- Dithering：[[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/2 EBU6230_L2_imagerep.pdf|L2]] Dithering and halftoning。
- Logarithmic brightness：[[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/2 EBU6230_L2_imagerep.pdf|L2]] Quantization methods。
- Median filter：[[课程笔记/图像与视频处理/附件/Part 2 - Image Transformation, Colour Images and Image Filtering/6 EBU6230_image_filtering.pdf|Image Filtering]] median filter。

### 易错提醒

- False colour 和 compression 没有必然关系，不能看到“colour”就联想到文件大小。
- Dithering 的关键词是“**降低 SNR，但提升视觉感知**”。
- Median filter 不是线性卷积滤波器，答题时可以强调 **non-linear**。

---

## Q1(b) Image Histograms

## Q1(b)(i)

### 原题

> Figure 1 shows a histogram of an image that can be used to reveal the image contrast. What does this histogram tell about the image?

Figure 1 的直方图大部分像素集中在较低灰度区域，并且只占据较窄灰度范围。

### 参考答案

该直方图说明：图像中大多数 intensity values 集中在**暗部的较窄范围**内，因此图像是 **low-contrast image** 或 **dark image**。

可写成考试答案：

> Most intensity values are concentrated in a narrow range in the dark region. Therefore, the image is dark / under-contrasted / low contrast.

### 相关考点

- **Histogram 反映灰度分布，而不是空间分布**。
- 如果像素集中在左侧：整体偏暗。
- 如果灰度只占窄范围：动态范围小，通常低对比度。
- 低对比度图像可用 histogram stretching 或 histogram equalization 改善。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/3 EBU6230_L3_histograms_updated.pdf|L3 Histograms]]：histogram definition、contrast、dynamic range、bad exposure。

### 易错提醒

- “集中在左边”强调 **dark / underexposed tendency**。
- “范围窄”强调 **low contrast**。
- 两点都写会更稳。

---

## Q1(b)(ii)

### 原题

> How do you represent a colour image histogram using the intensity histogram?

### 参考答案

先把 colour image 转换为 greyscale image，然后显示该灰度图像的 histogram。

考试可写：

> Convert the colour image to a greyscale image, then compute and display the histogram of the greyscale intensity values.

### 相关考点

- 彩色图像直方图常见两种：
  1. **Intensity histogram**：先转灰度，再统计灰度强度。
  2. **Individual channel histograms**：分别统计 R、G、B 三个通道。
- Intensity histogram 能反映亮度、对比度、曝光和动态范围，但**不能完整表示颜色分布**。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/3 EBU6230_L3_histograms_updated.pdf|L3 Histograms]]：Colour image histograms。

### 易错提醒

- 题目问的是 **using the intensity histogram**，所以不要答成只画 R/G/B 三个通道。
- 可以补充“另一种方法是 RGB channel histograms”，但主答案必须是“转灰度后统计”。

---

## Q1(b)(iii)

### 原题

> Consider the greyscale chess board image in Figure 2 (made with black and white squares).  
> Draw a labelled sketch of the image histogram, where the intensity value 0 represents black and the intensity value 255 represents white.  
> Now, consider rotating the chess-board image by 90 degrees. What effect, if any, would this have on the histogram? Explain your answer.

### 参考答案

棋盘图只包含黑白两种灰度：

- 黑色：intensity value = 0
- 白色：intensity value = 255

所以直方图应该只有两个主要脉冲/柱：

```text
N = H(D)
^
|      |                 |
|      |                 |
+------+-----------------+----> D, gray level
       0                255
```

如果黑白方块数量相同，0 和 255 处柱高相同；如果数量略不同，则柱高按黑白像素数对应变化。横轴是 **Gray-level, D**，纵轴是 **Number of pixels, N = H(D)**。

旋转 90 度后：**No effect**。因为旋转只改变像素的空间位置，相当于重新排列像素坐标；每个灰度值的像素数量没有变化，所以直方图不变。

### 相关考点

- Histogram 统计的是每个灰度值出现的次数。
- Histogram 不包含空间位置信息。
- Histogram 对某些几何操作不变，例如 rotation、mirroring、skew 等，前提是灰度值集合及数量不改变。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/3 EBU6230_L3_histograms_updated.pdf|L3 Histograms]]：histogram properties；histogram is invariant to certain geometric image operations。

### 易错提醒

- 旋转后图像看起来变了，但 histogram 不变。
- 不能说“棋盘旋转后黑白互换”；旋转不是 negative transformation，不改变灰度值。

---

## Q1(c) Histograms and Exposure

## Q1(c)(i)

### 原题

> Explain what a spike on the LEFT side of an image histogram indicates.

### 参考答案

直方图左侧 spike 表示图像中有大量低灰度/暗像素，通常说明图像 **underexposed**，原因是到达传感器的光线不足，导致许多像素强度值偏低。

### 相关考点

- Histogram 左侧对应 low intensity / dark region。
- 左侧堆积可能意味着 underexposure、shadow clipping、细节丢失在暗部。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/3 EBU6230_L3_histograms_updated.pdf|L3 Histograms]]：Detecting bad exposure using histograms。

### 易错提醒

- 左侧是暗，不是亮。
- 如果 spike 贴着最左端，可能有黑场裁剪；如果只是偏左但仍分散，则可能只是整体偏暗。

---

## Q1(c)(ii)

### 原题

> Explain what a spike on the RIGHT side of an image histogram indicates.

### 参考答案

直方图右侧 spike 表示图像中有大量高灰度/亮像素，通常说明图像 **overexposed**，原因是光线太多，导致许多像素接近最大强度值。

### 相关考点

- Histogram 右侧对应 high intensity / bright region。
- 右侧堆积可能意味着 overexposure、highlight clipping、高光细节丢失。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/3 EBU6230_L3_histograms_updated.pdf|L3 Histograms]]：overexposed / underexposed。

### 易错提醒

- 右侧 spike 不是“高对比度”的充分条件；它更多表示亮部过多或曝光过度。

---

## Q1(d) Upsampling in Image Processing

## Q1(d)(i)

### 原题

> Define the process of upsampling in the context of digital image processing.

### 参考答案

Upsampling 是指通过在已有像素之间加入新的像素来提高图像分辨率。新增像素的数值通常通过插值方法计算，例如 nearest-neighbour、bilinear 或 bicubic interpolation。

### 相关考点

- Upsampling = oversampling / zooming / increasing resolution。
- 关键动作：创建新的 pixel locations，再给这些位置赋灰度或颜色值。
- 插值不是创造真实新信息，而是估计未知位置的值。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/2 EBU6230_L2_imagerep.pdf|L2 Image Representation]]：Zooming and shrinking、Up-sampling、Nearest neighbour interpolation、Bilinear interpolation。

### 易错提醒

- Upsampling 和 downsampling / subsampling 相反。
- “增加像素数”不等于“增加真实细节”。

---

## Q1(d)(ii)

### 原题

> Explain why upsampling is necessary when processing digital images.

### 参考答案

当需要更高分辨率图像时，上采样是必要的。例如：

- 把小图放大到更大显示屏或打印尺寸，减少明显 pixelation。
- 在 zooming、image warping、geometric transformation 中，需要为输出网格生成像素。
- 为后续编辑、标注、配准或视觉显示提供更细的采样网格。

### 相关考点

- 几何变换后很多输出像素位置不是原图整数坐标，需要 interpolation。
- Inverse warping 中，要从输出像素反查源图连续坐标并插值。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/2 EBU6230_L2_imagerep.pdf|L2 Image Representation]]：up-sampling objective。
- [[课程笔记/图像与视频处理/附件/Part 2 - Image Transformation, Colour Images and Image Filtering/4 EBU6230_image_transformations.pdf|Image Transformations]]：inverse warping and interpolation。

### 易错提醒

- 答题时最好同时写“显示需求”和“几何变换/处理需求”，避免只写一个例子。

---

## Q1(d)(iii)

### 原题

> Describe a scenario where upsampling could be detrimental to an image.

### 参考答案

如果对低分辨率图像过度 upsampling，新增像素是插值得到的人工估计，会导致图像模糊、过软、边缘不清或出现插值伪影。对于医学影像、法医图像、机器视觉检测等需要细节真实性的场景，这些人工像素可能造成误判。

### 相关考点

- Interpolation may blur the result slightly。
- Upsampling 不会恢复不存在的细节。
- 低质量源图被放大后，噪声、压缩块、锯齿和模糊也可能更明显。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 1 - Introduction, Image Representation, Histograms/2 EBU6230_L2_imagerep.pdf|L2 Image Representation]]：nearest-neighbour and bilinear interpolation。

### 易错提醒

- 不要只写“文件变大”；题目问 detrimental to image，重点是画质和解释可信度。

---

# Question 2

## Q2(a) Image Transformation

## Q2(a)(i)

### 原题

> Which type of transformation is used to remove the background from an image?

### 参考答案

使用 **algebraic transformation**，更具体地说是 **image subtraction / background subtraction**。

可写公式：

$$
g(x,y)=f(x,y)-h(x,y)
$$

其中 $f(x,y)$ 是含前景的图像，$h(x,y)$ 是背景图像，差分结果 $g(x,y)$ 突出前景或变化区域。

### 相关考点

- Algebraic operations 是逐像素 arithmetic / logical operations。
- Image subtraction 用于增强两幅图之间的差异。
- Background subtraction 常用于前景检测、运动检测和监控视频。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 2 - Image Transformation, Colour Images and Image Filtering/4 EBU6230_image_transformations.pdf|Image Transformations]]：algebraic operations、image subtraction、background subtraction。

### 易错提醒

- 这题不是问 segmentation algorithm，也不是问 geometric transformation。
- 关键词：**algebraic transformation - subtraction**。

---

## Q2(a)(ii)

### 原题

> Algebraic operations (e.g., addition, multiplication, etc.) between two greyscale images may occur clipping (i.e., pixel values may exceed the range (0, ..., 255)). How do you ensure that the pixel values after an algebraic operation are within the range?

### 参考答案

通过 **normalization** 把运算后的像素值映射回 $[0,255]$ 范围。

常用线性归一化公式：

$$
g = c + (d-c)\frac{f-a}{b-a}
$$

其中 $f \in [a,b]$ 是原运算结果，$g \in [c,d]$ 是归一化后的结果。对于 8-bit 灰度图，通常 $c=0,d=255$。

### 相关考点

- Clipping：像素运算结果超出数据类型范围，例如 230 + 80 = 310，大于 255。
- Normalization：把结果重新缩放到合法范围，尽量保留细节。
- Clamping / clipping 虽然也能限制范围，但会造成饱和和细节损失；本题 PDF 标答是 normalization。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 2 - Image Transformation, Colour Images and Image Filtering/4 EBU6230_image_transformations.pdf|Image Transformations]]：clipping and normalization。

### 易错提醒

- 答“直接截断到 0 或 255”不如答 normalization 稳，因为题目问如何确保范围且标答明确是 normalization。

---

## Q2(a)(iii)

### 原题

> If an image requires horizontal shearing to correct for perspective distortion, and the desired shear factor is 0.3, what is the transformation matrix for this shear?

### 参考答案

水平 shear factor 为 0.3 时，二维矩阵为：

$$
Sh=\begin{bmatrix}
1 & 0.3\\
0 & 1
\end{bmatrix}
$$

对应变换：

$$
x' = x + 0.3y, \quad y' = y
$$

如果使用 homogeneous coordinates，可以写成：

$$
Sh=\begin{bmatrix}
1 & 0.3 & 0\\
0 & 1 & 0\\
0 & 0 & 1
\end{bmatrix}
$$

### 相关考点

- Shear / skew 是 affine transformation 的一种。
- 水平剪切：x 坐标随 y 变化，y 保持不变。
- 垂直剪切则相反：y 坐标随 x 变化。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 2 - Image Transformation, Colour Images and Image Filtering/4 EBU6230_image_transformations.pdf|Image Transformations]]：Affine transformation、Shear transformation。

### 易错提醒

- 不要把 0.3 放到左下角；左下角通常表示 vertical shear。
- 矩阵方向依赖课程约定，但本试卷标答使用 $\begin{bmatrix}1&0.3\\0&1\end{bmatrix}$。

---

## Q2(a)(iv)

### 原题

> Provide the transformation matrix for uniformly scaling an image to half its size while maintaining the aspect ratio.

### 参考答案

把图像等比例缩放到一半，x 和 y 方向都乘以 0.5：

$$
S=\begin{bmatrix}
0.5 & 0\\
0 & 0.5
\end{bmatrix}
$$

对应：

$$
x'=0.5x, \quad y'=0.5y
$$

如果用 homogeneous coordinates：

$$
S=\begin{bmatrix}
0.5 & 0 & 0\\
0 & 0.5 & 0\\
0 & 0 & 1
\end{bmatrix}
$$

### 相关考点

- Uniform scaling：两个方向使用相同 scale factor。
- Maintaining aspect ratio：宽高比例不变，因此 $s_x=s_y$。
- $s<1$ 表示 minification / shrinking，$s>1$ 表示 magnification / zoom。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 2 - Image Transformation, Colour Images and Image Filtering/4 EBU6230_image_transformations.pdf|Image Transformations]]：Scaling。

### 易错提醒

- “half its size” 在本题是线性尺寸变为 0.5，而不是面积变为 0.5。
- 如果面积减半，线性比例会是 $\sqrt{0.5}$，但本题标答明确为 0.5。

---

## Q2(b) Colour Images and Perception of Colours

## Q2(b)(i)

### 原题

> Describe the process of converting an RGB image to the CMY colour model and provide the formula.

### 参考答案

先把 RGB 值归一化到 $[0,1]$。然后每个 RGB 分量从 1 中减去，得到 CMY：

$$
C=1-R, \quad M=1-G, \quad Y=1-B
$$

矩阵形式：

$$
\begin{bmatrix}C\\M\\Y\end{bmatrix}
=
\begin{bmatrix}1\\1\\1\end{bmatrix}
-
\begin{bmatrix}R\\G\\B\end{bmatrix}
$$

如果是 8-bit 且不归一化，也可写作：

$$
C=255-R, \quad M=255-G, \quad Y=255-B
$$

但本课程和标答使用归一化 $[0,1]$ 形式。

### 相关考点

- RGB 是 additive colour model，常用于显示器、相机、屏幕。
- CMY 是 subtractive colour model，常用于打印。
- Cyan 吸收 Red，Magenta 吸收 Green，Yellow 吸收 Blue，因此 CMY 与 RGB 互补。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 2 - Image Transformation, Colour Images and Image Filtering/5 EBU6230_colour_image.pdf|Colour Image]]：CMY、subtractive mixture、RGB normalized。

### 易错提醒

- 不要写成 $C=R, M=G, Y=B$。
- 必须说明 RGB 已归一化到 $[0,1]$，否则公式中的 1 会让人困惑。

---

## Q2(b)(ii)

### 原题

> Why might this conversion be necessary?

### 参考答案

因为打印机使用 CMY / CMYK 油墨，是 subtractive colour model；而 RGB 是显示设备使用的 additive colour model。把 RGB 转换到 CMY 是为了适配打印流程，使屏幕颜色能转换成打印设备可使用的油墨分量。

### 相关考点

- Additive colours：红、绿、蓝光相加得到白光。
- Subtractive colours：青、品红、黄油墨吸收部分光，理论上合成黑色。
- 实际打印中常加入 K，即 CMYK，用黑色墨水获得更真实的黑色。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 2 - Image Transformation, Colour Images and Image Filtering/5 EBU6230_colour_image.pdf|Colour Image]]：additive and subtractive colours、CMY / CMYK。

### 易错提醒

- 题目问 “why necessary”，重点是 **printing process**，不是“为了压缩”或“为了灰度化”。

---

## Q2(b)(iii)

### 原题

> Explain how the trichromatic theory of colour vision and opponent-process theory contribute to our understanding of human colour perception.

### 参考答案

**Trichromatic theory** 说明：人眼视网膜中有三类 cone receptors，对红、绿、蓝附近波段敏感；通过不同强度组合，人可以感知大量颜色。它解释了为什么 RGB 三基色显示可以合成许多颜色。

**Opponent-process theory** 说明：从视网膜到大脑的颜色信息会被重新编码为对立通道，例如 red-green、blue-yellow，以及 luminance channel。它解释了为什么我们很难感知“reddish green”或“bluish yellow”这样的对立颜色，也解释了一些颜色后像现象。

因此，两种理论分别从不同层次解释颜色感知：

- Trichromatic theory：偏向 retina / cone receptor 层面。
- Opponent-process theory：偏向 brain / neural processing 层面。

### 相关考点

- Three cones：三类感光细胞。
- Opponent channels：red-green、blue-yellow、luminance。
- 两种理论不是互相排斥，而是互补。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 2 - Image Transformation, Colour Images and Image Filtering/5 EBU6230_colour_image.pdf|Colour Image]]：Trichromatic theory、Opponent-process theory。

### 易错提醒

- 不要只写“红绿蓝三色混合”而忽略 opponent-process。
- 标答按两部分给分：三色理论 2 分，对立过程理论 2 分。

---

## Q2(b)(iv)

### 原题

> Provide an example where both theories apply.

### 参考答案

一个例子是 colour television / computer screen。屏幕使用 RGB 子像素发光，刺激人眼三类 cone receptors，这体现 trichromatic theory；随后大脑将 cone signals 处理成 red-green、blue-yellow 等对立通道，从而形成完整颜色感知，这体现 opponent-process theory。

### 相关考点

- 显示设备使用 RGB additive model。
- 人眼和大脑不是直接“读 RGB 数值”，而是通过生理和神经处理形成颜色体验。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 2 - Image Transformation, Colour Images and Image Filtering/5 EBU6230_colour_image.pdf|Colour Image]]：RGB display、HVS colour perception。

### 易错提醒

- 例子要同时覆盖两种理论：设备如何产生颜色 + 人如何处理颜色。

---

## Q2(c) Image Formats

## Q2(c)(i)

### 原题

> Consider the following greyscale pixel-values:  
> 11 44 221  
> 15 0 89  
> 25 9 3  
> Write a full PGM header for this data (Binary format), including a comment line.

### 参考答案

该数据是 $3 \times 3$ 灰度图，binary PGM 的 magic number 是 **P5**。PDF 标答给出的 maximum value 是数据最大值 **221**。

```pgm
P5
# example file
3 3
221
```

评分点：

- `P5`：binary PGM magic number。
- `# example file`：comment line。
- `3 3`：width 和 height。
- `221`：maximum grey value。

### 相关考点

- PGM 存储灰度图，1 value per pixel。
- P2：ASCII PGM。
- P5：binary PGM。
- PGM/PPM header 通常包含：magic number、width height、maximum value，也可包含以 `#` 开头的 comment。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 2 - Image Transformation, Colour Images and Image Filtering/5 EBU6230_colour_image.pdf|Colour Image]]：PGM/PPM images、PGM format、magic numbers。

### 易错提醒

- Binary PGM 是 `P5`，不是 `P2`。
- 题目要求 header，不要求写后面的二进制像素数据。
- 在很多通用 PGM 文件中 max value 常写 255，但本题 PDF 标答使用给定数据最大值 221；考试按题目和标答写 221 更稳。

---

# Question 3

## Q3(a) Image Morphology - Dilation

## Q3(a)(i)

### 原题

> Describe how dilation can be useful for repairing breaks in objects within a binary image, and mention one effect of dilation that must be managed.

### 参考答案

Dilation 会向二值图像中 foreground objects 的边界添加像素，因此可以填补小间隙、连接断裂边界、修复物体中的小 breaks。

但 dilation 也会使物体变大，并可能让相邻物体合并。因此使用 dilation 时要管理的副作用是：object size increases / nearby objects may merge。

### 相关考点

- Dilation：结构元素与目标发生 hit 时，输出像素设为 1。
- 作用：填 gap、连接断裂、扩大 foreground。
- 副作用：边界膨胀、相邻物体合并、形状变粗。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 3 - Edges, Interest points, and Morphology/3-4_Morphology.pdf|Morphology]]：Structuring Element、Dilation、Dilation example。

### 易错提醒

- Dilation 与 erosion 的效果相反：dilation 扩张，erosion 收缩。
- 题目要求“repairing breaks”和“one effect to manage”，两个都要写。

---

## Q3(a)(ii)

### 原题

> Consider a binary image containing two separate square objects, each 2x2 pixels, separated by a single pixel. Perform dilation on this image using a 3x3 square structuring element. Describe the result.

### 参考答案

使用 $3 \times 3$ square structuring element 做 dilation 时，结构元素以每个 foreground pixel 为中心扩展一个像素邻域。由于两个 $2 \times 2$ 方块之间只隔一个像素，膨胀后中间间隙会被填满，因此两个方块会合并成一个更大的 rectangular object。

PDF 标答给出的结果矩阵为：

```text
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
0 0 0 0 0
0 0 0 0 0
```

更一般地说：结果不是两个独立方块，而是一个合并后的较大连通区域。

### 相关考点

- Structuring element 的大小决定膨胀范围。
- 两个物体间距小于或等于结构元素能覆盖的范围时，dilation 会把它们连接起来。
- 这就是 dilation 修复断裂与误合并相邻对象之间的 trade-off。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 3 - Edges, Interest points, and Morphology/3-4_Morphology.pdf|Morphology]]：Dilation by 3x3 square structuring element。

### 易错提醒

- 不要只说“两个方块变大”，还要写“gap filled / merge into one object”。
- 如果题目没有给具体初始矩阵，描述形状变化比死记矩阵更重要。

---

## Q3(a)(iii)

### 原题

> A binary image used for machine vision in a manufacturing process contains small specks of noise that interfere with shape analysis. How would you apply morphological operations to clean up the image, and why would this method be appropriate?

### 参考答案

应使用 **opening**，即先 erosion 后 dilation：

$$
f \circ s = (f \ominus s) \oplus s
$$

步骤：

1. **Erosion** 去除小的 isolated noise specks。
2. **Dilation** 尽量恢复主要物体的大小和形状。

这种方法适合该场景，因为噪声是小的、孤立的亮点，而 opening 能有针对性地去除比 structuring element 小的前景噪声，同时保留较大的目标物体。

### 相关考点

- Opening = erosion followed by dilation。
- 用于去除小 bright spots / salt noise。
- 结构元素大小要略大于噪声、明显小于要保留的物体结构。
- 如果问题是小黑洞或暗裂缝，通常考虑 closing；本题是 small specks of noise，所以 opening。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 3 - Edges, Interest points, and Morphology/3-4_Morphology.pdf|Morphology]]：Opening、compound morphological operations。

### 易错提醒

- Opening 顺序是 **erosion then dilation**；closing 是 **dilation then erosion**。
- 本题噪声是小 specks，优先 opening。

---

## Q3(b) Moravec Operator Calculation

## Q3(b)(i)

### 原题

> Given a grayscale image I(x, y) with a pixel of interest at location (x, y), centre a 3x3 window on this pixel. Assume the intensity values of the window are given by a 3x3 matrix, and the neighbouring windows are shifted by one pixel in the four principal directions. Calculate the Moravec interest operator value for the pixel (x, y) if the intensity values are as follows:

```text
Window shifted up:        Window shifted right:
1 0 1                     3 2 1
2 3 2                     2 4 1
1 0 1                     3 2 1

Window shifted down:      Window shifted left:
2 3 2                     1 2 3
1 0 1                     1 4 2
2 3 2                     1 2 3

Centre window:
2 1 2
1 4 1
2 1 2
```

### 参考答案

Moravec operator 对每个 shifted window 计算与 centre window 的差异，PDF 使用的是 SAD：

$$
SAD = \sum |W_c(i,j)-W_s(i,j)|
$$

#### Shifted up

$$
SAD_U=|2-1|+|1-0|+|2-1|+|1-2|+|4-3|+|1-2|+|2-1|+|1-0|+|2-1|=9
$$

#### Shifted right

$$
SAD_R=|2-3|+|1-2|+|2-1|+|1-2|+|4-4|+|1-1|+|2-3|+|1-2|+|2-1|=8
$$

#### Shifted down

PDF 标答写为：

$$
SAD_D=|2-2|+|1-3|+|2-2|+|1-1|+|4-0|+|1-1|+|2-2|+|1-3|+|2-2|=6
$$

> [!warning] 核算提醒
> 按上式逐项相加实际为 $0+2+0+0+4+0+0+2+0=8$，PDF 标答这里疑似有算术笔误。由于本笔记根据 PDF 整理，保留 PDF 标答的最终值 6；如果课堂或考试按严格计算，应向老师确认。本题 PDF 最终 Moravec value 使用的是 6。

#### Shifted left

$$
SAD_L=|2-1|+|1-2|+|2-3|+|1-1|+|4-4|+|1-2|+|2-1|+|1-2|+|2-3|=10
$$

因此 PDF 标答：

$$
Moravec(x,y)=\min(SAD_U,SAD_R,SAD_D,SAD_L)=\min(9,8,6,10)=6
$$

如果按逐项严格核算，则会得到 $\min(9,8,8,10)=8$。复习时请记住 PDF/marking scheme 版本，同时理解算法本身。

### 相关考点

- Moravec operator 是 difference-based interest operator。
- 对中心窗口与若干方向上的邻域窗口计算差异。
- 取不同方向响应的最小值作为兴趣值。
- 如果所有方向差异都大，说明该点在多个方向都有强变化，更可能是 corner / interest point。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 3 - Edges, Interest points, and Morphology/3-3_Interest points.pdf|Interest Points]]：Moravec operator、SSD/SAD over small windows。

### 易错提醒

- 题目文字说 Moravec，但 PDF 计算用的是 absolute difference；课程讲义常见表述可能是 SSD。考试中按题目/标答指定的差异度量计算。
- 最后一步是取 **minimum**，不是 maximum。
- 计算类题一定要逐项写出，哪怕结果错一点也能拿过程分。

---

## Q3(b)(ii)

### 原题

> Discuss the limitations of the Moravec operator and how the Harris corner detector improves upon it.

### 参考答案

Moravec operator 的局限：

1. 使用离散 rectangular / square window，窗口方向和形状比较粗糙。
2. 只检查有限的几个方向，不能连续地描述所有方向的强度变化。
3. 对 edges 敏感，可能把边缘误判为 corners。
4. 使用简单 minimum function，对方向变化的建模不够稳定。

Harris corner detector 的改进：

1. 使用图像梯度和 auto-correlation / structure tensor 描述局部区域变化。
2. 考虑 corner score 相对于方向的微分变化，而不是只比较几个离散窗口。
3. 可使用连续或平滑窗口函数，例如 Gaussian window。
4. 对真正角点的检测更准确，因为角点在多个方向上都有显著变化，而边缘主要只在一个方向上变化。

### 相关考点

- Moravec：简单、快速，但方向采样粗糙、易受边缘影响。
- Harris：基于局部自相关和梯度矩阵，判断两个方向的变化是否都大。
- “edge vs corner”的判断：
  - flat region：各方向变化都小。
  - edge：一个方向变化大，另一个方向变化小。
  - corner：两个主方向变化都大。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 3 - Edges, Interest points, and Morphology/3-3_Interest points.pdf|Interest Points]]：Moravec limitations、Harris & Stephens corner detector。

### 易错提醒

- 不要只写 Harris “more accurate”；要说明为什么：continuous window / differential corner score / variation with respect to direction。

---

# Question 4

## Q4(a) Motion Estimation

## Q4(a)(i)

### 原题

> Consider an image intensity value on a pixel $(x, y)$ at time $t$ as $I(x,y,t)=x^2+y+xyt+t$. By using the first-order Taylor series expansion, find the linear approximation of the function $I(x+\Delta x, y+\Delta y, t+\Delta t)$ with respect to $\Delta x$, $\Delta y$ and $\Delta t$ when $(x,y,t)=(1,1,1)$. Neglect the higher-order term.

### 参考答案

一阶 Taylor expansion：

$$
I(x+\Delta x,y+\Delta y,t+\Delta t) \approx I(x,y,t)+\frac{\partial I}{\partial x}\Delta x+\frac{\partial I}{\partial y}\Delta y+\frac{\partial I}{\partial t}\Delta t
$$

已知：

$$
I(x,y,t)=x^2+y+xyt+t
$$

先求偏导：

$$
\frac{\partial I}{\partial x}=2x+yt
$$

$$
\frac{\partial I}{\partial y}=1+xt
$$

$$
\frac{\partial I}{\partial t}=xy+1
$$

在 $(x,y,t)=(1,1,1)$：

$$
I(1,1,1)=1^2+1+1\cdot1\cdot1+1=4
$$

$$
\frac{\partial I}{\partial x}=2(1)+1\cdot1=3
$$

$$
\frac{\partial I}{\partial y}=1+1\cdot1=2
$$

$$
\frac{\partial I}{\partial t}=1\cdot1+1=2
$$

所以线性近似为：

$$
I(1+\Delta x,1+\Delta y,1+\Delta t)\approx 4+3\Delta x+2\Delta y+2\Delta t
$$

PDF 写法：

$$
3\Delta x+2\Delta y+2\Delta t+4
$$

### 相关考点

- Motion estimation 中的 gradient method 使用 brightness consistency 和小运动假设。
- 一阶 Taylor expansion 忽略 higher-order terms。
- $I_x, I_y, I_t$ 分别是空间 x、空间 y、时间 t 的梯度/偏导。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 4 - Image Compression (JPEG2000), Image Sequences, MPEG7/4-2_Sequences_updated.pdf|Image Sequences]]：motion estimation、gradient method、Taylor series expansion。

### 易错提醒

- 不要漏掉常数项 $I(1,1,1)=4$。
- $\frac{\partial}{\partial x}(xyt)=yt$，$\frac{\partial}{\partial y}(xyt)=xt$，$\frac{\partial}{\partial t}(xyt)=xy$。

---

## Q4(a)(ii)

### 原题

> Consider a $3\times3$ patch from a reference frame and three $3\times3$ patches, A, B, and C, from a target frame for block matching. Given the patch from the reference frame, 1) perform the mean squared difference (MSE) (or sum-of-squared difference (SSD)) based block matching to patch A, B, and C in the target frame, and 2) determine which patch corresponds to the reference patch.

Reference patch:

```text
1 2 0
2 1 2
0 2 2
```

Target patch A:

```text
1 2 1
2 1 2
0 2 2
```

Target patch B:

```text
2 0 2
0 8 0
2 0 2
```

Target patch C:

```text
1 0 1
0 0 0
2 0 0
```

### 参考答案

用 SSD：

$$
SSD(P_R,P)=\sum_{i=1}^{3}\sum_{j=1}^{3}(P_R(i,j)-P(i,j))^2
$$

#### Patch A

$$
SSD(P_R,P_A)=(1-1)^2+(2-2)^2+(0-1)^2+(2-2)^2+(1-1)^2+(2-2)^2+(0-0)^2+(2-2)^2+(2-2)^2=1
$$

#### Patch B

$$
SSD(P_R,P_B)=(1-2)^2+(2-0)^2+(0-2)^2+(2-0)^2+(1-8)^2+(2-0)^2+(0-2)^2+(2-0)^2+(2-2)^2=74
$$

#### Patch C

$$
SSD(P_R,P_C)=(1-1)^2+(2-0)^2+(0-1)^2+(2-0)^2+(1-0)^2+(2-0)^2+(0-2)^2+(2-0)^2+(2-0)^2=26
$$

因为：

$$
SSD(P_R,P_A)=1 < SSD(P_R,P_C)=26 < SSD(P_R,P_B)=74
$$

所以 **Patch A** 与 reference patch 最匹配。

如果使用 MSE，则只是在 SSD 基础上除以像素数 9：

$$
MSE_A=\frac{1}{9},\quad MSE_B=\frac{74}{9},\quad MSE_C=\frac{26}{9}
$$

最小值仍然是 A，因此匹配结果不变。

### 相关考点

- Block matching：把图像分成小 block，在目标帧搜索最相似 block。
- Similarity measure：SAD、SSD、MSE、cross-correlation 等。
- SSD / MSE 越小，两个 patch 越相似。
- Motion vector 来自 reference block 与 best matching block 的位置差。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 4 - Image Compression (JPEG2000), Image Sequences, MPEG7/4-2_Sequences_updated.pdf|Image Sequences]]：block matching technique、similarity measures、MSE。

### 易错提醒

- 本题不要求求 motion vector，只要求判断对应 patch。
- MSE 和 SSD 的最小 patch 一样，因为 MSE = SSD / 9。
- 逐项平方时不要把 $(1-8)^2$ 写成 7；它等于 49。

---

## Q4(b) JPEG 2000

## Q4(b)(i)

### 原题

> Describe the features of Region of Interest (RoI) coding principle.

### 参考答案

JPEG 2000 的 Region of Interest (ROI) coding 允许图像不同区域使用不同压缩质量，即 **non-uniform distribution of quality**。

主要特征：

1. ROI 区域用比 background (BG) 更高的质量编码。
2. 在保持 ROI 区域相同或更高质量的情况下，可以对背景更强压缩，从而获得更高 compression ratio。
3. 适合只关心图像中关键区域的场景，例如医学图像中的病灶区域、遥感图像中的目标区域。

### 相关考点

- JPEG2000 支持 progressive transmission、layers 和 ROI。
- ROI coding 的核心思想不是整幅图同等质量，而是把 bits / quality 优先分配给重要区域。
- ROI 高质量，背景可以低质量。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 4 - Image Compression (JPEG2000), Image Sequences, MPEG7/4-1_Image Compression_updated.pdf|Image Compression / JPEG2000]]：Region of Interest (ROI)、layers。

### 易错提醒

- ROI 不是“只压缩感兴趣区域”，而是“感兴趣区域保留更高质量，背景可更低质量”。
- 关键词：non-uniform quality distribution、ROI higher quality than BG、higher compression ratio。

---

## Q4(b)(ii)

### 原题

> In Region of Interest coding principle, describe the feature of static ROIs and dynamic ROIs.

### 参考答案

#### Static ROIs

Static ROIs 的特征：

- 在 encoding time 就定义好。
- 通常被称为 ROI coding。
- 适合 storage、fixed transmission、remote sensing 等场景。

#### Dynamic ROIs

Dynamic ROIs 的特征：

- 在 client/server progressive transmission 中由用户交互式定义。
- 系统可根据用户请求动态生成 matching layers。
- 适合 telemedicine、PDAs、mobile communications 等需要交互和逐步传输的场景。

### 相关考点

- Static ROI：编码前固定；适合离线存储或固定传输。
- Dynamic ROI：传输过程中由用户指定；适合交互式浏览和渐进传输。
- JPEG2000 的 layer/progressive 机制支持动态关注区域。

### 课程内容关联

- [[课程笔记/图像与视频处理/附件/Part 4 - Image Compression (JPEG2000), Image Sequences, MPEG7/4-1_Image Compression_updated.pdf|Image Compression / JPEG2000]]：Static ROIs、Dynamic ROIs。

### 易错提醒

- Static vs dynamic 的本质区别是 ROI 定义时间和交互方式。
- 静态不是“不会压缩”，动态也不是“视频 ROI”；动态强调 client/server progressive transmission。

---

# 全卷核心考点汇总

## 1. Histogram 必会点

- 定义：直方图统计每个灰度级出现次数。
- 公式：$h(r_k)=n_k$，归一化后 $p(r_k)=n_k/n$。
- 直方图反映 intensity distribution，不反映 spatial distribution。
- 多幅不同图像可以有相同 histogram，因此 histogram 是 many-to-one、non-invertible。
- 对 rotation、mirroring、skew 等几何重排通常不变。
- 左侧 spike：underexposed / dark。
- 右侧 spike：overexposed / bright。
- 窄范围：low contrast。
- 全范围较均匀：contrast 较好。

## 2. Sampling / Quantization / Interpolation

- Dithering：降低 SNR，但减少 false contour，提升视觉感知。
- Human eye brightness：近似 logarithmic。
- Up-sampling：增加像素位置，需要 interpolation。
- Nearest neighbour：复制最近像素，快但 blocky。
- Bilinear：用 4 个邻近像素线性插值，更平滑但可能模糊。
- 任何插值都不创造真实细节。

## 3. Image Transformation

- Algebraic operations：逐像素加减乘除。
- Background subtraction：$g=f-h$。
- Clipping：超出 0-255。
- Normalization：重新映射到 0-255。
- Scaling：$\begin{bmatrix}s_x&0\\0&s_y\end{bmatrix}$。
- Uniform scaling：$s_x=s_y$。
- Horizontal shear：$\begin{bmatrix}1&k\\0&1\end{bmatrix}$。
- Homogeneous coordinates 用 3x3 矩阵表示 translation 和复合变换。

## 4. Colour Images

- RGB：additive，显示器/相机。
- CMY：subtractive，打印。
- RGB to CMY：$C=1-R, M=1-G, Y=1-B$。
- Trichromatic theory：三类 cone receptors。
- Opponent-process theory：red-green、blue-yellow、luminance 通道。
- 两种理论互补：retina 层面 + brain processing 层面。

## 5. PGM/PPM 文件格式

- P2：ASCII PGM。
- P5：Binary PGM。
- P3：ASCII PPM。
- P6：Binary PPM。
- Header 通常包括：magic number、width height、maximum value、可选 comment。
- Comment 以 `#` 开头。

## 6. Morphology

- Structuring element：移动窗口，定义邻域形状。
- Erosion：fits 才保留，通常缩小物体、去除小亮噪声、分离连接。
- Dilation：hits 就设为 1，通常扩大物体、填 gap、连接断裂。
- Opening：erosion followed by dilation，去小亮噪声。
- Closing：dilation followed by erosion，填小洞、连接小裂缝。

## 7. Interest Points

- Moravec：比较中心窗口与不同方向 shifted windows 的差异。
- 响应取最小方向差异。
- 局限：离散方向、矩形窗口、对边缘敏感。
- Harris：用梯度/自相关矩阵，更连续、更稳定地区分 flat/edge/corner。

## 8. Motion Estimation

- Gradient method：brightness consistency + small motion + Taylor expansion。
- 一阶近似：

$$
I(x+\Delta x,y+\Delta y,t+\Delta t) \approx I + I_x\Delta x + I_y\Delta y + I_t\Delta t
$$

- Block matching：用 SAD/SSD/MSE 找最相似 block。
- SSD / MSE 越小，匹配越好。

## 9. JPEG2000 ROI

- ROI coding：不同区域不同质量。
- ROI 高质量，background 低质量。
- Static ROI：encoding time 定义，适合存储/固定传输/遥感。
- Dynamic ROI：用户交互定义，适合 client-server progressive transmission、远程医疗、移动通信。

---

# 复习建议

## 一、优先级最高的章节

### 第一优先级：必考计算与短答

1. **Histograms**
   - 会看图判断 dark / bright / low contrast / overexposed / underexposed。
   - 会解释 histogram 不含空间信息、对旋转不变。
   - 会画简单二值图或棋盘图的 histogram。

2. **Transformation matrices**
   - scaling、rotation、shear、translation homogeneous matrix。
   - 重点记：horizontal shear 的 0.3 在右上角。
   - 记住 normalization 公式和 clipping 概念。

3. **Morphology**
   - erosion、dilation、opening、closing 的顺序和用途。
   - 能根据场景选择操作：
     - 小亮噪声：opening。
     - 小黑洞/裂缝：closing。
     - 修复断裂：dilation 或 closing。
     - 分离粘连物体：erosion。

4. **Motion estimation**
   - Taylor expansion 必须会求偏导并代入点。
   - Block matching 必须会算 SSD/MSE 并选最小。

### 第二优先级：概念解释题

1. **Colour perception**
   - 三色理论：retina / cones / RGB。
   - 对立过程理论：brain / red-green / blue-yellow / luminance。

2. **Dithering and quantization**
   - Dithering 降低 SNR 但提高 perceived quality。
   - Human brightness perception 是 logarithmic。

3. **JPEG2000 ROI**
   - ROI coding 的非均匀质量分配。
   - Static ROI vs Dynamic ROI。

### 第三优先级：格式与术语

1. **PGM/PPM headers**
   - P2/P3/P5/P6 的含义。
   - width height maximum value comment。

2. **False colour images**
   - 用于突出信息，不是压缩。

3. **Median filter**
   - 非线性，去椒盐噪声，保边缘。

---

## 二、建议制作一页公式表

把下面内容写在一页纸上反复默写：

```text
Histogram:
h(r_k)=n_k, p(r_k)=n_k/n

Normalization:
g = c + (d-c)(f-a)/(b-a)

RGB to CMY:
C=1-R, M=1-G, Y=1-B

Scaling:
[sx 0; 0 sy]

Horizontal shear:
[1 k; 0 1]

Taylor:
I(x+dx,y+dy,t+dt) ≈ I + I_x dx + I_y dy + I_t dt

SSD:
SSD = sum (R(i,j)-T(i,j))^2
MSE = SSD / number_of_pixels

Opening:
erosion then dilation

Closing:
dilation then erosion
```

---

## 三、按题型训练

### 1. 判断题训练

每个判断题都要问自己：

- 这个说法是否把目的说错了？例如 false colour 不是压缩。
- 是否把客观指标和主观感知混淆？例如 dithering。
- 是否把线性和非线性混淆？例如 median filter。

### 2. 看图题训练

拿任何 histogram 图，按以下顺序分析：

1. 分布靠左还是靠右？
2. 范围宽还是窄？
3. 是否有 clipping spike？
4. 是否有多峰？可能对应 foreground/background。
5. 能否通过 stretching/equalization 改善？

### 3. 矩阵题训练

反复默写：

- scaling matrix。
- horizontal shear matrix。
- vertical shear matrix。
- homogeneous translation matrix。
- 复合变换顺序：右边矩阵先作用。

### 4. 形态学题训练

看到关键词就快速匹配：

| 题目关键词 | 首选操作 |
|---|---|
| repair breaks / fill gaps | dilation 或 closing |
| remove small bright specks | opening |
| remove salt noise in binary foreground | opening |
| fill holes | closing |
| separate touching objects | erosion |
| expand object boundary | dilation |
| shrink object boundary | erosion |

### 5. 计算题训练

- Moravec：逐项差值，最后取最小。
- SSD/MSE：逐项平方，最后选最小。
- Taylor：先写通式，再求偏导，再代入点。

建议每道计算题都写完整中间步骤，因为考试会给过程分。

---

## 四、常见失分点清单

- 把 false colour 误认为文件压缩方法。
- 忘记 dithering 会降低 SNR。
- 只说 histogram 反映对比度，忘记它不反映空间位置。
- 棋盘旋转后误以为 histogram 改变。
- 左右曝光判断反了：左暗右亮。
- Upsampling 误写成 downsampling。
- 认为 upsampling 能恢复真实细节。
- Background subtraction 误答成 geometric transformation。
- Clipping 题只写“clip to 255”，没写 normalization。
- Shear matrix 中 shear factor 放错位置。
- RGB to CMY 忘记 RGB 需要归一化。
- Opening / closing 顺序背反。
- Moravec 最后取 maximum 而不是 minimum。
- Taylor expansion 漏掉 $I(1,1,1)$ 常数项。
- MSE/SSD 题忘记“越小越匹配”。
- Static ROI 和 dynamic ROI 的定义时间混淆。

---

## 五、考前 3 天复习安排

### Day 1：基础概念和图像表示

- 复习 L2：sampling、quantization、dithering、up-sampling、interpolation。
- 复习 L3：histogram definition、properties、exposure、equalization。
- 完成训练：
  - 画 5 个不同二值图的 histogram。
  - 判断 10 个 histogram 的曝光和对比度。
  - 默写 dithering、upsampling、median filter 的定义。

### Day 2：变换、颜色、格式、形态学

- 复习 Image Transformations：algebraic operations、normalization、affine matrices。
- 复习 Colour Image：RGB/CMY、trichromatic、opponent-process、PGM/PPM。
- 复习 Morphology：erosion、dilation、opening、closing。
- 完成训练：
  - 默写 scaling/shear/translation matrices。
  - 写 3 个 PGM/PPM header。
  - 做 3 道 dilation/erosion 小矩阵题。

### Day 3：兴趣点、运动估计、JPEG2000

- 复习 Interest Points：Moravec、Harris。
- 复习 Image Sequences：Taylor expansion、block matching。
- 复习 JPEG2000：ROI、static/dynamic ROI。
- 完成训练：
  - 计算 2 道 Taylor expansion。
  - 计算 2 道 SSD/MSE block matching。
  - 用中文和英文各解释一次 static ROI vs dynamic ROI。

---

## 六、答题模板

### 概念解释题模板

```text
[概念名称] means ...
It is used for ...
The key advantage is ...
One limitation/side effect is ...
In this case, ...
```

### 计算题模板

```text
Formula:
...
Substitution:
...
Calculation:
...
Therefore:
...
```

### 场景选择题模板

```text
I would use [operation/method].
This is because [match the problem condition].
The steps are [step 1] followed by [step 2].
The expected result is [effect].
A side effect to manage is [risk].
```

---

## 七、最后建议

这份卷子覆盖面很广，但题型并不难。复习时不要只背定义，要把每个概念和“它解决什么问题、有什么副作用、对应哪个公式/矩阵”连起来。

最值得反复练的内容是：

1. Histogram interpretation。
2. Normalization 和 transformation matrices。
3. Opening / closing / dilation / erosion 的场景选择。
4. Taylor expansion。
5. SSD/MSE block matching。
6. RGB-CMY 与两种颜色感知理论。
7. JPEG2000 ROI 的 static/dynamic 区别。

如果考试时间紧，优先保证计算题过程完整、概念题关键词准确。对于 2 分小题，用“定义 + 关键词”即可；对于 4-6 分小题，务必写“原理 + 过程 + 作用/副作用 + 场景”。

