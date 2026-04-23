核心问题是：

**怎么从大量全景 token 里，抽取少量最有价值的 token，再送进 VLM。**

适合：

- 全景 token 很多
- 你想做任务相关的压缩
- 你想把语言也引入桥接过程

------

## 5. 举个和你课题最相关的例子

假设你有：

- 360° 全景图经过 SphereViT 得到 1024 个 patch token
- DA² 得到深度 / 法向几何特征
- 后面接一个 VLM 做操作决策

### 用 projector 的做法

直接把这 1024 个 token 过一个线性层：
$$
T_{vis}' = W T_{vis}
$$
然后送进 VLM。

优点是简单。
 缺点是 token 太多，冗余大。

------

### 用 query bridge 的做法

先放 16 个可学习 query，去 1024 个 token 里 cross-attend：
$$
T_{bridge} = \text{CrossAttention}(Q_{16}, T_{vis})
$$
最后只输出 16 个摘要 token 给 VLM。

优点是：

- 更紧凑
- 更像“任务相关摘要”
- 更适合大范围全景输入

------

## 6. 和 Q-Former 的关系

如果你听过 Q-Former，那它本质上就很像一种 query bridge。

它的思想就是：

- 不把所有视觉 token 全送进大语言模型
- 而是用少量 learnable query 去提取视觉摘要
- 再把摘要送进语言模型

你这里可以做一个 **Sphere Query Bridge**：

- query 带球面位置先验
- query 专门去提全景里与任务相关的区域
- 比普通 Q-Former 更适合 360° 输入