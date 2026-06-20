> [!info] 课件来源
> 原始课件：[[../附件/Part 1 - Introduction, Image Representation, Histograms/3 EBU6230_L3_histograms_updated.pdf]]  
> 本节是 Part 1 的第 3 个正式课件，主题是 **Image Histograms 图像直方图**。核心内容包括：histogram 的定义、数学表达、直方图能反映什么、直方图的局限、颜色直方图、thresholding 阈值分割、segmentation 分割，以及 histogram equalization 直方图均衡化。

---

## 0. 本节课的整体框架

这节课围绕一个问题展开：

> **如果只看一幅图像中不同灰度值出现了多少次，我们能知道什么？又不能知道什么？**

图像直方图就是回答这个问题的工具。

它不关心像素在哪里，只关心像素值出现了多少次。因此它可以快速告诉我们：

- 图像是否偏暗；
- 图像是否偏亮；
- 图像对比度是否低；
- 图像是否过曝或欠曝；
- 是否可以用 threshold 把目标和背景分开；
- 如何通过 histogram equalization 改善低对比图像。

本节主线可以写成：

```text
Image pixels
→ Count intensity occurrences
→ Histogram
→ Diagnose brightness / contrast / exposure
→ Thresholding / segmentation
→ Histogram equalization for enhancement
```

---

## 1. Learning objectives：学习目标

PPT 给出的目标是：

1. 理解 image histogram 的物理意义；
2. 理解如何 manipulate image histogram 来做 image enhancement。

换句话说，本节不仅要会画直方图，还要理解：

- 直方图的横轴和纵轴分别代表什么；
- 为什么直方图能反映亮度和对比度；
- 为什么两个不同图像可能有同一个直方图；
- 为什么 thresholding 可以用直方图找目标；
- 为什么 histogram equalization 能增强低对比图像。

---

## 2. Histogram 的基本定义

### 2.1 Histogram 是什么？

PPT 定义：

> Histogram is a function that maps the quantization levels into the frequency of each quantization level in the image.

中文解释：

> 图像直方图是一个函数，它把每个量化灰度级映射到该灰度级在图像中出现的次数。

对于灰度图来说，直方图统计的是：

```text
灰度值 0 出现多少次
灰度值 1 出现多少次
...
灰度值 255 出现多少次
```

如果是 8-bit 灰度图，灰度范围通常是：

$$
0,1,2,\dots,255
$$

### 2.2 frequency 不是 spatial frequency

PPT 特别提醒：这里的 **frequency** 不是 Fourier 里的 spatial frequency，而是 **count 次数**。

也就是说：

```text
Histogram frequency = 出现次数
NOT spatial frequency = 空间频率
```

例如灰度值 100 的 frequency 是 3500，意思是图像中有 3500 个像素的灰度值为 100。

### 2.3 直方图反映的是强度分布，不是空间分布

PPT 的重要句子：

> Histograms reflect the pixel intensity distribution, NOT the spatial distribution.

这意味着直方图告诉你：

- 哪些灰度值出现多；
- 哪些灰度值出现少；
- 灰度值是否集中在暗部、亮部或中间；
- 图像是否使用了完整亮度范围。

但直方图不能告诉你：

- 这些像素在哪里；
- 图像中物体的形状；
- 目标和背景的空间布局；
- 纹理和边缘的位置。

---

## 3. Histogram 的数学表达

### 3.1 灰度级范围

假设一幅数字图像有 $L$ 个可能灰度级，则灰度级可以写为：

$$
r_k,\quad k=0,1,2,\dots,L-1
$$

对于 8-bit 图像：

$$
L=256
$$

灰度级范围是：

$$
r_k \in \{0,1,2,\dots,255\}
$$

### 3.2 直方图函数

PPT 给出的直方图定义可以写成：

$$
h(r_k)=n_k
$$

其中：

- $r_k$：第 $k$ 个灰度级；
- $n_k$：图像中灰度值等于 $r_k$ 的像素数量；
- $k=0,1,\dots,L-1$。

所以 $h(r_k)$ 就是“灰度级 $r_k$ 的出现次数”。

### 3.3 总像素数

如果图像大小为 $M\times N$，则总像素数为：

$$
n=M\times N
$$

所有灰度级计数相加必须等于总像素数：

$$
\sum_{k=0}^{L-1} n_k=n
$$

### 3.4 Normalized histogram：归一化直方图

PPT 定义 normalized histogram：把每个灰度级的计数除以总像素数。

公式为：

$$
p(r_k)=\frac{n_k}{n}
$$

其中 $p(r_k)$ 可以理解为随机选一个像素时，它的灰度值等于 $r_k$ 的概率。

所有概率相加为 1：

$$
\sum_{k=0}^{L-1}p(r_k)=1
$$

> [!tip] 直方图和概率
> 普通 histogram 是 count；normalized histogram 是 probability。课程里说灰度直方图统计上等价于 Probability Density Function；严格说，离散灰度值时更像 Probability Mass Function。

---

## 4. 如何读一张 histogram？

### 4.1 横轴和纵轴

灰度直方图通常这样读：

| 轴 | 含义 |
|---|---|
| 横轴 | grey level / pixel value，例如 0-255 |
| 纵轴 | frequency / count，即该灰度值出现次数 |

对于 8-bit 灰度图：

- 左边接近 0：dark pixels；
- 中间接近 128：medium grey；
- 右边接近 255：bright pixels。

### 4.2 峰值位置说明亮度倾向

| histogram 特征 | 图像含义 |
|---|---|
| 峰值集中在左侧 | 图像偏暗，dark image |
| 峰值集中在右侧 | 图像偏亮，bright image |
| 峰值集中在中间很窄范围 | 低对比度，low contrast |
| 分布覆盖很宽范围 | 高对比度，high contrast |
| 大量像素堆在 0 或 255 | 可能欠曝/过曝并发生 clipping |

### 4.3 Histogram 不显示空间位置

如果两幅图像像素值完全一样，只是位置重新排列，那么它们的 histogram 完全相同。

例如：

```text
图像 A：黑白块排列成一张脸
图像 B：同样数量的黑白像素随机打乱
```

它们可能有相同 histogram，但视觉内容完全不同。

---

## 5. Histogram 能封装哪些图像信息？

PPT 中说 histogram 可以帮助发现 image acquisition issues，例如：

- over exposure；
- under exposure；
- brightness；
- contrast；
- dynamic range。

### 5.1 Brightness：亮度

Brightness 可以理解为图像整体偏亮或偏暗。

直方图表现：

- 偏左：整体较暗；
- 偏右：整体较亮。

如果图像经过加亮操作，例如每个像素加 50，那么 histogram 会整体向右移动。

### 5.2 Contrast：对比度

Contrast 是图像中亮暗差异的程度。

PPT 中直观解释：

> Contrast is how vivid or washed-out an image/object appears.

低对比图像：

- 灰度值集中在窄范围；
- 看起来灰蒙蒙；
- 物体和背景不明显。

高对比图像：

- 灰度值分布范围更宽；
- 亮暗差异明显；
- 视觉上更 vivid。

### 5.3 Dynamic range：动态范围

在本课程图像语境中，dynamic range 可以理解为图像使用的亮度范围。

对于 8-bit 图像，理论可用范围是：

$$
0\text{ to }255
$$

共 256 个灰度级。

但实际图像可能只用到了：

$$
80\text{ to }140
$$

这说明实际亮度范围很窄，通常对应低对比度图像。

---

## 6. 低对比、暗图像、亮图像在 histogram 上的表现

### 6.1 Low contrast and low brightness range

PPT 中展示了低对比和低亮度范围图像。

直方图特点：

```text
像素值集中在很窄范围内
```

如果集中在左侧，则图像既低对比又偏暗。

### 6.2 Higher contrast and brightness range

高对比图像的 histogram 通常覆盖更宽的灰度范围。

这说明图像中同时存在暗区域和亮区域。

### 6.3 Bright image

亮图像的 histogram peak 会向右移动。

```text
right-shifted peak → brighter image
```

### 6.4 Dark image

暗图像的 histogram peak 会向左移动。

```text
left-shifted peak → darker image
```

---

## 7. Brightness perception：亮度感知并不完全客观

PPT 中用了 Adelson brightness illusion 说明：人眼看到的亮度会受到背景影响。

### 7.1 同一个灰度，看起来可能不同

在幻觉图中，两个方块 A 和 B 实际灰度相同，但因为周围背景和阴影不同，看起来一个更暗、一个更亮。

这说明：

> 人眼感知 brightness 时，不只看单个像素值，还会受到上下文影响。

### 7.2 与图像处理的关系

这解释了为什么图像增强不能只考虑数学数值，还要考虑 HVS，人类视觉系统。

例如：

- 同样的灰度差在不同背景下感知不同；
- 边缘和局部对比会影响亮度判断；
- histogram equalization 改善的不一定是物理真实，而是视觉可解释性。

---

## 8. 用 histogram 检测曝光问题

PPT 展示了 properly exposed、underexposed、overexposed 图像。

### 8.1 Underexposed 欠曝

欠曝图像太暗。

histogram 特点：

- 大量像素集中在左侧；
- 暗部细节可能挤在 0 附近；
- 可能有 shadow clipping。

### 8.2 Overexposed 过曝

过曝图像太亮。

histogram 特点：

- 大量像素集中在右侧；
- 亮部细节可能挤在 255 附近；
- 可能有 highlight clipping。

### 8.3 Properly exposed 正常曝光

正常曝光图像的像素值通常在可用范围内更合理地分布。

注意：不是所有好图像的 histogram 都必须均匀。不同场景有不同合理分布，例如夜景本来就偏暗，雪景本来就偏亮。

---

## 9. Histogram properties：直方图性质

### 9.1 Many-to-one mapping

PPT 说：

> Histogram is a many-to-one mapping.

意思是很多不同图像可以对应同一个 histogram。

例如：

- 一幅人脸图；
- 把人脸图中的像素随机打乱；
- 两者像素值数量一样，所以 histogram 一样；
- 但图像内容完全不同。

### 9.2 Non-invertible mapping

因为 histogram 丢失了空间位置信息，所以它不可逆。

也就是说：

> 只知道 histogram，不能恢复原图。

PPT Quiz 的答案：

```text
No, it is not possible to reconstruct an image using only its histogram.
```

原因：histogram 只保存 intensity distribution，不保存 spatial distribution。

### 9.3 对某些几何操作不变

PPT 说 histogram 对某些 geometric operations 是 invariant 的，例如：

- rotation；
- scaling；
- mirroring；
- skew。

直观原因：如果这些操作不改变像素值总数量，只改变像素位置，那么 histogram 不变。

> [!warning] 注意
> 如果 scaling 过程中发生 interpolation 或 resampling，像素值可能改变，histogram 也可能改变。PPT 这里强调的是直方图本质上不记录空间位置。

---

## 10. Colour image histograms：颜色图像直方图

### 10.1 两种常见类型

PPT 说 colour image histograms 有两类：

1. **Intensity histogram**  
   先把彩色图像转成灰度图，再显示灰度 histogram。

2. **Individual color channel histograms**  
   分别画 R、G、B 三个通道的 histogram。

### 10.2 Intensity histogram

流程：

```text
RGB image → grayscale image → gray-level histogram
```

优点：

- 简单；
- 能看整体亮度、对比度、曝光。

缺点：

- 丢失颜色信息；
- 不知道颜色分布。

### 10.3 RGB channel histograms

分别统计：

```text
Red channel histogram
Green channel histogram
Blue channel histogram
```

它们可以帮助判断：

- 某个颜色通道是否过曝；
- 图像是否偏色；
- saturation effects；
- lighting effects。

### 10.4 3 个 1D 直方图 vs 1 个 3D 直方图

PPT 问：

```text
3 × 1D or 1 × 3D?
```

3 个 1D 直方图分别统计 R、G、B，但不能反映 RGB 之间的联合关系。

例如：

```text
R histogram 一样
G histogram 一样
B histogram 一样
```

不代表图像颜色组合一样。

1 个 3D colour histogram 则统计 RGB 三维颜色空间中的联合分布，更能表示实际颜色分布，但计算和存储更复杂。

### 10.5 颜色直方图的局限

PPT 强调：

> Images with totally different RGB colors can have same R, G and B histograms.

原因同样是：独立通道 histogram 不保存像素之间的配对关系，也不保存空间位置。

---

## 11. Histogram summary：直方图总结

PPT 对 histogram 的总结可以整理为：

### 11.1 Histogram 存储什么？

它存储：

- grey-level distribution；
- colour distribution；
- pixel value counts；
- normalized intensity probabilities。

### 11.2 Histogram 可以用来做什么？

它可以用于：

- 改变 contrast；
- 改变 grey level range；
- 判断图像是否使用了完整亮度范围；
- 检测曝光问题；
- thresholding；
- segmentation；
- background subtraction；
- histogram equalization。

### 11.3 Histogram 不能提供什么？

它不能提供：

- spatial information；
- object shape；
- edge location；
- texture arrangement；
- pixel neighbourhood relationship。

---

## 12. Image manipulation：加亮与 clipping

PPT 中有一个 image manipulation 示例：

```text
adding 128 & clipping
```

### 12.1 像素加常数

如果对每个像素加 128：

$$
g(x,y)=f(x,y)+128
$$

图像会变亮，histogram 会整体向右移动。

### 12.2 Clipping

但 8-bit 图像最大值是 255。如果加完超过 255，就必须截断：

$$
g(x,y)=\min(f(x,y)+128,255)
$$

这叫 clipping。

### 12.3 clipping 的问题

clipping 会造成信息丢失。

例如原本：

```text
180, 200, 230, 250
```

加 128 后都超过 255，被截断为：

```text
255, 255, 255, 255
```

这些原本不同的亮部细节全部变成纯白，无法区分。

---

## 13. Thresholding：阈值处理

### 13.1 Thresholding 的定义

Thresholding 是把灰度图像转换成二值图像的方法。

核心思想：

> 选择一个 threshold $T$，把像素分成两类。

常见公式：

$$
g(x,y)=
\begin{cases}
1, & f(x,y)\ge T\\
0, & f(x,y)<T
\end{cases}
$$

其中：

- 1 通常表示 foreground/object；
- 0 通常表示 background。

如果目标比背景更暗，也可以反过来定义。

### 13.2 Thresholding 和 histogram 的关系

PPT 说 thresholding splits histogram。

也就是在 histogram 上选择一个位置 $T$：

```text
灰度值 < T → 一类
灰度值 ≥ T → 另一类
```

这样就把灰度图变成 binary image。

### 13.3 为什么 bimodal histogram 适合 thresholding？

如果目标和背景灰度差异明显，histogram 可能是 bimodal，即有两个峰：

- 一个峰对应 object；
- 一个峰对应 background。

这时可以在两个峰之间的 valley 位置选择 threshold $T$。

PPT 例子：字符和背景。

```text
object characters → darker peak
background → brighter peak
T separates them
```

---

## 14. Thresholding 用于 segmentation

### 14.1 Segmentation 的目标

Segmentation 是把图像分成有意义区域或对象。

Thresholding 是最简单的 segmentation 方法之一。

流程：

```text
灰度图像
→ 选择 threshold T
→ 生成 binary image
→ 分离 object/background
```

### 14.2 适用条件

Thresholding 适合：

- object 和 background 对比明显；
- 光照相对均匀；
- histogram 有明显两个峰；
- 噪声不太严重。

### 14.3 不适用情况

如果出现以下情况，简单 thresholding 可能失败：

- 光照不均匀；
- 背景复杂；
- object 和 background 灰度重叠；
- 图像噪声大；
- histogram 没有明显 valley。

这时可能需要 adaptive thresholding、滤波、形态学处理或更复杂的 segmentation 方法。

---

## 15. 用 histogram 测量分割目标面积

PPT 给出了一个重要公式：如果深色目标在浅色背景上，并且 threshold 为 $T$，则深色目标面积可以由 histogram 计算。

公式：

$$
A=\sum_{D=0}^{T}H(D)
$$

其中：

- $A$：分割出的暗目标总面积，单位可以理解为像素数；
- $H(D)$：灰度值为 $D$ 的像素数量；
- $T$：阈值；
- $D=0$ 到 $T$：表示所有比阈值更暗的像素。

### 15.1 为什么这样能算面积？

如果目标是暗的，背景是亮的，那么所有灰度值小于等于 $T$ 的像素都属于目标。

把这些像素数量加起来，就是目标面积。

### 15.2 如果目标是亮的怎么办？

如果目标比背景亮，那么面积应计算：

$$
A=\sum_{D=T}^{L-1}H(D)
$$

也就是统计 threshold 右侧的像素数。

---

## 16. Interactive thresholding：交互式阈值

PPT 提到 GIMP 或 Photoshop 中的 interactive thresholding。

这种工具允许用户拖动 threshold slider，实时查看二值化结果。

优点：

- 直观；
- 适合人工调试；
- 可以快速找到合适 threshold。

缺点：

- 主观；
- 不适合大规模自动处理；
- 不同图像可能需要不同 threshold。

---

## 17. Histogram equalization：直方图均衡化

### 17.1 基本定义

PPT 定义：

> Histogram equalization is a technique used in image processing to improve the contrast of an image.

中文：

> 直方图均衡化是一种通过调整图像强度分布来提高图像对比度的方法。

### 17.2 它做了什么？

PPT 中说它：

- adjusts the intensity distribution；
- spreads out the most frequent intensity values；
- improves visibility in low-contrast images。

直观理解：

```text
原图灰度值集中在窄范围
→ 用变换把它们拉开
→ 图像覆盖更宽灰度范围
→ 对比度提高
```

### 17.3 目标

PPT 给出目标：

> To produce images with evenly distributed histograms without changing the number of grey levels.

也就是说，不改变可用灰度级数量，而是重新映射灰度值，使输出灰度分布更均匀。

---

## 18. Histogram equalization 的直觉

### 18.1 为什么能改善暗图像？

暗图像中，大部分像素集中在低灰度值区域。

如果把低灰度区域拉伸到更宽范围，图像中的暗部差异会变明显。

例如：

```text
原来大量像素在 20-80
均衡化后可能分布到 0-255
```

这样细节更容易看出来。

### 18.2 为什么叫 equalization？

因为它试图让输出 histogram 更平坦、更均匀。

但注意，离散图像中输出 histogram 通常不会完美平坦。

原因：

- 像素数有限；
- 灰度值是整数；
- 映射后可能出现 gaps；
- 多个输入灰度级可能映射到同一个输出灰度级。

---

## 19. Probability density transformation：概率密度变换

PPT 用连续概率密度解释 histogram equalization。

### 19.1 灰度变换

假设输入灰度为 $f$，输出灰度为 $g$，变换为：

$$
g=T(f)
$$

其中 $T(f)$ 是 monotonic 单调函数。

单调性很重要，因为它保证灰度顺序不乱：

```text
原来更亮的像素，变换后仍然不会比原来更暗的像素更暗
```

### 19.2 概率守恒

PPT 说：

> Probability of $f$ in $df$ must be equal to probability of $g$ in $dg$.

数学上：

$$
p(f)df=p(g)dg
$$

意思是变换前后像素不会凭空增加或消失，只是灰度坐标被重新拉伸。

### 19.3 让输出分布均匀

如果希望输出 $g$ 的分布均匀，可以设：

$$
p(g)=1
$$

于是：

$$
p(f)=\frac{dg}{df}
$$

积分得到：

$$
g=\int_0^f p(x)dx=P(f)
$$

其中 $P(f)$ 是输入灰度的 cumulative distribution function，CDF。

> [!important] 核心结论
> 连续 histogram equalization 的变换函数就是输入图像灰度分布的 CDF。

---

## 20. CDF 为什么能均衡 histogram？

### 20.1 高概率区域被拉开

如果某个灰度区域 $p(f)$ 很高，说明很多像素集中在那里。

CDF 在这一区域会增长很快，即斜率大。

这会让输出灰度跨度变大，把密集像素 spread out。

### 20.2 低概率区域被压缩

如果某个灰度区域 $p(f)$ 很低，说明像素很少。

CDF 在这一区域增长慢，输出跨度较小。

因此少量像素区域不会占用太多输出灰度范围。

### 20.3 结果

最终效果是：

```text
像素密集的灰度区间被拉开
像素稀疏的灰度区间被压缩
整体对比度通常提高
```

---

## 21. Discrete histogram equalization：离散直方图均衡化

实际数字图像是离散的，所以用 summation 而不是 integral。

### 21.1 灰度概率

对于灰度级 $r_k$：

$$
p(r_k)=\frac{n_k}{n}
$$

其中：

- $n_k$：灰度级 $r_k$ 的像素数；
- $n=M\times N$：总像素数；
- $L$：灰度级数量。

### 21.2 变换函数

PPT 给出离散变换：

$$
s_k=T(r_k)=(L-1)\sum_{j=0}^{k}p(r_j)
$$

这就是把累计概率 CDF 乘以最大灰度值 $L-1$。

通常还需要对 $s_k$ 取整，因为输出灰度必须是整数。

### 21.3 操作步骤

做 histogram equalization 的步骤：

1. 统计每个灰度级出现次数 $n_k$；
2. 计算 normalized histogram：

$$
p(r_k)=\frac{n_k}{n}
$$

3. 计算 cumulative histogram / CDF：

$$
CDF(k)=\sum_{j=0}^{k}p(r_j)
$$

4. 计算新灰度映射：

$$
s_k=(L-1)CDF(k)
$$

5. 把原图中灰度为 $r_k$ 的像素替换为 $s_k$。

---

## 22. 离散均衡化小例子

假设一幅图只有 4 个灰度级：

$$
L=4,\quad r_k\in\{0,1,2,3\}
$$

各灰度级计数为：

| 灰度 $r_k$ | 计数 $n_k$ | 概率 $p(r_k)$ | CDF |
|---:|---:|---:|---:|
| 0 | 4 | 0.50 | 0.50 |
| 1 | 2 | 0.25 | 0.75 |
| 2 | 1 | 0.125 | 0.875 |
| 3 | 1 | 0.125 | 1.00 |

因为 $L-1=3$，所以：

$$
s_k=3\times CDF(k)
$$

得到近似映射：

| 输入灰度 | $3\times CDF$ | 取整后输出 |
|---:|---:|---:|
| 0 | 1.5 | 2 |
| 1 | 2.25 | 2 |
| 2 | 2.625 | 3 |
| 3 | 3 | 3 |

这个例子说明：

- 大量集中在低灰度的像素被整体推向更高灰度；
- 输出灰度不一定每一级都使用；
- 离散均衡化不一定得到完美平坦 histogram。

---

## 23. Histogram equalization in colour images

PPT 说彩色图像中可以对 R、G、B 分别做 histogram equalization。

### 23.1 分通道均衡化

流程：

```text
R channel → equalization
G channel → equalization
B channel → equalization
combine channels
```

### 23.2 问题：colour distortion

如果每个通道独立调整，RGB 之间的比例可能改变，导致颜色失真。

例如原来一个区域是自然肤色，R、G、B 独立均衡后，可能变得偏红、偏绿或不自然。

### 23.3 CLAHE

PPT 提到替代方法：

> Contrast Limited Adaptive Histogram Equalisation, CLAHE.

CLAHE 的思想是：

- 不对整幅图做全局均衡；
- 把图像分成局部区域；
- 对局部区域做 contrast enhancement；
- 限制 contrast amplification，避免噪声被过度放大。

CLAHE 常用于医学图像、低对比图像和局部光照不均的图像。

---

## 24. Applications of histogram equalization

PPT 列出多个应用。

### 24.1 Medical imaging 医学影像

用于增强：

- X-rays；
- MRIs；
- CT scans。

目的：让组织边界、病灶、结构细节更清楚。

### 24.2 Satellite imaging 卫星图像

用于提升地球观测图像的对比度，例如：

- 地形；
- 云层；
- 植被；
- 水体；
- 城市区域。

### 24.3 Forensic analysis 取证分析

用于增强监控图像或安全 footage，例如：

- 人脸识别；
- 车牌识别；
- 暗光场景增强；
- 模糊低对比区域改善。

### 24.4 Photography and video processing

用于纠正 poor lighting conditions，例如：

- 暗图提亮；
- 灰蒙图增强；
- 视频画面对比度调整。

---

## 25. Challenges and limitations：挑战与局限

PPT 问：When does histogram equalisation fail?

### 25.1 过度增强会丢失细节

如果 applied aggressively，图像可能出现：

- 局部细节丢失；
- 亮暗过度夸张；
- 噪声被放大；
- 视觉不自然。

### 25.2 对高对比图像不一定有效

如果图像本来已经 high-contrast，继续均衡化可能没有帮助，甚至破坏原本自然的亮度关系。

### 25.3 彩色图像可能产生 artifacts

分通道均衡化可能导致颜色失真和伪影。

### 25.4 不适合局部对比问题

全局 histogram equalization 只考虑整幅图的灰度分布。

如果图像只有局部区域太暗或太亮，全局均衡可能不能有效解决，甚至影响其他区域。

这种情况更适合 adaptive histogram equalization 或 CLAHE。

---

## 26. 本节与考试的连接

### 26.1 可能考点 1：定义 histogram

可以这样答：

> An image histogram is a function that maps each quantization level or grey level to the number of pixels in the image with that level. It represents the pixel intensity distribution, not the spatial distribution.

中文：

> 图像直方图把每个灰度级映射到该灰度级出现的像素数，反映像素强度分布，而不是空间分布。

### 26.2 可能考点 2：写出 histogram 和 normalized histogram 公式

普通直方图：

$$
h(r_k)=n_k
$$

归一化直方图：

$$
p(r_k)=\frac{n_k}{n}
$$

并且：

$$
\sum_{k=0}^{L-1}p(r_k)=1
$$

### 26.3 可能考点 3：解释 histogram 为什么不能恢复图像

答题关键词：

- many-to-one mapping；
- non-invertible；
- histogram stores intensity distribution only；
- spatial information is lost；
- different images can have the same histogram。

### 26.4 可能考点 4：判断亮度、对比度、曝光

| Histogram 形态 | 图像情况 |
|---|---|
| 集中在左侧 | dark / underexposed |
| 集中在右侧 | bright / overexposed |
| 集中在狭窄范围 | low contrast |
| 覆盖宽范围 | high contrast |
| 堆在 0 或 255 | clipping，细节丢失 |

### 26.5 可能考点 5：colour histogram 类型

两类：

1. intensity histogram：转灰度后统计；
2. individual RGB histograms：分别统计 R/G/B。

局限：没有完整 spatial information，也可能没有真实 joint colour distribution。

### 26.6 可能考点 6：thresholding

公式：

$$
g(x,y)=
\begin{cases}
1, & f(x,y)\ge T\\
0, & f(x,y)<T
\end{cases}
$$

适合 object 和 background 对比明显、histogram bimodal 的情况。

### 26.7 可能考点 7：用 histogram 计算面积

深色目标在浅色背景上：

$$
A=\sum_{D=0}^{T}H(D)
$$

亮色目标在深色背景上：

$$
A=\sum_{D=T}^{L-1}H(D)
$$

### 26.8 可能考点 8：histogram equalization 原理

答题模板：

> Histogram equalization improves contrast by remapping grey levels using the cumulative distribution function of the input image, spreading frequent intensity values over a wider range.

公式：

$$
s_k=(L-1)\sum_{j=0}^{k}p(r_j)
$$

### 26.9 可能考点 9：为什么离散 equalization 不一定得到平坦 histogram？

原因：

- grey levels are discrete；
- pixel counts are finite；
- output values must be integers；
- some output grey levels may be skipped；
- multiple input levels may map to same output level。

### 26.10 可能考点 10：直方图均衡化的局限

写出：

- may amplify noise；
- may lose details if applied aggressively；
- may distort colours；
- not useful for already high-contrast images；
- not ideal for local contrast problems。

---

## 27. 本节关键词表

| 英文 | 中文 | 解释 |
|---|---|---|
| Histogram | 直方图 | 统计每个灰度级出现次数 |
| Grey level | 灰度级 | 像素亮度的量化等级 |
| Quantization level | 量化级 | 离散化后的强度等级 |
| Frequency | 次数 | histogram 中表示 count，不是空间频率 |
| Intensity distribution | 强度分布 | 像素值出现情况 |
| Spatial distribution | 空间分布 | 像素在图像中的位置布局 |
| Normalized histogram | 归一化直方图 | 计数除以总像素数，表示概率 |
| PDF | 概率密度函数 | 连续随机变量的概率分布描述 |
| CDF | 累积分布函数 | 从低灰度到当前灰度的累计概率 |
| Brightness | 亮度 | 图像整体明暗程度 |
| Contrast | 对比度 | 亮暗差异程度 |
| Dynamic range | 动态范围 | 图像使用的亮度范围 |
| Underexposed | 欠曝 | 图像过暗，histogram 偏左 |
| Overexposed | 过曝 | 图像过亮，histogram 偏右 |
| Clipping | 截断 | 超出范围的像素被压到 0 或 255 |
| Many-to-one | 多对一 | 多幅图像可有同一 histogram |
| Non-invertible | 不可逆 | 无法只由 histogram 恢复原图 |
| Colour histogram | 颜色直方图 | 统计颜色或颜色通道分布 |
| Thresholding | 阈值处理 | 用阈值把灰度图转二值图 |
| Bimodal histogram | 双峰直方图 | 通常对应目标和背景两类像素 |
| Segmentation | 分割 | 把图像分成对象和背景等区域 |
| Histogram equalization | 直方图均衡化 | 用 CDF 重新映射灰度以增强对比度 |
| CLAHE | 限制对比度自适应直方图均衡化 | 局部增强且限制噪声放大 |
| Artifact | 伪影 | 处理后产生的不真实视觉结构 |

---

## 28. 复习自测题

1. Histogram 的横轴和纵轴分别表示什么？
2. 为什么 histogram 里的 frequency 不是 spatial frequency？
3. 写出 $h(r_k)=n_k$ 中每个符号的含义。
4. Normalized histogram 的公式是什么？为什么所有概率和为 1？
5. 为什么 histogram 反映 intensity distribution，而不是 spatial distribution？
6. 两幅不同图像为什么可能有相同 histogram？
7. 为什么不能只用 histogram 重建原图？
8. 欠曝、过曝、低对比图像的 histogram 分别有什么特征？
9. Colour image histogram 有哪两类？各有什么局限？
10. Thresholding 如何把灰度图转成 binary image？
11. 为什么 bimodal histogram 适合 thresholding？
12. 如何用 histogram 和 threshold 计算暗目标面积？
13. Histogram equalization 的目标是什么？
14. 为什么 CDF 可以作为 histogram equalization 的映射函数？
15. 写出离散 histogram equalization 公式 $s_k$。
16. 为什么离散 equalization 后输出 histogram 不一定完全平坦？
17. 对 RGB 三个通道分别 equalize 会有什么问题？
18. CLAHE 相比全局 histogram equalization 的优点是什么？
19. Histogram equalization 在医学影像和卫星图像中有什么作用？
20. Histogram equalization 什么时候可能失败？

---

## 29. 一句话总结

本节课的核心是：**图像直方图统计像素强度或颜色的分布，可用于判断亮度、对比度、曝光、阈值分割和直方图均衡化；但它不包含空间位置信息，因此不同图像可能有相同 histogram，也不能仅凭 histogram 恢复原图。**
