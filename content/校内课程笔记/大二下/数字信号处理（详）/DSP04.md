DSP[数字信号处理 04 Filters](https://www.beyondpluto.cn/?p=853)
## **4.1 介绍**
**模拟滤波器**处理连续时间信号（analog signal），用电阻、电容、电感等物理元件构成。
**数字滤波器**处理离散时间信号（digital signal），用加法器、乘法器、延迟器等模块实现，或由软件程序完成。
**数字滤波器的主要应用**：
- **信号分离（Signal Separation）**：去除干扰或其他信号。
- **信号恢复（Signal Restoration）**：修复受损信号。
## **4.2 滤波器的表示**
### **4.2.1 基本运算符号：**
它们用于构建和表示数字滤波器的实现结构。
![image1 2|image1 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image1%202.png)
![image2 2|image2 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image2%202.png)
**例子：**
![image3 2|image3 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image3%202.png)
### **4.2.2 差分方程（Difference Equation）**
这是描述数字滤波器最基础的方法，类似于离散时间系统的“动态方程”：
![image4 2|image4 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image4%202.png)
**用法说明：**
- 可用于手动推导冲激响应、z变换
- 输入 x[n]=δ[n] 时，输出即为冲激响应 h[n]
- 是绘制 Block Diagram 的基础
### **4.2.3 传递函数（Transfer Function）**
由差分方程通过 Z 变换得到传递函数：
![image5 2|image5 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image5%202.png)
**特点：**
- 表示系统在**Z域**的输出与输入之比
- 可用极点-零点（Pole-Zero）分析图判断**系统稳定性**
- 频率响应 H(ejω) 可由 H(z) 取单位圆 |z|=1 得出
MATLAB 中的 filter(b, a, x) 用法解释：
这个函数实现的是：
![image6 2|image6 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image6%202.png)
- b：输入信号的系数 b0,b1,…，对应**分子**
- a：输出信号的系数 a0,a1,…，对应**分母**
- x：原始输入信号序列（向量）
注意：a(1)（即 a0）不能为 0，通常为 1。
假设系统的传递函数为：
![image7 2|image7 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image7%202.png)
那么 MATLAB 代码为：
|   |   |
|---|---|
||b = [1, -0.5]_; % 分子系数_|
||a = [1]_; % 分母系数_|
||x = [0, 1, 1, 2]_; % 输入信号_|
||y = filter(b, a, x)_; % 输出信号_|
输出的 y 就是滤波后的离散信号。
## **4.3 时域响应**
### **4.3.1 介绍**
**时域响应（Time-Domain Response）**描述的是**信号在时间上如何变化**。说明何时（when）一个事件发生和幅度（what）是多少。**每一个采样点**本身就具有完整含义，不依赖其他点。
### **4.3.2 Impulse Response**
输入单位冲激 δ[n]，输出即为系统的冲激响应 h[n]。决定系统是 **FIR**（有限冲激响应）还是 **IIR**（无限冲激响应）：
- **FIR**：h[n] 在有限范围内非零
- **IIR**：h[n] 在无限范围内非零（但衰减）
### **4.3.3 Step Response**
**阶跃响应**描述的是系统在输入发生“突然变化”时的反应，通常是从 0 跳变到 1 的单位阶跃函数：
![image8 2|image8 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image8%202.png)
**三个主要参数**：
**Settling Time（稳定时间）**：指输出在扰动后进入并保持在稳态值附近所需的时间，衡量系统响应速度。
![image9 2|image9 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image9%202.png)
**Overshoot（超调）**：指输出第一次超过最终稳态值的最大偏差，反映系统是否“反应过度”。
![image10 2|image10 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image10%202.png)
**Phase Linearity（相位线性）**：如果系统相位响应是线性的，则不同频率成分不会发生时域错位，这是判断系统是否会导致波形“失真”的关键指标。
![image11 2|image11 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image11%202.png)
|**性能指标**|**描述**|**目标表现**|
|---|---|---|
|Settling Time|响应进入容差范围所需时间|越短越好（快速稳定）|
|Overshoot|最大过冲量|越小越好（最好为 0）|
|Phase Linearity|响应对称性，反映相位是否线性|上升/下降对称|
## **4.4 频域响应**
### **4.4.1 介绍**
**频域响应（Frequency-Domain Response）**描述的是**系统对周期性信号（正弦、复指数）**的响应情况。它解释系统在不同频率下是**增强**、**抑制**还是**不变**。**单个频域采样点**（如某个频率下的增益）无法独立说明系统行为，需整体频谱。
**频率响应**表示滤波器如何改变输入信号中不同频率成分。可以分成两个部分：
- **幅度响应（Amplitude Response）**：反映信号中各个频率的“强度”如何被滤波器改变。
- **相位响应（Phase Response）**：反映各频率成分的“时序”（相位）如何被改变。
幅度响应中有三个关键区域：
- **通带（Passband）**：允许信号通过的频率范围，要求“无波纹”以保证信号不失真。
- **过渡带（Transition Band）**：通带与阻带之间的过渡区域，过渡带越窄，滤波器越理想。
- **阻带（Stopband）**：信号会被抑制的频率区域，阻带衰减越强越好。
![image12 2|image12 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image12%202.png)
**Passband**对比：
![image13 2|image13 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image13%202.png)
**Transition band**对比：
![image14 2|image14 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image14%202.png)
**Stopband**对比：
![image15 2|image15 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image15%202.png)
**截止频率**是**通带（passband）与过渡带（transition band）之间的边界**，在这个频率点，滤波器的输出幅度开始明显下降。
- 模拟滤波器中，截止频率通常指的是**输出幅度从 1 降低到 0.707** 的点。也就是功率下降了一半，对应于 **3 dB（分贝）**。
- 数字滤波器中，一些常见的定义包括幅度下降到：**99%**，**90%**，**70.7%**（与模拟一致），**50%**等
在MATLAB中提供了几个函数来帮助你分析滤波器的响应：
|**函数**|**含义**|
|---|---|
|[h,t] = impz(b, a, n)|计算**冲激响应（Impulse Response）**|
|[h,t] = stepz(b, a, n)|计算**阶跃响应（Step Response）**|
|[h,w] = freqz(b, a, n)|计算**频率响应（Frequency Response）**|
其中：
- b 是分子系数（对应输入信号 x[n]）
- a 是分母系数（对应输出信号 y[n]）
- n 是你想要的输出样本点数
**例子：**
![image16 2|image16 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image16%202.png)
![image17 2|image17 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image17%202.png)
![image18 2|image18 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image18%202.png)
![image19 2|image19 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image19%202.png)
![image20 2|image20 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image20%202.png)
## **4.4 滤波器的分类**
### **4.4.1 介绍**
滤波器的四种类型：
- **低通滤波器（Low-pass filters）**：只允许低频通过，阻止高频。
- **高通滤波器（High-pass filters）**：只允许高频通过，阻止低频。
- **带通滤波器（Band-pass filters**）：只允许某一频带的频率通过，阻止其他频率。
- **带阻滤波器（Band-stop filters）**：阻止某一频带的频率，其他频率正常通过。
### **4.4.2 低通滤波器**
它的作用是：**衰减（attenuate）高频成分，同时允许低频成分通过。**常用于：去除信号中的噪声或不需要的高频成分。
它包含两个频带：
- **通带（passband）：**低频部分，信号可以顺利通过。
- **阻带（stopband）：**高频部分，信号被削弱或阻止。
- 中间有一个**过渡带（transition band）**，如右上角图所示，过渡带是从通带逐渐过渡到阻带的区域。
![image21 2|image21 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image21%202.png)
### **4.4.3 高通滤波器**
它的作用是：**衰减低频成分（attenuate low-frequency components）**，同时允许**高频成分通过（high-frequency components to pass through）**。也就是说，它跟低通滤波器正好相反。常用于：移除直流偏移（DC offset）或不需要的低频信号。
其典型幅度响应：
- **阻带（stopband）：** 低频部分，信号被削弱。
- **通带（passband）：** 高频部分，信号得以保留。
- 中间有一个过渡带（transition band）。
![image22 2|image22 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image22%202.png)
### **4.4.4 带通滤波器**
它的作用是：让一个**特定频率范围内**的信号通过，同时**抑制（attenuate）该范围之外**的频率成分。常用于：**从信号中提取某个特定频率范围**，或者**去除不需要的频率成分**。
其典型幅度响应：
- 一个 **通带（passband）**：中间那一小段允许通过的频率范围；
- 两侧有两个 **阻带（stopbands）**：低频和高频两边的信号被抑制；
- 中间的频率范围（例如 [f₁, f₂]）是保留目标。
![image23 2|image23 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image23%202.png)
### **4.4.5 带阻滤波器**
它的作用是：**抑制某一段频率范围的信号**，同时允许其他频率通过。是带通滤波器的“反向版本”。常用于：移除特定频率的干扰信号。
其典型幅度响应：
- **中间一段（stopband）**是被抑制的频率范围；
- **两边的通带（passbands）**允许低频和高频通过；
![image24 2|image24 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image24%202.png)
### **4.4.6 滤波器之间的互相转换**
### **1 低通到高通**
![image25 2|image25 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image25%202.png)
![image26 2|image26 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image26%202.png)
### **2 低通到带通**
![image27 2|image27 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image27%202.png)
![image28 2|image28 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image28%202.png)
### **3 低通到带阻**
![image29 2|image29 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image29%202.png)
![image30 2|image30 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image30%202.png)
### **4.4.7 实例**
![image31 2|image31 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image31%202.png)
![image32 2|image32 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image32%202.png)
![image33 2|image33 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image33%202.png)
![image34 2|image34 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image34%202.png)
![image35 2|image35 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image35%202.png)
![image36 2|image36 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image36%202.png)
![image37 2|image37 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image37%202.png)
## **4.5 有限冲激响应滤波器 Finite Impulse Response (FIR) Filters**
### **4.5.1 介绍**
FIR（Finite Impulse Response）滤波器是一类**冲激响应是有限长度**的滤波器。其差分方程**不包含过去的输出项**（如 y[n−1],y[n−2] 等）。
**通常表示为：**
![image38 2|image38 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image38%202.png)
**其传输函数为：**
![image39 2|image39 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image39%202.png)
**其脉冲响应为：**
![image40 2|image40 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image40%202.png)
FIR有四个**主要特性：**
- 滤波器的输出**不依赖于过去的输出**；
- 所有极点都在原点，因此 FIR **天然稳定**；
- 冲激响应是有限序列，因此可以通过**卷积**来实现滤波器。
- FIR 通常可以实现**线性相位**。
**一个典型的FIR滤波器：**
![image41 2|image41 2.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image41%202.png)
### **4.5.2 设计一个FIR滤波器**