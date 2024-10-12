Virtual environments allow different versions of packages and libraries to **coexist** on the same machine, ensuring **no conflicts** between projects.

The importance of virtual environments lies in **reproducibility**, ensuring that code runs consistently across different systems when sharing projects.

**Conda** is an open-source package and environment management system, widely used in the Python community.

```bash
conda --version
conda create -n my_env python=3.12 pandas jupyterlab
conda env list
conda activate my_env
conda deactivate
conda remove -n dsci521 --all # 删除环境
conda env export -f environment.yml # 导出当前环境到文件
conda env create -f environment.yml # 从 YAML 文件创建环境
```





Hmmmm



What else should I write....



Well, 



Good Luck ！



