[DCD 02](https://www.beyondpluto.cn/?p=508)
[Basic Logic Functions and Switching Algebra](https://www.beyondpluto.cn/?p=508)
## **1 基本门**
### **1.1 基本门：AND**
![image1 8|image1 8.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image1%208.png)
### **1.2 基本门：OR**
![image2 7|image2 7.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image2%207.png)
### **1.3 基本门：NOT**
![image3 7|image3 7.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image3%207.png)
## **2 其他门**
### **2.1 其他门：Buffer**
![image4 7|image4 7.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image4%207.png)
### **2.2 其他门：NAND**
![image5 6|image5 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image5%206.png)
### **2.3 其他门：NOR**
![image6 6|image6 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image6%206.png)
### **2.4 其他门：XOR**
![image7 6|image7 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image7%206.png)
### **2.5 其他门：XNOR**
![image8 6|image8 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image8%206.png)
## **3 基本定义 Basic Definitions**
![image9 6|image9 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image9%206.png)
**运算优先级规则**
- 取反（’）＞ 与（·）＞ 或（+）
## **4 定理**
### **4.1 基本定理**
让 **X** 成为逻辑变量，取值 0 或 1
![image10 5|image10 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image10%205.png)
### **4.2 单变量定理**
![image11 5|image11 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image11%205.png)
### **4.3 完备归纳（Perfect Induction）**
其实就是枚举法（）
### **4.4 二/三变量定理**
![image12 4|image12 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image12%204.png)
![image13 3|image13 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image13%203.png)
**反演律：**
![image14 3|image14 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image14%203.png)
长逆变短逆，与变或，或变与
**吸附定理**：
![image15 3|image15 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image15%203.png)
- **定理(T8)** 可用于将一个“积的和”（Product of Sums, POS）表达式转换成“和的积”（Sum of Products, SOP）表达式。
- **定理(T8′)** 则常用于将“SOP”表达式转换回“POS”形式。
- **定理(T9)、(T10) 和 (T11)** 经常用来 **最小化** 或 **简化** 逻辑电路。这些定理的**共同特点**是在化简过程中，从左到右电路所需的逻辑门／布尔运算次数会逐步减少。
### **4.5 N变量定理**
**1.广义幂等律（Generalised Idempotency）**
![image16 3|image16 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image16%203.png)
**2.德摩根定理（De Morgan’s Theorems）**
![image17 3|image17 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image17%203.png)
德摩根定律可用于积的和与和的积之间的转换。
**3.广义德摩根定理（Generalised De Morgan’s Theorem）**
![image18 3|image18 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image18%203.png)
（相当于对任意逻辑函数取反时，把“+”⇄“·”互换并对所有变量取反）
**4.香农展开定理（Shannon’s Expansion Theorems）**
![image19 3|image19 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image19%203.png)
### **4.6 NAND定理**
![image20 3|image20 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image20%203.png)
### **4.7 XOR定理**
![image21 3|image21 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image21%203.png)
### **4.8 对偶定理**
要得到一个表达式的**对偶形式**：
1. **把所有的 AND（∙）换成 OR（+）**；
2. **把所有的 OR（+）换成 AND（∙）**；
3. 保留变量和括号结构不变。
|   |   |
|---|---|
||F = X • Y + Z • W|
||Fᴰ = (X + Y) • (Z + W)|
对偶定理的意义：
- 在**化简逻辑函数**时非常有用；
- 在**布尔代数的证明**中，可以用对偶原理直接推出一组对应的定理；
### **4.9 Consensus Theorem (T11) 一致性定理**
是布尔代数中一个非常重要的**化简规则**，它可以帮助我们识别和**删除逻辑表达式中不必要的（冗余）项**，使表达式更简洁高效。
一致性定理的标准形式是：
![image22 3|image22 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image22%203.png)
## **5 求逻辑函数的补**
**方法一：使用德摩根定律（De Morgan’s Theorem）**
![image23 3|image23 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image23%203.png)
这就告诉我们：
- 补一个与式（AND）会变成一个或式（OR）并对每个变量取反；
- 补一个或式（OR）会变成一个与式（AND）并对每个变量取反。
**方法二：使用真值表（Truth Table）**
简单地说就是暴力枚举
**方法三：互换运算符并对变量取反**
将 AND 和 OR 互换，同时对每个变量取反。
例如：
![image24 3|image24 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image24%203.png)
## **6 标准形式表示逻辑函数**
![image25 3|image25 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image25%203.png)
一共有如下三种形式：
### **6.1 最小项代数和 Algebraic sum of minterms (Canonical Sum)**
**minterms：最小项**是一个逻辑表达式，在某一特定输入组合下取值为 **1**，在其它输入组合下取值为 **0**。每个最小项是 **所有输入变量的“与”运算（AND）**，变量个数等于输入变量个数；
**1 → 原变量**，例如 A = 1 → 用 A；
**0 → 取反变量**，例如 A = 0 → 用 A’。
将函数 F 表示为所有输出为 1 的最小项（minterms）之和（逻辑“或”），每个最小项表示使函数为真的输入组合。
本例中：
![image26 3|image26 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image26%203.png)
### **6.2 最大项代数积**
**maxterns：**是一个逻辑表达式，它在某一个输入组合下为 0，在其他所有输入组合下都为 1。每个最大项是所有输入变量的 **“或”（OR）表达式**；
**0 → 原变量（不取反）**；
**1 → 取反变量**。
将函数表示为所有输出为 0 的最大项（maxterms）之积（逻辑“与”）。与最小项方式互为对偶。
先求 F'（F 的反函数）：
![image27 3|image27 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image27%203.png)
利用**德摩根定律（de Morgan’s law）**：
![image28 3|image28 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image28%203.png)
### **6.3 总结**
|**表示方式**|**来源**|**特点**|
|---|---|---|
|真值表|最直观表示，列出全部输入/输出|可以生成下面两种|
|最小项代数和（Canonical Sum）|从真值表中输出为 1 的行得到|表示逻辑函数为“为真的所有情况”之和|
|最大项代数积（Canonical Product）|从真值表中输出为 0 的行得到|表示逻辑函数为“为假的所有情况”|
出题方向可能是把一个式子化成最小项代数和或者最大项代数积，可以用各种变换化出来，实在不行就用真值表（）