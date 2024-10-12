```python
概念: pd.Series对象中的元素实际上在内存中被表示为一个ndarray,Series有索引可用标签访问 ndarray没有,只能用数字索引访问 | pd.Series(my_arr)  my_series.to_numpy() 可互相转
创建: np.array([[1,2],[3,4]]) | np.full((3,1,2), 4) 3x1x2填充数为4 | np.arange(0,6,1) 1维数组5行0列,间隔为1,可用.reshape(1,5)转1行5列 | np.zeros或np.ones((3,3), dtype=int) 2维数组,3x3矩阵 | numpy.linspace(0,10,5,dtype=int,axis=0) 5个0-10的等间距数值,默认endpoint=True含末尾,可加restep=True返回步长
随机数组: np.random.rand(5) 5个0-1的随机数的数组, np.random.rand(3,3) 3x3随机数矩阵, np.random.rand(2,3,4) 2x3x4随机数数组 | 3d数组: 3x3cube cube[0,:,2]指0行所有列2层
运算: np.sum(my_arr) np.mean() np.min() np.max() np.log() | my_arr[my_arr>0] 筛选>0的值, my_arr[my_arr<0]=np.nan 给负数赋值为nan | .dtype .size .ndim
Reshape: my_arr.transpose() | my_arr.reshape() | np.ravel(my_arr) 返回视图 my_arr.flatten() 返回副本 都是改1维
heterogenous(异构数组): a=np.array([['a','b','c'],1,3.14],dtype='object') 查看类型 list(map(type,a))
```

```python
数据类型: int float bool str list,[],可变,有序,不唯一 tuple,(),不可变,有序,不唯一 set{},无序,唯一 dict{'key':value} 键值唯一 NoneType | type() 查看变量类型
比较: ==比较内容 is比较内存地址 | 0.1+0.2不等于0.3,要用np.isclose(a,b)比较 | 转换 int(),float(),str() | +,-,*,/,//,%,** 运算 | and or not != 运算符
布尔值判断: False,None,0,0.0,"",[],(),{} 这些为False, 其他所有值都为True
字符串: .lower(),.upper(),.strip(),.replace(),.contains(),.split(),.join() | df['col'].str.xxx 操作Series,split参数expand=True分列 | f'age is {age:.2f}'
列表: .append(),.insert(),.remove('a') 或者 .pop(1),.sort(),.reverse() | [x**2 for x in range(5)]
字典: .get(),.pop(),.items(),.keys(),.values(),.clear() | {key: len(key) for key in ['apple', 'banana', 'cherry']}
集合: .add(),.remove(),.union(),.intersection(),.difference() | {word[0] for word in ['apple', 'banana', 'cherry']}
for i in range(start,stop,step): | while n<5: ...n+=1 | for index,value in enumerate(mylist): | for i,j in zip(ls1,ls2) | for key,value in my_dict.items(): 
```

```python
def add(*args): 
  try: 
  	return sum(args) 
	except TypeError: 
    print('Type error')
  except: 
    pass # 什么都不做 
  	print('other error') 
def mytest():
  assert isinstance(area(1), float), 'test failed'
  print('test passed')
def add(**kwargs): return mean(kwargs.values())
```

```python
class Animal:
    species = "Animal"  # 类属性，所有实例共享
    def __init__(self, name: int, age: int = 0):
        self.name = name  # 实例属性，表示动物的名字
        self.age = age  # 这里如果self._age就是私有 改属性需要setter和getter
		# def _read_data(self) -> pd.DataFrame: return get_massive_data(self.languages, self.split) 比如这样
    def speak(self):
        return f"{self.name} makes a sound."  # 普通方法，返回动物发出的声音
    @classmethod
    def describe_species(cls):
        return f"This is a {cls.species}."  # 类方法，描述当前类的种类
    @staticmethod
    def average_age(ages) -> float: # 静态方法，计算一组年龄的平均值
        return sum(ages) / len(ages)
    def __str__(self):
        return f"{self.name}, {self.age} years old"  # 魔法方法，定义对象的字符串表示
class Dog(Animal):
    species = "Dog"  # 子类重写父类的类属性
    def __init__(self, name, age, breed):
        super().__init__(name, age)  # 调用父类的构造函数
        self.breed = breed  # 子类独有的属性，表示狗的品种
    def speak(self):
        return f"{self.name} barks."  # 重写父类的 speak 方法，狗的叫声是“barks”
    def fetch(self, item):
        return f"{self.name} fetches the {item}."  # 定义新的方法，狗叼回物品
    def __eq__(self, other): # 魔法方法，定义两个狗对象是否相等
        if not isinstance(other, Animal):
            return False
        return self.name == other.name and self.breed == other.breed
animal = Animal("Generic Animal", 5)
animal | animal.speak() | Animal.describe_species() | Animal.average_age([5, 7, 3]) | animal.age = 7 设置年龄
dog = Dog("Atlas", 3, "German Shepherd")
dog | dog.speak() | Dog.describe_species() | dog.fetch("ball")
```

```python
PEP8变量,函数,模块名使用snake_case, 类名使用CamelCase, 每行代码不超过 79 个字符。
Linter: 检查代码中的编程错误和样式问题,例如 flake8; 格式化工具: 自动重构代码样式,例如 black | flake8 <文件路径> black <文件路径> --check
```

