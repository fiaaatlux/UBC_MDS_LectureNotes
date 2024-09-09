# Lecture 1&2

**0. 基本设置与包导入**

```python
# 安装和导入pandas
conda install pandas
import pandas as pd

# 设置显示选项，设置最多展示6行
pd.set_option('display.max_rows', 6)

# 其他需要的库
import numpy as np
import altair as alt
```

在使用 `pandas` 时，首先要导入所需的包，如 `pandas` 用于数据操作，`numpy` 用于数值计算，`altair` 用于数据可视化。此外，`pd.set_option('display.max_rows', 6)` 设置了数据框在 Jupyter Notebook 中显示的最大行数为6。

**1. 读取和保存数据**

```py
# 读取CSV文件
df = pd.read_csv('文件路径.csv', sep='\t', skiprows=6, index_col='列名')
# sep: 指定分隔符，默认为Tab
# skiprows: 跳过前几行
# index_col: 指定哪一列作为索引

# 读取Excel文件
df = pd.read_excel('文件路径.xlsx', sheet_name='表名')
# sheet_name: 可以是表格的索引或名称

# 保存为CSV文件
df.to_csv('保存路径.csv', index=False)
# index=False: 不保存索引列
```

当读取本地文件时，`pd.read_csv()` 需要指定文件路径。如果是从URL读取，则直接传递链接。

`sep='\t'` 表示Tab作为分隔符，适用于制表符分隔的文件，如TSV文件。

`skiprows=6` 表示跳过前6行内容，常用于跳过文件中的元数据。

`header=None` 表示数据文件没有列名，需要手动指定列名。

使用 `index_col='列名'` 时，指定某一列作为数据框的索引，适用于已经有逻辑顺序的列。

读取Excel文件时，`sheet_name=2` 表示读取第二个工作表。如果表名是字符串，也可以直接传递表名。

除了最常用的这两个以外, pandas还能读各种不同类型的数据, 比如 `pd.read_html()`, `pd.read_json()`, and `pd.read_sql()` 等等...

**2. 数据框的基本操作**

```py
# 查看数据的前几行或后几行
df.head(3)  # 显示前3行
df.tail()   # 显示后5行（默认）

# 查看数据的基本统计信息
df.describe()  # 仅对数值列生效, 提供每个数值列的统计信息 (如平均值、标准差等)

# 获取数据框的形状
df.shape  # 返回(行数, 列数)

# 获取列名列表
df.columns.to_list()  # 返回列名作为列表
```

`.head()` 和 `.tail()` 是常用的查看数据方法，分别显示数据的前几行和后几行。未指定参数时，默认返回5行。

`.describe()` 提供数值列的统计信息，包括计数、均值、标准差、最小值、四分位数和最大值。仅适用于数值型数据。

`.shape` 返回数据框的行数和列数，形式为 (行数, 列数)，例如 (20, 9) 表示20行9列。

`.columns.to_list()` 将数据框的列名转化为列表形式，便于快速查看。

**3. 数据类型与转换**

```py
# 检查数据类型
df.dtypes  # 返回每列的数据类型

# 转换列的数据类型
df['列名'] = df['列名'].astype('int')  # 将列的数据类型转换为整数类型
```

`.dtypes` 返回数据框中每列的数据类型，帮助检查数据的结构，例如 int64, float64, object 等。

`astype()` 用于将列的数据类型进行转换，如从 float 转换为 int，或从字符串类型转换为日期类型等。

**4. 缺失值处理**

```py
# 检查缺失值
any(df.isna()) # 是否存在缺失值
df.isnull().sum()  # 每列的缺失值数量

# 填充缺失值
df.fillna(0)  # 将缺失值替换为0

# 删除含有缺失值的行
df.dropna()  # 删除所有含有缺失值的行
```

`.isnull().sum()` 是检查缺失值的常用方法，`isnull()` 返回一个布尔值数据框，`True` 表示缺失值，`sum()` 则对每列的 True 进行计数。

`.fillna()` 用于填充缺失值，可以指定不同的替换值，如0或均值。常用于处理缺失数据。

`.dropna()` 用于删除包含缺失值的行或列，默认删除有任何缺失值的行。

**5. 数据筛选与索引**

```py
# 选择特定列
df['列名']  # 返回特定列作为Series

# 按行索引选择数据
df.loc[[0]]  # 返回索引为0的行 (用loc按索引值选择行)
df.iloc[[0]] # 用iloc按行号选择数据

# 基于条件筛选行
df[df['列名'] == '条件']  # 返回符合条件的行

# 按行号和列名选择数据
df.loc[0:1, '列名1':'列名2']  # 使用loc按列名范围和行范围选择数据
df.iloc[0:1, 0:3]  # 使用iloc按行号和列号选择数据
```

`df['列名']` 返回某一列的数据，结果为 Series 类型。

`.loc[]` 和 `.iloc[]` 分别根据标签和位置进行数据选择。.loc[] 可以使用索引标签，.iloc[] 只支持位置索引。

基于条件筛选可以使用布尔索引，例如 `df[df['age'] > 30]` 返回所有 age 大于30的行。

**6. 数据修改**

```py
# 创建新列
df['新列'] = df['已有列'] * 2  # 通过现有列进行运算，创建新列

# 删除列
df = df.drop(columns=['列名'])  # 删除指定列

# 使用apply函数对每个元素进行操作
df['新列'] = df['已有列'].apply(lambda x: x * 2)  # 对每个元素进行运算，生成新列

# 基于条件为新列赋值
df['新列'] = np.where(df['列名'] > 10, '大于10', '小于等于10')  # 根据条件为列赋值

# 重置索引
df = df.reset_index(drop=True)  # 重置索引，丢弃旧索引
```

`apply()` 用于对列中每个元素应用函数，通常用于自定义的逐行运算。

`np.where()` 是 NumPy 提供的条件运算函数，可以根据条件返回不同的值，常用于快速生成新列。

`.reset_index()` 将数据框的索引重置为默认的整型索引，并可以选择是否丢弃旧索引。

**7. 统计与计算**

```py
# 计算最大值、最小值、平均值等
df.max()        # 每列最大值
df.idxmax()     # 每列最大值对应的索引
df.min()        # 每列最小值
df.mean(axis=1) # 每行平均值 (axis=1表示按行计算)

# 计数
df.value_counts()  # 返回每个唯一值的计数
df.nunique()       # 返回每列唯一值的数量

# 统计唯一值
df.unique()  # 返回某列的唯一值
```

`.max()` 和 `.min()` 返回每列的最大值和最小值，适用于数值型列。

`idxmax()` 返回每列最大值所在行的索引，适合定位特定值的位置。

`.mean()` 计算每行或每列的平均值，`axis=1` 表示按行计算，`axis=0` 表示按列计算。

`.value_counts()` 用于统计某列每个唯一值的出现次数，适合分析分类数据。

`.nunique()` 返回每列中的唯一值数量，适合分析数据的唯一性。

`.unique()` 返回某列中不重复的值列表。

**8. 数据分组与聚合**

```py
# 按某列分组并计算聚合值
df_grouped = df.groupby('列名').agg({'另一列': 'sum'})  # 按某列分组，并对另一列求和
```

`.groupby()` 用于按某一列分组，通常与 `.agg()` 或 `.apply()` 配合使用进行数据聚合操作。

`agg()` 可以传递多个聚合函数，如 `sum()`、`mean()`、`count()`，灵活处理分组后的数据。

**9. 排序与合并**

```py
# 按列值排序
df = df.sort_values(by='列名', ascending=False)  # 按指定列进行降序排序

# 合并两个数据框
df_merged = pd.merge(df1, df2, on='共同列名', how='inner')  # 根据共同列进行内连接

# 拼接数据框
df_concat = pd.concat([df1, df2], axis=0)  # 按行拼接（纵向）
df_concat = pd.concat([df1, df2], axis=1)  # 按列拼接（横向）
```

`.sort_values()` 用于对数据框按某一列排序，`ascending=False` 表示降序排列。

`pd.merge()` 是合并两个数据框的常用方法，`on` 参数指定共同列，`how='inner'` 表示内连接，left 和 right 表示外连接。

`pd.concat()` 用于拼接多个数据框，`axis=0` 表示纵向拼接，`axis=1` 表示横向拼接。

**10. 数据透视与整理**

```py
# 透视表操作
df_pivot = df.pivot(index='行索引', columns='列索引', values='要展示的值')  # 将长格式数据转换为宽格式

# 重命名列
df = df.rename(columns={'旧列名': '新列名'})  # 重命名数据框的列
```

`.pivot()` 用于数据透视，将长格式的数据转换为宽格式。`index` 表示行索引，`columns` 表示列索引，`values` 表示要展示的值。

`.rename()` 用于重命名数据框的列，传递字典格式，如 {'旧列名': '新列名'}。

**11. 数据可视化**

```py
# 使用Altair进行数据可视化
import altair as alt
alt.Chart(df).mark_bar().encode(x='列名', y='列名')  # 使用Altair绘制条形图
```

altair 是基于 Vega-Lite 的声明式数据可视化库。`mark_bar()` 用于绘制条形图，`encode()` 函数指定图表的 x 轴和 y 轴。

**12. Python基本运算**

```py
# 基本运算
a = 5
b = 3
result = a + b  # 加法运算

# 布尔运算
logical_result = a > b  # 判断是否大于
```

`.sum()` 是加法运算符，`>` 是用于判断两个值之间的大小关系的布尔运算符。

**13. 运算符**

| 符号    | function                    |
| ------- | --------------------------- |
| `a & b` | and                         |
| `a | b` | or                          |
| `a ^ b` | either a or b, but not both |

