# Lecture 5



```R
指数分布：
dexp()：密度函数
pexp()：累积分布函数
qexp()：分位数函数
rexp()：随机数生成

均匀分布：
dunif()：密度函数(PDF)
punif()：累积分布函数(CDF)
qunif()：分位数函数(Quantile Function)
runif()：随机数生成(Random Generation)

正态分布：
dnorm()
pnorm()
qnorm()
rnorm() 
```



**1. Continuous Uniform Distribution 连续均匀分布**

**a. Expected Value $\mathbb{E}(Y)$**

$\mathbb{E}(Y) = \frac{a+b}{2} = \frac{0+4}{2} = 2$

```R
expect_y <- mean(0:4) # expected value 2
```

**b. CDF $P(lowerbound \leq Y \leq upperbound)$**

例：$Y \sim \text{Continuous Uniform(0, 4)}$；求 $P(0.2 \leq Y \leq 0.3)$

首先要算连续均匀分布的PDF：$$f(y) = \frac{1}{b-a} = \frac{1}{4-0}$$ ，其中a和b是分布的下限和上限

```R
pdf <- dunif(1, min = 0, max = 4) # density 0.25
```

然后求CDF，$$P(0.2 \leq Y \leq 0.3) = \int_{0.2}^{0.3} \frac{1}{4} \, dy =[\frac{1}{4}x]_{0.2}^{0.3} = \frac{1}{4} \cdot (0.3 - 0.2) = \frac{1}{4} \cdot 0.1= \frac{1}{40}$$

```R
cdf <- punif(0.3, min = 0, max = 4) - punif(0.2, min = 0, max = 4) # probability 0.025
```

**c. Variance $\text{Var}(Y)$**

连续均匀分布Var公式：$$\text{Var}(Y) = \frac{(b-a)^2}{12}$$; 所有的连续均匀分布都是除12

 $$\text{Var}(Y) = \frac{(4-0)^2}{12} = \frac{16}{12} = \frac{4}{3} \approx 1.333$$

```R
variance <- (b - a)^2 / 12
```





**2. 分段线形分布**

PDF： $$ f_X(x) = \begin{cases} x \quad \text{for} \quad 0 < x \leq 1 \\ 2 - x \quad \text{for} \quad 1 < x \leq 2. \end{cases} $$

**a. Lecture在预定结束时间后60到90秒之间结束的概率是多少？**

计算CDF：$P(1 < X \leq 1.5) = \int_1^{1.5} (2-x) dx$

$\int_1^{1.5} (2-x) dx = [2x - \frac{1}{2}x^2]_1^{1.5} = (3 - \frac{9}{8}) - (2 - \frac{1}{2}) = \frac{3}{8} = 0.375$

**b. 分布的0.4-quantile是多少，即满足 $P(X \leq a) = 0.4$ 的 a 值？**

我们需要找到 a，使得 $\int_0^a f_X(x)dx = 0.4$

先试假如 a ≤ 1，那么就是： $\int_0^a x dx = \frac{1}{2}a^2 = 0.4$ 

$a^2 = 0.8$ $a = \sqrt{0.8} \approx 0.894$

因为 0.894 < 1，所以是对的

**c. 求Conditional PDF(条件概率密度函数)，给定Lecture最多超时1分钟内；即：** $$f_X(x \mid X \leq 1)$$

1. 根据原始的 PDF： $$ f_X(x) = \begin{cases} x \quad \text{for} \quad 0 < x \leq 1 \\ 2 - x \quad \text{for} \quad 1 < x \leq 2. \end{cases} $$
2. 条件 PDF ： $f_X(x | X \leq 1) = \frac{f_X(x)}{P(X \leq 1)} \quad \text{for} \quad 0 < x \leq 1$
3. 计算 $P(X \leq 1)$： $P(X \leq 1) = \int_0^1 x dx = [\frac{1}{2}x^2]_0^1 = \frac{1}{2}$
4. 现在，对于 $0 < x \leq 1$： $f_X(x | X \leq 1) = \frac{x}{\frac{1}{2}} = 2x$
5. 对于 $x > 1$，根据条件，概率为 0。

因此，条件 PDF 为：

$f_X(x | X \leq 1) = \begin{cases} 2x & \text{for } 0 < x \leq 1 \\ 0 & \text{otherwise} \end{cases}$













```R
# Sample generation
set.seed(1)
outcomes <- c('coin', 'shell', ...)
probs <- c(0.2, 0.05, ...)
n <- 10
sample(outcomes, size = n, replace = TRUE, prob = probs)


rbinom(n = 10, size = 5, prob = 0.6)
rgeom
rnbinom
rpois
```

```python
# Sample generation
np.random.seed(1)
outcomes = ['coin', 'shell', ...]
prob = [0.2, 0.05, ...]
n = 10
np.random.choice(1 = outcomes, size = n, p = probs)


scipy.stats.binom.rvs(n = 5, p = 0.6, size = 10)
scipy.stats.geom.rvs()
scipy.stats.nbino.rvs()
scipy.stats.poisson.rvs()
```



























