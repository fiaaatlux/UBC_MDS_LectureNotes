# Lecture 3

**1. 联合分布 (Joint Distributions)**

- 联合分布是同时涉及两个或多个随机变量的概率分布。它可以是离散或连续的，并涵盖了所有可能的结果。

- 对于两个独立的抛硬币实验，每个硬币可能的结果为：正面 (H) 或反面 (T)。这些结果的联合概率为：

$$
P(X = H \cap Y = H) = P(X = H) \cdot P(Y = H) = 0.5 \cdot 0.5 = 0.25
$$

联合概率分布表如下：

$$
\begin{array}{|c|c|c|}
\hline
X / Y & H & T \\
\hline
H & 0.25 & 0.25 \\
T & 0.25 & 0.25 \\
\hline
\end{array}
$$

- 表中各个概率加和为 1，这符合概率分布的要求。

```r
# 定义联合概率分布
joint_prob <- matrix(c(0.25, 0.25, 0.25, 0.25), nrow=2, byrow=TRUE,
                     dimnames=list(c("H", "T"), c("H", "T")))
joint_prob

# 计算联合概率 P(X = H ∩ Y = H)
joint_prob["H", "H"]
```

**2. 边缘分布 (Marginal Distributions)**

- 边缘分布是从联合分布中获得的一个单独随机变量的分布。它通过将联合分布中的概率求和得到。

例如，计算$ P(X = H)$ 时，通过将联合分布中与 \( X = H \) 相关的概率加总：

$$
P(X = H) = P(X = H \cap Y = H) + P(X = H \cap Y = T) = 0.25 + 0.25 = 0.5
$$

```r
# 计算边缘分布 P(X = H)
P_X_H <- sum(joint_prob["H", ])
P_X_H
```

**3. 独立性 (Independence) 和 相关性 (Dependence)**

- 如果两个随机变量 \( X \) 和 \( Y \) 是独立的，则有：

$$
P(X = x \cap Y = y) = P(X = x) \cdot P(Y = y)
$$

- 例子：两个硬币抛掷的联合分布表表明它们是独立的，因为每个事件的联合概率等于其边缘概率的乘积。

```r
# 检查两个随机变量是否独立
P_X_H * P_X_H == joint_prob["H", "H"]
```

**4. 协方差 (Covariance) 和 Pearson 相关系数**

- **协方差** 用于衡量两个数值型随机变量之间的依赖关系。协方差公式如下：

$$
\text{Cov}(X, Y) = E[(X - E(X))(Y - E(Y))] = E(XY) - E(X)E(Y)
$$

- 若协方差为正，说明两个变量呈正相关；若为负，说明它们呈负相关；若为 0，则说明无线性关系。

- **Pearson 相关系数** 标准化了协方差，公式为：

$$
\rho_{XY} = \frac{\text{Cov}(X, Y)}{\sqrt{\text{Var}(X) \cdot \text{Var}(Y)}}
$$

相关系数的范围为 [-1, 1]，其中：
  - $\rho = 1$ 表示完全正相关，
  - $\rho = -1$ 表示完全负相关，
  - $\rho = 0$ 表示无线性关系。

```r
# 计算协方差
X <- c(1, 2, 3, 4)
Y <- c(2, 3, 4, 5)
cov(X, Y)

# 计算Pearson相关系数
cor(X, Y)
```

**5. Kendall’s $\tau_K$**

- **Kendall’s $\tau_K$** 是另一种衡量依赖性的方式，尤其适用于非线性依赖关系。其公式为：

$$
\tau_K = \frac{\text{Number of concordant pairs} - \text{Number of discordant pairs}}{\binom{n}{2}}
$$

其中，\( n \) 是样本对数。

**6. 方差的求和**

- 如果 \( X \) 和 \( Y \) 是独立的，两个随机变量和的方差为：

$$
\text{Var}(X + Y) = \text{Var}(X) + \text{Var}(Y)
$$

- 如果它们不独立，则需要加入协方差项：

$$
\text{Var}(X + Y) = \text{Var}(X) + \text{Var}(Y) + 2\text{Cov}(X, Y)
$$
