# Lecture 1

**1. 概率的定义**

- 概率 \( P(A) \) 是事件 \( A \) 发生的可能性，定义为：

$$
P(A) = \frac{\text{事件 A 发生的次数}}{\text{试验总次数}}，\ \lim_{n \to \infty} P(A) = \frac{\text{成功次数}}{n}
$$

其中，$$ 0 \leq P(A) \leq 1 $$。

**2. 全概率法则 (Law of Total Probability)**

设事件集合 \( B_1, B_2, \dots, B_n \) 互不相交且覆盖样本空间 \( S \)，对于任意事件 \( A \)，全概率法则为：

$$
P(A) = \sum_{i=1}^{n} P(A \mid B_i) P(B_i)
$$

**3. 包含-排除原理 (Inclusion-Exclusion Principle)**

对于两个事件 \( A \) 和 \( B \)，包含-排除原理为：

$$
P(A \cup B) = P(A) + P(B) - P(A \cap B)
$$

若扩展到三个事件 \( A \)、\( B \)、\( C \)，则：

$$
P(A \cup B \cup C) = P(A) + P(B) + P(C) - P(A \cap B) - P(B \cap C) - P(A \cap C) + P(A \cap B \cap C)
$$

**4. 条件概率与独立性**

条件概率表示事件 \( A \) 在事件 \( B \) 发生的条件下发生的概率：

$$
P(A \mid B) = \frac{P(A \cap B)}{P(B)},\ P(B) > 0
$$

若 $$ P(A \mid B) = P(A) $$，则 \( A \) 和 \( B \) 是独立事件。

**5. 期望值 (Expectation)**

对于离散随机变量 \( X \)，其期望 \( E(X) \) 为：

$$
E(X) = \sum_{x} x P(X = x)
$$

期望值表示随机变量可能取值的加权平均，权重为其发生的概率。

**6. 方差 (Variance)**

方差 \( \text{Var}(X) \) 衡量随机变量离散程度，定义为：

$$
\text{Var}(X) = E[(X - E(X))^2] = E(X^2) - [E(X)]^2
$$

方差是随机变量偏离其期望值的平方的期望，方差越大，随机变量的波动越大。

**7. 标准差 (Standard Deviation)**

标准差 $\text{SD}(X)$ 是方差的平方根：

$$
\text{SD}(X) = \sqrt{\text{Var}(X)}
$$

标准差的单位与原变量相同，因此比方差更直观。

**8. 集中趋势 (Measures of Central Tendency)**

集中趋势指标帮助总结随机变量的典型值：

- **均值 (Mean)**：数据的平均值，是最常用的集中趋势度量。
- **中位数 (Median)**：数据排序后位于中间的值，不受极端值的影响。
- **众数 (Mode)**：数据中出现频率最高的值，适用于分类数据。

**9. 不确定性 (Uncertainty)**

不确定性反映数据的波动性或分散性，常用指标包括：

- **方差**：衡量数据分散程度。
- **标准差**：与方差相关，但单位与数据相同，易于解释。
- **熵 (Entropy)**：用于离散随机变量，衡量信息量或不确定性，公式为：

$$
H(X) = - \sum_{x} P(X = x) \log[P(X = x)]
$$

熵越大，随机变量的结果越不确定。

**10. 概率分布**

概率分布描述了随机变量可能取值及其对应的概率。常见分布包括：

- **离散概率分布**：如二项分布 (Binomial Distribution)，表示重复独立试验中成功的次数。
- **连续概率分布**：如正态分布 (Normal Distribution)，常用于自然现象的数据建模。

**11. 中心极限定理 (Central Limit Theorem)**

当样本量足够大时，任意分布的样本均值将近似服从正态分布：

$$
\bar{X} \sim N\left(\mu, \frac{\sigma^2}{n}\right)
$$

这一定理为许多统计推断方法提供了理论基础。
