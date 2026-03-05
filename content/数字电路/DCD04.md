[DCD 04 LatchesAndFlipFlops](https://www.beyondpluto.cn/?p=646)
## **1 时序电路（Sequential circuits）**
### **1.1 介绍**
时序电路是一种由两部分组成的电路：
- **组合逻辑电路** combinational circuits（用逻辑门实现）
- **存储元件** memory.（如锁存器、触发器）
![image1 10|image1 10.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image1%2010.png)
### **1.2 同步 vs 异步时序系统**
**同步系统（Synchronous）**：所有操作都基于时钟信号的节拍，在特定时间点发生状态改变。
**异步系统（Asynchronous）**：电路状态随时可能因输入变化而改变，容易出错。
### **1.3 状态（State）**
**状态**：电路的状态或特征由其**输出的数值**来描述。
- 举例来说：如果一个电路有 **N 个输出**，每个输出都是二进制（0或1），那么这个电路就有 **2ⁿ 种可能的状态**。
- 状态可以是：
    - **稳定状态（Stable）**：输出保持不变；
    - **亚稳态（Metastable）**：输出处于一个不确定、可能会随机变化的状态。
对于一个**时序电路**，只要知道它的 **当前状态（current state）** 和 **当前输入（input）**，就可以**预测出下一个状态（next state）**。
**时序电路**也被称为 **有限状态机（FSM, Finite State Machines）**
### **1.4 时钟信号**
**大多数时序电路** 都是通过一个**时钟信号（clock signal）** 来驱动状态的变化（state change）
时钟信号可以是：
- **高电平有效（active high）**
- **低电平有效（active low）**
它可能的状态包括：
- **高电平（high）**
- **低电平（low）**
- **上升沿（rising edge）**
- **下降沿（falling edge）**
常见的参数包括：
- **周期（period）**：同一方向的两个边沿之间的时间间隔（如连续两个上升沿之间的时间）；
- **频率（frequency）**：单位时间内时钟周期的次数；
- **占空比（duty cycle）**：高电平持续时间与整个周期的比例。
![image2 9|image2 9.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image2%209.png)
![image3 9|image3 9.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image3%209.png)
### **1.5 门延迟与时间图（Gate Delays and Time Diagrams）**
在信号通过一个门时，通常会存在**门延迟（Propagation Delay）**
![image4 9|image4 9.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image4%209.png)
### **1.6 振荡电路：不稳定状态（Oscillating Circuit: Not Stable）**
![image5 8|image5 8.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image5%208.png)
电路不停地“自我反转”，变成一个**振荡器。电路永远无法稳定**
### **1.7 反馈回路（Feedback Loop）**
![image6 8|image6 8.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image6%208.png)
**最简单的双稳态反馈电路**
## **2 双稳态元件 Bistable Elements**
### **2.1 介绍**
**Bistable Element** 是最简单的时序电路。由两个**反相器（inverter）**组成；
**没有输入，只有两个输出**；**状态（state）**由两个输出值共同决定；
只存在 **两个稳定状态**：
- (1,0) 或
- (0,1)；
输出仅取决于**上一个输入状态（previous input）**，通过**反馈回路**维持状态。
![image7 8|image7 8.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image7%208.png)
图中两路交叉连接的反相器构成了一个环形反馈回路。例如：
此时输出 Q = 1，Q_L = 0。若 Vin1 = LOW → Vout1 = HIGH，这反过来又影响 Vin2 变高 → Vout2 = LOW；此时输出 Q = 1，Q_L = 0。
如图：
![image8 7|image8 7.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image8%207.png)
看两个反相器的交叉点，表现出**三种状态：**
- **Stable High**（稳定高电平）；
- **Stable Low**（稳定低电平）；
- **Metastable**（亚稳态）——输出卡在“不上不下”的临界状态中。
如果系统处在这个亚稳区，而没有外部干扰，它可能**长时间停留在不稳定状态**。
### **2.2 Metastability & Stable States（亚稳态与稳定状态）**
![image9 7|image9 7.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image9%207.png)
一个双稳态系统实际上有**三个状态**，第三种状态是**亚稳态（Metastable）**是一种**非稳定状态**，输出处于0与1之间，电路短时间内无法做出明确判断。主要原因是**异步信号**没有在触发器规定的**建立时间（setup time）和保持时间（hold time）**范围内到达；
- 当输入信号 **在0和1之间**时，两个反相器会陷入一种**无法确定是0还是1的中间状态**。
- 在这时，输出电压可能卡在阈值附近，既不像“0”也不像“1”——这是一个**非法状态（Not a valid state）**。
- 如果没有外界干扰（例如噪声、扰动），它甚至可能**无限期停留在这个不稳定状态中**。
如图：
![image10 6|image10 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image10%206.png)
中间山顶是**亚稳态**，就像小球刚好处在山顶的**临界点**，非常容易左右滑落。一旦外界有一点干扰，小球就会掉向其中一个谷底，也就是**最终进入一个稳定态**。
高速系统中的危险性大。高速系统中时钟周期非常短，如果亚稳态持续的时间（称为**metastability resolution time**）**超过了一个时钟周期**，就可能会导致导致：数据丢失，状态错误，整个系统运行异常等。
## **3 锁存器 Latches**
### **3.1 介绍**
**Latch（锁存器）**：是一种最基本的存储元件，**所有的触发器（flip-flops）都是由它构建而来的**。
锁存器**本身不能直接用于同步系统**，因为锁存器（特别是 **SR Latch** 和 **D Latch**）虽然可以存储状态，但它们缺乏**时钟控制机制**。也就是说，它们无法确保数据在特定的“时钟时刻”写入或更新。在复杂的同步电路中，这会导致状态更新“时机不统一”，从而产生**竞态条件（racing）或数据不一致**的问题。
比如：**SR Latch** 和 **D Latch** 是**电平敏感型（level sensitive）**，只要控制信号（如使能信号）为高电平，它就持续响应输入。而同步系统需要的是**边沿触发型（edge-triggered）**，只能在时钟“边沿”（如上升沿或下降沿）触发一次状态更新。
### **3.2 置位-复位锁存器 Set Reset (SR) Latch**
**SR锁存器** 是最基础的一种锁存器，用于“设置”（Set）和“复位”（Reset）存储单元的状态。
![image11 6|image11 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image11%206.png)
输入 S = 1：→ **Q 被置为 1（Set）**，输入 R = 1：→ **Q 被清为 0（Reset）**，而合法状态下，Q 和 QN 始终是**互补**的。而S和R都为零时则会**保持上次输入状态**。
当 **S = R = 1**时：
两个输入都为 1，两个 **NOR 门的输出都变成 0**，输出进入一个**未定义状态（undefined state）**。这就违反了 SR 锁存器最基本的规则：**Q 和 Q′ 应当互为反相（complement）**。
当 S 和 R 从 1 同时返回 0，会发生**振荡（Oscillation）**。两个 NOR 门会由于反馈回路产生**持续的相互干扰**，这种状态称为**振荡状态（oscillating condition）**，**电路无法稳定**。
![image12 5|image12 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image12%205.png)
使用 “恢复时间（recovery time）” 概念可以避免该问题。
### **3.3 NAND 门实现的 SR 锁存器（SR Latch）**
![image13 4|image13 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image13%204.png)
这里的两个门都可以换成**NAND门**，它和用 NOR 门构建的版本原理类似，但**逻辑电平相反**。
### **3.4 有控制输入（Control Input）的SR 锁存器（SR Latch）SR Latch with Control Input**
![image14 4|image14 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image14%204.png)
即控制输入为1时输入才有效。
### **3.5 D 锁存器 D Latch**
![image15 4|image15 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image15%204.png)
**只有两个输入**：
- D（Data，数据输入）
- C（Control，控制输入）
D 输入**直接连接 Set 输入**，D 的**反相信号连接 Reset 输入**，这样一来，**永远不会同时出现 Set = 1 和 Reset = 1**。因此，**不再存在不确定状态（indeterminate state）**。
|**项目**|**SR Latch**|**D Latch**|
|---|---|---|
|输入数量|2（S 和 R）|2（D 和 C）|
|风险点|S = R = 1 会出错|设计确保永远不会出现非法输入|
|状态确定性|存在不确定状态|始终确定（只有 0 或 1）|
|实用性|结构简单但不安全|更安全、更常用于实际同步逻辑系统中|
输入与输出的图示：
![image16 4|image16 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image16%204.png)
C 由高变低（**下降沿 falling edge**）时间点的附近，**D 输入必须保持稳定**，不能跳变，否则可能导致 Q 输出进入**亚稳态（metastability）** 或产生不确定状态。
## **4 触发器 Flip-Flops**
### **4.1 介绍**
|**项目**|**Latch（锁存器）**|**Flip-Flop（触发器）**|
|---|---|---|
|控制方式|电平敏感（Level-sensitive）|边沿触发（Edge-triggered）|
|同步支持|不支持同步时钟控制|完全支持同步系统|
|适合的应用|简单存储或异步控制系统|时序逻辑电路、寄存器、FSM 等|
因为锁存器输出可能一直随输入变化，会导致电路不稳定，比如当使能信号为高电平时，输入 D 改变就会立即影响输出 Q；同时竞态条件（Race conditions）可能出现，即当多个信号在同一时间变化，会出现不确定、不可预测的状态，所以锁存器不够用。
为了构建**可靠的同步数字系统**，必须使用更稳定、时钟控制更好的器件，即**触发器**。
### **4.2 主从触发器 Master-Slave Flip-Flops**
**使用两个锁存器（Latches）**：一个主（Master），一个从（Slave），它们通过**时钟信号反向控制**，保证它们**不会同时开启**。主锁存器在 **时钟高电平** 时采样输入，从锁存器在 **时钟低电平** 时锁存主锁存器的输出。通过这种串联与时序配合，使输入与输出解耦，达到**边沿触发的效果**。
其中时钟信号（Clock）是核心控制信号，接入两个锁存器的控制端，但：
- **主锁存器**用 **直接接入的 C**；
- **从锁存器**用 **反相后的 C̅（NOT C）**。
这样可以确保：
- 当 **C = 1**，主锁存器工作，从锁存器关闭；
- 当 **C = 0**，主锁存器关闭，从锁存器工作。
这就是为什么叫 “Master-Slave” —— 两个锁存器轮流接管数据控制，**始终只有一个在工作**，输出稳定不抖动。
### **4.3 主从 D 触发器 Master-Slave D Flip-Flop**
使用 **两个 D 锁存器（2 D Latches）** 组成，Master D Latch：采集数据 D；Slave D Latch：延迟一周期输出 Q。**使用窄脉冲时钟（narrow pulse clocking）机制**。
![image17 4|image17 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image17%204.png)
![image18 4|image18 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image18%204.png)
### **4.4 JK 主从触发器 JK Master-Slave Flip-Flop**
它通过加入 **反馈和逻辑门（如 AND 门）**，解决了 SR 触发器在 S=1 和 R=1 时的**不确定状态（indeterminate state）**问题
![image19 4|image19 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image19%204.png)
工作逻辑：
- 当 **J = 0, K = 0**：触发器保持当前状态（无变化）；
- 当 **J = 1, K = 0**：类似于 Set 操作：Q = 1，Q̅ = 0；
- 当 **J = 0, K = 1**：类似于 Reset 操作：Q = 0，Q̅ = 1；
- 当 **J = 1, K = 1**：它将输出**反转（Toggle）**,即1变0，0变1。
如果 **JK 触发器的输入 J = K = 1** 一直保持，**Q 会在每一个时钟“下降沿”翻转一次（Toggle）**。
**问题：1’s catching 和 0’s catching**
![image20 4|image20 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image20%204.png)
（待施工）
### **4.5 边沿触发触发器 Edge-triggered flip-flops**
**Edge-triggered flip-flops** 是只在 **时钟信号的边沿（transition）** 发生时才响应输入变化的触发器。
无论时钟是高电平还是低电平期间，**输入 D 都会被忽略**；唯有在 **时钟边沿（上升或下降）** 的瞬间，才会采样输入、更新输出。这就避免了主锁存器那种电平敏感导致的不稳定采样。
**两种边沿类型：**
|**类型**|**含义**|**触发时刻**|
|---|---|---|
|Positive edge|时钟从 0 → 1 的跳变（上升沿）|↑（上升沿）|
|Negative edge|时钟从 1 → 0 的跳变（下降沿）|↓（下降沿）|
**例子：上升沿触发D Flip-Flop**
![image21 4|image21 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image21%204.png)
D Flip-Flop 的关键时序参数：
![image22 4|image22 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image22%204.png)
同样，**下降沿触发D Flip-Flop**如下：
![image23 4|image23 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image23%204.png)
Edge Triggered JK Flip-Flop：
![image24 4|image24 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image24%204.png)
### **4.6 T Flip-Flop**
**T 触发器**是一种会在每次时钟有效边沿“翻转”输出状态的触发器。
工作逻辑（功能表）
|**输入 T**|**触发行为**|**输出 Q（下一状态）**|
|---|---|---|
|0|保持|Q_next = Q|
|1|**翻转（toggle）**|Q_next = Q̅|
![image25 4|image25 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image25%204.png)
### **4.7 T Flip-Flop with Enable：带使能的 T 触发器**
在很多应用中，我们不希望 **每次时钟跳变都进行翻转**，所以引入 **使能信号 EN（Enable）**，控制 T 是否生效。
只有当 EN = 1 且 T = 1 时，Q 才在时钟边沿翻转，若 EN 为 0，即使 T=1 也不触发任何变化。
|**EN**|**T**|**时钟边沿时 Q 行为**|
|---|---|---|
|1|1|翻转 Q（Toggle）|
|1|0|保持 Q 不变|
|0|x|保持 Q 不变（忽略 T）|
### **4.8 把其他触发器转换成 T Flip-Flop**
![image26 4|image26 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image26%204.png)
（待施工）
### **4.9 触发器（Flip-Flops）在数字系统中的两大典型应用**
**应用 1：并行数据存储（Parallel Data Storage）**
![image27 4|image27 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image27%204.png)
**应用 2：数字计数器（Digital Counters）**
![image28 4|image28 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image28%204.png)