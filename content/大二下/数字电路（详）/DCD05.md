[DCD 05 时序逻辑电路的分析方法](https://www.beyondpluto.cn/?p=679)
## **1 基本概念**
### **1.1 分析和综合的区别**
- **分析（Analysis）**：已有电路，分析其行为、状态转换与输出。
- **综合（Synthesis）**：目标功能已知，设计一个能实现该功能的电路。
### **1.2 时序电路的组成部分 Behavior of sequential circuits:**
![image1 11|image1 11.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image1%2011.png)
**下一状态逻辑（Next-State Logic）**：是**组合逻辑电路**，将**输入信号和当前状态**作为输入，生成“激励”信号（即下一状态的输入）。表达式形式称为：**输入方程（Input Equation）**或**激励方程（Excitation Equation）**。
**状态存储器（State Memory）**：通常由触发器构成，存储当前状态。一般使用**n个触发器（flip-flops）构建一个n位状态寄存器（n-bit state register）**。
![image2 10|image2 10.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image2%2010.png)
每个触发器有两种状态（0 或 1），n 个触发器能组合出： 2n  种不同状态
**输出逻辑（Output Logic）**：决定整个电路在某一状态下的输出。有两种类型：
- **Moore型**：输出仅由当前状态决定。
![image3 10|image3 10.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image3%2010.png)
- **Mealy型**：输出由当前状态和输入共同决定。
![image4 10|image4 10.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image4%2010.png)
## **2 触发器（Flip-Flop）和锁存器（Latch）的特性方程（Characteristic Equations）**
**特性方程**描述的是**触发器/锁存器的功能行为**，即：
- **给定当前状态和控制输入，决定下一时刻的输出（Q*）**
- 不关注时序细节（如建立时间、保持时间等），只描述功能逻辑
**Q*** 表示 “**下一个 Q 的值**”（下一时钟周期的输出），方程形式：Q* = f(Q, 输入)，它告诉我们：**控制输入改变时，Q 的变化规律**
常见的**特性方程**：
![image5 9|image5 9.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image5%209.png)
|**触发器类型**|**特性方程**|**功能简述**|
|---|---|---|
|S-R 锁存器|Q* = S + R′Q|设置、清除、保持|
|D 触发器|Q* = D|数据传输|
|JK 触发器|Q* = JQ′ + K′Q|通用状态控制|
|T 触发器|Q* = Q′|翻转|
|D 启用触发器|Q* = END + EN′Q|控制性的数据存储|
|T 启用触发器|Q* = ENQ′ + EN′Q|控制性翻转|
**注释**：
- **EN**：使能信号（Enable）
- **MS**：主从型（Master-Slave）
- **ET**：边沿触发（Edge-Triggered）
## **3 分析时序电路的流程**
1. **获得激励方程（Excitation/Input Equations）**：如 D = AX + BX。
2. **获得输出方程（Output Equations）**：如 Y = (A + B)X’。
3. **获得下一状态方程（Characteristic Equations）**：如 Q* = D。
4. **代入激励方程得出状态转移方程（Transition Equations）**。
5. **绘制转移表（Transition Table）**：当前状态 + 输入 → 下一状态。
6. **绘制状态表（State Table）**：用字母代替状态名，如 A=00, B=01 等。
7. **绘制状态/输出表（State/Output Table）**：加入输出信息。
8. **绘制状态图（State Diagram）**：用有向图表示状态之间的跳转与输出。
![image6 9|image6 9.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image6%209.png)
## **4 同步时序状态机**
### **4.1 介绍**
通常由四个部分组成：
**① Current State（当前状态）**
- 表示当前时刻（时间点 **t**）**触发器的状态**。
- 这些状态通常用**二进制（如 A=0, B=1）**或**字母代号（如 M, N, O）**表示。
- 这是状态转移和输出的起点。
**② Input（输入）**
- 指每种状态下电路接收到的**外部输入值**。
- 输入与当前状态共同决定**下一状态（Next State）**。
- 例：输入变量可能是 X、Y、Z 等。
**③ Next State（下一状态）**
- 指一个时钟周期之后（即时间点 **t+1**）电路将进入的新状态。
- 是由**输入 + 当前状态**经过组合逻辑和触发器的作用得到的。
- 对应公式： Next State=F(Current State,Input)
**④ Output（输出）**
- 表示系统当前状态下的输出值。
- 输出可以只依赖当前状态（Moore 机），或还依赖输入（Mealy 机）：
    - **Moore**：Output = G(Current State)
    - **Mealy**：Output = G(Current State, Input)
**同步时序状态机（CSSMs）中的三类重要表格**，分别是：
### **4.2 状态转移表（Transition Table）**
- 描述“当前状态 + 输入”与“下一状态”之间的映射关系。
- 用二进制代码（如A、B）表示状态。
- 常用于从方程推导逻辑行为。
![image7 9|image7 9.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image7%209.png)
### **4.3 状态表（State Table）**
与状态转移表类似，但将状态用**字母/符号代号（如 A、B、C、D）**表示，更易理解和人类阅读。
![image8 8|image8 8.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image8%208.png)
### **4.4 状态/输出表（State/Output Table）**
- 在状态表基础上，**额外加入输出**，形成“状态 + 输入” → “下一状态 + 输出”。
- 对于 **Mealy 状态机**：输出依赖状态和输入。
- 对于 **Moore 状态机**：输出只依赖当前状态。
![image9 8|image9 8.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image9%208.png)
### **4.5 编写表格时必须注意的几点**
1. 正确标注你的表格（Correctly label your tables）,**必须为你的表格列清晰的标题**（如“Current State”、“Next State”等）
2. 为你的**字母状态（Alphanumeric States）**提供对照表
## **5 实例：使用 D 触发器构建的状态机**
### **5.1 电路组成分析**
![image10 7|image10 7.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image10%207.png)
|**区域**|**作用**|**在图中的位置说明**|
|---|---|---|
|左上红框|**下一状态逻辑**（Next-State Logic）|多个逻辑门用于生成 D 触发器输入（激励）|
|右上红框|**状态存储器**（State Memory）|两个 D 触发器 A 和 B 存储状态（输出为 A′、B′）|
|底部红框|**输出逻辑**（Output Logic）|由状态 A′、B′ 和输入 X 决定输出 Y|
同时，该电路是**Mealy 状态机**，特点：输出不仅取决于当前状态，也取决于当前输入。
### **5.2 状态方程推导**
**激励方程（Excitation Equations）和输出方程（Output Equation）：**
![image11 7|image11 7.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image11%207.png)
**下一状态方程（Characteristic Equations）**：
![image12 6|image12 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image12%206.png)
由这些我们可以推导出**状态转移方程（Transition Equations）**：
![image13 5|image13 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image13%205.png)
### **5.3 绘制TransitionTable，State Table，State/Output Table**
**Transition Table，State Table**可以通过**状态转移方程（Transition Equations）**计算，**如下：**
![image14 5|image14 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image14%205.png)
![image15 5|image15 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image15%205.png)
而**State/Output Table**的输出可以由**输出方程（Output Equations）**计算
![image16 5|image16 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image16%205.png)
### **5.4 从状态输出表到状态图**
### **状态图的开发流程如下（如图所示）：**
1. **从状态/输出表中提取状态转移信息**
2. 用**圆圈表示当前状态（Present States）**
3. 用**箭头（有向边）表示状态之间的转移**
4. 每条边上标注**输入/输出（X/Y）**
![image17 5|image17 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image17%205.png)
表格字段含义为：
|**当前状态 S**|**输入 X=0 → 下一状态,输出**|**输入 X=1 → 下一状态,输出**|
|---|---|---|
|M (00)|M,0|O,0|
|N (01)|M,1|N,0|
|O (10)|M,1|P,0|
|P (11)|M,1|N,0|
## **6 JK 触发器分析状态机**
和D触发器流程一样，但是现在我们要分析含有 **两个输入（J 和 K）的 JK 触发器**电路，就需要使用更复杂的**特性方程（Characteristic Equation）**来计算下一状态。
![image18 5|image18 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image18%205.png)
![image19 5|image19 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image19%205.png)
![image20 5|image20 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image20%205.png)
![image21 5|image21 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image21%205.png)
![image22 5|image22 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image22%205.png)
![image23 5|image23 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image23%205.png)
## **7 状态机的时间延迟与最大时钟频率**
- **门延迟（Gate Delay）限制了状态机的运行速度**：每个逻辑门都会有一定的传播延迟（propagation delay）。
- **反馈路径的逻辑延迟决定了最大时钟频率（Fₘₐₓ）**：因为状态的反馈必须在一个时钟周期内“稳定”并被锁存。
**最大时钟频率公式**：
![image24 5|image24 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image24%205.png)
- TD：是电路中最长路径的总逻辑延迟（critical path delay）
- 如果时钟频率 **超过 Fₘₐₓ**，电路将变得**不稳定**
具体示例如下：
![image25 5|image25 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image25%205.png)
![image26 5|image26 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image26%205.png)