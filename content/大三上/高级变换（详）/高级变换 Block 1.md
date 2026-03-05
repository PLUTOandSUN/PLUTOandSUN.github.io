> 何威翰，编辑于2025/12/4
## 2 线性代数
### 2.1 双正交和对偶积

如果两组向量满足：

- 第 i 个向量和第 j 个向量的内积是 0，当 $i \neq j$
- 内积为 1，当 $i = j$

也就是：
$$
\langle \Psi_i , \hat{\Psi}_j \rangle = \delta_{ij}
$$
那么这 **两组向量彼此是双正交的（bi-orthogonal）**。

这与普通正交（orthogonal）不同：

- **正交基**：同一组向量内部两两正交
- **双正交基**：两组向量之间对应相互正交

**双正交的两组向量 = 对偶基（Dual Basis）**



### 2.2 正交归一基 Orthonormal Basis

什么叫正交归一（ONB）？
$$
\langle \psi_i, \psi_j \rangle = \delta_{ij}
$$
即：

- 不同向量点积为 0（正交）
- 每个向量长度为 1（归一）



如果基是正交归一的，则展开系数满足：
$$
\boxed{c_n = \langle s, \psi_n \rangle}
$$
这意思是：

> 一个向量的第 n 个分量，就是它和第 n 个基向量做内积。

向量 $s$ 可以写成：
$$
s = \sum_j \langle s, \psi_j \rangle \psi_j
$$
也就是说：
$$
s = 
\langle s, \psi_1\rangle\psi_1
+
\langle s, \psi_2\rangle\psi_2
+\cdots+
\langle s, \psi_n\rangle\psi_n
$$


## 3 傅里叶变换

### 3.1 离散傅里叶变换 DFT

离散时间信号 $x[n]$ 的 DTFT 是：
$$
X(\omega) = \sum_{n=-\infty}^{\infty}x[n]e^{-j\omega n}
$$
特点：

- 连续的
- 周期性（周期 $2\pi$）
- 数学上正确，但**不实用**，因为输入需要是无限长度。

**DFT 解决了 DTFT 不可计算的问题。**

若 $x[n]$ 在 0 到 $N-1$ 有效，则：
$$
X[k] = \sum_{n=0}^{N-1} x[n] e^{-j\frac{2\pi nk}{N}},\quad k=0,...,N-1
$$
DFT 假设：

- 输入信号 **周期性延拓为 N 周期**
- 输出 $X[k]$ 也是周期 N 的



### 3.2 快速傅立叶变换 FFT

FFT（快速傅里叶变换）是一种 **快速计算 DFT（离散傅里叶变换）** 的算法。
$$
X[k] = 
\sum_{n\text{ even}} x[n]W_N^{nk}
+
W_N^k \sum_{n\text{ odd}} x[n] W_N^{nk}
$$
令：

- even 部分：$x[2r]$
- odd 部分：$x[2r+1]$

得到：
$$
X[k] 
= G[k] + W_N^k H[k]
$$
其中：

- **G[k]**：偶数序列的 N/2 点 DFT
- **H[k]**：奇数序列的 N/2 点 DFT
**其输出结果与原始 DFT 在数学上是完全一致**

### 3.3 奈奎斯特折叠

当实际频率 $f$ 超过奈奎斯特频率 $f_s/2$ 时，
 信号会被映射成：
$$
f_{\text{alias}} = |f - m f_s|
$$
其中 $m$ 是让频率折回到 $0 \sim f_s/2$ 的整数
 （最常用的是离它最近的整数倍：$m = \text{round}(f/f_s)$）。



### 3.4 位反转

这是 FFT 的“输入重新排序技巧”。

例：8 点序列的二进制编号是：

| 十进制 | 二进制 |
| ------ | ------ |
| 0      | 000    |
| 1      | 001    |
| 2      | 010    |
| 3      | 011    |
| 4      | 100    |
| 5      | 101    |
| 6      | 110    |
| 7      | 111    |

将二进制位 **反转** 得到新的排序顺序。

![image-20251203155023405](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203155023405.png)

![image-20251203155031805](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203155031805.png)

### 3.5 计算低通滤波器阶数

先把目标幅度比 $p$（比如 5% = 0.05）变成 dB：
$$
A = 20\log_{10}(p)
$$
看从通带顶到要抑制的频率，是几倍频程（多少个 octave），记为 $N_{\text{oct}}$。
 比如这里是 1 个 octave。

每阶是 -6 dB / octave → n 阶总衰减约 **6n·$N_{\text{oct}}$** dB。
 所以：
$$
6n \cdot N_{\text{oct}} \ge |A|
\Rightarrow
n \ge \frac{|A|}{6N_{\text{oct}}}
$$
算出来再**向上取整**，就是估计的滤波器阶数。



## 4 离散余弦变换（DCT）

### 4.1 一阶DCT

对于长度为 N 的序列 s[n]，它的 DCT 系数是：
$$
DCT[k] = c(k) \sum_{n=0}^{N-1} s[n] \cos \frac{\pi (2n+1)k}{2N}
$$
其中：
$$
c(k)=
\begin{cases}
\sqrt{\frac{1}{N}}, &k=0\\
\sqrt{\frac{2}{N}}, &k>0
\end{cases}
$$
这相当于计算 **输入信号与不同频率余弦波的“相似度”（相关性）**。

k越大频率越高。

对 N 点 DCT，可以写成：
$$
DCT = \Psi \cdot s
$$
其中 Ψ 是 N×N 的 DCT 基函数矩阵。

例如 N=4 时：
$$
\Psi =
\begin{bmatrix}
0.5 & 0.5 & 0.5 & 0.5 \\
0.65 & 0.27 & -0.27 & -0.65 \\
0.5 & -0.5 & -0.5 & 0.5 \\
0.27 & -0.65 & 0.65 & -0.27
\end{bmatrix}
$$
N = 8 时：

![image-20251203165349256](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203165349256.png)



### 4.2 二阶DCT

![image-20251203165600319](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image-20251203165600319.png)
