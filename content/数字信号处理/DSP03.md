DSP[数字信号处理 03](https://www.beyondpluto.cn/?p=854)
## **3.1 DSP系统**
### **3.1.1 介绍**
DSP系统是指**输入信号进入系统后产生输出信号**的处理过程。
常见的DSP系统类型：
- **线性 vs 非线性系统**（是否满足叠加性）
- **时不变 vs 时变系统**（系统是否随时间改变）
- **因果 vs 非因果 vs 反因果系统**（是否依赖未来输入）
- **无记忆 vs 有记忆系统**（是否需要存储过去输入）
- **稳定 vs 不稳定 vs 边界稳定系统**
**线性系统性质**：
- **齐次性（homogeneity）**
![image1](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image1.png)
- **加性（additivity）**
![image2](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image2.png)
**判断线性系统例子：**
![image3](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image3.png)
**判断时不变系统例子：**
![image4](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image4.png)
**LTI系统（线性时不变系统）**：同时具备线性和时不变性的系统。
优点：
- **可用卷积求解响应**
- **傅里叶和Z变换适用**
- **可以用极点和零点分析稳定性和频率响应**
### **3.1.2 差分方程**
在数字信号处理中常见的两种形式：**标准形式**和**递归形式**。
**标准形式（Standard Form）：**
![image5](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image5.png)
- 表示当前输出 y[n] 与过去的输出 y[n−1],…,y[n−N] 及输入 x[n],x[n−1],…,x[n−M] 的线性关系。
- 常用于**理论分析**，如解系统响应、分析系统性质。
**递归形式（Recursive Form）：**
![image6](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image6.png)
- 把原本含 y[n] 的等式整理成“**解出当前输出**”的形式；
- 适合实际程序中逐步计算每个输出值，**用于实现和仿真**；
- 显示出一个“递归”的过程：当前输出依赖过去的输出值。
**递归型差分方程（recursive difference equation）**的**特点：**说明输出依赖**过去的输出值**，所以它是**递归的**。
当前输出 y[n] 是由**过去的输出** y[n−1],y[n−2],…和 **当前及过去的输入** x[n],x[n−1],… 加权计算出来的。
## **3.2 时域响应**
### **3.2.1 求解差分方程**
### **1 一个一个试**
![image7](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image7.png)
### **2 利用Z变换（z-transform）**
**步骤详解：**
![image8](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image8.png)
|**步骤**|**目的**|
|---|---|
|整理方程|明确结构|
|Z变换|化为代数表达式|
|初始条件|帮助解方程|
|分式展开|准备反变换|
|逆Z变换|得到时间域表达式 y[n]y[n]|
**例子：**
![image9](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image9.png)
![image10](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image10.png)
![image11](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image11.png)
### **3.2.2 冲激响应（Impulse Response）**
**冲激响应 h[n]** 是系统对单位冲激输入 δ[n] 的输出。对于 LTI 系统，只要知道 h[n]，就能确定它对任意输入的响应。**冲激响应只适用于 LTI 系统**。
输出 y[n] 是输入 x[n] 与冲激响应 h[n] 的离散卷积（convolution）
**数学表达：**
![image12](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image12.png)
这个公式是 LTI 系统最重要的计算公式，**任何输入通过卷积都能求出输出**。
![image13](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image13.png)
**例子：**
- **非递归型冲激响应：**
![image14](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image14.png)
![image15](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image15.png)
- **递归型冲激响应：**
![image16](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image16.png)
![image17](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image17.png)
### **3.2.3 阶跃响应（Step Response）**
阶跃响应是系统对单位阶跃函数 u[n] 输入的输出。
![image18](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image18.png)
求阶跃响应方法：和冲激响应一样，只不过输入变为阶跃函数 u[n]。
**例子：**
![image19](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image19.png)
## **3.3 频域响应**
### **3.3.1 介绍**
它描述一个**线性时不变系统（LTI system）**对不同频率的正弦信号是如何响应的。频率响应告诉我们这个系统在每个频率下**如何改变输入信号的幅度和相位**。
形式上记为：
![image20](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image20.png)
也就是**系统单位冲激响应的DTFT**（离散时间傅里叶变换）。
- 频率响应用 H(ω) 表示，输入信号是 x[n]=ejωn。
- 系统对这个输入的输出是 y[n]=H(ω)ejωn。
这说明了两个关键点：
- **频率不变**：输入是 ejωn，输出也是这个形式，只是前面多了一个复数因子 H(ω)；
- **系统只改变幅度和相位**：而不改变频率。
**总而言之：**
- **输入是正弦波，输出还是正弦波**，频率不变，但系统会对其“变形”。
- 变形的方式就是“乘以”一个复数 H(ω)，这个数的模决定**放大/衰减**，相位角决定**延迟**。
- H(ω) 是通过对单位冲激响应 h[n] 做 **DTFT** 得到的。
在频域中，一个系统的频率响应 H(ω) 是一个**复数**，它可以被分解为：
![image21](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image21.png)
其中：
- |H(ω)|：**幅度响应（amplitude response）**
- ∠H(ω)：**相位响应（phase response）**
![image22](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image22.png)
同时，**离散时间傅里叶变换（DTFT）是 z 变换在单位圆上的特例**，即：
![image23](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image23.png)
**求解频率响应例子：**
![image24](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image24.png)
### **3.3.2 幅度响应（Amplitude Response）**
幅度响应的计算公式有两种等价形式：
- **1.用实部和虚部表示：**
![image25](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image25.png)
- **2.用共轭乘积表示：**
![image26](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image26.png)
对于**实信号系统**，频率响应有共轭对称性：
![image27](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image27.png)
**例子：**
![image28](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image28.png)
![image29](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image29.png)
![image30](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image30.png)
### **3.3.3 相位响应（Phase Response）**
相位响应描述的是：**输入信号的不同频率成分经过系统后，系统引入了多少“时间延迟”**。如果输入是多个不同频率的正弦波组成的信号，那么系统对每个频率的波可能会让它“提前”或“延后”一点，造成整体波形的变化。
### **相位响应的定义公式：**
![image31](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image31.png)
![image32](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image32.png)
- Im 和 Re 表示频率响应 H(ω) 的**虚部**和**实部**。
- 本质上是一个复数的极角（argument）计算。
|**项目**|**说明**|
|---|---|
|条件|H(ω)=e−jωn0|
|相位响应|∠H(ω)=−ωn0（线性相位）|
|含义|所有频率成分都延迟了 n0 个采样点|
|输出信号|相当于将输入信号整体向右平移 n0： y[n]=x[n–n0]|
|重要意义|系统不改变信号形状，只延迟，**不会失真**|
## **3.4 离散 LTI 系统（Discrete Linear Time-Invariant System）中的传递函数（Transfer Function）**
### **3.4.1 介绍**
离散 LTI 系统输出为**输入和单位脉冲响应的卷积**：
![image33](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image33.png)
**卷积定理（Z 变换中的重要性质）：**
![image34](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image34.png)
所以，离散 LTI 系统的**传递函数**就是输出与输入 Z 变换的比值：
![image35](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image35.png)
换言而之，传递函数其实就是**单位脉冲响应的 Z 变换**：
![image36](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image36.png)
### **3.4.2 极点与零点（Poles and Zeros）**
**传输函数形式：**
![image37](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image37.png)
- N(z)：分子多项式，对应**零点（zeros）**，决定信号在哪些频率被抑制或增强。
- D(z)：分母多项式，对应**极点（poles）**，极点的位置决定系统的**动态特性和稳定性**。
**极零图（Pole-Zero Plot）**指将极点用“×”、零点用“○”画在复平面上，单位圆（|z|=1）是判断稳定性的关键参考。
**示例：**
![image38](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image38.png)
![image39](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image39.png)
### **3.4.3 稳定性 Stability**
**稳定性分类：**
- **稳定系统（Stable systems）**：系统受到扰动后，会**回到平衡**或**进入稳态**，输出最终趋于一个有限值，常见于所有极点都在单位圆内的因果系统。
- **不稳定系统（Unstable systems）**：系统受到扰动后会**发散**（无限增大），输出会不断变大、无法控制，对应有一个或多个极点在单位圆外。
- **边界稳定系统（Marginally stable systems）**：系统既不会发散，也不会收敛。可能会：**持续震荡**（例如单位圆上的复数极点）；**保持某个恒定值**（例如单位阶跃响应）。极点通常位于单位圆上，且不重复。
![image40](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image40.png)
**判断方法：**
### **Step 1：确定极点（Poles）**
- 从系统的传输函数 H(z) 中找到所有极点。
- 极点是使分母为 0 的那些 z 值。
### **Step 2：判断所有极点是否在单位圆内 |z|<1**
- 是 → 系统是 **Stable（稳定）**
- 否 → 进入下一步
### **Step 3：判断是否有极点在单位圆外 |z|>1**
- 是 → 系统是 **Unstable（不稳定）**
- 否 → 进入下一步
### **Step 4：判断是否有极点正好在单位圆上 |z|=1**
- 如果存在**重复极点**（重根）：→ 系统是 **Unstable（不稳定）**
- 如果在单位圆上的极点**位置不同、各自唯一**：→ 系统是 **Marginally Stable（边界稳定）**
**例子：**
![image41](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image41.png)
![image42](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image42.png)
**稳定性和冲激响应关系**：
|**冲激响应特性**|**稳定性类型**|**极点特征**|
|---|---|---|
|输出趋于 0 或常数|稳定（Stable）|所有极点都在单位圆内 (|
|输出持续振荡，振幅不变|边界稳定（Marginal）|极点在单位圆上但**不重复**|
|输出随时间增长（多项式/指数）|不稳定（Unstable）|极点在单位圆上重复或在圆外|
**例子：**
![image43](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image43.png)
![image44](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image44.png)
![image45](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image45.png)
![image46](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image46.png)
![image47](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image47.png)
![image48](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image48.png)