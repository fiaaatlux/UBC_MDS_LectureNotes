# 环境管理

```
# renv 的主要命令：
renv::init()：在当前项目目录下创建一个新的虚拟环境
install.packages("package_name")
remove.packages("package_name")
renv::snapshot()：保存或导出环境到文件（如 renv.lock），可以通过 install.packages() 和 remove.packages() 管理包。
每当你移除或安装包后，建议使用 renv::snapshot() 来更新项目的环境快照，以确保项目的依赖关系保持最新状态
renv::restore()：从 renv.lock 文件中恢复环境
```

```bash
project/
├── data/              # 存放数据
│   ├── processed/     # 已处理的数据
│   └── raw/           # 原始数据
├── reports/           # 报告文件 (.ipynb 或 .Rmd)
├── src/               # 源代码 (.py 或 .R)
├── doc/               # 文档
├── README.md          # 项目说明文件
└── environment.yaml   # 环境设置文件（或者 renv.lock）
```

```python
conda --version
conda create -n dsci521 python=3.12 pandas jupyterlab

# sklearn & conda-forge
conda install -c conda-forge scikit-learn
conda install -c conda-forge art

# 激活环境
conda env list
conda activate my_env

# 删除环境
conda deactivate
conda remove -n dsci521 --all

# 导出&重建环境
conda env export -f environment.yaml
conda env create -f environment.yaml
```

