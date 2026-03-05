### 9.1 arallel-plate transmission lines平行板传输线
**核心图像：**
![image.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/20251219015834611.png)
**1. 场分布与电压电流的关系**

- **电场 ($E$) $\rightarrow$ 电压 ($V$)：** 在两板之间对电场积分，可以得到电压 $V(z)$ 
- **磁场 ($H$) $\rightarrow$ 电流 ($I$)：** 利用安培环路定理，磁场在导体表面的积分对应电流 $I(z)$ 


2. 传输线方程 (Transmission-Line Equations)

- 通过麦克斯韦方程组的推导，得出了描述电压和电流沿 $z$ 轴变化的方程组（无损耗）：

$$\frac{dI(z)}{dz} = -j\omega C V(z)$$

$$\frac{dV(z)}{dz} = -j\omega L I(z)$$


   这两个方程描述了电压 $V$ 和电流 $I$ 沿传输方向 $z$ 的变化关系 。
    
- 二阶波动方程：通过对上述方程再次求导并相互代入，得到了二阶微分方程：
    
    $$\frac{d^2I(z)}{dz^2} = -\omega^2 LCI(z)$$
    $$\frac{d^2V(z)}{dz^2} = -\omega^2 LCV(z)$$
    
    这说明电压和电流在传输线上是以**波**的形式传播的。
    
- **通用解**：图中给出的解形式为 $I(z) = I_0 e^{-j\beta z}$ 和 $V(z) = V_0 e^{-j\beta z}$，其中相位常数定义为 $\beta = \omega \sqrt{LC}$ 。

3. 关键的电路参数 ($L$ 和 $C$)

这两个参数是传输线的“身份证”，由物理结构决定：

- **单位长度电容 ($C$)：** $C = \epsilon \frac{w}{d}$ 。
- **单位长度电感 ($L$)：** $L = \mu \frac{d}{w}$ 。
	- 其中 $\epsilon$ 是介电常数，$\mu$ 是磁导率，$w$ 是板宽，$d$ 是板间距。


4. 特性参数 (Characteristic Parameters)

这一部分非常重要，用于计算传输线的性能：

- **相位常数 ($\beta$)：** 描述波传播时的相位变化快慢。 $\beta = \omega \sqrt{LC} = \omega \sqrt{\mu\epsilon}$ 。
- **波速 ($v_p$)：** 波传播的速度。 $v_p = \frac{1}{\sqrt{LC}} = \frac{1}{\sqrt{\mu\epsilon}}$ 。
- **特性阻抗 ($Z_0$)**： 这是传输线最重要的参数之一，代表电压波和电流波的比值。

$$Z_0 = \sqrt{\frac{L}{C}} = \frac{d}{w} \sqrt{\frac{\mu}{\epsilon}}$$

### 9.2 arallel-plate transmission lines 平行板传输线
1. **等效电路模型**

我们将传输线切成无数个微小的段 ($\Delta z$)，每一段包含四个元件：
- $R$：串联电阻（导体的损耗）
- $L$：串联电感（磁场效应）
- $G$：并联电导（介质的漏电流损耗）
- $C$：并联电容（电场效应）

2. **通用的传输线方程**

电流变化 ($\Delta I$)：由于并联支路（$G$ 和 $C$）的分流，电流随距离增加而减小 8：
    $$\Delta I = -V(j\omega C\Delta z + G\Delta z)$$
    
电压变化 ($\Delta V$)：由于串联支路（$R$ 和 $L$）的压降，电压随距离增加而减小 9：
    $$-\Delta V = I(j\omega L\Delta z + R\Delta z)$$

在这个模型下，方程变得稍微复杂一点：

$$-\frac{dV}{dz} = I(R + j\omega L)$$
$$-\frac{dI}{dz} = V(G + j\omega C)$$


3. **通用的特性参数**

- 传播常数 ($\gamma$)： 现在变成了一个复数 $\gamma = \alpha + j\beta$。
    $$\gamma = \sqrt{(R + j\omega L)(G + j\omega C)}$$
    其中 $\alpha$ 是衰减常数（波会变弱），$\beta$ 是相位常数。
    
- 有损耗的特性阻抗 ($Z_0$)：
    $$Z_0 = \sqrt{\frac{R + j\omega L}{G + j\omega C}}$$

当我们解这些方程时，会发现电压和电流由两部分组成：

$$V(z) = V_0^+ e^{-\gamma z} + V_0^- e^{\gamma z}$$



这里你要理解物理意义：

- $e^{-\gamma z}$ 项代表**入射波 (Forward wave)**，向 $+z$ 方向传播。
- $e^{\gamma z}$ 项代表**反射波 (Reflected/Backward wave)**，向 $-z$ 方向传播 。


**关键结论：**

- 对于**入射波**，电压除以电流等于 $Z_0$ 。
- 对于**反射波**，电压除以电流等于 $-Z_0$ 。



