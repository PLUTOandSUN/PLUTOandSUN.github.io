
> [!info] 课件来源
> 原始课件：[[课程笔记/图像与视频处理/附件/Part 2 - Image Transformation, Colour Images and Image Filtering/4 EBU6230_image_transformations.pdf]]  
> 本小节整理 **Part 2 的第 1 个 PPT：Image Transformation**。当前文件后续已继续整理 Colour Images 与 Image Filtering。

---

## 0. 这节课在讲什么

这节课的核心是：**图像变换如何在像素层面改变图像**。

PPT 把它分成两类：

- **Algebraic transformations 代数变换**：改像素值，不改位置；
- **Geometric transformations 几何变换**：改像素位置，必要时再用插值补值。

一句话概括：

> **代数变换处理“值”，几何变换处理“坐标”。**

---

## 1. 学习目标

PPT 希望你掌握：

- 什么是 **spatial domain processing 空间域处理**；
- 什么是 **algebraic transformation** 和 **geometric transformation**；
- 怎样用 **affine matrix 仿射矩阵** 实现几何变换。

空间域处理的意思很直接：直接对图像像素做运算，而不是先去频域。

---

## 2. 图像变换的总公式

图像变换通常写成：

$$
g(x,y)=T[f(x,y)]
$$

其中：

| 符号 | 含义 |
|---|---|
| $f(x,y)$ | 输入图像 |
| $g(x,y)$ | 输出图像 |
| $T$ | 变换算子 |
| $(x,y)$ | 像素坐标 |

如果是多幅图像，$T$ 也可以作用在一组输入图像上。

---

## 3. Algebraic transformations：代数变换

### 3.1 基本思想

代数变换就是对像素值逐点做算术或逻辑操作：

- 加法
- 减法
- 乘法
- 除法
- 逻辑运算

通常要求两幅图像尺寸一致，才能逐像素对应。

### 3.2 图像相减

$$
g(x,y)=f(x,y)-h(x,y)
$$

作用：**突出差异**。

典型用途：

- 背景减除
- 变化检测
- 边缘近似

> [!tip]
> 如果两幅图像几乎一样，相减后大部分区域接近 0；如果某处变化明显，那一块就会被显出来。

### 3.3 图像平均与降噪

如果噪声图像满足：

$$
g(x,y)=f(x,y)+\eta(x,y)
$$

且噪声独立、均值为 0，那么多张图像求平均：

$$
\bar{g}(x,y)=\frac{1}{K}\sum_{i=1}^{K}g_i(x,y)
$$

会让噪声减弱，期望上回到原图：

$$
E[\bar{g}(x,y)]=f(x,y)
$$

直觉：

- 真实信号每张图都相同；
- 噪声每次随机变化；
- 平均后噪声会相互抵消。

### 3.4 代数操作的三个副作用

#### Non-invertible 不可逆

很多操作做完后无法唯一恢复原图。因为多个输入可能对应同一个输出。

#### Clipping 截断

8-bit 图像范围通常是 $[0,255]$。如果计算结果超出范围，就会被压到边界：

$$
230+80=310\;>\;255
$$

于是结果会变成 255，细节丢失。

#### Normalization 归一化

把原始范围 $[a,b]$ 映射到目标范围 $[c,d]$：

$$
g=c+(d-c)\frac{f-a}{b-a}
$$

对 8-bit 图像常取 $c=0,d=255$。

> [!warning]
> clipping 是“硬截断”，normalization 是“整体拉伸”。前者更容易丢细节。

---

## 4. 用代数变换理解边缘

### 4.1 什么是边缘

边缘就是图像强度突然变化的位置。

### 4.2 差分近似导数

如果把图像平移一点再相减，就能近似导数：

前向差分：

$$
\frac{f(x+\Delta x)-f(x)}{\Delta x}
$$

中心差分：

$$
\frac{f(x+\Delta x/2)-f(x-\Delta x/2)}{\Delta x}
$$

中心差分一般更好。

### 4.3 有限差分滤波器

差分可以写成线性滤波：

$$
[-1,\,1]
$$

或中心差分：

$$
\left[-\frac12,\,0,\,\frac12\right]
$$

这就是很多边缘检测算子的基础。

### 4.4 一阶导数和二阶导数

- 一阶导数：边缘处出现 **peak**；
- 二阶导数：边缘处出现 **zero-crossing**。

---

## 5. Gradient：梯度

二维图像的梯度写作：

$$
\nabla f(x,y)=\left[\frac{\partial f}{\partial x},\frac{\partial f}{\partial y}\right]
$$

梯度是向量，不是标量。

### 5.1 梯度幅值

$$
|\nabla f|=\sqrt{\left(\frac{\partial f}{\partial x}\right)^2+\left(\frac{\partial f}{\partial y}\right)^2}
$$

含义：

- 值大：强边缘；
- 值小：弱边缘。

### 5.2 梯度方向

$$
\operatorname{dir}(\nabla f)=\tan^{-1}\left(\frac{\partial f/\partial y}{\partial f/\partial x}\right)
$$

梯度方向通常和边缘方向垂直。

### 5.3 方向导数

任意方向 $\theta$ 的导数可写成：

$$
\frac{\partial f}{\partial \theta}
=\cos\theta\frac{\partial f}{\partial x}+\sin\theta\frac{\partial f}{\partial y}
$$

这说明：只要知道 x、y 两个方向的导数，就能组合出任意方向的响应。

---

## 6. Geometric transformations：几何变换

### 6.1 基本思想

几何变换改变的是**像素位置**，不是像素值本身。

它包含两步：

1. 坐标变换；
2. 插值补值。

### 6.2 一般坐标变换

可以写成：

$$
(x',y')=(a(x,y),b(x,y))
$$

意思是：原图中的点映射到新坐标系中的新位置。

---

## 7. Affine transformation：仿射变换

仿射变换会保持：

- 点
- 直线
- 平行关系
- 线段比例

二维线性部分可写成：

$$
\begin{bmatrix}
x'\\y'
\end{bmatrix}
=
\begin{bmatrix}
a&b\\c&d
\end{bmatrix}
\begin{bmatrix}
x\\y
\end{bmatrix}
$$

行列式：

$$
\det(A)=ad-bc
$$

如果行列式不为 0，矩阵可逆。

仿射变换常见特例：

- 平移
- 缩放
- 旋转
- 错切
- 镜像

---

## 8. 常见几何变换

### 8.1 Scaling：缩放

$$
\begin{bmatrix}
x'\\y'
\end{bmatrix}
=
\begin{bmatrix}
a&0\\0&b
\end{bmatrix}
\begin{bmatrix}
x\\y
\end{bmatrix}
$$

- $a,b>1$：放大；
- $0<a,b<1$：缩小；
- $a\ne b$：非等比例缩放。

### 8.2 Rotation：旋转

绕原点旋转：

$$
\begin{bmatrix}
x'\\y'
\end{bmatrix}
=
\begin{bmatrix}
\cos\theta&-\sin\theta\\
\sin\theta&\cos\theta
\end{bmatrix}
\begin{bmatrix}
x\\y
\end{bmatrix}
$$

即：

$$
x'=x\cos\theta-y\sin\theta
$$

$$
y'=x\sin\theta+y\cos\theta
$$

### 8.3 Shear / Skew：错切

一个常见形式：

$$
\begin{bmatrix}
x'\\y'
\end{bmatrix}
=
\begin{bmatrix}
1&sh\\0&1
\end{bmatrix}
\begin{bmatrix}
x\\y
\end{bmatrix}
$$

即：

$$
x'=x+sh\cdot y,\quad y'=y
$$

效果：正方形会变成平行四边形。

### 8.4 Reflection：镜像

关于 y 轴：

$$
\begin{bmatrix}
-1&0\\0&1
\end{bmatrix}
$$

关于 x 轴：

$$
\begin{bmatrix}
1&0\\0&-1
\end{bmatrix}
$$

关于原点：

$$
\begin{bmatrix}
-1&0\\0&-1
\end{bmatrix}
$$

---

## 9. 为什么 2×2 矩阵不能表示平移

平移是：

$$
x'=x+t_x,\quad y'=y+t_y
$$

这不是纯线性变换，因为有常数项。

所以 2×2 矩阵不够，要用 **homogeneous coordinates 齐次坐标**。

---

## 10. Homogeneous coordinates：齐次坐标

把二维点写成三维向量：

$$
\begin{bmatrix}x\\y\\1\end{bmatrix}
$$

这样平移就可以写成 3×3 矩阵：

$$
\begin{bmatrix}
1&0&t_x\\
0&1&t_y\\
0&0&1
\end{bmatrix}
\begin{bmatrix}
x\\y\\1
\end{bmatrix}
=
\begin{bmatrix}
x+t_x\\y+t_y\\1
\end{bmatrix}
$$

齐次坐标的好处是：

- 平移可以写进矩阵；
- 多个变换可以统一合成；
- 计算机图形和图像处理实现更方便。

---

## 11. 复合变换：Compound transformations

多个变换可以合成一个矩阵。

例如：先平移，再旋转，再平移回去。

对列向量来说，顺序要**从右往左**读：

$$
M=T(x_0,y_0)R(\theta)T(-x_0,-y_0)
$$

这也是“绕任意点旋转”的标准套路。

> [!important]
> 矩阵乘法顺序很重要，通常 $AB\ne BA$。

---

## 12. 绕任意点旋转

步骤：

1. 把旋转中心移到原点；
2. 绕原点旋转；
3. 再移回去。

所以总矩阵是：

$$
M=T(x_0,y_0)R(\theta)T(-x_0,-y_0)
$$

这一步是 Part 2 里很容易考的概念。

---

## 13. Image warping：图像扭曲 / 重映射

图像扭曲本质是：

$$
(x,y)\rightarrow(x',y')=W(x,y)
$$

目标是把源图像映射到新图像。

### 13.1 Forward warping

把源像素“推”到目标图。

问题：会出现空洞，因为某些目标像素没人落上去。

### 13.2 Inverse warping

从目标图像出发，对每个像素反查源位置：

$$
(x,y)=W^{-1}(x',y')
$$

然后从源图插值取值。

优点：不会出现 holes。

---

## 14. Bilinear interpolation：双线性插值

当反查坐标不是整数时，需要插值。

设四个邻近像素为 $f_{00},f_{10},f_{01},f_{11}$，则：

$$
f(x,y)\approx (1-\alpha)(1-\beta)f_{00}
+\alpha(1-\beta)f_{10}
+(1-\alpha)\beta f_{01}
+\alpha\beta f_{11}
$$

插值会让图像略微变软，但能避免空洞和锯齿。

---

## 15. 本节课最该记住的点

1. **代数变换**：改像素值；
2. **几何变换**：改像素位置；
3. **边缘** 本质上是强度突变；
4. **梯度方向** 和边缘方向垂直；
5. **2×2 矩阵不能平移**，平移要靠齐次坐标；
6. **矩阵组合顺序很重要**；
7. **几何变换实际实现常用 inverse warping + interpolation**。

---

## 16. 关键公式速记

### 代数变换

$$
g=f-h
$$

$$
g=f+\eta
$$

$$
\bar{g}=\frac1K\sum_{i=1}^{K}g_i
$$

### 归一化

$$
g=c+(d-c)\frac{f-a}{b-a}
$$

### 导数与梯度

$$
\frac{f(x+\Delta x)-f(x)}{\Delta x}
$$

$$
\nabla f=\left[\frac{\partial f}{\partial x},\frac{\partial f}{\partial y}\right]
$$

$$
|\nabla f|=\sqrt{f_x^2+f_y^2}
$$

### 旋转与平移

$$
\begin{bmatrix}
x'\\y'
\end{bmatrix}
=
\begin{bmatrix}
\cos\theta&-\sin\theta\\
\sin\theta&\cos\theta
\end{bmatrix}
\begin{bmatrix}
x\\y
\end{bmatrix}
$$

$$
\begin{bmatrix}
x'\\y'\\1
\end{bmatrix}
=
\begin{bmatrix}
1&0&t_x\\
0&1&t_y\\
0&0&1
\end{bmatrix}
\begin{bmatrix}
x\\y\\1
\end{bmatrix}
$$

---

## 17. 和后续课程的关系

- 前置：[[../附件/归档笔记/Part 1|Part 1]] 里学的像素、图像表示、直方图；
- 后续：Part 2 的 Colour Image 和 Image Filtering 会继续用到本节的空间域思想；
- 实践：MATLAB / Python 做图像旋转、缩放、插值、降噪、边缘检测时，本节公式都会直接用到。

> [!quote]
> 如果只记一句话：
> **图像变换就是“值的运算 + 坐标的运算”，而几何变换在实现时几乎总是离不开逆映射和插值。**


---
