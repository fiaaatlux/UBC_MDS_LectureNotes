**运算符**

| 符号    | function                    |
| ------- | --------------------------- |
| `a & b` | and                         |
| `a | b` | or                          |
| `a ^ b` | either a or b, but not both |

**缺失值处理**

```python
# check if there is at least one NaN value in the DataFrame
any(languages.isna())

# Or check just a specific column
any(languages['family'].isna())

# drop NA
languages.dropna()

# fill NA
languages.fillna('No source')
```

