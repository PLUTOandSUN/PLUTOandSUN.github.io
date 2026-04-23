## 1. projector 是什么

projector 就是一个**特征投影层**。

它做的事情很简单：

**把一种特征空间里的向量，映射到另一种特征空间里。**

比如你从 SphereViT 得到的 token 维度是 768 维，但你后面的 VLM 视觉输入维度是 1024 维，这时就要用 projector：
$$
T' = \text{Projector}(T)
$$
最常见就是：

- 线性层（Linear）
- 两层 MLP
- 带 LayerNorm 的小网络

------

### 直观理解

你可以把 projector 理解成一个“翻译器”：

- 前端说的是 **SphereViT 的语言**
- 后端 VLM 说的是 **CLIP / PaliGemma / OpenVLA 的语言**

projector 的作用就是把前端特征翻译成后端能接收的格式。

------

### 在你这个任务里 projector 可以投什么

比如：

- **patch token projector**：把 SphereViT 的视觉 token 投到 VLM 视觉空间
- **geometry projector**：把 depth / normal / point cloud token 投到 VLM 空间
- **attention projector**：把注意力摘要 token 投到统一空间

这样最后就能拼起来送入 VLM：
$$
[T_{vis}', T_{geo}', T_{att}', T_{lang}]
$$

------

## 2. query bridge 是什么

query bridge 可以理解成一种**带“查询能力”的桥接模块**，比 projector 更主动。

它不是简单把特征“变换一下”，而是：

**用一组 query 去前端特征里提取最有用的信息，再生成给后端的 token。**

------

### 数学上看

它通常像这样：
$$
Q_{bridge} = \text{learnable queries}
$$
这里：

- $Q_{bridge}$：桥接查询向量
- $T_{input}$：你前端的大量 token，比如 SphereViT token
- $T_{out}$：抽取出来的少量、精炼后的 token

------

### 直观理解

projector 像：

**把整本书翻译成另一种语言。**

query bridge 像：

**先提出几个关键问题，再从整本书里摘出最相关的内容，整理后交给下游。**

所以 query bridge 比 projector 多了一步：

- projector：直接映射
- query bridge：先“选取/压缩/摘要”，再输出

------

## 3. 为什么你可能更需要 query bridge

因为全景图 token 很多。

如果你直接把所有 SphereViT token 全送进 VLM，会有两个问题：

1. token 太多，算力开销大
2. 很多 token 对当前任务没用

这时 query bridge 就很合适，因为它可以：

- 压缩 token 数量
- 保留任务相关信息
- 丢掉冗余区域
- 提取全局摘要 / 几何摘要 / 目标区域摘要

------

## 4. 你这个方向里二者的区别

### projector

偏“格式对齐”

核心问题是：

**怎么把特征维度、分布、空间对齐到 VLM 能接受的样子。**

适合：

- 你已经知道哪些 token 要送进去
- 只是需要统一维度和表示空间