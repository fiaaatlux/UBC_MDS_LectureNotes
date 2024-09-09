# Lecture 4

**1. 条件概率 (Conditional Probability)**

- 条件概率描述了在已知某事件发生的前提下，另一事件发生的概率。对于两个事件 \(A\) 和 \(B\)，条件概率定义为：

$$
P(A \mid B) = \frac{P(A \cap B)}{P(B)}, \quad P(B) > 0
$$

- 示例：假设一艘船在港口停留的时间随机分布，停留时间 \(L\) 的概率质量函数 (PMF) 如下：

$$
\begin{array}{|c|c|}
\hline
L (\text{天数}) & P(L = l) \\
\hline
1 & 0.25 \\
2 & 0.35 \\
3 & 0.20 \\
4 & 0.10 \\
5 & 0.10 \\
\hline
\end{array}
$$

假设我们知道船至少停留了 2 天，那么条件概率 $P(L = l \mid L > 2)$ 可以通过重新归一化 \(L = 3, 4, 5\) 的概率计算得到：

$$
P(L = 3 \mid L > 2) = \frac{P(L = 3)}{P(L > 2)} = \frac{0.20}{0.40} = 0.50
$$

同理可以得到：

$$
P(L = 4 \mid L > 2) = 0.25, \quad P(L = 5 \mid L > 2) = 0.25
$$

```r
# 定义原始概率
P_L <- c(0.25, 0.35, 0.20, 0.10, 0.10)
L_values <- 1:5

# 计算 P(L > 2)
P_L_gt_2 <- sum(P_L[3:5])

# 计算条件概率 P(L = 3 | L > 2), P(L = 4 | L > 2), P(L = 5 | L > 2)
P_L_given_gt_2 <- P_L[3:5] / P_L_gt_2
P_L_given_gt_2
```

**2. 条件期望与全期望法则 (Law of Total Expectation)**

- **全期望法则**指出，可以通过已知的条件期望和边缘概率来计算总体期望。若有随机变量 \(X\) 和 \(Y\)，则有：

$$
E(X) = \sum_{y} E(X \mid Y = y) P(Y = y)
$$

- 例如，对于船只停留时间 \(L\) 和所需的工作人员 \(G\)，假设我们知道条件期望$E(G \mid L = l)$ ，则可以通过边缘概率 \(P(L = l)\) 计算总期望 \(E(G)\)：

$$
E(G) = \sum_{l} E(G \mid L = l) P(L = l)
$$

具体计算为：
$$
E(G)=5×0.25+8×0.35+10×0.20+12×0.10+15×0.10=8.15
$$

```r
# 定义条件期望和边缘概率
E_G_given_L <- c(5, 8, 10, 12, 15)  # E(G | L = l)
P_L <- c(0.25, 0.35, 0.20, 0.10, 0.10)  # P(L = l)

# 计算总期望 E(G)
E_G <- sum(E_G_given_L * P_L)
E_G
```

**3. 多变量条件分布 (Multivariate Conditional Distributions)**

- 条件概率不仅可以用于单变量，还可以用于多变量情况。例如，若我们同时考虑船只停留时间 \(L\) 和所需的工作人员 \(G\)，则有联合分布：

$$
P(G = g \mid L = l) = \frac{P(G = g \cap L = l)}{P(L = l)}
$$

```r
# 定义联合概率和边缘概率
P_G_L <- matrix(c(0.1, 0.2, 0.15, 0.25, 0.1, 0.2), nrow=2, byrow=TRUE)
P_L <- rowSums(P_G_L)

# 计算条件概率 P(G | L)
P_G_given_L <- P_G_L / P_L
P_G_given_L
```

**4. 条件独立性 (Conditional Independence)**

- 随机变量 \(X\) 和 \(Y\) 在给定 \(Z\) 的情况下条件独立，当且仅当：

$$
P(X = x \cap Y = y \mid Z = z) = P(X = x \mid Z = z) P(Y = y \mid Z = z)
$$

- 条件独立性意味着在给定第三个变量的信息后，两个变量之间没有直接关联。
