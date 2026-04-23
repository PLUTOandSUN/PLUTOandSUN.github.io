## 0 总结
背景：
- arxiv预印本，阿里巴巴团队

解决问题：
- 提出了一种面向全景图像的视觉 Transformer 框架，用于从单张 360° 全景图中进行房间布局估计。

创新点：
- 通过**非均匀的 patch sampling 和针对不同来源的 patch embedding**，融合原始图像与多尺度 CNN 特征
- 提出**循环位置编码（RPE）**，通过随机起点消除水平绝对位置偏置，从而适配全景图的环形结构
- 引入**频域边缘增强模块**强化几何边界信息，并设计**基于三维空间的几何感知损失（3D loss）**，在真实空间中计算误差以缓解全景畸变影响
## 1 背景
与通过单张全景相机照片理解房间布局的CNN 的方法不同，提出了一种基于 Transformer 的方法，能够更好地利用全景图像中的全局依赖关系。CNN 更擅长局部模式提取，ViT 更擅长全局关系建模。


## 2 整体框架
模型输出一个大小为 $C × 1 × W$ 的张量。其中$C = 3$, 表示通道数。前两个通道分别表示天花板-墙体和地板-墙体的边界。最后一个通道表示墙与墙之间边界的概率。

整个框架由四个模块组成。分别是：主干网络（a）、Transformer 编码器（c）、边缘增强模块（b）和布局预测模块（d）。


全景图像首先输入主干网络以提取多尺度特征，同时也输入到边缘增强模块中。Transformer 编码器以原始图像、边缘图和多尺度特征作为输入，并输出一个特征向量用于布局预测。如下图所示：

![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260420143557779.png)

### 2.1 Backbone
主干网络是一个**卷积神经网络**，用于从全景图像中提取多尺度特征。在本文中使用 ResNet34，并将来自不同 ResNet 模块的中间特征图组合起来，作为多尺度特征，以捕捉低层和高层的视觉模式。

### 2.2 Vision Transformer Encoder
视觉 Transformer 编码器以原始图像和多尺度特征图作为输入，并输出一个房间布局特征向量。

下图展示了视觉Transformer编码器的整体架构

![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260420143539025.png)
编码器首先从原始图像和多尺度特征图中采样 patch,然后通过不同的嵌入操作，将不同类型的 patch 投影为不同的 patch embedding，所有的 patch embedding 都会附加一个循环位置编码（recurrent position embedding），并通过视觉 Transformer 主干网络预测房间布局特征向量。

#### 1 Patch Sampling
论文为多尺度特征图和原始图像设计了两种不同的采样方法：
- 对于多尺度特征图，沿水平方向采样竖直的 patch。具体来说，给定一个尺寸为 $C×W×H$ 的特征图，将其采样为 W 个大小为 $C×1×H$ 的 patch，其中 H 是特征图的高度，W 是特征图的宽度，C 是通道数。
- 对于全景图像，论文在整个图像上均匀采样方形 patch。

#### 2 Patch Embedding
通过不同的嵌入操作，将不同类型的 patch 投影为对应的 patch embedding。
- 对于多尺度特征图，采用高度压缩模块来计算来自多尺度特征图的 patch 的 embedding。该高度压缩模块是一个卷积层，包含 $C_emb$ 个卷积核，其大小为 $1 × H$，从而能够覆盖整个特征图的高度。对于一个尺寸为 $C × 1 × H$ 的 patch，高度压缩模块会将其映射为一个一维的 patch embedding，其尺寸为 $C_emb × 1 × 1$。
- 对于从全景图像中采样得到的 patch，使用一个简单的多层感知机（MLP）来计算其 patch embedding。

所有的 patch embedding 会被拼接在一起，作为视觉 Transformer 编码器的输入。

#### 3 Recurrent Position Embedding
现有的位置编码方法都是针对透视图像设计的。本文为全景图像设计了一种循环位置编码方法。透视图像与全景图像的一个主要区别在于，全景图像具有“滚动稳定性”，这意味着沿水平方向对全景图像进行任意像素的平移，其对应的三维布局与原始图像是相同的。这一特性表明，在水平方向上无需强调 patch 的绝对起始位置。

如下图所示，(a) 和 (b) 中的位置编码应当产生相同的结果。

![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260420150201776.png)
为了体现这一属性，论文在循环位置编码中引入了一个沿水平方向随机采样的起始位置。

具体来说，我们的递归位置嵌入计算方式如下：
- 全景图像：其中 $d_model$ 是位置嵌入的维度，pos 是从左侧开始、到右侧结束的绝对位置，而 randinit 是一个随机的初始位置。
![](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260420151026195.png)
- ResNet输出的多尺度特征：其中，$RPE_k$ 表示来自第 k 个 ResNet 模块特征图的 patch 的位置编码，$s_k$ 表示从第 k 个特征图中采样得到的 patch 数量（根据论文的采样方式，$s_k$ 等于第 k 个 ResNet 特征图的宽度）。
![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260420151201445.png)

#### 4 Vision Transformer Backbone
使用在 ImageNet 上预训练的 ViT 作为视觉 Transformer 的主干网络。与标准 ViT 相比，我们对 Transformer 编码器做了两个改动：
- 首先，移除了 ViT 中为目标分类任务设计的扩展 patch（classification token）。
- 其次，将来自多尺度特征图的所有 patch 的特征向量进行组合，作为最终输出的房间布局特征向量，其长度为 $∑_{k=1}^{N} s_k$，其中 N 表示特征尺度的数量。扩展开来，就是，来自多尺度特征图的所有 patch 特征向量也要经过 Transformer；它们会和原始全景图 patch 的 embedding 拼接在一起，统一送入 vision transformer encoder，最后再从 Transformer 输出中取出多尺度 patch 对应的特征来构成 room layout feature vector。

### 2.3 Layout Prediction
布局预测模块的结构如下图所示。
![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260420161543429.png)
- 首先将房间布局特征向量按照对应特征图的尺度，重新变换回多尺度特征表示。
- 随后，通过插值操作将不同尺度的特征调整为相同的长度，并在垂直维度上将这些特征进行拼接。
- 接着，使用文献中提出的 [[概念汇总/ConvSqueezeH 层]]，对多尺度特征在垂直方向上进行压缩。
- 最后，我们依次使用三个一维卷积层，其卷积核大小分别为 3、3 和 1，并结合批归一化（BN）和 ReLU 激活函数，输出墙与墙之间边界存在的概率 $y_w$，以及天花板-墙体边界 $y_c$ 和地板-墙体边界 $y_f$。

### 2.4 Edge enhancement
本文中，在频域中提取边缘信息。与文献]中使用的 LSD 方法相比，方法更加高效，并且能够取得更高的精度。边缘增强模块可以表示为：

$$E = F^{-1}(M \cdot F(I))$$
其中，I 表示全景图像，E 表示边缘增强后的图像，M 是一个二值掩码，对频域中的一部分频率分量进行采样，F 表示快速傅里叶变换（FFT），$F^{-1}$ 表示逆快速傅里叶变换。如下图所示：
![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260420164411856.png)
边缘增强的关键在于使用**掩码 M** 对频域的不同部分进行采样。众所周知，高频部分包含图像的边缘信息，而低频部分主要表示图像的整体内容（平均信息）。如下图（a）所示。因此，一个直观的掩码设计方式是使用高通滤波器。如文献[[概念汇总/Layoutnet]]所示，分别沿不同方向（如 x、y、z 轴）提取边缘有助于提升精度。为了在频域中提取不同方向的边缘，我们提出根据频域中三角函数的方向来设计掩码。不同方向的三角函数可以突出全景图中对应方向的边缘信息。所以，本文设计了两个掩码，分别用于提取水平方向和垂直方向的边缘。具体效果如下图（b）所示：
![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260420164856925.png)
位置坐标的三角函数方向和**掩码M**的具体计算公式为：
![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260420165407476.png)
![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260420165419828.png)

### 2.5 Loss Functions

PanoViT 的损失函数由两部分组成：角点损失 $L_{cor}$ 和边界损失 $L_{bon}$。其中，$L_{cor}$ 使用二元交叉熵来监督墙角（corner）的位置预测，而 $L_{bon}$ 则用于约束天花板-墙体和地板-墙体边界的预测精度。与传统方法直接在全景图像的二维像素空间计算误差不同，PanoViT 进一步设计了**3D 几何感知损失**：先将图像中的像素点通过经纬度映射到三维空间，再计算预测边界与真实边界对应三维点之间的 L1 距离，从而更真实地反映全景图中的空间几何误差。这种设计能够有效缓解全景图像畸变带来的影响，使模型在结构重建任务中获得更高的精度和更强的几何一致性。

## 3 baseline对比
![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260421011720677.png)
![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260421011729057.png)
