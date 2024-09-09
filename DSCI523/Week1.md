# Lecture 1&2

**0. 基本包导入**

```R
# 安装并加载tidyverse包
install.packages("tidyverse")
library(tidyverse)

# 加载其他所需的包
library(readr)
library(readxl)
library(ggplot2)
```

`tidyverse` 是一个包含数据操作和可视化功能的R包集。
`readxl` 用于读取Excel文件，支持多工作表。
`ggplot2` 是用于绘制各种类型图表的强大工具。

**1. 读取和导入数据**

```R
# 读取CSV文件
df <- read_csv("path_to_file.csv")  # 从本地CSV文件读取数据

# 从Excel文件读取
df <- read_excel("path_to_file.xlsx", sheet = "Sheet1")  # 从Excel读取指定工作表

# 使用download.file从URL下载文件
download.file("https://example.com/data.csv", "local_file.csv")  # 下载远程文件并保存为本地CSV

# 从RDS文件读取
df <- readRDS("path_to_file.rds")  # 读取RDS格式的R文件
```

`download.file()` 从URL下载文件并保存到本地。
`read_csv()` 用于读取CSV文件，支持指定分隔符如 `sep="\t"`。
`read_excel()` 读取Excel文件时可通过 `sheet="Sheet1"` 指定工作表。
`readRDS()` 读取RDS格式的文件，适用于高效存储大数据。

**2. 查看数据**

```r
head(df)
dim(df)
df.shape

# Jupyter里可以用options来限制最大读取行数方便展示数据
options(repr.matrix.max.rows = 10) # 表示最多展示10行(前后各5行)

# 重命名columns
rename(df,
      NEW_COLUMN_NAME = `OLD COLUMN NAME`)

# 建议直接用另一个包里的自动重命名function
library(janitor)
clean_names(df) # 这个会自动重命名所有的columns
```

**3. 数据类型与转换**

```R
# 查看数据结构和类型
str(df)  # 检查数据框的列名及类型，如factor、numeric、character等

# 修改数据类型
df$column_name <- as.numeric(df$column_name)  # 将列转换为数值类型
df$column_name <- as.integer(df$column_name)  # 将列转换为整数类型
```

`str()` 显示每列的数据结构和类型。
`as.numeric()` 将列转换为数值类型，适用于带小数的数值。
`as.integer()` 将列转换为整数类型，通常用于离散数据。

**4. 数据操作与处理**

```r
# 筛选特定行
df_filtered <- df |>
  filter(column_name == "value")  # 按条件筛选行

# 选择特定列
df_selected <- df |>
  select(column1, column2)  # 选择需要的列

# 创建新列
df <- df |>
  mutate(new_column = column1 * 2)  # 通过现有列的运算创建新列

# 分组并计算聚合值
df_grouped <- df |>
  group_by(group_column) |>
  summarise(new_column = sum(value_column))  # 按某列分组并计算总和

# 数据排序
df_sorted <- df |>
  arrange(desc(column_name))  # 按指定列降序排序

# 选择特定行
df_slice <- df |>
  slice(1:10)  # 选择前10行

# 选取特定值
df |>
	arrange(desc(column_name)) |> # 先按指定列降序排序
	slice(1) |> # 然后选第1行
	pull(column_name) # 最后选需要的那列

# 合并数据框
df_merged <- df1 |>
  left_join(df2, by = "key_column")  # 根据共同列名合并两个数据框
```

`filter()` 用于筛选行，基于指定条件。
`select()` 选择指定的列，用于简化数据框的列。
`mutate()` 创建新列，支持使用现有列的运算结果。
`group_by()` 与 `summarise()` 结合使用，用于按组汇总统计。
`arrange()` 按列进行升序或降序排序。
`slice()` 用于选择特定行，例如前10行。
`left_join()` 根据共同列合并数据框，类似于SQL中的左连接。

**5. 数据转换与整理**

```r
# 数据透视表
df_pivot <- df |>
  pivot_wider(names_from = "category_column", 
              values_from = "value_column"
             )  # 将长格式数据转换为宽格式

# 数据长宽转换
df_long <- df |>
  pivot_longer(cols = c("col1", "col2"), 
               names_to = "new_column", 
               values_to = "values"
              )  # 将宽格式转换为长格式

# 数据收集与展开
df_gathered <- df |>
  gather(key = "key_column", 
         value = "value_column", 
         col1, col2
        )  # 将多列收集为键值对
```

`pivot_wider()` 将长格式数据转换为宽格式，适合将类别变量转换为列名。
`pivot_longer()` 将宽格式转换为长格式，便于处理多列数据并合并到一列中。
`gather()` 是旧版的函数，用于将多列数据收集到两列中，类似于`pivot_longer()`。

**6. 数据可视化**

```r
# 绘制散点图
ggplot(df, aes(x = x_column, y = y_column)) +
  geom_point()  # 创建散点图，适用于展示两个变量之间的关系

# 绘制柱状图
ggplot(df, aes(x = factor_column, y = value_column)) +
  geom_bar(stat = "identity")  # 创建柱状图，展示不同类别的数值分布

# 绘制箱线图
ggplot(df, aes(x = factor_column, y = value_column)) +
  geom_boxplot()  # 创建箱线图，展示数据的分布及离群值
```

`ggplot()` 用于创建可视化图表。
`geom_point()` 用于创建散点图，展示两个变量之间的关系。
`geom_bar()` 用于创建柱状图，展示不同类别的数据分布。
`geom_boxplot()` 用于创建箱线图，展示数据的中位数、四分位数和离群值。

**7. 数据导出**

```r
# 将数据导出为CSV文件
write_csv(df, "output_file.csv")  # 将数据框导出为CSV格式

# 保存为RDS文件
saveRDS(df, "output_file.rds")  # 将数据保存为RDS格式
```

`write_csv()` 将数据框保存为CSV文件，便于与其他工具交换数据。
`saveRDS()` 保存为RDS格式，适合长期存储并在后续R项目中加载。

**8. 基本运算与控制结构**

```r
# 基本运算符
x <- 10
y <- 5

result <- x + y  # 加法运算
result <- x * y  # 乘法运算

# 条件判断
if (x > y) {
  print("x大于y")  # 如果x大于y，输出提示
} else {
  print("x小于或等于y")  # 否则输出其他提示
}

# 循环
for (i in 1:10) {
  print(i)  # 循环打印1到10的数字
}
```

`+` 和 `*` 分别用于加法和乘法运算。
`if` 语句用于条件判断，决定程序的执行逻辑。
`for` 循环用于遍历数值序列或数据框中的行，适合重复性操作。
