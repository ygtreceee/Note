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

概念:  



























类的属性和方法可以是公有的（即默认可访问），也可以是私有的（即只能在类中访问）。私有属性和方法以两个下划线`__`开头

```python
class Computer:
    brand = "Lenovo"
    
    def __init__(self, price):
        self.__price = price
        
    def __describe(self):
        print(f"This is a {self.brand} computer, priced at {self.__price}.")

    def describe(self):
        self.__describe()
        
        
在上面的例子中，price属性和describe方法都加上了两个下划线作为前缀，变成了私有属性和方法。私有属性和方法不能从类的外部访问，而只能从类内部访问。
```

在实际编程中，类是一个非常重要的概念，它可以将对象的属性和行为封装起来，使得代码更加可读、模块化和易于维护。
