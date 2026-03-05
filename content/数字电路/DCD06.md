[DCD 06 自主时序电路](https://www.beyondpluto.cn/?p=718)
[Autonomous Sequential Circuit](https://www.beyondpluto.cn/?p=718)
## **1 定义**
自主时序电路（Autonomous Sequential Circuit）是没有**主输入（primary inputs）的时序电路，它们只有次级输入（secondaries）**，这些输入来自于**时钟信号**和**触发器（flip-flops）**的反馈。
- 次级输入由组合逻辑构成，其输入来源于触发器的输出，再反馈回触发器的输入。
- 有时也包括输出逻辑。
## **2 通用设计方法**
设计自主时序电路一般遵循四个步骤：
1. **绘制状态表**：列出当前状态和下一状态，要结合使用触发器的特性方程（例如 D、JK、T 触发器的方程）。
2. **绘制卡诺图（Karnaugh Map）**：为每个触发器输入（即每个下一状态）绘制逻辑表达式的化简图。
3. **简化逻辑表达式**：使用卡诺图技巧对表达式进行化简。
4. **绘制电路图**：将化简后的逻辑表达式转换为实际的逻辑门和触发器电路。
## **3 示例一：D 型触发器**
**题目：**Design an autonomous sequential circuit using D-type flip-flops to generate the following sequence of states: 001, 100, 010,101, 110, 111, 011.
**Step 1：绘制当前状态和下一状态表** **注意：D inputs = Nest State**
![image1 12|image1 12.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image1%2012.png)
**Step 2：为每个触发器的输入绘制卡诺图**
为每一个flip-flop的**输入**，也就是每一个**D input**画一个卡诺图，如下所示
![image2 11|image2 11.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image2%2011.png)
![image3 11|image3 11.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image3%2011.png)
**Step 3：绘制电路图（FSM）**
![image4 11|image4 11.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image4%2011.png)
## **4 示例二：JK 型触发器（三位二进制计数器）**
**Step 1：绘制当前状态和下一状态表**
- 要列出电路的每个状态，比如状态 000, 001, 010, …, 并明确每个状态在时钟信号作用下会跳转到哪个“下一状态”。
- 由于你使用的是 JK 触发器，因此不能直接把“下一状态”当作输入，而是要根据 **JK触发器的激励表（excitation table）** 来确定各个输入 J 和 K 的取值。
- JK触发器的激励规则如下：
|**当前状态(Q)**|**下一状态(Q*)**|**J**|**K**|
|---|---|---|---|
|0|0|0|X|
|0|1|1|X|
|1|0|X|1|
|1|1|X|0|
所以你需要根据 Q 和 Q* 推导出每个触发器对应的 J 和 K。
![image5 10|image5 10.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image5%2010.png)
**Step 2：为每个触发器的输入绘制卡诺图**
- 你对每个 **J 和 K 输入** 绘制一个卡诺图（K-map），变量是“当前状态”的比特位，比如 Q2、Q1、Q0。
- 一共需要画 **6 个卡诺图（3个触发器 × 每个触发器2个输入 J/K）**。
- 这些卡诺图会帮助你直观地观察并合并逻辑表达式中为1的位置。
![image6 10|image6 10.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image6%2010.png)
![image7 10|image7 10.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image7%2010.png)
![image8 9|image8 9.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image8%209.png)
**Step 3：绘制电路图（FSM）**
- 根据简化后的 J 和 K 输入表达式，为每个触发器搭建其控制逻辑。
- 最终你将得到一个包含三个 JK 触发器和一组组合逻辑门的完整状态机电路图。
## **5 “Cannot Happen” 状态**
在某些有限状态机（FSM）设计中，为了简化逻辑，我们会
- 将“不能发生”的状态（在正常设计中不会进入的状态）视为“don’t care”；
- 在卡诺图（K-map）中用这些状态位置上的“X”来合并更多的“1”，以减少逻辑门的数量；
- 这虽然优化了硬件资源，但**也等于人为地为这些“非法状态”指定了“下一状态”**，即——**“强制”它们跳转到某些位置。**
![image9 9|image9 9.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image9%209.png)
图中的表格解释了两种原本**不应该出现的状态**在你的状态机中被“强制赋予”的下一状态
### **状态解读：**
- **状态6（110）→ 状态7（111）**
- **状态7（111）→ 状态0（000）**
这说明即使系统意外进入了状态6或7，也会被“引导”回合法状态路径中，不会卡死或循环在非法状态里。
所以完整的state diagram是：
![image10 8|image10 8.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image10%208.png)
## **6 示例三：T flip-flop**
![image11 8|image11 8.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image11%208.png)
![image12 7|image12 7.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image12%207.png)
![image13 6|image13 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image13%206.png)
![image14 6|image14 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image14%206.png)
![image15 6|image15 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image15%206.png)
![image16 6|image16 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image16%206.png)