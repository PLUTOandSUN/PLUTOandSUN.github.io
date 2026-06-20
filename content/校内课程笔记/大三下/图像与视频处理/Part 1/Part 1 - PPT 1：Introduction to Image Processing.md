> [!info] 课件来源
> 原始课件：[[../附件/Part 1 - Introduction, Image Representation, Histograms/1 EBU6230_L1_introduction_to_image_processing.pdf]]  
> 本笔记按 **Lecture 1: Introduction to Image Processing** 整理。Part 1 文件夹中的 `0 EBU6230_module_intro.pdf` 更偏模块说明，本节按正式第 1 讲处理。

---

## 0. 本节课的整体框架

这节课是 **Image and Video Processing 图像与视频处理** 的入门课，作用是建立整门课的基本地图。它不只是在讲“图片怎么变好看”，而是在回答几个更基础的问题：

1. **什么是数字图像？**  
   图像如何用数学函数、像素、灰度值、颜色值来表示。

2. **什么是数字图像处理？**  
   输入是一幅图像，经过算法处理后输出新图像，或者提取出图像中的有用信息。

3. **图像处理系统由哪些部分组成？**  
   从传感器采集，到计算机处理，再到存储、显示、传输。

4. **图像处理能解决哪些问题？**  
   包括去噪、增强、压缩、修复、分割、识别、检索、HDR、全景拼接、医学影像、遥感、取证等。

5. **这门课后续会学什么？**  
   图像表示、直方图、颜色图像、滤波、边缘检测、形态学、压缩、视频序列等。

一句话概括：

> **图像与视频处理就是用计算机对视觉数据进行表示、改善、压缩、分析和理解。**

---

## 1. Learning objectives：学习目标

PPT 给出的学习目标包括：

- 理解 **digital image processing 数字图像处理** 的概念；
- 定义 image processing 这个领域的范围；
- 简要了解数字图像处理中常见的主要方法；
- 了解一个通用图像处理系统的组成部分。

从考试角度看，这节课重点不是复杂计算，而是概念框架。需要掌握：

| 英文关键词 | 中文 | 需要理解什么 |
|---|---|---|
| Digital image | 数字图像 | 图像怎样被像素和数值表示 |
| Image processing | 图像处理 | 输入图像，输出图像或图像信息 |
| Image enhancement | 图像增强 | 改善视觉效果，方便人看 |
| Image analysis | 图像分析 | 提取特征，方便机器理解 |
| Computer vision | 计算机视觉 | 更高层次地理解图像中的物体和场景 |

---

## 2. 图像、视频与视觉信息

### 2.1 为什么视觉信息重要？

PPT 中强调：

> Visual information is the most important type of information perceived, processed and interpreted by human brain.

也就是说，人类大脑处理的信息中，视觉信息占非常重要的位置。我们通过图像和视频理解世界，例如：

- 看照片识别人脸；
- 看医学影像判断疾病；
- 看卫星图像分析天气或森林覆盖；
- 看监控视频识别事件；
- 看运动回放判断是否犯规。

因此，让计算机处理图像和视频，就具有非常大的应用价值。

### 2.2 Image 的定义

**Image 图像** 可以理解为：

> 一个二维的视觉信息表示。

在数学上，灰度图像常写成：

$$
f(x,y)
$$

其中：

- $x$ 和 $y$ 是空间坐标；
- $f(x,y)$ 是该位置处的强度值，即 intensity 或 grey level。

如果是彩色图像，则每个位置不只有一个灰度值，而是多个颜色通道，例如 RGB：

$$
I(x,y) = [R(x,y),G(x,y),B(x,y)]
$$

### 2.3 Video 的定义

**Video 视频** 是由一系列图像按时间顺序组成的视觉多媒体数据。

可以表示为：

$$
f(x,y,t)
$$

其中：

- $x,y$ 表示空间位置；
- $t$ 表示时间或帧编号。

所以视频比图像多了一个时间维度。

| 类型 | 数学表示 | 含义 |
|---|---|---|
| 灰度图像 | $f(x,y)$ | 二维空间中的亮度值 |
| 彩色图像 | $[R(x,y),G(x,y),B(x,y)]$ | 每个像素有多个颜色通道 |
| 视频 | $f(x,y,t)$ | 随时间变化的图像序列 |

---

## 3. 什么是 Digital Image？

### 3.1 连续图像与数字图像

现实世界中的光强通常可以看成连续变化的信号，但计算机不能直接存储无限连续的值。因此图像要经过数字化，变成有限个离散数值。

PPT 中定义：

> When $x$, $y$ and the intensity values of $f$ are all finite, discrete quantities, we call the image a digital image.

也就是说，如果：

- 空间坐标 $x,y$ 是离散的；
- 像素值 $f(x,y)$ 也是有限、离散的；

那么这幅图像就是 **digital image 数字图像**。

### 3.2 Pixel：像素

数字图像由很多小格子组成，每个小格子叫 **pixel**。

每个 pixel 可以表示：

- 灰度值 grey level；
- 颜色值 colour value；
- 高度 height，例如深度图或地形图；
- 透明度 opacity；
- 医学或遥感中的某种测量值。

所以 pixel 不一定只表示“颜色”，本质上它是图像采样点处的数值。

### 3.3 数字化会造成近似

PPT 强调：

> Digitization causes a digital image to become an approximation of a real scene.

原因是现实场景是连续的，而数字图像是有限采样和有限量化的结果。

数字化通常包含两个过程：

1. **Sampling 采样**  
   把连续空间变成离散像素网格。

2. **Quantization 量化**  
   把连续亮度或颜色变成有限等级的数值。

因此数字图像不是现实世界本身，而是现实场景的近似表示。

---

## 4. 图像文件大小：为什么图像数据很大？

PPT 用不同相机分辨率说明：未压缩图像会占用大量存储空间。

### 4.1 未压缩图像大小公式

对于一幅未压缩 RGB 图像：

$$
\text{Size(bits)} = W \times H \times C \times b
$$

其中：

- $W$：图像宽度，单位 pixel；
- $H$：图像高度，单位 pixel；
- $C$：通道数，RGB 图像通常是 3；
- $b$：每个通道的 bit depth，常见为 8 bit。

如果要换算成 bytes：

$$
\text{Size(bytes)} = \frac{W \times H \times C \times b}{8}
$$

对于 8-bit RGB 图像，因为每个通道 8 bit = 1 byte，所以：

$$
\text{Size(bytes)} = W \times H \times 3
$$

### 4.2 例子 1：iPhone X 图像

PPT 示例：iPhone X 相机分辨率为：

$$
4032 \times 3024
$$

RGB，每通道 8 bit：

$$
4032 \times 3024 \times 3 \times 8 \div 8
$$

即：

$$
4032 \times 3024 \times 3 \approx 36,578,304\ \text{bytes}
$$

约为：

$$
36\ \text{MB}
$$

### 4.3 例子 2：iPhone 5 图像

PPT 示例：iPhone 5 分辨率为：

$$
3264 \times 2448
$$

则未压缩 RGB 大小约为：

$$
3264 \times 2448 \times 3 \approx 24\ \text{MB}
$$

### 4.4 例子 3：超大 panorama 图像

PPT 中的 Xrez Panorama 原始 RAW 尺寸：

$$
30,000 \times 70,000
$$

RGB 8-bit 未压缩大小为：

$$
30,000 \times 70,000 \times 3 = 6,300,000,000\ \text{bytes}
$$

约为：

$$
6\ \text{GB}
$$

这说明高分辨率图像的数据量非常大，因此后续课程中的 **compression 压缩** 非常重要。

> [!important] 考试常见计算
> 如果题目给出宽、高、通道数、bit depth，要求计算 raw image size，就用：  
> $$\text{Size(bits)}=W\times H\times C\times b$$  
> 再除以 8 得到 bytes。

---

## 5. What is Digital Image Processing？

### 5.1 基本定义

PPT 中给出一个非常核心的定义：

> Digital image processing refers to algorithms that alter an input image to create a new image.

也就是：

```text
Input image → Image processing algorithm → Output image
```

例如：

```text
原始图像 → Sobel filter → 边缘图像
```

或者：

```text
有噪声图像 → denoising algorithm → 去噪图像
```

### 5.2 图像处理的两大任务

PPT 说数字图像处理主要关注两类任务：

#### 任务 1：Improvement for human interpretation

即改善图像，让人更容易看懂。

例子：

- 增强对比度；
- 去除噪声；
- 锐化边缘；
- 调整亮度；
- 使用 false colour 突出组织边界或血流区域。

这类任务的目标是：**让人看得更清楚**。

#### 任务 2：Processing for machine perception

即处理图像数据，让机器更容易存储、传输、表示或理解。

例子：

- 压缩图像，降低存储和传输成本；
- 分割图像，把物体从背景中分离；
- 提取边缘、角点、纹理等特征；
- 进行人脸识别、车牌识别、指纹识别。

这类任务的目标是：**让计算机更有效地处理和理解图像**。

### 5.3 Image processing 与 computer vision 的区别

这节课也提到 computer vision。

| 概念 | 主要目标 | 输出通常是什么 | 例子 |
|---|---|---|---|
| Image processing | 改善或变换图像 | 图像或低层特征 | 去噪、滤波、增强、压缩 |
| Image analysis | 提取图像信息 | 特征、区域、边界 | 分割、形状描述 |
| Computer vision | 理解视觉世界 | 物体类别、场景意义、三维结构 | 自动驾驶识别行人 |

一句话：

> **Image processing 更偏“处理图像本身”，computer vision 更偏“理解图像内容”。**

---

## 6. Fundamental steps in digital image processing

PPT 引用了 Gonzalez & Woods 的经典图像处理流程图。这个图非常重要，因为它相当于整门课的知识地图。

注意：

- 不是每个任务都会用到所有步骤；
- 不同应用会选择不同步骤组合；
- 很多步骤之间可以相互连接；
- 中间的 **knowledge base 知识库** 可以帮助指导处理过程。

### 6.1 Image acquisition：图像采集

这是图像处理流程的起点。

图像采集包括：

- 用相机、扫描仪、显微镜、卫星传感器等获取图像；
- 将真实世界光信号转成电子信号；
- 进行采样和量化，形成数字图像。

例子：

```text
真实场景 → 镜头/传感器 → 数字图像
```

如果采集质量差，后续处理会更困难。例如：

- 光照不足导致噪声大；
- 镜头模糊导致细节丢失；
- 传感器动态范围不足导致过曝或欠曝。

### 6.2 Image enhancement：图像增强

图像增强的目标是让图像更适合人观察或后续处理。

常见操作：

- contrast adjustment 对比度调整；
- histogram stretching 直方图拉伸；
- smoothing 平滑；
- sharpening 锐化；
- edge enhancement 边缘增强。

增强通常带有主观性：

> 一幅增强后的图像对人眼可能更清楚，但不一定更接近真实场景。

### 6.3 Image restoration：图像复原

图像复原和增强不同。

| 类型 | 目标 | 特点 |
|---|---|---|
| Image enhancement | 让图像看起来更好 | 更主观 |
| Image restoration | 根据退化模型恢复原图 | 更客观、模型驱动 |

例如：

- 图像被运动模糊了，使用 deblurring 复原；
- 图像受到噪声污染，基于噪声模型去噪；
- 老照片破损，尝试恢复丢失区域。

### 6.4 Colour image processing：彩色图像处理

彩色图像不只是灰度图像的三倍。颜色空间、颜色感知和颜色通道之间的关系都会影响处理方法。

常见颜色空间：

- RGB；
- HSV；
- YCbCr；
- Lab。

应用：

- 色彩增强；
- 颜色分割；
- 皮肤检测；
- 遥感图像分析；
- false colour visualization。

### 6.5 Wavelets and multiresolution processing

Wavelet 小波和多分辨率处理用于从不同尺度分析图像。

直观理解：

- 低分辨率层看整体结构；
- 高分辨率层看细节和边缘。

应用：

- 图像压缩；
- 去噪；
- 多尺度特征分析。

### 6.6 Compression：压缩

压缩的目标是减少表示图像所需的 bit 数。

原因：

- 图像文件很大；
- 存储成本高；
- 网络传输慢；
- 视频数据量更大。

压缩分两类：

| 类型 | 含义 | 例子 |
|---|---|---|
| Lossless compression | 无损压缩，解压后完全恢复 | PNG、TIFF 某些模式 |
| Lossy compression | 有损压缩，允许丢失不明显信息 | JPEG、MPEG |

### 6.7 Morphological processing：形态学处理

形态学处理主要关注图像中物体的形状结构。

常见操作：

- erosion 腐蚀；
- dilation 膨胀；
- opening 开运算；
- closing 闭运算。

应用：

- 去除小噪点；
- 填补小孔洞；
- 分离或连接物体；
- 处理二值图像中的形状。

### 6.8 Segmentation：分割

Segmentation 是把图像划分成有意义的区域或对象。

例如：

- 医学图像中分割肿瘤区域；
- 监控图像中分割行人；
- 自动驾驶中分割道路、车辆、天空；
- 工业检测中分割缺陷区域。

分割是图像分析中非常关键的一步，因为后续识别往往依赖分割结果。

### 6.9 Representation and description：表示与描述

分割之后，需要把区域或物体表示成计算机可以处理的特征。

常见特征：

- 形状 shape；
- 边界 boundary；
- 面积 area；
- 周长 perimeter；
- 颜色 colour；
- 纹理 texture；
- 角点 corner；
- 方向 orientation。

例如，对一个分割出的细胞区域，可以提取：面积、圆度、边界复杂度等。

### 6.10 Object recognition：目标识别

目标识别是根据图像特征判断对象类别。

例如：

```text
图像区域 → 特征提取 → 分类器 → 肿瘤/非肿瘤
```

或：

```text
车牌图像 → 字符分割 → 字符识别 → 车牌号码
```

### 6.11 Knowledge base：知识库

流程图中间是 **knowledge base**。

它表示先验知识、规则、模型或训练数据可以帮助指导图像处理。

例如：

- 医学图像中，医生知道某种组织大概的位置和形状；
- 人脸识别中，人脸通常有眼睛、鼻子、嘴巴的结构；
- 车牌识别中，车牌字符有固定排列规则。

---

## 7. General-purpose image processing system：通用图像处理系统

PPT 展示了一个通用图像处理系统，主要包括以下组件。

### 7.1 Problem domain：问题域

问题域是图像来源的真实世界场景。

例子：

- 医院中的人体组织；
- 道路交通场景；
- 卫星观测到的地表；
- 工厂生产线上的产品；
- 显微镜下的细胞。

### 7.2 Image sensors：图像传感器

传感器负责把物理世界的信息变成电子信号。

例子：

- CCD/CMOS camera；
- X-ray detector；
- MRI/PET scanner；
- satellite sensor；
- depth sensor。

### 7.3 Specialized image processing hardware

专用硬件用于加速图像处理。

例子：

- GPU；
- FPGA；
- DSP；
- camera ISP；
- depth camera processing chip。

图像和视频数据量通常很大，因此很多实时系统需要专用硬件。

### 7.4 Computer

计算机是系统的核心控制与处理平台，负责运行图像处理软件、管理数据和连接其他设备。

### 7.5 Image processing software

软件实现具体算法，例如：

- filtering；
- denoising；
- compression；
- segmentation；
- recognition；
- visualization。

### 7.6 Mass storage

图像和视频数据体积很大，需要大量存储。

例如：

- 原始医学影像；
- 卫星遥感数据；
- 监控视频；
- 训练计算机视觉模型的数据集。

### 7.7 Image displays and hardcopy

- **Image displays**：显示器，用于观察图像结果；
- **Hardcopy**：打印输出，例如医学胶片、报告图像、工业检测报告。

### 7.8 Network

网络用于传输图像和视频数据。

例如：

- 视频会议；
- 医学影像远程诊断；
- 云端图像识别；
- 监控视频上传；
- 卫星图像下载。

---

## 8. Noise removal：图像去噪

### 8.1 什么是 noise？

Noise 噪声是图像中不希望出现的随机或非随机干扰。

PPT 说：

> Noise is the result of errors in the image acquisition process that result in pixel values that do not reflect the true intensities of the real scene.

也就是说，噪声会让像素值偏离真实场景的强度。

噪声来源包括：

- 传感器电子噪声；
- 低光照条件；
- 高 ISO；
- 传输错误；
- 压缩伪影；
- 扫描或采集设备误差。

### 8.2 Denoising 的目标

Denoising 去噪的目标是：

> 在尽量保留真实图像结构的同时，减少噪声。

例如：

```text
有白色 specks 的图像 → denoising → 更平滑、更干净的图像
```

### 8.3 低通滤波与噪声

PPT 中提到：

> Low pass filter removes high frequency components.

很多噪声表现为快速变化的高频成分，因此低通滤波可以减弱噪声。

但是有一个重要 trade-off：

> 低通滤波会去掉高频噪声，也可能模糊真实边缘。

因为边缘本身也是图像强度快速变化的位置，也属于高频成分。

| 操作 | 好处 | 风险 |
|---|---|---|
| Low-pass filtering | 减少噪声、平滑图像 | 边缘和细节可能变模糊 |
| High-pass filtering | 强调边缘和细节 | 可能放大噪声 |

---

## 9. Image enhancement：图像增强

### 9.1 Laplacian enhancement

PPT 中给出 Laplacian 增强的例子：月球北极图像经过 Laplacian filter 后边缘更明显。

Laplacian filter 的作用是：

> 检测图像中 intensity 的突然变化，并突出边缘。

直观理解：

- 平坦区域变化小；
- 边缘处灰度变化快；
- Laplacian 对这种快速变化敏感。

因此 Laplacian 常用于：

- edge detection；
- image sharpening；
- highlight sudden intensity transitions。

### 9.2 Contrast adjustment

PPT 展示了 low contrast、original contrast、high contrast 的对比。

**Contrast 对比度** 表示图像中亮暗差异的强弱。

- 低对比度：整体灰蒙蒙，亮暗差异不明显；
- 高对比度：亮的更亮，暗的更暗；
- 合适对比度：细节更容易看清。

后续直方图章节会详细讲：

- histogram；
- histogram stretching；
- histogram equalization。

---

## 10. Image compression：图像压缩

### 10.1 为什么需要压缩？

PPT 强调：

> Images take up a lot of space.

未压缩图像会占用大量存储空间，尤其是：

- 高分辨率照片；
- RAW 图像；
- 医学图像；
- 卫星图像；
- 视频序列。

压缩的目标是：

> Reduce the number of bits needed to represent an image.

### 10.2 压缩的好处

图像压缩可以：

1. 减少存储空间；
2. 降低传输成本；
3. 减少网络延迟；
4. 降低带宽需求；
5. 让视频流媒体成为可能。

### 10.3 JPEG compression 示例

PPT 展示了同一张 450K 原图在不同 JPEG quality 下的大小变化：

| 图像版本 | 文件大小 | 说明 |
|---|---:|---|
| Original | 450K | 原图 |
| JPEG 80% quality | 85K | 压缩明显，质量仍较好 |
| JPEG 10% quality | 15K | 文件更小，质量下降明显 |
| JPEG 5% quality | 5K | 高压缩，伪影严重 |

这说明有损压缩存在质量与文件大小之间的权衡：

```text
更高压缩率 → 更小文件 → 更多信息丢失 → 图像质量下降
```

---

## 11. Image inpainting：图像修复

PPT 给出 inpainting 的例子：

> Inpainting: reconstruct corrupted or destroyed parts of an image.

也就是图像中某些区域损坏、缺失或被遮挡时，用算法估计并填补这些区域。

应用包括：

- 修复老照片划痕；
- 去除图像中的遮挡物；
- 删除不想要的对象；
- 医学图像缺失区域补全；
- 影视后期修复。

inpainting 的难点是：

> 算法不仅要填颜色，还要保持纹理、结构和语义一致。

例如修复人脸时，不能只填相似颜色，还要符合脸部结构。

---

## 12. 应用领域总览

PPT 列出了大量图像与视频处理应用。

### 12.1 Medical research 医学研究

医学图像处理中常见任务包括：

- 显微镜图像分析；
- 肿瘤边界检测；
- 细胞计数；
- MRI、CT、PET 图像增强；
- 病灶检测；
- false colour 显示不同组织。

例如 PPT 展示了 AIDS-virus particles 和 cancer tumor 的显微图像。图像处理可以用滤波器突出边缘或组织结构。

### 12.2 Environmental control 环境监测

图像处理可用于：

- 森林覆盖监测；
- 水质检测；
- 植被变化分析；
- 木材质量检测；
- 灾害监测。

例如遥感图像可以帮助判断森林退化、火灾影响或土地利用变化。

### 12.3 Scientific photography and videography 科学成像

科学成像的目的通常不是拍得“好看”，而是获取定量信息。

应用包括：

- microscopy 显微成像；
- biomedical imaging 生物医学成像；
- remote sensing 遥感；
- astronomy 天文学。

这些领域常常需要从图像中测量物体大小、亮度、位置、速度或结构。

### 12.4 Satellite imaging 卫星图像

卫星图像可用于：

- 天气预报；
- 地表监测；
- 城市规划；
- 农业分析；
- 海洋监测；
- 灾害评估。

卫星图像经常涉及多光谱或红外数据，因此后续会用到 false colour、segmentation、classification 等方法。

---

## 13. False colour images：假彩色图像

PPT 中用 MRI head scan 举例说明 false colour images。

### 13.1 什么是假彩色？

**False colour image 假彩色图像** 指：

> 图像显示出来的颜色不一定是物体真实颜色，而是人为把某些灰度值、波段或测量量映射成颜色，用来突出重要信息。

例如医学图像中，原始 MRI 可能是灰度图，但可以把不同组织、边缘或血流强度映射成不同颜色。

### 13.2 为什么使用 false colour？

因为人眼对颜色差异通常比灰度差异更敏感。

False colour 可以帮助：

- 突出组织边界；
- 显示血流强度；
- 区分不同材料或区域；
- 增强医学、遥感或科学图像的可读性。

### 13.3 True colour 与 false colour 对比

| 类型 | 颜色含义 | 例子 |
|---|---|---|
| True colour | 接近人眼真实看到的颜色 | 普通 RGB 照片 |
| False colour | 人为映射的数据颜色 | MRI 组织图、PET 热点图、遥感红外图 |

> [!tip] 考试答法
> False colour images are images in which the displayed colours do not correspond to the true colours of the scene. Instead, grey levels, spectral bands, or other measurements are mapped artificially to colours to highlight important structures or information.

---

## 14. Image-based diagnosis：基于图像的诊断

PPT 展示了 X-ray 和 PET。

### 14.1 X-ray image

X-ray 使用电磁辐射成像。不同组织对 X-ray 的吸收不同，因此图像中会形成不同亮度。

常见用途：

- 骨折检测；
- 胸片检查；
- 牙科影像；
- 安检扫描。

### 14.2 PET scan

PET，即 Positron Emission Tomography，可以显示组织和器官的功能活动。

PET 图像常使用 false colour 显示代谢活动强弱。例如：

- 高活动区域可能显示为红色或黄色；
- 低活动区域可能显示为蓝色或黑色。

这里的颜色不代表真实颜色，而代表某种医学测量量。

---

## 15. Forensics and law enforcement：取证与执法

图像处理在执法领域非常常见。

PPT 中例子包括：

- number plate recognition 车牌识别；
- fingerprint recognition 指纹识别；
- CCTV image enhancement 监控图像增强。

### 15.1 车牌识别流程示例

一个简单流程可以是：

```text
输入车辆图像
→ 定位车牌区域
→ 字符分割
→ 字符识别
→ 输出车牌号码
```

涉及的图像处理步骤包括：

- contrast enhancement；
- edge detection；
- segmentation；
- pattern recognition。

### 15.2 CCTV 图像增强

监控图像常见问题：

- 分辨率低；
- 光照差；
- 运动模糊；
- 噪声大；
- 压缩伪影明显。

图像处理可以改善可见性，但不能凭空恢复完全不存在的信息。

---

## 16. Video production：视频制作与体育应用

图像与视频处理也用于艺术效果和体育分析。

### 16.1 艺术效果

例如：

- green screen 绿幕合成；
- composite images 合成图像；
- special effects 特效；
- color grading 调色；
- motion tracking 动作跟踪。

### 16.2 体育结果判断

PPT 提到体育中用于准确计算结果，例如 long-jump foul 判断。

这类应用可能用到：

- 视频帧分析；
- 运动轨迹检测；
- 边界线检测；
- 时间同步；
- 多摄像机视角。

---

## 17. Histograms：直方图入门

虽然 histograms 会在 Part 1 后续 PPT 中详细讲，但本节已经给出基本概念：

> Histogram tells the distribution of pixels in an image.

图像直方图表示不同灰度值或颜色值出现的频率。

### 17.1 灰度直方图

对于 8-bit 灰度图，像素值范围为：

$$
0,1,2,\dots,255
$$

直方图统计每个灰度值出现多少次。

### 17.2 直方图与对比度

如果图像灰度值集中在很窄范围内，通常对比度较低。

Histogram stretching 的思想是：

```text
把窄范围灰度拉伸到更宽范围 → 增强对比度
```

这也是后续课程的重要内容。

---

## 18. Segmentation and boundary issues：分割与边界问题

### 18.1 Segmentation 定义

PPT 定义：

> Segmentation is the process of dividing an image into meaningful parts or objects.

也就是把图像分成有意义的区域或目标。

例子：

- 把医学图像分成肿瘤和正常组织；
- 把道路图像分成车道线、车辆、行人、天空；
- 把卫星图像分成水体、森林、城市、农田。

### 18.2 为什么边界很难？

PPT 问：

> Can you draw a line around the edge of this galaxy?

这说明现实图像中的 object boundary 不总是清晰的。

原因包括：

- 物体边缘模糊；
- 噪声影响；
- 光照变化；
- 纹理复杂；
- 目标和背景颜色相似；
- 三维物体投影到二维图像后边界不明确。

因此 segmentation 是图像处理中很难但很重要的问题。

---

## 19. Image retrieval：图像检索

PPT 介绍了从大量图像集合中浏览和检索图像的方法。

### 19.1 Metadata-based image retrieval

Metadata-based retrieval 是根据图像外部描述信息检索。

元数据可以包括：

- 文件名；
- 标签；
- 拍摄时间；
- GPS 位置；
- 人工标注；
- 图像说明文字。

例子：搜索 “moon corona”，系统根据文字描述找到相关图像。

优点：

- 简单直观；
- 对文字搜索友好。

缺点：

- 依赖标注质量；
- 没有标注或标注错误时效果差；
- 图像真实内容可能和标签不完全一致。

### 19.2 Content-based image retrieval, CBIR

Content-based retrieval 是根据图像本身的视觉特征检索。

常用特征：

- colour；
- texture；
- shape；
- spatial information。

例如把 London tube map 拖到 Google 图片搜索中，系统会根据颜色、形状和空间结构寻找相似图像。

优点：

- 不完全依赖人工标注；
- 能找到视觉上相似的图像。

缺点：

- 视觉相似不一定语义相同；
- 可能出现“看起来像但意义不对”的结果。

### 19.3 Semantic image analysis

Semantic image analysis 试图自动识别高层语义内容。

例如：

- 图像中有什么物体；
- 有没有人；
- 人的动作是什么；
- 场景是海边、城市还是森林；
- 图像表达什么情绪。

这通常需要 AI 或 machine learning。

---

## 20. Computer vision：计算机视觉

PPT 给出的定义大意是：

> Computer vision trains computers to interpret and understand the visual world.

它通常包括：

- hardware；
- image processing；
- intelligence。

并且常涉及：

- 多张图像；
- 视频；
- 多视角；
- 三维世界理解；
- object-level understanding。

### 20.1 为什么本课程不是 computer vision 课？

因为本课程重点是 image and video processing 的基础方法，例如：

- 图像表示；
- 滤波；
- 边缘；
- 形态学；
- 颜色；
- 压缩；
- 视频序列。

Computer vision 会进一步研究识别、理解和决策。

但图像处理是计算机视觉的基础。

---

## 21. Exploiting photo and video collections：利用图像和视频集合

PPT 介绍了利用大量图像和视频产生新视觉媒体的方法。

### 21.1 Intelligent compositing

智能合成是把来自不同视觉来源的元素组合在一起。

例子：

- green screen effects；
- 电影特效；
- 虚拟背景；
- 把人物从一张图中提取并放到另一张图。

它通常需要：

- foreground extraction；
- matting；
- segmentation；
- colour matching；
- blending。

### 21.2 Object recognition/classification-based manipulation

先识别图像中的对象，再对对象进行修改。

例子：

- 自动识别人脸并美颜；
- 识别天空并替换天空；
- 识别车辆并打码；
- 识别背景并虚化。

### 21.3 Efficient image navigation

当图像集合很大时，需要有效浏览和组织。

例如：

- 按地点聚类；
- 按人物分类；
- 按主题搜索；
- 按相似图像排序。

---

## 22. Multiple images and camera arrays：多图像与相机阵列

PPT 说明：多张图像可以顺序拍摄，也可以同时拍摄，用来产生新的或增强的图像。

常见应用包括：

- mosaicing；
- collages and montages；
- refocusing；
- light field rendering；
- high dynamic range；
- extended depth of field。

核心思想：

> 单张图像信息有限，多张图像可以提供更多视角、更多曝光、更多时间信息或更多空间采样。

---

## 23. HDR images：高动态范围图像

### 23.1 什么是 dynamic range？

Dynamic range 表示图像中最暗区域和最亮区域之间的亮度范围。

**High Dynamic Range, HDR** 指图像能够同时保留非常亮和非常暗区域中的细节。

PPT 中说：

> High dynamic range means very bright and very dark parts in a single image.

### 23.2 为什么需要 HDR？

人眼能感知的动态范围通常比普通相机更宽。

普通照片可能出现：

- 天空过曝，变成一片白；
- 阴影欠曝，变成一片黑；
- 亮部和暗部无法同时保留细节。

### 23.3 HDR 的工作方式

PPT 给出的思路：

1. 对同一场景拍摄多张不同曝光的图像；
2. 每张图保留不同亮度区域的细节；
3. 用图像处理算法把它们组合成 HDR 图像。

例如：

| 曝光 | 保留信息 |
|---|---|
| 短曝光 | 保留亮部细节，避免天空过曝 |
| 中曝光 | 保留中间亮度区域 |
| 长曝光 | 保留暗部细节，避免阴影太黑 |

最终合成图像亮暗更平衡。

---

## 24. Panoramic mosaics：全景拼接

### 24.1 什么是 panoramic mosaic？

Panoramic mosaics 是把多张顺序拍摄的图像拼接成一张宽视角图像。

用途：

- 手机全景照片；
- 街景地图；
- 火星或月球表面全景；
- 大场景记录。

### 24.2 为什么会有 distortion？

PPT 提到：

> There is no distortion-free way to create a full panorama.

因为真实世界是三维的，相机拍到的是透视投影，拼接成大范围二维图像时不可避免要做投影变换。

常见现象：

- 直线变弯；
- 物体形状拉伸；
- 边缘区域变形；
- 运动物体拼接错位。

这就是 panoramic distortion。

---

## 25. Refocusing and light field rendering

### 25.1 Light field rendering 是什么？

PPT 解释：light field rendering 可以一次捕捉场景的多个视角，使用户在拍摄后改变焦点。

普通相机主要记录二维图像，而 light field camera 试图记录光线方向信息。

### 25.2 Post-capture refocusing

Post-capture refocusing 指：

> 拍照之后再选择图像中哪里清晰。

例如：

- 拍摄时苍蝇清晰、背景模糊；
- 后期可以让背景清晰、苍蝇模糊；
- 或通过合成让二者都清晰。

### 25.3 Extended depth of field

Depth of field, DOF，表示图像中看起来清晰的距离范围。

| 类型 | 含义 |
|---|---|
| Shallow DOF | 只有小范围清晰，背景容易虚化 |
| Extended DOF | 前景到背景更大范围都清晰 |

Extended depth of field 可以通过多焦点图像合成实现。

---

## 26. 3D imaging and display：三维成像与显示

### 26.1 Multi-focus light-field camera

PPT 提到 Lytro 相机。它属于 light-field camera，可以记录不同方向的光线，用于后期调焦。

### 26.2 3D light-field camera

PPT 提到 Raytrix camera，使用大量 micro-lenses 微透镜捕捉 3D 深度信息。

这种系统可以用于：

- 三维重建；
- 后期调整焦点；
- 深度估计；
- 工业检测。

### 26.3 Time-of-Flight + RGB systems

Time-of-Flight, ToF，相机通过测量光从发射到反射回来的时间估计深度。

基本思想：

```text
发出光 → 光碰到物体反射 → 测量返回时间 → 估计距离
```

RGB 相机提供颜色和纹理信息，ToF 提供深度信息。

组合后可用于：

- facial recognition；
- augmented reality；
- 3D scanning；
- gesture tracking；
- motion capture。

### 26.4 Old-style 3D and 3DTV

旧式 3D 常用 anaglyph 红蓝眼镜：

- 一只眼看红色图像；
- 另一只眼看蓝色图像；
- 大脑融合形成 3D 感。

3DTV 使用偏振光或同步快门眼镜实现双眼不同图像。

### 26.5 Tensor displays and VR

Tensor displays 是一种 advanced glasses-free multi-view 3D display，通过 directional backlighting 和 layered LCD panels 产生多视角。

VR headsets 例如 Oculus Rift 和 Sony Morpheus，则通过头戴显示器向双眼呈现不同视图，产生沉浸式三维体验。

---

## 27. Multiple images 的其他增强功能

PPT 最后还提到，多张图像或相机阵列还能用于：

### 27.1 Super-resolution

把多张低分辨率图像组合，提高最终图像分辨率。

核心思想：

> 多张图像可能包含略微不同的采样信息，合并后能恢复更多细节。

### 27.2 Denoising by averaging

多张图像中真实结构相对稳定，而随机噪声每次不同。

因此对多张图平均可以降低随机噪声：

$$
\text{Noise average} \rightarrow \text{smaller noise variance}
$$

### 27.3 Multispectral imaging

Multispectral imaging 捕捉可见光之外的波段，例如：

- infrared 红外；
- ultraviolet 紫外；
- thermal 热红外。

应用：

- 植被健康分析；
- 材料检测；
- 医学成像；
- 遥感分类。

### 27.4 Polarization imaging

Polarization imaging 检测光波振动方向，用于增强材料识别或表面反射分析。

应用包括：

- 水面反射检测；
- 材料区分；
- 工业检测；
- 医学和显微成像。

---

## 28. 本节与考试的连接

这节课的考点通常偏概念题和简单计算题。

### 28.1 可能考点 1：定义 digital image

可以这样答：

> A digital image is a finite and discrete representation of a two-dimensional image. It can be represented as a function $f(x,y)$, where $x$ and $y$ are spatial coordinates and $f(x,y)$ is the intensity or grey level at that position.

中文：

> 数字图像是二维图像的有限、离散表示，可写作 $f(x,y)$，其中 $x,y$ 为空间坐标，$f(x,y)$ 表示该位置的亮度或灰度值。

### 28.2 可能考点 2：计算 raw image size

答题步骤：

1. 找宽度 $W$；
2. 找高度 $H$；
3. 找通道数 $C$；
4. 找每通道 bit depth $b$；
5. 用公式：

$$
\text{Size(bits)} = W \times H \times C \times b
$$

6. 除以 8 转成 bytes。

### 28.3 可能考点 3：解释 digital image processing

可以这样答：

> Digital image processing refers to the use of computer algorithms to process, manipulate, enhance, compress, analyse or interpret digital images.

重点写出：

- computer algorithms；
- digital images；
- processing/manipulation/enhancement/analysis；
- input image and output image or extracted information。

### 28.4 可能考点 4：列举 fundamental steps

常见步骤包括：

- image acquisition；
- image enhancement；
- image restoration；
- colour image processing；
- wavelets and multiresolution processing；
- compression；
- morphological processing；
- segmentation；
- representation and description；
- object recognition；
- knowledge base。

不需要每次都全部应用。

### 28.5 可能考点 5：说明 compression 的目的

关键词：

- reduce file size；
- reduce number of bits；
- save storage；
- reduce transmission bandwidth；
- trade-off between quality and compression ratio。

### 28.6 可能考点 6：解释 false colour image

可以这样答：

> False colour images display data using colours that do not correspond to the true colours of the scene. They are used to highlight important structures, edges, tissue types, blood flow levels, or other invisible information.

### 28.7 可能考点 7：区分 metadata-based 与 content-based retrieval

| 方法 | 根据什么检索 | 优点 | 缺点 |
|---|---|---|---|
| Metadata-based | 文件名、标签、描述、注释 | 简单、适合文字搜索 | 依赖人工标注 |
| Content-based | 颜色、纹理、形状、空间信息 | 能按视觉相似性检索 | 视觉相似不等于语义相同 |

### 28.8 可能考点 8：解释 HDR

答题关键词：

- very bright and very dark parts in one image；
- wider range of brightness levels；
- cameras have lower dynamic range than human eye；
- capture multiple exposures；
- combine them to preserve highlight and shadow details。

---

## 29. 本节关键词表

| 英文 | 中文 | 解释 |
|---|---|---|
| Image | 图像 | 二维视觉信息 |
| Video | 视频 | 按时间排列的图像序列 |
| Digital image | 数字图像 | 有限、离散的图像表示 |
| Pixel | 像素 | 数字图像中的最小采样单元 |
| Intensity | 强度 | 像素亮度或灰度值 |
| Grey level | 灰度级 | 灰度图像中的亮度等级 |
| RGB | 红绿蓝 | 常见彩色图像通道 |
| Sampling | 采样 | 把连续空间离散化 |
| Quantization | 量化 | 把连续强度离散化 |
| Image processing | 图像处理 | 用算法处理图像 |
| Enhancement | 增强 | 改善视觉效果 |
| Restoration | 复原 | 根据退化模型恢复图像 |
| Denoising | 去噪 | 减少图像噪声 |
| Low-pass filter | 低通滤波器 | 平滑图像、减少高频噪声 |
| Laplacian filter | 拉普拉斯滤波器 | 突出强度突变和边缘 |
| Compression | 压缩 | 减少图像所需 bit 数 |
| Inpainting | 图像修复 | 重建损坏或缺失区域 |
| False colour | 假彩色 | 用人为颜色映射突出信息 |
| Histogram | 直方图 | 像素值分布 |
| Segmentation | 分割 | 把图像分成有意义区域 |
| Boundary | 边界 | 物体或区域的分界线 |
| Metadata | 元数据 | 文件名、标签、描述等外部信息 |
| CBIR | 基于内容的图像检索 | 根据颜色、纹理、形状等视觉特征检索 |
| Computer vision | 计算机视觉 | 让计算机理解视觉世界 |
| HDR | 高动态范围 | 同时保留亮部和暗部细节 |
| Panorama | 全景图 | 多图拼接形成宽视角图像 |
| Light field | 光场 | 记录光线方向信息的成像方式 |
| Depth of field | 景深 | 图像中看起来清晰的距离范围 |
| ToF | 飞行时间 | 根据光返回时间估计深度 |

---

## 30. 复习自测题

1. 什么是 digital image？如何用 $f(x,y)$ 表示？
2. 为什么说数字图像是真实场景的 approximation？
3. 一张 $1920\times1080$ 的 RGB 8-bit 图像，未压缩大小是多少 bytes？
4. Image processing 和 computer vision 有什么区别？
5. Image enhancement 和 image restoration 有什么区别？
6. 为什么 low-pass filter 可以去噪？它有什么副作用？
7. JPEG quality 下降时，文件大小和图像质量分别会怎样变化？
8. False colour image 的目的是什么？
9. Segmentation 为什么困难？举一个 boundary issue 的例子。
10. Metadata-based retrieval 和 content-based retrieval 的区别是什么？
11. HDR 为什么需要多张不同曝光图像？
12. Panoramic mosaics 为什么会产生 distortion？
13. Light field rendering 为什么可以实现 post-capture refocusing？
14. ToF + RGB 系统分别提供什么信息？

---

## 31. 一句话总结

本节课建立了图像与视频处理的入门框架：**数字图像是对真实场景的离散近似，图像处理用计算机算法对图像进行增强、复原、压缩、分割、检索和理解，并广泛应用于医学、遥感、取证、视频制作、HDR、全景拼接和三维成像等领域。**
---

