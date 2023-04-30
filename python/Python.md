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

**数值**

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



**字符串**

由单个字符组成的一个集合

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

  ```
  name[index]
  index: 正数则从头部开始定位, 初始为0; 负数则从尾部开始定位, 初始为-1
  name[-1]: 表示字符串末位字符
  ```

- 获取一个字符串片段

  ```
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

  ```
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

  ```
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

  ```
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

  ```
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

  ```
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

  ```
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



**列表**

**有序**的**可变**的元素集合

1. 定义

- 方式1

  ```
  [ele1, ele2, ...]
  
  注意:
  列表集合其中的元素可以多种数据类型的元素, 且可以为空;
  列表本身也可以是一个元素, 可以列表嵌套列表;
  [1, 2, 3, ["a", "b", True]]
  ```

- 方式2

  ```
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

  ```
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

  ```
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

  ```
  l[index] = val;
  当我们以后要操作一个列表当中的某个元素时, 一定是通过这个索引(下标), 来操作指定元素的
  ```

- 查

  ```
  获取单个元素
  items[index]
  注意负索引
  
  获取元素索引
  list.index(val, start, end)
  同样可以限定索引区间, 也可以不写, 取默认值
  
  获取指定元素的个数
  list.count(val, start, end)
  
  获取多个元素
  list[start:end:step]
  [::-1]是反转列表
  
  遍历
  
  ```

- 额外操作

  ```
  
  ```

  

  **元组**





