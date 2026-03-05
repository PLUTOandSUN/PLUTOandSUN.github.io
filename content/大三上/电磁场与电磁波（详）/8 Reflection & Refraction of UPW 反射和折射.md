### 8.1 正常入射于完美导体

![image-20251218231500442](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251218231500442.png)

![image-20251218231509838](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251218231509838.png)

如上图，反射波的E和电磁波传输方向相反，H的传输方向相同。

### 8.2 正常入射于普通导体

#### 1 入射，反射和折射电场的关系

![image-20251218234917898](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251218234917898.png)



#### 2 入射，反射和折射磁场的关系

- **反射波磁场系数推导**

公式展示了反射波磁场振幅 $\dot{H}_0^r$ 与入射波磁场振幅 $\dot{H}_0^i$ 的关系：

- 推导过程：根据反射波磁场与电场的关系 $\dot{H}_0^r = -\frac{\dot{E}_0^r}{\eta_1}$，代入电场反射系数公式 $\dot{E}_0^r = \frac{\eta_2 - \eta_1}{\eta_2 + \eta_1} \dot{E}_0^i$，最终得出

  $$\dot{H}_0^r = -\frac{\eta_2 - \eta_1}{\eta_2 + \eta_1} \dot{H}_0^i$$

- **物理意义**：磁场反射系数 $R_H$ 等于电场反射系数 $R$ 的负值（即 $R_H = -R$）。

  

- **折射（透射）波磁场系数推导**

公式展示了折射波磁场振幅 $\dot{H}_0^t$ 与入射波磁场振幅 $\dot{H}_0^i$ 的关系：

- 推导过程：利用 $\dot{H}_0^t = \frac{\dot{E}_0^t}{\eta_2}$，代入电场透射系数公式 $\dot{E}_0^t = \frac{2\eta_2}{\eta_2 + \eta_1} \dot{E}_0^i$，化简后得出：

  $$\dot{H}_0^t = \frac{2\eta_1}{\eta_2 + \eta_1} \dot{H}_0^i$$

- **物理意义**：这定义了磁场透射系数 $T_H$。



| **物理量**  | **电场系数 (E)**                                  | **磁场系数 (H)**                    |
| -------- | --------------------------------------------- | ------------------------------- |
| **反射系数** | $R = \frac{\eta_2 - \eta_1}{\eta_2 + \eta_1}$ | $R_H = -R$                      |
| **折射系数** | $T = \frac{2\eta_2}{\eta_2 + \eta_1}$         | $T_H = \frac{\eta_1}{\eta_2} T$ |
| **关系式**  | $1 + R = T$                                   | $1 + R_H = T_H$                 |


#### 3 合成电场的物理分解 (Travelling vs. Standing Wave)

图片首先将总电场 $\vec{E}_1$ 进行数学变换，将其拆分为两部分：

$$\vec{E}_1 = \vec{e}_x \dot{E}_0^i (1+R) e^{-j\beta_1 z} e^{j\omega t} + \vec{e}_x \dot{E}_0^i R (e^{j\beta_1 z} - e^{-j\beta_1 z}) e^{j\omega t}$$

- **行波部分 (Travelling wave)**：
  - **公式**：$\vec{e}_x \dot{E}_0^i (1+R) e^{-j\beta_1 z} e^{j\omega t}$。
  - **解释**：这一项表示一列沿 $+z$ 方向传播的波，其振幅为入射电场与反射电场在界面处的叠加。这部分场代表了最终能够穿过界面、进入介质 2 进行能量传输的分量。
- **驻波部分 (Standing wave)**：
  - **公式**：$\vec{e}_x \dot{E}_0^i R (2j \sin \beta_1 z) e^{j\omega t}$（由括号内指数项利用欧拉公式转换而来）。
  - **解释**：这一项由于含有 $\sin \beta_1 z$ 且其时间项与空间项正交（由于 $j$ 的存在），它在空间中表现为固定的波节和波腹，不随时间向前移动。它代表了被“困”在介质 1 界面附近振荡、不传输净能量的场。



#### 4 驻波比 (Standing Wave Ratio, SWR)

当存在反射时，介质 1 中的电场振幅不再恒定，而是随位置 $z$ 波动：

- **线性比值**：$S = \frac{1+|R|}{1-|R|}$。
  - **推导**：这是合成场振幅最大值（$1+|R|$）与最小值（$1-|R|$）之比。
- **分贝形式**：$S_{dB} = 20 \lg S$。
- **意义**：$S$ 衡量了阻抗匹配的程度。若 $R=0$（匹配），则 $S=1$；若 $|R|=1$（全反射），则 $S=\infty$。



#### 5  功率流与能量守恒 (Power Flow)

这部分公式利用波印廷矢量证明了界面上的能量守恒：

- **反射功率流 ($\vec{S}_{av}^r$)**：
  - $$\vec{S}_{av}^r = -\vec{e}_z \frac{1}{2} \text{Re} [R \dot{E}_0^i (-R \dot{H}_0^i)^*] = -\vec{e}_z |R|^2 S_{av}^i$$
  - **解释**：反射功率的大小是入射功率的 $|R|^2$ 倍，方向向左（$-\vec{e}_z$）。
- **折射/透射功率流 ($\vec{S}_{av}^t$)**：
  - $$\vec{S}_{av}^t = \vec{e}_z \frac{\eta_1}{\eta_2} |T|^2 S_{av}^i = \vec{e}_z (S_{av}^i - S_{av}^r)$$
  - **解释**：这是进入介质 2 的功率。公式最后的 $(S_{av}^i - S_{av}^r)$ 明确表达了能量守恒定律：**入射功率 = 反射功率 + 透射功率**。



### 8.3 斜入射于完美导体

#### 1 电场强度表达式

根据波矢量的分解，推导出电场在空间和时间上的复数表示：

- 入射电场 $\vec{E}^i$：

  $$\vec{E}^i = \vec{e}_y \dot{E}_0^i e^{j(\omega t - \beta x \sin \theta_i - \beta z \cos \theta_i)}$$

- 反射电场 $\vec{E}^r$：

  $$\vec{E}^r = \vec{e}_y \dot{E}_0^r e^{j(\omega t - \beta x \sin \theta_r + \beta z \cos \theta_r)}$$

合成波的表达式：

$$\vec{E}^i + \vec{E}^r = \vec{e}_y [\dot{E}_0^i e^{-j(\beta x \sin \theta_i + \beta z \cos \theta_i)} + \dot{E}_0^r e^{-j(\beta x \sin \theta_r - \beta z \cos \theta_r)}] e^{j\omega t}$$



#### 2 斯涅尔反射定律

**角度关系**：从相位匹配条件中得出 $\theta_i = \theta_r$。

**物理结论**：即**反射角等于入射角**，这就是著名的斯涅尔反射定律。

当确定 $\theta_i = \theta_r$ 后，边界条件为：

- **振幅关系**：$\dot{E}_0^i + \dot{E}_0^r = 0$，即 $\dot{E}_0^r = -\dot{E}_0^i$。
- **相位翻转**：负号在复数表示中等同于 $e^{j\pi}$。
- **结论**：在理想导体表面，垂直偏振波的反射电场与入射电场相比，**相位发生了 $180^\circ$ ($\pi$) 的突变**。



#### 3 合成场方程

**最终场方程**：$\vec{E}^{total} = -j2\dot{E}_0^i \sin(kz \cos\theta)e^{j(\omega t - kx \sin\theta)}$。

- 注意公式中的 **$\sin(kz \cos\theta)$** 部分：它只与距离 $z$ 有关，表示在垂直于界面的方向上形成了**驻波**。
- 注意 **$e^{j(\omega t - kx \sin\theta)}$** 部分：它表示在平行于界面的 $x$ 方向上，波仍在**行进**。

总场是一种“混合波”：

- **行驻波特性**：在 $z$ 方向（垂直方向）表现为**驻波**，场强幅值随距离呈正弦变化；在 $x$ 方向（水平方向）表现为**行波**，能量沿界面传播。
- **TE 波 (横电波)**：由于电场 $\vec{E}$ 始终垂直于传播平面（仅有 $y$ 分量），这种合成波被称为横电波。



#### 4 **全反射 (Total reflection)**

$$
S_{av}^i = S_{av}^r
$$

**平均能流密度 ($S_{av}$)**：公式显示入射波的平均功率大小 $S_{av}^i$ 与反射波的平均功率大小 $S_{av}^r$ 完全相等。

**物理意义**：理想导体不消耗能量，所有的入射能量被全部反射回介质 1 中。虽然在界面附近有电磁场存在，但能量净流向仅平行于表面，**没有能量穿过 $z=0$ 的界面进入导体**。



### 8.4 斜入射于普通导体

#### 1 磁场强度表达式

![image-20251219134315889](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251219134315889.png)

**$\vec{H}^i$ (左上)**：入射磁场。

- $\vec{e}_y$：表示方向沿 y 轴（垂直纸面）。
- 指数部分 $e^{j(\omega t - \beta_1 \cos\theta_i z - \beta_1 \sin\theta_i x)}$：描述了波在介质 1 中向右下方传播的相位变化。

**$\vec{H}^r$ (右上)**：反射磁场。

- 注意前面的负号（或者是坐标定义导致的），表示反射波的某些分量方向变化。
- 指数部分体现了波向右上方传播（$z$ 方向变成了反向）。

**$\vec{H}^t$ (右下)**：透射磁场。

- 参数变成了 $\beta_2$（因为进入了介质 2，波数改变）。
- 角度变成了 $\theta_t$（折射角）。



#### 2 斯涅尔定律（Snell's Law）

**物理背景**：在无源（source-free）的分界面 $z=0$ 处，磁场的切向分量必须是连续的。

**数学表达式**：$H_{1t(z=0)} = H_{2t(z=0)}$，这意味着介质1中的总切向磁场（入射波 + 反射波）等于介质2中的切向磁场（透射波）。

**展开式**：通过代入磁场波函数的表达式，得到相位项的等式：$H_0^i e^{-j\beta_1 \sin\theta_i x} - H_0^r e^{-j\beta_1 \sin\theta_r x} = H_0^t e^{-j\beta_2 \sin\theta_t x}$

为了让上述等式对界面上**任意的 $x$ 值**都成立，所有指数项中的系数必须相等。

由此得出核心结论：

**$$\beta_1 \sin\theta_r = \beta_1 \sin\theta_i = \beta_2 \sin\theta_t$$



从上述相位匹配等式中，可以推导出两个重要的物理定律：

- **反射定律 (Law of Reflection)**：由于 $\beta_1 \sin\theta_r = \beta_1 \sin\theta_i$，得出 **$\theta_r = \theta_i = \theta$**，即反射角等于入射角。
- **折射定律 (Law of Refraction / Snell's Law)**：
  - 通过 $\beta_1 \sin\theta_i = \beta_2 \sin\theta_t$，整理得到：**$\frac{\sin\theta_t}{\sin\theta_i} = \frac{\beta_1}{\beta_2}$**。
  - 进一步利用波数 $\beta = \omega\sqrt{\mu\varepsilon}$ 展开，得到与介质参数的关系：$\frac{\sin\theta_t}{\sin\theta_i} = \frac{\omega\sqrt{\mu_0\varepsilon_1}}{\omega\sqrt{\mu_0\varepsilon_2}} = \sqrt{\frac{\varepsilon_1}{\varepsilon_2}}$。
  - 用折射率表示即为：$\frac{\sin\theta_t}{\sin\theta_i} = \frac{n_1}{n_2}$。

#### 3 菲涅耳公式 (Fresnel Equations)

给出了计算**反射系数 ($R$)** 和 **透射系数 ($T$)** 的具体公式，这些系数决定了能量有多少被反射，多少进入了第二种介质

![image-20251219140604863](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251219140604863.png)



#### 4 全反射（Total Reflection）

全反射并不是在任何情况下都会发生的，它必须满足以下两个前提：

- **光密介质射向光疏介质**：波必须从折射率（或介电常数）**高**的介质射向折射率**低**的介质。
  - 数学表达为：$\varepsilon_1 > \varepsilon_2$ 或 $n_1 > n_2$。
  - 在这种情况下，根据斯涅尔定律，折射角 $\theta_t$ 总是大于入射角 $\theta_i$（即图中所示的 $\theta_t > \theta_i$）。
- **入射角足够大**：当入射角 $\theta_i$ 达到或超过一个特定的数值——**临界角（Critical Angle, $\theta_c$）时，才会发生全反射。**


**临界角 ($\theta_c$) 的定义与计算**

- **物理定义**：临界角是指使**折射角达到 $90^\circ$** 时的入射角。

  - 此时折射波不再进入第二种介质，而是沿着交界面“滑行”。

- 数学公式：通过斯涅尔定律 $\frac{\sin\theta_t}{\sin\theta_i} = \frac{n_1}{n_2}$，令 $\theta_t = 90^\circ$（则 $\sin 90^\circ = 1$），可以推导出：

  

  $$\theta_i \ge \theta_c = \arcsin\sqrt{\frac{\varepsilon_2}{\varepsilon_1}} \quad \text{或} \quad \arcsin(\frac{n_2}{n_1})$$

  

**全反射时的物理特性**

- **能量完全反射**：当 $\theta_i > \theta_c$ 时，没有能量透射进入介质 2，所有的入射能量都被反射回介质 1。
- **反射系数**：在数学表达式上，此时平行极化和垂直极化的反射系数模值均等于 1，即 **$|R_P| = |R_N| = 1$**。

#### 5 全折射（Total refraction）

- **定义**：当反射系数等于零（$R=0$）时，所有的入射能量都透射进入了第二种介质，这种状态称为全折射。
- **条件**：这只发生在特定的入射角下，这个角度被称为 **布鲁斯特角 ($\theta_B$)**。



**全折射只对平行极化有效。**

- **平行极化 ($R_P$)**：通过令其反射系数公式的分子为零，可以解出一个特定的角度 $\theta_B$。
  - **计算公式**：$\theta_B = \arctan \sqrt{\frac{\varepsilon_2}{\varepsilon_1}}$（或者 $\arctan \frac{n_2}{n_1}$）。
  - 当波以这个角度入射时，平行极化波将**完全没有反射**。
#### 6 极化判断
在电磁学中，判断波的**极化状态（Polarization）**通常分为两种情景：一种是**相对于入射面**（多见于界面反射/折射问题），另一种是**描述电场矢量轨迹**（波本身的固有属性）。

---


当电磁波斜入射到两种介质的交界面时，我们通过以下步骤判断：

1. **确定入射矢量 $\vec{k}$**：根据相位项（如 $e^{-j\vec{k}\cdot\vec{r}}$）找波的传播方向。
    
2. **确定法线矢量 $\vec{n}$**：通常由界面决定（例如 $z=0$ 面，法线就是 $z$ 轴）。
    
3. **确定入射面**：由 $\vec{k}$ 和 $\vec{n}$ 共同构成的平面。
    
4. **观察电场 $\vec{E}$ 的方向**：
    
    - **垂直极化（Perpendicular / TE / s-polarization）**：$\vec{E}$ 垂直于入射面。
        
    - **平行极化（Parallel / TM / p-polarization）**：$\vec{E}$ 在入射面内。
        

> **以你之前的题目为例：**
> 
> - 入射方向 $\vec{k}$ 在 $y$ 和 $z$ 方向上，界面法线是 $z$ 轴，所以**入射面是 YZ 平面**。
>     
> - 电场 $\vec{E}$ 指向 $x$ 方向。
>     
> - 因为 $x$ 轴垂直于 YZ 平面，所以结论是**垂直极化**。
>