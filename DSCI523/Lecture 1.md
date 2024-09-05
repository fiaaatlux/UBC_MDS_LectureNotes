### Reading data, single data frame manipulations & tidying data in R

1. 写入/写出

```{r}
library(readr)
df <- read_csv("filename.csv", header = True, sep = ',', Skip = 0)
write_csv(df, "example-data/mtcars.csv")
```

2. 查看数据

```R
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

3. 清洗数据

```R
library(dplyr)

# select (选列)
select(df, COLUMN_NAME_1, COLUMN_NAME_2)
select(df, COLUMN_NAME_1:COLUMN_NAME_5) # 选1-5列
select(df, 1:5) # 还是1-5列，这样写也可以，但不建议

# filter（选行）
filter(df, country == 'USA', year > 2000) # 这个是and的关系
filter(df, country == 'USA' | year == 2000) # 这个是or的关系
filter(df, country %in% c('USA', 'Canada', 'Mexico')) # 也是or的关系

# mutate (新增/修改列)
mutate(df, 
       age = round(age, 0),
       tot_gdp = pop * gdpPercap,
       pop_thousands = pop / 1000
      ) # age那行就是直接在原col上修改；支持同时新增/修改多列

# arrange（排序）
arrange(df, age) # 这个是ascending order
arrange(df, desc(age)) # 要倒序的话得加这个
```

4. pipe `|>` operator

```R
# |> 等同于"then"的意思, 可以用于提升代码的可读性
# 这是R在21年新增的built-in功能, 在此之前需要用到别的包, 写法是%>%来表示
output <- select(filter(mutate(df, new_col = old_col * 2), other_col > 5), new_col)

# 比如针对上面这行代码，用|>的写法可以改成这样
output <- df |>
  mutate(new_col = old_col * 2) |>
  filter(other_col > 5) |>
  select(new_col)
```

5. 数据切片

```R
# Getting a single value from a dataframe
df |>
	arrange(desc(age)) |> # 先用age按倒序排列
	slice(1) |> # 然后选第1行
	pull(country) # 最后选需要的那列
```

6. 列转行 & 行转列

```R
# 列转行 pivot_longer
df |>
	pivot_longer(cols = `1999`:`2000`,
               names_to = 'year',
               values_to = '')

# 行转列 pivot_wider
df |>
	pivot_wider(names_from = type,
             values_from = count)
```

