---
title: "Part 3 - Tutorial Week 3"
course: 图像与视频处理
part: 3
type: tutorial
topic: Edges and Interest Points
source: "[[../附件/Part 3 - Edges, Interest points, and Morphology/Week3_tutorials.pdf]]"
created: 2026-06-18
tags:
  - course/image-video-processing
  - image-processing/edge-detection
  - image-processing/interest-points
  - tutorial
---

> [!info] 课件来源
> 原始 tutorial：[[../附件/Part 3 - Edges, Interest points, and Morphology/Week3_tutorials.pdf]]  
> 本 tutorial 对应 **图像与视频处理 Part 3 / Week 3**，主要复习 **Edges** 和 **Interest Points**：包括 gradient、Laplacian / LoG、Moravec operator 和 Harris corner detector。

---

## 0. Tutorial 总览

Week 3 tutorial 的内容可以分为两大块：

1. **Edges 边缘检测**
   - 一阶导数方法：Gradient；
   - 二阶导数方法：Laplacian；
   - Laplacian 对噪声敏感，因此引出 LoG（Laplacian of Gaussian）。
2. **Interest Points 兴趣点 / 角点**
   - Moravec operator；
   - Harris corner detector。

它不是单纯讲新概念，而是通过公式回顾和手算题帮助理解 Part 3 的核心算法。

> [!summary] 一句话理解本 tutorial
> **边缘检测关注“灰度变化在哪里大”，兴趣点检测关注“局部窗口向任何方向移动是否都会明显变化”；Gradient / LoG 解决边缘问题，Moravec / Harris 解决角点和匹配点问题。**

---

## 1. Gradient：一阶导数边缘检测

### 1.1 图像梯度定义

对二维图像 $f(x,y)$，梯度定义为：

$$
\nabla f(x,y)=
\begin{bmatrix}
G_x\\
G_y
\end{bmatrix}
=
\begin{bmatrix}
\frac{\partial f(x,y)}{\partial x}\\
\frac{\partial f(x,y)}{\partial y}
\end{bmatrix}
$$

梯度是一个向量，指向图像灰度值增长最快的方向。

### 1.2 梯度幅值

梯度幅值表示边缘强度。

精确形式：

$$
|\nabla f|=\sqrt{G_x^2+G_y^2}
$$

tutorial 中采用的简化形式是：

$$
|\nabla f|\approx |G_x|+|G_y|
$$

这种近似计算简单，适合手算。

### 1.3 梯度方向

梯度方向为：

$$
\alpha(x,y)=\tan^{-1}\left(\frac{G_y}{G_x}\right)
$$

实际编程时更常用：

$$
\alpha(x,y)=\operatorname{atan2}(G_y,G_x)
$$

因为 `atan2` 可以正确处理象限和 $G_x=0$ 的情况。

> [!important] 梯度方向与边缘方向
> 梯度方向总是垂直于边缘方向。边缘方向可以看作梯度方向旋转 $-90^\circ$ 或 $+90^\circ$。

---

## 2. Finite Differences：用有限差分估计梯度

tutorial 第 6 页给出 forward finite differences：

$$
\frac{\partial f}{\partial x}
\approx
\frac{f(x+h_x,y)-f(x,y)}{h_x}
$$

当 $h_x=1$：

$$
G_x=f(x+1,y)-f(x,y)
$$

同理：

$$
\frac{\partial f}{\partial y}
\approx
\frac{f(x,y+h_y)-f(x,y)}{h_y}
$$

当 $h_y=1$：

$$
G_y=f(x,y+1)-f(x,y)
$$

> [!note] 坐标理解
> 这里的 $x$ 可以理解为列方向，$y$ 可以理解为行方向。因此 $G_x$ 看右边像素减当前像素，$G_y$ 看下方像素减当前像素。

---

## 3. Gradient 手算例题

### 3.1 题目

tutorial 第 7 页给出一个 $5\times5$ 灰度块，红框内是要计算的 $3\times3$ 区域：

$$
\begin{bmatrix}
7&7&7&7&7\\
7&7&7&7&7\\
0&0&0&0&0\\
1&1&1&0&0\\
1&1&1&0&0
\end{bmatrix}
$$

要求：

1. 用 forward difference 求红框区域的 $G_x$；
2. 求 $G_y$；
3. 求梯度幅值：

$$
|\nabla f|=|G_x|+|G_y|
$$

4. 用 threshold = 5 判断边缘。

红框区域对应原图中的第 2 到第 4 行、第 2 到第 4 列。

### 3.2 计算 $G_x$

使用：

$$
G_x=f(x+1,y)-f(x,y)
$$

得到：

$$
G_x=
\begin{bmatrix}
0&0&0\\
0&0&0\\
0&-1&0
\end{bmatrix}
$$

解释：大部分位置左右灰度相同，所以 $G_x=0$；只有第三行中间位置右边从 1 变到 0，因此 $G_x=-1$。

### 3.3 计算 $G_y$

使用：

$$
G_y=f(x,y+1)-f(x,y)
$$

得到：

$$
G_y=
\begin{bmatrix}
-7&-7&-7\\
1&1&0\\
0&0&0
\end{bmatrix}
$$

解释：红框第一行下面是 0，而当前是 7，所以垂直方向变化很大，得到 $-7$。

### 3.4 梯度幅值

$$
|\nabla f|=|G_x|+|G_y|
$$

得到：

$$
|\nabla f|=
\begin{bmatrix}
7&7&7\\
1&1&0\\
0&1&0
\end{bmatrix}
$$

### 3.5 threshold = 5 的边缘图

如果采用：

$$
|\nabla f|>5
$$

则边缘图为：

$$
\begin{bmatrix}
1&1&1\\
0&0&0\\
0&0&0
\end{bmatrix}
$$

即红框顶部一行是边缘。

> [!tip] 解题要点
> 这个例子主要说明：边缘对应灰度突变。上方从 7 突然变到 0，因此 $G_y$ 很大；左右方向变化小，因此 $G_x$ 基本为 0。

---

## 4. 一阶导数 vs 二阶导数

tutorial 第 9 页回顾 1st vs 2nd derivatives。

### 4.1 一阶导数

一阶导数直接衡量灰度变化率。

- step edge 附近，一阶导数出现峰值；
- 梯度幅值大的位置通常是边缘候选点。

### 4.2 二阶导数

二阶导数衡量变化率的变化。

- 边缘附近二阶导数会出现正负变化；
- 常通过 zero-crossing 检测边缘位置。

### 4.3 关系

| 方法 | 检测依据 | 典型输出 |
|---|---|---|
| Gradient | 一阶导数大 | 边缘强度与方向 |
| Laplacian | 二阶导数过零 | zero-crossing 边缘 |

---

## 5. Laplacian 与 LoG

### 5.1 Laplacian 对噪声敏感

Laplian filters are very sensitive to noise。

原因：

- Laplacian 是二阶导数；
- 导数会放大高频成分；
- 噪声通常具有高频特征；
- 因此直接 Laplacian 会把噪声也当成强响应。

### 5.2 解决方法：先平滑

为降低噪声影响，通常先做 Gaussian smoothing。

因为卷积满足结合律：

$$
(G * \nabla^2) * f = G * (\nabla^2 * f)
$$

也可以先把 Gaussian 和 Laplacian 合成一个滤波器，再与图像卷积。这就是：

> **LoG = Laplacian of Gaussian**

### 5.3 Gaussian 函数

tutorial 中给出：

$$
G(r)=e^{-\frac{r^2}{2\sigma^2}},\qquad r^2=x^2+y^2
$$

其中 $\sigma$ 是标准差，控制平滑程度。

### 5.4 LoG 函数

tutorial 给出 LoG 的形式：

$$
\nabla^2G(r)=\left[\frac{r^2-\sigma^2}{\sigma^4}\right]e^{-\frac{r^2}{2\sigma^2}}
$$

> [!note] 公式版本提醒
> 不同教材可能会因为 Gaussian 是否归一化、Laplacian 符号约定不同，导致 LoG 常数项或整体符号略有差异。复习时重点记住：**先 Gaussian 平滑，再 Laplacian 求二阶变化，最后常用 zero-crossing 找边缘。**

### 5.5 Mexican hat

Laplacian of Gaussian 的形状像墨西哥帽，所以也叫：

> Mexican hat function

---

## 6. MATLAB 代码：Laplacian vs LoG

tutorial 第 13-14 页给出 MATLAB 示例代码：

```matlab
img = rgb2gray(imread('qmul.jpg'));
% img = imnoise(img,'gaussian',0,0.001);
f = img;
w1 = fspecial('laplacian',0.2);
w2 = fspecial('log',[3 3],0.5);
filtered_img1 = imfilter(f,w1,'replicate');
filtered_img2 = imfilter(f,w2,'replicate');
figure, imshow(img)
figure, imshow(filtered_img1);
figure, imshow(filtered_img2);
```

加入噪声时：

```matlab
img = imnoise(img,'gaussian',0,0.001);
w2 = fspecial('log',[3 3],0.7);
```

### 6.1 代码想说明什么？

- `fspecial('laplacian',0.2)`：直接构造 Laplacian filter；
- `fspecial('log',[3 3],0.5)`：构造 LoG filter；
- `imnoise(...,'gaussian',...)`：人为加入 Gaussian noise；
- 对比结果可看到：直接 Laplacian 对噪声更敏感，LoG 因为先平滑，响应更稳定。

---

## 7. Interest Points 总览

Tutorial 后半部分转向 interest points。

Interest point 的核心用途是：

- 图像匹配；
- 物体识别；
- 图像拼接；
- 增强现实；
- 3D reconstruction；
- 机器人导航。

与 edge 不同，interest point 更强调：

> **局部窗口向多个方向移动时都会有明显变化。**

---

## 8. Moravec Operator

### 8.1 基本思想

Moravec operator 是一个差分型兴趣点算子。

它通过比较局部窗口在不同方向移动后的灰度差异来判断该点是否是 corner。

如果一个点是 corner，那么窗口往任何方向移动，窗口内容都会发生明显变化。

### 8.2 算法流程

给定灰度图像 $I(x,y)$：

1. 在每个像素上放置一个 $3\times3$ window；
2. 将另一个 window 相对它移动 1 个像素；
3. 对两个 window 中对应像素求差；
4. 将 9 个差异值求和；
5. 对上、下、左、右和对角方向重复；
6. 取多个方向响应的最小值作为：

$$
M(i,j)
$$

7. 对 $M(i,j)$ threshold，得到 corner。

常见 SSD 写法为：

$$
E_{u,v}(x,y)=\sum_{(a,b)\in W}\left[I(x+a+u,y+b+v)-I(x+a,y+b)\right]^2
$$

然后：

$$
M(x,y)=\min_{(u,v)\in D}E_{u,v}(x,y)
$$

### 8.3 为什么取最小值？

| 局部结构 | 多方向窗口移动变化 | 最小值 |
|---|---|---|
| flat | 所有方向都小 | 小 |
| edge | 垂直边缘方向大，沿边缘方向小 | 小 |
| corner | 所有方向都大 | 大 |

因此，只有 corner 的最小方向响应也会很大。

### 8.4 Moravec 的缺点

- 使用离散方向，方向刻画粗糙；
- diagonal edges 可能被误检为 corners；
- 使用简单窗口和简单 min function；
- 理论和实际效果不如 Harris。

---

## 9. Moravec 手算例题

### 9.1 题目

tutorial 第 24 页给出一个 $6\times5$ 灰度矩阵：

$$
\begin{bmatrix}
200&255&255&250&190\\
180&240&250&245&240\\
180&245&240&240&240\\
45&25&30&230&230\\
50&30&20&200&200\\
25&35&30&220&230
\end{bmatrix}
$$

要求计算灰色 block 与粗框 block 之间的 Moravec operator 差异值。

### 9.2 两个 $3\times3$ block

灰色 block 为：

$$
\begin{bmatrix}
245&240&240\\
25&30&230\\
30&20&200
\end{bmatrix}
$$

红色粗框 block 为：

$$
\begin{bmatrix}
250&245&240\\
240&240&240\\
30&230&230
\end{bmatrix}
$$

### 9.3 Absolute difference

逐元素绝对差：

$$
\begin{bmatrix}
5&5&0\\
215&210&10\\
0&210&30
\end{bmatrix}
$$

求和：

$$
5+5+0+215+210+10+0+210+30=685
$$

所以如果按课件 detail 页的 absolute differences，Moravec 差异值为：

$$
685
$$

### 9.4 如果使用 SSD

如果按 SSD 定义：

$$
\sum d^2=135475
$$

> [!note] 为什么有两个值？
> tutorial 前面文字提到 SSD，但 detail 页说 absolute differences。两者都是“窗口差异”的度量。做题时应按题目或老师要求；若按本页 detail 操作，答案是 absolute difference sum = 685。

---

## 10. Harris Corner Detector

### 10.1 Harris 的核心思想

Harris detector 判断一个点是否为 corner 的标准是：

> 小窗口向任意方向移动时，强度都发生大变化。

用 $E(u,v)$ 表示窗口位移后的强度变化：

$$
E(u,v)=\sum_{x,y}w(x,y)\left[I(x+u,y+v)-I(x,y)\right]^2
$$

### 10.2 小位移二次型近似

对于小位移：

$$
E(u,v)\approx
\begin{bmatrix}u&v\end{bmatrix}
M
\begin{bmatrix}u\\v\end{bmatrix}
$$

其中：

$$
M=\sum_{x,y}w(x,y)
\begin{bmatrix}
I_x^2&I_xI_y\\
I_xI_y&I_y^2
\end{bmatrix}
$$

$M$ 是一个 $2\times2$ 矩阵，由局部窗口内图像导数组成。

### 10.3 用特征值分类

设 $M$ 的特征值为 $\lambda_1,\lambda_2$。

| 情况 | 判断 |
|---|---|
| $\lambda_1,\lambda_2$ 都小 | flat region |
| $\lambda_1\gg\lambda_2$ 或 $\lambda_2\gg\lambda_1$ | edge |
| $\lambda_1,\lambda_2$ 都大且接近 | corner |

### 10.4 Harris response

Harris 使用：

$$
R=\det(M)-k(\operatorname{trace}(M))^2
$$

其中：

$$
\det(M)=\lambda_1\lambda_2
$$

$$
\operatorname{trace}(M)=\lambda_1+\lambda_2
$$

课件给出：

$$
k=0.04\sim0.06
$$

判断：

| $R$ | 含义 |
|---|---|
| large positive | corner |
| large negative | edge |
| close to 0 | flat |

---

## 11. Harris 手算例题

### 11.1 题目

tutorial 第 32 页给出 $I_x$ 和 $I_y$，要求用：

- $3\times3$ equal weighting window；
- empirical constant $k=0.05$；
- box filter；

计算中心点的 Harris matrix 和 corner response。

红框内的 $I_x$ 为：

$$
I_x=
\begin{bmatrix}
7&7&7\\
0&0&7\\
1&1&7
\end{bmatrix}
$$

红框内的 $I_y$ 为：

$$
I_y=
\begin{bmatrix}
1&0&7\\
1&0&7\\
7&7&7
\end{bmatrix}
$$

### 11.2 计算 $M$

Harris 矩阵：

$$
M=\sum w(x,y)
\begin{bmatrix}
I_x^2&I_xI_y\\
I_xI_y&I_y^2
\end{bmatrix}
$$

若 equal weighting 不做 $1/9$ 归一化，直接求和：

$$
\sum I_x^2=247
$$

$$
\sum I_y^2=247
$$

$$
\sum I_xI_y=168
$$

所以：

$$
M=
\begin{bmatrix}
247&168\\
168&247
\end{bmatrix}
$$

### 11.3 计算 determinant 和 trace

$$
\det(M)=247\times247-168^2
$$

$$
\det(M)=61009-28224=32785
$$

$$
\operatorname{trace}(M)=247+247=494
$$

### 11.4 计算 Harris response

$$
R=\det(M)-k(\operatorname{trace}(M))^2
$$

代入 $k=0.05$：

$$
R=32785-0.05\times494^2
$$

$$
494^2=244036
$$

$$
R=32785-12201.8=20583.2
$$

因此：

$$
R=20583.2>0
$$

该中心位置具有较强 corner response。

### 11.5 若 box filter 使用 $1/9$ 归一化

如果将 box filter 解释为平均权重，则：

$$
M=\frac{1}{9}
\begin{bmatrix}
247&168\\
168&247
\end{bmatrix}
=
\begin{bmatrix}
27.444&18.667\\
18.667&27.444
\end{bmatrix}
$$

此时：

$$
R\approx254.114>0
$$

结论仍然是 corner。

> [!tip] 观察结论
> 该例中 $M$ 的两个特征值约为 $415$ 和 $79$（未归一化），都为正且不小，所以中心点不是 flat；$R>0$，因此按 Harris response 判断为 corner-like point。

---

## 12. Tutorial 中 Edges 与 Interest Points 的联系

| 内容 | 关注点 | 数学工具 | 输出 |
|---|---|---|---|
| Gradient | 一阶灰度变化 | $G_x,G_y$ | 边缘强度与方向 |
| Laplacian | 二阶变化/zero crossing | $\nabla^2 f$ | 边缘候选 |
| LoG | 抗噪二阶边缘 | Gaussian + Laplacian | 更稳的边缘响应 |
| Moravec | 窗口多方向变化 | window difference | 角点响应 $M(i,j)$ |
| Harris | 局部梯度二阶统计 | structure matrix $M$ | corner response $R$ |

> [!summary] 关键区别
> Gradient/Laplacian 找的是边缘；Moravec/Harris 找的是适合匹配的角点。边缘通常只有一个强变化方向，角点需要多个方向都有强变化。

---

## 13. 常见易错点

| 易错点 | 正确理解 |
|---|---|
| 梯度方向就是边缘方向 | 错。梯度方向垂直于边缘方向。 |
| $G_x$ 和 $G_y$ 的符号无所谓 | 对幅值是无所谓，但对方向很重要。 |
| threshold = 5 时是否包含等于 5 | 题目一般写 determine edge，可按 $>5$；若写 $\ge5$ 要另说。 |
| Laplacian 直接用就最好 | 错。Laplian 对噪声敏感，通常要先 Gaussian smoothing。 |
| LoG 是两个独立步骤 | 可以先平滑再 Laplacian，也可以预先合成 LoG filter。 |
| Moravec 只算一个方向就是最终值 | 错。最终 Moravec response 通常取多个方向响应的最小值。 |
| Moravec 中 SAD 与 SSD 混淆 | 课件文字有 SSD，也有 absolute difference；按题目要求说明使用哪一种。 |
| Harris 的 $M$ 是图像矩阵 | 错。$M$ 是由窗口内 $I_x^2,I_y^2,I_xI_y$ 求和得到的结构矩阵。 |
| $R>0$ 但很小也一定是强角点 | 不一定。实际还需要 threshold 和 local maximum。 |

---

## 14. 复习清单

### 14.1 必须会写公式

Gradient：

$$
\nabla f=
\begin{bmatrix}
G_x\\G_y
\end{bmatrix}
$$

Forward finite difference：

$$
G_x=f(x+1,y)-f(x,y)
$$

$$
G_y=f(x,y+1)-f(x,y)
$$

Gradient magnitude：

$$
|\nabla f|\approx |G_x|+|G_y|
$$

LoG：

$$
\nabla^2G(r)=\left[\frac{r^2-\sigma^2}{\sigma^4}\right]e^{-\frac{r^2}{2\sigma^2}}
$$

Harris matrix：

$$
M=\sum_{x,y}w(x,y)
\begin{bmatrix}
I_x^2&I_xI_y\\
I_xI_y&I_y^2
\end{bmatrix}
$$

Harris response：

$$
R=\det(M)-k(\operatorname{trace}(M))^2
$$

### 14.2 必须会做题

1. 给定灰度矩阵，用 forward differences 计算 $G_x,G_y$；
2. 计算 $|G_x|+|G_y|$ 并 threshold；
3. 解释 Laplacian 为什么对噪声敏感；
4. 说明 LoG 为什么先平滑；
5. 给定两个 patch，计算 Moravec 的差异值；
6. 给定 $I_x,I_y$ 窗口，计算 Harris matrix；
7. 计算 $\det(M)$、$\operatorname{trace}(M)$ 和 $R$；
8. 根据 $R$ 或特征值判断 flat / edge / corner。

---

## 15. 自测题

1. 为什么梯度幅值可以表示边缘强度？
2. 梯度方向和边缘方向有什么关系？
3. 用 forward difference 计算 $G_x,G_y$ 时分别看哪个邻居？
4. 为什么 Laplacian 对噪声比 Gradient 更敏感？
5. LoG 为什么能减弱噪声影响？
6. Mexican hat function 指什么？
7. Moravec operator 的核心判断是什么？
8. Moravec 为什么要取多个方向响应的最小值？
9. 为什么 diagonal edges 可能被 Moravec 误判为 corners？
10. Harris detector 中 $E(u,v)$ 表示什么？
11. Harris matrix $M$ 的三个元素分别来自什么？
12. $\lambda_1,\lambda_2$ 都大说明什么？
13. 为什么 $R<0$ 常对应 edge？
14. Page 32 的 Harris 例题为什么最终判断为 corner？
15. Moravec 与 Harris 最大的理论区别是什么？

---

## 16. 本 tutorial 总结

Week 3 tutorial 通过几个核心练习巩固了 Part 3 的重点。

首先，gradient 方法用一阶差分计算图像灰度变化，边缘强度可用 $|G_x|+|G_y|$ 近似；梯度方向垂直于边缘方向。手算例题中，上方 7 到 0 的突变产生了强 $G_y$，因此 threshold 后顶部一行被判为边缘。

其次，Laplacian 是二阶导数方法，但对噪声非常敏感，因此需要先做 Gaussian smoothing，形成 LoG。LoG 可以理解为 Gaussian 平滑与 Laplacian 的组合。

最后，interest point 部分比较了 Moravec 和 Harris。Moravec 用窗口在多个方向平移后的差异判断角点；Harris 则通过局部梯度矩阵 $M$ 和 response function $R$ 更系统地判断 flat、edge 与 corner。Tutorial 的 Harris 例题中，中心窗口得到 $M=\begin{bmatrix}247&168\\168&247\end{bmatrix}$，$R=20583.2>0$，因此是 corner-like point。

> [!summary] 最重要的一句话
> **Gradient/LoG 是边缘检测的练习核心；Moravec/Harris 是角点检测的练习核心。做题时要抓住：边缘是单方向突变，角点是多方向都变化明显。**
