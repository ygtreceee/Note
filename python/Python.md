# Python



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

1. 常用数据类型

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

2. 数据类型转换

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

当 int 和 float 类型进行算数运算时, 结果会被提升为 float 类型

**数据类型转换图**

<img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20230427001942350.png" alt="image-20230427001942350" style="zoom:50%;" />

3. 动态类型/静态类型

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

4. 强类型/弱类型

强类型: 类型比较强势, 不轻易随着环境的变化而变化

弱类型: 类型比较柔和, 不同的环境下, 容易被改变

**Python属于强类型的, 动态类型的语言**



#### 运算符

1. 算术运算符

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

2. 复合运算符

```
*=   /=   //=   **=  -=   +=   %=
```

3. 比较运算符

```
>   <    != (在python2.x中也可写作<>)    >=    <=    ==
```

对比唯一标识: `is`

```python
a = 9
b = 9
print(id(a))
print(id(b))
print(id(a) == id(b))
print(a is b)
print(id(a) is id(b))

#output
3128375116272
3128375116272
True
True
False


a = [9]
b = [9]
print(id(a))
print(id(b))
print(id(a) == id(b))
print(a is b)
print(id(a) is id(b))

#output
1936594819520
1936594820736
False
False
False
```

4. 链状比较运算符

python 允许链式比较

```python
num = 5
print(3 < num < 20)
print(8 < num < 20)

#output
True
False
```

5. 逻辑运算符

`not`  `and`  `or` 

注意

非布尔类型的值, 如果作为真假来判定, 一般都是**非零即真, 非空即真**

```python
print(bool("0"))
print(bool(""))
print(bool(1))
print(bool(-1))
print(bool(0))

# output
True
False
True
True
False
```

整个逻辑表达式的值不一定是 True 或 False, 是根据最终能确定表达式值的位置的值来输出的

```python
print(0 or 1)
print(False or 1)
print(True or 0)
print(3 and 2)
print(3 or 2)
print(0 or False or 3)

# output
1
1
True
2
3
3
```



#### 输入和输出

1. 输入

**Python2**

 `raw_input` 

格式: `result = raw_input("提示信息")`

功能: 会等待用户输入内容, 直至用户按下  Enter ; 会将用户输入的内容当作字符串, 传递给接收的变量

```python
p1 = raw_input("Please input: ")
p2 = raw_input("Please input: ")
p3 = raw_input("Please input: ")
print(type(p1))
print(type(p2))
print(type(p3))
print(p1)
print(p2)
print(p3)

#output
Please input: 123
Please input: abc
Please input: 1+1
<type 'str'>
<type 'str'>
<type 'str'>
123
abc
1+1
```

`input`

格式: `result = input("提示信息")`

功能: 会等待用户输入内容, 直到用户按下 Enter; 会将用户输入的内容当作"代码"处理!

```python
p = input("Please input: ")
print(type(p1))
print(p1)

#output
Please input: 123
<type 'int'>
123


p = input("Please input: ")
print(type(p1))
print(p1)

#output
Please input: abc
NameError: name 'abc' is not defined

#出错原因是因为输入的内容被当作代码原封不动的取代input的位置的内容, 即p = abc, 必然出错


p = input("Please input: ")
print(type(p1))
print(p1)

#output
Please input: 1+1
<type 'int'>
2
```

可理解为 input 函数是 raw_input 和 eval 的结合

`eval`: 对用户输入的字符串进行处理, 将字符串内容处理成代码

```python
#input = raw_input + eval

p = "1 + 1"
result = eval(p)
#result = 1 + 1
print(type(result))
print(result)

#output
<type 'int'>
2


p = raw_input("Please input: ")
result = eval(p)
print(type(result))
print(result)

#output
Please input: 123
<type 'int'>
123


p = raw_input("Please input: ")
result = eval(p)
print(type(result))
print(result)

#output
Please input: abc
NameError: name 'abc' is not defined
```



**Python3**

`input`

相当于 Python2 中的 raw_input, 如果要实现类似于 Python2 中 input 的功能, 可以再使用 eval 函数

```python
p = input("Please input: ")
result = eval(p)
print(type(p))
print(type(result))
print(p)
print(result)

#output
Please input: 1+1
<class 'str'>
<class 'int'>
1+1
2


num1 = eval("123")
num2 = eval("123.5")
# num1 = int("123")    #若要用int()转换, 则要保证字符串里面是个整数格式的数字, 否则会报错, float()转换也一样
# num2 = float("123.5")
# Error: num3 = int("123.5")
print(type(num1))
print(type(num2))
print(num1)
print(num2)

#output
<class 'int'>
<class 'float'>
123
123.5
```

2. 输出

**Python2**

`print` **语句**

```
print xxx
```

**使用**

输出变量

```python
print 10
num = 10
print num
num2 = 44
print num, num2

#ouput
10
10
10 44
```

格式化输出

```python
name = "hhh"
age = 19
print "My name is %s, my age is %d"%(name, age)
print "My name is {0}, my age is {1}".format(name, age)

#output
My name is hhh, my age is 19
My name is hhh, my age is 19
```

输出到文件中

```python
f = open("test.txt", "w")
print >>f, "xxxxxx"
#or
print >>open("test.txt", "w"), "xxxxxx"
```

输出不自动换行

```python
print "1",
print "2",
print "3",

#output
1 2 3
```

输出各个数据并用分隔符分隔

```python
print "-".join(["a", "b", "c"])

#output
a-b-c
```



**Python3**

`print` **函数**

`print(values, sep, end, file, flush)`

```
values: 需要输出的值; 多个值, 使用","进行分割
sep: 分隔符; 多个值, 被输出出来之后, 值与值之间, 会添加指定的分隔符
end: 输出结束之后, 以指定的字符结束, 默认是换行'\n'
file: 表示输出的目标, 默认是标准的输出(控制台), 还可以是一个可写入的文件句柄	
flush: 表示立即输出的意思, 值为Bool类型, 从缓冲区读取内容到控制台立即输出
```

输出变量

```python
print(123)
num = 55
print(num)
num2 = 44
print(num, num2)

#output
123
55
55 44
```

格式化输出

```python
name = "hhh"
age = 19
print("My name is %s, my age is %d"%(name, age))  #可视为整个是一个字符串参数
print("My name is {0}, my age is {1}".format(name, age))

#output
My name is hhh, my age is 19
My name is hhh, my age is 19
```

输出到文件

```python
#输出到文件
f = open("text.txt", "w")
print("xxxxxxx", file=f)

#print默认输出到标准输出流
import sys
print("xxxxxx", file=sys.stdout)
```

输出不自动换行

```python
print("123", end='')
```

输出各个数据使用分隔符分隔

```python
print("1", "2", "3", sep='=')
```

`flush` 使用

```python
#以下代码实际效果在新版本无效, 3.6版本仍然可行
from time import sleep
#休眠5秒再输出内容
print("请输入账号: ", end='')
sleep(5)

#直接输出内容
print("请输入账号: ")
print("请输入账号: \n", end='')
print("请输入账号: ", end='', flush=True)
sleep(5)
```

**占位格式符**

格式

```
%[(name)][flags][width][.precision]typecode
使用[]包含的部分, 代表可选
```

`(name)` : 用于选择指定名称对应的值

```python
mathScore = 148
englishScore = 149
print("My math score is %d, Englihs score is %d" % (mathScore, englishScore))
print("My math score is %(ms)d, Englihs score is %(es)d" % ({"ms": mathScore, "es": englishScore}))

#output
My math score is 148, Englihs score is 149
My math score is 148, Englihs score is 149
```

`flags` : 空默认表示右对齐, `-` 表示左对齐, 

```py
# 默认表示右对齐
mathScore = 148
print("%10d" % mathScore)
# '-'表示左对齐
print("%-10d" % mathScore)
# ' '为一个空格, 表示在正数的左边填充一个空格, 从而与负数对齐
a = 10
b = -20
print("% d" % a)
print("% d" % b)
# '0'表示位数不够时, 用0填充
min = 5
sec = 8
print("%02d:%02d" % (min, sec))

#output
       148
148
 10
-20
05:08
```

`width` : 表示显示的宽度

```python
mathScore = 148
print("%10d" % mathScore)

#output
       148
```

`.precision` : 表示小数点后精度

```py
score = 140.4
print("%.2f" % score)

#output
140.40
```

`typeCode` : 

数值

```python
i/d  #将整数, 浮点数转换成十进制表示, 并将其格式化到指定位置
o    #将整数转换成八进制数表示, 并将其格式化到指定位置
x    #将整数转换成十六进制数表示, 并将其格式化到指定位置
e    #将整数, 浮点数转换成科学计数法表示, 并将其格式化到指定位置(小写e)
E    #将整数, 浮点数转换成科学计数法表示, 并将其格式化到指定位置(小写E)
F/f  #将整数, 浮点数转换成浮点数表示, 并将其格式化到指定位置(默认保留小数点后6位)
G/g  #自动调整整数, 浮点数为浮点型或科学计数法表示(超过6位数用科学计数法), 并将其格式化到指定位置(如果是科学计数法则是E/e)

#注意
Python中百分号格式化是不存在自动将整数转换成二进制表示的方式, 即不存在%b
```

字符串

```python
s    #获取传入对象的 _str_ 方法的返回值, 并将其格式化到指定位置
r    #获取传入对象的 _repr_ 方法的返回值, 并将其格式化到指定位置
c    #整数:将数字转换成其unicode对应的值, 10进制范围为 0 <= i <= 1114111(py27只支持0 ~ 255); 字符:将字符添加到指定位置
```

特殊

``` python
%    #当字符串中存在格式化标志时, 需要用 %% 表示一个百分号
```



#### 分支循环

1. 分支

`if`

```
# 单分支
if 条件:
	pass
	
# 双分支
if 条件:
	pass
else: 
	pass
	
# 多分支
if 条件:
	pass
elif 条件:
	pass
elif 条件:
	pass
...
```

注意

强制缩进: Tab 缩进, Python 是利用代码缩进来区分代码块的, 所以一定要注意缩进格式

Python 中没有 `switch ... case ...` 语法

2. 循环

`while`

```
# 
while 条件: 
	pass
	
#
while 条件:
	pass
else:
	pass
```

注意: Python 中没有类似与其它语言的 `do ... while ` 语句

`for` 

```
for x in xxx:
	pass
# xxx通常是一个集合, 可以是字符串, 列表, 


for x in xxx:
	pass
else: 
	pass
# 如果for可以顺利的执行完毕, 则会执行else; 反之, 使用了break则不会执行else

# 遍历区间[1, num]
for x in range(1, num + 1)
	pass
```

注意:

`range()` 是左闭右开区间的集合; `break` 打断本次循环, 跳出整个循环; `continue` 结束本次循环, 继续执行下次循环



#### 常用数据类型操作

###### 数值

1. 类型

整数 `int` 

类型: 二进制 `0b` , 八进制 `0/0o`, 十进制 (不需要加前缀) , 十六进制 `0x`

```py
num = 0b111
print(num)  #7
```

浮点数 `float`

由整数部分和小数部分组成, `168,2` ; 也可以用科学计数法表示, `1.682e2`

复数 `complex` 

由实部和虚部组成, `a  + bj` 表示为 `complex(a, b)` ; 注意 `a, b` 都是浮点数

注意: Python3 的整型, 可以自动调整大小, 当作 `long` 类型使用 

2. 进制转换

```python
#x进制转换为其他进制
num = 0x37
print(bin(num))
print(oct(num))
print(hex(num))
print(num)   #十进制不需要前缀

#output
0b110111
0o67
0x37
55
```

3. 常用操作

注意: 部分函数使用前注意要引入对应模块, 如 `import math` ; 使用函数时**格式**是 '模块名.函数名(参数)', 如 `math.fabs(-10)`

- **适用于几乎所有 Python 运算符操作**

- **数学函数** 

  - 内建函数: 存在于 `builtins.pyi` 文件中, 无需导入

    `abs(num)`, `min(a, b, c, ...)` , `max(a, b, c, ...)` , `pow(x, y)` 

    `round(num[, n])` : n 表示四舍五入的小数位数, 同样可以不写, 默认为0, 即四舍五入取整


  - math 模块函数: 使用前需要先导入 `math` 模块, 即 `import math` 

    `ceil(num)` : 上取整    `floor(num)` : 下取整    `sqrt(num)` : 开平方    `log(x, base)` : 以 base 为基数, x 为对数

- **随机函数**

以下函数均属于 `random` 模块, 需加入 `import random` 

`random()` :  $[ 0, 1)$ 范围之间的随机小数

```python
print(random.random())            #0.818697325436201
```

`choice` : 从一个序列中随机挑选一个数值

```python
seq = [1, 3, 4, 5, 8, 10]
print(random.choice(seq))         #4
```

 `uniform(x, y)` : $[x, y]$ 范围内的随机小数

```python
print(random.uniform(1, 3))       #1.5886732714782932
```

`randint(x, y)` : $[x, y]$ 范围内的随机整数

```python
print(random.randint(1, 3))       #3
```

`randrange(start, stop=None, step=1)` : 给定区间 `[start, stop)` 内取一整数, 且可以设置步长

```python
print(random.randrange(1, 4))     #3
print(random.randrange(1, 20, 2)) #17
```

- **三角函数**

属于 `math` 模块

`sin(x)` , `cos(x)`, `tan(x)`, `asin(x)`, `acos(x)`, `atan(x)` , `degress(x)` : 弧度 -> 角度, `radian(x)` : 角度 -> 弧度

数学常量 `pi` : 数学中的 $Π$ , 可直接调用  `math.pi` 

```python
import math
result = math.sin(math.radians(30))  #注意三角函数参数接受的是弧度, 传入角度需要先转换为弧度
print(result)   #0.49999999999999994
```



**布尔**

1. `Bool` : `True`, `Flase` 

2. `int` 类型的子类

```python
print(True + 2)
print(issubclass(bool, int))
#output
3
True
```



###### 字符串

概念: 由单个字符组成的一个集合

1. **形式**

- 非原始字符串

  ```
  'abc'          #使用单引号包含
  "abc"          #使用双引号包含
  '''abc'''      #使用三个单引号包含
  """abc"""      #使用三个双引号包含
  ```

- 原始字符串: 能使字符串忽略转义符, 保留原始内容

  ```python
  #格式: r'abc'
  #同样可以改为其他引号形式
  
  name = r"And the last character is \n, not \t."
  print(name)
  #output
  And the last character is \n, not \t.
  ```

- 转义符: 有 `\n`       `\t`       `\'`        `\"`        `\` : (在行尾时), 表示续行符

    ```python
    name = "Hong"\
    "Kong"
    print(name)  #HongKong 
    ```



2. **各形式特点**

单/双引号

- 混合使用能避免使用引号转义符

    ```python
    print('I am "King"')   #I am "King"
    print("I am 'King'")   #I am 'King'
    ```

- 需要跨行时

  ```
  # 需要换行符
  name = "Hong" \ 
  "Kong"
  
  # 使用小括号
  name = ("Hong "
  "Kong")
  ```
  

三引号

- 可以直接跨行书写

  ```python
  print("""So who
  am I ?""")
  
  #output
  So who
  am I ?
  ```

- 可用于注释

  ```python
  '''
  hhh
  '''
  ```

  

3. **字符串一般操作**

字符串**拼接**

```python
#1. str1 + str2
print("I am" + "King")  #I am King

#2. str1srt2  直接把两个字符串放在一起, 只要保证字符串在同一行即可, 且中间的空格都会被忽略
print("I am "    "King") #I am King

#3. "str1%s" % (str2)
print("I am %s" % ("King")) #I am King

#4. str * n  字符串乘法
print("I am King " * 3) #I am King I am King I am King
```

字符串**切片**

概念: 获取字符串的某个片段

- 获取某个字符

  ```python
  name[index]
  index: 正数则从头部开始定位, 初始为0; 负数则从尾部开始定位, 初始为-1
  name[-1]: 表示字符串末位字符
  ```

- 获取一个字符串片段

  ```python
  name[start:end:step]
  获取范围: [start, end) 左闭右开
  
  默认值
  起始默认值: 0
  结束默认值: len(name) 即整个字符串长度
  步长默认值: 1
  
  获取顺序
  step > 0: 从左到右
  step < 0: 从右到左
  注意: 不能从头跳跃到尾部, 也不能从尾部跳跃到头部
  #下面代码无输出
  name = "abcdefg"
  print(name[0:len(name):-1])
  print(name[len(name):0:1])
  
  特殊
  name[::-1]  反转字符串
  ```

字符串**函数操作**

如果是内建函数, 可直接使用; 如果是属于对象方法, 使用格式是 `对象.方法(参数)` 

- 查找计算

  ```python
  内建函数
  len
  作用: 用于字符串字符个数; 一个汉字, 字母或转义符都是占一个
  语法: len(str1)
  print("我是hh\n") #5
  
  对象方法
  find()
  作用: 查找子串(下标)的索引位置
  语法: str.find(sub, start=0, end=len(str))
  参数: sub 需要检索的子字符串, start 检索的起始位置, end 检索的结束位置
  返回: 子串首字符下标, 找不到则返回-1
  注意: 从左到右查找, 找到后立即停止, 范围[start, end)
  
  rfind()
  功能同find(), 区别是该函数从右往左查找, 且同样返回sub首字符下标
  
  index()
  功能同find(), 区别是找不到时不返回-1, 而是报错
  
  rindex()
  功能同index(), 区别是从右往左查找
  
  count()
  作用: 计算某个子字符串出现的次数
  语法: str.count(sub, start=0, end=len(str))
  返回值: 子字符串出现的个数
  ```

- 转换操作

  ```python
  对象方法
  replace()
  作用: 使用新的字符串, 替换原字符串中的旧字符串
  语法: str.replace(old, new[, count])
  参数: old 需要被替换的旧字符串;  new 替换后的新字符串; count 替换的个数, 可省略, 表示替换全部
  返回值: 替换后的结果字符串
  注意: 不会修改原字符串
  
  capitalize()
  作用: 将字符串的首字母变成大写
  语法: str.capitalize()
  参数: 无
  返回值: 首字符大写后的新字符串
  注意: 不会修改原字符串; 如果字符串不是字母开头, 则没有作用
  
  title()
  作用: 将字符串中每个单词首字母变成大写
  语法: str.title()
  参数: 无
  返回值: 每个单词首字母大写后的新字符串
  注意: 不会修改原字符串; 且只要是非字母字符都算是单词分隔符
  name = "abc1de*fg"
  print(name.title())  #Abc1De*Fg
  
  lower()
  作用: 将字符串中每个字符都变为小写
  语法: str.lower()
  参数: 无
  返回值: 作用后的新字符串
  
  upper()
  作用: 将字符串中每个字符都变为大写
  ```

- 填充压缩

  ```python
  对象方法
  ljust()
  作用: 根据一个指定字符, 将原字符串填充够指定长度, l表示原字符串靠左
  语法: str.ljust(width, fillchar)
  参数: width 指定结果字符串的长度; fillchar 如果原字符串长度小于指定长度, 填充字符
  返回值: 作用后的字符串
  注意: 不会修改原字符串; fillchar的字符长度只能为1; 只有原字符串长度小于指定长度才会填充, 大于指定长度就返回原字符串
  
  rjust()
  作用同上, 区别是原字符串靠右
  
  center()
  作用同上, 区别是原字符串居中
  
  lstrip()
  作用: 移除原字符串指定字符(默认是空白字符), l表示从左侧开始移除; 注意空白字符指的是换行符, 空格等
  语法: lstrip(chars)
  参数: chars 需要移除的字符集, 表现形式为字符串
  返回值: 作用后的新字符串
  注意: 不会改变原字符串, 当参数中有多个字符时, 其作用形式是从左往右遍历字符串, 遇到第一个不属于该字符集的字符即停止遍历, 同时删去前面遍历到的字符
  name = "iiiaaammm King"
  print(name.lstrip("mai")) # King
  
  rstrip()
  作用同上, 区别是从右往左遍历
  ```

- 分割拼接

  ```python
  对象方法
  split()
  作用: 将一个大的字符串分割成几个子字符串
  语法: str.split(sep, maxsplit)
  参数: sep 分隔符; maxsplit 最大的分割次数, 可省略, 代表有多少分割多少
  返回值: 分割后的子字符串, 组成的列表; list列表类型
  注意: 不会修改字符串本身
  name = "hh-ww-pp"
  print(name.split("-"))  #['hh', 'ww', 'pp']
  
  partition()
  作用: 根据指定的分隔符, 返回分隔符左侧内容, 分隔符和分隔符右侧内容
  语法: str.partition(sep)
  参数: sep 分隔符
  返回值: 如果找到分割附, 则返回分隔符左侧内容, 分隔符和分隔符右侧内容(tuple类型); 如果没有找到, 则返回('str', ",")
  注意: 不会修改原字符串; 从左侧开始查找分隔符
  name = "I-am-King"
  word = "IamKing"
  print(name.partition("-"))
  print(word.partition("-"))
  #output
  ('I', '-', 'am-King')
  ('IamKing', '', '')
  
  rpatition()
  作用同上, 区别是从右往左开始查找
  
  splitlines()
  作用: 按照换行符(\r, \n), 将字符串拆成多个元素, 保存到列表中
  语法: str.splitlines(keepends)
  参数: keepends 是否保留换行符, bool类型
  返回值; 被换行符分割的多个字符串, 作为元素组成的列表, list类型
  注意: 不会修改原字符串
  name = "I \n am \r King"
  print(name.splitlines())
  #output
  ['I ', ' am ', ' King']
  
  join()
  作用: 根据指定的字符串, 将给定的迭代对象, 进行拼接, 得到拼接后的字符串
  语法: sep.join(iterable)
  参数: iterable 可迭代对象, 如字符串,元组,列表...; sep 分割每个对象的分隔符
  返回值: 拼接好的新字符串
  item = ["I", "am", "King"]
  print(" ".join(item))  #I am King
  ```

- 判定

  ```python
  对象方法
  str.isalpha()
  作用: 判断是否字符串所有的字符都是字母, 即不包含数字,特殊符号,标点符号等等
  参数: 无
  返回类型: Bool类型, 给定一个空串则判定为False
  
  str.isdigit()
  作用: 判断字符串所有字符都是数字
  
  str.isalnum()
  作用: 判断字符串所有字符都是数字或字母
  
  str.isspace()
  作用: 判断字符串所有字符都是空白字符, 包括空格,缩进,换行符等不可见转义字符
  
  startswith()
  作用: 判断字符串是否以某个前缀开头
  语法: str.startswith(prefix, start = 0, end=len(str))
  参数: prefix 需要判定的前缀字符串; start 判定起始位置; end 判定结束位置
  返回值: Bool类型
  
  endswith()
  作用: 判定一个字符串是否以某个后缀结尾
  语法: str.endswith(suffix, start=0, end=len(str))
  ```

- 补充

  ```python
  in
  判定一个字符串是否被另一个字符串包含
  not in
  判定一个字符串是否不被另一个字符串包含
  
  name = "I am King"
  print("am" in name)
  print("I" not in name)
  #output
  True
  False
  ```



###### 列表

概念: **有序**的**可变**的元素集合

1. 定义

- 方式1

  ```python
  [ele1, ele2, ...]
  
  注意:
  列表集合其中的元素可以多种数据类型的元素, 且可以为空;
  列表本身也可以是一个元素, 可以列表嵌套列表;
  [1, 2, 3, ["a", "b", True]]
  ```

- 方式2

  ```python
  #列表生成式
  快速生成list([start, end))
  语法:range(stop)  or  range(start, end, step) 
  
  注意: 为了防止生成的列表没有被使用导致空间浪费, python3做了改变, 不会立即生成列表
  #python2
  num = range(10)
  print(num) #[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
  #python3
  num = range(10)
  print(num) #range(0, 10)
  
  
  #列表推导式
  从一个list, 推导出另一个list
  概念:
  1.映射解析: 一对一变更
  2.过滤: 从多到少
  
  nums = [1, 2, 3, 4, 5]
  new_list1 = [num ** 2 for num in nums if num % 2 == 1]
  new_list2 = [1 for num in nums]
  new_list3 = [num for num in nums for num2 in nums]
  print(new_list1)
  print(new_list2)
  print(new_list3)
  #output
  [1, 9, 25]
  [1, 1, 1, 1, 1]
  [1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 3, 3, 3, 3, 3, 4, 4, 4, 4, 4, 5, 5, 5, 5, 5]
  ```

2. 常用操作

- 增

  ```python
  append()
  作用: 在列表的最后增加一个新的元素
  语法: l.append(object)
  参数: object 增加的元素
  返回值: None
  注意: 会修改原列表
  
  
  insert()
  作用: 在列表中, 在指定索引值之前增加一个新的元素
  语法: l.insert(index, object)
  参数: index 下标索引值; object 想要添加的元素
  返回值: None
  注意: 会修改原列表
  
  
  extend()
  作用: 在列表中扩展另一个可迭代序列
  语法: l.extend(iterable)
  参数: iterable 可迭代集合, 如字符串,列表,元组...
  返回值: None
  注意: 会修改原列表
  list1 = [1, 2, 3]
  list2 = ['a', 'b', 'c']
  list3 = [4, 5, 6]
  ret = "abcdefg"
  # list1.extend(list2)
  print(list1.extend(list2))
  print(list1)
  list3.extend(ret)  #特别注意
  print(list3)
  #output
  None
  [1, 2, 3, 'a', 'b', 'c']
  [4, 5, 6, 'a', 'b', 'c', 'd', 'e', 'f', 'g']
  
  
  乘法运算
  list1 = [1, 2, 3]
  print(list1 * 3)   #[1, 2, 3, 1, 2, 3, 1, 2, 3]
  
  加法运算
  list1 = [1, 2, 3]
  list2 = ['a', 'b', 'c']
  print(list1 + list2) #[1, 2, 3, 'a', 'b', 'c']
  #和extend()的区别: 加法运算时左右两端都应该是列表; 但是extend()的参数可以是任何可迭代集合, extend()本质是集合的扩充, 加法运算时列表简单相加
  
  ```

- 删

  ```python
  del()
  作用: 可以删除一个指定元素(对象)
  语法: del 指定元素
  注意: 也可以删除整个列表
  nums = [1, 2, 3, 4, 5]
  del nums[2]
  print(nums)  #[1, 2, 4, 5]
  #del nums
  #print(nums)  #Error
  
  pop()
  作用: 移除并返回列表中指定索引对应的元素
  语法: l.pop(index=-1)
  参数: index 需要被删除元素的索引, 默认是-1, 即最后一个元素
  返回值: 被删除的元素
  注意: 会直接修改原列表, 注意索引越界
  
  remove()
  作用: 移除列表中的指定元素
  语法: l.remove(object)
  参数: 需要被删除的元素
  返回值: None
  注意: 会直接修改原列表, 如果元素不存在, 会报错; 若存在多个元素, 只会删除最左边的一个, 注意删除内循环列表带来的坑
  ```

- 改

  ```python
  l[index] = val;
  当我们以后要操作一个列表当中的某个元素时, 一定是通过这个索引(下标), 来操作指定元素的
  ```

- 查

  - 获取单个元素:  `items[index]` 

    注意负索引

  - 获取元素索引: `list.index(val, start, end)`

    同样可以限定索引区间, 也可以不写, 取默认值

  - 获取指定元素的个数: `list.count(val, start, end)`

  - 获取多个元素: `list[start:end:step]`

    `[::-1]` 是反转列表

  - 遍历

    - 根据元素进行遍历

      ```python
      for item in list:
      	pass
      ```

    - 根据索引进行遍历

      ```python
      for index in range(len(list)):
      	print(index, list[index])
      ```

    - 创建对应的枚举对象, 遍历枚举对象(了解)

      枚举对象: 通过枚举函数生成的一个新的对象

      作用: 函数用于将一个可遍历的数据对象(如列表,元组或字符串)组合为一个索引序列, 同时列出数据下标和数据

      语法: `enumerate(sequence[, start])`

      ```python
      values = ['a', 'b', 'c', 'd', 'e']
      print(enumerate(values))
      # 将枚举对象转换为列表类型
      print(list(enumerate(values)))
      # 遍历整个枚举对象（枚举对象可以直接被遍历）
      for idx, val in enumerate(values):
          print(idx, val)
      for tup in enumerate(values):
          print(tup)
      #output
      <enumerate object at 0x0000019D7BC7BFC0>
      [(0, 'a'), (1, 'b'), (2, 'c'), (3, 'd'), (4, 'e')]
      0 a
      1 b
      2 c
      3 d
      4 e
      (0, 'a')
      (1, 'b')
      (2, 'c')
      (3, 'd')
      (4, 'e')
      ```

    - 使用**迭代器**进行遍历(了解)

      (1) 概念

      **迭代**: 是访问集合的一种方式, 按照某种顺序逐个访问集合中的每一项

      **可迭代对象**: 能够被迭代的对象; 判定依据是能作用于 `for in` 

      判定方法: 

      ```python
      from collections.abc import Iterable
      nums = [1, 2, 3, 4]
      values = 123
      print(isinstance(nums, Iterable))   #True
      print(isinstance(values, Iterable)) #False
      ```

      **迭代器**: 是可以记录遍历位置的对象; 从第一个元素开始, 往后通过 `next()` 函数进行遍历; 只能往后不能往前;判断依据是能做用于 `next()` 

      判定方法: 

      ```python
      import collections.abc
      nums = [1, 2, 3, 4]
      print(isinstance(nums, collections.abc.Iterator))   # False
      # 借助iter() 生成迭代器
      i = iter(nums)
      print(isinstance(i, collections.abc.Iterator))      # True
      # 迭代器本身也是可迭代对象
      print(isinstance(i, collections.abc.Iterable))      # True
      注意: 迭代器也是可迭代对象, 所以也可以作用于for in
      ```

      (2) 为什么会产生迭代器?

      Ⅰ.仅仅在迭代到某个元素时才处理该元素, 在此之前元素可以不存在, 在此之后元素可以被销毁, 特别适合于遍历一些巨大的或是无限的集合
      Ⅱ.提供了一个统一的访问集合的接口, 可以把所有的可迭代对象, 转换成迭代器进行使用
      生成迭代器: `iter(iterable)` 

      (3) 迭代器的简单使用

      使用`next()`函数, 从迭代器中取出下一个对象, 从第1个元素开始; 因为迭代器比较常用, 所以在Python中, 可以直接作用于`for in`, 其内部会自动调用迭代器对象的 `next()` , 会自动处理迭代完毕的错误

      ```python
      nums = [1, 2, 3, 4]
      it = iter(nums)
      print(next(it))          # 1
      print(next(it))          # 2
      v = iter(nums)
      print(v)                 # <list_iterator object at 0x000001C916D78A60>
      for vv in v:
          print(vv, end=' ')   # 1 2 3 4
      ```

      (4) 注意事项

      如果取出完毕, 再继续取, 则会报错: `StopIteration`

      迭代器一般不能多次迭代, 即只能使用一次, 想再次使用必须重新创建

      ```python
      nums = [1, 2, 3, 4]
      it = iter(nums)
      for v in it:
          print(v)  # 1 2 3 4
      for v in it:
          print(v)  # 无输出, 因为迭代器it已经被使用过了
      ```

      

- 额外操作

  ```python
  判定
  print(ele in list)
  print(ele not in list)
  事实上, in 和 not in 适用于所有集合的元素的判定
  
  
  比较
  Python2: 内建函数, 如果比较的是列表, 则针对每个元素从左到右逐一比较, 若左大于右则返回1, 左等于右则返回0, 左小于右则返回-1
  Python3: 直接使用比较运算符进行比较, 即 > < ==
  
  
  排序
  (1)内建函数
  可适用于对所有可迭代对象进行排序
  语法: sorted(itetable, key=None, reverse=False)
  参数: iterable 可迭代对象; key 排序关键字,值为一个函数,此函数只有一个参数且返回一个值; reverse 控制升序降序, 默认False, 即升序
  返回值: 一个排好序的列表
  注意: 列表本身不会发生改变
  示例
  values = "hcfboahfu"
  nums = [2, 6, 4, 9, 1, -1]
  mems = [("s1", 14), ("s3", 19), ("s2", 15), ("s4", 20)]
  print(sorted(values))
  print(sorted(values, reverse=True))
  print(sorted(nums))
  print(sorted(mems)) 
  def getKey(x):
      return x[1]
  print(sorted(mems, key=getKey)) 
  # output
  ['a', 'b', 'c', 'f', 'f', 'h', 'h', 'o', 'u']
  ['u', 'o', 'h', 'h', 'f', 'f', 'c', 'b', 'a']
  [-1, 1, 2, 4, 6, 9]
  [('s1', 14), ('s2', 15), ('s3', 19), ('s4', 20)]
  [('s1', 14), ('s2', 15), ('s3', 19), ('s4', 20)]
  
  (2)列表对象方法
  语法: list.sort(key=None, reverse=False)
  参数: key 排序关键字, 值为一个函数, 此函数只有一个参数且返回一个值用来比较; reverse 控制升序降序, 默认False, 即升序
  返回值: None
  注意: 列表本身直接发生改变
  示例
  nums = [2, 6, 4, 9, 1, -1]
  mems = [("s1", 14), ("s3", 13), ("s2", 15), ("s4", 20)]
  print(mems.sort())
  print(mems)
  def getKey(x):
      return x[1]
  mems.sort(key=getKey)   # 注意不要写成getkey(), 因为不是立即调用, 而是传入后由该方法内部进行调用
  print(mems)
  # output
  None
  [('s1', 14), ('s2', 15), ('s3', 13), ('s4', 20)]
  [('s3', 13), ('s1', 14), ('s2', 15), ('s4', 20)]
  
  
  乱序
  可以随机打乱一个列表
  返回值为None, 列表直接被改变
  导入random模块
  import random
  random.shuffle(list)
  
  
  反转
  对象方法: l.reverse()  返回值同样为None, 列表直接被改变
  切片反转: l[::-1]      返回值为反转后的对象, 原对象不改变
  ```

  

######   元组

概念: **有序的不可变的**集合, 和列表的区别就是元组元素不能修改

1. 定义

   ```python
   一个元素的写法
   t = (1,)        #主要需要添加一个逗号, 与提升运算优先级的小括号作区分
   print(type(t))  # <class, 'tuple'> 
   
   多个元素的写法
   t = (1, 2, 3)
   
   多个对象, 以逗号隔开, 默认为元组
   t = 1, 2, 3, "hh"
   print(type(t))  # <class, 'tuple'>
   
   从列表转换成元组
   l = [1, 2, 3, 4]
   changeTuple = tuple(l)
   print(changeTuple, type(changeTuple))  # (1, 2, 3, 4)  <class, 'tuple'>
   
   元组嵌套
   t = (1, 2, (3, 4))  # 元组中的元素可以是元组
   ```

2. 常用操作

- 由于元组元素不可修改, 所以也不支持**增, 删, 改**的操作

- 查

  ```python
  获取单个元素
  tuple[index]
  index是索引, 可以为负
  
  获取多个元素
  切片
  tuple[start:end:step]
  ```

- 额外操作

  ```python
  获取
  tuple.count(item)   # 统计元素中指定元素的个数
  tuple.index(item)   # 获取元组中指定元素的索引
  len(tuple)          # 返回元组中元素的个数
  max(tuple)          # 返回元组中元素最大的值
  min(tuple)          # 返回元组中元素最小的值
  
  判定
  in                  
  not in
  
  比较
  Python2
  cmp()
  内建函数, 如果比较的是元组, 则针对每个元素, 从左到右注意比较; 左大于右, 返回1; 左小于右, 返回-1; 相等则返回0; 类型相同逐一比较元素, 类型不同则比较类型名称, 如列表和元组是'list'和'tuple'的比较
  Python3
  比较运算符 == > <   返回的是True或False
  
  拼接
  乘法: tuple * n       # n是整型数值
  加法: tuple1 + tuple2
  
  拆包
  a, b = (ele1, ele2)  # 结果: a = ele1, b = ele2
  ```

  

###### 字典

概念: **无序的可变的**键值对集合

1. 定义

   ```python
   方式1
   {key:value; key:value; ...}
    
   
   方式2
   fromkeys(S, v=None)
   静态方法: 类和对象都可以调用
   
   类调用:
   dict.fromkeys(seq, val)   # 此处的dict是指字典类型, seq是有序集合, val是值
   示例
   dic = dict.fromkeys("abc", 123)
   print(dic)        # {'a': 123, 'b': 123, 'c': 123}
   
   对象调用(不常用):
   dic.fromkeys(seq, val)    # 此处的dic是实例化的字典对象
   示例
   dic = {1: 2, 2: 3}.fromkeys("abc", 123)
   print(dic)        #{'a': 123, 'b': 123, 'c': 123}
   
   
   注意:
   1. key不能重复, 如果key重复, 旧的值则会被新的覆盖
   2, key必须是任意不可变类型
   (1) 原因: Python的字典, 采用的是哈希(Hash)的方式实现
   (2) 简单储存过程: 初始化一个表格, 用来存放所有的值, 这个表格成为"哈希表"; 在存储一个键值对时, 会根据给定的key, 通过哈希函数得到一个在"哈希表"中的索引位置, 然后根据索引位置, 存储给定的值
   哈希: 把key通过"哈希函数"转换成一个整型数字, 称为一个"哈希值", 将该数字对数组长度进行取余, 取余结果就是数组的下标, 如果发生了"哈希冲突", 则采用"开放寻址法", 通过探测函数查找下一个空位
   (3) 简单查找过程: 再次使用哈希函数将key转换为对应的哈希表的索引, 定位到哈希表位置然后获取value
   
   
   类型
   可变: 列表, 字典, 可变集合...
   不可变: 数值, 布尔, 字符串, 元组...
   如何判断是否可变? 尝试修改, 如果修改之后id()发生改变, 则说明是不可变的, id()不变则类型是可变的
   ```

2. 存在意义

   - 可以通过key, 访问对应的值, 使得这种访问更具意义

   - 查询的效率得到很大提升

3.  常用操作

- 增

  ```python
  dic[key] = value
  ```

- 删

  ```python
  del dic[key]
  注意: key不存在时会报错
  
  dic.pop(key[, default])
  删除指定的键值对, 并返回对应的值
  如果key不存在那么直接返回给定的default值, 不作删除动作; 如果没有给定default, key不存在时会报错
  
  dic.popitem()
  删除最后一个键值对, 并以元组的形式返回键值对
  如果字典为空则报错
  
  dic.clear()
  删除字典内所有键值对, 返回值是None, 且字典仍然是存在的, 只是为空; 而del删除整个字典后, 字典将不存在
  示例
  dic = {"a": 12, "b": 13, "c": 14}
  dic.clear()
  print(dic)  # {}
  del dic
  print(dic)  # Error
  ```

- 改

  ```python
  只能改值, 不能修改key
  
  修改单个键值对
  dic[key] = value  # 直接设置, 如果key不存在则新增, 若存在则是修改
  
  批量修改键值对
  oldDic.update(newDic)
  根据新的字典, 批量修改旧字典中的键值对; 如果旧字典中没有对应的key, 则是新增键值对
  ```

- 查

  ```python
  1.获取单个值
  方式1: dic[key]
  方式2: dic.get(key[, default]) 如果不存在对应的key, 则取给定的default值, 如果没有默认值, 则为None, 但不会报错, 且原字典不会新增这个键值对
  方式3: dic.setdefault(key[, default]) 和方式2相同, 区别是它在key不存在时给字典加上新的键值对key:default(key:None)
  
  
  2.获取所有的值
  dic.values()
  
  3.获取所有的键
  dic.keys()
  
  4.获取字典的键值对
  dic.items()
  
  注意: 
  Python2和Python3版本之间关于通过keys(),values(),items()获取键,值,item之间的区别: Python2直接是一个列表, 可通过下标获取指定元素, 而Python3中是Dictionary view objects(视图对象), 不能通过下标获取指定元素, 除非通过list()强转为列表或tuple()强转为元组;
  而且Python2中也提供了viewkeys(), viewvalues(), viewitems(), 作用等同于Python3中的Dictionary view objects
  
  示例(Python3环境)
  d = {"a": 12, "b": 13, "c": 14}
  ks = d.keys()
  vs = d.values()
  its = d.items()
  print(ks, vs, its)
  d["d"] = 19
  print(ks, vs, its)
  #output
  dict_keys(['a', 'b', 'c']) dict_values([12, 13, 14]) dict_items([('a', 12), ('b', 13), ('c', 14)])
  dict_keys(['a', 'b', 'c', 'd']) dict_values([12, 13, 14, 19]) dict_items([('a', 12), ('b', 13), ('c', 14), ('d', 19)])
  
  
  5.遍历
  方法1:获取键
  示例
  keys = d.keys()
  for key in keys:
  	print(key, d[key])
  方法2:获取键值对(更推荐, 因为所得kvs是视图对象, 在字典添加新元素时其依然能起到获取字典所有元素的作用)
  kvs = d.items()
  for k, v in kvs:
  	print(k, v)
  
  
  6.计算
  len(info)   # 键值对的个数
  
  
  7.判定
  x in dic
  x not in dic
  判定的是key是否存在
  dic.has_key(key)
  Python2中会存在, 但Python3中已过期, 建议使用is替代
  ```



###### **集合**

1. 概念: **无序的, 不可随机访问的, 不可重复的**元素集合; 与数学中的集合的概念类似, 可对其进行交, 并, 差, 补等逻辑运算

   分为**可变集合**和**非可变集合**: 

   - `set` 为可变集合, 可进行增, 删, 改操作

   - `frozenset` 为不可变集合, 创建好之后无法增删改



2. 定义

   - 可变集合

     ```python
     方法1: s = {v1, v2, ...}
     
     
     方法2: s = set(itetable)
     iterable可以是字符串, 列表, 元组, 字典等, 但是为字典时, 只会获取key作为set的元素
     示例
     d = {"a": 12, "b": 13, "c": 14}
     s = set(d)
     print(s, type(s))  # {'b', 'a', 'c'} <class 'set'>
     
     
     方法3: 集合推导式
     s = set(推导式)  
     s = {推导式}
     示例
     s = set(x ** 2 for x in range(1, 10) if x % 2 == 0)  # {16, 64, 4, 36}
     ```

   - 不可变集合

     ```python
     大致与可变集合的定义相似
     fs = frozenset(iterable)
     fs = frozenset(推导式)
     ```

   - 注意事项

     ```python
     1. 创建一个空的集合时, 需要使用set()或者frozenset(), 不能直接使用{}, 否则会被识别为字典
     示例
     d = {}
     s = set()
     fs = frozenset()
     print(type(d), type(s), type(fs))  # <class 'dict'> <class 'set'> <class 'frozenset'>
     
     2. 集合中的元素, 必须是可哈希的值. 如果一个对象在自己的生命周期中有一哈希值(hash value)是不可改变的, 那么它就是可哈希的(hashable), 可以暂时理解为不可变类型
     
     3. 如果集合中的元素值出现重复, 则会被合并为1个
     可利用此性质进行去重操作
     示例
     l = [1, 1, 2, 3, 2, 3, 3]
     s = set(l)           # 转换为set去重
     print(s, type(s))        
     result = list(s)     # 转换回list
     print(result, type(result))
     # output
     {1, 2, 3} <class 'set'>
     [1, 2, 3] <class 'list'>
     ```

   

3. 常用操作

   - 单一集合操作

     ```python
     可变集合
     1.增
     s.add(element)   # 增加的元素也必须是hashable
     
     2.删
     s.remove(element)
     指定删除set对象的一个元素, 如果没有这个元素则返回一个错误
     s.discard(element)
     指定删除set对象的一个元素, 如果没有这个元素则返回None
     s.pop(element)
     随机删除并返回一个集合中的元素, 若集合为空, 则返回一个错误
     s.clear()
     清空集合中的所有元素, 但是集合还存在, 即结果为set(), 除非使用del
     
     3.改
     元素为不可变类型, 不可修改
     
     4.查
     无法通过索引或者key进行查询, 但是可以通过for in进行遍历或者迭代器进行访问
     示例
     s = {1, 2, 3, 4}
     for v in s:
         print(v, end=' ')   # 1 2 3 4 
     its = iter(s)           # 生成迭代器
     for it in its:
         print(it, end=' ')  # 1 2 3 4 
     
     
     不可变集合
     不能进行增删改 
     查: 通过for in进行遍历或迭代器进行访问, 方式同上
     ```

   - 集合之间的操作

     ```python
     交集
     方法1: intersection(Iterable) 
     参数: Iterable 可以是字符串, 列表, 元组, 字典, 集合..., 但其中的元素必须是可哈希的值
     注意: 可变与不可变类型混合运算, 返回结果类型以运算符左侧为主;
     示例
     s1 = frozenset([1, 2, 3, 4])
     s2 = {3, 4, 5, 6}
     res1 = s1.intersection(s2)
     res2 = s2.intersection(s1)
     print(res1, type(res1))    # frozenset({3, 4}) <class 'frozenset'>
     print(res2, type(res2))    # {3, 4} <class 'set'>
     
     方法2: 逻辑与'&'
     示例
     s1 = frozenset([1, 2, 3, 4])
     s2 = {3, 4, 5, 6}
     res1 = s1 & s2
     res2 = s2 & s1
     print(res1, type(res1))    # frozenset({3, 4}) <class 'frozenset'>
     print(res2, type(res2))    # {3, 4} <class 'set'>
     
     方法3: intersection_update(...)
     交集计算完毕后, 会再次赋值给原对象, 且返回值为None, 即直接修改原对象本身, 所以只适用于可变集合, 否则会报错;
     示例
     s1 = {3, 4, 5, 6}
     s2 = {1, 2, 3, 4}
     s1.intersection_update(s2)
     print(s1, s2)              # {3, 4} {1, 2, 3, 4}
     
     
     并集
     union()  返回并集
     逻辑或'|' 返回并集
     update() 更新并集
     
     
     差集
     difference()         返回差集
     算术运算符'-'          返回差集
     difference_update()  更新差集
     
     
     判定
     isdisjoint()   两个集合是否相交, 相交返回False, 不相交返回True
     issuperset()   一个集合是否包含另一个集合, 或者是否是另一个集合的父集合, 是则返回True, 否则返回False
     issubset()     一个集合包含于另一个集合, 或者是否是另一个集合的子集和, 是则返回True, 否则返回False
     ```

     

###### 时间日历

Python程序能用很多方式处理日期和时间, 转换日期格式是一个常见的功能

**常用操作**

- `time` 模块

  提供了处理时间和表示之间转换的功能, 使用下列函数前都需要添加语句 `import time` 表示引用模块

  - 获取当前的时间戳

    概念: 从0时区的1970年1月1日0时0分0秒, 到所给定日期时间的秒数;

    类型: 浮点数

    获取方式: `time.time()`

  - 获取时间元组

    概念: 很多python时间函数将时间处理为9个数字的元组, 见图

    <img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20230502232002949.png" alt="image-20230502232002949" style="zoom:50%;" align="center"/>

    获取方式: `time.localtime([seconds])`

    参数: `seconds` 可选的时间戳, 默认是当前的时间戳

    ```python
    import time
    print(time.localtime())
    # output
    time.struct_time(tm_year=2023, tm_mon=5, tm_mday=2, tm_hour=23, tm_min=21, tm_sec=51, tm_wday=1, tm_yday=122, tm_isdst=0)
    ```

  - 获取格式化时间

    - 时间戳格式化. 获取方式: `time.ctime([seconds])`

    - 时间元组格式化. 获取方式: `time.asctime([p_tuple])`

      参数: `p_tuple` 可选的时间元组, 默认是当前的时间元组

  - 格式化日期字符串

    - 时间元组转为格式化日期

      实现方式: `time.strftime(string, p_tuple)` 

      ```python
      import time
      print(time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()))
      print(time.strftime("%y-%m-%d %H:%M:%S", time.localtime()))
      # output
      2023-05-02 23:33:13
      23-05-02 23:33:13
      ```

      常用格式符

      ```python
      %Y: 返回四位数格式的年份。在我们的例子中，它返回 “2018”
      %y: 返回两位数格式的年份，例如，”18“ 而不是 ”2018“
      %b: 返回月份名称的前三个字符。在我们的例子中，它返回 “Sep”
      %d: 返回本月的日期，从 1 到 31。在我们的例子中，它返回 “15”
      %H: 返回小时。在我们的例子中，它返回 “00”
      %M: 返回分钟，从 00 到 59。在我们的例子中，它返回 “00”
      %S: 返回秒，从 00 到 59。在我们的例子中，它返回 “00”
      %a: 返回工作日的前三个字符，例如 Wed
      %A: 返回返回工作日的全名，例如 Wednesday
      %B: 返回月份的全名，例如 September
      %w: 返回工作日作为数字，从 0 到 6，周日为 0
      %m: 将月份作为数字返回，从 01 到 12
      %p: 返回 AM/PM 标识
      %f: 返回从 000000 到 999999 的微秒
      %Z: 返回时区
      %z: 返回 UTC 偏移量
      %j: 返回当年的日期编号，从 001 到 366。
      %W: 返回年份的周数，从 00 到 53。星期一被记为一周第一天
      %U: 返回年份的周数，从 00 到 53。星期日被记为一周第一天
      %c: 返回本地日期和时间版本
      %x: 返回本地日期版本
      %X: 返回本地时间版本
      ```

    - 格式化日期改为时间元组

      实现方式: `time.strptime(string, format)` 

      也可将时间元组再转回时间戳: `time.mktime(t_tuple)` 

      ```python
      import time
      t1 = time.strftime("%Y-%m-%d %H:%M:%S", time.localtime())
      t2 = time.strptime(t1, "%Y-%m-%d %H:%M:%S")
      t3 = time.mktime(t2)
      print(t1)
      print(t2)
      print(t3)
      # output
      2023-05-02 23:54:18
      time.struct_time(tm_year=2023, tm_mon=5, tm_mday=2, tm_hour=23, tm_min=54, tm_sec=18, tm_wday=1, tm_yday=122, tm_isdst=-1)
      1683042858.0
      ```

  - 获取当前 CPU 时间

    获取方式: `time.perf_counter()` 

    ```python
    import time
    start = time.perf_counter()
    for i in range(0, 10000):
        pass
    end = time.perf_counter()
    print(end - start)
    # output
    0.0004401000333018601
    ```

  - 休眠

    推迟线程的执行, 可简单理解为, 让程序暂停

    实现方式: `time.sleep(secs)`

    ```python
    import time
    while True:
        print(time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()))
        time.sleep(1)
    # output
    2023-05-03 00:02:04
    2023-05-03 00:02:05
    2023-05-03 00:02:06
    ...
    ```



- `calendar` 模块

  提供与日历相关的动能, 例如为给定的月份或年份打印文本日历的功能; 使用前要添加 `import calendar` 

  获取某月日历实现方式: `calendar.month(2023, 5)` 

  ```python
  import calendar
  print(calendar.month(2023, 5))
  #output
        May 2023
  Mo Tu We Th Fr Sa Su
   1  2  3  4  5  6  7
   8  9 10 11 12 13 14
  15 16 17 18 19 20 21
  22 23 24 25 26 27 28
  29 30 31
  
  ```



- `datetime` 模块

  Python 处理日期和时间的标准库, 这个模块里面有 `datetime` 类, 此外常用的还有 `date` 类, 以及 `time` 类, 可以做一些计算之类的操作

  - 获取当天日期

    ```python
    import datetime
    print(datetime.datetime.now())
    print(datetime.datetime.today())
    # output
    2023-05-03 00:11:13.718011
    2023-05-03 00:11:13.718989
    ```

  - 单独获取当天的年月日时分秒

    ```python
    import datetime
    t = datetime.datetime.now()
    print(t, type(t))
    print(t.year)
    print(t.minute)
    # output
    2023-05-03 00:15:43.063749 <class 'datetime.datetime'>
    2023
    15
    ```

  - 计算 n 天之后的日期

    ```python
    import datetime
    t = datetime.datetime.now()
    tt = t + datetime.timedelta(days=7)
    print(t)
    print(tt)
    # output
    2023-05-03 00:21:42.325113
    2023-05-10 00:21:42.325113
    ```

  - 获取两个日期时间的时间差

    ```python
    import datetime
    start = datetime.datetime(2023, 5, 3, 0, 23, 0)
    end = datetime.datetime(2023, 11, 10, 0, 0, 0)
    res = end - start
    print(res, type(res))
    print(res.total_seconds())
    # output
    190 days, 23:37:00 <class 'datetime.timedelta'>
    16501020.0
    ```

    

#### 函数

**分类:** 内建函数, 三方函数, 自定义函数

###### **定义**

```python
def name():
	pass
```

**参数**

- 多个参数调用

    ```python
    方式1
    function(p1, p2, p3...)    # 形参与实参一一对应
    
    方式2
    function(name1 = p1, name2 = p2...)  # 可以指明形参名称, 称为"关键字参数", 不需要严格按照顺序
    ```

- 不定长参数

    场景: 如果函数体中, 需要处理的数据不确定长度, 则可以以不定长参数的方式接收数据

    实现

    - 方式1

      定义: `def function(*args)` 

      函数体中可以直接以**元组**变量的方式使用该参数, 接收参数时则是逐一接收即可; 而使用元组的原因是元组有序且不可改变, 这是函数所需要的特性

      ```python
      def col(*t):
          print(t, type(t))
          res = 0
          for v in t:
              res += v
          print(res)
      
      col(1, 2, 3, 4)
      
      # output
      (1, 2, 3, 4) <class 'tuple'>
      10
      ```

    - 方式2

      定义: `def function(**args)` 

      函数体中可以直接以**字典**变量的方式使用该参数, 接收参数时同样逐一接受即可. 

      ```python
      def Stu(**d):
          print(d, type(d))
      
      Stu(name="hh", age=19)   # key在这里不需要引号
      
      # output
      {'name': 'hh', 'age': 19} <class 'dict'>
      ```

- 参数拆包

    装包: 把传递的参数包装成一个集合

    拆包: 把集合参数, 再次分解为单独的个体

    ```python
    def Sum(*t):                # 装包
        print(t, type(t))       
        print(*t)               # 拆包, *t = 1, 2, 3, 4
    
    
    def myPrint(a, b):           # 传进来的是a和b, 所以也要是a和b的参数名接受, 若不同则会报错
        print(a, b)
    
    
    def Std(**d):
        print(d, type(d))
        # print(**d)              # 此处于元组拆包不同, 不能直接打印, 否则会报错, 字典拆包可用于函数传参
        myPrint(**d)              # 效果相当于下一条语句, 要特别注意的是, 传进去的键值对的key值必须拥有接受参数的函数的参数名
        # myPrint(a="hh", b=19)
    
    
    Sum(1, 2, 3, 4)
    Std(a="hh", b=19)
    
    # output
    (1, 2, 3, 4) <class 'tuple'>
    1 2 3 4
    {'a': 'hh', 'b': 19} <class 'dict'>
    hh 19
    ```

- 缺省参数

    场景: 当我们使用一个函数的时候, 如果大多数情况下, 使用的某个数据是一个固定值, 或者属于主功能之外的小功能实现, 则可以使用默认值, 这种参数, 则称为"缺省参数"

    定义: `def function(p1 = v1, p2 = v2): ` 

    函数体中, 即使外界没有传递指定变量, 也可以使用, 只不过该值是给定的默认值

    ```python
    def fun(someone="you"):
        print("I love", someone)
    
    fun()
    fun("her")
    
    # output
    I love you
    I love her
    ```

- 参数注意

    值传递和引用传递

    - 值传递: 是指传递过来的, 是一个数据的副本, 修改副本, 对原件没有任何影响
    - 引用传递: 是指传递过来的是一个变量的地址, 通过地址可以操作同一份原件

    - 注意: 在 Python 中, 我们无法选择传递方式, **只有引用传递(地址传递)**, 而能否改变变量**只取决于该变量的类型**. 如果数据类型是不可变类型, 则是无法改变的, 如果是可变类型, 则可以改变. 

    ```python
    # 不可变类型
    def change(num):
        print(id(num))          # 1934455603824
        num = 14                # 数值是不可变类型, 如果强行修改, 程序会自动开辟一个新的空间储存新的变量
        print(id(num))          # 1934455603856
    
    
    b = 13
    print(id(b))                # 1934455603824
    change(b)
    print(b)                    # 13
    print(id(b))                # 1934455603824
    
    
    # 可变类型
    def change(num):
        print(id(num))          # 2154446641728
        num.append(5)           # 列表是可变类型, 可直接修改, 地址不会改变
        print(id(num))          # 2154446641728
    
    
    a = [1, 2, 3]
    print(id(a))                # 2154446641728
    change(a)
    print(a)                    # [1, 2, 3, 5]
    print(id(a))                # 2154446641728
    ```

    

**返回值**

`return` 

`->` 出现在函数定义的`()` 之后, 表示返回值的类型

`:` 表示输入参数的类型建议符

```python
class CQueue:
    def _init__(self):
        self.A,self.B=[],[]
//value:int表示建议的value类型为int型，->None表示函数返回
值为空，->int表示函数返回值为int型。
    def appendTail(self,value:int)->None:
        self.A.append(value)

    def deleteHead(self)->int:
        if self.B:
            return self.B.pop()
        if not self.A:
            return -1
        while self.A:
            self.B.append(self.A.pop())
        return self.B.pop()
```

注意: 

1. `return` 后续代码不会被执行
2. 只能返回一次
3. 如果想要返回多个数据, 可先把多个数据包装成一个集合 (列表, 元组, 字典...) , 整体返回.

```python
def cal(a, b):
    return (a + b, a - b, a * b, a / b)   # 包装成元组

print(cal(3, 4))                          # (7, -1, 12, 0.75)
v1, v2, v3, v4 = cal(3, 4)                # 拆包
print(v1, v2, v3, v4)                     # 7 -1 12 0.75    
```



**使用描述**

场景: 当我们编写三方函数, 为了方便他人使用, 就需要描述清楚我们所写的函数功能以及使用方式等信息

格式: 直接在函数体的最上边, 添加三个引号对注释

```python
def function():
	"""
	Exegesis
	"""
	pass
```

查看函数使用文档: `help(function)` 

```python
help(print)
# output
Help on built-in function print in module builtins:

print(...)
    print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)

    Prints the values to a stream, or to sys.stdout by default.
    Optional keyword arguments:
    file:  a file-like object (stream); defaults to the current sys.stdout.
    sep:   string inserted between values, default a space.
    end:   string appended after the last value, default a newline.
    flush: whether to forcibly flush the stream.

```

规范

一般函数的描述, 需要说明如下信息

1. 函数的功能
2. 函数的参数: 含义, 类型, 是否可以省略, 默认值
3. 函数返回值; 含义, 类型



###### **偏函数**

概念: 当我们写一个参数比较多的函数时, 如果有些参数, 不同使用下需要固定不同的值, 那么为了简化使用, 就可以创建多个新函数, 并在不同的新函数中固定不同的参数; 或者, 某个函数的某个参数在大部分情况下都是一个固定的值, 我们也可以利用创建新函数, 新函数中对该参数固定一个值; 这个新函数就是"偏函数"

语法

```python
#
import functools


def cal(a, b, c, d):
    print(a + b + c + d)


newFunc1 = functools.partial(cal, d=1)      # 固定我们所需要固定的值
newFunc2 = functools.partial(cal, d=2)
newFunc1(1, 2, 3)              # 7
newFunc2(1, 2, 3)              # 8
print(newFunc2)                # functools.partial(<function cal at 0x000002964CBC6050>, d=2)


#
import functools

new_int = functools.partial(int, base=2)   # 创建一个函数,能将二进制的字符串转变为十进制数据,这样可以不必每次都写base=2
print(new_int("10010"))        # 18
```



###### **高阶函数**

概念: 当一个函数 A 的参数, 接受的又是另一个函数时, 则把这个函数 A 称为是 "高阶函数"

例如: `sorted(iterable, key, reverse)` , 其中的 `key` , 就是需要接收一个排序函数

```python
#
# mems = [("s1", 14), ("s3", 19), ("s2", 15), ("s4", 20)]
mems = [{"name": "aa", "age": 17}, {"name": "bb", "age": 15}, {"name": "cc", "age": 19}]


def getKey(x):
    return x["age"]       # mems列表元素是字典, 无法直接比较(字典无序), 需要将成员传入函数, 返回需要比较的值
    
    
print(sorted(mems, key=getKey))      # key在这里就是高阶函数

#
def add(a, b):
    print(a + b)


def sub(a, b):
    print(a - b)


def cal(a, b, func):
    func(a, b)


cal(1, 2, add)            # 3
cal(1, 2, sub)            # -1
```



###### **返回函数**

概念: 是指一个函数内部, 它返回的数据是另一个函数, 把这样的操作称为 "返回函数", **可以认为函数也是一种数据变量, 可以赋予, 可以返回**

```python
def getFunc(flag):
    def add(a, b):
        return a + b
    def sub(a, b):
        return a - b
    if flag == '+':
        return add
    elif flag == '-':
        return sub


func = getFunc('+')
print(func, type(func))         # <function getFunc.<locals>.add at 0x000002319E366170> <class 'function'>
print(func(1, 2))               # 3
```



###### **匿名函数**

概念: 顾名思义就是没有名字的函数, 也称为 "lambda函数" 

语法: `lambda 参数1, 参数2, ...: 表达式`

限制: 只能写一个表达式, 不能直接 `return` , 而表达式的结果就是返回值, 所以只适用于一些简单的操作处理或简短的函数

```python
mems = [{"name": "aa", "age": 17}, {"name": "bb", "age": 15}, {"name": "cc", "age": 19}]
print(sorted(mems, key=lambda x: x["name"]))
# output
[{'name': 'aa', 'age': 17}, {'name': 'bb', 'age': 15}, {'name': 'cc', 'age': 19}]
```



###### **闭包**

概念: 在函数嵌套的前提下, 内层函数引用了外层函数的变量(包括参数); 与此同时, 外层函数又把内层函数当作返回值进行返回, 这个内层函数加上所引用的外层变量, 称为"闭包"

标准格式: 

```python
def test1(a):            # 外层函数
	b = 13
	def test2():         # 内层函数
		print(a, b)      # 内层函数引用了外层函数变量(包括参数)
	return test2         # 外层函数将内层函数当作返回值进行返回
```

应用场景: 外层函数, 根据不同的参数, 来生成不同作用功能的函数

案例: 根据配置信息, 生成不同的分割线函数

```python
def line_config(content, length):
    def line():
        print("-" * (length // 2) + content + "-" * (length // 2))
    return line

func = line_config("bibao", 20)            # 生成函数
func()                                     # 多次使用时, 不用再传参, 直接使用生成过的函数
func()
# output
----------bibao----------
----------bibao----------
```

注意事项: 

1. 闭包中, 如果要修改引用的外层变量, 需要使用 `nonlocal` 进行变量声明, 否则当作是闭包内新定义的变量, 即不同于地址传递

   特别注意: `nonlocal` 仅仅适用于内层函数对应外层函数的闭包, 仅仅一层函数时不可以使用这个声明! 

```python
def test():
   num1 = 10
   num2 = 15
   def test2():
       nonlocal num2
       num1 = 13
       num2 = 19
       print(num1, num2)           # 13 19
   print(num1, num2)               # 10 15
   test2()
   print(num1, num2)               # 10 19

test()
```

2. 当闭包内引用了一个后期会发生变化的变量时, 一定要注意变量和函数所形成的闭包关系

```python
# first example
# 这个例子中for循环产生的闭包, 都是共用变量i的, 所以最后执行的时候只取决于最后i的值
def test():
    funcs = []
    for i in range(1, 4):
        def test2():
            print(i)
        funcs.append(test2)
    return funcs


newFuncs = test()
print(newFuncs)
print(type(newFuncs))
print(type(newFuncs[0]))
newFuncs[0]()
newFuncs[1]()
newFuncs[2]()


# output
[<function test.<locals>.test2 at 0x0000023A60506170>, <function test.<locals>.test2 at 0x0000023A60506200>, <function test.<locals>.test2 at 0x0000023A60506290>]
<class 'list'>
<class 'function'>
3
3
3



# second example
# 这个例子是执行test2()函数, 而test2()函数内又返回一个inner()函数, 因此将inner()函数传给了funcs, 后面调用时, inner()去在它所属的闭包内寻找num变量的值, 而在每个闭包所属的空间中, num的值都是不同的, 所以输出的结果是不同的; 在这里, 我们一定要理解, 每个闭包都有自己的num和inner(), 也就是说每个循环都产生一个新的闭包, 这里从每个inner()的存储地址都是不同的就可以看出, 然后每个inner()再去寻找自己闭包对应的num, 所以每次结果是不同的.
def test():
    funcs = []
    for i in range(1, 4):
        def test2(num):
            num = i
            def inner():
                print(num)
            return inner
        funcs.append(test2(i))
    return funcs


newFuncs = test()
print(newFuncs)
print(type(newFuncs))
print(type(newFuncs[0]))
newFuncs[0]()
newFuncs[1]()
newFuncs[2]()

# output
[<function test.<locals>.test2.<locals>.inner at 0x0000023DCBDD2200>, <function test.<locals>.test2.<locals>.inner at 0x0000023DCBDD2170>, <function test.<locals>.test2.<locals>.inner at 0x0000023DCBDD2290>]
<class 'list'>
<class 'function'>
1
2
3


# third example
# 这里例子中, 由于test2(i)在执行时, 我们选择直接执行inner()函数, 所以funcs得到的是None, 而在执行时, inner()函数与外层的test2()函数的num变量形成了一个闭包, 所以inner()函数中的num取决于闭包内此时的num, 即num = i, 其实本质上这就是每次都直接执行inner()函数
def test():
    funcs = []
    for i in range(1, 4):
        def test2(num):
            num = i
            def inner():
                print(num)
            inner()
            # return inner
        funcs.append(test2(i))
    return funcs


newFuncs = test()
print(newFuncs)
print(type(newFuncs))
print(type(newFuncs[0]))

# output
1
2
3
[None, None, None]
<class 'list'>
<class 'NoneType'>


# fourth example
# 这个例子也是利用了test2()函数和test()函数的i变量形成的闭包, 直接执行, 每次执行时i取决于闭包内此时的i变量
def test():
    funcs = []
    for i in range(1, 4):
        def test2():
            print(i)
        funcs.append(test2())  # test2()是执行函数, test2是传递函数, 注意写法不同导致的作用不同
    return funcs


newFuncs = test()
print(newFuncs)
print(type(newFuncs))
print(type(newFuncs[0]))

# output
1
2
3
[None, None, None]
<class 'list'>
<class 'NoneType'>



# fifth example
# 从空间地址看闭包本质
def test():
    funcs = []
    for i in range(1, 4):
        print(id(i))
        def test2():
            num = i
            print(id(num))
            print(num)
        funcs.append(test2)
    return funcs


newFuncs = test()
print(newFuncs)
print(type(newFuncs))
print(type(newFuncs[0]))
newFuncs[0]()
newFuncs[1]()
newFuncs[2]()

# output
2465119338736
2465119338768
2465119338800              # i指向了3的空间地址
[<function test.<locals>.test2 at 0x0000023DF7866170>, <function test.<locals>.test2 at 0x0000023DF7866200>, <function test.<locals>.test2 at 0x0000023DF7866290>]
<class 'list'>
<class 'function'>
2465119338800              # num指向的空间和最后的i一致, 说明在这里实际已经受了闭包影响
3
2465119338800
3
2465119338800
3


# sixth example
# 从空间地址看闭包本质, 本质就是变量指向数据存储空间
def test():
    funcs = []
    for i in range(1, 4):
        print("test()  running when i =", i, "  id:", id(i))
        def test2():
            num = i
            print("test2() running when num =", num, "id:", id(num))
            def inner():
                print("inner() running ans num is", num, "id:", id(num))
                # print(num)
            return inner
        funcs.append(test2())
    return funcs


newFuncs = test()
print(newFuncs)
print(type(newFuncs))
print(type(newFuncs[0]))
newFuncs[0]()
newFuncs[1]()
newFuncs[2]()

# output
test()  running when i = 1   id: 2878097981680
test2() running when num = 1 id: 2878097981680
test()  running when i = 2   id: 2878097981712
test2() running when num = 2 id: 2878097981712
test()  running when i = 3   id: 2878097981744
test2() running when num = 3 id: 2878097981744
[<function test.<locals>.test2.<locals>.inner at 0x0000029E1EF26200>, <function test.<locals>.test2.<locals>.inner at 0x0000029E1EF26170>, <function test.<locals>.test2.<locals>.inner at 0x0000029E1EF26290>]
<class 'list'>
<class 'function'>
inner() running ans num is 1 id: 2878097981680
inner() running ans num is 2 id: 2878097981712
inner() running ans num is 3 id: 2878097981744
```



###### **装饰器**

作用: 在函数名以及函数体不改变的前提下, 给一个函数附加一个额外代码, 属于python语法糖 (Syntactic sugar) 的一种

语法: 

```python
def delicate(func):
	def inner(*args, **kwargs):
		pass;
		return func(*args, **kwargs);
	return inner;
	
@delicate
def func():
	pass;
```

**本质**是为了遵循开发时下面的原则

- 开放封闭原则: 已经写好的代码, 尽可能不要修改, 如果你想要新增功能, 在原先代码的基础上, 单独进行扩展

- 单一职责: 每个函数都有自己对应的单一功能, 不要在其中添加额外的功能

**注意**: 装饰器的执行时间, 是立即执行, 也就是说, 就算没有使用被装饰的函数, 一旦加了装饰器代码, 且运行了程序, 那函数就会被装饰

实现

```python
//装饰器用法
def check(func):
    def inner():
        print("what?")
        func()
    return inner

@check
def work():
    print("hh")

work()

# output
what?
hh


//上面代码等价于
def check(func):
    def inner():
        print("what?")
        func()
    return inner

def work():
    print("hh")

work = check(work)
work()

# output
what?
hh
```

**进阶**

- 装饰器的叠加: 从上到下装饰, 从下到上执行 (从实现原理出发, 不难理解) 

- 对有参函数进行装饰: 使用**不定长参数**

  ```python
  def delc(func):
      def inner(*args, **kwargs):   # 约定俗成的参数名称, 分别代表元组和字典, 且作用是装包
          print("hh")
          func(*args, **kwargs)    # 怎样装包就怎样拆包
      return inner
  
  
  @delc
  def func1(n1, n2, name):
      print(n1, n2, name)
  
  
  @delc
  def func2(n1, n2):
      print(n1, n2)
  
  
  func1(1, 2, name='kk')
  func2(3, 4)
  
  # output
  hh
  1 2 kk
  hh
  3 4
  ```

- 对有返回值的函数进行装饰

  **原理剖析**: 在这里其实就可以对装饰器的本质有更深的理解: 首先是 `func1()` 指向函数的空间地址, 然后装饰器生效后, 调用 `delc()` 函数, `func` 和 `func1` 一样, 都指向了 `func1` 函数的空间地址, 而 `func1` 被 `delc` 返回的 `inner` 函数的空间地址赋值, 所以 `func1` 指向了 `inner` 函数的空间地址, 然后运行 `func1()` 时, 实质上是执行 `inner()` 函数, 然后 `inner()` 函数里面的 `func()` 执行的是 `func1` 原本指向的函数, 其返回的返回值再交给 `inner()` 返回; 所以我们在书写

  ```python
  def delc(func):
      def inner(*args, **kwargs):
          print("hh")
          return func(*args, **kwargs)   # 必须对应的对函数返回的结果进行返回
      return inner
  
  
  @delc
  def func1(n1, n2, n3):
      print(n1, n2, n3)
      return n1 + n2 + n3
  
  
  res1 = func1(1, 2, 9)
  print(res1)
  
  # output
  hh
  1 2 9
  12
  ```

- 带有参数的装饰器

  当我们需要传递参数给装饰器时, 由于原有的装饰器和语法糖格式无法改变, 所以我们可以给原本的装饰器的外面定义一个外部函数接受参数, 该函数返回的是装饰器

  ```python
  def getdelc(char):         # 接收参数
      def delc(func):
          def inner(*args, **kwargs):
              print("hh", 'k' * 7)
              return func(*args, **kwargs)
          return inner
      return delc            # 返回装饰器
  
  
  
  @getdelc('k')              # 写法有所不同
  def func1(n1, n2, n3):
      print(n1, n2, n3)
      return n1 + n2 + n3
  
  
  res1 = func1(1, 2, 9)
  print(res1)
  
  # output
  hh kkkkkkk
  1 2 9
  12
  ```



###### 生成器

1. **概念**: 是一种特殊的迭代器 (迭代器的抽象层级更高) , 所以, 拥有迭代器的特性, 但是, 如果打造一个自己的迭代器, 比较复杂, 需要实现很多方法, 故有一个更加优雅的方式 "生成器" 

拥有的迭代器的特性: 

- 惰性计算数据, 节省内存
- 能够记录状态, 并通过 `next()` 函数, 访问下一个状态
- 具备可迭代特性

2. **创建方式**

- 生成器表达式: 把列表推导式的 `[]` 修改成 `()` 

  ```python
  gt = (i for i in range(0, 10000) if i % 2 == 1)
  print(gt)                  # <generator object <genexpr> at 0x000001C958C57ED0>
  print(next(gt))            # 1
  print(gt.__next__())        # 3
  
  # or
  # for i in gt:
  #	 pass
  ```

- 生成函数: 函数中包含 `yield` 语句, 这个函数的执行结果就是"生成器"

  `yield` : 可以阻断当前函数的执行, 然后当使用 `next()` 函数或者 `__next__()` 都会让函数继续执行, 直至下一个 `yield` 语句, 才会被挂起暂停

  ```python
  # example 1
  def gen():
      print("xx")
      yield 1
      print("xxx")
      yield 2
      print("xxxx")
      yield 3
      print("xxxxx")
      yield 4
  
  
  t = gen()         # 执行函数, 产生一个生成器, 而函数里面的代码不会执行
  print(t)
  print(next(t))
  print(t.__next__())
  r = gen()         # 执行函数, 又能够重新产生一个新的生成器
  
  # output
  <generator object gen at 0x0000029491144040>
  xx
  1                 # 还会紧跟着打出此时的状态值
  xxx
  2
  
  
  
  # example 2
  def gen():
      for i in range(0, 10):
          yield i
      
  
  t = gen()
  for i in range(0, 5):
      print(next(t))
      
  # output
  0
  1
  2
  3
  4
  ```

3. **产生数据的方式**

生成器具有可迭代性, 故可用 `next() ` 或者 `__next__()` 函数, 或 `for in ` 访问

`next()` 和 `__next__` : 遇到对应的 `yield` 就挂起

`for in` : 遇到下一个 `yield` 前才挂起

```python
# for in 访问与next()或__next__()有所不同, 它能够
def test():
    print("hh")
    yield 1
    print("x")
    yield 2
    print("xx")
    yield 3
    print("xxx")


g = test()
for i in g:
    print(i)

# output
hh
1
x
2
xx
3
xxx         # 在这里, 它能够打印出最后一个yield后面的部分, 且不报错, 与next()或__next()__有所区别
```

4. **`send` 方法**

`send` 方法有一个参数, 指定的是上一个被挂起的 `yield` 语句的返回值, 相比于 `__next__` , 可以额外的给 `yield` 传值

注意: 如果不存在上一个 `yield` , 即第一次调用时, 则要写成 `send(None)` , 即表示是个空值, 如果强行赋值则会报错; 当然, 存在上一个 `yield` 时, 我们写为 `send(None)` 也可以, 虽然没有意义

```python
def test():
    res1 = yield 1
    print(res1)
    res2 = yield 2
    print(res2)
    res3 = yield 3
    print(res3)


g = test()
print(next(g))
print(g.__next__())
print(g.send("xxx"))           # 给上一个yield, 也就是yield 2赋值

# output
1
None
2
xxx
3
```

5. **关闭生成器**

`g.close()` : 后续如果继续调用, 会抛出 `StopIteration` 异常提示

6. **注意**

- 如果碰到 `return` , 会直接终止, 抛出 `StopIteration` 异常提示

  ```python
  def test():
      print("xx")
      yield 1
      print("xxx")
      return 9
      yield 2
  
  g = test()
  print(g.__next__())
  print(g.__next__())
  
  # output
  xx
  1
  xxx
  Error: StopIteration: 9
  ```

- 生成器只会遍历一次





###### 函数作用域

1. **概念**: 变量的作用域就是变量的作用范围, 或是可操作范围. Python 是静态作用域, 也就是说变量的作用域源于它在代码中的位置, 在不同的位置, 可能有不同的命名空间

​		**命名空间**: 是作用域的体现形式, 不同的具体的操作范围

2. **Python-LEGB:**

    Python中的变量解析顺序（Variable Resolution Order）被称为**LEGB规则**，其中LEGB是一个缩写，分别表示 **Local、Enclosing、Global 和 Built-in** 四个作用域。

    - Local: 指代函数内的作用域, 也就是局部变量. 作用范围: 当前整个函数体范围
    - Enclosing: 指代函数内部嵌套函数的作用域, 也就是嵌套作用域. 作用范围: 闭包函数
    - Global: 指代模块的作用域, 也就是全局变量. 作用范围: 当前模块(文件)
    - Built-in: 指代Python内置模块的作用域, 也就是内置变量和函数. 作用范围: 所有模块(文件)

    如果一个变量在当前作用域找不到, Python会按照上述顺序依次进行查找, 直到找到为止. 如果还是找不到, 则会抛出 NameError 异常。

    注意: Python 中**没有块级作用域** (块级作用域: 代码块中, 比如 `if` , `while` , `for` 后的代码块)

3. **基于命名空间的常见变量类型:**

	- **局部变量**: 在一个函数内部定义的变量; 作用域为函数内部
	
	  查看局部变量: `locals()` 
	
	- **全局变量**: 在函数外部, 文件最外层定义的变量; 作用域为整个文件内部
	
	  查看全局变量: `globals()` 
	
	  ```python
	  print(globals())
	  print(locals())
	  ```
	
	- **注意**
	
	  - 访问原则: 从内到外
	  - 结构规范
	  - 命名: 一般全局变量名前会加 `g_` , 便于了解
	
	-  `global` 和 `nonlocal` 的使用区别
	
	  在Python中，`nonlocal`和`global`关键字都用于修改变量作用域, 但是它们的使用方式和作用范围是不同的
	
	  `nonlocal`: `nonlocal`是Python 3新增的关键字, 用于指示变量在外层的封闭函数作用域中声明. 在函数内部使用`nonlocal`关键字声明的变量, 可以从内层函数中访问并修改外层函数中声明的同名变量.
	
	  ```python
	  def outer():
	      x = 1
	      def inner():
	          nonlocal x
	          x += 1
	          print(x)
	      inner()
	  
	  outer()  # 输出2
	  
	  该例子中，通过nonlocal关键字声明的变量x可以从内层函数inner中访问并修改外层函数outer中声明的同名变量x
	  ```
	
	  `global`: `global`关键字用于在函数内部声明一个全局变量. 在函数内部使用`global`关键字声明的变量, 可以跨越模块级别的作用域, 对全局变量进行修改.
	
	  ```python
	  x = 1
	  def foo():
	      global x
	      x += 1
	      print(x)
	  
	  foo()  # 输出2
	  
	  在上面的例子中，通过global关键字声明的变量x可以在内部函数foo中访问全局变量，并对其进行修改。需要注意的是，全局变量不推荐在函数内部声明和修改。
	  ```





#### 文件操作

###### 文件

- 数据存放的容器

- 作用: 持久性的存储数据内容

- 组成

  - 文件名: 同级目录下, 不允许同名文件存在

  - 扩展名: `.jpg` , `.avi` , `.doc` , `.xls` , `.html` ...  

    注意: 一般不同的扩展名, 对应着不同的文件格式, 不同的文件格式有着不同的存储约定, 方便程序处理

  - 文件内容

    - 文本文件: `.txt` , `.doc` , `.xls` ...
    - 二进制文件: 图片, 视频, 音乐...

###### 文件使用流程

- **打开**: `open(file, mode)` 

  语法: 

  ```
  file = open('文件路径', '模式')
  ```

  使用`open()`函数打开文件，在打开文件时需要 `file` 传递文件路径和 `mode` 指定文件打开模式。其中文件打开模式有以下几种

  - `r`: **读取文件**（默认值是以只读方式打开文件），文件的指针将会放在文件的开头。如果文件不存在会抛出异常。
  - `w`: **写入文件**（以只写方式打开文件），文件的指针将会放在文件的开头，故写入时会覆盖原始内容。如果文件不存在则会创建文件，如果文件存在则会截断文件。
  - `a`: **追加写入**，文件的指针会放在文件的结尾，故写入的内容会新增到文件末尾。如果文件不存在则会创建文件。
  - `b`: 以**二进制**形式打开文件。当打开二进制文件，如视频、图片、音频等时，在`r` , `w` 或 `a` 后需要追加 `b` 表示以二进制形式打开
  - `+`: 以**读写模式**打开文件
    - `r+` ：读写模式，打开文件后既可以读取文件内容，也可以写入文件内容，在文件开头处进行读写操作。如果文件不存在，则会抛出错误。如果文件存在，则会从文件开头开始进行读写操作并覆盖原有内容。同时支持二进制模式和文本模式。
    - `w+` ：读写模式，打开文件后既可以读取文件内容，也可以写入文件内容，在文件开头处进行读写操作。如果文件存在，则会清空原有数据；如果文件不存在，则会创建一个新的文件。同时支持二进制模式和文本模式。
    - `a+` ： 读写模式，打开文件后既可以读取文件内容，也可以写入文件内容，在文件末尾处进行读写操作，即添加内容。如果文件不存在，则会创建一个新的文件。同时支持二进制模式和文本模式。
    - `rb+`  ： 二进制读写模式，打开二进制文件后既可以读取文件内容，也可以写入文件内容，在文件开头处进行读写操作。如果文件不存在，则会抛出错误。如果文件存在，则会从文件开头开始进行读写操作并覆盖原有内容。
    - `wb+` ：二进制读写模式，打开二进制文件后既可以读取文件内容，也可以写入文件内容，在文件开头处进行读写操作。如果文件存在，则会清空原有数据；如果文件不存在，则会创建一个新的文件。
    - `ab+` ：二进制读写模式，打开二进制文件后既可以读取文件内容，也可以写入文件内容，在文件末尾处进行读写操作，即添加内容。如果文件不存在，则会创建一个新的文件。

- **读写**: 对于打开的文件，可以使用文件对象进行读写操作。

  **定位**：

  - `seek()` 

    在Python中，文件指针指向当前读/写位置，在读写文件时，Python会自动根据读写操作改变指针位置。如果需要手动改变指针位置，可以使用`seek()`函数。

    `seek()`函数用于改变当前文件指针的位置，该函数接受两个参数，第一个参数是要移动的指针位置，第二个参数是指针移动的起始位置，可选的值包括0、1、2。第二个参数为0时，表示从文件开头开始移动指针，默认值为0；第二个参数为1时，表示从当前位置开始移动指针；第二个参数为2时，表示从文件结尾开始移动指针。

    ```python
    # 如果我们想要移动指针到文件开头的第40个字节处，可以使用以下代码
    with open("example.txt", "r") as f:
        f.seek(40, 0)   # 指针从文件开头开始移动40个字节
        data = f.read()
        
    # 如果想要从文件末尾开始移动指针，可以使用以下代码：
    with open("example.txt", "r") as f:
        f.seek(-40, 2)  # 指针从文件末尾向前移动40个字节
        data = f.read()
    ```

    注意： `seek()`函数只能在**二进制模式中使用**。在文本模式中，指针位置是按照字符数进行计算的，因此移动指针可能会导致读取到错误的数据。

  - `tell()`

    在Python中，`tell()`函数用于返回当前在文件中的位置，它返回值表示文件指针（也称偏移量）相对于文件开头的字节数。`tell()`方法不需要参数，调用它将会返回当前文件位置。

    ```python
    # 例如，下面的代码打开一个文件，从文件开头读取前 10 个字符，然后使用tell()方法获取当前文件指针位置：
    with open('example.txt', 'r') as f:
        content = f.read(10)  # 读取前10个字符
        pointer_position = f.tell()
        print(f"当前指针位置为：{pointer_position}")
        
    # 输出：当前指针位置为：10
    ```

    在读取与写入文件时，`tell()`方法可以帮助我们了解文件处理的情况，方便我们做调试和记录。

  **判断**

  ```python
  # 操作文件之前先判断文件是否可读，可以增加代码健壮性
  if f.readable():
  	pass
  
  # 操作文件之前先判断文件是否可写，可以增加代码健壮性
  if f.writeable():
      pass
  ```

  常见的文件**读取方法**有：

  - `read(size=-1)`: 读取文件内容，可以指定读取的字符数，如果不指定则读取整个文件的内容。
  - `readline(size=-1)`: 读取文件的一行内容（包括换行符），如果指定了参数`size`，则最多读取指定个数的字符。
  - `readlines(hint=-1)`：从文件中读取多行内容（包括换行符），并返回一个字符串列表。如果指定了参数`hint`，则每次最多读入前`hint`行
  - `for in` ：可以直接遍历 `f` 本身（因为 `f` 本质是迭代器）；也可以遍历行列表

  - 注意：`read()` 和 `readlines()` 能一次性读取全部内容，加载到内存中，比较耗内存，但多次处理时更加快速便捷，性能比较高；`readline` 和 `for in` 则适用于文件比较大的时候，可以按行加载，节省内存，相比于之前两种读取方法性能则较低‘

  常见的文件**写入方法**有：

  - `write()`: 向文件中写入内容，返回值是写入的字节长度
  - `writelines()`: 向文件中写入多行内容。

  示例:

  ```python
  # 读取文件
  file = open('example.txt', 'r')
  contents = file.read()
  print(contents)
  file.close()
  
  # 写入文件
  file = open('example.txt', 'w')
  file.write('hello, world!')
  file.close()
  ```

- **关闭**: 使用完文件之后需要使用`close()`方法关闭文件，释放该文件所占用的资源， 且缓存区的数据内容会被立即清空到磁盘文件，当然，必要时候也可以使用 `flush()` 函数立即清空缓存区的数据内容到磁盘空间

  ```python
  file.close()
  ```

  `with` 语句: 使用`with`语句可以自动关闭文件，不需要手动调用`close()`方法。当`with`语句与文件对象配合使用时，在语句块中对文件的操作结束后，会自动调用`close()`方法释放资源。

  ```python
  with open('example.txt', 'r') as file:
      contents = file.read()
      print(contents)
  ```

以上是Python中文件的基本使用流程，使用文件时需要注意关闭文件以避免资源浪费和数据丢失的情况发生。

###### 文件的相关操作

`os`模块是Python中一个非常重要的模块，它提供了许多用于操作文件和目录的函数。

- 获取当前工作目录

使用`os.getcwd()`函数可以获取当前工作目录的路径。

```python
import os

print(os.getcwd())
```

- 切换工作目录

使用`os.chdir(path)`函数可以改变当前工作目录。其中，`path`为需要切换到的目标工作目录的路径。

```python
import os

os.chdir('/home/user/workspace')
print(os.getcwd())
```

- 获取目录列表

使用`os.listdir(path)`函数可以获取一个目录下所有文件和子目录的列表。其中，`path`为需要获取列表的目标目录的路径。

```python
import os

files = os.listdir('/home/user')
for file in files:
    print(file)
    
# 可根据'.'进行递推
os.listdir('./')  当前目录
os.listdir('../')  当前目录的上一级目录
...
```

- 创建子目录

`os.mkdir()` 函数用于创建一个新的目录。其语法为 `os.mkdir(path[, mode])` ，其中，`path`是您要创建的文件夹的路径，可以是相对路径或绝对路径。`mode`是可选参数，可以设置文件夹的访问权限，默认为0777（即所有用户都有完全访问权限）

```python
import os

# 创建文件夹 test
os.mkdir("test")

# 创建具有权限 777 的文件夹 test2
os.mkdir("test2", 0o777)
```

以上代码将在当前工作目录中创建一个名为`test`的文件夹和一个名为`test2`的文件夹，`test2`文件夹具有777的访问权限。

需要注意的是，如果文件夹已经存在，`os.mkdir()`函数将会引发异常。此时，您可以使用`os.path.isdir()`函数检查文件夹是否存在，或使用`os.makedirs()`函数创建多层目录。例如：

```python
if not os.path.isdir("test"):
    os.mkdir("test")
```

或者：

```python
os.makedirs("/path/to/new/folder")
```

这将创建一个`new`文件夹，它在`/path/to/`目录下，并且可以在创建`/path/to/`的同时创建任意数量的中间文件夹。

- 删除文件或目录

使用`os.remove(path)`函数可以删除一个文件， `os.rmdir(path)`可以删除一个空目录， `os.removedirs(path)`可以递归删除一个目录树，包括所有子目录和文件。

```python
import os

os.remove('example.txt')
os.rmdir('empty_dir')
os.removedirs('parent_dir')
```

- 文件重命名

  - `os.rename(src, dst)`函数用于将**一个**文件或者目录从旧路径`src`重命名为新路径`dst`。例如：

  ```python
  import os
  
  os.rename('/path/to/old_name', '/path/to/new_name')   # 如果path或to不存在，即有目录不存在就会报错
  ```

  - `os.renames(old_file_name, new_file_name)`函数也可以重命名文件，但它比`os.rename()`函数更强大，因为它可以递归地移动多个文件和目录。例如：

  ```python
  import os
  
  os.renames('/path/to/old_folder_name', '/path/to/new_folder_name')
  ```

  在该函数中，如果文件夹不存在，则会被创建。`renames()`函数会递归地遍历整个文件/目录树，将所有名称中包含旧名称的文件和目录重命名为新名称。如果目标文件/目录已经存在，则会触发一个异常。

  所以，主要区别在于`os.rename()`只能用于单个文件或目录的重命名，而`os.renames()`可以递归地移动多个文件和目录，并且会**自动创建目标目录**（会自动创建一个修改前的目标目录），但是如果目标文件或目录已经存在，则会触发异常。

以上是与文件操作相关的一些常用函数。请注意，文件操作通常需要在受限的权限下进行，如操作系统或文件系统的限制。因此，这些操作可能会受到权限的限制。在进行文件操作之前，请先确保您有足够的权限进行相应操作。

**Tips:**

报错: "在vscode使用相对路径的python应用报错找不到该文件"

原因: 在 vscode 编译器下, 编写运行以上代码大多会提示报错, 找不到文件. 这是因为我们使用了相对路径, 而相对路径和终端的cwd有密切联系. ( `cwd`是当前工作目录 **Current Working Directory** 的缩写，指的是在终端中执行命令时的当前目录 ) 在vscode中, 子文件夹内的文件的相对路径的基准不再是该文件所在路径, 而是用 vscode 打开的根目录作为整个项目的相对路径的基准. 项目中所有文件的相对路径都是指项目根目录. 正是由于 vscode 默认使用项目文件夹根目录作为工作目录(cwd), 才使得子文件夹中的程序无法使用相对路径.

解决方法: 

```python
#加上下面代码

import os, sys

os.chdir(sys.path[0])

#然后就可以愉快使用相对路径了
```

总结: 在命令行中运行 py 文件, 工作目录取决于当前命令行所在的目录,由于通常我们会将命令行 cd 到 py 文件同目录下(这样没有执行的时候不需要敲一堆路径，python src/bala/bala/program.py 之类的), 工作目录就与 py 文件同目录, 生成的文件自然在这个目录下. 如果从 vscode 中启动，如果没有修改 launch.json 中的 cwd 的值，默认以 "${workspaceFolder}" 作为工作目录(项目根目录)，所以相对路径的起点也要从这个目录开始，需要我们手动进行修改。

###### 案例

1. 文件复制

2. 文件分类

   ```python
   import os
   import shutil
   
   path = "files"
   if not os.path.exists(path):   # 容错处理
       exit()
    
   os.chdir(path)                 # 转移当前目录
   file_list = os.listdir("files")
   
   for file_name in file_list:
       # 分解文件后缀名
       index = file_name.rfind('.')
       if index == -1:            # 容错处理
           continue
       extension = file_name(index + 1:)
       # 不存在该目录则创建
       if not os.path.exists(extension):
           os.mkdir(extension)
       # 移动到对应的目录下
       shutil.move(file_name, extension)
   ```

3. 生成文件清单

   ```python
   # 递归
   import os
   def listFiles(dir):
   	file_list = os.listdir(dir)
   	for file_name in file_list:
   		new_filename = dir + "/" + file_name
           # 判定是否是目录
   		if os.path.isdir(new_filename):
   			print(new_filename)
   			listFiles(new_filename)
   		else:
               # 打印文件名称
   			print("\t" + file_name)
   	print("")
   
   listFiles("files")
   ```





## 面向对象

#### 基本理论

**对象**

对象是指在内存中分配的一块区域，有状态和行为。在Python中，每个对象都有自己的标识、类型和值。

Python中的体现: Python是一门特别**彻底的面向对象编程** (OOP) 的语言. 其他语言可能包括基本数据类型 (int, float, bool...) 和对象类型(string, arrat...), 而Python中都是对象类型 (int, float, bool, list). 

**面向对象&面向结果**

Python既是面向过程的，也是面向对象的编程语言。

- **面向过程编程**的核心是**过程**，是一种以顺序、选择和循环为主线的程序设计方法。其中函数是一种重要的组织代码的方式，使用函数封装代码，便于复用和维护。在Python中，使用`def`语句定义函数，对函数进行调用可以实现程序的不同功能。面向过程编程的优点是逻辑清晰，执行效率高，但是代码可读性差，并且不易扩展和维护。

- **面向对象编程**的核心是**对象**，是一种以封装、继承和多态为主线的程序设计方法。其中类是一种重要的组织代码的方式，使用类可以定义对象的属性和方法，进而实现一个个具有特定功能的对象。在Python中，使用`class`语句定义类，对类进行实例化可以创建对象。面向对象编程的优点是代码可读性强，易于扩展和维护，并且易于重用代码，但是执行效率相对较低。

Python是一种支持多种编程范式的语言，既可以使用面向过程的方式编写程序，也可以使用面向对象的方式编写程序。通常情况下，面向对象编程比面向过程编程更加适用于大型和复杂的程序，而面向过程编程则更加适合简单的处理过程。因此，需要根据具体的项目需求和程序规模选择合适的编程范式。



#### **类**

**概念**: 在Python中，面向对象的编程是通过定义类的形式来实现的，类是一种抽象数据类型，表示一类具有相同属性和行为的对象

###### **定义**

类的定义以`class`关键字开头，其后是类名，然后是一个冒号`:`，接着是类的定义体，类的定义体中可以定义类的属性和方法

```python
class Name:
    pass
```

类的**实例化**就是创建类的一个对象。可以使用类名后面跟一对括号`()`来创建类的对象

创建好对象后，可以通过对象名访问其属性和方法

```python
print(my_computer.brand)
my_computer.describe()
```



###### **属性**

**对象属性**

- 给对象添加属性

  ​	对于已经创建的对象，可以在任何时候添加属性。添加属性的方法有两种：

  - 直接给对象添加属性, 可以使用`.`符号，直接给对象添加一个新属性

    ```python
    class Person:
        pass
    
    person = Person()
    person.name = "Tom"   # 直接给person对象添加一个name属性，值为"Tom"
    ```

  - 使用`setattr`函数给对象动态添加属性

    `setattr`函数接受3个参数，第一个参数是要添加属性的对象，第二个参数是属性的名字，第三个参数是属性的值

    ```python
    class Person:
        pass
    
    person = Person()
    setattr(person, "age", 18)   # 动态给person对象添加一个age属性，值为18
    ```

    需要注意的是，虽然Python允许在运行时动态地给对象添加属性，但这样做可能会让代码变得难以理解和维护。最好在类的定义中指定所有属性，避免动态添加属性导致代码的不确定性。

- 删除对象属性

  使用 `del` 可以直接删除对象属性

- 查看对象属性

  在Python中，每个正常的对象都有一个字典属性 `__dict__`，它存储了该对象的所有属性。这个字典是一个包含属性名称和对应值的映射，可以通过 `__dict__` 属性来访问和更新。

  ```python
  # 例如
  class MyClass:
      def __init__(self):
          self.a = 1
          self.b = 2
  
  my_object = MyClass()
  print(my_object.__dict__)
  
  # 运行代码会输出一个字典，里面包括了 `my_object` 的全部属性：
  {'a': 1, 'b': 2}
  ```

  `__dict__` 属性对于动态地添加或修改对象属性非常有用，可以直接通过操作字典来完成。但是需要注意，对于某些特殊类来说，`__dict__` 属性可能会被禁用或者限制。或者说，默认来说，对于类的 `__dict__` 属性，是只读而不能修改的；对象的 `__dict__` 才可以修改

  ```python
  class Person:
  	pass
  
  one = Person()
  one.__dict__ = {"name": "hh", "age": 19}
  print(one.name, one.age)   # hh 19
  one.__dict__["age"] = 13
  print(one.age)             # 13 
  ```

  

**类属性**

- 查看类属性

  同样可以使用 `__dict__` 进行查看, 或者直接 `class.属性`  或者 `对象.属性` 

  Python对象属性查找机制: **优先**到对象自身去查找属性, 找到则结束, 如果没找到, 则根据 `__class__` 找到对象的类, 在这个类中进行查找, 所以我们也可以动态修改对象 `__class__` 指向的类, 从而修改对象所属的类

  ```python
  class One:
      pass
  
  class Two:
      pass
  
  ret = One()
  print(ret.__class__)       # <class '__main__.One'>
  ret.__class__ = Two
  print(ret.__class__)       # <class '__main__.Two'>
  ```

- 添加类属性

  可以在定义类的时候直接添加, 也可以后续在实现过程中使用 `类.属性` 进行添加, 注意无法通过对象直接添加类属性

- 修改类属性

  使用 `类.属性` 或者 `对象.属性` 进行修改, 但是 `对象.属性` 修改时不影响类的属性, 也可以理解为对象只是自己为属性创建了一个新的值, 也就是说无法通过对象修改类属性

- 删除类属性

  使用`del` 删除即可, 同样无法通过类的对象删除类属性

- 内存存储问题
  - 一般情况下, 属性存储在 `__dict__` 的字典中, 有些内置对象没有这个 `__dict__` 属性; 一般对象可以直接修改 `__dict__` 属性, 但类对象的 `__dict__` 为只读, 默认无法修改, 不过可以通过 `setattr` 方法修改 
  - 类属性被各个对象所共享

- 限制类属性

  在 Python 中，我们可以使用 `__slots__` 来限制一个类的属性，防止在运行时动态地给对象添加新的属性。 `__slots__` 是一个特殊的属性，它是一个类属性，定义为一个字符串列表或一个字符串元组，其中每个字符串表示一个属性名。

  当一个类定义了 `__slots__` 属性时，该类的实例将不能动态地添加新的属性，只能使用 `__slots__` 中定义的属性。这样一来，实例所需要的内存空间就更小了，程序的执行速度也会更快。

  例如

  ```python
  class Person:
      __slots__ = ('name', 'age')
      
      def __init__(self, name, age):
          self.name = name
          self.age = age
  
  person = Person('Tom', 18)
  person.gender = 'male'
  #AttributeError: 'Person' object has no attribute 'gender'
  ```

  在上面的代码中，我们定义了 `Person` 类，其中 `__slots__` 属性包含了 `name` 和 `age` 两个属性。当我们尝试为 `person` 实例添加 `gender` 属性时，就会抛出 `AttributeError` 异常。因此，使用 `__slots__` 可以限制我们动态地为实例添加任意属性的能力。

  需要注意的是，使用 `__slots__` 会让代码变得更加脆弱。因为实例属性的数量是限制的，所以如果你在 `__slots__` 中添加属性名时出现错误，就会导致程序运行出现各种奇怪的问题。

**类和对象属性总结**:

- 类本质上也属于对象, 只是在程序中, 为了区分出抽象级或者相互之间的层次, 才有类和对象的关系

- 类属性和对象属性的查看, 修改, 添加和删除操作语法基本是一致的. 区别就是, 类属性的添加还可以写在类的构造中; 修改类属性, 只能通过类进行修改, 不能通过对象进行修改

- 再次强调, 属性本质是存储在 `__dict__` 字典中, 访问对象属性时, 先到对象本身查找, 查找不到时, 就会在其所属的类中再继续查找; 同时, 对于一个 `对象.属性` 或者 `类.属性` , 我们在使用时, 应该清楚该语法在此处是查询, 还是修改, 抑或新增

  ```python
  class Person:
  	age = 19
  
  
  print(id(Person.age))
  print(Person.age)      # 查询
  one = Person()
  print(id(one.age))
  print(one.__dict__)    # 特别注意: 此时对象的__dict__并没有任何内容! 这也证明了上文提及的查找机制.
  one.age = 19           # 新增
  print(one.__dict__)    # 注意, 此处相比之前, 多了'age': 19
  print(id(one.age))
  one.age = 13           # 修改
  print(one.age)
  print(id(one.age))
  
  # 输出
  2030017512240
  19
  2030017512240
  {}
  {'age': 19}
  2030017512240
  13
  2030017512048
  ```





###### **方法**

**概念**:  方法是一段代码，它可以在类或对象的上下文中调用并执行任务。方法包含在类中，并且可以仅在类实例化后通过该对象执行。方法是类中的函数，用于执行特定的任务。在Python中，方法是类中定义的一种函数。

**划分**

- 实例方法

  这是最基本的方法类型，它与类实例相关联并允许访问实例属性和方法。通常，实例方法的第一个参数称为 `self`，并将实例作为参数传递。

  ```python
  class MyClass:
      def instance_method(self, x, y):
          print(self, x, y)
          
  # 标准调用
  obj = MyClass()
  obj.instance_method(3, 4) #Output: <__main__.MyClass object at 0x00000208EF3B8A00> 3 4
  
  # 间接调用, self参数可以传参
  func = MyClass.instance_method 
  func(1, 2, 3)             #Output: 1 2 3
  
  ```

  **调用**

  - 标准调用 (常用)
    使用实例调用实例方法, 不用手动传, 解释器本身会自动把调用对象本身传递过去, 如果实例方法没有接受任何参数, 则会报错, 即一个自动传, 一个不接收, 会报错; 还要注意的是, 即便函数第一个参数不写 `self` , 解释器也会将对象本身传到第一个参数, 也就是说写法不会改变解释器的传递, 也可以理解为, 我们一定要一个参数来接收对象, 这个参数我们通常写为 `self` 
  - 其他调用: 使用类调用, 间接调用, 本质就是直接找到函数本身来调用

- 类方法

  这种方法与整个类相关联，而不是与类实例相关联。它们被作为从类本身调用的方法定义，而不是从类的实例调用。编写函数前要加一个装饰器 `@classsmethod`,  通常，它们的第一个参数称为`cls`，并将类作为参数传递。

  ```python
  class MyClass:
      @classmethod
      def class_method(cls, x, y):
          return x + y
  
  print(MyClass.class_method(3, 4)) #Output: 7
  ```

- 静态方法

  这种方法类似于类方法，但与整个类和类实例都没有绑定, 使用前要添加装饰器 `@staticmethod` . 静态方法通常用于较小的任务，不需要访问类的属性或方法。它们没有参数 `self` 或 `cls` ，并且可以由类本身或类的实例引用。

  ```python
  class MyClass:
      @staticmethod
      def static_method(x, y):
          return x + y
  
  print(MyClass.static_method(3, 4)) #Output: 7
  
  obj = MyClass()
  print(obj.static_method(3, 4)) #Output: 7
  ```

- 注意：
  - 总之，Python中的方法有三种类型：实例方法、类方法和静态方法。实例方法与特定的类实例相关联，类方法与整个类相关联，而静态方法与整个类和类实例都没有绑定。需要根据需求选择适当的方法类型。
  - 划分依据：方法的第一个参数必须要接接收的数据类型
  - 不管是哪一种方法，都是存储在类的 `__dict__` 字典中，没有存储在实例中, 因为函数也可以视为对象, 作为 `value` 值
  - 不同类型方法的调用方式不同, 调用的时候把握的原则是, 无论是我们自己传递还是解释器帮我们传递, 最终要保证不同类型的的方法第一个参数接收到的数据是对应的数据

###### 元类

**概念**

元类是Python面向对象编程中的高级概念之一. 元类实际上就是用来创建类的类. 在Python中, 所有的类都是通过 `type`(元类)动态创建的. 在Python中, 元类实际上就是一个可以创建类的类. 它可以控制类的生成过程, 决定类的属性, 方法等行为, 甚至可以在类创建之前修改类的定义. 元类的实例是类对象, 它可以定义新的类

```python
class MyClass:
    def instance_method(self, x, y):
        print(self, x, y)
        

print(MyClass.__class__)          # output: <class, 'type'>
print(int.__class__)              # output: <class, 'type'>
print(str.__class__)              # output: <class, 'type'>
print(int.__class__.__class__)    # output: <class, 'type'>
```

**类对象创建**

1. **方式**

- 使用 `class` 关键字, 利用解释器会根据我们的类描述自动创建对应的类对象

- 调用 `type` 函数进行手动创建

  ```python
  def run(self):
      print(self)
  
  
  func = type("Cla", (), {"count": 0, "run": run})
  print(func)
  print(func.__dict__)
  
  obj = func()
  print(obj)
  obj.run()
  
  #output
  <class '__main__.Cla'>
  {'count': 0, 'run': <function run at 0x000002821F856050>, '__module__': '__main__', '__dict__': <attribute '__dict__' of 'Cla' objects>, '__weakref__': <attribute '__weakref__' of 'Cla' objects>, '__doc__': None}
  <__main__.Cla object at 0x000002821F8889D0>
  <__main__.Cla object at 0x000002821F8889D0>
  ```

不管是什么方式, 本质都是通过 `type` 元类, 来创建类对象, 这也是元类的作用, 但是也并不是所有类对象的创建都是通过 `type` 元类, 

2. **流程**
   1. 检测类中是否有明确 `__metaclass__` 属性
   2. 检测父类中是否存在 `__metaclass__` 属性
   3. 检测模块中是否存在 `__metaclass__` 属性
   4. 通过内置的 `type` 这个元素, 来创建这个类对象

3. 元类的应用场景
   - 拦截类的创建
   - 修改类
   - 返回修改之后的类

###### 描述

描述方式

~~~python
class Person:
	```
	类的描述, 类的作用, 类的构造函数等等;
	Attributes:
		类属性的描述
	```
	def func(self)
        ```
        参数含义, 参数类型int, 是否有默认值
        返回结果, 返回数据类型
        ```
	
help(Person)
~~~

生成项目文档

- 方式1: 使用内置模块 `pydoc` 

  步骤:

  - 查看文档描述 `python3 -m pydoc` 模块名称
  - 启动本地服务, 浏览文档 `python3 -m pydoc -p`
  - 生成指定模块 `html` 文档 `python3 -m pydoc -w` 模块名称

  注意: 具体细节可以在cmd窗口输入`python3 -m pydoc -p` , 能得到具体的指令描述 

- 方式2: 使用第三方模块 `Sphinx` , `epydoc` , `doxygen`  



###### 属性访问权限

**概念**: 属性访问权限指的是对类成员的公开程度。Python 中的属性有三种访问权限：公开的（public）、保护的（protected）和私有的（private）

**类型**

- 共有属性

  - 允许类内部访问, 子类内部访问 
  - 模块内其他位置: 允许父类和派生类, 父类实例和派生类实例访问
  - 跨模块访问: 通过 `import` 和 `from 模块 import *` 形式导入也可访问

- 受保护属性

  受保护属性以单下划线 `_` 为前缀. 

  当使用单下划线 `_` 为前缀时，Python并不会将属性或方法视为私有，只是表示这是一个受保护属性或方法。可以在类的外部访问受保护属性或方法，只是作为一种约定俗成的编程风格，建议只在类的内部或子类中访问这些属性和方法. 

  - 允许类内部访问, 子类内部访问

  - 模块内其他位置: 可以访问, 但是会编译器会发出警告

  - 跨模块访问: 以 `_` 开头的全局变量, 在其他文件以 `import` 形式导入, 可以访问, 会发出警告;  `from 模块 import *` 形式导入, 若变量放入 `__all__` 列表中, 则可以访问, 且不会有警告, 否则将无法访问

    ```python
    __all__ = ["_x"]
    _x = 79
    ```

- 私有属性

  通过在属性或方法名前添加双下划线 `__ `来将其私有化

  - 可以在类内部访问, 不能在子类内部访问
  - 也不允许在模块内其他位置进行访问
  - 跨模块访问: 以 `__` 开头的全局变量, 系统会识别为以 `_` 开头的变量, 例如 `__x` 识别为以 `_` 开头的 `_x` 变量, 所以权限与受保护属性一致, 即可参照单下划线的访问原则.

```python
class MyClass:
    def __init__(self):
        self.mypublicattribute = 1        # public attribute
        self._myprotectedattribute = 2    # protected attribute
        self.__myprivateattribute = 3     # private attribute
```

**注意**

-  Python 中并没有真正的私有化支持, 但是可以通过下划线完成伪私有的效果, 类属性(方法) 和实例属性(方法) 遵循相同的规则; 也就是说, 本质上其实没有真正的私有化, 只是基于名字重整（Name Mangling）, Python 自动将其重命名, 从而使得我们在某些区域无法直接通过表面的名称来调用属性, 但是通过使用系统内存储的真正名称, 还是能够调用, 所以并没有真正的私有化.

- 有些代码可能会出现 `xx_` 或者 `__xx__` 形式的变量, 这只是出于规范, 并不涉及访问权限, 可以用于区分系统关键字; 通常我们使用的是 `xx_` 来回避关键字, 而 `__xx__` 通常表示是系统内置的变量或函数, 我们自己命名时尽量避免使用这种命名方法. 

**实现机制**

名字重整(Name Mangling)

名字重整指的是一种在类定义中使用的特殊命名约定，用于将变量和函数名与类名区分开来，以避免名称冲突。该机制使用双下划线“__”作为前缀，将变量和函数名重命名成类名和前缀的组合。

主要分为两种形式

- 双下划线前缀和类名重命名：在类定义中，以双下划线 `__` 为前缀的变量和函数名将被重命名为 `_类名__变量名` 或`_类名__函数名` 的形式。这种形式一般用于避免变量和函数名与类的属性和方法发生冲突。

- 单下划线前缀和类名重命名：在类定义中，以单下划线 `_` 为前缀的变量和函数名将被重命名为`_类名_变量名` 或 `_类名_函数名` 的形式。这种形式一般用于指示变量和函数是受保护的，建议只在类内部或派生类中使用。

  ```python
  # vscode python3.10.8版本下的文字重整, 显然在受保护属性上有所区别
  class MyClass:
      _my_protected_variable = 2
      __my_private_variable = 3
  
      def _my_protected_function(self):
          print("Protected!")
  
      def __my_provited_function(self):
          print("Privated!")
  
      def my_public_function(self):
          print(self._my_protected_variable)
          print(self.__my_private_variable)
          self._my_protected_function()
  
  
  print(MyClass.__dict__)
  # output
  {'__module__': '__main__', '_my_protected_variable': 2, '_MyClass__my_private_variable': 3, '_my_protected_function': <function MyClass._my_protected_function at 0x0000026D476C6170>, '_MyClass__my_provited_function': <function MyClass.__my_provited_function at 0x0000026D476C6200>, 'my_public_function': <function MyClass.my_public_function at 0x0000026D476C6290>, '__dict__': <attribute '__dict__' of 'MyClass' objects>, '__weakref__': <attribute '__weakref__' of 'MyClass' objects>, '__doc__': None}
  ```

需要注意的是，名字重整只对**类定义内**的变量和函数有效，对类定义之外的变量和函数没有影响，因此直接访问“`_类名_变量名`”或 `_类名_函数名` 仍然是可以的，但是不建议这样使用。另外，名字重整只是一种约定，并没有强制性规定，因此在某些情况下可能会出现命名冲突。而且, 不同解释器的名字重整规则可能不一样, 比如有的解释器并不会重整单下滑线开头的受保护属性. 

```python
class Person:
    def __init__(self) -> None:
        self.__age = 19


a = Person()
a.__age = 18
print(a.__dict__)        # {'_Person__age': 19, '__age': 18}
print(a._Person__age)    # 19 (No advised!)
print(a.__age)           # 18
```

**补充**

1. **只读属性**

   概念: Python中的只读属性指的是只能读取不能修改的类成员。在一些应用场景中，我们可能需要保护某些属性，避免外部程序不小心修改它们而导致程序出现问题，例如数据库连接信息或者配置文件中的信息等。定义只读属性可以有效地解决这个问题。

   - 方法1：使用·`property()` 

     ```python
     class MyClass(object):
         def __init__(self):
             self._my_var = 3
     
         def get_my_var(self):
             return self._my_var
         
         my_var = property(get_my_var)
     
     Stu = MyClass()
     print(Stu.my_var)   # 3
     ```

   - 方法2：使用 `@property` 

     ```python
     class MyClass(object):
         def __init__(self):
             self._my_var = 3
     
         @property
         def my_var(self):
             return self._my_var
     
     Stu = MyClass()
     print(Stu.my_var)   # 3
     ```

   - 方法3：使用 `__setattr__`

     ```python
     class MyClass(object):
         def __setattr__(self, key, value) -> None:
             print(key, value)
             if key == "age" and key in self.__dict__.keys():   # 先判断是否为我们要设置的可读属性名称
                 print("You can't change this value.")
             else:
                 # 下面不能使用self.age = value，否则就又是调用了__setattr__，会死循环
                 self.__dict__[key] = value
     
     
     Stu = MyClass()
     Stu.age = 18
     print(Stu.age)
     Stu.age = 19
     print(Stu.age)
     print(Stu.__dict__)
     
     #output
     age 18
     18
     age 19
     You can't change this value.
     18
     {'age': 18}
     ```

     

2. **经典类和新式类**

   在Python中，类可以分为经典类和新式类。

   经典类是Python早期版本中的类定义方式，不需要继承自 `object` 类。当Python 3.x 中定义一个类时，如果没有显式指定其继承自任何类，那么默认会继承自 `object` 类。这种默认继承方式被称为新式类。Python中的新式类于2001年正式引入。

   新式类和经典类在多继承、super() 函数调用、特殊方法的解析顺序等方面表现不同。下面展示了一个新式类和经典类的定义和使用示例：

   - 经典类：

   ```python
   class OldStyle:
       def __init__(self):
           self.attr = 0
   
   class ChildOldStyle(OldStyle):
       def __init__(self):
           OldStyle.__init__(self)
           self.child_attr = 1
   
   c1 = ChildOldStyle()
   print(c1.attr)
   ```

   在 Python 2.x 版本中，如果没有显式指定类继承自 `object`，那么定义出来的类为经典类。在 Python 3.x 版本中，所有定义的类都默认继承自对象（object）类，如果没有指定，则也是继承自 object 类，即默认为新式类。`OldStyle.__init__(self)` 表示 `ChildOldStyle` 继承了 `OldStyle` 类。

   - 新式类：

   ```python
   class NewStyle(object):
       def __init__(self):
           self.attr = 0
   
   class ChildNewStyle(NewStyle):
       def __init__(self):
           super().__init__()
           self.child_attr = 1
   
   c2 = ChildNewStyle()
   print(c2.attr)
   ```

   在 Python 3.x 版本中，如果采用 `class NewStyle(object):` 这种方式定义类，则该类为新式类。子类 `ChildNewStyle` 继承自父类 `NewStyle`，`super().__init__()` 表示调用父类构造函数，即初始化 `NewStyle` 类的 `self.attr`，然后才能调用 `c2.attr`。与经典类不同，新式类必须继承自 `object`。

   新式类相比经典类提供了更多的特性，如多重继承、属性修饰符等，也更符合面向对象的设计理念，因此在 Python 中推荐使用新式类。但在 Python 2.x 版本中，如果不需要使用新式类的特性，经典类仍然可有实用价值。而在 Python 3.x 版本中，经典类已经被弃用，只允许使用新式类。在 Python 3.x 版本中，我们要使用新式类最好也显式地表示出来，这样的话如果代码被移植到 Python 2.x 版本中也能很好的兼容。

3. `property` 

   用于把类中的方法变成属性，从而控制对类属性的访问和修改，使得代码更加简洁和易读。它实现对类属性的取值和赋值的控制和封装，从而达到保护属性的目的。它在新式类和经典类中的使用方法是不同的

   **property() 函数**

   语法：

   ```python
   property(fget=None, fset=None, fdel=None, doc=None) -> property attribute
   说明：
   fget 是获取属性值的方法
   fset 是设置属性值的方法
   fdel 是删除属性值的方法
   doc 是属性描述信息。如果省略，会把 fget 方法的 docstring 拿来用（如果有的话）
   ```
   
   **@property 装饰器**
   
   `@property` 语法糖提供了比 `property()` 函数更简洁直观的写法。
   
   ```python
   被 @property 装饰的方法是获取属性值的方法，被装饰方法的名字会被用做 属性名
   被 @属性名.setter 装饰的方法是设置属性值的方法
   被 @属性名.deleter 装饰的方法是删除属性值的方法
   ```
   
   **用法**
   
   - 新式类
   
     - 第一种方法
   
       使用 `@property` 装饰器和 `setter` 方法定义 `getter` ， `setter` 和 `deleter` 方法。示例代码如下，需要注意使用这种方法的时候，不同的方法的名称必须要一致，且不能和变量名重合，否则会死循环，示例中 `_my_var` 使用的是 `my_var` 属性名称
   
         ```python
       class MyClass(object):
           def __init__(self):
               self._my_var = None
       
           @property
           def my_var(self):
               print("Getting _my_var")
               return self._my_var
       
           @my_var.setter
           def my_var(self, value):
               print('Setting _my_var to %s' % value)
               self._my_var = value
       
           @my_var.deleter
           def my_var(self):
               print("Deleting _my_var")
               del self._my_var
       
       
       Stu = MyClass()
       Stu.my_var = "hh"
       print(Stu.my_var)
       del Stu.my_var
       
       #output
       Setting _my_var to hh
       Getting _my_var
       hh
       Deleting _my_var
         ```
     
     - 第二种方法
     
       这种方法需要使用 `property` 方法，重写函数，并定义 `setter` ，`getter` 和 `deleter` 方法。示例代码如下，需要注意的是这里的方法名称是不同的，这里也要注意新包装成的属性名称与变量名称不能相同
     
       ```python
       class MyClass(object):
           def __init__(self):
               self._my_var = None
       
           def get_my_var(self):
               print("Getting _my_var")
               return self._my_var
       
           def set_my_var(self, value):
               print('Setting _my_var to %s' % value)
               self._my_var = value
       
           def del_my_var(self):
               print("Deleting _my_var")
               del self._my_var
       
           my_var = property(get_my_var, set_my_var, del_my_var, "Describtion")
           
       
       Stu = MyClass()
       Stu.my_var = "hh"
       print(Stu.my_var)
       print(MyClass.my_var.__doc__)   # 注意要使用 class.attribution.__doc__
       del Stu.my_var
       # output
       Setting _my_var to hh
       Getting _my_var
       hh
       Describtion
       Deleting _my_var
       ```
   
   - 经典类
   
     经典类中property 的用法与新式类基本一致，区别就是经典类中无论是哪一种方法，都是能实现`get`的功能，也就是说只读，并不能设置或者删除，尽管在编写的时候可能能够顺利编写且不会报错。

4. `__setattr__` 

   `__setattr__`是Python中的一个特殊方法，用于自定义类的属性赋值。当我们使用一个类的对象来设置属性值时，如果这个类中定义了`__setattr__`方法，那么Python就会调用这个方法来实现属性设置的逻辑。

   `__setattr__`方法需要至少两个参数，第一个参数是`self`，代表类的实例对象，在`__setattr__`方法中不用特别传递，Python解释器会自动传递。第二个参数是属性名，第三个参数是属性值。

   我们可以在`__setattr__`方法中**自定义属性赋值的逻辑**。例如，我们可以对属性进行验证、修改或记录属性赋值的历史记录等，包括上面的只读属性的设置。

   下面是一个简单的例子来演示`__setattr__`的用法：

   ```python
   class MyClass:
       def __setattr__(self, name, value):
           if name == 'my_var':
               print('Setting my_var to %s' % value)
               self._my_var = value
           else:
               print('Setting %s to %s' % (name, value))
               super(MyClass, self).__setattr__(name, value)
   
   a = MyClass()
   a.my_var = "hello"
   a.other_var = "world"
   ```

   在这个例子中，我们定义了一个名为`MyClass`的类，并重写了`__setattr__`方法。当代码执行到`a.my_var = "hello"`时，Python会调用`__setattr__`方法来设置`my_var`属性的值。在`__setattr__`方法中，我们打印了一个信息，然后将传递的值存储到变量`_my_var`中。当代码执行到`a.other_var = "world"`时，因为`MyClass`类没有定义`other_var`属性的设置逻辑，所以Python会使用默认的属性赋值逻辑，并将`"world"`赋值给`other_var`属性。

   需要注意，当我们在`__setattr__`方法中使用属性赋值的方式来代替直接为属性赋值时，需要使用super函数来调用父类的`__setattr__`方法，否则会陷入死循环。

5. 私有化方法

   私有化方法同样采用的是名字重整的机制, 命名和使用方式和私有化属性一致



###### 内置

**类内置属性**

- `__dict__` : 类的属性
- `__bases__` : 类的所有父类构成的元组
- `__doc__` : 类的文档字符串, 和 `help()` 相比, 它只能查看类的描述, 不会出现属性等信息
- `__name__` : 类名
- `__module__` : 类定义所在的模块

**实例内置属性**

- `__dict__` : 实例的属性
- `__class__` : 实例对应的类

**方法内置特殊方法**

- 生命周期方法

- 信息格式化操作

  - `_str_` 

    ` __str__` 是一个用于自定义类的字符串表示的特殊方法。它可以让我们在类的对象被打印（使用 `print` 函数）时，能够以我们期望的方式输出类的信息，而不是默认的 `<__main__.ClassName object at 0x7f1a1162f550>` 格式。该方法应该返回一个字符串，用于代表类的对象。

  - `__repr__` 

     `__repr__` 方法也是一个特殊的方法，它用于返回类的对象的“官方字符串表示”，它的使用场景与 `__str__` 基本相同, 但是主要用于调试和开发。也就是说，但开发者要查看该对象的属性时，可以使用此方法查看该对象属性的官方字符串表示，以便进行编程调试。

    例如，我们可以为一个时间类定义一个 `__str__` 方法和一个`__repr__`来实现自定义时间格式的输出: 

    ```python
    class Time:
        def __init__(self, hour, minute):
            self.hour = hour
            self.minute = minute
    
        def __str__(self):
            return "{}:{}".format(self.hour, self.minute)
    
        def __repr__(self):
            return "Time({}, {})".format(self.hour, self.minute)
    
    
    t = Time(12, 30)
    print(t, type(t))           #  __str__第一种使用方式
    s = str(t)                  #  __str__第二种使用方式
    print(s, type(s))
    print(repr(t))              # __repr__的使用方式
    print(eval(repr(t)), type(eval(repr(t))))  # 使用eval(), 能将其再次转化为对象
    
    # output
    12:30 <class '__main__.Time'>
    12:30 <class 'str'>
    Time(12, 30)
    12:30 <class '__main__.Time'>
    ```

    在这个例子中，我们定义了一个 `Time` 类来表示时间。在类的 `__str__` 方法中，我们使用了字符串格式化来输出时间的小时与分钟。当我们将 `Time` 类的实例对象 `t` 传递给 `print` 函数时，Python 自动会调用 `__str__` 方法，并输出时间对象的字符串表示。需要注意的是，`__str__` 方法的返回值应该是一个描述类对象的字符串，而不是编程调试信息，这个任务应该交给 `__repr__` 方法完成。

    除了上述使用方式外，两种方法也可以在交互模式下使用，使用方式有所不同，示例如下

    ```python
    class Time:
        def __init__(self, hour, minute):
            self.hour = hour
            self.minute = minute
    
        def __str__(self):
            return "{}:{}".format(self.hour, self.minute)
    
        def __repr__(self):
            return "Time({}, {})".format(self.hour, self.minute)
    
    t = Time(12, 30)
    print(t)      #输出：12:30
    r             #输出：Time(12, 30)
    ```

- 调用操作

  `__call__` 方法

  在Python中，对象有时需要像函数一样被调用。为了实现这个功能，可以在类中定义一个特殊方法`__call__`。

  当对象被调用时，会自动调用`__call__`方法，可以在这个方法中实现自定义的对象调用行为。

  一般直接定义为`__call__(self, *args: Any, **kwds: Any) -> Any:`

  以下是一个使用`__call__`方法的例子：

  ```python
  class CallableClass:
      def __init__(self, value):
          self.value = value
  
      def __call__(self, value_to_add):
          self.value += value_to_add
  
  c = CallableClass(10)
  print(c.value)  # 输出 10
  
  c(2)            # 等同于调用 c.__call__(2)
  print(c.value)  # 输出 12
  ```

  在这个例子中，定义了一个名为`CallableClass`的类，它有一个初始化方法`__init__`和一个`__call__`方法。在初始化方法中，对象被赋予初始值。在`__call__`方法中，对象的值被增加。在调用对象时，会自动调用`__call__`方法。

  需要注意的是，如果一个类实现了`__call__`方法，那么这个类的对象就可以像函数一样被调用，但是调用对象本身并不会变成一个函数对象。因此，对象保留了对象状态和类自己的名称空间等信息。同时，由于可以传递参数，这种方式比使用闭包更为灵活。

- 索引和切片操作

  在Python中，`__getitem__`，`__setitem__` 和 `__delitem__` 方法定义了对象的索引和切片行为。

  `__getitem__(self, idx)` 方法用于实现对象的索引和切片操作。当我们对一个对象进行索引或切片时，`__getitem__` 方法将被调用。它接受一个参数 `idx`，如果 `idx` 是整数，则为索引操作，如果 `idx` 是一个 `slice` 对象，则为切片操作。索引操作时，如果对象不支持索引操作，此方法应当抛出`TypeError`异常。

  `__setitem__(self, idx, value)` 方法用于设置对象的索引和切片值。当我们对一个对象进行设置索引或切片赋值时，`__setitem__` 方法将被调用。它接受两个参数：`idx` 和 `value`。如果 `idx` 是整数，则为索引操作，将相应位置设置为 `value`。如果 `idx` 是一个 `slice` 对象，则为切片操作，将相应切片位置设置为 `value`。索引时，如果对象不支持修改某个索引值，此方法应当抛出`TypeError`异常。

   `__delitem__(self, idx)` 方法用于删除对象的索引和切片值。当我们对一个对象进行删除索引或切片赋值时，`__delitem__` 方法将被调用。它接受一个参数 `idx`。如果 `idx` 是整数，则为删除索引操作。如果 `idx` 是一个 `slice` 对象，则为删除切片操作。索引操作时，如果对象不支持删除某个索引值，此方法应当抛出 `TypeError` 异常。

  示例如下

  ```python
  class MyList:
      def __init__(self, data):
          self.data = data
  
      def __getitem__(self, idx):
          if isinstance(idx, slice):
              return MyList(self.data[idx])
          else:
              return self.data[idx]
  
      def __setitem__(self, idx, value):
          if isinstance(idx, slice):
              self.data[idx] = value
          else:
              self.data[idx] = value
  
      def __delitem__(self, idx):
          if isinstance(idx, slice):
              self.data = self.data[:idx.start] + self.data[idx.stop:]
          else:
              del self.data[idx]
  
      def __repr__(self):
          return repr(self.data)
  ```

  在上面这个示例中，我们创建了一个 `MyList` 类，其内部包含一个列表。我们实现了 `__getitem__`、`__setitem__` 和 `__delitem__` 方法，允许我们对 `MyList` 对象进行索引、切片、赋值和删除操作。

  ```python
  >>> m = MyList([1, 2, 3, 4, 5])
  >>> print(m[1:4])
  [2, 3, 4]
  >>> m[1:4] = [10, 20, 30]
  >>> print(m)
  [1, 10, 20, 30, 5]
  >>> del m[2]
  >>> print(m)
  [1, 10, 30, 5]
  ```

  需要注意的是，Python内置类型如`list`、`tuple`、`dict`等也实现了这些方法，因此，它们也可以进行索引操作。但是，它们的索引操作有时候并不完全符合我们的需求，这时就可以自定义类来实现自己需要的索引行为。

- 比较操作

  在 Python 中，我们可以通过实现特殊方法（也称为魔术方法）来定义对象类型之间的比较操作。下面是一些常用的特殊方法：

  ```python
  __eq__(self, other)：定义 == 操作符的行为；
  __ne__(self, other)：定义 != 操作符的行为；
  __lt__(self, other)：定义 < 操作符的行为；
  __le__(self, other)：定义 <= 操作符的行为；
  __gt__(self, other)：定义 > 操作符的行为；
  __ge__(self, other)：定义 >= 操作符的行为；
  
  这些特殊方法都以双下划线 __ 开头和结尾，其中 self 表示当前实例对象，other 表示与之比较的另一个对象。在实现这些方法时，我们可以根据具体情况判断是否需要比较对象的值、引用（即身份是否相同）或其他属性，从而实现不同类型之间的比较行为。
  注意：如果对于反向操作的比较符，只定义了其中一个方法，但使用的是另外一种比较运算，那么解释器会采用调换参数的方式进行调用该方法，但是不支持叠加操作
  例如我们已经定义了__lt__，此时我们可以使用>比较符，因为系统会帮我们自动调换，但是如果我们已经定义了__eq__和__lt__，我们不能使用<=或者>=，因为无法叠加，除非使用装饰器
  
  # 装饰器实现操作符“反向”，“组合”的方法
  import functools
  @functools.total_ordering
  class Person:
      def __init__(self) -> None:
          pass
  
      def __eq__(self, other):
          pass
  
      def __lt__(self, other):
          pass
  
  p1 = Person()
  p2 = Person()
  print(p1 <= p2)
  ```

  例如，假设我们有一个自定义的类 `Person`，我们可以实现 `__eq__` 方法来判断两个 `Person` 对象是否相等，如下所示：

  ```python
  class Person:
      def __init__(self, name, age):
          self.name = name
          self.age = age
  
      def __eq__(self, other):
          if isinstance(other, Person):
              return self.name == other.name and self.age == other.age
          return False
  ```

  在上面的代码中，我们通过判断 `other` 是否为 `Person` 对象，再根据 `name` 和 `age` 属性的值进行比较，来实现两个 `Person` 对象的相等性定义。这样，我们就可以使用 `==` 操作符对两个 `Person` 对象进行比较了。

  ```python
  p1 = Person("Alice", 20)
  p2 = Person("Bob", 30)
  p3 = Person("Alice", 20)
  
  print(p1 == p2) # False
  print(p1 == p3) # True
  ```

- 对象布尔值

  Python 中的 `__bool__` 是一个特殊方法，用于定义一个对象的真假判断行为。该方法在 Python 3 中替代了 Python 2 中的 `__nonzero__` 方法。

  当我们在 Python 中对一个对象执行条件判断时，比如使用 `if` 语句，Python 会调用该对象的 `__bool__` 方法来确定其真假值。在 `__bool__` 方法中，我们需要返回一个布尔值 `True` 或 `False`，来表示对象的真假状态。

  下面是一个例子，展示如何实现 `__bool__` 方法来定义一个自定义对象的真假值判断行为：

  ```python
  class MyObject:
      def __init__(self, value):
          self.value = value
  
      def __bool__(self):
          return self.value != 0
  ```

  在上面的例子中，我们定义了一个 `MyObject` 类，其中包含一个值属性 `value`。我们通过实现 `__bool__` 方法来定义当该对象被作为条件判断时，如果 `value` 不等于 0，则返回 `True`，否则返回 `False`。

  ```python
  obj1 = MyObject(10)
  obj2 = MyObject(0)
  
  if obj1:
      print("obj1 is true")
  else:
      print("obj1 is false")
  
  if obj2:
      print("obj2 is true")
  else:
      print("obj2 is false")
  ```

  在上面的代码中，我们分别创建了两个 `MyObject` 对象 `obj1` 和 `obj2`，分别初始化为 10 和 0。然后我们对它们进行了条件判断，输出了它们的真假状态。

  由于 `obj1` 的 `value` 属性为 10，不为 0，因此在条件判断时返回的是 `True`，输出了 "obj1 is true"。而 `obj2` 的 `value` 属性为 0，因此在条件判断时返回的是 `False`，输出了 "obj2 is false"。

  当我们需要自定义一个对象的真假判断行为时，我们可以实现 `__bool__` 方法来满足自己的需求。

- 遍历操作

  在 Python 中，实现一个迭代器的最基本方法是为所需类定义`__iter__()`和`__next__()`方法，且缺一不可。其中`__iter__()`方法返回一个自身的迭代器对象，而`__next__()`方法返回当前迭代位置的数据，并将位置移动到下一个数据。

  示例

  ```python
  class MyIterator:
      def __init__(self, n):
          self.num = n
          self.count = 0
  
      def __iter__(self):
          return self
  
      def __next__(self):
          if self.count < self.num:
              self.count += 1
              return self.count
          else:
              raise StopIteration
  ```

  在上面的例子中，我们定义了 `MyIterator` 类来表示一个迭代器。类的构造方法中，我们接收一个整数作为参数，作为迭代器的长度。在 `__iter__()` 方法中，我们返回自身作为迭代器对象。实际上，这个方法是必须实现的，因为迭代器对象必须是一个迭代器。最后，在`__next__()` 方法中，我们实现了迭代器的主要逻辑，即每次返回下一个数据，直到迭代完毕抛出 StopIteration 异常。

  我们现在可以使用 `for` 循环来迭代该迭代器，像这样：

  ```python
  my_iterator = MyIterator(5)          # 此时my_iterator是一个迭代器
  for i in my_iterator:
      print(i)
  ```

  在上面的代码中，我们创建了一个名为 `my_iterator` 的 `MyIterator` 实例，并使用 `for` 循环来遍历它。在循环中，`i` 将依次被赋值为迭代器的下一个元素，并被打印出来。

  要注意的是，上面的`my_iterator`同样遵循迭代器的特性，例如，再对其进行`for in`循环时，会从上一次的位置继续走。若要实现每次`for in`都能重新开始，则需要在`__iter__`中添加初始化语句

  ```python
  delf __iter__(self):
  	self.count = 0
  	return self
  ```

  还有一种更简洁的定义迭代器的方法是使用生成器函数。我们可以使用 yield 语句来简化上面的 `MyIterator` 迭代器实现：

  ```python
  def my_generator(n):
      count = 0
      while count < n:
          yield count
          count += 1
  ```

  在上面的代码中，我们使用了一个名为 `my_generator` 的生成器函数来创建一个迭代器。生成器函数包含一个 while 循环，用于不断产生下一个元素，直到达到指定的数量。在每次迭代时，我们使用`yield`语句来返回当前元素，并让生成器函数暂停，等待下一次迭代。

  我们可以像这样使用生成器函数来迭代：

  ```python
  for i in my_generator(5):
      print(i)
  ```

  在上面的代码中，生成器函数 `my_generator(5)` 将产生 0 到 4 的 5 个数字，这些数字将分别被赋值给变量' i '然后打印出来。

  **Tips**：

  1. 迭代器一定是一个可迭代对象，一个可迭代对象却不一定是一个迭代器

  ```python
  from collections.abc import Iterable
  from collections.abc import Iterator
  
  p = MyIterator(5)
  print(type(p))
  print(isinstance(p, Iterator))     # 判断是否是迭代器 
  print(isinstance(p, Iterable))     # 判断是否是可迭代对象
  # output
  True
  True
  ```

  查看`_collections_abc.py`可以看到, `class Iterable` 中只包含了`__iter__`函数, 而没有`__next__` 函数, 说明, 只要有`__iter__`, 就是一个可迭代对象, 而`class Iterator`中有`__iter__` 函数和`__next__` 函数, 说明作为一个迭代器必须同时要有`__iter__`和`__next__`函数

  2. 一个可迭代对象必定可以通过`for in`进行访问, 但是能通过`for in`进行访问, 不一定就是一个可迭代对象

     例如我们修改类的定义: 

  ```python
  class MyIterator:
      def __init__(self, n):
          self.num = n
          self.count = 0
  
      def __getitem__(self, item):
      	return 1
      
  p = MyIterator(5)
  print(isinstance(p, Iterator))     # False
  print(isinstance(p, Iterable))     # False
  for i in p:                        # 可以执行
      print(p)
  ```

  上面的类实例出的对象可以用于`for in`遍历, 但却不是可迭代对象, 因为不存在`__item__`函数

  3. `iter()`函数

  `iter()` 函数的作用是将一个可迭代的对象转化为一个迭代器。

  它在此处有两种使用方式, 第一种是直接传入一个实例. 如果一个对象实例实现了 `__iter__()` 方法并返回一个迭代器对象，那么该对象实例就可以使用内置函数 `iter()` 来返回一个迭代器。

  ```python
  class MyIterator:
      def __init__(self, n):
          self.num = n
          self.count = 0
  
      # def __getitem__(self, item):
      # 	return 1
  
      def __iter__(self):
          return self
  
      def __next__(self):
          if self.count < self.num:
              self.count += 1
              return self.count
          else:
              raise StopIteration
          
  
  p = MyIterator(5)
  pt = iter(p)
  print(p is pt)          # p是迭代器,pt也是迭代器,两者都是迭代器,且内存地址都是一致的
  for i in pt:
      print(i, end=' ')
  
  # output
  True
  1 2 3 4 5
  ```

  第二种方式是前面写一个可调用对象, 后面写一个终止值. 例如, 可以定义`__call__` 函数, 使其能够接收多个参数, 在下面的例子中, `item(p, 3)` 代表迭代器迭代到`3`会停止, 且不会执行`3`的内容. 其中的原理,  `item()` 执行的是前面传进去的可调用对象, 也就说此时是直接调用 `p` 来获取下一个数据, 再将数据和后面的`3`进行比较, 如果是`3`就立即终止

  ```python
  class MyIterator:
      def __init__(self, n):
          self.num = n
          self.count = 0
  
      def __iter__(self):
          return self
          
      def __call__(self, *args: Any, **kwds: Any) -> Any:
          if self.count < self.num:
              self.count += 1
              return self.count
          else:
              raise StopIteration
  
  p = MyIterator(5)
  pt = iter(p, 3)
  for i in pt:
      print(i, end=' ')
      
  # output
  1 2 
  
  
  # 也可以使用iter(p.__next__, 3), 但是此时pt却不是同一个迭代器,内存地址不一致
  class MyIterator:
      def __init__(self, n):
          self.num = n
          self.count = 0
  
      # def __getitem__(self, item):
      # 	return 1
  
      def __iter__(self):
          return self
  
      def __next__(self):
          if self.count < self.num:
              self.count += 1
              return self.count
          else:
              raise StopIteration
          
  
  p = MyIterator(5)
  pt = iter(p.__next__, 3)
  print(p is pt)                        # False 两者内存地址不同
  for i in pt:
      print(i, end=' ')                 # 1 2
  print('')
  print(isinstance(pt, Iterator))       # True 说明pt是迭代器
  print(isinstance(p, Iterator))        # True 说明p是迭代器
  ```

- **描述器**

  - 方式一: 使用`property` 

  - 方式二: 定义一个描述器的类, 并用包含该描述器的类的实例进行操作, 注意不能直接在类操作, 需要先创建实例对象, 才能将属性的增删查改操作转化到描述器的实例方法中. 还要注意的是, 此种装饰器方式只适用于新式类, 在经典类不适用

    ```c++
    class Age:
        def __get__(sefl, instance, owner):
            print("get")
    
        def __set__(self, instance, value):
            print("set")
    
        def __delete__(self, instance):
            print("delete")
    
    
    class Person:
        age = Age()
    
    
    p = Person()
    p.age = 10
    p.age
    del p.age
    
    #output
    set
    get
    delete
    ```

  注意: 

  - `__getattrubution__` 注意使用装饰器时, 不要使用该名称再次命名某种方法, 因为这是系统内置的函数, 再次实现会导致原来的方法被覆盖而导致失去对应的功能, 在这里会导致装饰器失效, 所以我们在命名方法的时候, 一定要小心, 不要覆盖系统内置的函数

  - 描述器和实例属性同名时, 操作优先级

    概念补充:

    - 资料描述器: 存在`get` 和`set` 方法

    - 非资料描述器: 仅仅实现了`get`方法,  

    如果是资料描述器, 则该描述器的优先级高于实例属性, 会优先操作资料描述器, 例如下面的代码, 创建实例对象`p`时, `__init__` 初始化方法中, 调用的是装饰器的`__set__`进行设置

    ```python
    class Age:
        def __get__(sefl, instance, owner):
            print("get")
    
        def __set__(self, instance, value):
            print("set")
    
        def __delete__(self, instance):
            print("delete")
    
    
    class Person:
        age = Age()
    
        def __init__(self) -> None:
            self.age = 10
    
    
    p = Person()
    p.age = 10
    p.age
    print(p.__dict__)
    del p.age
    ```

    如果是非资料描述器, 实例属性的优先级大于资料描述器, 例如下面的代码, 从输出中, 可以看出并没有调用`__get__` 函数

    ```c++
    class Age:
        def __get__(sefl, instance, owner):
            print("get")
    
    
    class Person:
        age = Age()
    
        def __init__(self) -> None:
            self.age = 10
    
    
    p = Person()
    p.age = 10
    print(p.age)
    print(p.__dict__)
                
    # output
    10
    {'age': 10}
    ```

  - 数据存储问题

    类创建的不同实例, 实际上是公用同一个`age` 对象, 因为创建的都是`Person`的实例, 它们自然是共用父类的`age`属性, 从下面代码运行得到的内存地址也可以看出, 它们的`age`属性的内存地址都是一致的, 只有不同的实例的内存地址不同, 所以, 如果我们将存储的数据保存到`self`中, 也就是存在`age`中, 那每次实例的创建和修改, 都会导致该属性改变, 即该属性是共享的

    ```c++
    class Age:
        def __get__(self, instance, owner):
            print("get", end=' ')
            return self.v
    
        def __set__(self, instance, value):
            print("set", self, instance, value)
            self.v = value
    
        def __delete__(self, instance):
            print("delete")
    
    
    class Person:
        age = Age()
    
        def __init__(self) -> None:
            self.age = 10
    
    
    p1 = Person()
    p1.age = 12
    p2 = Person()
    p2.age = 13
    print(p1.age)
    print(p2.age)
                
    # output
    set <__main__.Age object at 0x000002B1A8068670> <__main__.Person object at 0x000002B1A80686A0> 10
    set <__main__.Age object at 0x000002B1A8068670> <__main__.Person object at 0x000002B1A80686A0> 12
    set <__main__.Age object at 0x000002B1A8068670> <__main__.Person object at 0x000002B1A8068A30> 10
    set <__main__.Age object at 0x000002B1A8068670> <__main__.Person object at 0x000002B1A8068A30> 13
    get 13
    get 13
    ```

    我们可以将数据存储到`instance`中, 也就是对应的实例的内存地址, 所以能够存储实例各自不同的数据

    ```C++
    class Age:
        def __get__(self, instance, owner):
            print("get", end=' ')
            return instance.v
    
        def __set__(self, instance, value):
            print("set", self, instance, value)
            instance.v = value
    
        def __delete__(self, instance):
            print("delete")
    
    
    class Person:
        age = Age()
    
        def __init__(self) -> None:
            self.age = 10
    
    
    p1 = Person()
    p1.age = 12
    p2 = Person()
    p2.age = 13
    print(p1.age)
    print(p2.age)
    
    # output
    set <__main__.Age object at 0x00000258C20A8640> <__main__.Person object at 0x00000258C20A8670> 10
    set <__main__.Age object at 0x00000258C20A8640> <__main__.Person object at 0x00000258C20A8670> 12
    set <__main__.Age object at 0x00000258C20A8640> <__main__.Person object at 0x00000258C20A8A00> 10
    set <__main__.Age object at 0x00000258C20A8640> <__main__.Person object at 0x00000258C20A8A00> 13
    get 12
    get 13
    ```

- 类实现装饰器

  借助语法糖, 实现实例的创建, 之前提及的装饰器的作用是重新实现函数, 现在是利用语法糖创建一个类对象, 然后使用`__call__`直接调用类对象, 同样实现了装饰器的效果

  ```python
  from typing import Any
  
  class check:
      def __init__(self, func) -> None:
          self.f = func
  
      def __call__(self, *args: Any, **kwds: Any) -> Any:
          print("Today is 520")
          self.f()
  
  @check
  def work():
      print("I am working")
  
  # work = check(work)      @check 等价于此行代码, 作用是创建一个check类的对象
  work()
  
  # output
  Today is 520
  I am working
  ```




#### 生命周期

###### 概念

Python生命周期是指Python程序运行过程中，各个对象的创建、使用和销毁等状态变化的整个过程。在Python生命周期中，解释器会负责管理和维护对象的内存分配、使用和释放，以保证程序的正常运行

###### 监听对象生命周期

`__new__` 方法:

在Python中，每个对象都是某个类的实例，而类则是对象的抽象。当我们创建一个对象时，Python会自动调用类的构造方法__init__()来初始化对象的属性。但在__init__()之前，Python还会调用另一个特殊方法__new__()来创建对象并分配内存空间。

**new**()方法是一个类方法，用于创建类的新实例。它的主要作用是分配内存空间，并返回一个新的对象实例。**new**()方法接收的第一个参数是类本身，其余参数则是用于初始化对象的参数。**new**()方法的返回值通常是一个新的对象实例，这个实例将被传递给__init__()方法，并用于初始化对象的属性。

**new**()方法通常被用于自定义对象的创建过程，例如单例模式、工厂模式等。在这些模式中，我们需要控制对象的创建过程，并确保每次创建的对象都是唯一的或符合特定的要求。通过自定义__new__()方法，我们可以在对象创建之前进行一些额外的操作，并对对象的创建过程进行精细的控制。

需要注意的是，**new**()方法是一个静态方法，它不会被继承。因此，如果我们要自定义__new__()方法，需要在子类中重新定义该方法，而不是在父类中定义。另外，**new**()方法的返回值必须是一个实例对象，否则将会引发TypeError异常。

```python
class Person:
    def __new__(cls):
        print("creat a new object, but be held up")  # 自己重新定义__new__, 却没有为对象分配内存, 所以并没有创建
        pass


p = Person()
print(p)

# output
creat a new object, but be held up
None
```

`__init__` and `__del__` 方法:

```python
class Person:
    __count = 0
    def __init__(self) -> None:
        print("add object")
        Person.__count += 1

    def __del__(self) -> None:
        print("sub object")
        self.__class__.__count -= 1
    
    @staticmethod
    def log():
        print("there are %d objects"%Person.__count)

	# 下面也能实现上一个函数功能
    # @classmethod
    # def log(cls):
    #     print("there are %d objects"%cls.__count)

p = Person()
Person.log()
del p
Person.log()

# output
add object
there are 1 objects
sub object
there are 0 objects
```

###### 内存管理机制

**存储方面**

1. 在python中万物皆对象, 不存在基本数据类型
2. 所有对象都会在内容中开辟一块空间进行存储, 会根据不同的类型以及内容, 开辟不同的空间大小进行存储, 返回该空间的地址给外界接收(称为"引用"), 用于对于后续这个对象的操作, 可以通过`id()`函数获取内存地址(十进制), 也可以通过`hex(id())`函数查看对应的十六进制地址
3. 对于整数和短小的字符, python会进行缓存, 不会创建多个相同对象
4. 容器对象, 存储的其它对象, 仅仅是其他对象的引用, 并不是其他对象本身

**垃圾回收方面**

Python中的内存管理机制主要是由垃圾回收器（Garbage Collector）实现的。垃圾回收器是Python解释器的一部分，它会自动管理和回收不再使用的内存对象，以避免内存泄漏和内存溢出等问题。

Python中的垃圾回收器采用了引用计数（Reference Counting）和标记清除（Mark and Sweep）两种算法相结合的方式来回收内存对象。具体来说，引用计数算法会记录每个对象的引用计数器，当引用计数器为0时，垃圾回收器会立即回收该对象所占用的内存。而标记清除算法则会从根节点开始遍历程序中的所有对象，并标记所有可达对象，最后将未标记的对象回收。

1. 引用计数器

   查看引用计数

   ```python
   import sys
   sys.getrefcount()   # 注意值会大1
   ```

   引用计数+1情景 对象被创建 `p1 = Person()`

   1. 对象被引用 `p1 = p2` 
   2. 对象被作为参数，传入到一个函数中
   3. 对象作为一个元素，存储在容器中 `l = [p1]` 

   引用计数-1情景

   1. 对象别名被显式销毁 `del p1` 
   2. 对象的别名被赋予新的对象 `p1 = 123` 
   3. 一个对象离开它的作用域
   4. 对象所在的容器被销毁，或从容器中删除对象

2. 垃圾回收

   Python中的垃圾回收机制基于引用计数和循环垃圾收集两种方法。
   
   引用计数是Python中最基本的垃圾回收机制，它跟踪每个对象的引用计数器，当引用计数器为0时，对象就被认为是垃圾。Python会自动释放这些垃圾对象的内存空间。
   
   循环垃圾收集是一种更高级的垃圾回收机制，用于处理引用计数无法处理的循环引用。循环引用是指两个或多个对象相互引用，形成一个环形结构，导致无法判断对象是否还在被使用。Python的循环垃圾收集器会定期扫描内存中的所有对象，找出循环引用的对象，并将其标记为垃圾。然后，Python会将这些垃圾对象从内存中删除。
   
   Python的垃圾回收机制是自动的，程序员不需要手动释放内存。同时，Python还提供了一些工具，如gc模块和sys模块，用于控制和调试垃圾回收机制的行为。例如，可以使用gc模块中的方法手动触发垃圾回收，或者使用sys模块中的方法查看内存使用情况和垃圾回收统计信息。



#### 三大特性

###### 封装

1. 概念

   在Python中，封装是一种面向对象编程的概念，指的是将数据和方法包装在一个类中，以实现数据的保护和隐藏。封装可以通过两种方式来实现：访问控制和属性。

2. 优点

   1. 数据隐藏和保护：封装可以将类的实现细节隐藏起来，只暴露出必要的接口，从而保护数据的安全性和完整性。即使外部代码能够访问类的数据，也只能通过类中定义的方法来访问和修改数据，从而减少了数据被误操作的可能性。
   2. 简化代码：封装可以将类的实现细节隐藏起来，使外部代码只需要关注类的接口，而不需要了解类的内部实现。这样可以简化代码，提高代码的可读性和可维护性。
   3. 降低耦合度：封装可以将类的实现细节隐藏起来，使类与其他类之间的依赖关系变得更加松散，从而降低了类之间的耦合度。这样可以使代码更加灵活和可扩展，便于维护和修改。
   4. 提高安全性：封装可以将类的实现细节隐藏起来，使外部代码无法直接访问类的数据和方法，从而提高了程序的安全性。这可以防止不合法的访问和修改，减少了程序的漏洞和错误。

###### 继承

1. 概念

   继承是面向对象编程中的一种机制，它允许一个类从另一个类中继承属性和方法。被继承的类称为父类或基类，继承的类称为子类或派生类。

   继承的核心思想是：子类可以重用父类的代码，从而避免代码重复和冗余。在继承关系中，子类会继承父类的所有公共属性和方法，并且可以添加自己的属性和方法。这样，子类就可以在父类的基础上进行扩展和修改，从而实现更加复杂的功能。

   继承可以分为单一继承和多重继承两种形式。单一继承是指一个子类只能继承一个父类的属性和方法，而多重继承是指一个子类可以同时继承多个父类的属性和方法。Python是一种支持多重继承的编程语言，这使得Python的继承机制更加灵活和强大。

2. 优点

   1. 代码重用：子类可以重用父类的代码，从而避免代码重复和冗余
   2. 扩展和修改：子类可以在父类的基础上进行扩展和修改，从而实现更加复杂的功能
   3. 统一接口：父类定义了一组公共接口，子类继承了这些接口，从而实现了统一的接口，便于代码的维护和扩展
   4. 继承层次结构：继承可以形成一个层次结构，便于组织和管理代码

3. 分类

   在Python中，继承可以分为单继承和多继承两种形式。

   1. 单继承

   单继承是指一个子类只能继承一个父类的属性和方法。在Python中，可以通过在类定义中指定一个父类来实现单继承。例如：

   ```python
   class Parent:
       def method(self):
           print("Parent.method")
   
   class Child(Parent):
       pass
   
   c = Child()
   c.method()  # 输出 "Parent.method"
   ```

   2. 多重继承

   多重继承是指一个子类可以同时继承多个父类的属性和方法。在Python中，可以通过在类定义中指定多个父类来实现多重继承。例如：

   ```python
   class A:
       def method(self):
           print("A.method")
   
   class B:
       def method(self):
           print("B.method")
   
   class C(A, B):
       pass
   
   c = C()
   c.method()  # 输出 "A.method"
   ```

   在多重继承中，如果多个父类中存在同名的方法或属性，Python会按照从左到右的顺序搜索父类，并调用第一个找到的方法或属性。如果多个父类中都没有找到相应的方法或属性，Python会抛出AttributeError异常。

   总之，单继承和多重继承是Python中继承的两种形式。通过继承，子类可以继承父类的属性和方法，并且可以在父类的基础上进行扩展和修改。在多重继承中，如果多个父类中存在同名的方法或属性，Python会按照从左到右的顺序搜索父类，并调用第一个找到的方法或属性。

4. `type` 和 `object` 的区分

   在Python中，`type`和`object`是两个重要的内置类，它们有一些区别和不同的作用。

   1. `type`

   `type`是Python中所有类型的元类。元类是用于创建类的类，它定义了类的行为和属性，并控制类的实例化过程。在Python中，我们可以使用`type`来创建新的类。

   例如，下面的代码使用`type`来创建一个新的类`Person`：

   ```python
   Person = type('Person', (object,), {'name': 'John', 'age': 30})
   ```

   在上面的代码中，我们使用`type`创建了一个名为`Person`的类，它继承自`object`类，有两个属性`name`和`age`。这相当于下面的类定义：

   ```python
   class Person:
       name = 'John'
       age = 30
   ```

   2. `object`

   `object`是Python中所有类的基类，即所有类都直接或间接地继承自`object`类。`object`类提供了一些基本的方法和属性，如`__str__`、`__repr__`、`__eq__`、`__hash__`等。

   例如，下面的代码定义了一个类`MyClass`，它继承自`object`类：

   ```python
   class MyClass(object):
       pass
   ```

   在上面的代码中，我们通过在类定义中指定`object`类来继承`object`类的所有方法和属性。如果我们不指定父类，Python会默认将`object`类作为父类。

   并且, 我们可以通过`__bases__`来得到类的所有父类所构成的元组, 通过`__class__`来查询实例所对应的类. 

   总之，`type`和`object`是Python中两个重要的内置类，它们有不同的作用和用途。`type`是所有类型的元类，用于创建新的类；`object`是所有类的基类，提供了一些基本的方法和属性。

   <img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20230701155407102.png" alt="image-20230701155407102" style="zoom: 50%;" />

5. 资源的继承

   在python中继承是指资源的使用权, 所以测试某个资源能否被继承, 其实就是在测试在子类当中, 能不能访问到父类中的这个资源; 而除了私有的属性和私有的方法, 其他的基本都能被继承, 包括共有属性和方法, 受保护属性和方法, 内置方法. 

6. 资源的使用

   Python中的继承有多种形态，包括单继承、多继承、抽象基类和Mixin类等 

   <img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20230701162147429.png" alt="image-20230701162147429" style="zoom: 50%;" />

   几种形态遵循的标准原则

   1. 单继承: 从下往上查找
   2. 无重叠的多继承链: 单调原则, 按照从左到右的链条顺序, 对链条从下到上查找
   3. 有重叠的多继承链: 同样是从左到右, 从下到上原则

   <img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20230701171903949.png" alt="image-20230701171903949" style="zoom: 50%;" />

7. 针对于几种标准原则的方案演化

   Python2.2之前, 仅仅存在经典类, MRO原则, 深度优先(从左往右) , 问题: 有"重叠的多继承"中, 违背"重写可用原则"; 

   Python2.2, 产生了新式类, MRO原则中经典类深度优先(从左到右), 新式类则是在深度优先的算法基础上, 优化了一部分, 注意不是"广度优先算法", 问题是无法检测出有问题的继承, 有可能还会违背"局部优先"的原则;

   Python2.3-2.7, 新式类经典类并存, MRO原则, 经典类深度优先(从左到右), 新式类C3算法; 

   Python3.x之后,  MRO原则, 新式类, C3算法; 

   ```python
   class D:
       pass
   
   class B(D):
       pass
   
   class C(D):
       def test(self):
           print(self)
       
       @classmethod
       def test2(cls):
           print(cls)
   
   
   class A(B, C):
       pass
   
   print(A.mro())
   
   # output
   [<class '__main__.A'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.D'>, <class 'object'>]
   ```

8. 资源的覆盖

   1. 包括: 属性的覆盖, 方法的重写

   2. 原理: 在MRO的资源检索链当中, 优先级比较高的类写了一个和优先级比较低的类一样的一个资源(属性或方法), 当我们查找或者获取资源的时候, 就会优先选择优先级比较高的, 而摒弃优先级较低的, 造成"覆盖"现象

   3. 注意: 当调用优先级比较高的资源时, 注意`self`的变化

      ```python
      class D:
          pass
      
      class B(D):
          pass
      
      class C(D):
          def test(self):
              print(self)
          
          @classmethod
          def test2(cls):
              print(cls)
      
      class A(B, C):
          pass
      
      A.test2()
      a = A()
      a.test()
      
      # output
      <class '__main__.A'>
      <__main__.A object at 0x0000019B7DB68A00>
      ```

9. 资源的累加

   1. 概念: 在一个类的基础上, 增加一些额外的资源
   
   2. 子类相比于父类, 多一些自己特有的资源
   
   3. 在被覆盖的方法基础之上, 新增内容
   
      1. 方案一
   
      2. 方案二: 在低优先级类的方法中, 通过`super`来调用高优先级类的方法
   
         `super` 
   
         **概念**
   
         Python中的`super()`函数是一个特殊的函数，它用于调用父类的方法。它的作用是在子类中调用父类的方法，从而实现代码复用和继承。`super()`函数主要用于多重继承的情况下，以便在父类之间进行正确的调用。它起着代理的作用, 沿着 `MRO`链条, 找到下一级节点, 去调用对应的方法
   
         **语法原理**
   
         `super([type[, object-or-type]])`
   
         `super()`函数接受两个可选参数：`type`和`object-or-type`。`type`通常是当前类的类型，而`object-or-type`则是当前类的实例或者是该类。如果省略这两个参数，则默认使用当前方法所在的类和实例。
   
         当调用`super()`函数时，它会返回一个代理对象（proxy object），该对象用于调用父类的方法。这个代理对象的工作原理是基于方法解析顺序（MRO，Method Resolution Order）的算法，MRO算法决定了在多继承情况下，Python解释器查找方法的顺序。MRO算法基于C3算法，它利用拓扑排序的方法来解决方法调用的冲突问题，确保每个类的方法都能被正确地调用，而且每个方法只会被调用一次。
   
         当使用`super()`函数调用父类的方法时，Python解释器会自动根据MRO算法确定应该调用哪个父类的方法，然后将方法的参数传递给它。这样，就可以实现代码复用和继承。另外需要注意的是，`super()`函数只能用于新式类（即继承了`object`的类），对于旧式类则不支持。
   
         总之，`super()`函数的语法原理是基于MRO算法的多重继承调用机制，它可以帮助我们在多重继承的情况下，正确地调用父类的方法。
   
         其中`super`是沿着参数2的`MRO`链条, 找参数1的下一个节点, 并且使用参数2进行调用来应对类方法, 静态方法, 以及实例方法的传参问题. 
   
         **常用语法格式**
   
         在Python中，`super()`函数的常用语法格式有两种：
   
         1. 无参数形式：
   
         ```python
         class ChildClass(ParentClass):
             def some_method(self, arg1, arg2, ...):
                 super().some_method(arg1, arg2, ...)
         ```
   
         在这种形式下，`super()`函数会自动推断出当前类和实例，并调用当前类的父类中名为`some_method()`的方法。这种形式在Python 3及以上版本中是常用的形式。
   
         2. 带参数形式：
   
         ```python
         class ChildClass(ParentClass):
             def some_method(self, arg1, arg2, ...):
                 super(ChildClass, self).some_method(arg1, arg2, ...)
         ```
   
         在这种形式下，`super()`函数需要传入当前类和实例作为参数。这种形式在Python 2及以下版本中比较常用。
   
         在使用`super()`函数时，需要注意以下几点：
   
         1. `super()`函数只能用于新式类（即继承了`object`的类），对于旧式类则不支持。
   
         2. `super()`函数只能用于调用父类的方法，不能用于调用父类的属性。
   
         3. `super()`函数只能用于单继承和多重继承的情况下，不能用于多继承的情况下。
   
         总之，`super()`函数的常用语法格式是无参数形式和带参数形式，可以根据具体的情况选择适合的形式来使用。
   
         **注意**
   
         带参数时可以将`super()`参数中的类名直接写为`self.__calss__`, 这样可以更加灵活, 但是会出现死循环问题, 所以不要这么写	

###### 多态

在Python中，多态是一种面向对象编程的特性，它允许不同的对象对同一个方法做出不同的响应。在Python中，多态可以通过方法重写和方法重载来实现。

方法重写是指在子类中重新定义父类中已存在的方法。当子类对象调用这个方法时，它将调用子类中的方法而不是父类中的方法。这样就可以根据不同的子类对象实现不同的方法响应。

例如，假设我们有一个动物类和一个狗类，狗类继承自动物类，并且重写了动物类中的`make_sound`方法：

```python
class Animal:
    def make_sound(self):
        pass

class Dog(Animal):
    def make_sound(self):
        print("汪汪汪！")
```

在这里，`Dog`类重写了`Animal`类中的`make_sound`方法，并实现了狗叫的功能。当我们创建一个`Dog`对象并调用`make_sound`方法时，它将输出“汪汪汪！”：

```python
dog = Dog()
dog.make_sound()  # 输出：汪汪汪！
```

方法重载是指在同一个类中定义多个方法，它们具有相同的名称但不同的参数类型和/或数量。在调用这个方法时，会根据传入的参数类型和/或数量来决定具体调用哪个方法。方法重载在Python中并不是一个必需的特性，因为Python是一种动态类型语言，它不需要在编译时确定变量的数据类型。

举个例子，我们可以在一个类中定义多个add方法，每个方法都有不同的参数类型和数量：

```python
class Math:
    def add(self, x, y):
        return x + y
    
    def add(self, x, y, z):
        return x + y + z
```

当我们创建一个Math对象并调用add方法时，Python会根据传入的参数类型和数量来决定具体调用哪个add方法：

```python
math = Math()
print(math.add(1, 2))  # 输出：3
print(math.add(1, 2, 3))  # 输出：6
```

需要注意的是，在Python中，方法重载并不是一个严格的规则，因为Python是一种动态类型语言，它不需要在编译时确定变量的数据类型。因此，我们可以使用`*args`和`**kwargs`参数来实现灵活的方法定义，例如：

```python
class Math:
    def add(self, *args):
        return sum(args)
```

在这里，我们使用了*args参数来接收任意数量的参数，并使用内置函数sum来计算它们的和。这样，我们就可以在调用add方法时传入任意数量的参数，而不需要在类中定义多个方法。

###### 补充

在Python中，抽象类和抽象方法是一种用于面向对象编程的概念，它们可以用来描述一种通用的行为或结构，并且要求子类实现这些行为或结构。抽象类和抽象方法通常用于设计和实现框架或API，以便其他人可以在其基础上构建自己的应用程序。

抽象类是不能被实例化的类，它只能被用作其他类的基类。抽象类通常包含一些抽象方法，这些方法只有方法声明，没有具体实现。抽象方法必须在子类中实现，否则子类也必须被声明为抽象类。

在Python中，我们可以使用abc模块来创建抽象类和抽象方法。下面是一个简单的例子：

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def make_sound(self):
        pass

class Dog(Animal):
    def make_sound(self):
        print("汪汪汪！")

class Cat(Animal):
    def make_sound(self):
        print("喵喵喵！")
```

在这里，`Animal`类是一个抽象类，它包含一个名为`make_sound`的抽象方法。因为`make_sound`是一个抽象方法，所以它没有具体实现。`Dog`和`Cat`类是`Animal`类的子类，并且都实现了`make_sound`方法。因此，它们都可以被实例化并使用。

**要特别注意的是, 如果定义了抽象方法, 在抽象类的子类中一定要对抽象方法进行具体实现, 否则会报错. **

如果我们尝试实例化`Animal`类，Python将抛出`TypeError`异常，因为抽象类不能被实例化：

```python
animal = Animal()  # 抛出TypeError异常
```

需要注意的是，在Python中，我们也可以定义一个没有任何抽象方法的抽象类，例如：

```python
class Shape(ABC):
    pass
```

在这里，`Shape`类是一个抽象类，它没有任何抽象方法。这种情况下，我们通常使用抽象类来表示一个通用的概念，例如形状，而不需要实现任何具体的行为。

总之，抽象类和抽象方法是一种用于面向对象编程的概念，它们可以用来描述一种通用的行为或结构，并且要求子类实现这些行为或结构。在Python中，我们可以使用abc模块来创建抽象类和抽象方法，并且抽象类不能被实例化，而抽象方法必须在子类中实现。



#### 设计原则

在Python中，面向对象编程是一种重要的编程范式，它可以帮助我们更好地组织和管理代码。为了编写高质量的面向对象代码，我们需要遵循一些面向对象的设计原则。下面是一些常见的面向对象设计原则：

1. 单一职责原则（SRP）：一个类应该只有一个单一的功能，即只有一个职责。这样可以使类的设计更加简单、清晰，并且易于维护。

2. 开放-封闭原则（OCP）：一个类应该对扩展开放，对修改封闭。这意味着添加新功能应该通过添加新的代码来实现，而不是修改原有代码。

3. 里氏替换原则（LSP）：子类应该能够替换掉父类并且不会产生任何错误或异常。这意味着子类应该与其父类遵循相同的接口和行为。

4. 接口隔离原则（ISP）：一个类不应该强迫其客户端依赖于不需要使用的接口。这意味着我们应该将接口拆分成更小的、更具体的接口，以便客户端只需要依赖于它们所需要的接口。

5. 依赖倒置原则（DIP）：高层模块不应该依赖于低层模块，它们应该依赖于抽象。这意味着我们应该将高层模块和低层模块都依赖于抽象接口，而不是直接依赖于具体的实现。

6. 迪米特法则（LoD）：一个模块不应该了解它所不需要知道的信息。这意味着我们应该尽可能地减少模块之间的耦合度，以便更容易地进行维护和修改。

遵循这些面向对象设计原则可以帮助我们设计出更加灵活、可扩展、易于维护的面向对象程序。它们可以使我们的代码更加清晰，易于理解，并且更容易满足需求变更。







## 异常处理

#### 错误和异常的概念

在Python中，异常和错误是指在程序运行时遇到的问题，这些问题可能会导致程序无法正常执行或产生不正确的结果。异常和错误是Python中的两个不同的概念，它们的含义如下：

1. 异常（Exception）：指程序在运行时遇到的非致命问题，例如输入错误的数据、文件不存在等。当程序遇到异常时，可以捕获和处理异常，以便程序能够继续执行。出现此类错误时，语法和逻辑通常是正确的。Python中的异常通常是由raise语句抛出的，可以使用try...except语句来捕获和处理异常。

2. 错误（Error）：指程序在运行时遇到的致命问题，例如内存不足、语法错误等。当程序遇到错误时，通常无法继续执行，需要修复程序代码或者更换计算机硬件等。Python中的错误通常是由Python解释器抛出的，例如SyntaxError、NameError等。但是如果是出现逻辑错误，解释器则无法帮我们检测出来。

#### 常见的系统异常

在Python中，有许多内置的异常类型，这些异常类型可以帮助我们识别和处理程序运行时遇到的问题。下面是一些常见的系统异常以及它们的说明：

1. NameError：当Python在局部或全局命名空间中找不到变量或函数时抛出。这通常是因为变量或函数未被定义或未正确导入。

2. TypeError：当Python无法将对象与正确类型进行匹配时抛出。这通常是因为使用了错误的参数类型或对象类型。

3. ValueError：当Python接收到正确类型的对象，但是这些对象的值不符合预期时抛出。这通常是因为使用了错误的参数值或对象值。

4. IndexError：当Python尝试访问列表、元组或其他序列类型中不存在的索引时抛出。这通常是因为使用了错误的索引值。

5. KeyError：当Python尝试访问字典中不存在的键时抛出。这通常是因为使用了错误的键值。

6. AttributeError：当Python尝试访问对象中不存在的属性时抛出。这通常是因为对象类型没有该属性或者属性名称被错误拼写。

7. ZeroDivisionError：当Python尝试将一个数除以0时抛出。这通常是因为代码逻辑错误或者输入数据错误导致的。

8. IOError：当Python无法读取文件或者文件不存在时抛出。这通常是因为文件路径错误或者文件权限问题导致的。

9. StopIteration：迭代器异常是指在使用迭代器遍历集合时可能会出现的异常情况。在Python中，迭代器通常是通过调用内置函数iter()来创建的。当迭代器调用next()方法时，如果已经到达了集合的末尾，就会抛出一个StopIteration异常，表示迭代已经结束。

这些是Python中常见的一些系统异常，当程序出现这些异常时，通常需要对其进行适当的处理，以便程序能够继续执行或者输出有用的错误信息。需要注意的是，这些异常只是Python中的一部分异常类型，还有许多其他的异常类型，需要根据具体情况进行处理。

**系统异常类继承树**

在Python中，内置的异常类都是继承自基类Exception的。Exception是所有异常类的基类，它本身又继承自BaseException类。所有的异常类都可以通过继承自这些基类来定义自己的异常。

下面是Python内置异常类的继承树：

```python
BaseException
├── SystemExit
├── KeyboardInterrupt
├── GeneratorExit
├── Exception
│   ├── StopIteration
│   ├── ArithmeticError
│   │   ├── FloatingPointError
│   │   ├── OverflowError
│   │   └── ZeroDivisionError
│   ├── AssertionError
│   ├── AttributeError
│   ├── BufferError
│   ├── EOFError
│   ├── ImportError
│   ├── LookupError
│   │   ├── IndexError
│   │   └── KeyError
│   ├── MemoryError
│   ├── NameError
│   │   └── UnboundLocalError
│   ├── OSError
│   │   ├── BlockingIOError
│   │   ├── ChildProcessError
│   │   ├── ConnectionError
│   │   ├── FileExistsError
│   │   ├── FileNotFoundError
│   │   ├── InterruptedError
│   │   ├── IsADirectoryError
│   │   ├── NotADirectoryError
│   │   ├── PermissionError
│   │   ├── ProcessLookupError
│   │   ├── TimeoutError
│   │   └── UnsupportedOperation
│   ├── ReferenceError
│   ├── RuntimeError
│   │   ├── NotImplementedError
│   │   └── RecursionError
│   ├── SyntaxError
│   ├── IndentationError
│   │   ├── TabError
│   │   └── UnindentError
│   ├── SystemError
│   ├── TypeError
│   ├── ValueError
│   │   ├── UnicodeError
│   │   │   ├── UnicodeDecodeError
│   │   │   └── UnicodeEncodeError
│   │   └── ValueError
│   ├── Warning
│   │   ├── DeprecationWarning
│   │   ├── PendingDeprecationWarning
│   │   ├── RuntimeWarning
│   │   ├── SyntaxWarning
│   │   ├── UserWarning
│   │   └── Warning
│   └── KeyboardInterrupt
```

在这个继承树中，所有的异常类都直接或间接继承自BaseException。SystemExit、KeyboardInterrupt和GeneratorExit是三个特殊的异常类，分别用于表示程序退出、用户中断和生成器退出。Exception是所有常规异常类的基类，它包含了大部分常规的异常类型，例如StopIteration、ArithmeticError、AssertionError、AttributeError、LookupError、OSError、TypeError、ValueError等等。Warning是所有警告异常的基类，它包含了各种警告类型，例如DeprecationWarning、RuntimeWarning、SyntaxWarning等等。

通过理解这个继承树，我们可以更好地了解Python中各种异常类型之间的关系，并且可以更好地使用它们来处理程序运行时可能遇到的各种问题。



#### 捕获和处理异常

1. `try...except`

在Python中，try...except语句是一种用于捕获和处理异常的语句，它的基本语法格式如下：

```python
try:
    # 可能会抛出异常的代码块
except [异常类型1 [as 异常实例1]]:
    # 异常类型1 的处理代码
except [异常类型2 [as 异常实例2]]:
    # 异常类型2 的处理代码
...
except [Exception [as 异常实例]]:
    # 通用异常处理代码
else:      # 可省略
    # 没有异常时执行的代码
finally:   # 可省略
    # 最终要执行的代码
```

在这个语法格式中，try语句包含了可能会抛出异常的代码块。这里不管会抛出多少个异常，只会从上往下检测，检测到一个后，就立即匹配下去，不会多次检测。

except语句包含了处理异常的代码块。except语句可以指定一个或多个异常类型，也可以使用通用的Exception类型来捕获所有可能的异常。当程序执行到try语句时，会尝试执行其中的代码块。如果代码块执行过程中出现了异常，就会跳转到对应的except语句，并执行其中的代码块。在except语句中，可以使用as关键字来指定一个异常实例，这个异常实例可以用于获取异常的详细信息。

如果没有出现异常，则会跳过所有的except语句，并执行else语句中的代码块。

在finally语句中，可以指定最终要执行的代码块，无论是否出现异常，这些代码都会被执行。

下面是一个简单的try...except语句的例子，用于处理除数为零的情况：

```python
try:
    x = 10 / 0
except ZeroDivisionError as e:   # as后面的名称可以自己定义
    print("除数为零：", e)
else:
    print("结果是：", x)
finally:
    print("程序执行结束")
    
    
# output
除数为零： division by zero
程序执行结束
```

在这个例子中，try语句尝试计算10除以0的结果，这会引发一个ZeroDivisionError异常。由于我们在except语句中指定了ZeroDivisionError类型，并将异常实例命名为e，因此程序会跳转到except语句，输出异常信息。最后，程序会执行finally语句，输出“程序执行结束”。

**注意**

1. 通过使用try...except语句，我们可以捕获和处理程序执行过程中可能出现的异常，以确保程序能够正常执行，或者提供有用的错误信息。需要注意的是，在处理异常时，需要根据具体情况选择合适的异常类型和处理方式，以便尽可能地准确地解决问题。

2. try语句没有捕获到异常，先执行try代码段后，再执行else，最后执行finally

3. 如果try捕获到异常，首先执行except处理错误，然后执行finally

4. 如果异常名称不确定，而又想捕获，可以直接写Exception

5. 如果代码段出现多个错误，只会对第一个错误进行处理，无论下面except有无对应的错误类型，如果没有，直接抛出异常，如果有则捕获异常

6. 如果针对于多个不同的异常有相同的处理方式，那么可以将多个异常合并。

   ```python
   # 将多种类型包装成元组
   except (ZeroDivisionError, NameError) : 
   ```


2. `with`

在 Python 中，`with` 语句提供了一种方便的方式来管理资源，例如打开和关闭文件、建立和断开数据库连接等等。它可以在代码块开始时自动获取资源，然后在代码块结束时自动释放资源，从而确保资源被正确地释放并且不会遗漏。

使用 `with` 语句可以避免手动管理资源时出现的一些常见问题，例如遗漏释放资源、资源泄漏、异常处理等等。这样可以使代码更加简洁、易读和可维护。

一个简单的 `with` 语句的示例是打开一个文件并读取其中的内容：

```python
with open('example.txt', 'r') as f:
    contents = f.read()
    print(contents)
```

在这个示例中，`with` 语句打开名为 `example.txt` 的文件，并将其赋值给变量 `f`。在代码块中，我们读取文件内容并打印它。当代码块结束时，`with` 语句会自动关闭文件，即使在代码块中出现异常也会如此。这可以确保文件被正确地关闭，从而避免资源泄漏问题。

3. 自定义上下文管理器

在 Python 中，我们可以通过实现上下文管理器来自定义 `with` 语句的行为。上下文管理器是一个对象，它可以定义在 `with` 语句中需要执行的一些操作，例如资源的获取和释放。一个对象要成为上下文管理器，它必须实现 `__enter__()` 和 `__exit__()` 方法。

`__enter__()` 方法在进入 `with` 代码块时被调用，并返回一个对象，这个对象将被赋值给 `as` 关键字后面的变量。`__exit__()` 方法在 `with` 代码块结束时被调用，无论代码块是否抛出异常，都会执行该方法。`__exit__()` 方法可以用来释放资源或者处理异常。

下面是一个简单的自定义上下文管理器的示例，它用于计时一个代码块的执行时间：

```python
import time

class Timer:
    def __enter__(self):
        self.start_time = time.time()
        return self
    
    def __exit__(self, exc_type, exc_value, traceback):
        self.end_time = time.time()
        print('Elapsed time: {:.6f}s'.format(self.end_time - self.start_time))

# 使用 Timer 上下文管理器计时代码块的执行时间
with Timer():
    time.sleep(1)  # 模拟执行时间
```

在这个示例中，`Timer` 类实现了 `__enter__()` 和 `__exit__()` 方法。在 `__enter__()` 方法中，我们记录了当前时间。在 `__exit__()` 方法中，我们再次记录当前时间，计算出代码块的执行时间，并打印出来。

在 `with Timer():` 语句中，我们创建了一个 `Timer` 对象，并使用 `with` 语句将其作为上下文管理器。当代码块执行完毕后，`__exit__()` 方法会被自动调用，输出代码块的执行时间。

在 Python 中，上下文管理器可以通过 `__exit__()` 方法来**处理异常**。当代码块中出现异常时，Python 解释器会将异常类型、异常值和 traceback 对象传递给 `__exit__()` 方法。我们可以在 `__exit__()` 方法中检查异常类型，并相应地处理异常。

下面是一个处理异常的上下文管理器的示例，它用于打开和关闭文件：

```python
class FileManager:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
        self.file = None
        
    def __enter__(self):
        try:
            self.file = open(self.filename, self.mode)
        except:
            print('Failed to open file')
            return None
        return self.file
    
    def __exit__(self, exc_type, exc_value, traceback):
        if self.file:
            self.file.close()
            
        if exc_type is not None:
            print('Exception occurred: {}: {}'.format(exc_type.__name__, exc_value))
            return True
```

在这个示例中，`FileManager` 类实现了 `__enter__()` 和 `__exit__()` 方法。在 `__enter__()` 方法中，我们尝试打开一个文件，并将文件对象存储在实例变量 `self.file` 中。如果打开文件失败，我们输出错误信息并返回 `None`。在 `__enter__()` 方法中，我们返回文件对象，这样就可以在代码块中使用文件对象了。

在 `__exit__()` 方法中，我们首先判断文件是否打开，如果打开则关闭文件。然后我们检查异常类型是否为 `None`。如果不是 `None`，说明在代码块中出现了异常，我们输出异常信息并返回 `True`，这样就可以将异常交给上层调用者处理。

使用上面的上下文管理器，我们可以像这样打开文件并读取其中的内容：

```python
with FileManager('example.txt', 'r') as f:
    if f is None:
        print('Failed to open file')
    else:
        contents = f.read()
        print(contents)
```

在这个示例中，`with` 语句会使用 `FileManager` 上下文管理器打开 `example.txt` 文件。如果文件打开失败，`__enter__()` 方法返回 `None`，我们输出错误信息。如果文件打开成功，我们读取文件内容并打印出来。当代码块执行完毕后，`__exit__()` 方法会被自动调用，如果出现异常，异常信息会被输出。

4. `contextlib`模块

   1. `@contextlib.contextmanager`

      `contextlib.contextmanager` 是 Python 标准库中 `contextlib` 模块提供的一个装饰器函数，它可以帮助我们更方便地定义上下文管理器。

      使用 `contextlib.contextmanager` 装饰器，我们可以将一个生成器函数转换成一个上下文管理器。生成器函数中的 `yield` 语句用来将控制权交给 `with` 语句，而 `yield` 语句之前的代码通常用来获取资源，而 `yield` 语句之后的代码通常用来释放资源。在 `yield` 语句之前的代码中，我们可以将资源传递给 `with` 语句中的代码块。

      下面是一个使用 `contextlib.contextmanager` 装饰器定义上下文管理器的示例，它用于计时一个代码块的执行时间：

      ```python
      import time
      from contextlib import contextmanager
      
      @contextmanager
      def Timer():
          start_time = time.time()
          yield
          end_time = time.time()
          print('Elapsed time: {:.6f}s'.format(end_time - start_time))
      
      # 使用 Timer 上下文管理器计时代码块的执行时间
      with Timer():
          time.sleep(1)  # 模拟执行时间
      ```

      在这个示例中，我们使用 `@contextmanager` 装饰器将 `Timer()` 函数转换成了一个上下文管理器。在 `Timer()` 函数中，我们记录了当前时间，并使用 `yield` 语句将控制权交给 `with` 语句中的代码块。在 `with` 代码块执行完毕后，`yield` 语句之后的代码会被执行，我们再次记录当前时间，并输出代码块的执行时间。

      使用 `contextlib.contextmanager` 装饰器定义上下文管理器的好处是，我们可以使用生成器函数来定义上下文管理器，这样可以使代码更加简洁和易读。同时，`contextlib.contextmanager` 装饰器还处理了一些错误处理和异常处理的细节，使得我们不必自己编写一些繁琐的代码。

      下面是一个使用该装饰器实现一个异常处理的上下文管理器的例子

      ```python
      from contextlib import contextmanager
      
      @contextmanager
      def ze():
          try:
              yield
          except ZeroDivisionError as e:
              print("error", e)
      
      
      x = 1
      y = 0
      with ze():
          x / y
      
      a = 1
      b = 0
      with ze():
          a / b
          
      # output
      error division by zero
      error division by zero
      ```

   2. `context.closing` 

      `contextlib.closing` 是 Python 标准库中 `contextlib` 模块提供的一个上下文管理器，它用于自动关闭实现了 `close()` 方法的对象。

      通常情况下，我们需要手动调用对象的 `close()` 方法来释放资源，例如关闭文件、关闭数据库连接等等。但是，如果我们在使用对象时忘记了调用 `close()` 方法，就可能会出现资源泄漏的问题。为了避免这种问题，我们可以使用 `contextlib.closing` 上下文管理器。

      `contextlib.closing` 接受一个对象作为参数，并返回一个上下文管理器，这个上下文管理器会自动在代码块结束时调用对象的 `close()` 方法。这样可以确保对象被正确地关闭，从而避免资源泄漏的问题。

      下面是一个使用 `contextlib.closing` 上下文管理器的示例，它用于自动关闭一个文件：

      ```python
      from contextlib import closing
      
      with closing(open('example.txt', 'r')) as f:
          contents = f.read()
          print(contents)
      ```

      在这个示例中，我们使用 `open()` 函数打开 `example.txt` 文件，并将文件对象作为参数传递给 `contextlib.closing` 函数。`contextlib.closing` 函数返回一个上下文管理器，我们使用 `with` 语句将其作为上下文管理器。在代码块中，我们读取文件内容并打印出来。当代码块执行完毕后，`contextlib.closing` 上下文管理器会自动调用文件对象的 `close()` 方法，从而确保文件被正确地关闭，避免资源泄漏的问题。

      使用 `contextlib.closing` 上下文管理器的好处是，我们不必手动调用对象的 `close()` 方法，从而避免忘记关闭对象的情况。同时，`contextlib.closing` 上下文管理器还处理了一些错误处理和异常处理的细节，使得我们不必自己编写一些繁琐的代码。

   3. `context.nexted` 

      `contextlib.nested` 是 Python 标准库中 `contextlib` 模块提供的一个上下文管理器，它可以让我们同时使用多个上下文管理器。

      `contextlib.nested` 接受多个上下文管理器作为参数，并返回一个上下文管理器，这个上下文管理器可以同时管理多个上下文管理器。在代码块中，我们可以使用多个上下文管理器，它们的作用会被合并起来。

      但是需要注意的是，`contextlib.nested` 函数在 Python 2 中被引入，但在 Python 3 中已经被弃用。在 Python 3 中，我们可以使用 `with` 语句嵌套的方式来达到类似的效果。

      下面是一个使用 `contextlib.nested` 上下文管理器的示例，它用于同时打开多个文件：

      ```python
      from contextlib import nested
      
      with nested(open('file1.txt', 'r'), open('file2.txt', 'r')) as (f1, f2):
          contents1 = f1.read()
          contents2 = f2.read()
          print(contents1)
          print(contents2)
      ```

      在这个示例中，我们使用 `contextlib.nested` 函数同时打开了 `file1.txt` 和 `file2.txt` 两个文件，并将它们的文件对象作为参数传递给 `contextlib.nested` 函数。`contextlib.nested` 函数返回一个上下文管理器，我们使用 `with` 语句将其作为上下文管理器。在代码块中，我们分别读取两个文件的内容，并打印出来。

      在 Python 3 中，我们可以使用 `with` 语句嵌套的方式来达到类似的效果。例如，上面的示例可以改写为：

      ```python
      with open('file1.txt', 'r') as f1, open('file2.txt', 'r') as f2:
          contents1 = f1.read()
          contents2 = f2.read()
          print(contents1)
          print(contents2)
      ```

      在这个示例中，我们使用 `with` 语句嵌套的方式同时打开了 `file1.txt` 和 `file2.txt` 两个文件，并将它们的文件对象赋值给变量 `f1` 和 `f2`。在代码块中，我们分别读取两个文件的内容，并打印出来。当代码块执行完毕后，两个文件对象会被自动关闭。

#### 手动抛出异常

在Python中，手动抛出异常通常需要使用`raise`语句。`raise`语句用于引发一个异常，并将控制权传递给异常处理程序。

以下是一个Python代码示例，演示如何手动抛出异常：

```python
def divide(x, y):
    if y == 0:
        raise ZeroDivisionError("除数不能为零") # 抛出一个ZeroDivisionError异常
    return x / y

try:
    result = divide(10, 0)
    print(result)
except ZeroDivisionError as e:
    print("出现异常：", e)
```

在这个示例中，我们定义了一个`divide`函数，该函数接受两个参数并返回它们的商。如果第二个参数为0，函数将抛出一个`ZeroDivisionError`异常。在`try`块中，我们调用`divide`函数并尝试计算10除以0，这将引发一个异常。然后我们使用`except`块来捕获该异常并打印错误消息。

请注意，当您手动抛出异常时，您可以选择任何异常类。在Python中，有许多内置的异常类可供使用，例如`ValueError`、`TypeError`、`IndexError`等。您还可以定义自己的异常类，以便更好地管理您的应用程序中的异常。

#### 自定义异常

在Python中，您可以通过创建一个新的异常类来定义自己的异常。通常情况下，您可以从Python内置的`Exception`类派生您的异常类，并添加您自己的属性和方法。

以下是一个Python代码示例，演示如何定义一个自定义异常类：

```python
class MyCustomException(Exception):
    def __init__(self, message, code):
        super().__init__(message)
        self.code = code

    def __str__(self):
        return f"{self.code}: {self.args[0]}"

try:
    raise MyCustomException("自定义异常", 500)
except MyCustomException as e:
    print(e)
```

在这个示例中，我们定义了一个名为`MyCustomException`的自定义异常类。该类从`Exception`类派生，并添加了一个名为`code`的属性和一个名为`__str__()`的方法，用于返回异常的字符串表示形式。在`__init__()`方法中，我们初始化了`message`和`code`属性，并调用了`super()`方法以便调用父类的构造函数。

然后，我们使用`raise`语句抛出一个新的`MyCustomException`异常。在`except`块中，我们捕获该异常并打印它的字符串表示形式。

当您在自己的应用程序中定义自定义异常时，请确保给它们一个有意义的名称，并使用它们来表示特定类型的异常情况。这样做可以使您的代码更加清晰和易于理解。





## 包和模块

#### 概念

1. **模块**：模块是一个Python文件，其中包含了一组相关的函数、类、变量和常量。通常情况下，每个模块都会定义一组相关的功能，以便在其他Python程序中重复使用

2. **包**：包是一个包含多个模块或者多个子包的有层次的文件目录结构。通常情况下，包中的每个模块都会定义一组相关的功能，以便在其他Python程序中重复使用，且该目录下一定包含`__init__.py`文件。

3. **库**：在计算机编程中，库是一组可重用代码的集合，该集合被打包在一起以便在多个程序或系统中共享和重复使用。库通常包含函数、类、变量和常量等元素，旨在提供特定领域的特定功能。

   与包和模块不同，库通常是独立的软件包，可以独立于主要应用程序之外进行开发和维护。库通常由第三方开发人员或团队创建，以便向其他开发人员提供可重用的功能，从而减少代码冗余和提高开发效率。

   在Python中，有许多流行的库可以帮助您执行各种任务，例如数据分析、Web开发、机器学习、图像处理等。一些常见的Python库包括：

   - NumPy：用于数值计算和科学计算的库
   - Pandas：用于数据分析和数据处理的库
   - Flask：用于Web开发的轻量级框架
   - Django：用于Web开发的全功能框架
   - TensorFlow：用于机器学习的库
   - Matplotlib：用于数据可视化的库

4. **框架**：在计算机编程中，框架是一种为特定领域的应用程序提供基础结构和功能的软件架构。框架提供了一个通用的结构，使开发人员可以编写自己的应用程序，而无需从头开始构建所有必需的功能。

   框架通常包含许多预定义的类、函数、接口和协议，这些元素可以帮助开发人员快速构建应用程序，并实现通用的编程模式和最佳实践。框架通常也提供了一些标准化的方式来组织和管理代码，以便使代码更易于维护和扩展。

   在Web开发中，框架通常用于构建Web应用程序。Web框架提供了一组用于处理HTTP请求和响应的类和函数，以及用于处理数据库、模板渲染、表单验证等常见任务的工具。一些常见的Python Web框架包括：

   - Flask：一个轻量级的Web框架，适用于小型应用程序和API
   - Django：一个全功能的Web框架，适用于大型Web应用程序和内容管理系统
   - Pyramid：一个灵活的Web框架，适用于各种规模的应用程序和API

#### 作用

- 组织代码：模块可以将相关的代码组织在一起，使代码更易于维护和理解。
- 提供可重用的功能：模块可以在不同的应用程序之间共享和重用，从而减少代码冗余。
- 支持命名空间：模块中的函数、类、变量和常量可以使用模块名作为前缀，以便在大型项目中避免名称冲突。

#### 分类

1. 标准包/模块：标准库包是Python语言本身提供的包，无需额外安装即可使用。这些包包括`os`、`sys`、`re`、`math`等，它们提供了许多常用的功能。
2. 第三方包/模块：第三方包是由第三方开发人员或团队开发的包，提供了各种不同的功能。这些包需要通过`pip`或其他包管理器进行安装，例如`numpy`、`requests`、`pandas`等。
3. 自定义包/模块



#### 一般操作

###### 创建

1. 创建模块: 直接创建一个`.py`文件, 并在其中定义一些函数、类、变量等元素即可
2. 创建包: 创建一个文件夹, 文件夹内务必创建一个`__init__.py`文件(其实python3.3版本之后不必创建, 但是为了代码兼容, 以及做一些其他包处理操作, 目前还是建议创建)
3. 创建多层级包: 在包里面创建另一个包即可, 可以无限极嵌套



###### 查看

`dir()` 

要查看模块的信息，您可以使用`help()`函数或`dir()`函数。例如，要查看名为`mymodule`的模块的信息，您可以执行以下操作：

```python
import mymodule

# 使用help()函数查看模块信息
help(mymodule)

# 使用dir()函数查看模块中的元素
print(dir(mymodule))
```

`__file__`

`__file__`是一个内置变量，在Python程序中可以用来获取当前模块的文件路径。具体来说，`__file__`变量包含了当前模块的绝对路径或相对路径。

当您在Python程序中使用`__file__`变量时，它将返回包含当前模块代码的文件的绝对路径或相对路径。例如，假设您有一个名为`mymodule.py`的模块，并且该模块的绝对路径为`/path/to/mymodule.py`，则以下代码将打印`/path/to/mymodule.py`：

```python
import os

print(os.path.abspath(__file__))
```

在这个例子中，`os.path.abspath()`函数用于将相对路径转换为绝对路径，并打印出当前模块文件的绝对路径。

`__file__`变量的主要作用是允许您在运行时获取当前模块的路径，以便您可以使用该路径来执行各种文件操作，例如读取文件内容、写入文件等。在一些特定的场景下，它也可以用于调试代码或构建动态的文件路径。

总之，`__file__`变量是一个非常有用的内置变量，可以帮助您获取当前模块文件的路径，或者查看包/模块的基本信息, 需要的是注意的是, 查看包时得到的是 `__init__.py` 路径



###### 导入

**方式**

1. `import M`: 使用`import`语句可以导入一个模块, 如果是某个包里面的模块, 则可以通过点语法来定位, 需要注意的是每次调用包时, 都会先执行包里面的`__init__.py` 文件

2. `import M1, M2` : 导入多个模块, 可以用逗号隔开

3. `import M as ...` : 使用import...as语句可以给导入的模块或函数起一个别名, 可以简化资源访问前缀, 增加程序的扩展性

4. `from ... import ...[as ...]`: 从一个模块中导入**指定**的函数、类或变量; 需要明确的是只能从大的地方找小的东西: 包 > 模块 > 模块资源, 而且注意面向关系, 即包只能看到模块, 模块只能看到模块资源

   ```python
   # 只能从包到模块, 模块到模块资源
   from p1 import Tool1 as t1, Tool2 as t2      # 多模块
   from p1 import Tool1, Tool2
   from p1.sub_p import sub_tool                # 多层级
   ```

5. `from ... import * [as ...]` : 导入一个模块或者包中的**所有非下划线开头**的公共函数、类和变量, 在使用时我们需要小心, 因为我们无法预知会导入哪些内容到当前位置, 容易产生变量名冲突

   ```python
   # 也可以通过在模块中重写__all__列表, 来选择我们所认为的需要从模块中导入的资源, 或者从包中需要导入的模块; 注意列表中每个元素都是字符串, 即引号包含变量名称或者文件名称
   __all__ = ["num1", ... ]
   ```

**注意**

1. 使用时需要指明资源的模块名称

2. 如果导入的是一个包, 默认不会导入任何模块, 所以我们要在`__init__` 文件中再次导入需要的模块, 即把导入模块的代码写入`__init__` 文件; 以`from ... import ...` 的形式导入

3. 导入模块: 首先在`sys.modules`中查找是否已经导入, 如果是第一次导入, 首先是在自己当下的命名空间中, 执行所有代码; 接着创建一个模块对象, 并将模块内所有顶级变量以属性的形式绑定到模块对象上(可通过`__dict__` 查看); 最后在`import` 的位置, 引入`import` 后面的变量名称到当前命名空间. 如果先前已经导入过, 那就属于第二次导入, 当第二次导入时, 直接进行上述最后一个步骤, 即从已经加载过的模块中去找, 也就是说, 多次导入模块时, 模块并不会多次执行

4. 上述几种导入方式不存在哪一种更节省内存, 区别在于要导入的内容而已. 

5. 当出现重名时, 从哪个位置找到需要导入的模块? 第一次导入时, 按照模块检索路径顺序寻找

   1. 第一级是内置模块
   2. 第二级是`sys.path`, 其构成是
      - 当前目录
      - 环境变量PYTHONPATH指定的路径列表
      - 特定路径下的`.pth`文件中的文件路径列表
      - 在python安装路径的lib库中搜索, 追加路径的方式

6. 追加路径方式

   1. 直接修改`sys.path`, 但注意修改后仅使用于该文件

      ```python
      import sys
      sys.path.append(r"C:\Users\ygtrece\Desktop")
      ```

   2. 修改环境变量

      可以添加在用户变量, 适用于当前该用户, 也可以添加在系统变量, 适用于该系统, 根据自己的需求即可; 添加的变量名为`PYTHONPATH`, 变量值为所需要添加的模块路径. 但是该方式只在shell中有效, 因为pycharm对系统环境变量支持不是很好, 所以有时候需要在settings的Interpreter Paths中手动添加. 

   3. 添加`.pth`文件

      `getsitepackage` 

      ```python
      import site
      print(site.getsitepackage())
      ```

      `getsitepackages()` 函数是 Python 中的一个函数，通常用于获取安装 Python 包的系统级目录。该函数返回一个由系统级 Python 包目录的路径组成的列表。

      具体而言，`getsitepackages()` 函数可以用于查找系统中所有已安装的 Python 包的目录。这些目录通常存储在一个名为 `site-packages` 的文件夹中，并且可以包含多个版本的 Python 包。在使用 `getsitepackages()` 函数时，它将会返回一个列表，其中包含了所有这些包的目录路径

      这个函数的返回值可以用于许多不同的目的，例如：

      - 查找并导入已安装的 Python 包
      - 为特定的 Python 脚本或应用程序创建虚拟环境
      - 将 Python 包安装到系统级目录中，以便其他用户可以轻松地使用它们
      - 可以在目录中加入写有我们需要导入的模块的路径的`.pth`文件，起到追加路径的作用

      需要注意的是，`getsitepackages()` 函数返回的路径可能因操作系统和 Python 版本而异。

7. 查看已加载模块

   `sys.modules` 是 Python 的一个内置模块，它是一个字典，用于存储 Python 中已经导入的模块。字典的键是模块名，值是模块对象。

   当你导入一个模块时，Python 会将模块对象存储在 `sys.modules` 字典中。下次导入相同的模块时，Python 会从 `sys.modules` 字典中返回已经存在的模块对象，而不是重新加载模块。

   `sys.modules` 可以用于检查哪些模块已经加载，以及获取已经加载的模块对象。例如，可以使用以下代码获取 `math` 模块的对象:

   ```python
   import sys
   
   math_module = sys.modules['math']
   ```

   `sys.modules` 还可以用于删除已经加载的模块，以及强制重新加载模块。例如，可以使用以下代码删除 `math` 模块的对象:

   ```python
   import sys
   
   if 'math' in sys.modules:
       del sys.modules['math']
   ```

   这样，下次导入 `math` 模块时，Python 会重新加载它。

   需要注意的是，尽管 `sys.modules` 可以用于删除和重新加载模块，但是这样做可能会导致未定义的行为和意外的结果。因此，在实际使用中，应该谨慎操作 `sys.modules`

**导入模块的常见情景**

1. 局部导入

   在局部范围内导入模块, 在其他范围无法使用, 所以如果想要全局范围都能使用, 在文件顶部导入相关模块

   ```python
   def cal():
   	import math
   	print(math.acos)
   
   cal()   # <built-in function acos>
   ```

2. 覆盖导入

   自定义模块和非内置标准模块重名, 根据前者存储位置, 有可能前者会覆盖后者; 所以自定义模块命名不要与后者重名;

   自定义模块和内置模块重名, 内置肯定覆盖自定义, 如果我们又特别需要使用自定义模块, 则需要使用`from ... import ... `指明绝对路径进行导入

3. 循环导入

   当两个或多个模块相互导入时，可能会出现循环依赖的问题。

   ```python
   # module_a.py
   import module_b
   
   def func_a():
       pass
   
   # module_b.py
   import module_a
   
   def func_b():
       pass
   ```

   在这个例子中，`module_a` 和 `module_b` 相互导入了对方，这可能会导致循环依赖的问题。为了避免这种情况，应该尽量避免相互导入，或者重构代码以消除循环依赖。

4. 可选导入

   可选导入：有时候，某些模块可能不存在，或者只在某些条件下才需要使用。在这种情况下，可以使用可选导入，以避免在模块不存在或者不需要使用时出现错误。例如：

   ```python
   try:
       import pandas as pd
   except ImportError:
       pd = None
   ```

   在这个例子中，我们尝试导入 `pandas` 模块，如果导入失败，则将变量 `pd` 设置为 `None`。这样，在后续代码中使用 `pd` 时，需要先检查 `pd` 是否为 `None`。

5. 包内导入

   绝对导入和相对导入

   理论: Python绝对导入和相对导入, 这两个概念是相对于包内导入而言的, 包内导入即包内模块导入包内部的模块

   概念: 

   1. 绝对导入

      参照`sys.path`路径进行检索; 例如指明包名或者模块名`import a` , `from a import b` ; 注意以上结论基于python3.x之后

   2. 相对导入

      使用`.`来指明相对路径, `.`是根据模块名称所获取的当前目录, `..`是根据模块名称所获取的上层目录; 例如`from . import a` , `from .. import a`; 





###### 三方包/模块的安装与升级

1. 概念: 三方包和模块是由第三方开发者编写的、可供其他 Python 程序使用的代码库。这些代码库通常提供了一些有用的函数、类和工具，可以帮助程序员更快、更方便地开发 Python 程序

2. 包管理项目

   目前有许多包管理工具, 但是官方支持的且认可度高的就两个: `distutils`, 它是官方标准库, 从python2到python3.6全部内置支持; `setuptools`, 是三方库, 在部分python子社区已经成为标准

   1. `distutils` : 是标准库的一部分, 能处理简单的包的安装, 通过`setup.py`进行安装
   2. `setuptools` : 现行的包安装标准, 自带一个`easy_install`安装脚本; 且引入了`.egg`格式; 是目前的主要选择
   3. [更多包管理项目](https://packaging.python.org/key_projects)

3. 常见已发布三方包和模块的形式: 

   1. 源码

      - 单文件模块
      - 多文件模块(由包管理工具发布的项目), 基于`distutils` 工具发布的项目特点, 包含`setup.py` 文件, `setuptools`也是基于`distutils`

   2. `.egg`

      `setuptools` 引入的一种格式, `setuptools`可以识别它, 安装它

   3. `.whl`

      本质是`.zip`格式, 是为了替代`.egg` 

4. 安装方式

   1. 本地安装

      - 对于单文件模块: 直接拷贝到相关文件夹就可以; 存放位置: `sys.path`中所包含的路径都可以, 一般存放在`Lib/site-package`文件夹中 

      - 对于带`setup.py`文件: 通过`setup.py`脚本即可安装

        步骤1: 打开命令行工具`cmd` 

        步骤2: 切换到`setup.py`文件所在目录

        步骤3: 执行命令`python3 setup.py install` (python3.x版本)

        注意: 如果项目是使用`distutils`打包的, 上述命令可以直接使用; 如果是用`setuptools`打包的, 有可能上述命令会报错

      - `.egg`文件: 使用setuptools的自带的安装脚本easy_install进行安装

        使用`setuptools`自带的安装脚本`easy_install`进行安装, 要求先安装`setuptools` 

        语法: `easy_install xxx.egg` 

      - `.whl`文件: 使用`pip`进行安装

        1. 使用`easy_install`安装

           语法: `easy_install xxx.whl` 

        2. 使用`pip` (推荐)

           安装`pip`

           1. 通过`easy_install`远程或者本地安装
           2. 远程: `easy_install pip` , 自动下载, 自动安装
           3. 本地: `easy_install xxx.egg` 或者 `easy_install xxx.whl`或者 `easy_install xxx.tar.gz` 

           使用语法

           `pip install xxx.whl` 

   2. 远程安装

      概念: 自动地从远程地址检索 -> 下载 ->安装某个模块

      安装方式

      - `easy_install`: 语法: `easy_install xxx` (后面可以直接写包的名称, 但需要先安装`setuptools`)
      - `pip` : 语法: `pip install xxx` (同样可以直接写包的名称, 且需要先安装`pip` )
      - `pycharm` 

      注意: 安装包是从`https://pypi.python.org/` 下载的, 一般安装在本地的`Lib/site_packages` 文件中

   3. 安装源

      - [Python官方](https://pypi.python.org/simple)
      - [豆瓣](https://pypi.douban.com/simple/)
      - 阿里
      - 中国科技大学





###### 模块的其他操作

1. `easy_install` 

   [详细介绍地址](https://peak.telecommunity.com/DevCenter/EasyInstall)

   其他常用操作

   - 多个python版本的切换安装

     如果一台电脑上既装了python2.x也安装了python3.x, 两个版本环境都装了setuptools, 都可以使用easy_install, 我们可以通过easy_install安装到指定版本的环境中, 语法是`easy_install-N.N` , `N.N`用于指明安装在哪个版本的环境中, 例如 `easy_install-3.6 requests` 

   - 安装指定版本包

     如果一个包有多个版本, 而有的项目使用的是某个特定版本, 则应该使用`easy_install "库名 限定符 版本[,限定符 版本]"` , 中括号部分代表可选, 库名是包的名称, 限定符有`< > <= >= ==` ; 例如`easy_install "requests >= 2.14.1"` 表示安装大于或等于2.14.1版本的最新包, `easy_install "requests > 1.0, <2.0"` 表示安装大于1.0并且小于2.0的包, `easy_install "requests == 2.14.1"` 安装该版本的包, 如果已安装则切换至该版本. 

   - 升级三方包

     有些包的作者, 修复了之前的某个bug, 本地需要更新到最新版本. 应该使用`easy_install --upgrade (-U) 库名` , 例如 `easy_install --upgrade requests` 

   - 卸载三方包

     有些已经安装的包, 因某些原因想要删除

     解决方法

     1. 手动卸载: 删除在`easy_install` 中的包记录, 并删除对应的包文件
     2. `easy_install -m 包名` : 效果是删除在`easy_install.pth`文件中对应的包记录, 需要注意的是, 并没有真正把`.egg`包文件删除, 不删除的原因是为了方便多版本切换, 但我们也可以手动删除包文件, 与此同时, 依赖包也不会被删除, 这是因为依赖包有可能被其他第三方包依赖

     补充

     1.  `easy_install.path`作用是记录着当前通过`easy_install`已经安装的模块, 多个版本的模块只记录最后一次安装的, 用于导入模块时的路径检索

     2. `-m`的真正作用: 便于支持多版本, 可在运行时进行切换, 如果不直接指明包的某个版本, 使得用户无法直接导入, 因为它删除了在`easy_install.pth`文件中对应包的记录 , 用户如果想使用某个版本, 需要使用如下代码, 例如

        ```python
        import pkg_resources
        pkg_resources.require("requests==2.18.4")
        import requests
        ```

   - 切换三方安装源

     有可能python官方库的托管平台服务器在国外导致安装速度慢甚至失败, 可以修改`easy_install.py`文件中的安装源路径

     

2. `pip` 

   [详细介绍地址](https://pip.pypa.io/en/stable/)

   其他常用操作

   - 切换安装源

     1. 一次性修改

        `pip install --index-url https://pypi.douban.com/simple/ requests` 指定检索, 仅仅只到某一个地址检索指定包

        `pip install --extra-url https://pypi.douban.com/simple/ requests` 扩展检索, 到官方的pypi地址检索, 检索失败后才到扩展的地址检索

     2. 永久性修改

        在c://users/username/ 中创建pip文件夹, 在`pip`文件夹中创建`pip.ini` 文件

        ```
        [global]
        index-url = http://pypi.douban.com/simple/
        [install]
        trusted-host=pypi.douban.com
        ```

     3. 安装源

   - 安装在不同的python版本环境中

     1. python2版本: `python -m pip install requests` 或者 `py -2 -m pip install requests` 

        python3版本: `python3 -m pip install requests` 或者 `py -3 -m pip install requests` 

     2. python的安装包实际上在系统中安装了一个启动器 `py.exe` , 启动器可以调用不同版本的python去执行某些脚本 `py -2` 和 `py -3` 

   - 查看包

     1. 所有已经安装的包 : `pip list`
     2. 不被依赖的包 : `pip list --not-required` 
     3. 所有过期的包: `pip list --outdated` , 如果出现警告, 可以使用 `pip list --outdated --trusted-host url` , `url` 是具体网址
     4. 查看某个包的具体信息: `pip show xxx` 

   - 搜索包

     `pip search xxx` : 例如 `pip search peppercorn` 

     `pip search -i url xxx`, 其中 `url` 表示检索地址, 可以手动选择检索地址

   - 安装特定版本

     `pip install "requests == 2.18"` 

     `pip install "requests >= 2.0"`

     `pip install "requests > 2.0, < 3.0"` 

   - 升级包

     `pip install --upgrade xxx` 

     注意: `pip install xxx` 检索到包存在时就不会安装了, 所以没有更新功能, 只有包不存在时才会安装到最新版本. 

   - 卸载包

     `pip uninstall xxx` 

     注意: 如果是通过`easy_install` 安装的, 那会自动删除`easy_install.pth`文件中对应包路径, 并且自动删除对应`.egg`包的原文件; 如果是通过`pip install` 安装的, 会直接删除对应包文件

   - 生成冻结需求文本

     可以将当前安装的三方包记录, 存储到指定的文件当中, 以后就可以根据这个需求文本去安装三方包

     `pip freeze`  生成除了`pip` 和 `setuptools` 之外的包信息

     `pip freeze > ./requirements.txt`  将包信息写入`requirements.txt` 文件

   - 根据冻结需求文本安装

     `pip install -r requirement.txt` 

     

3. 三方模块的版本规则

   版本由三部分组成 `n1.n2.n3 `

   - n3 : 当版本的bug修复之后, n3 + 1
   - n2 : 新增了一个小功能, n2 + 1
   - n1 : 修改了之前的功能, 或者添加了一个新功能(修改了之前俺的api), n1 + 1

   例如

   1. 发布了一个库 1.0.0
   2. 修复了一个bug 1.0.1
   3. 在库中新增了一个小功能 1.1.0
   4. 发布一个超大功能, api修改, 发布 2.0.0



#### 高级操作

**包和模块的发布**

0. 文档地址

     https://python-packaging.readthedocs.io/en/latest/minimal.html

1. 账号操作

   注册账号: https://pypi.python.org/pypi

   邮箱验证: http://pypi.org/manage/account/

2. 环境准备

   1. setuptools 安装

      https://pypi.python.org 搜索setuptools下载源码文件, 解压后打开命令行工具, 切换当前目录为`setup.py`所在目录(`cc xxx`), 在命令行中执行命令`python setup.py install` 或者 `python3 setup.py install` 

   2. pip 安装

      setuptools 安装完毕后会有一个安装脚本, 在命令行中执行`easy_install pip` 或者 `easy_install-3.6 pip` 

   3. wheel 安装

      在命令行中执行 `pip install wheel` 或者 `python3 -m pip install wheel` 

   4. twine 安装

      `pip install twine` 或者 `python3 -m pip install twine` 

   注意安装的python版本环境问题

3. 发布前准备

   1. 创建一个包项目

      项目结构

      ```
      项目名称
      	包名称             # 真正的包和模块
      		__init__.py
      		模块
      	模块
      	setup.py          # 非常重要, 必不可少
      	README.rst        # 可选补充
      	LICENSE.txt
      	MANIFEST.in
      ```

      命名建议

      - 全部小写
      - 多个单词以中划线`-`作为分割, 不要使用`_` , 因为pip安装对`_`支持不是很好
      - 不能和Pypi上已有的包名重复

      `setup.py` 

      - 作用: 项目信息的配置文件, 这个里面最重要的就是执行一个setup函数, 通过这个函数来指明信息

      - 示例

        ```python
        # 写法1
        from distutils.core import setup
        setup(形参1=实参1, 形参2=实参2)
        
        # 写法2(建议)
        from setuptools import setup
        setup(形参1=实参1, 形参2=实参2)
        ```

      - `setup`函数

        在 Python 包和模块中，可以使用 `setup.py` 文件来定义和配置项目的元数据信息，如名称、版本、作者、依赖项等，并且可以使用 `setuptools` 模块中提供的 `setup()` 函数来构建、打包和发布项目。

        下面是 `setup()` 函数中常用的一些参数及其作用：

        - `name`: 项目的名称，通常是一个字符串。
        - `version`: 项目的版本号，通常是一个字符串。
        - `description`: 项目的简要描述，通常是一个字符串。
        - `long_description`: 项目的详细描述，通常是一个包含多行文本的字符串，可以从 README 文件中读取。
        - `url`: 项目的主页或源代码仓库地址，通常是一个字符串。
        - `author`: 项目的作者姓名，通常是一个字符串。
        - `author_email`: 项目作者的电子邮件地址，通常是一个字符串。
        - `license`: 项目的许可证类型，通常是一个字符串。
        - `classifiers`: 项目的分类标签，通常是一个列表或元组，可以从 PyPI 的分类列表中选择。
        - `packages`: 项目的包含的 Python 包，通常是一个列表或元组。
        - `install_requires`: 项目的依赖项列表，通常是一个列表或元组。
        - `entry_points`: 项目的命令行入口点，通常是一个字典。

        除了上述参数之外，还有一些其他的参数可以用于 `setup()` 函数，如 `keywords`、`zip_safe`、`include_package_data`、`package_data` 等，这些参数的作用和用法可以参考官方文档。

        总之，`setup()` 函数是用于定义和配置 Python 项目元数据信息的重要函数，掌握其常用参数和用法对于开发和发布 Python 项目是非常有帮助的。

      - 具体的`setup.py`脚本文档 

        https://docs.python.org/2/distuils/setupscript.html

        https://packaging.python.org/tutorials/distributing-packages/
        
        

   2. `README.rst`文件

      Python包和模块中的README.rst文件是一个文本文件，通常位于包或模块的根目录下，用于描述该包或模块的功能、使用方法、注意事项等信息。该文件以reStructuredText格式编写，是Python社区广泛使用的一种文档格式。

      作用: 可以使用特定的字符, 来描述文本的格式, Pypi平台能够自动识别`long_description`字段中所写的这种格式的字符串; 同时提供给使用者和开发者一个简洁而又清晰的文档，方便他们了解该包或模块的用途和使用方法。同时，该文件也可以提供一些代码示例、注意事项、参考链接等信息，帮助使用者更好地使用该包或模块。

      以下是README.rst文件的一些基本语法：

      1. 标题：使用“=”，“-”等符号来表示一级、二级标题等。

      ```
      My Package
      ==========
      
      Subheading
      ----------
      ```

      2. 列表：使用“*”符号表示无序列表，使用“#.”表示有序列表。

      ```
      * Item 1
      * Item 2
      * Item 3
      ```

      3. 代码块：使用“::”表示代码块开始，使用缩进表示代码块中的内容。

      ```
      :: 
      
          def hello():
              print("Hello, World!")
      ```

      4. 强调：使用“*”或“**”表示强调。

      ```
      This is *italic* and this is **bold**
      ```

      5. 链接：使用“`链接文本 <链接地址>`_”表示链接。

      ```
      For more information, please see `the official documentation <https://docs.python.org/3/>`_.
      ```

      除了上述语法外，还可以使用其他reStructuredText语法来编写README.rst文件。具体语法文档说明https://zh-sphinx-doc.readthedocs.io/en/latest/contents.html

      在编写README.rst文件时，需要注意以下事项：

      1. 文件名必须为README.rst，大小写敏感；
      2. 文件内容必须使用reStructuredText格式编写；
      3. 尽量使用简洁明了的语言描述包或模块的功能和用途；
      4. 包或模块的使用方法应该尽可能详细，包括代码示例；
      5. 可以提供一些注意事项、参考链接等信息，方便使用者更好地使用该包或模块。

      语法检测: 

      1. 有时候会发现写的`rst`文件在pypi平台无法正常显示, 原因是pypi上对于rst的解析器问题, 并不是sphinx, 导致部分语法有一些差异
      2. 解决方案: 先从本地对`long_description`进行验证, 验证通过后再进行上传
      3. 步骤: 安装库 `pip install readme_renderer` , 执行命令 `python3 setup.py check -r -s` 

      

   3. `LICENSE.txt` 文件

      `LICENSE.txt`文件是一个文本文件，通常位于Python包或模块的根目录下，用于描述该包或模块的许可证信息。该文件包含许可证的文本内容，以及授权方式等信息，是开源软件项目必备的一部分。

      `LICENSE.txt`文件的作用是告知使用者该包或模块的许可证类型以及使用该包或模块的许可条件。在开源软件项目中，开发者通常会选择一种开源许可证，比如MIT许可证、BSD许可证、GPL许可证等，让使用者可以在符合许可证条件的前提下使用、修改和分发该软件。

      使用者在使用该包或模块时，应该仔细阅读`LICENSE.txt`文件中的许可证条款，并遵守许可证中规定的条件。如果使用者不同意许可证中的条件，则不能使用该软件。

      `LICENSE.txt`文件的编写要求和格式没有统一的标准，但通常应该包含以下信息：

      1. 许可证类型：应该明确指出所采用的许可证类型，比如MIT、BSD、GPL等；
      2. 许可证文本：应该将许可证的全文复制到`LICENSE.txt`文件中；
      3. 许可证授权方式：应该说明使用者可以如何使用该软件，比如可以免费使用、修改和分发该软件等；
      4. 许可证限制：应该说明使用者不允许做的事情，比如不允许删除版权声明、不允许将该软件用于商业用途等；
      5. 作者信息：应该明确指出该软件的作者或开发者；
      6. 其他信息：可以包括其他与许可证相关的信息，比如版本号、发布日期等。

      总之，`LICENSE.txt`文件是一个非常重要的文件，它告知用户使用该软件的条件和限制，为使用者和开发者之间建立了一种法律关系，保护了软件的知识产权。

      文件内容获取地址 https://choosealicense.com/

      

   4. `MANIFEST.in` 文件

      `MANIFEST.txt`文件是一个文本文件，通常位于Python包或模块的根目录下，用于描述该包或模块的文件清单。该文件列出了应该包含在发布版本中的所有文件，以及它们在包或模块中的相对路径。

      `MANIFEST.txt`文件的作用是帮助开发者在发布软件时，确保包或模块中的所有文件都被包括在发布版本中。在Python中，发布软件通常使用`distutils`或`setuptools`等工具来打包发布版本，这些工具可以使用`MANIFEST.txt`文件来确定应该包含哪些文件。

      例如

      ```python
      include README.rst
      include LICENSE.txt
      ```

      `MANIFEST.txt`文件的编写要求和格式没有统一的标准，但通常应该包含以下信息：

      1. 包含的文件列表：应该列出应该包括在发布版本中的所有文件，以及它们在包或模块中的相对路径；
      2. 排除的文件列表：可以列出应该排除在发布版本中的文件，比如测试文件、示例文件等；
      3. 包含的文件类型：可以指定应该包括哪些类型的文件，比如Python源代码文件、配置文件、文档等；
      4. 其他信息：可以包括其他与发布版本相关的信息，比如版本号、发布日期等。

      总之，`MANIFEST.txt`文件是一个帮助开发者管理包或模块文件的工具，它可以确保所有必要的文件都包含在发布版本中，并排除一些不必要的文件。使用`MANIFEST.txt`文件可以使发布软件的过程更加自动化、可靠和高效。

      具体官方文档

      1. https://docs.python.org/3/distuils/sourcedist.html#specifying-the-files-to-distribute
      2. 包含 `include *.txt`
      3. 递归包含 `recursive-include example *.txt *.py`
      4. 修剪 `prune examples/sample/build` 

      

   5. 编译生成发布包

      在命令行工具中执行

      1. 进入`setup.py`同级目录: `cd xxx` 

      2. 执行

         ```python
         python3 setup.py sdist
         python3 setup.py bdist
         python3 setup.py bdist_egg
         python3 setup.py bdsit_wheel
         python3 setup.py bdist_wininst
         ...
         ```

      3. 更多命令以及命令的具体作用可通过 `python3 setup.py --help-commands` 查看 

         

   6. 安装方式

      以上生成的发布包已经可以本地安装

      - 带 `setup.py`源码压缩包

        1. 方式1: 解压, 进入同级目录, 执行 `python3 setup.py install` 
        2. 方式2: `pip install xxx`
        3. 方式3: `easy_install xxx` 

      - 二进制发行包

      - windows下的安装文件

      - `.egg`文件

        `easy_install xxx.egg` 

      - `.whl`格式

        `easy_install xxx.whl` 

        `pip install xxx.whl` 

   

4. 发布过程

5. 发布后使用



#### 补充

1. 区分模块的测试和发布状态

   借助`__name__`来区分py文件被执行的模式

   - 直接执行: 值为`__main__`
   - 被当作模块执行: 值为模块名称

   示例

   ```python
   if __name__ == '__name__':
   	pass
   ```

2. 使用Pycharm安装包和模块

   在编译器中直接安装包和模块会比较方便

   

   

   

## 虚拟环境

#### 概念

Python中的虚拟环境是一种工具，可以为不同的Python项目创建独立的开发环境。虚拟环境允许您在同一计算机上同时运行不同版本的Python，以及不同的Python库和依赖项。这样，您可以在不影响其他项目的情况下，针对特定项目使用特定的Python版本和库。

虚拟环境的好处在于，它们可以帮助您避免因为不同项目之间的Python版本和依赖项冲突而导致的问题。它们还可以使得项目的部署和分享变得更加容易。

#### 安装

Python中有几个虚拟环境管理工具，其中最常用的是venv和virtualenv。venv是Python 3.3及以上版本自带的虚拟环境管理工具，而virtualenv是一个第三方库，可以在Python 2和Python 3中使用。

1. `venv`

使用venv创建一个新的虚拟环境的步骤如下：

1. 打开终端或命令行窗口。
2. 创建一个名为myenv的新虚拟环境：`python -m venv myenv`
3. 激活虚拟环境：`source myenv/bin/activate`（在Windows系统上，激活命令是`myenv\Scripts\activate`）
4. 在虚拟环境中安装所需的Python库和依赖项。
5. 在虚拟环境中完成项目开发后，使用`deactivate`命令退出虚拟环境。



2. `virtualenv`

使用virtualenv创建虚拟环境的步骤与上述类似，只是第二步需要使用virtualenv命令来创建虚拟环境。

安装命令: `pip install virtualenv` 

文档说明: https://virtualenv.pypa.io/en/latest/userguide

使用步骤

1. 创建一个局部的隔离的虚拟环境

   语法; `virtualenv xxx` , `xxx`是虚拟环境名称, 例如 `virtualenv ENV` 

   可选参数

   - `-p` 指明python版本创建, 后面加上python某一版本的解释器, 到时候就使用此版本的python解释器, 默认是安装virtualenv包的

     时候所在的python版本, 例如 `virtualenv - C:\Python\36\python3.exe ENV` 

   - `__system-site-packages` : 继承系统的三方库, 到时候检索库的时候也会到系统的三方库中找, 如果不加此项到时候只会在当前的虚拟环境中找, 例如 `virtualenv --system-site-packages ENV` 

2. 激活虚拟环境

   语法: 进入到虚拟环境目录/scripts文件夹中, 然后使用命令`activate`

3. 在激活状态下开发

4. 退出虚拟环境

   语法: 进入到虚拟环境目录/scripts文件夹中, 然后使用命令`deactivate.bat` 

5. 删除虚拟环境

   直接删除整个文件夹目录即可

补充: 以后把项目交给别人的时候, 如何能保证项目在别人的电脑跑得起来

解决方案

1. 连同虚拟环境和项目一起拷贝给别人
2. 在虚拟环境中冻结依赖需求文本, 把项目和依赖需求文本给别人, 别人自己在本地创建一个新的虚拟环境, 并根据依赖需求文本安装环境

3. 也可以使用Pycharm使用虚拟环境



#### 进阶

1. 集中式虚拟环境管理

   库名称: `virtualenvwrapper-win`, 基于`virtualenv`, 开发的一个工具包

   功能作用: 可以将之前分散在各个路径下的虚拟环境集中到统一的路径下进行管理, 方便各个虚拟环境之间的切换, 更加方便的去使用`virtualenv` 

   文档说明: https://pypi.python.org/pypi/virtrualenvwrapper-win

   使用说明:

   - 创建虚拟环境

     语法; `mkvirtualenv xxx` , `xxx`是虚拟环境名称  

     作用效果: 会创建在特定的文件夹中, windows下默认在用户目录的Envs文件夹中, 同时激活新建的虚拟环境

   - 查看所有虚拟环境

     语法: `lsvitualenv` 或者`workon` 

     作用效果: 列出当下创建的所有虚拟环境

   - 切换激活虚拟环境

     语法: `workon xxx`

     作用效果: 激活指定的虚拟环境

   - 关闭虚拟环境

      语法: `deactivate` 

     作用效果: 关闭当下所在的虚拟环境

   - 删除虚拟环境

     语法: `rmvirtualenv xxx` 

     作用效果: 删除指定虚拟环境以及对应的文件夹, 退出对应虚拟环境的激活状态

2. 更加基于项目的虚拟环境管理

   库名: `pipenv`

   功能作用: `pip + virtualenv`  更加基于项目, 使得我们更加关注于项目的管理, 工具内部封装了以上两个功能

   优势: 不需要再分别使用`pip`和`virtualenv`, 直接使用`Pipenv`即可, 会自动地帮你创建虚拟环境, 以及安装三方库, 会自动地记录你的项目依赖的所有三方库; 使用`Pipfile` 和 `Pipfile.lock`取代了`requirements.txt`

   文档说明: https://docs.pipenv.org

   在命令行中输出`pipenv` 或者 `pipenv --help`能帮助我们了解具体的命令使用说明

   使用说明: 

   - 创建虚拟环境

     语法: `pipenv --two` (python2) 或者`pipenv --three` (python3)

     查看相关信息

     - `pipenv --where` :  查看项目位置
     - `pipenv --venv` : 查看虚拟环境位置
     - `pipenv --py` : 查看解释器信息

   - 激活虚拟环境

     语法: `pipenv shell` 

     作用效果: 激活虚拟环境之后不会像之前那样在命令行前出现括号和虚拟环境名称, 但是在命令行窗口处会有 `pipenv shell` 的标识

     ![image-20230713150856934](C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20230713150856934.png)

   - 虚拟环境下开发

     - 执行代码 `python3 xxx.py` 会使用虚拟环境

     - 安装包

       命令: `pipenv install xxx` 

       作用效果:

       1. 检测当前项目对应的虚拟环境是否存在, 不存在则创建
       2. 在虚拟环境中安装指定的三方库, 如果没有指定则不安装
       3. 在项目目录下通过`pipfile` 和 `pipfile.lock` 记录当下已经安装的

       注意: 不要使用`pip install` , 虽然在虚拟环境中安装对应的包, 但是不会更新`pipfile` 和 `pipfile.lock` 

     - 查看包的依赖结构

       `pipenv graph` 

     - 卸载包

       `pipenv uninstall xxx`

   - 退出虚拟环境

     `exit` 或者直接关闭 `shell`窗口

   - 删除虚拟环境

     先`cd xxx` 进入对应的虚拟环境目录, 然后使用命令`pipenv --rm`

   补充: 以后上传项目给他人时直接传项目的源码以及 `pipfile` 和 `pipfile.lock` 文件即可. 

   

   

   















​	
