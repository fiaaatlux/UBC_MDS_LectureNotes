**1. Piecewise Linear Distribution (分段线形分布)** 在不同区间上变量的概率密度按线性规律变化,但不同区间有不同斜率和截距    |    PDF 密度函数:  $f_X(x) = \begin{cases} x & \text{for} \ 0 < x \leq 1 \\2 - x & \text{for} \ 1 < x \leq 2. \end{cases}$

问Lecture推迟60-90秒的概率是多少(CDF) $P(1 < X \leq 1.5) = \int_1^{1.5} (2 - x) dx= [2x - \frac{1}{2}x^2]_1^{1.5} = (3 - \frac{9}{8}) - (2 - \frac{1}{2}) = \frac{3}{8} = 0.375$

```r
f_X <- function(x) {ifelse(x <= 1, x, 2 - x)} # 定义pdf
cdf_value <- integrate(function(x) {2 - x}, lower = 1, upper = 1.5)$value # cdf, 结果应为 0.375
expected_value <- integrate(function(x) {x * f_X(x)}, lower = 0, upper = 2)$value # 期望值
expected_value_square <- integrate(function(x) {x^2 * f_X(x)}, lower = 0, upper = 2)$value # E(X^2)
variance <- expected_value_square - expected_value^2 # 方差
```

0.4-Quantile 即要找到 a使得 $P(X \leq a)=\int_0^a f_X(x)dx = 0.4$ ; 假如 a ≤ 1，那么 $\int_0^a x dx = \frac{1}{2}a^2 = 0.4$ ;  $a^2 = 0.8, a = \sqrt{0.8}$

```r
f_X <- function(x) {return(x)} # 定义目标函数，用于求解积分达到0.4的a值
quantile_0.4 <- uniroot(function(a) {integrate(f_X, lower = 0, upper = a)$value - 0.4}, interval = c(0, 1))$root # 结果应为0.894
```

求Conditional PDF(条件概率密度函数)，给定Lecture最多超时1分钟内；即条件PDF: $f_X(x | X \leq 1) = \frac{f_X(x)}{P(X \leq 1)} \quad \text{for} \quad 0 < x \leq 1$

其中: $P(X \leq 1) = \int_0^1 x dx = [\frac{1}{2}x^2]_0^1 = \frac{1}{2}$; 所以$f_X(x | X \leq 1) = \frac{x}{\frac{1}{2}} = \begin{cases} 2x & \text{for } 0 < x \leq 1 \\ 0 & \text{otherwise} \end{cases}$

**2. Continuous Uniform Distribution (连续均匀分布)** 表示在两个点 $a$ 和 $b$ 之间，所有值发生的可能性是相等的；常用于模拟完全随机事件，比如随机抽取数字

PDF 密度函数 :  $f_Y(y) = \frac{1}{b - a} \quad \text{for} \ a \leq y \leq b$    |    CDF 累积分布函数: $F_Y(y) = P(Y \leq y) = \frac{y - a}{b - a} \quad \text{for} \ a \leq y \leq b$    |    Expected Value: $\mathbb{E}(Y) = \frac{a + b}{2}$    |    Variance: $\text{Var}(Y) = \frac{(b - a)^2}{12}$

```r
pdf <- dunif(1, min = 0, max = 4) # 密度值为0.25
cdf <- punif(0.3, min = 0, max = 4) - punif(0.2, min = 0, max = 4) # 概率为0.025
expect_y <- mean(0:4) # 期望值为2
variance <- (b - a)^2 / 12 # a <- 0, b <- 4
```

**3. Gaussian Distribution (高斯分布 正态分布)** 由均值 $\mu$ 和标准差 $\sigma$ 描述, 常用于自然现象，如身高、测量误差、股市收益等    |    PDF 密度函数: $f_X(x \mid \mu, \sigma^2) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{(x - \mu)^2}{2\sigma^2}\right)$

```r
pdf <- dnorm(x, mean = mu, sd = sigma) # 结果为该点处的PDF值 x <- 1, mu <- 0, sigma <- 1
cdf <- 1 - pnorm(700, mean = mu, sd = sigma) # P(X>700)
quantile_0.95 <- qnorm(0.95, mean = mu, sd = sigma) # 结果应为 1.645
# E(X)就是mu, Var(X)就是sigma^2 不用算
```

**4. Exponential Distribution (指数分布)** 描述独立事件之间的时间间隔，记忆无关性 (Memoryless Property)；用于如电话呼叫间隔    |    PDF 密度函数：$f_X(x \mid \lambda) = \lambda \exp(-\lambda x) \quad \text{for} \ x \geq 0$

```r
pdf_value_exp <- dexp(x, rate = lambda) # x <- 1, lambda <- 2
cdf_value_exp <- pexp(x, rate = lambda) # cdf
quantile_0.9_exp <- qexp(0.9, rate = lambda) # 结果应为 1.151
expected_value_exp <- 1 / lambda
variance_exp <- 1 / lambda^2
```

**5. Maximum Likelihood Estimation (最大似然估计, MLE)** 是一种通过最大化观测数据发生的可能性来估计分布参数的方法；用于根据数据拟合分布模型，估计未知的参数

```r
accident_sample <- tibble(day_observed = as.integer(c(6, 5, 2, ...)))
possible_lambdas <- seq(0.3, 5, by = 0.1)
lambda_sequence_values <- tibble(
  possible_lambdas = possible_lambdas,
  likelihood = map_dbl(possible_lambdas, function(lambda){prod(dpois(accident_sample$day_observed, lambda = lambda))}),
  log_likelihood = map_dbl(possible_lambdas, function(lambda){sum(dpois(accident_sample$day_observed, lambda = lambda, log = TRUE))})
)
empirical_mle <- lambda_sequence_values$possible_lambdas[which.max(lambda_sequence_values$log_likelihood)]
analytical_mle <- mean(accident_sample$day_observed)
```

**6. Simulation** 以Poisson分布为例 - Poisson分布描述了单位时间或单位区域内发生某个事件的次数

```r
arrivals <- rpois(n_days, lambda=5) # 模拟每一天的到港船只数 n_days <- 10000
demand_gangs <- function(n_ships, lambda=5) {sum(rpois(n_ships, lambda))} # 模拟每艘船所需的工人
total_requests <- sapply(arrivals, demand_gangs) # 总请求,对每天到的船只数运行一次demand_gangs
simulation_outputs <- tibble(
  mean = mean(total_requests),
  var = var(total_requests),
  sd = sd(total_requests),
  q = quantile(total_requests, probs = c(0.25, 0.5, 0.75))
)
# A.Normal 正态分布; 连续型, 常用于模拟测量误差或自然现象，例如人的身高
heights <- rnorm(n, mean = mu, sd = sigma) # n <- 10, 均值mu <- 170 方差sigma <- 10
# B.Exponential 指数分布; 连续型, 常用于模拟两个独立事件之间的时间间隔
arrival_times <- rexp(n, rate = lambda_exp) # n <- 10, lambda_exp <- 2, 例:客户到达间隔
# C.Binomial 二项分布; 离散型, 模拟抛硬币
flip_results <- rbinom(n, size = 10, prob = p_success) # 随机数数量n<-10, 实验次数size<-10, p_success <- 0.5
# D.Geometric 几何分布; 离散型, 第一次成功前的失败次数
failures_before_first_success <- rgeom(n, prob = p_success) # n< - 10, p_success <- 0.3
# E.Negative Binomial 负二项分布; 离散型, 模拟n次成功前的失败次数
failures_before_success <- rnbinom(n, size = successes, prob = p_success) # successes <- 5 p_success <- 0.3
```

