# DSCI 511

**0.基本概念**

```python
axis=0 指的是纵向操作(针对每一列所有指定行)
axis=1 指的是横向操作(针对每一行所有指定列)
```

**1. 读写数据**

```python
# 读csv
df = pd.read_csv('data.csv', sep='\t', index_col=0, skiprows=3, header=None, parse_dates=True)

# 读excel
df = pd.read_excel('data.xlsx', sheet_name='sheet1')

# 读txt纯文本(非表格格式)
with open('data/test_emails.txt', 'r') as file:
    email_text = file.read()

# 写csv
df.to_csv('data.csv', index=False)
```

当`parse_dates=True` 时，pandas会尝试自动解析数据中的日期列；`parse_dates=[column_list]` 指定特定列解析为日期时间格式 `datetime64[ns]` 类型；`parse_dates=[['col1', 'col2']]` 可将多个列组合为一个日期列。

**2. 查看DataFrame基本信息**

```python
df.head(3)  # 显示前3行
df.tail()   # 显示后5行（默认）

df.describe()  # 仅对数值列生效, 提供每个数值列的统计信息 (如平均值、标准差等)
df.shape  # 返回(行数, 列数)

df.columns.to_list()  # 返回列名作为列表
df.index.to_list()  # 返回index作为列表
```

**3. DataFrame增删改查**

```python
df_deep = df.copy() # 默认就是deep=True, 修改df不会改变df_deep, 如果是False修改df嵌套对象则复制的df也会改

# 新增列
df['new_col'] = df['old_col'] * 2 # 添加列
df['new_col'] = df['old_col'].apply(lambda x: x * 2)  # 使用apply对每个元素进行操作，生成新列
df['new_col'] = np.where(df['old_col'] > 10, '大于10', '小于等于10')  # 基于条件为新列赋值

df = df.drop(columns='col', axis=1) # 删除列

# 操作索引
df.sort_index()  # 按索引排序
df.set_index('col', inplace=True) # 设置索引; inplace表示进行原地操作
df = df.reset_index(drop=True)  # 重置索引，drop可以选择是否丢弃旧索引

# 操作列名
df = df.rename(columns={'old_col': 'new_col'})  # 重命名特定列
df.columns = ['new_name1', 'new_name2', ...]  # 重命名所有列

# 计数
df.col.unique() # 返回唯一值列表
df.nunique() # 返回唯一值的数量
df.col.value_counts()  # 每个唯一值出现的次数

df = df.sort_values(['col1', 'col2'], ascending=[True, False])  # 排序，可以按多列
```

**4. 缺失值处理**

```python
# 检查整张表是否有缺失值
any(df.isna())
df.isnull().sum()

# 遍历df每一行，检查指定列是否有为空的值
df[df.apply(lambda row: any(row[col] == '' for col in df.columns), axis=1)]

# 缺失值补全或删除
df.fillna(0) # 用指定值填充；或者也可以method='ffill'用前一个有效值填充，method='bfill'用后一个有效值填充
df.dropna() # 删除有缺失值的行

# 给指定列空值位置赋值
df['col'] = np.where(df['col'] == '', 'new_value', df['col'])
df['col'] = df['col'].map({'old_value': 'new_value'})  # 使用映射替换值
```

**5. 数据类型转换**

```python
df.dtypes # 返回每列的数据类型
df['col'] = df['col'].astype('int64') # 该列转换为整数类型
df['class'] = df['class'].astype('category')  # 将列转换为分类类型，节省内存

# 使用
df['class'].cat.categories

# 字典举例
carrier_names = {
    'AA': 'American Airlines',
    'US': 'US Airways'
}
df['carrier'] = df['carrier'].map(carrier_names) # 替换为字典的值
```

**6. 计算**

```python
# 最大值、最小值、平均值等
df.max() | df.min() # 每列最大/最小值
df.idxmax() | df.idxmin() # 每列最大/最小值对应的索引
df.col.mean() # 求指定列均值
df.mean(axis=1) # 每行平均值

# groupby指定列，求另一列的均值
df.groupby(['col1', 'col2']).agg({'col3':'mean'}) # 如果要by index的话，需要先.reset_index()

# 遍历DataFrame计算
df = df.apply(np.sum, axis=0)  # 每列总和，axis=0，纵向操作
df = df.apply(lambda x: x - x.mean(), axis=1) # 横向操作；每一行每个数值分别减去该行的均值
df = df[list(df.columns)].apply(lambda x:x - x.mean()) # 默认axis=0，纵向操作；每一列每个数值分别减去该列的均值
```

`agg()` 可以传递多个聚合函数，如 `sum()`、`mean()`、`count()`

**7. Reshape DataFrame**

```python
# 列转行
df = df.reset_index().melt(
  	id_vars=['index', 'col2'], # 指定保持不变的列
  	var_name='variable', # 新列名，用于存储原来的列名
  	value_name='value' # 新列名，用于存储值
).rename(columns={'index':'dt'}).set_index('dt') # 重命名列并指定为索引

# 行转列
df = df.pivot(
    index='index_col', # 指定作为新df行索引的列
    columns='column_to_pivot', # 指定要转换的列
    values='value_column' # 指定作为填充值的列
)

# 另一种是pivot_table; pivot要求索引/列组合是唯一的, 而pivot_table可以处理重复的索引/列组合，因为它可以执行聚合操作
df = df.pivot_table(
    index='index_col',
    columns='column_to_pivot',
    values='value_column',
    aggfunc='mean' # 或其他聚合函数，如sum, median
)

# 转置
df.transpose()  # 或df.T，行列对调

# 合并DataFrame(相当于join)
df_merged = pd.merge(df1, df2, on='共同列名', how='inner')  # 根据共同列进行内连接
# 拼接DataFrame(相当于append)
df_concat = pd.concat([df1, df2], axis=0)  # axis=0 纵向拼接，axis=1 横向拼接
```

**8. 时间日期处理**

```python
# 创建时间戳和日期范围
timestamp = pd.Timestamp('2023-01-01 12:00:00')
dt_range = pd.date_range(start='2023-01-01', end='2023-12-31', freq='D') # freq='D'表示by天
dt_range = pd.period_range(start='2023Q1', end='2023Q4', freq='Q') # freq='Q'表示按季度

# 转日期格式
df['date'] = pd.to_datetime(df['date'], format='%m/%d/%y') # String转日期 '12/13/20' => '2020-12-13'
df.to_period('M') # DatetimeIndex转换为PeriodIndex 2020-12-13 => 2020-12
df.to_timestamp() # 转DatetimeIndex() 2020-12 => 2020-12-01 

# 重新采样
df.resample('MS') # 2020-12-13 => 2020-12-01
df[['col1', 'col2']].resample('1D') # 按天resample

# 移动窗口计算
df.rolling(window=7).mean()  # 7天移动平均
df.expanding().sum()  # 累计总和

# 提取&选择日期
df.index.year # 获取年份；月份(month),日(day),星期几(weekday)0=周一，6=周日,季度(quarter)

# 选择时间范围内数据
df['2023-01-01':'2023-12-31']  # 特定日期范围数据
df.between_time('09:00', '17:00')  # 特定时间范围数据
```

在`df.resample` 中，`MS` 月首日；`ME` 月末日；`W` 周(礼拜天开始)；`W-MON` 周(礼拜一开始)；`QS` 季度首日；`Q` 季度末日

`.week()`, `.day_name()`

**9. 字符串处理**

```python
# 字符串方法可以通过 .str 访问器应用于整个Series
df['col'].str.lower() # 转换为小写;大写(upper)
df['col'].str.strip() # 去除首尾空白;或者前缀.lstrip('prefix_') 后缀.rstrip('_suffix')
df['col'].str.replace('old', 'new') # 替换字符串
df['col'].str.contains('pattern') # 检查是否包含特定字符
df[['col1', 'col2']] = df['col'].str.split('_', expand=True) # 分割字符串by逗号
df['col'].str.len() # 计算字符串长度

# 正则表达式
df['col'].str.extract(r'([A-Za-z0-9.-]+)') # 提取字母数字小数点连字符，+表示匹配前面的字符类一次或多次
df['col'].str.findall(r'\b\w{6}\b')   # 查找6个字符的单词
```

**10. 数据查询**

```python
# 选择列
df['col'] # 选择单列，返回一个Series对象
df[['col1', 'col2']]  # 选择多列，返回一个新的DataFrame
df[df['列名'] == '条件']  # 基于条件筛选行

# 按行索引选择数据
df.loc[[0]]  # 返回索引为0的行 (用loc按索引值选择行)
df.iloc[[0]] # 用iloc按行号选择数据

# 按行号和列名选择数据
df.loc[0:1, 'col1':'col2']  # loc按列名和index选择数据
df.iloc[0:1, 0:3]  # iloc按行号和列号选择数据

# 用query进行复杂过滤
df.query('(col1 > 5) & (col2 < 10) | (col3 == "value")')
```

**11. 可视化**

a. 用Matplotlib

```python
import matplotlib.pyplot as plt
plt.figure(figsize=(10, 6))
plt.plot(df.index, df['column'])
plt.title('Title')
plt.xlabel('X Label')
plt.ylabel('Y Label')
plt.show()
```

b. 用Altair

```python
import altair as alt
chart = alt.Chart(df).mark_point().encode(
    x='column1',
    y='column2',
    color='category_column'
).interactive()
chart.show()
```

