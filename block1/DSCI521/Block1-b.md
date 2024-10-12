# DSCI 521

**1. R studio**

```R
getwd() # 获取当前路径
setwd() # 设置路径

```









```python
conda create -n dsci521 python=3.12 pandas



# sklearn & conda-forge
conda install -c conda-forge scikit-learn
conda install -c conda-forge art




# 导出环境
conda env export > environment.yaml

# 删除环境
conda deactivate
conda remove -n dsci521 --all

# 重建环境based on yaml file
conda env create -f environment.yaml




conda install scikit-learn


from sklearn.linear_model import LinearRegression
# 准备数据
X = np.array([[1], [2], [3], [4]])  # 形状为 (4, 1)，4 个样本，每个样本 1 个特征
y = np.array([3, 5, 7, 9])  # 目标变量，形状为 (4,)

model = LinearRegression()
model.fit(X, y)

y_pred = model.predict([[5]])
print(y_pred)
```

