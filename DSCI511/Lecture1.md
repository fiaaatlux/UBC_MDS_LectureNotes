# Lecture 1

**0. Basic setting & packages**

```py
conda install pandas
import pandas as pd
pd.set_option('display.max_rows', 6) # 设置jupyter notebook最多展示行数
```

**1. Read data**

```python
# csv, tsv, txt
df = pd.read_csv('data/imdb.csv', sep='\t', skiprows=6, index_col='iso_code')

url = 'https://github.com/ttimbers/master/dataset.xlsx?raw=true'
df = pd.read_csv(url, header=None, names=['a', 'b', 'c'])
```

读本地文件写本地路径, url写链接

文本文件, `sep=\t` 表示分隔符是Tab, `skiprows=6` 表示不读取文件1-6行, `header=None` 表示没有列名, 后面通过`names` 指定列名; 另外比如`header=2` 则表示列名在文件的第3行(如果前面有空行的话是不算在内的); `index_col='region'` 表示指定region那列作为index

```py
# excel
df = pd.read_excel('data/abbotsford_lang.xlsx', sheet_name=2)
```

Excel文件, `sheet_name=2` 表示读excel的第二个sheet, 也可以写sheet的名字, 比如`sheet_name='data'`

除了最常用的这两个以外, pandas还能读各种不同类型的数据, 比如 `pd.read_html()`, `pd.read_json()`, and `pd.read_sql()` 等等...

**2. Examine a DataFrame**

```py
df.head(3) # 展示前3行
df.tail() # 没指定parameter所以展示后5行
df.describe() # 返回basic stats, 仅对numeric类型的列生效
df.shape # 返回行数和列数, 比如20行9列(20, 9)
df.columns.to_list() # 返回list类型的列名
```

**3. Access values from a DataFrame**

```py
# 选列
df['region'] # 返回pandas series, 数据是region这一列

# 选行
df[df.index == 0] # 返回DataFrame, 数据是index为0的那行(第1行)
df.loc[[0]] # 效果同上, 这里的0指的是index为0
df.iloc[[0]] # 效果同上, 这里的0指的是第0行
# 如果要选最后一行
df.loc[[df.index[-1]]] # loc的话得这样写
df.iloc[[-1]] # 而iloc可以直接用-1表示取最后一行

df.loc[0] # 还是第1行, 但返回的是pandas series
df.iloc[0] # 同上

# 按指定行列返回df中某个位置的具体值
df[df.index == 32]['region'] # 返回第33行region那列的值
df.loc[32, 'region'] # 同上
df.iloc[32, 0] # 同上, 但iloc只能填第几列, 不支持用列名
```

这里注意⚠️: `loc[]` 里写的是index和列名, 而`iloc` 里写的是第几行和第几列

**4. Subsetting a DataFrame**

筛选特定行, 特定列

```py
# filter的功能, 选择符合条件的特定行
df[df['region'] == 'Vancouver']
df[df.region == 'Vancouver']

# 选择符合条件的行和列
df.loc[0:1, 'region':'area'] # 返回从index0-index1的行(1-2行), 从region到area列(1-3列)
df.iloc[0:1, 0:3] # 同上
```



**5. Modify a DataFrame**

```py
# 创建新列

# 删除列
```



**6. 计算**

```py
df.value_counts()
df.unique()
df.nunique()
```



**7. 排序**

```py
df.sort_values()
```

**8. Write a DataFrame to file**

```py
df.to_csv('my_data.csv')
```



