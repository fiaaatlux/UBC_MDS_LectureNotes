**1. Why all this emphasis on sampling distributions? 为什么我们要强调抽样分布？**

- 在实际生活中，我们通常只有一个样本，无法像在模拟中那样揭示抽样分布。
- 抽样通常会耗费大量的时间和金钱，同时在某些推论或因果研究中，可能存在伦理问题。
- 由于样本统计量也是随机变量，它在估计总体参数时会存在变异性。因此，报告单一的估计值是不够的。

**2. Population, Sample, and Sampling Distributions (总体、样本和抽样分布)**

- 样本分布和样本估计量的抽样分布不同，它们与总体的关系也不相同。

- 示例：使用 Airbnb 数据集估计温哥华 Airbnb 房源每晚价格的总体均值 `μprice`。

  - **样本均值（sample mean）**：`x̄price`

  ```
  # 加载数据集并计算总体均值
  listings <- listings |>
    select(id, price) |>
    mutate(price = as.numeric(gsub('[$,]', '', price)))
  
  pop_mean_price <- listings |> 
  	summarize(pop_mean_price = round(mean(price), 2))
  ```

- 使用 `ggplot2` 绘制总体价格分布的直方图：

  ```
  pop_price_dist <- ggplot(listings, aes(price)) +
    geom_histogram(fill = "dodgerblue3", color = "lightgrey", bins = 60) +
    labs(x = "Price per Night ($)", y = "Count") +
    geom_vline(xintercept = pop_mean_price, color = "red", linewidth = 1.5)
  ```

**3. Sampling and Plotting (单次抽样和绘图)**

- 以样本大小 `n = 50` 进行抽样并绘制样本分布图。

  ```
  one_sample <- rep_sample_n(listings, size = 50)
  one_sample_mean_price <- one_sample |> 
  	summarize(one_sample_mean_price = mean(price))
  
  sample_dist_price <- ggplot(one_sample, aes(price)) +
    geom_histogram(fill = "dodgerblue3", color = "lightgrey", bins = 60) +
    geom_vline(xintercept = one_sample_mean_price, color = "purple", linewidth = 1.5)
  ```

**4. Multiple Sampling and Plotting (多次抽样和绘图)**

- 从数据集中抽取 1000 个样本，计算每个样本的均值，并绘制样本均值的分布。

  ```
  multiple_samples_n50 <- rep_sample_n(listings, size = 50, reps = 1000)
  multiple_samples_mean_price_n50 <- multiple_samples_n50 |> 
  	summarise(sample_mean = mean(price))
  
  sampling_dist_price_n50 <- ggplot(multiple_samples_mean_price_n50, aes(sample_mean)) +
    geom_histogram(fill = "dodgerblue3", color = "lightgrey", bins = 60)
  ```

**5. Sampling Distributions and their Relationship to Sample Size (抽样分布与样本大小的关系)**

- 不同样本大小对抽样分布的影响。样本越大，抽样分布越窄，标准误差越小。

  - 样本大小 `n = 10, n = 100` 进行相同操作，并比较不同样本大小的抽样分布。

  ```
  generate_sampling_dist <- function(data, size) {
    set.seed(552)
    sample <- rep_sample_n(data, size = size, reps = 10000) |> 
      summarise(
        mean = mean(diameter),
        standard_deviation = sd(diameter),
        .groups = 'drop'
      )
  }
  
  sampling_dist_10 <- generate_sampling_dist(answer2_1, 10)
  sampling_dist_100 <- generate_sampling_dist(answer2_1, 100)
  
  answer3_1 <- tibble(
    n = c(10, 100),
    mean = c(mean(sampling_dist_10$mean), mean(sampling_dist_100$mean)),
    standard_error = c(sd(sampling_dist_10$mean), sd(sampling_dist_100$mean))
  )
  
  plot_sampling_dist <- function(data, n) {
    ggplot(data, aes(x = mean)) +
    geom_histogram(binwidth = 0.01, fill = 'lightgrey') + 
    geom_vline(xintercept = mean(data$mean), color = "red", linewidth = 0.5) +
    labs(
      x = 'Acer tree\'s diameters (meters)',
      y = 'Count',
      title = paste('Sampling Distribution of 10,000 Sample Means with n =', n)
    ) +
    theme_minimal()
  }
  
  sampling_dist_by_n <- plot_grid(
    plot_sampling_dist(sampling_dist_10, 10),
    plot_sampling_dist(sampling_dist_100, 100),
    ncol = 1, rel_heights = c(1, 1)
  )
  ```

**6. Bootstrapping (自助法)**

- **自助法** 是从原始样本中有放回地抽样，生成大量 bootstrap 样本，并计算每个 bootstrap 样本的估计量。

- 生成一个 bootstrap 样本的代码如下：

  ```
  bootstrap_sample1 <- one_sample |>
    rep_sample_n(size = 50, replace = TRUE, reps = 1)
  mean_price_bootstrap_sample1 <- bootstrap_sample1 |> summarize(mean_price = round(mean(price), 2))
  ```

- 生成 1000 个 bootstrap 样本并计算每个样本的均值：

  ```
  bootstrap_distribution_n50 <- one_sample |>
    specify(response = price) |>
    generate(reps = 1000, type = "bootstrap") |>
    calculate(stat = "mean")
  ```

- 绘制 1000 个 bootstrap 样本的分布：

  ```
  boot_sampling_dist_price_n50 <- ggplot(bootstrap_distribution_n50, aes(stat)) +
    geom_histogram(fill = "dodgerblue3", color = "lightgrey", bins = 60)
  ```