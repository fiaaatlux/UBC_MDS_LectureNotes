**Probability**

$$1=P(A) + P(A^c)$$ ; $^c$ 就是 "not" 的意思

$$P(A \cup B) = P(A) + P(B) - P(A \cap B)$$ ; $\cup$ 是 "or" $\cap$ 是 "and"

$$P(A \cup B \cup C))&= P(A) + P(B) + P(C) - P(A \cap B) - P(B \cap C) - P(A \cap C) + \\ & \qquad P(A \cap B \cap C)$$

**Odds 赔率**

Odds是赔率，就是发生这件事的概率/不发生的概率

$$o = \frac{p}{1 - p}$$ ; 也可以推导出 $$p = \frac{o}{o+1}$$

**Entropy 熵**

$$H(X) = -\displaystyle \sum_x P(X = x)\log[P(X = x)]$$

熵越大表示包含的信息量越大，越小则信息量越小，比如如果为0则表示没有随机性

**Mean and Variance**

If $X$ is discrete, with $P(X = x)$ as a PMF, then:

$${E}(X) = \displaystyle \sum_x x \cdot P(X = x)$$

If $X$ is continuous, with $f_X(x)$ as a PDF, then:

$${E}(X) = \displaystyle \int_x x \cdot f_X(x) \text{d}x$$ ; 这个暂时不用，另一个课学

Total Variance: $${Var}(X) = \mathbb{E}(X^2) - [\mathbb{E}(X)]^2$$

Sample Variance: $$S^2 = \frac{1}{n-1} \sum_{i=1}^n (X_i - \bar{X})^2.$$

一般来说，实际操作中用到的都是sample variance，因为我们几乎不可能拥有全局样本。计算sample variance需要有每一个样本，如果没有样本默认就是算total variance

**Mode**

Mode 就是出现频率最高的那个值

**Standard Deviation**

$${SD}\left[ \text{Var}(X) \right] = \sqrt{\text{Var}(X)}$$



| Concept   | Formula                  | Explanation                                                  |
| --------- | ------------------------ | ------------------------------------------------------------ |
| Accuracy  | (TP + TN) / Total Sample | 对于给定的测试数据集，分类器正确分类的样本数与总样本数之比   |
| Precision | TP / (TP + FP)           | 预测为正的样本中有多少是真正的正样本(是针对我们预测结果而言的) |
| Recall    | TP / (TP + FN)           | 样本中的正例有多少被预测正确了(是针对我们原来的样本而言的)   |
