## 1 全景图特征和面临的问题
绝大部分全景图的输出是ERP = **Equirectangular Projection（等距柱状投影）**

简单理解： **把一个球面“展开”成一张长方形图片**

特点：

- 横向：360°（完整一圈）
- 纵向：180°（从天到地）
- 常见比例：**2:1（宽:高）**
- 中间区域 → 正常
- 上下（天/地）→ 被拉伸
- 左右两边 → 实际上是“连在一起”的

ERP 图像放进 Transformer，相比普通透视图，主要有四类问题：
- 第一，**ERP 有强几何畸变**。球面被展开成平面后，越靠近顶部和底部拉伸越严重，所以普通 ViT 里“大小一样的方形 patch”在真实球面上代表的面积和形状并不一样。这样一来，普通图像里成立的局部统计规律在 ERP 上会被破坏，token 的几何含义也不一致。
- 第二，**ERP 左右边界在图像上看似断开，但在球面上其实是相邻的**。普通 Transformer 若按平面图像处理，会把最左列和最右列当成远距离 token，破坏全景图的周期性。
- 第三，**普通位置编码不适合 ERP/球面图像**。标准 ViT 的绝对位置编码默认是平面坐标系，但全景图在水平方向有循环性、在垂直方向有纬度相关的几何变化，所以普通 PE 会把“几何上等价”的位置编码成不合理的差异。
- 第四，**全景任务往往比普通分类更依赖全局结构，但又不能丢掉局部几何细节**。

## 2 先前工作
### 2.1 PanoFormer: Panorama Transformer for Indoor 360° Depth Estimation（ECCV 2022）
**做出第一个专门面向全景深度估计的 Transformer，让模型既能减轻全景畸变影响，又能更好地感知场景几何结构。**

解决的问题是**如何从一张室内 360° 全景图里，估计出每个像素的深度**。

作者提出了一个模型：**PanoFormer**。  
它的核心思想可以概括成两句话：

- **先在 token 构造阶段尽量避开全景畸变，  
- **再在 attention 阶段让 token 能顺着场景结构“流动”。**

 **创新点1： tangent patch：在球面切平面上取 patch，减少畸变**

普通 ViT 是直接在图像平面上切 patch。  
但如果直接在 ERP 图上切 patch，会把严重畸变的区域也当作普通局部块处理，这不合理。

所以作者提出：

- 不直接在 ERP 平面上规则取 patch
- 而是以某个中心 token 为基准
- 在它对应的**球面切平面（tangent plane）**上找 8 个邻近位置
- 再把这些位置映射回 ERP 图像上取样

这样形成的 patch，论文称为 **tangent patch**。

这一步的直觉是：

**在球面几何上定义邻域，比在畸变后的 ERP 平面上定义邻域更合理。**
![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260421021526210.png)

**创新点2：token flow：让 token 顺着物体结构移动**(待研究)
先按球面几何去找“应该关注的邻域 token”，减少全景图畸变；再让这些 token 通过可学习的 flow 沿着场景结构微调位置，从而更好地感知几何结构并做深度估计。

PST Block 本质上还是一个 Transformer block，但它不是普通的 ViT block。  
普通 Transformer block 一般是：

- 输入特征
- 做 self-attention
- 再做 FFN
- 残差连接输出

而 PST Block 把最关键的 **self-attention** 换成了作者自己设计的 **PSA（Panorama Self-Attention）**。  
同时，又把普通 FFN 换成了 **LeFF**，用来增强局部特征。
![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260421021725145.png)

### 2.2 PAVER: Panoramic Vision Transformer for Saliency Detection in 360° Videos（ECCV 2022）
这篇论文解决的是 **360°视频显著性预测（saliency detection）** 问题。问题在于360°视频天然存在几何畸变和边界不连续。

景视频常见格式比如 ERP（equirectangular projection，等距柱状投影），会把球面展开成平面。这样一来：

- 靠近两极的位置会被严重拉伸
- 左右边界其实在球面上是连着的，但在平面图上却被切开了
- 普通图像/视频模型学到的卷积或 patch 划分方式，直接拿来处理 360° 内容会出错

作者提出了一个模型：**PAVER（Panoramic Vision Transformer）**。
![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/20260421015339608.png)
我主要关注Encoder部分。

普通 ViT 是直接按平面规则把图像切成 patch，但在 360° ERP 图像上这样切会导致严重畸变。于是作者引入了 **deformable convolution**：

- 对于球面上每个 patch 中心点，先根据它的经纬度确定局部切平面
- 计算这个局部切平面映射回 ERP 图像时的采样偏移
- 用 deformable conv 按这些偏移采样，得到近似无畸变的局部 patch 表示

而且这些 offset 不是训练出来的，而是**根据球面几何公式一次性算好并固定**。
### 2.3 PanoViT: Vision Transformer for Room Layout Estimation from a Single Panoramic Image（2022 arXiv）
[[PanoViT：用于从单张全景图像估计房间布局的视觉Transformer]]

#### PanoSwin: A Pano-Style Swin Transformer for Panorama Understanding（CVPR 2023）
它把 Swin Transformer 的窗口机制改造成了 **Pano-style Shift Windowing**，专门处理 panorama 的 **左右首尾相连** 和 **极区连续性** 问题。

#### GFormer: Equirectangular Geometry-biased Transformer for 360 Depth Estimation（ICCV 2023）
提出 **geometry-biased local attention**，把 equirectangular 几何偏置直接注入局部 attention。

#### Open Panoramic Segmentation（ECCV 2024）
**如何让模型只用普通视角（pinhole）的标注图像训练，却能在测试时直接理解 360° 全景图，而且还能识别开放词汇里的类别**。

#### SphereUFormer: A U-Shaped Transformer for Spherical 360 Perception（CVPR 2025）
不同于传统基于等距矩形投影的方法，该工作直接在球面空间中进行建模，通过提出球面局部自注意力机制、球面位置编码以及球面下采样策略，有效避免了投影畸变问题。

#### DA²: Depth Anything in Any Direction
[[Depth Anything in Any Direction：一种高精度、具备强零样本泛化能力、并且完全端到端的全景深度估计方法]]


## 3 与VLM和VLA的联系
全景视觉领域已经从早期基于 CNN 的畸变补偿与局部特征建模，发展到以 Transformer/ViT 为核心的全局关系建模与球面几何感知，但现有方法主要停留在深度、分割和布局等感知任务层面；与此同时，VLM 和 VLA 已经在单视角图像上实现了从视觉理解到语言推理再到动作决策的闭环，却缺乏对 360°全局环境的感知能力，因此两者的关键联系在于：**利用全景 Transformer 提供完整场景表征，将其作为输入接入 VLM/VLA，从而为机器人在复杂真实场景中的认知与交互提供更强的信息基础。**

## 4 一点想法
目前全景图像ViT相关工作已经不少，但是就如之前所说，利用全景 Transformer 提供完整场景表征，将其作为输入接入 VLM/VLA，从而为机器人在复杂真实场景中的认知与交互提供更强的信息基础的工作还不存在。

因此，我的想法是将 全景相机的ViT作为一个面向 360° 全景输入的几何感知视觉前端，先从全景图中提取同时包含语义信息、球面结构信息和注意力关系的视觉 token，再将这些 token 通过轻量 [[概念汇总/projector|projector]] 或 [[概念汇总/query bridge|query bridge]] 对齐到 VLM 的输入空间，与语言指令和机器人状态共同送入 VLM / VLA 主干进行跨模态推理，最后接一个类似 π0 的 action expert 或 flow matching 动作头输出连续动作；这样做的核心优势在于，全景相机的ViT能显式建模全景图的球面畸变与空间几何，又能补充可操作的 3D 结构约束，从而让 VLA 不只是“看见全景”，而是真正具备面向全景场景的空间理解、目标定位和动作决策能力。