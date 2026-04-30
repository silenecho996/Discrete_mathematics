
## 目录

1. Möbius函数
2. Möbius反演公式
3. 容斥原理
4. Burnside引理
5. Pólya计数定理
6. 典型应用举例
7. 总结表
---
## 1. Möbius函数
### 1.1 偏序集上的zeta函数
**定义**：在有限偏序集 $(P, \le)$ 上，定义 **zeta函数** $\zeta(x,y)$ 为：
$$\zeta(x,y) = \begin{cases} 1 & \text{if } x \le y \\ 0 & \text{otherwise} \end{cases}$$
**作用**：对于函数 $f: P \to \mathbb{R}$，定义
$$(f\zeta)(x) = \sum_{y \in P} f(y) \zeta(y, x) = \sum_{y \le x} f(y)$$
即zeta函数扮演了“前缀和”的角色。

---
### 1.2 Möbius函数的定义
**定义**：Möbius函数 $\mu: P \times P \to \mathbb{Z}$ 是zeta函数的**逆**（在卷积意义下）：
$$\mu \zeta = I$$
其中 $I$ 是单位矩阵：$I(x,y) = \begin{cases} 1 & x = y \\ 0 & x \ne y \end{cases}$
**等价定义**（递归形式）：
$$\mu(x,y) = \begin{cases}
1 & \text{if } x = y \\
-\sum_{x \le z < y} \mu(x,z) & \text{if } x < y \\
0 & \text{if } x \not\le y
\end{cases}$$
**基本性质**：
$$\sum_{x \le z \le y} \mu(x,z) = \begin{cases}
1 & \text{if } x = y \\
0 & \text{otherwise}
\end{cases}$$
---
### 1.3 链上的Möbius函数
设 $P = [n] = \{1,2,\dots,n\}$ 按自然序 $\le$，则：
$$\mu(i,j) = \begin{cases}
1 & \text{if } i = j \\
-1 & \text{if } i+1 = j \\
0 & \text{otherwise}
\end{cases}$$
---
### 1.4 乘积偏序集上的Möbius函数
**引理**：若 $P, Q$ 是偏序集，$P \times Q$ 是乘积偏序集（分量比较），则：
$$\mu_{P \times Q}\big( (x,y), (x',y') \big) = \mu_P(x,x') \cdot \mu_Q(y,y')$$
---
### 1.5 子集格上的Möbius函数
**偏序集**：$P = 2^{U}$，$S \le T \iff S \subseteq T$。
**Möbius函数**：
$$\mu(S,T) = \begin{cases}
(-1)^{|T| - |S|} & \text{if } S \subseteq T \\
0 & \text{otherwise}
\end{cases}$$
**证明思路**：子集格同构于 $\{0,1\}^{|U|}$ 的乘积偏序集，利用乘积性质可得。

---
### 1.6 除数格上的Möbius函数
**偏序集**：$P = \{ a \in \mathbb{N}^+ \mid a \mid n \}$，$a \le b \iff a \mid b$。
**Möbius函数**（数论中的Möbius函数）：
$$\mu(a,b) = \begin{cases}
(-1)^r & \text{if } \frac{b}{a} \text{ 是 } r \text{ 个不同素数的乘积} \\
0 & \text{otherwise}
\end{cases}$$
**证明**：利用质因数分解，将除数格同构为乘积偏序集 $P_1 \times P_2 \times \dots \times P_k$，其中 $P_i = \{0,1,\dots,n_i\}$ 是全序，再应用乘积性质。

---
## 2. Möbius反演公式
### 2.1 定理陈述
> **Möbius反演公式**（第一形式）
> 设 $P$ 是有限偏序集，$\mu$ 是其Möbius函数。对于 $f,g: P \to \mathbb{R}$，
> $$\forall x \in P,\ g(x) = \sum_{y \le x} f(y) \iff \forall x \in P,\ f(x) = \sum_{y \le x} g(y) \mu(y,x)$$

**矩阵形式**：$g = f\zeta \iff f = g\mu$。

---
### 2.2 对偶形式
> **Möbius反演公式**（第二形式）
> $$\forall x \in P,\ g(x) = \sum_{y \ge x} f(y) \iff \forall x \in P,\ f(x) = \sum_{y \ge x} \mu(x,y) g(y)$$

**矩阵形式**：$g = \zeta f \iff f = \mu g$。

---
### 2.3 例子：子集格上的反演
在子集格 $2^{U}$ 上，$\mu(S,T) = (-1)^{|T|-|S|}$（当 $S \subseteq T$）。
反演公式变为：
$$g(T) = \sum_{S \subseteq T} f(S) \iff f(T) = \sum_{S \subseteq T} (-1)^{|T|-|S|} g(S)$$
这就是**容斥原理**的代数形式。

---
### 2.4 例子：除数格上的反演

在除数格 $P = \{a \mid a \mid n\}$ 上，反演公式变为：
$$g(n) = \sum_{d \mid n} f(d) \iff f(n) = \sum_{d \mid n} \mu(d, n) g(d)$$
其中 $\mu(d,n)$ 是数论中的Möbius函数（常用记法 $\mu(n/d)$）。

---
## 3. 容斥原理
### 3.1 标准形式
**容斥原理**：设 $A_1, A_2, \dots, A_n \subseteq U$，则：
$$\left| U \setminus \bigcup_{i=1}^n A_i \right| = \sum_{I \subseteq [n]} (-1)^{|I|} \left| \bigcap_{i \in I} A_i \right|$$

---
### 3.2 Möbius反演推导
定义：
- $f(J) = \left| \left( \bigcap_{i \in J} A_i \right) \setminus \left( \bigcup_{i \notin J} A_i \right) \right|$（恰好只在 $J$ 中出现的元素个数）
- $g(J) = \left| \bigcap_{i \in J} A_i \right|$（至少包含所有 $J$ 中集合的元素个数）
则 $g(J) = \sum_{I \supseteq J} f(I)$。
在子集格 $2^{[n]}$ 上应用Möbius反演（对偶形式，$x=J, y=I$，$\mu(J,I)=(-1)^{|I|-|J|}$）：
$$f(J) = \sum_{I \supseteq J} \mu(J,I) g(I) = \sum_{I \supseteq J} (-1)^{|I|-|J|} \left| \bigcap_{i \in I} A_i \right|$$
取 $J = \emptyset$，$f(\emptyset) = \left| U \setminus \bigcup A_i \right|$：
$$\left| U \setminus \bigcup_{i=1}^n A_i \right| = \sum_{I \subseteq [n]} (-1)^{|I|} \left| \bigcap_{i \in I} A_i \right|$$
这就是容斥原理。

---
## 4. Burnside引理
### 4.1 基本概念
**配置 (Configuration)**：一个函数 $x: [n] \to [m]$，表示在 $n$ 个位置上染 $m$ 种颜色。所有配置的集合 $X = [m]^{[n]}$。
**置换 (Permutation)**：$\pi: [n] \to [n]$ 是双射。所有置换构成对称群 $S_n$。
**置换群 (Permutation Group)**：$G \subseteq S_n$，满足封闭性、结合律、单位元、逆元。
**群作用 (Group Action)**：$G \times X \to X$，定义为 $(\pi \circ x)(i) = x(\pi(i))$。
**轨道 (Orbit)**：$Gx = \{ \pi \circ x \mid \pi \in G \}$，即与 $x$ 等价的所有配置。
**等价类集合**：$X/G = \{ Gx \mid x \in X \}$，即所有不同的染色方案。

---
### 4.2 Burnside引理
> **Burnside引理**
> $$|X/G| = \frac{1}{|G|} \sum_{\pi \in G} |X_{\pi}|$$
> 其中 $X_{\pi} = \{ x \in X \mid \pi \circ x = x \}$ 是在置换 $\pi$ 下不变的配置集合。

**证明思路**（双计数）：
定义 $R = \{ (\pi, x) \in G \times X \mid \pi \circ x = x \}$。
- 按 $\pi$ 计数：$\sum_{\pi \in G} |X_{\pi}|$
- 按 $x$ 计数：$\sum_{x \in X} |\text{Stab}(x)|$，其中 $\text{Stab}(x)$ 是稳定子群
由轨道-稳定子定理，$|\text{Stab}(x)| = \frac{|G|}{|Gx|}$，因此：
$$\sum_{x \in X} |\text{Stab}(x)| = \sum_{x \in X} \frac{|G|}{|Gx|} = |G| \sum_{x \in X} \frac{1}{|Gx|} = |G| \cdot |X/G|$$
整理得 $|X/G| = \frac{1}{|G|} \sum_{\pi \in G} |X_{\pi}|$。

---
### 4.3 计算 $|X_{\pi}|$
给定置换 $\pi$，将其分解为**不相交轮换 (Cycle)** 的乘积：
$$\pi = (a_{11}a_{12}\dots a_{1l_1})(a_{21}a_{22}\dots a_{2l_2})\dots(a_{k1}a_{k2}\dots a_{kl_k})$$
其中 $l_1 + l_2 + \dots + l_k = n$。
**关键事实**：配置 $x$ 在 $\pi$ 下不变 $\iff$ 在每个轮换上，$x$ 取值**恒为常数**。
因此，每个轮换独立地选择一种颜色，共有 $m$ 种选择。
$$\boxed{|X_{\pi}| = m^{k}}$$
其中 $k = \#\text{cycle}(\pi)$ 是 $\pi$ 的轮换个数。

---
### 4.4 Burnside引理的标准形式
$$\boxed{|X/G| = \frac{1}{|G|} \sum_{\pi \in G} m^{\#\text{cycle}(\pi)}}$$
---
## 5. Pólya计数定理
### 5.1 问题背景
Burnside引理只能计算**染色方案的总数**，不能区分不同颜色出现次数的分布。
**更细粒度的需求**：对于给定的颜色计数向量 $\vec{v} = (n_1, n_2, \dots, n_m)$（$n_1 + \dots + n_m = n$），有多少种染色方案恰好包含 $n_i$ 个颜色 $i$？

---
### 5.2 模式清单 (Pattern Inventory)
**定义**：
- $a_{\vec{v}}$：在群 $G$ 作用下，恰好有 $n_i$ 个位置染颜色 $i$ 的**不同等价类**个数
- **模式清单**（多元生成函数）：
  $$F_G(y_1, y_2, \dots, y_m) = \sum_{\vec{v} = (n_1, \dots, n_m)} a_{\vec{v}} \, y_1^{n_1} y_2^{n_2} \cdots y_m^{n_m}$$

**目标**：找到 $F_G$ 的显式表达式。

---
### 5.3 Pólya计数定理
> **Pólya计数定理**
> $$F_G(y_1, y_2, \dots, y_m) = \frac{1}{|G|} \sum_{\pi \in G} M_{\pi} \left( \sum_{i=1}^m y_i,\ \sum_{i=1}^m y_i^2,\ \dots,\ \sum_{i=1}^m y_i^n \right)$$
> 其中 $M_{\pi}(t_1, t_2, \dots, t_n) = \prod_{j=1}^{k} t_{l_j}$，$l_j$ 是 $\pi$ 的第 $j$ 个轮换的长度。

---
### 5.4 推导思路
**第1步**：将配置按颜色计数向量分层
定义 $X^{\vec{v}} = \{ x \in X \mid \forall i,\ |x^{-1}(i)| = n_i \}$。
则 $a_{\vec{v}} = |X^{\vec{v}} / G|$。
**第2步**：对每个 $\vec{v}$ 应用Burnside引理
$$a_{\vec{v}} = \frac{1}{|G|} \sum_{\pi \in G} |X_{\pi}^{\vec{v}}|$$
其中 $X_{\pi}^{\vec{v}} = X^{\vec{v}} \cap X_{\pi}$。
**第3步**：构造生成函数
$$\sum_{\vec{v}} a_{\vec{v}} y_1^{n_1} \cdots y_m^{n_m} = \frac{1}{|G|} \sum_{\pi \in G} \sum_{\vec{v}} |X_{\pi}^{\vec{v}}| y_1^{n_1} \cdots y_m^{n_m}$$
**第4步**：内层求和的计算
对于固定的 $\pi$，轮换分解为长度 $l_1, \dots, l_k$。一个配置在 $\pi$ 下不变 $\iff$ 每个轮换内颜色相同。
因此，在 $\pi$ 下不变的配置，其颜色计数由每个轮换染什么颜色决定。对应的生成函数为：
$$\prod_{j=1}^k \left( y_1^{l_j} + y_2^{l_j} + \cdots + y_m^{l_j} \right) = M_{\pi} \left( \sum y_i,\ \sum y_i^2,\ \dots,\ \sum y_i^n \right)$$
**第5步**：代入即得Pólya公式。

---
### 5.5 例子：二面体群 $D_6$ 作用在六边形顶点上
设颜色数为 $2$（红、蓝），$F_{D_6}(y_1, y_2)$ 的展开包含：
- $y_1^6$：全红，1种
- $y_1^5 y_2$：5红1蓝，1种
- $y_1^4 y_2^2$：4红2蓝，3种
- ... 等
---
## 6. 典型应用举例
### 6.1 立方体面着色
**问题**：对正立方体的6个面用红、蓝、绿3种颜色着色，问：
1. 有多少种不同的方案？
2. 3种颜色各出现2次的方案有多少种？
**解法**：立方体的旋转群 $G$ 有24个元素。计算每个旋转的轮换结构，代入Burnside引理和Pólya公式。
---
### 6.2
布尔电路分类
**问题**：三元布尔函数可视为有3个输入端的布尔电路。通过交换输入端，多个布尔函数可表示为同一个电路。求实现所有三元布尔函数需要多少个不同的布尔电路？
**解法**：三元布尔函数共有 $2^{2^3} = 256$ 个。对称群 $S_3$ 作用在3个输入上。用Burnside引理计算轨道数。

| 置换类型 | 个数 | 不变函数数 |
| :--- | :--- | :--- |
| 恒等 | 1 | $2^8 = 256$ |
| 对换 | 3 | $2^{2^2} = 16$ |
| 3-轮换 | 2 | $2^{2^1} = 4$ |

轨道数 = $\frac{1}{6}(256 + 3 \times 16 + 2 \times 4) = \frac{1}{6}(256 + 48 + 8) = \frac{312}{6} = 52$。

---
## 7. 总结表

| 概念                  | 定义/公式                                                                            | 应用场景    |
| :------------------ | :------------------------------------------------------------------------------- | :------ |
| Zeta函数 $\zeta(x,y)$ | $1$ 若 $x \le y$，否则 $0$                                                           | 前缀和/后缀和 |
| Möbius函数 $\mu$      | $\zeta$ 的逆，$\mu\zeta = I$                                                        | 反演公式    |
| 子集格Möbius           | $\mu(S,T)=(-1)^{T-S}(S\subseteq T$）                                              | 容斥原理    |
| 除数格Möbius           | $\mu(a,b)=(-1)^r$（$b/a$ 为 $r$ 个不同素数积）                                            | 数论反演    |
| Möbius反演            | $g(x)=\sum_{y\le x}f(y) \iff f(x)=\sum_{y\le x}g(y)\mu(y,x)$                     | 反演求和    |
| 容斥原理                | $\bigcup A_i=\sum_{\emptyset\neq I\subseteq[n]}(-1)^{I+1}\bigcap_{i\in I}A_i$    | 计数并集    |
| Burnside引理          | $X/G= \frac{1}{G}\sum_{\pi\in G} m^{\#\text{cycle}(\pi)}$                        | 计数等价类总数 |
| Pólya定理             | $F_G = \frac{1}{G}\sum_{\pi\in G} \prod_{j} \left(\sum_{i=1}^m y_i^{l_j}\right)$ | 按颜色分布计数 |

---

## 8. 常见证明技巧总结

1. **Möbius反演**：递归定义 + 乘积偏序集分解
2. **容斥原理**：Möbius反演在子集格上的特例
3. **Burnside引理**：双计数法（$\sum |X_\pi| = \sum |Gx| = |G| \cdot |X/G|$）
4. **Pólya定理**：Burnside引理 + 生成函数 + 轮换分解

---

## 9. 自测题

1. 计算子集格 $2^{\{1,2,3\}}$ 中 $\mu(\{1\}, \{1,2,3\})$。
2. 写出容斥原理的Möbius反演推导过程。
3. 用Burnside引理计算正三角形顶点用2种颜色染色的方案数。
4. 用Pólya定理写出正三角形顶点染色中“2红1蓝”的系数。

**答案**：
1. $(-1)^{3-1} = (-1)^2 = 1$。
2. 见3.2节。
3. $D_3$有6个元素：恒等($2^3=8$)，3个反射($2^2=4$)，2个旋转($2^1=2$)，总数=$\frac{1}{6}(8+12+4)=4$。
4. 轮换结构：恒等 $t_1^3$，反射 $t_1t_2$，旋转 $t_3$。代入 $\sum y_i$ 展开得系数。

---

> 本文档涵盖课件《组合数学-3.pdf》的主要知识点：Möbius函数、Möbius反演、容斥原理的推导、Burnside引理和Pólya计数定理。如需更多例题或深入讲解，请告知具体方向。