[DCD 07 数字电路模块](https://www.beyondpluto.cn/?p=740)
[Digital System Blocks](https://www.beyondpluto.cn/?p=740)
## **1 总线（Buses）**
- **总线**是由两个或多个导体组成的集合，用来表示一个二进制数（如 1101）。
- 总线通常用于在不同逻辑设备之间传输多个位的数据。
- 常见的总线宽度包括 **4位总线** 和 **8位总线**。
- 总线连接不一定是一对一的，可能被多个元件共享，实现复杂的通信结构。
![image1 13|image1 13.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image1%2013.png)
## **2 选择器和多路选择器（Selectors / Multiplexers, MUX）**
**选择器**或**多路复用器**用于从多个输入中选择一个输出。
**2路选择器**有两个输入，一个选择信号，输出为对应选择的输入。
![image2 12|image2 12.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image2%2012.png)
**4路选择器**有四个输入，两个选择信号，对应如下真值表：
![image3 12|image3 12.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image3%2012.png)
![image4 12|image4 12.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image4%2012.png)
![image5 11|image5 11.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image5%2011.png)
![image6 11|image6 11.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image6%2011.png)
## **3 解码器与数据分配器（Decoder / Demultiplexer）**
**解码器**将n位的输入转换为 2n2^n2n 条输出线中仅一条为高电平，其余为低电平。
示例：2位输入可以选择4个输出中的一个：
![image7 11|image7 11.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image7%2011.png)
## **4 大小比较器 （Magnitude Comparator）**
基本比较器使用 **XNOR** 门来判断两个输入是否相等。
![image8 10|image8 10.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image8%2010.png)
多位比较器会将每个位的比较结果（XNOR）通过 **与门（AND）** 相连接，实现整体判断。
![image9 10|image9 10.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image9%2010.png)
## **5 半加器（Half Adder）**
半加器是一个组合逻辑电路，**输入两个二进制位（X 和 Y）**，产生两个输出：
- **Sum（和，S）**
- **Carry（进位，C）**
数学含义：
![image10 9|image10 9.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image10%209.png)
真值表：
![image11 9|image11 9.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image11%209.png)
输出逻辑表达式：
![image12 8|image12 8.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image12%208.png)
半加器的三种示例：
![image13 7|image13 7.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image13%207.png)
**用NAND门实现如下：**
![image14 7|image14 7.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image14%207.png)
- **Sum（和 S）**：路径最深，需要 **3 个逻辑门延迟**；
- **Carry（进位 C）**：只需要 **2 个逻辑门延迟**；
    - 如果需要的是 **Carry’（进位的反）**，只需要 **1 个逻辑门延迟**。
**门延迟（Gate Delay）可能导致**错误脉冲（Spurious Pulse）
![image15 7|image15 7.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image15%207.png)
## **6 全加器（Full Adder）**
**全加器**是数字电路中用于执行三位二进制加法的组合逻辑单元。输入包括：
- X：第一位二进制输入
- Y：第二位二进制输入
- Cin（Carry-in）：来自前一位的进位
输出包括：
- S（Sum）：本位的和
- Cout（Carry-out）：进位输出，传到下一位
**逻辑表达式：**
![image16 7|image16 7.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image16%207.png)
**真值表：**
![image16 7|image16 7.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image16%207.png)
![image17 6|image17 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image17%206.png)
**组合逻辑结构：**
可由两个半加器 + 一个或门构成：
- 第一个半加器：计算 X + Y → 得中间和、进位
- 第二个半加器：加上 Cin
- 最终进位由三个进位项“或”起来
![image18 6|image18 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image18%206.png)
**用NAND门实现：**
![image19 6|image19 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image19%206.png)
## **7 4位并行加法器（4-bit Parallel Adder）**
**输入与输出标记：**
- N1(3:0)：第一组加数的4位（从低位 N1(0) 到高位 N1(3)）
- N2(3:0)：第二组加数的4位
- Cin：最右侧最开始的进位输入（通常为0）
- SUM(3:0)：输出结果（从低位 SUM(0) 到高位 SUM(3)）
- Cout：最终进位输出
**构造方式：**
四个 fa 块就是四个 **全加器模块**，每个全加器执行：
![image20 6|image20 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image20%206.png)
**关键点：**
- 每一级的进位输出（Cout）成为下一位的进位输入（Cin）；
- 所有加法操作“并行结构连接”，所以称为“并行加法器”。
![image21 6|image21 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image21%206.png)
![image22 6|image22 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image22%206.png)
## **8 4位串行减法器（4-bit Ripple Subtractor）**
通过**加法器（Full Adder）+ 补码技巧**实现。
![image23 6|image23 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image23%206.png)
原理为：
![image24 6|image24 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image24%206.png)
这就是**二进制补码减法的原理**。它的含义是：
- **对B取反（按位非）**，即 B‾\overline{B}B
- **加上1**，即形成 **B的补码**
- **再加上A**
## **9 4位加/减法器（4-bit Adder/Subtractor）**
**具有一个控制输入（CONTROL）**，用来决定执行的是加法还是减法。
![image25 6|image25 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image25%206.png)
![image26 6|image26 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image26%206.png)
## **10 算术单元（Arithmetic Unit）**
它不仅可以执行加法和减法，还支持：
- **自增（A + 1）**
- **自减（A – 1）**
模块图所示的**Arithmetic**单元具有以下接口：
- **输入 A 和 B：** 各为 4 位
- **控制信号 Control（2位）**：决定执行哪种运算
- **Cin/Bin**：作为进位或借位输入
- **输出：**
    - Output[3:0]：结果
    - Cout/Bout：进位或借位输出
![image27 5|image27 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image27%205.png)