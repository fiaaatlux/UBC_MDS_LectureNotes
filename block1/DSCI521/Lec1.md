# Bash

**1. Bash 基础命令**

```
ls -a -l  # 显示全部文件以list的形式
cd <directory_name>  # 切换到指定目录
pwd  # 显示当前的工作目录
```
`cd ..` 切换到上一级目录，`cd ~` 返回到用户的主目录

**2. Bash 文件操作**

```
touch <file_name>               # 创建文件

cat <file_name>                 # 查看文件
head <file_name>                # 查看文件前几行
tail <file_name>                # 查看文件最后几行
less <file_name>                # 分页查看文件内容

mkdir <directory_name>          # 创建新目录
mv <source_file> <destination>  # 移动或重命名文件

rm <file_name>                  # 删除指定文件
rm -r <directory_name>          # 递归删除目录及其内容
```

**3. 命令历史和帮助**

```
history           # 查看命令历史
man <command>     # 显示命令的手册页
<command> --help  # 显示命令的帮助信息
```

**4. 权限管理**

```
# 修改文件权限
chmod 755 <file_name>  # 授予文件所有者读取、写入和执行权限，其他人读取和执行权限

# 显示文件权限
ls -l  # 以详细列表形式显示文件权限
```

**5. Bash 变量与条件**

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

**6. Bash 循环**

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
