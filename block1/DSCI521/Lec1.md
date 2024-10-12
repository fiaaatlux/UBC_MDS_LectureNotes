# Lecture 1 - Bash

#### **1. Bash 基础命令**

```
# 列出目录内容
ls  # 显示当前目录中的文件和文件夹

# 改变当前目录
cd <directory_name>  # 切换到指定目录

# 查看文件内容
cat <file_name>  # 显示文件的内容

# 显示当前目录路径
pwd  # 显示当前的工作目录
```

`ls` 用于列出当前目录的文件和文件夹，`cd` 改变当前目录，`pwd` 显示当前的工作路径。

#### **2. Bash 文件操作**

```
# 创建新文件
touch <file_name>  # 创建一个空文件

# 创建新目录
mkdir <directory_name>  # 创建新目录

# 移动或重命名文件
mv <source_file> <destination>  # 移动或重命名文件

# 删除文件或目录
rm <file_name>  # 删除指定文件
rm -r <directory_name>  # 递归删除目录及其内容
```

`touch` 用于创建空文件，`mkdir` 创建新目录，`mv` 移动或重命名文件，`rm -r` 删除整个目录及其内容。

#### **3. 目录管理**

```
# 切换到上一级目录
cd ..  # 返回上一级目录

# 切换到用户的主目录
cd ~  # 进入用户的主目录
```

使用 `cd ..` 切换到上一级目录，`cd ~` 返回到用户的主目录。

#### **4. 权限管理**

```
# 修改文件权限
chmod 755 <file_name>  # 授予文件所有者读取、写入和执行权限，其他人读取和执行权限

# 显示文件权限
ls -l  # 以详细列表形式显示文件权限
```

`chmod` 用于修改文件或目录的权限，`ls -l` 以详细列表显示文件的权限设置。

#### **5. Bash 变量与条件**

```
# 定义变量
name="John"  # 变量赋值
echo $name  # 输出变量的值

# 条件判断
if [ -f "file.txt" ]; then
  echo "文件存在"
else
  echo "文件不存在"
fi
```

`$name` 用于引用变量值，`if` 条件语句判断文件是否存在或满足其他条件。

#### **6. Bash 循环**

```
# for 循环
for i in {1..5}; do
  echo "循环 $i"
done

# while 循环
counter=1
while [ $counter -le 5 ]; do
  echo "计数器: $counter"
  ((counter++))
done
```

`for` 循环遍历数字范围或列表，`while` 循环直到条件不成立。
