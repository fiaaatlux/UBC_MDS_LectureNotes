# Lecture 2

**1. 分布的性质**

单一概率质量函数 (PMF)：如下表展示了墨西哥海滩上的螃蟹巢中的螃蟹数量。
$$
\begin{array}{|c|c|}
\hline
X = \text{螃蟹数量} & P(X = x) \\
\hline
0 & 0.4 \\
1 & 0.1 \\
2 & 0.1 \\
3 & 0.4 \\
\hline
\end{array}
$$

- 根据表格计算期望值 \(E(X)\) 和方差 \(Var(X)\)：

$$
E(X) = \sum_{x=0}^{3} x \cdot P(X = x) = 0 \times 0.4 + 1 \times 0.1 + 2 \times 0.1 + 3 \times 0.4 = 1.5
$$

  方差的计算：

$$
Var(X) = E(X^2) - [E(X)]^2
$$

  其中 \(E(X^2) = \sum_{x=0}^{3} x^2 \cdot P(X = x)\)，计算得：

$$
E(X^2) = 0^2 \times 0.4 + 1^2 \times 0.1 + 2^2 \times 0.1 + 3^2 \times 0.4 = 4.1
$$

  最终方差为：

$$
Var(X) = 4.1 - (1.5)^2 = 1.85
$$

**2. 随机变量变换**

- **随机变量变换**：随机变量可以通过数学函数进行变换，如 $Z = X^2$，即将螃蟹数量的平方作为新的随机变量 \(Z\)。对于变换后的随机变量，其概率分布会相应改变。

- 变换后的概率质量函数 (PMF) 如下：

$$
\begin{array}{|c|c|}
\hline
Z = X^2 & P(Z = z) \\
\hline
0 & 0.4 \\
1 & 0.1 \\
4 & 0.1 \\
9 & 0.4 \\
\hline
\end{array}
$$

**3. 期望值和方差的性质**

- **期望值的线性性质**：对于常数 \(a\) 和 \(b\)，随机变量 \(X\) 和 \(Y\)，有：

$$
E(aX + bY) = aE(X) + bE(Y)
$$

  注意：期望值并不满足通常的代数规则，如 \(E(XY) \neq E(X)E(Y)\)。

- **方差的性质**：对于独立的随机变量 \(X\) 和 \(Y\)，方差有：

$$
Var(aX + bY) = a^2 Var(X) + b^2 Var(Y)
$$

**4. 常见分布族**

**4.1 伯努利分布 (Bernoulli Distribution)**

- **定义**：只有两个可能结果的分布，记作 $X \sim \text{Bernoulli}(p)$，其中 \(p\) 是事件发生的概率。

- **概率质量函数 (PMF)**：

$$
P(X = x \mid p) = p^x(1 - p)^{1-x}, \quad x = 0, 1
$$

- **均值**：$E(X) = p$

- **方差**：$\text{Var}(X) = p(1 - p)$

**4.2 二项分布 (Binomial Distribution)**

- **定义**：进行 \(n\) 次独立试验，每次试验成功的概率为 \(p\)，记作 $X \sim \text{Binomial}(n, p)$。

- **概率质量函数 (PMF)**：

$$
P(X = x \mid n, p) = \binom{n}{x} p^x (1 - p)^{n-x}, \quad x = 0, 1, \dots, n
$$

- **均值**：$E(X) = np$

- **方差**：$\text{Var}(X) = np(1 - p)$

**4.3 几何分布 (Geometric Distribution)**

- **定义**：表示在首次成功前发生失败的次数，记作 $X \sim \text{Geometric}(p)$。

- **概率质量函数 (PMF)**：

$$
P(X = x \mid p) = p(1 - p)^x, \quad x = 0, 1, \dots
$$

- **均值**：$E(X) = \frac{1 - p}{p}$

- **方差**：$\text{Var}(X) = \frac{1 - p}{p^2}$

**4.4 泊松分布 (Poisson Distribution)**

- **定义**：描述单位时间内事件发生的次数，记作 $X \sim \text{Poisson}(\lambda)$，其中 $\lambda$ 是单位时间内的平均发生率。

- **概率质量函数 (PMF)**：

$$
P(X = x \mid \lambda) = \frac{\lambda^x e^{-\lambda}}{x!}, \quad x = 0, 1, \dots
$$

- **均值**：$E(X) = \lambda$

- **方差**：$\text{Var}(X) = \lambda$
