# DSCI 523

**1. 读写数据**

```R
# 读csv
df <- read.csv('data.csv', sep='\t', row.names=1, skip=3, header=FALSE, stringsAsFactors=TRUE, parse_dates = TRUE)

# 读excel（需要readxl包）
library(readxl)
df <- read_excel('data.xlsx', sheet='sheet1')

# 使用download.file从URL下载文件
url <- 'https://example.com/data.csv'
download.file(url, "local_file.csv")  # 下载远程文件并保存为本地CSV

# 写csv
write.csv(df, 'data .csv', row.names=FALSE)
```

当`stringsAsFactors=TRUE` 时，会将df中的字符型变量自动转换为因子类型。

**2. 查看DataFrame基本信息**

```R
head(df, 3)  # 显示前3行
tail(df)     # 显示后6行（默认）

summary(df)  # 提供每列的统计信息
dim(df)      # 返回c(行数, 列数)

names(df)    # 返回列名
rownames(df) # 返回行名
```

**3. DataFrame增删改查**

```R
# 用clang举例
df <- df |>
  select(c('region', 'language', 'lang_known', 'population')) |> # 选择指定的列
	filter(language %in% c('Mandarin', 'Cantonese', 'Japanese', 'Korean')) |> # 根据条件筛选行
  group_by(region) |> # 按region分组
  summarise(
    lang_known = sum(lang_known),
    population = max(population) ) |> # 计算
  mutate(pct = round(lang_known / population * 100, 2)) |> # 创建新列
  rename(population = pop) |> # 重命名
  arrange(desc(pct)) |> # 按pct列降序排序
  slice(1:5) # 选1:5行
```

`%in%`：检查一个向量的元素是否在另一个向量中，`%within%`：检查某个日期/时间是否在指定的时间区间内

**4. 缺失值处理**

```R
# 检查整张表是否有缺失值
any(is.na(df))
colSums(is.na(df))

# 遍历df的指定列，检查每一行是否有为空的值
df[apply(df, 1, function(row) any(row == "")), ]

# 处理缺失值
df[is.na(df)] <- 0  # 用指定值填充
df |> drop_na()  # 删除包含NA的行  # 删除有缺失值的行
df |> replace_na(list(col = value))  # 用指定值替换NA

# 给指定列空值位置赋值
df |> replace_na(list(col = value))  # 用指定值替换NA
```

**5. 数据类型转换**

```R
sapply(df, class)  # 返回每列的数据类型
typeof(object)  # 返回对象的内部存储类型

df$col <- as.integer(df$col)  # 该列转换为整数类型
df$col <- as.character(df$col)  # 转换为字符型

# factor操作
sizes <- factor(c("large", "small", "medium"))  # 将列转换为因子类型，节省内存
df$size <- fct_relevel(df$size, "small", "medium", "large") # 重新排序
df$size <- fct_infreq(df$size) # 根据频率重新排序
df$size <- fct_lump_min(df$size, min = 2, other_level = "other") # 合并低频factor
df$size <- fct_recode(df$size, S = "small", M = "medium", L = "large") # 重命名factor

# 使用
levels(df$Class)
```

**6. 计算**

```R
# 最大值、最小值、平均值等
sapply(df, max)  # 每列最大值
sapply(df, min)  # 每列最小值
which.max(df$col)  # 指定列最大值对应的索引
mean(df$col)  # 求指定列均值
rowMeans(df)  # 每行平均值

# 按指定列分组，求另一列的均值
aggregate(col3 ~ col1 + col2, data=df, FUN=mean)

# 遍历数据框计算
apply(df, margin=2, sum)  # 每列总和，margin=2表示按列操作
t(apply(df, 1, function(x) x - mean(x)))  # 每行每个数值分别减去该行的均值
```

**7. Reshape DataFrame**

```R
# 列转行
df_long <- df |> 
  pivot_longer(
    cols = -c(index, col2),  # 选择要转换的列,排除index和col2
    names_to = "variable",   # 新的列名,用于存储原来的列名
    values_to = "value"      # 新的列名,用于存储值
  )

# 行转列
df_wide <- df_long |> 
  pivot_wider(
    id_cols = index,         # 用作标识的列
    names_from = variable,   # 从哪一列获取新的列名
    values_from = value      # 从哪一列获取值
  )

# 转置
t(df)

# 合并DataFrame
df_merged <- left_join(df1, df2, by = "key_column")  # 保留df1的所有行
# 除此以外还有inner_join, full_join, semi_join, anti_join

# 拼接DataFrame
df_concat <- bind_rows(df1, df2)  # 纵向拼接
df_concat <- bind_cols(df1, data.frame(z = c(1, 2, 3)))  # 横向拼接
```

**8. 时间日期处理**

```R
today() # 获取当前日期
now() # 获取当前日期和时间

# 创建日期时间
date <- ymd("2023-09-10")
datetime <- ymd_hms("2023-09-10 22:36:51")

# 解析日期字符串
date <- ymd("2023-01-31") # 年-月-日格式；还可以是mdy月日年，dmy日月年
year(df$date) # 获取年份; 月份month(), 日day(),星期几-以标签形式wday(label = TRUE), 季度quarter()

# 日期计算
date + days(1) # 加一天, 加一个月months(1), 加一年years(1)

# 创建日期范围
date_range <- seq(from = ymd("2023-01-01"), to = ymd("2023-12-31"), by = "day")
date_range <- interval(start = '2021-06-10', end = '2021-09-10')
```

**9. 字符串操作**

```R
# 字符串操作（使用stringr包）
str_to_lower(df$col)  # 转换为小写；大写str_to_upper(df$col)
str_trim(df$col)  # 去除首尾空白
str_detect(df$col, 'pattern')  # 检查是否包含特定字符
str_extract(string, 'of.*Columbia')  # "of-British-Columbia"
str_extract_all(string, 'pattern')  # 提取所有匹配的子串
str_replace_all(text, "-", " ")  # 替换字符串
str_split(df$col, ',')  # 分割字符串by逗号
str_c("Hello", "World", sep = " ")  # 连接字符串 "Hello World"
str_length(df$col)  # 计算字符串长度

# 正则表达式
str_extract(df$col, '([A-Za-z0-9.-]+)')  # 提取字母数字小数点连字符
str_extract_all(df$col, '\\b\\w{6}\\b')  # 查找6个字符的单词
```

**10. DataFrame改动**

```R
df$new_col <- df$old_col * 2  # 添加列
df$new_col <- sapply(df$old_col, function(x) x * 2)  # 使用sapply对每个元素进行操作
df$new_col <- ifelse(df$old_col > 10, '大于10', '小于等于10')  # 基于条件为新列赋值

df$col <- NULL  # 删除列
df <- df[, -which(names(df) == "col")]  # 删除特定列

df <- df[order(df$col1, -df$col2), ]  # 排序，可以按多列
rownames(df) <- df$col  # 设置行名

# 操作列名
rename(df, new_name = `OLD NAME`)
names(df) <- c('new_name1', 'new_name2', ...)  # 重命名所有列
# 或者自动重命名
library(janitor)
clean_names(df) # 这个会自动重命名所有的columns

# 计数
unique(df$col)  # 返回唯一值
length(unique(df$col))  # 返回唯一值的数量
table(df$col)  # 每个唯一值出现的次数
```

**11. for和if-else的例子**

```R
aqi <- list(1, 3, 7)
date <- list("2020-09-13", "2020-09-12", "2020-09-11")
aqi_dict <- setNames(aqi, unlist(date))

aqi_before <- 0
aqi_after <- 0
for (i in 1:length(aqi_dict)) {
  key <- names(aqi_dict)[i]
  value <- aqi_dict[[i]]
  if(key > '2020-09-12'){
    aqi_after <- aqi_after + value
  } else {
    aqi_before <- aqi_before + value
  }
}
aqi_before_mean <- round(aqi_before/sum(names(aqi_dict) < '2020-09-12'), 2)
```

**12. 可视化**

```R
library(ggplot2)
ggplot(df, aes(x=column1, y=column2, color=category_column)) +
  geom_point() + # sccater, 或者geom_bar, geom_boxplot
  labs(title="Title", x="X Label", y="Y Label") +
  theme_minimal()
```

