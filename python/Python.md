# Python

## 

## 简介

定位: 一门解释型的高级语言

特点: 简单, 优雅, 可移植性, 代码规范性, 胶水语言

应用领域: Web全栈开发, 图形界面开发, 大数据, 人工智能, 爬虫, 系统网络运维, 云计算系统管理等

版本: 流行版本是 Python3.x 和 Python2.x

解释器: 作用是将源码转换为二进制代码进行运行



## python程序的编译和执行

#### 环境

方式1: Python的交互模式下直接编写

方式2: 使用任意的文本编辑器, 进行编写代码文件

方式3: Python官方提供的 IDLE 工具

**方式4(常用)**

IDE 集成开发环境

特点: 把开发相关的各种环境和工具集成到一起

包括: 项目的组织管理, 编辑, 提示, 运行, 调试, 辅助工具, 代码规范( PEP8 标准)等

常见的 Python IDE: Pycharm, PyScriper, Eclipse with PyDev, Emacs等

#### 过程

图解

<img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20230425161313753.png" alt="image-20230425161313753" style="zoom: 33%;" />

**注意**

严格来说 Python 是先编译成字节码, 然后再解释执行的一门语言

`.pyc` 文件的主要作用是持久化编译结果, 提升下次的执行效率, 而会不会被持久化, 一般是根据 `import` 机制, 也可以通过命令手动编译&持久化, 以 `test.py` 文件为例, 代码是 `python -m py_compile test.py`, 这样就会生成 `test.pyc` 文件, 但要注意的是, 但我们再次运行 `test.py` 文件时, 并不会去执行刚才自己通过命令生成的 `test.pyc` , 可以理解为它本身不是一个被引用文件, 只有被 `import` 的文件, 才会在每次引用运行时编译其 `.pyc` 文件

`.py` 和 `.pyc` 文件都可以直接交给解释器直接处理, 只不过处理的步骤有些差别. 



## 基础编程

#### 注释

**单行注释** `#xxx`

**多行注释** `'''xxx'''` 或者 `"""xxx"""` 

**特殊注释** 

`#!/usr/bin/python` 

Linux 系统下用于增加一种运行模式, 更好的写法是 `#!/usr/bin/env python` , 它更加灵活, 因为它指明的是虚拟环境里的 python 路径, 而不是一个绝对的死路径. 

`#encoding=utf-8`  

解决的是中文支持问题, 对于非 ACSII 编码的中文, python3 直接支持, 但是 python2 默认不支持, 需在源文件顶部添加代码行 `#encoding=utf-8` 或者 `coding=utf-8` , 而推荐的最正规的官方写法则是 `# _*_coding:utf-8_*_` , 当然了, python3 默认支持中文, 所以不必写这句话. 



#### 变量

定义: 是一个存储数据的容器, 变量引用着某个具体数值, 并且可以改变这个引用. 

定义变量

```
a = 6
a, b = 6, 7
a = b = 7
name = "hhha"
```

命名规范

1. 必须只能由字母数字下划线组成, 数字不能在最前面
2. 驼峰标识, 即驼峰命名法, 函数名中的每一个逻辑断点都有一个大写字母来标记, 如  `phoneNumber` , 首个单词的首字母若大写则为大驼峰法, 小写则为小驼峰法; 还有另一种命名法叫下划线法, 函数名中的每一个逻辑断点都有一个下划线来标记, 如 `phone_number` 
3. 非关键字

注意: 变量名使用之前要先赋值



#### 数据类型

**常用数据类型**

Numbers (数值类型): int (二进制, 八进制, 十进制, 十六进制), long, float, complex 

Bool (布尔类型): True, Flase

String (字符串): `'abc'`, `"abc"`, `'''abc'''`, `"""abc"""` (三个引号, 赋值情况下才是字符串, 否则就是注释)

List (列表), Set (集合), Tuple(元组),  Dictory (字典), NoneType (空类型). 

**查看数据类型**: `type()`

```python
print(type(6))

result = type("8")
print(result)

# output
<class 'int'>
<class 'str'>
```

**数据类型转换**

常用于输入时, 无法控制数据类型

```py
score = input("请输入一个数字")
print(type(score))
print(int(score) + 6)

#input
5
#output
请输入一个数字
<class 'str'>
11
```

注意:

有时候数据类型转换无法实现

```py
ret = "123a"
print(int(ret))

#报错
Exception has occurred: ValueError
invalid literal for int() with base 10: '123a'
```

也并非所有的数据类型都能进行相互转换

**数据类型转换图**

<img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20230427001942350.png" alt="image-20230427001942350" style="zoom:50%;" />

**动态类型/静态类型**

静态类型: 类型是编译的时候确定的, 后期无法修改, 如 C++

```C++
int ret = 6;
ret = "hhh"  //error
```

动态类型: 类型是运行时进行判定的, 可以动态修改, 如 python

```python
ret = 6
ret = "hhh"
```

**强类型/弱类型**

强类型: 类型比较强势, 不轻易随着环境的变化而变化

弱类型: 类型比较柔和, 不同的环境下, 容易被改变

**Python属于强类型的, 动态类型的语言**



#### 运算符

**算术运算符**

加法运算符 `+` 

```
print(1 + 2)
print('1' + '2')
print([1, 2] + [3, 4])
```

减法运算符 `-`

乘法运算符 `*`

幂运算符 `**`

```
print(3 ** 4)
```

除法运算符 `/`

```py
print(5 / 2)
#output
2.5

print(5 / 0)
#error
Exception has occurred: ZeroDivisionError
division by zero
```

整除运算符 `//`

```py
print(5 // 2)
print(5.2 // 2) #5.2 / 2 = 2.6 直接取整数部分, 而不是四舍五入
#ouput
2
2.0  
```

求模运算符 `%`

赋值运算符 `=`

**注意**
