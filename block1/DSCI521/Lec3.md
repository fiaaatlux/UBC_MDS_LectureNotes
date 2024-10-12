# Quarto

**1. 创建 Quarto 项目**

```bash
quarto create project website  # 创建新的 Quarto 网站项目
```

**2. 渲染 Quarto 文档**

```bash
quarto preview            # 预览 Quarto 项目并实时更新
quarto render             # 渲染 Quarto 项目
quarto publish
```

**3. Quarto YAML 配置**

```yaml
project:
  type: website
output-dir: docs  # 渲染文件的输出目录
```

**4. 其他功能**

```bash
quarto render filename.ipynb --to pdf
quarto render filename.rmd --to md
```