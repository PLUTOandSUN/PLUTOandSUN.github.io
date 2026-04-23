## 0 论文背景
CVPR2025,腾讯混元

## 1 想解决的问题
输入一张 **360° 全景图（panorama）**，直接预测每个像素到相机中心的距离，并且希望这个模型不仅在训练过的数据域里有效，还要有很强的 **zero-shot 泛化能力**。

主要面临两个问题
1. 训练数据太少
2. ERP 全景图的球面畸变很难处理

因此，本篇论文主要提出了两个创新点：
1. 作者提出了一个 **panoramic data curation engine**，把大量已有的高质量透视 RGB-D 数据，自动变成可用于全景深度训练的数据。
2. 作者提出了 **SphereViT**，让 ViT 在处理 ERP 全景图时显式利用球面坐标信息，减少球面投影造成的畸变影响。

## 2 panoramic data curation engine
这个模块的核心创新点是把普通的RGB-D转化成全景图
![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260422160331226.png)

从普通透视 RGB-D：先利用 [[概念汇总/Perspective-to-Equirectangular 投影]]把透视图映射到 ERP 全景坐标系中，得到一个只覆盖局部视野的 partial panorama。由于透视图的视场有限，所以它只能填满球面中的一小块区域，图中球面高亮部分就是这张图的 FoV 覆盖范围。然后作者使用 [[概念汇总/FLUX-I2P]] 对 RGB 的缺失区域进行全景补全，生成完整的 full panorama 作为训练输入；

深度真值：只做投影、不做补全，以避免伪造深度监督。

这套流程让大量高质量透视 RGB-D 数据能够转化为全景训练数据，从而大幅扩充全景深度估计的数据规模。

对于我来说，本质是RGB图像补成完整全景，深度真值只保留真实投影部分，投射到ERP上。

## 3 SphereViT

先提取普通 ViT 图像特征，再构造一个由球面坐标得到的 spherical embedding，然后让图像特征通过 cross-attention去“查询”球面几何信息，得到更适合全景图的特征。
![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260422163356877.png)

具体做法是：
1. 先把 ERP 全景图中每个像素的位置 $(u,v)$ 转成球面上的方位角和极角 $(\phi,\theta)$，再把这两个角度通过[[概念汇总/多频率的正弦余弦编码|多频率的正弦余弦编码]]扩展成与图像特征同维度的 **Spherical Embedding $E_{sphere}$**；
2. 随后，不再像普通 ViT 那样把位置编码直接加到图像特征上，而是让 ViT 提取出的图像特征 $Z$ 作为 Query，球面嵌入 $E_{sphere}$ 作为 Key 和 Value 做 **cross-attention**，从而让图像特征主动去“学习”全景图背后的球面几何关系，得到对球面畸变更敏感、更符合真实空间结构的特征表示。

[[概念汇总/相关公式|相关公式]]

左下角的图把这个过程可视化了：左下角的球体和角度场 $A$ 对应公式里由 $(u,v)$ 计算 $(\phi,\theta)$ 的步骤，接着被编码成 Spherical Embedding $E_{sphere}$；中间的 ViT Image Feature $Z$ 和 $E_{sphere}$ 在 CrossAttn 模块里交互；交互后的 SphereViT 特征再用于预测 **Distance** 和 **Normal**，并进一步恢复 **3D Point Cloud**，所以整张图完整展示了“球面坐标编码 → cross-attention 注入几何信息 → 提升深度/法向/三维重建质量”的整条链路。

## 4 损失函数
SphereViT 训练时同时用距离损失和法向损失进行监督。
其中：
- 一个是距离损失 $\mathcal{L}_{dis}$，用于约束全局距离值的准确性；
- 另一个是法向损失 $\mathcal{L}_{nor}$，用于促进局部几何表面的平滑与锐利，尤其是在那些距离值相近、但表面法向变化很大的区域。

在训练 SphereViT 时，作者对距离损失 $\mathcal{L}_{dis}$ 和法向损失 $\mathcal{L}_{nor}$ 都采用逐像素的 L1 差异最小化：
$$
\mathcal{L}_{dis}
=
\frac{1}{|\Omega|}
\sum_{p \in \Omega}
\left|
\hat{D}^{med}_p - D^\star_p
\right|,
\qquad
\mathcal{L}_{nor}
=
\frac{1}{|\Omega|}
\sum_{p \in \Omega}
\left|
\hat{N}_p - N^\star_p
\right|,
$$

总损失是两者的加权和：
$$
\mathcal{L} = \lambda_d \mathcal{L}_{dis} + \lambda_n \mathcal{L}_{nor},
$$
其中 $\lambda_d$ 和 $\lambda_n$ 是两个标量权重。

由于任务是尺度不变距离估计，作者先对预测距离做中位数对齐，再计算逐像素 L1 损失，最终将两项损失加权求和作为总训练目标。

