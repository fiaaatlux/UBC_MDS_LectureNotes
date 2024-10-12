**1. Statistical Inference (统计推断)**

Statistical inference is the process of using sample data to make conclusions about a population. 统计推断是使用样本数据来推断总体的过程。

There are two types of inference:

- **Estimation (估计)**
- **Hypothesis Testing (假设检验)**

**2. Types of Statistical Questions (统计问题的类型)**

1. **Descriptive (描述性问题)**: Summarizes characteristics of a data set. Example: What is the population in each US state?
2. **Exploratory (探索性问题)**: Identifies patterns or relationships between variables. Example: Does air pollution correlate with life expectancy?
3. **Inferential (推断性问题)**: Draws conclusions about a population based on sample data. Example: Is eating more vegetables associated with fewer illnesses?
4. **Predictive (预测性问题)**: Predicts outcomes for individuals. Example: How many illnesses will a person have next year?
5. **Causal (因果性问题)**: Examines whether changing one factor will change another. Example: Does smoking lead to cancer?
6. **Mechanistic (机制性问题)**: Explains the process of how changes occur. Example: How do changes in diet reduce illness?

**3. Steps for Performing Estimation (估计的步骤)**

1. Define the population of interest. 定义感兴趣的总体。
2. Select the appropriate sampling method (random, systematic, stratified, etc.). 选择合适的抽样方法（随机抽样、系统抽样、分层抽样等）。
3. Decide the sample size (using Power Analysis). 决定样本大小（使用功效分析）。
4. Collect the sampled data. 收集样本数据。
5. Calculate the sample statistic (e.g., mean, proportion). 计算样本统计量（如均值、比例）。
6. Infer the population parameter, accounting for sampling variability. 在考虑抽样变异的情况下推断总体参数。

**4. Airbnb Dataset Example (Airbnb 数据集示例)**

The dataset contains Airbnb listings for Vancouver in September 2020, including room types. The goal is to estimate the proportion of "Entire home/apt" listings. 数据集包含2020年9月温哥华的Airbnb房源信息，目的是估计“整套房/公寓”房源的比例。

Key Code Snippets (代码示例)：

```R
# Load necessary libraries
library(tidyverse)
library(infer)

# Load the dataset
listings <- read_csv("data/listings.csv")

# Select relevant columns
listings <- listings |> select(id, room_type)

# Group by room type and calculate frequency
listings |> group_by(room_type) |> summarise(n = n()) |> mutate(freq = round(n / sum(n), 3))
```

This code calculates the proportion of "Entire home/apt" in the dataset. In this case, 75.6% of the listings are entire homes or apartments. 该代码计算数据集中“整套房/公寓”的比例，在这个例子中，75.6%的房源为整套房/公寓。

**5. Sampling Example (抽样示例)**

Random sampling is used to estimate the proportion of entire homes/apartments. 通过随机抽样来估计整套房/公寓的比例。

```R
set.seed(552) # Ensure reproducibility
sample_1 <- rep_sample_n(listings, size = 40)
sample_1 |> group_by(room_type) |> summarise(n = n()) |> mutate(freq = round(n / sum(n), 3))
```

In the first sample of 40 listings, 80% are entire homes or apartments. 在第一个包含40个房源的样本中，80%的房源为整套房/公寓。

**6. Sampling Distribution (抽样分布)**

Sampling variation occurs when drawing multiple random samples. This is reflected in the distribution of the sample proportions. 抽样变异会在抽取多个随机样本时发生，这可以在样本比例的分布中反映出来。

```R
set.seed(552)
samples_10000 <- rep_sample_n(listings, size = 40, reps = 10000)

# Summarize the sampling distribution
sampling_dist <- samples_10000 |>
  group_by(replicate) |>
  summarise(
    n_E = sum(room_type == "Entire home/apt"),
    p_hat_E = sum(room_type == "Entire home/apt") / 40
  )

# Plot the distribution
sampling_dist |>
  ggplot(aes(x = p_hat_E)) +
  geom_histogram(binwidth = 0.025) +
  xlab("Sample Proportion Based on n = 40") +
  ggtitle("Sampling Distribution of the Sample Proportions")
```

This shows that the sampling distribution is centered near 0.756 (the population parameter) and follows a bell-shaped curve. 该示例展示了抽样分布的中心接近于0.756（总体参数），且呈现钟形曲线。

**7. Conclusion (结论)**

- Estimation allows us to make informed guesses about population parameters. 估计让我们能够对总体参数做出有依据的猜测。
- Sampling helps us avoid doing a complete census. 抽样可以帮助我们避免进行完整的人口普查。
- The sampling distribution gives insight into the variability of our estimates. 抽样分布让我们了解估计值的变异性。