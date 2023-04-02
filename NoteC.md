

# Note

# Knowledge

## 1.初识C语言

###### 定义

C语言是一门通用计算机编程语言，广泛应用于底层开发。C语言的设计目标是提供一种能以简易的方式编译、处理低级存储器、产生少量的机器码以及不需要任何运行环境支持便能运行的编程语言。尽管C语言提供了许多低级处理的功能，但仍然保持着良好跨平台的特性，以一个标准规格写出的C语言程序可在许多电脑平台上进行编译，甚至包含一些嵌入式处理器（单片机或称MCU）以及超级电脑等作业平台。二十世纪八十年代，为了避免各开发厂商用的C语言语法产生差异，由美国国家标准局为C语言制定了一套完整的美国国家标准语法，称为**ANSI C**，作为C语言最初的标准。目前2011年12月8日，国际标准化组织（ISO）和国际电工委员会（IEC）发布的**C11**标准是C语言的第三个官方标准，也是C语言的最新标准，该标准更好的支持了汉字函数名和汉字标识符，一定程度上实现了汉字编程。C语言是一门面向过程的计算机编程语言，与C++，Java等面向对象的编程语言有所不同。其编译器主要有Clang、GCC、WIN-TC、SUBLIME、MSVC、Turbo C等

###### 数据类型

**整型**

> 有符号整型
>
> 有符号整型的数据类型通常包括 `int、short、long、long long` 四种，因为是有符号类型，所以前面要加上 `signed`，但是通常省略，也就是说在代码中直接打出 int 类型就代表是有符号类型的

**int**
数据类型大小是 4 字节，能表示的数值范围是
-2^(32-1) – 2^(32-1)-1 （即 -2147483648 ~ 2147483647）
打印类型是 %d ，使用格式为 int 名 = 值;

**short**
数据类型大小是 2 字节，能表示的数值范围是
-2^(16-1) – 2(16-1) -1 （即 -32768 ~ 32767）
打印类型是 %hd ，使用格式为 short 名 = 值;

**long**
数据类型大小是 4 字节，能表示的数值范围是
-2^(32-1) – 2^(32-1)-1 （即 -2147483648 ~ 2147483647）
打印类型是 %ld ，使用格式为 int 名 = 值;

**long long**
数据类型大小是 8 字节，能表示的数值范围是
-2^(63) ~ 2^(63)-1 (这个数足够大了)
打印类型是 %lld ，使用格式为 long long 名 = 值;

> 无符号整型
>
> 无符号数用 unsigned 表示 ，只表示数据量，而没有方向（没有正负，且无符号数最高位不是符号位，而就是数的一部分，无符号数不可能是负数

**unsigned int **
数据类型大小是 4 字节，能表示的数值范围是
0 – 2^(32）-1 （即 0~4294967295）
打印类型是 %u ，使用格式为 unsigned int 名 = 值;

**unsigned short **
数据类型大小是 2 字节，能表示的数值范围是
0 ~ 2^8 -1 （即 0~65535）
打印类型是 %hu ，使用格式为 unsigned short 名 = 值;

**unsigned long **
数据类型大小是 4 字节，能表示的数值范围是
0 – 2^(32）-1 （即 0~4294967295）
打印类型是 %lu ，使用格式为 unsigned long 名 = 值;

**unsigned long long **
数据类型大小是 8 字节，能表示的数值范围是
0~2^63-1
打印类型是 %llu ，使用格式为 unsigned long long 名 = 值;

```
unsigned int a = 10u;  // 简写成 unsigned int a = 10;
unsigned short b = 20u;// 简写成 unsigned short b = 20;
```

**字符型**

>字符型变量用于存储一个单一字符，在 C 语言中用 char 表示，其中每个字符变量都会占用 1 个字节。在给字符型变量赋值时，需要用一对英文半角格式的单引号 '' 把字符括起来。字符变量实际上并不是把该字符本身放到变量的内存单元中去，而是将该字符对应的 **ASCII 编码**放到变量的存储单元中。char的**本质就是一个1字节大小的整型**

char 的格式匹配符（打印格式) 为：%c

数值表示范围是：
有符号: -2^(8-1) – 2(8-1) -1 （即 -128 ~ 127）
无符号： 0 ~ 2^8 -1 （即 0~255）

```
int main()
{
	char ch = 'A';
	printf("ch = %d\n", ch);//65
	return 0;
}
```

**浮点型**

**单精度浮点型（float）**
单精度浮点型的大小是 4 字节

```
float v1 = 4.345;
unsigned float v1 = 4.345; 无符号的 float 数据
格式匹配符是：%f ， 默认保留 6 位小数。
```

**双精度浮点型（double）**
双精度浮点型的大小为 8 字节

```
double v2 = 5.678;
unsigned double v2 = 5.678; //无符号的 double 数据
printf(“n = %08.3f\n”, n);
//输出的含义为：显示8位数（包含小数点）， 不足8位用0填充。并且保留3位小数。对第4位做四舍五入

int main(void)
{
	float m = 3.145;
	double n = 4.566545;

	printf("m = %08.2f\n", m);//m = 00003.14
	printf("n = %08.3lf\n", n);//n = 0004.567
	return0;
}
```

###### 变量

定义变量的方法

```
int age = 150;
float weight = 45.5f;
char ch = 'w';
```

**变量分类**

- 局部变量
- 全局变量

```
#include <stdio.h>
int global = 2019;//全局变量
int main()
{
	int local = 2018;//局部变量
	int global = 2020;//accepted
	return 0;
}
```

>上面的局部变量global变量的定义是标准接受的
>
>当局部变量和全局变量同名的时候, ==局部变量优先使用==
>
>注: 不建议把全局变量和局部变量的名字写成一致

**变量的作用域和生命周期**

作用域

> 作用域(scope)是程序设计概念, 通常来说, 一段程序代码中所用到的名字并不总是有效的
>
> 而限定这个名字的可用性的代码范围就是这个名字的作用域
>
> 1. 局部变量的作用域是变量所在的局部范围
> 
> 2. 全局变量的作用域是整个过程

生命周期

> 变量的生命周期指的是变量的创建到变量的销毁之间的一个时间段
>
> 1. 局部变量的生命周期是: 进入作用域生命周期开始, 出作用域生命周期结束
> 2. 全局变量的生命周期是: 整个程序的生命周期

###### 常量

- 字面常量
- const 修饰的常变量
- #define 定义的标识符常量
- 枚举常量

```
#include <stdio.h>
enum Sex
{
	//枚举常量
	MALE,
	FEMALE,
	SECRET
};

int main()
{
	//字面常量
	3.14;
	1000;
	
	//const修饰的常变量
	const float pai = 3.14f;
	pai = 5.14;//error
	
	//#define的标识符常量
	#define MAX 100
	printf("max = %d\n", MAX);
}
```

> 上面的pai被称为const修饰的常变量, const修饰的常变量在C语言中只是在语法层面限制了变量pai不能直接被改变, 但是pai本质上还是一个变量, 所以叫常变量

> 即const修饰变量，这个变量就变成常变量，不可被修改，但是本质还是变量.
> const修饰指针变量的时候，如果放在*左边，例如const int* p  修饰的是*p，表示指针指向的内容，是不能通过指针来改变的,但是指针变量本身是可以修改的，例如p=&n；如果放在*右边，例如int* const p,修饰的是p，表示指针变量p本身，则p不能被改变，即不能够p=&n，但是它所指向的内容是可以改变的，例如*p=10；但是还可以双const，例如int const* const p

###### 字符串

> 这种由双引号(Double Quote)引起来的一串字符称为字符串字面值(String Literal), 或者简称字符串

注: 字符串的结束标志是一个\0的转义字符(字符串在结尾位置隐藏了一个\0的字符), 在计算字符串长度的时候\0是结束标志, 不算做字符串内容.

***strlen***求字符串长度不计入'\0'

易错

```
int main()
{
	char a[1000];
	char b[3];
	scanf("%s", b);//输入abc
	scanf("%s", a);//输入def
	printf("%p\n", a);//000000000061D710
	printf("%p\n", b);//000000000061D70D
	printf("%s\n", b);//abcdef
	return 0;
}


//此处为什么打印b会输出abcdef?
//因为栈区储存是由高地址到低地址, 所以b放在a的上端,输入abc,会自动添加'\0',但是b中已经没有空间放'\0',所以会放到a[0]中去,等到a再被赋值,会在a[4]才出现'\0',所以打印b会输出a和b的内容


int main()
{
	char a[1000];
	char b[3];
	scanf("%s", a);//abc
	scanf("%S", b);//def
	printf("%c", a[0])//为'\0',无输出
	return 0;
}

//此处a[0]不是a,却是'\0',再次印证'\0'会被放到b后面的内存空间
```



###### 转义字符

> 转义字符(Escape character), 所有的[ASCII码](https://baike.baidu.com/item/ASCII码?fromModule=lemma_inlink)都可以用"\\"加数字(一般是8进制数字)来表示. 而[C](https://baike.baidu.com/item/C/7252092?fromModule=lemma_inlink)中定义了一些字母前加"\\"来表示常见的那些不能显示的ASCII字符, 如\0,\t,\n等, 就称为转义字符, 因为后面的[字符](https://baike.baidu.com/item/字符/4768913?fromModule=lemma_inlink), 都不是它本来的ASCII字符意思了.

```
#include <stdio.h>
int main()
{
	//打印一个单引号'
	printf("%c\n", '\'');
	//打印一个双引号"
	printf("%c\n", "\"");
	//\62被解析成一个转义字符
	printf("%d\n", strlen("c:\test\628\test.c"));
	return 0;
}
```

ASCII

###### 注释

1. 代码中有不需要的代码可以直接删除, 也可以注释掉
2. 代码中有些代码比较难懂, 可以加一下注释文字

- C语言风格注释 /* xxxxxx */

  缺陷: 不能嵌套注释

- C++风格注释  //xxxxxxx

  可以注释一行也可以注释多行

## 2. 语句

#### 语句分类

三种语句结构:

1. 选择结构
2. 循环结构
3. 顺序结构

C语句可分为五类:

1. 表达式语句
2. 函数调用语句
3. 控制语句
4. 复合语句
5. 空语句

**控制语句**用于控制程序的执行流程, 以实现程序的各种程序方式, 它们由特定的语句定义符组成, C语言有九种控制语句

可分为以下三类:

1. 条件判断语句也叫分支语句: if语句, switch语句
2. 循环执行语句: do while语句, while语句, for语句
3. 转向语句: break语句, goto语句, continue语句, return语句

#### 分支语句(选择结构)

>  C语言中非0表示真, 0表示假

**if语句**

> else是和它离得最近的if匹配的

```
int num = 1;
if(num == 5)	;
//
int num = 1;
if(5 == num)	;

//第二种代码风格更好, 逻辑更加清晰
```

**switch语句**

> case后面只能接整型常量表达式
>
> break语句的效果实际就是把语句列表划分为不同的分支部分
>
> 建议: 在最后一个case语句的后面加上一条break语句,可避免忘记添加break; 在每个switch语句后面都放一条default子句,甚至可以在后面加上break

```
//用法
switch()
{
case 整型常量表达式:
	//内容;
	break;	
default:
         ;
}
```

```
int main()
{
	int day = 0;
	switch(day)
	{
		case 1:
		case 2:
		case 3:
		case 4:
		case 5:
		    printf("weekday\n");
		    break;
		case 6:
		case 7:
		    printf("weekend\n");
	}
}
```

**while语句**

>  break: 停止后期所有的循环, 直接终止循环, 所以while中break是用于永久终止循环的.
>
> continue: 用于终止本次循环, 也就是本次循环中continue后边的代码不会再执行, 而是直接跳转到while语句的判断部分, 进行下一次循环的入口判断.

**for循环**

> for循环中也可以出现break和continue, 意义和在while中一样, 但是需要特别注意的是, for循环中continue之后会执行调整部分.
>
> 建议: 不可在for循环体内修改循环变量, 防止for循环失去控制

```
for(表达式1; 表达式2; 表达式3)
     ;
//1,2,3都可以根据实际情况省略
//1:初始化部分  2:条件判断部分  3:调整部分
```

```
#include <stdio.h>
int main()
{
	for(int i=0, int k=0; k=0; i++, k++)
		k++;
	return 0;
}
//此处判断部分不是k==0, 而是k为假, 即不成立, 0次循环
```

**do...while循环**

> 先执行后判断
>
> 循环至少执行一次, 且使用场景有限

**goto语句**

> C语言中提供了可以随意滥用的goto语句和标记跳转的标号, 从理论上goto语句是没有必要的, 实践中没有goto语句也可以很容易写出代码, 但是某些场合下goto语句仍然有用, 最常见的就是终止程序在某些深度嵌套的结构的处理过程.
>
> 例如: 一次跳出两层循环或多层循环
>
> 多层循环这种情况使用break是达不到目的的, 它只能从最内层循环退出到上一层的循环

```
for()
	for()
	{
		for()
		{
			id(disaeter)
				goto error;
		}
	}
	...
error:
	if(disaster)
		//处理错误情况
```

```
//关机程序
#include <stdio.h>
#include <stdlib.h>
int main()
{
	char input[10] = {0};
	system("shutdown -s -t 60");
again:
	printf("电脑将在1分钟内关机, 如果输入: 我是猪, 就取消关机!\n请输入:>");
	scanf("%s", input);
	if(0 == strcmp(input, "我是猪"))
	{
		system("shutdown -a");
	}
	else
	{
		goto again;
	}
	return 0;
}

//

#include <stdio.h>
#include <stdlib.h>
int main()
{
	char input[10] = {0};
	system("shutdown -s -t 60");
	while(1)
	{
		printf(""电脑将在1分钟内关机, 如果输入: 我是猪, 就取消关机!\n请输入:>");
		scanf("%s", input);
		if(0 == strcmp(input, "我是猪"))
		{
			system("shutdown -a");
			break;
		}
	}
	return 0;
}
//更多shutdown命令可至win+R -> cmd
```

## 3.操作符

###### 操作符分类

>算术操作符
>
>位移操作符
>
>位操作符
>
>赋值操作符
>
>单目操作符
>
>关系操作符
>
>逻辑操作符
>
>条件操作符
>
>逗号操作符
>
>下标引用, 函数调用和结构成员

###### 算术操作符

> \+  	\-     /  	%

1. 除了 % 操作符之外，其他的几个操作符可以作用于整数和浮点数。
2. 对于 / 操作符如果两个操作数都为整数，执行整数除法。而只要有浮点数执行的就是浮点数除法。
3. % 操作符的两个操作数必须为整数。返回的是整除之后的余数。

###### **移位操作符**

> \<<  左移操作符
>
> \>> 右移操作符
>
> 注意
>
> 1. 移位操作符的操作数只能是整数
> 2. 移位操作符移动的是二进制位
> 3. 对于移位操作符, 不要移动负数位, 这是标准未定义的
> 4. 位移之后若没有赋值, 自身的值不会发生变化
>
> ```
> int num = 10;
> num>>-1;//error
> ```

**左移操作符**

移位规则: 左边抛弃, 右边补0

<img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20221018141846977.png" alt="image-20221018141846977" style="zoom:67%;" />

**右移操作符**

移位规则: 分为两种

1. 逻辑位移: 左边用0补充, 右边丢弃
2. 算术位移: 左边用原该值的符号位填充, 右边丢弃

<img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20221018142128327.png" alt="image-20221018142128327" style="zoom:67%;" />

###### 位操作符

> &   按位与
>
> |     按位或
>
> ^    按位 (相同为0, 相异为1)
>
> 注：他们的操作数必须是整数

```
a^a == 0
a^0 == a
```

```c
//不能创建临时变量(第三个变量), 实现两个数的交换
#include <stdio.h>
int main()
{
	int a = 10, b = 20;
	a = a^b;
	b = a^b;
	a = a^b;
	printf("a = %d  b = %d", a, b)//a = 20  b = 10
	return 0;
}
```

```c
//编写代码实现：求一个整数存储在内存中的二进制中1的个数
#include <stdio.h>
int main()
{
 	int num = -1;
 	int i = 0;
 	int count = 0;//计数
 	while(num)
 	{
	count++;
 	num = num&(num-1);
 	}
 	printf("二进制中1的个数 = %d\n",count);
 	return 0;
}
```

```c++
//判断一个数是不是2的n次方
bool Judge(int n)
{
	if(n&(n-1) == 0)	bool = true;
	else	bool = false;
}
```

```c
//判断两个整数二进制格式有多少个位不同
#include <stdio.h>
#include <math.h>
int main()
{
	int m = 0, n = 0, cntm = 0;
	for (int i = 0; i < 32; i++)
    {
        if((m >> i) & 1 == 1)	cntm++;
        if((n >> i) & 1 == 1)	cntn++;
       	if(i == 31)	printf("%d", abs(cntm - cntn));
    }
	return 0;
}
```

###### 赋值操作符

> '='

```
//赋值操作符可以连续使用, 即连续赋值
a = x = y+1;
```

复合赋值符

>+=    -=	*=	/=	%=	>>=	<<=	&=	^=	|=	  

###### 单目操作符

>!      逻辑反操作
>
>\-      负值
>
>\+      正值
>
>&      取地址
>
>sizeof    操作数的类型长度（以字节为单位）
>
>~      对一个数的二进制按位取反
>
>--      **前置、后置**--
>
>++      **前置、后置**++
>
>\*      间接访问操作符(解引用操作符)
>
>(类型)    强制类型转换

###### **关系操作符**

> \>	\>=	<	<=	!=   ==    
>
> 特别注意: 极易将 == 错写成 = , 前者是关系比较, 后者为赋值

###### 逻辑操作符

> &&   逻辑与
>
> ||      逻辑或
>
> 注意区分: 逻辑与和按位与, 逻辑或和按位或
>
> ```
> 1&2----->0
> 1&&2---->1
> 1|2----->3
> 1||2---->1
> ```

```c
//清楚逻辑操作符原理
//逻辑与遇假停止判断, 逻辑或遇真停止判断
#include <stdio.h>
int main()
{
    int i = 0,a = 0,b = 2,c = 3,d = 4;
    i = a++ && ++b && d++;
    //a = 1, b = 2, c = 3, d = 4
    //i = a++||++b||d++;
    //a = 1, b = 3, d = 4
    printf("a = %d\n b = %d\n c = %d\nd = %d\n", a, b, c, d);
    return 0;
}
```

###### 条件操作符

```
exp1 ? exp2 : exp3
```

###### **逗号表达式**

> 逗号表达式，就是用逗号隔开的多个表达式
>
> 逗号表达式，从左向右依次执行。整个表达式的结果是最后一个表达式的结果。

```
exp1, exp2, exp3, …expN
```

```c
//
int a = 1;
int b = 2;
int c = (a>b, a=b+10, a, b=a+1);//c = 13

//
if (a =b + 1, c=a / 2, d > 0)

//
a = get_val();
count_val(a);
while (a > 0)
{
		//
}
如果使用逗号表达式，改写：
while (a = get_val(), count_val(a), a>0)
{
         //
}
```

###### **下标引用、函数调用和结构成员**

1. [ ] 下标引用操作符

​	操作数：一个数组名 + 一个索引值

2. ( ) 函数调用操作符

   接受一个或者多个操作数：第一个操作数是函数名，剩余的操作数就是传递给函数的参数

3. 访问一个结构的成员 

    **.**     结构体.成员名

   **->**   结构体指针->成员名

###### **表达式求值**

表达式求值的顺序一部分是由操作符的优先级和结合性决定;  同样, 有些表达式的操作数在求值的过程中可能需要转换为其他类型

###### **隐式类型转换**

C的整型算术运算总是至少以缺省整型类型的精度来进行的, 为了获得这个精度, 表达式中的字符和短整型操作数在使用之前被转换为普通整型, 这种转换称为**整型提升**

整型提升的意义:
表达式的整型运算要在CPU的相应运算器件内执行, CPU内整型运算器(ALU)的操作数的字节长度一般就是int的字节长度, 同时也是CPU的通用寄存器的长度. 因此, 即使两个char类型的相加, 在CPU执行时实际上也要先转换为CPU内整型操作数的标准长度.
通用CPU(general-purpose CPU)是难以直接实现两个8比特字节直接相加运算(虽然机器指令中可能有这种字节相加指令).所以, 表达式中各种长度可能小于int长度的整型值, 都必须先转换为int或unsigned int, 然后才能送入CPU去执行运算.

```
//实例1
//b和c的值被提升为普通整型，然后再执行加法运算
char a,b,c;
...
a = b + c;
```

如何进行整体提升呢?

整形提升是按照变量的数据类型的符号位来提升的

```
//负数的整形提升
char c1 = -1;
变量c1的二进制位(补码)中只有8个比特位：
1111111
因为 char 为有符号的 char
所以整形提升的时候，高位补充符号位，即为1
提升之后的结果是：
11111111111111111111111111111111
//正数的整形提升
char c2 = 1;
变量c2的二进制位(补码)中只有8个比特位：
00000001
因为 char 为有符号的 char
所以整形提升的时候，高位补充符号位，即为0
提升之后的结果是：
00000000000000000000000000000001
//无符号整形提升，高位补0
```

```
//实例1
int main()
{
 char a = 0xb6;
 short b = 0xb600;
 int c = 0xb6000000;
 if(a==0xb6)
 printf("a");
 if(b==0xb600)
 printf("b");
 if(c==0xb6000000)
 printf("c");
 return 0;
}

//实例1中的a,b要进行整形提升,但是c不需要整形提升
a,b整形提升之后,变成了负数,所以表达式 a==0xb6 , b==0xb600 的结果是假,但是c不发生整形提升,则表达式 c==0xb6000000 的结果是真.
//所以程序输出的结果是:
c
```

```
//实例2
int main()
{
	char c = 1;
	printf("%u\n", sizeof(c));
	printf("%u\n", sizeof(+c));
	printf("%u\n", sizeof(-c));
	return 0;
}
//实例2中的,c只要参与表达式运算,就会发生整形提升,表达式 +c ,就会发生提升,所以 sizeof(+c) 是4个字节.表达式 -c 也会发生整形提升,所以 sizeof(-c) 是4个字节,但是 sizeof(c) ,就是1个字节.
```

###### **算术转换**

如果某个操作符的各个操作数属于不同的类型，那么除非其中一个操作数的转换为另一个操作数的类型，否则操作就无法进行。下面的层次体系称为**寻常算术转换**

```
long double
double
float
unsigned long int
long int
unsigned int
int

//如果某个操作数的类型在上面这个列表中排名较低,那么首先要转换为另外一个操作数的类型后执行运算

//警告：但是算术转换要合理，要不然会有一些潜在的问题。
float f = 3.14;
int num = f;//隐式转换，会有精度丢失
```

###### **操作符的属性**

复杂表达式的求值有三个影响的因素

1. 操作符的优先级
2. 操作符的结合性
3. 是否控制求值顺序

两个相邻的操作符先执行哪个取决于他们的优先级. 如果两者的优先级相同, 取决于他们的结合性.

**总结**：我们写出的表达式如果不能通过操作符的属性确定唯一的计算路径，那这个表达式就是存在问题

的。

操作符==优先级==

![image-20221018155824885](C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20221018155824885.png)
![image-20221018155549644](C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20221018155549644.png)

```
//表达式的求值部分由操作符的优先级决定。
//表达式1
a*b + c*d + e*f
//在计算的时候，由于*比+的优先级高，只能保证，*的计算是比+早，但是优先级并不能决定第三个*比第一个+早执行
//所以表达式的计算机顺序就可能是:
a*b
c*d
a*b + c*d
e*f
a*b + c*d + e*f
或者：
a*b
c*d
e*f
a*b + c*d
a*b + c*d + e*f


//表达式2
c + --c;
//同上，操作符的优先级只能决定自减--的运算在+的运算的前面，但是我们并没有办法得
知，+操作符的左操作数的获取在右操作数之前还是之后求值，所以结果是不可预测的，是有歧义
的。


//代码3-非法表达式
int main()
{
	int i = 10;
	i = i-- - --i * ( i = -3 ) * i++ + ++i;
	printf("i = %d\n", i);
	return 0;
}
//不同编译器会导致不同答案


//代码4
int fun()
{
     static int count = 1;
     return ++count;
}
int main()
{
     int answer;
     answer = fun() - fun() * fun();
     printf( "%d\n", answer);//输出多少？
     return 0;
}
//这个代码存在实际问题!
//虽然在大多数的编译器上求得结果都是相同的, 但是上述代码 answer = fun() - fun() * fun(); 中我们只能通过操作符的优先级得知: 先算乘法, 再算减法. 函数的调用先后顺序无法通过操作符的优先级确定。


//代码5
#include <stdio.h>
int main()
{
 int i = 1;
 int ret = (++i) + (++i) + (++i);
 printf("%d\n", ret);
 printf("%d\n", i);
 return 0;
}
//在linux 环境gcc编译器: 10 4
//在VS2013环境下: 12 4
//同样的代码产生了不同的结果, 这是因为这段代码中的第一个 + 在执行的时候，第三个++是否执行，这个是不确定的，因为依靠操作符的优先级和结合性是无法决定第一个 + 和第三个前置 ++ 的先后顺序
```



























## 4.函数

###### 定义

> 维基百科中对函数的定义: 子程序
>
> - 在计算机科学中, 子程序(英语: Subroutine, procedure, function, routine, method, 
>
> subprogram, callable unit), 是一个大型程序中的某部分代码, 由一个或多个语句块组
>
> 成. 它负责完成某项特定任务, 而且相较于其他代码, 具备相对的独立性.
>
> - 一般会有输入参数并有返回值, 提供对过程的封装和细节的隐藏, 这些代码通常被集成为软
>
> 件库.

###### 库函数

>为了支持可移植性和提高程序的效率, C语言的基础库中提供了一系列类似的库函数, 方便程序员进行软件开发. 

> 使用库函数必须包含头文件

>库函数查询:
>
>MSDN(Microsoft Developer Network)
>
>www.cplusplus.com
>
>https://en.cppreference.com
>
>https://zh.cppreference.com

C语言常用的库函数有:

- IO函数
- 字符串操作函数
- 字符操作函数
- 内存操作函数
- 时间/日期函数
- 数学函数
- 其他库函数

###### 自定义函数

> 与库函数, 需要函数名, 返回值类型, 函数参数

```
ret_type fun_name(para1, * )
{
	statement;//语句项
}
ret_type 返回类型
fun_name 函数名
para1    函数参数
```

###### 函数参数

**实际**参数(实参)

> 真实传给函数的参数. 
>
> 可以是: 常量, 变量, 表达式, 函数等
>
> 无论实参是何种类型的量, 在进行函数调用的时候, 他们都必须有确定的值, 以便把这些值传送给形参

**形式**参数(形参)

> 形式参数是指函数名后括号中的变量, 因为形式参数只有在函数被调用的过程中才实例化(分配内存单元),所以叫形式参数. 形式参数当函数调用完之后就自动销毁了, 因此形式参数只有在函数中才有效. 

注意: 形参和实参使用的**不是**同一块空间, 可以认为, 形参实例化之后其实相当于实参的一份临时拷贝.

###### 函数的调用

传值调用

> 函数的形参和实参分别占有不同内存块, 对形参的修改不会影响实参

传址调用

> - 传址调用是把函数外部创建的变量的内存地址传递给函数参数的一种调用函数的方式
> - 这种传参方式可以让函数和函数外边的变量建立起真正的联系, 也就是函数内部可以直接函数外部的变量

###### 函数的嵌套调用和链式访问

> 函数和函数之间可根据实际的需求进行组合的, 也就是互相调用的.
>
> 链式访问: 把一个函数的返回值作为另外一个函数的参数.
>
> 注意: 不可嵌套定义

###### 函数的声明和定义

>函数的声明:
>
>1. 告诉编译器有一个函数叫什么, 参数是什么, 返回类型是什么, 但是是否真实存在, 函数声明无法决定
>2. 函数的声明一般出现在函数的使用之前, 要满足先声明后使用
>3. 函数的声明一般要放在头文件中
>
>函数的定义:
>
>指函数的具体实现, 交代函数的功能实现.

###### 函数递归

定义

> 程序调用自身的编程技巧称为递归(recursion).
>
> 递归作为一种算法在程序设计语言中广泛应用, 一个过程或函数在其定义或说明中有直接或间接调用自身的一种方法, 它通常把一个大型复杂的问题层层转化为一个与原问题相似的规模较小的问题来求解, 递归策略只需少量的程序就可描述出解题过程所需要的多次重复计算, 大大减少了程序代码量. 

必要条件

- 存在限制条件, 当满足这个限制条件的时候, 递归便不再继续
- 每次递归之后越来越接近这个限制条件

注意:

使用递归的时候, 如果参数比较大, 那就会报错: stack overflow(栈溢出). 系统分配给程序的栈空间是有限的, 但是如果出现了死循环, 或者死递归, 就有可能导致一直开辟栈空间, 最终产生栈空间耗尽的情况, 这样的现象称为栈溢出.

如何解决:

1. 将递归改写成非递归.
2. 使用static对象替代nonstatic局部对象. 在递归函数设计中, 可以使用static对象替代nonstatic局部对象(栈对象), 这不仅可以减少每次递归调用和返回时产生和释放nonstatic对象的开销, 而且static对象还可以保存递归调用的中间状态, 并且可为各个调用层所访问.

提示:

1. 许多问题是以递归形式进行解释的, 只是因为它比非递归的形式更为清晰.
2. 但是这些问题的迭代实现往往比递归实现效率更高, 虽然代码的可读性稍微差些.
3. 当一个问题相当复杂, 难以用迭代实现时, 此时递归实现的简洁性便可以补偿它所带来的运行是开销.

[波兰表达式](https://vjudge.csgrandeur.cn/problem/OpenJ_Bailian-2694)

[母牛的故事](https://vjudge.csgrandeur.cn/contest/515042#problem/S)



###### 字符串函数

***strlen***

size_t strlen (const char* string);

Remarks: Each of these functions returns the number of characters in string, not including the terminating null character.


```
#include <stdio.h>
int main()
{
    char a1[] = "abc";
    char a2[] = { 'a', 'b', 'c' };
    printf("%d\n", strlen(a1));//3 字符串后面会自动添加一个'\0'
    printf("%d\n", strlen(a2));//randon
}
```

- 注意函数的返回值是size_t, 是无符号的


```
#include <stdio.h>
int main()
{
    //strlen的返回值size_t是无符号数unsigned int, 无符号数相减仍然得到无符号数
    if(strlen("abc") - strlen("abcdef") > 0)
    {
        printf(">\n");//be printed
    }
    else
    {
        printf("<\n");
    }
}
```

```
//模拟实现strlen
size_t my_strlen(const char* str)//size_t是unsigned int ,表示无符号整型，即count不可能为负数
{
	assert(*str != NULL);
	size_t count = 0;
	while (*str++)
	{
		count++;
	}
	return count;
}
int main()
{
	char arr[] = "Hello world";
	printf("%d\n", my_strlen(arr));
	return 0;
}
```

***strcpy***

char* ctrcpy( char* strDestination, const char *strSource );

Remarks: The strcpy function copies *strSource*, **including the terminating  null character**, to the location specified by *strDestination*. No overflow  checking is performed when strings are copied or appended. The behavior of  strcpy is undefined if the source and destination strings overlap.

```
#include <stdio.h>
#include <string.h>
int main()
{
    char arr[20] = { 0 };
    strcpy(arr, "Hello");
    printf("%s\n", arr);//Hello
    return 0;
}
```

```
#include <string.h>
int main()
{
    //源字符必须以'\0'结束，且会将'\0'拷贝到目标空间
    char a[20] = "#########";
    strcpy(a, "Hello");
    printf("%s\n", a);//Hello\0##
    
    char a[20] = { 0 };
    char b = {'a', 'b', 'c'};
    strcpy(a,b);//error(need '\0' to stop)
}
```

```
#incldue <string.h>
int main()
{
    //目标空间必须可变
    char* a = "xxxxxxxxxxxxxx";//常量字符串,不可修改
    char* b = "Hello"; 
    strcpy(a, b);//error  This strDestination can not be changed
    return 0;
}
```

```
#include <stdio.h>
#include <string.h>
int main()
{    
    //目标空间必须足够大,能够存放源字符串
    char arr[5] = { 0 };
    strcpy(arr, "Hello world");
    printf("%s\n", arr);//error
    return 0;
}
```

```
//模拟实现strcpy
#include <assert.h>
char* my_strcpy(char* dest,const char* sour)
{
	assert(*dest != NULL);//断言
	assert(*sour != NULL);
	char* ret = dest;
	while (*dest++ = *sour++)
	{
		;//hello的拷贝
	}
	return ret;//返回目标空间的起始地址
}
int main()
{
	char arr1[20] = "xxxxxxxxxx";
	char arr2[] = "hello";
	//1.目标空间的起始地址 2.源空间的起始地址
	printf("%s\n", my_strcpy(arr1, arr2));//链式访问
	return 0;
}


//strcpy源代码
char* _cdecl strcpy(char* dst, const char* src)
{
	char* cp = dst;
	while (*dst++ = *src++);
	return (dst);
}
```

***strcat***

char* strcat( char* strDestination, const char* strSource);

Remarks: The strcat function appends *strSource* to *strDestination*  and terminates the resulting string with a null character. The initial character  of *strSource* overwrites the terminating null character of  *strDestination*. No overflow checking is performed when strings are copied  or appended. The behavior of **strcat** is undefined if the source and  destination strings overlap.

- 源字符必须以'\0'结束
- 目标空间必须足够大, 能够容纳源字符串的内容
- 目标空间必须可修改

```
#include <string.h>
int main()
{
    char arr1[20] = "Hello ";
    char arr2[] = "world";
    strcat(arr1, arr2);
    pritnf("%s\n", arr1);//Hello world
    return 0;
}
```

```
#include <string.h>
#include <assert.h>
//模拟实现strcat
char* my_strcat(char* dest, char* src)
{
    assert(dest && src)
    char* ret = dest;
    while(*dest)
    {
        dest++;
    }
    while(*dest++ = *src++)
    {
        ;
    }
    return ret;
}
int main()
{
    char arr1[20] = "Hello ";
    char arr2[] = "world";
    my_strcat(arr1, arr2);
    pritnf("%s\n", arr1);//Hello world
    return 0;
}
```

***strcmp***

int strcmp( const char* string1, const char* string2 );

Remarks: The strcmp function compares *string1* and *string2*  lexicographically and returns a value indicating their relationship. 

```
int main()
{
    char* a = "abc";
    char* b = "defghi";
    //error  都是在比较a和d的地址而已
    if(a > b)
    or
    if("abc" > "defghi")
}
```

```
int main()
{
    int ret = strcmp("abbb", "abq");
    printf("%d\n", ret);//-1
    return 0;
}
```

***strncpy***

char* strncpy( char *strDest, const char *strSource, size_t count);

Remarks: The strncpy function copies the initial *count* characters of  *strSource* to *strDest* and returns *strDest*. If *count*  is less than or equal to the length of *strSource*, a null character is not  appended automatically to the copied string. If *count* is greater than the  length of *strSource*, the destination string is padded with null characters up to length *count*. The behavior of strncpy is  undefined if the source and destination strings overlap.

```
int main()
{
    char arr1[] = "abcd";
    char arr2[] = "efg";
    strncpy(arr1, arr2, 2);//efcd
    
    char a[] = "abcdefghi";
    char b[] = "qwer";
    //自动用'\0'补充至所需size_t
    ctrncpy(a, b, 6);//qwer\0\0ghi
}
```

***strncat***

char* strncat( char* strDest, const char* strSource, size_t count);

Remarks:The strncat function appends, at most, the first *count*  characters of *strSource* to *strDest*. The initial character of  *strSource* overwrites the terminating null character of *strDest*. If  a null character appears in *strSource* before *count* characters are  appended, strncat appends all characters from *strSource*, up to the  null character. If *count* is greater than the length of *strSource*,  the length of *strSource* is used in place of *count*. The resulting  string is terminated with a null character. If copying takes place between  strings that overlap, the behavior is undefined.

***strncmp***

int ctrncmp(const char* string1, const char* string2, size_t count);

Remarks: The strncmp function lexicographically compares, at most, the first  *count* characters in *string1* and *string2* and returns a value  indicating the relationship between the substrings. strncmp is a  case-sensitive version of **_**strnicmp.** Unlike strcoll,  strncmp is not affected by locale.

***strstr***

char *strstr( const char *string, const char *strCharSet);

Remarks: The strstr function returns a pointer to the first occurrence of *strCharSet* in *string*. The search does not include terminating null  characters. 

***strtok***

char *strtok( char *strToken, const char *strDelimit );

Remark: The strtok function finds the next token in *strToken*. The set of  characters in *strDelimit* specifies possible delimiters of the token to be  found in *strToken* on the current call. 

- strDelimit参数是字符串，定义了用作分隔符的字符集合
- 第一个参数指定了一个字符串，它包含了0个或多个由StrDelimit字符串中一个或多个分隔符分割的标记
- strtok函数找到strToken中的下一个标记，并将其用\0结尾，返回一个指向这个字符串的指针。(注意:strtok函数会改变被操作的字符串，所以在使用strtok函数切分的字符串一般都是临时拷贝的内容且可修改)
- strtok函数的第一个参数不为NULL，函数将找到str中第一个标记，strtok函数将保存它在字符串中的位置
- strtok函数的第一个参数为NULL，函数将在同一个字符串中被保存的位置开始，查找下一个标记(库函数可能使用了static来记忆)
- 如果字符串中不存在更多标记，则返回NULL指针

```
#include <stdio.h>
int main()
{
    char a[] = "ygtreceee@Guthub.com";
    char* p = "@.";
    char tmp[20] = { 0 };
    strcpy(tmp, p);
    for(ret = strtok(tmp, p); ret != NULL; ret = strtok(NULL, p))
    {
        printf("%s\n", ret;)
    }
    return 0;
}
```

***strerror***

char *strerror( int errnum );

Remarks: The strerror function maps *errnum* to an error-message string,  returning a pointer to the string. Neither strerror nor _strerror  actually prints the message: For that, you need to call an output function such  as *fprintf*;

> 返回错误码所对应的错误信息(使用库函数的时候, 若调用库函数失败，都会设置错误码)
>
> errno: 全局错误码

```
#include <string.h>
#include <errno.h>
int main()
{
    //打开文件失败时,会返回NULL
    FILE* pf = fopen("test.txt", "r");
    if(pf == NULL)
    {
        printf("%s\n", strerror(errno));//No such file or directory
        return 1;
    }
    //...
    fclose(pf);
    pf = NULL;
    return 0;
}
```

###### 字符分类函数

| 函数     | 如果它的函数符合下列条件就返回真                             |
| -------- | ------------------------------------------------------------ |
| iscntrl  | 任何控制字符                                                 |
| isspace  | 空白字符: 空格' ',换页'\f', 换行'\n', 回车'\r', 制表符'\t', 垂直制表符'\v' |
| isdigit  | 十进制数字0~9                                                |
| isxdigit | 十六进制, 包括所有十进制数字, 小写字母a~f, 大写字母A~F       |
| islower  | 小写字母a~z                                                  |
| isupper  | 大写字母A~Z                                                  |
| isalpha  | 字母a~z 或 A~Z                                               |
| isalnum  | 字母或数字, a ~ z, A ~ Z, 0~9                                |
| ispunct  | 标点符号, 任何不属于数字或字母的图形字符(可打印)             |
| isgraph  | 任何图形字符                                                 |
| isprint  | 任何可打印字符, 包括图形字符和空白字符                       |

###### 字符转换函数

```
int tolower (int c);//大写转小写
int toupper (int c);//小写转大写
```

###### 内存函数

***memcpy***

Copies characters between buffers.

void * memcpy( void *dest, const void *src, size_t count  );

Remarks: The memcpy function copies *count* ==bytes== of *src* to  *dest.* If the source and destination overlap, this function does not  ensure that the original source bytes in the overlapping region are copied  before being overwritten. Use memmove to handle overlapping regions.

注意: c语言标准只要求memcpy只需实现不重叠拷贝就行, 但VS中的memcpy既可以实现不重叠拷贝, 也可以实现重叠拷贝, 其他编译器则不一定

***memmove***

Moves one buffer to another.

void *memmove( void *dest, const void *src, size_t count);

```
int main()
{
    //memcpy一般只能拷贝不重叠的内存
    //memmove可以处理内存重叠的情况
    int a[20] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 0};
    memcpy(a+2, a, 20);//1 2 1 2 1 2 1 7 8 9 0
    memmove(a+2, a, 20);//1 2 1 2 3 4 5 7 8 9 0
}
```

***memcmp***

Compare characters in two buffers.

int memcmp( const void* buf1, const void* buf2, size_t count );

Remarks: The memcmp function compares the first *count* bytes of  *buf1* and *buf2* and returns a value indicating their  relationship.

***memset***

Sets buffers to a specified character.

void *memset( void *dest, int c, size_t count );

Remarks: The memset function sets the first *count* ==bytes== of *dest*  to the character *c.*

###### Others

***getchar and gets***

```
int n;
char a[1000] = { 0 };
scanf_s("%d", &n);
getchar();//用于清除前面scanf留下的回车键
          //特别注意：getchar返回的是吸收的字符，这个特性可以用于判别
gets(a);//读取字符串
```

gets()函数用来从标准输入设备（键盘）读取字符串直到换行符结束，但换行符会被丢弃，然后在末尾添加’\0’字符。其调用格式为：gets(s); 其中s为字符串变量（字符串数组名或字符串指针）。

gets(s)函数与scanf("%s", s)相似，但不完全相同，使用scanf("%s", s) 函数输入字符串时存在一个问题，就是如果输入了空格会认为字符串结束，空格后的字符将作为下一个输入项处理，但gets()函数将接收输入的整个字符串直到遇到换行为止。

总结：gets()函数读取到\n（我们输入的回车）于是停止读取，但是它不会把\n包含到字符串里面去。然而，和它配合使用的puts函数，却在输出字符串的时候自动换行。

gets(s) 函数中的变量s为一字符串指针。如果为单个字符指针，编译连接不会有错误，但运行后内存溢出错误。

while (gets(arr) != NULL)//gets的返回值是一个空指针，所以此处用NULL而不用EOF

***extren***

声明外部符号用extern

***sizeof***

```
[int main()
{
    short s = 5;
    int a = 4;
    printf("%d\n", sizeof(s = a + 6));//2  s是short类型，表达式的结果由s说了算，所以没有类型转换，即便后面有int，也只能存进short
    printf("%d\n", s);//5  sizeof内部的表达式不会计算！
}]()
```

***perror***

Print an error message.

void perror( const char *string );

```
#include <stdio.h>
int main()
{
    FILE* pf = fopen("text.exe", "r");
    if(pf == NULL )
    {
        perror("fopen");//fopen: No such a file or directory
        return 1;
    }
   return 0;
}
```

***sleep***

休眠

```
#include <windows.h>
int main()
{
	sleep(1000);//单位:ms
	return 0;
}
```

***bool***

**C++ Specific** 

**bool** *declarators*

This keyword is an integral type. A variable of this type can have values true and false.  All conditional expressions now return a value of type **bool**. For example,  `i!=0` now returns **true** or **false** depending on the value  of `i`.(MSDN)

```
//example
//
bool flag = false;
if(...)	flag = true;
printf(flag ? "Yes\n" : "No\n");

//
bool judge(...)
{
	//主体
	//return后接判断, 若判断为真, 则会返回true, 否则返回false
	return ...;
}

```













## 5.数据在内存中的存储

###### 类型的基本归类

- 整型家族：char   unsigned char   signed char   （由于字符类型底层存储的时候存储的是这个字符的ASCII码值，ASCII值也是个整数，所以归类的时候把char类型归类到整型）

  ​          short   unsigned short[int]   signed short[int]     (最大为65535)
  ​          int       unsigned int             signed int                (最大为4294967295)
  ​          long    unsigned long[int]   signed long[int]

  ​          char    unsigned char           signed char              (有符号的char的取值范围是-128~127)

- 浮点数家族：float   double

- 构造类型——自定义类型
            struct结构体类型
            数组(如arr[10])
            enum 枚举
            union 联合体

- 指针类型
            int* pi
            char* pc
            float* pf
            void* pv

- 空类型:void表示空类型（无类型），通常用于函数的返回类型void test()、函数的参数void test(void)、指针类型void* pv

###### 整型在内存中的存储

数据在内存中以二进制的形式进行存储，对于整数来说，整数二进制有3种表示形式：原码、反码、补码
按照数据的数值直接写出的二进制序列就是原码，原码的符号位不变，其他位按位取反，得到的就是反码，反码+1得到的就是补码
正整数：原码、反码、补码相同
负整数：原码、反码、补码要进行计算
整数在内存中存储的是补码，原因是使用补码可以将符号位和数值域统一处理，同时加法和减法也可以统一处理（CPU只有加法处理器），此外，反码和补码相互转换，其运算过程是相同的（补码再次按位取反加一又可以得到原码），不需要额外的硬件电路

```
int main()
{
	char a = -1;
		//首先，-1的二进制为10000000000000000000000000000001，在内存中的补码为           11111111111111111111111111111111，由于char的大小是一个字符，所以会发生截断，只能11111111，然后打印的又是%d，即一个整型，所以又要发生整型提升，由于char是有符号的，所以提升为11111111111111111111111111111111，再打印出原码就是10000000000000000000000000000001，即-1
	signed char b = -1;//signed表示有符号，所以同上
	unsigned char c = -1;//无符号整型，高位补零，从11111111变成00000000000000000000000011111111，即c=255
	printf("a=%d b=%d c=%d", a, b, c);//a=-1 b=-1 c=255
	return 0;
}
```

```
int main()
{
	char a = 128;
	//0000000000000000000000001000000
	//10000000
	//整型提升的时候，是按照原来a的类型，即char来进行提升的，而char是有符号的，所以认为高位是符号位，整型提升为
	//1111111111111111111111111000000 （此时为补码）
	printf("%u\n", a);//a=4294967168
	return 0;
}
```

```
int main()
{
	char a = -128;
	//10000000000000000000000010000000 原码
	//11111111111111111111111101111111 反码
	//11111111111111111111111110000000 补码
	//10000000 储存一个字节
	//11111111111111111111111110000000 char是有符号整型，高位是符号位，整型提升时前面全部补1，而打印是打印unsigned int，所以高位1应该看作运算位，不是符号位(打印的是一个整型，就要进行整型提升，但是无论打印的是有符号还是无符号，整型提升的时候都是按照符号位进行提升的）同时注意，printf打印的是%u，无符号整型认为原码反码补码全相同，但如果是%d，则还需转化为原码
	printf("%u\n", a);//a=4294967168
	return 0;
}

```

```
int main()
{
	char a = 128;
	//0000000000000000000000001000000
	//10000000
	//整型提升的时候，是按照原来a的类型，即char来进行提升的，而char是有符号的，所以认为高位是符号位，整型提升为
	//1111111111111111111111111000000 （此时为补码）
	printf("%u\n", a);//a=4294967168
	return 0;
}
```

```
int main()
{
	int i = -20;
	//10000000000000000000000000010100
	//11111111111111111111111111101011
	//11111111111111111111111111101100
	unsigned int j = 10;
	//00000000000000000000000000001010
	printf("%d\n", i + j);
	//11111111111111111111111111101100
	//00000000000000000000000000001010
	//11111111111111111111111111110110 -相加得到的补码
	//11111111111111111111111111110101
	//10000000000000000000000000001010  -> -10
	return 0;
}

```

```
int main()
{
	int a = -20;
	//10000000000000000000000000010100
	//11111111111111111111111111101011
	//11111111111111111111111111101100
	unsigned int b = 10;
	//00000000000000000000000000001010
	//11111111111111111111111111110110 （此处a+b会使结果默认被强制类型转换为unsigned int，如果打印，则直接打印补码，因为
	//                                   补码等于原码，且高位非符号位）
	//11111111111111111111111111110101
	//10000000000000000000000000001010 （若打印为%d，说明还要进行强制类型转化为int，即要将补码转换为原码，且高位为符号位）
	if (a + b > 0)
	{
		pritnf("a+b>0\n");//此行会被打印，可再次印证上面推论
	}
	printf("%u", a + b);//4294967286
	printf("%d", a + b);//-10（至于此处为什么会变成-10，因为虽然a+b在内存中是无符号整型，但是想要打印出来，还得以%后的类型为准，此处
	//                        为%d，所以无符号再次被强制类型转化为有符号，所以输出是-10）
	return 0;
}
```

```
int main()
{
	char a[1000];
	int i;
	for (i = 0; i < 1000; i++)
	{
		a[i] = -1 - i;//此处涉及到char类型的二进制存储规律，从00000000到11111111并不是一个从小到大的过程，而是先从00000000到01111111，逐渐变大，即从0~127，然后01111111加1得到的10000000其实已经变成-128，然后从10000000到11111111是从-128到-1，因为高位为符号位，所以是一个循环，此题中strlen遇0即停，从-1，-2，-3，-4，......,-127,-128,127,126,125,......,2,1,0,
一共255个
	}
	printf("%d\n", strlen(a));//找到'\0' -> 0,打印为255
	return 0;
}
//可知：signed char 的取值范围是-128~127  unsigned char 的取值范围是0~255
//补充：char到底是signed char还是unsigned char，c语言标准并没有规定，取决于编译器，且大部分编译器都是signed char；但是int有规定是signed int、short是signed short
```

```
#include <stdio.h>
int i;//i是全局变量，不初始化，默认是0
int main()
{
	i--;//i=-1
	//sizeof这个操作符，算出的结果的类型是unsigned int，所以前后比较的时候，会使得前面的i先转换为一个无符号数，是一个很大的数
	//类似于int类型与double类型相加得到double类型数
	if (i > sizeof(i))
	{
		printf(">\n");//be printed
	}
	else
	{
		printf("<\n");
	}
	return 0;
}
```

###### 大小端

指数据在电脑上存储的字节顺序

大端（存储）模式：是指数据的低位保存在内存的高地址中，而数据的高位，保存在内存的低地址中；
小端（存储）模式：是指数据的低位保存在内存的低地址中，而数据的高位，保存在内存的高地址中；

```
//判断机器的字节序
int main()
{
	int a = 1;
	char* pc = (char*)&a;//对指针进行强制类型转换
	if (*pc == 1)
	{
		printf("小端\n");
	}
	else
	{
		printf("大端\n");
	}
	return 0;
}
//or
int check_sys()
{
	int a = 1;
	char* pc = (char*)&a;
	return *pc;
}
int main()
{
	int ret = check_sys();
	if (ret = 1)
	{
		printf("小端\n");
	}
	else
	{
		printf("大端\n");
	}
	return 0;
}
```

###### 浮点型在内存中的存储

浮点数类型：float    double    long double 
整型家族的取值范围定义在limits.h，浮点型取值范围定义在float.h

```
#include <limits.h>
int main()
{
	INT_MAX;//转到定义可以看每种类型的极值
	return 0;
}
```

根据国际标准IEEE(电气与电子工程协会)754，任意一个二进制浮点数V可以表示成下面的形式：(-1)^S^M2^E^
(-1)^S表示符号位，当S=0时，V为正数，当S=-1，V为负数
M表示有效数字，大于等于1，小于2
2^E表示指数位
e.g.浮点数：10.5 --10进制
101.1 --二进制（2^(-1)=0.5)
(-1)^0*1.01*2^2
S=0  M=1.01  E=2
        IEEE 754规定：对于32位的浮点数，最高的一位是符号位s，接着的8位是指数E，剩下的23位为有效数字M；对于64位的浮点数，最高的一位是符号位s，接着的11位是指数E，剩下的52位为有效数字M
      IEEE 754对有效数字M和指数E，还有一些特别规定：前面说过，1<=M<2,也就是说，M可以写成1.xxxxxx的形式，其中xxxxxx表示小数部分。 754规定，在计算机内部保存M时，默认这个数的第一位总是1，因此可以被舍去，只保存后面的xxxxxx部分，比如保存1.01时， 只保存01，等到读取的时候，再把第一位的1加上去，这样可以节省1位有效数字，以32位浮点数为例，留给M只有23位，将第一位的1舍去以后，等于可以保存24位有效数字。 至于指数E，比较复杂：首先E为一个无符号整型（unsigned int),这意味着，如果E为8位，它的取值范围为0-255；如果E为11位，它的取值范围为0-2047.但是，我们知道，科学计数法中的E是可以出现负数的，所以IEEE 754规定，存入内存时E的真实值必须再加上一个中间数，对于8为的E，这个中间数是127，对于11位的E，这个中间数是1023。比如2^10的E是10，所以保存成32位浮点数时，必须保存成10+127=137，即10001001
// e.g.

```
int main()
{
	float f = 5.5f;
	//101.1
	//1.011*2^2
	//s=0  M=1.011  E=2
	//s=0  M=011    E=2+127
	//0 10000001 01100000000000000000000
	//0100 0000 1011 0000 0000 0000 0000 0000
	//40 b0 00 00
	//查找地址可得00 00 b0 40(小端存储）
	return 0;
 }
```

然后，指数E从内存中取出分成三种情况：
E不为全0或全1：这时，浮点数就采用下面的规则表示，即指数E的计算值减去127（或1023），得到真实值，再将有效数字M前加上第一位的1
E全为0：这时浮点数的指数E等于1-127（或者1-1023）即为真实值（内存已规定，不必再计算），有效数字M不在加上第一位的1，而是还原为 0.xxxxxx的小数，这是内存的特殊规定，是为了表示+-0，以及接近于0的很小的数字
E全为1：这时表示+-无穷大（正负取决于符号位s）

```
int main()
{
	int n = 9;
	float* pFloat = (float*)&n;//强制类型转换
	printf("n的值为：%d\n", n);//9
	printf("*pFloat的值为：%f\n", *pFloat);//此时n在内存中存放为00000000000000000000000000001001，以浮点类型打印，则会被以浮点数类型的读取方式进行读取，即0 00000000 00000000000000000001001，得到的是一个极小的数，所以打印出来是0.000000(特别注意：如果要对一个数以另一种类型打印出来，是需要利用一次指针强制类型转换的，不能直接打印，且不可以在printf里面直接转换）
	*pFloat = 9.0;//n变为浮点数类型，二进制为1001.0，即（-1）^0*1.001*2^3,储存为0 10000010 00100000000000000000
	printf("num的值为：%d\n", n);//以整型类型的方式进行读取，得到一个极大的数，为1091567616
	printf("*pFloat的值为：%f\n", *pFloat);//以浮点数类型的方式进行读取，为9.000000
	return 0;
}
```

```
int main()
{
	float f = 9.0;
	printf("%d", f);//ERROR!!!
	printf("%d", (unsigned int)f);//打印出来是9
	//特别注意：如果要对一个数以另一种类型打印出来，是需要利用一次指针强制类型转换的，不能直接打印，且不可以在printf里面直接转换
}
```

## 6.指针

###### 指针的定义

> 指针的理解：
>
> 1. 指针是内存中一个最小单元的编号，也就是地址
>
> 2. 平时口语中说的指针，通常指的是指针变量，是用来存放内存地址的变量
>
> 总结：指针就是地址，口语中说的指针通常指的是指针变量

内存

<img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20221018161649345.png" alt="image-20221018161649345" style="zoom:50%;" />

指针变量

> 我们可以通过&(取地址操作符)取出变量的内存其实地址, 把地址可以存放到一个变量中, 这个变量就是指针变量

```
#include <stdio.h>
int main()
{
	int a = 10;//在内存中开辟一块空间
	int *p = &a;//这里我们对变量a，取出它的地址，可以使用&操作符。
    //a变量占用4个字节的空间，这里是将a的4个字节的第一个字节的地址存放在p变量中，p就是一个之指针变量
	return 0;
}
```

###### 指针的大小

经过仔细的计算和权衡我们发现一个字节给一个对应的地址是比较合适的. 对于32位的机器, 假设有32根地址线, 那么假设每根地址线在寻址的时候产生高电平(高电压)和低电平(低电压)就是(1或者0); 那么32根地址线产生的地址就会是:00000000 00000000 00000000 00000000等32位数,这里就有2的32次方个地址. 每个地址标识一个字节, 那我们就可以给 (2^32^Byte == 2^32^/1024KB == 2^32^/1024/1024MB==2^32^/1024/1024/1024GB == 4GB)4G的空闲进行编址. 同样的方法, 那64位机器, 如果给64根地址线, 那能编址多大空间, 也可计算.

>在32位的机器上，地址是32个0或者1组成二进制序列，那地址就得用4个字节的空间来存储，所以一个指针变量的大小就应该是4个字节
>
>如果在64位机器上，如果有64个地址线，那一个指针变量的大小是8个字节，才能存放一个地址

总结:

- 指针是用来存放地址的，地址是唯一标示一块地址空间的

- 指针的大小在32位平台是4个字节，在64位平台是8个字节

###### 指针类型与用法

```
char  *pc = NULL;
int   *pi = NULL;
short *ps = NULL;
long  *pl = NULL;
float *pf = NULL;
double *pd = NULL;
//指针的定义方式为
//type + * 
//不同类型的指针是为了存放不同类型变量的地址, 也决定了指针解引用的权限大小
```

**指针的解引用**

指针的类型决定了, 对指针解引用的时候有多大的权限(能操作几个字节)

```
#include <stdio.h>
int main()
{
	int n = 0x11223344;
	char *pc = (char *)&n;
	int *pi = &n;
	*pc = 0;   //重点在调试的过程中观察内存的变化。
	*pi = 0;   //重点在调试的过程中观察内存的变化。
	return 0;
}
```

###### **野指针**

> 野指针是指指针指向的位置是不可知的（随机的、不正确的、没有明确限制的）

**野指针成因**

```
//1.指针未初始化
#include <stdio.h>
int main()
{ 
	int *p;//局部变量指针未初始化，默认为随机值
    *p = 20;
	return 0;
}

//2.指针越界访问
#include <stdio.h>
int main()
{
   int arr[10] = {0};
   int *p = arr;
   int i = 0;
   for(i=0; i<=11; i++)
   {
       //当指针指向的范围超出数组arr的范围时，p就是野指针
       *(p++) = i;
   }
   return 0;
}

//3. 指针指向的空间释放
可参见动态内存管理
```

**如何规避野指针**

1. 指针初始化
2. 小心指针越界
3. 指针指向空间释放即使置NULL
4. 避免返回局部变量的地址
5. 指针使用之前检查有效性

```
#include <stdio.h>
int main()
{
	//初始化为空指针
    int *p = NULL;
    //....
    int a = 10;
    p = &a;
    if(p != NULL)
   {
        *p = 20;
   }
    return 0;
}
```

###### 指针运算

**指针+-整数**

指针的类型决定了指针向前或者向后走一步有多大(地址前后移动的字节)

```
#include <stdio.h>
int main()
{
	int n = 10;
	char *pc = (char*)&n;
	int *pi = &n;
 
	printf("%p\n", &n);
	printf("%p\n", pc);
	printf("%p\n", pc+1);
	printf("%p\n", pi);
	printf("%p\n", pi+1);
	return  0;
}
```

**指针-指针**

等于中间元素个数(前提是两个指针指向同一个空间)

```
int my_strlen(char *s)
{
     char *p = s;
     while(*p != '\0' )	p++;
     return p-s;
}
```

###### 指针的关系运算

```
for(vp = &values[N_VALUES]; vp > &values[0];)
{
    *--vp = 0;
}
//代码简化, 这将代码修改如下
for(vp = &values[N_VALUES-1]; vp >= &values[0];vp--)
{
    *vp = 0;
}
//实际在绝大部分的编译器上是可以顺利完成任务的，然而我们还是应该避免这样写，因为标准并不保证
它可行
//标准规定：允许指向数组元素的指针与指向数组最后一个元素后面的那个内存位置的指针比较，但是不允许与指向第一个元素之前的那个内存位置的指针进行比较
```

###### 指针和数组

数组名是数组首元素地址，但是有两种情况例外

- sizeof(数组名）-- 数组名表示的是整个数组，计算的是整个数组的大小，单位是字节
- &数组名 -- 数组名表示整个数组，取的是整个数组的地址

```
#include <stdio.h>
int main()
{
 int arr[10] = {1,2,3,4,5,6,7,8,9,0};
 	//结果一致
    printf("%p\n", arr);
    printf("%p\n", &arr[0]);
    return 0;
}
```

把数组名当成地址存放到一个指针中，我们就能够使用指针来访问数组.


```
#include <stdio.h>
int main()
{
    int arr[] = {1,2,3,4,5,6,7,8,9,0};
    int *p = arr; //指针存放数组首元素的地址
    int sz = sizeof(arr)/sizeof(arr[0]);
    for(i=0; i<sz; i++)
   {
        printf("&arr[%d] = %p   <====> p+%d = %p\n", i, &arr[i], i, p+i);
   }
    return 0;
}

//p+i 其实计算的是数组 arr 下标为i的地址
//那我们就可以直接通过指针来访问数组

int main()
{
	int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 0 };
	int *p = arr; //指针存放数组首元素的地址
	int sz = sizeof(arr) / sizeof(arr[0]);
	int i = 0;
	for (i = 0; i<sz; i++)	printf("%d ", *(p + i));
	return 0;
}
```



###### 二级指针

指针变量也是变量, 是变量就有地址, 那指针变量的地址存放的地方就是 二级指针 

<img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20221018164315412.png" alt="image-20221018164315412" style="zoom:67%;" />

```
*ppa 通过对ppa中的地址进行解引用，这样找到的是 pa ， *ppa 其实访问的就是 pa .
**ppa 先通过 *ppa 找到 pa ,然后对 pa 进行解引用操作： *pa ，那找到的是 a .

int b = 20;
*ppa = &b;//等价于 pa = &b;
**ppa = 30;
//等价于*pa = 30;
//等价于a = 30;
```

```
int main()
{
	int a = 10;
	int *pa = &a;//pa是指针变量，pa是一级指针
	int **ppa = &pa;//pa也是一个变量，ppa是一个二级指针变量，&pa取出pa在内存中的地址

    //二级指针有两层指向关系
	//*ppa == pa     *pa == a     所以**ppa == a
	//以此类推还有三级指针（***pppa）等等，但是很少用到
	return 0;
}
```

> 指针概念：

- 指针就是个变量，用来存放地址，地址唯一标识一块内存空间
- 指针的大小是固定的4（32位平台）或8个（64位平台）字节
- 指针是有类型的，指针的类型决定指针的+-整数的步长，指针解引用操作时候的权限
- 指针的运算

```
//字符指针
int main()
{
	char ch = 'q';
	char* pc = &ch;
	return 0;
}
```

```
int main()
{
	char* pc = "Hello world";
	//本质上是把"Hello world"这个字符串的首字符的地址存储在了pc
	printf("%c\n", *pc);//H
	printf("%s\n", *pc);//"Hello world"
	//相似用法
	char arr[] = "Hello world";
	printf("%s\n", arr);//"Hello world"
	return 0;
}
```

```
int main()
{
	char* str = "hello world";
	*str = 'w';//ERROR!!!
	//"hello world"是一个常量字符串，是不允许修改的，一些语法严格的编译器甚至需要在char之前加上const 
	return 0;
}
```

```
int main()
{
	//字符串指针两种血法
	//1
	char str1 = "hello world";
	char* pc1 = str1;
	//2
	char* pc2 = "hello world";
	//两种写法的区别在于在内存中存储的区域不同，字符数组存储在全局数据区或栈区，第二种形式字符串存储在常量区。全局变量区和栈区
	//的字符串有读取和写入和权限，而常量区字符串只有读取权限，没有写入权限，这就导致了字符数组在定义后可读取和修改每个字符而第
	//二种形式（字符串常量）一旦定义后便不可修改，对它的赋值都是错误的（可整体赋值）
	return 0;
}
```

```
int main()
{
	char str1[] = "hello world";
	char str2[] = "hello world";
	char* str3 = "hello world";
	char* str4 = "hello world";
	//这里的str3和str4指向的是同一个常量字符串，C/C++会把常量字符串存储到单独的一个内存区域，当几个指针指向同一个字符串的时候，他们实际会指向同一块内存，但是用相同的常量字符串去初始化不同的数组的时候就会开辟出不同的内存块，即str1和str2是两个不同的数组，开辟的是两个不同的空间，所以str1和str2不同，str3和str4相同
	if (str1 == str2)
		printf("str1 and str2 are same.\n");
	else
		printf("str1 and str2 are not same.\n");//be printed
	if (str3 == str4)
		printf("str3 and str4 are same.\n");//be printed
	else
		printf("str3 and str4 are not same.\n");
	return 0;
}
```

###### 指针数组

>  本质是数组---数组中存放的是指针（地址）

```
int main()
{
	int a[5] = { 1,2,3,4,5 };
	int b[] = { 2,3,4,5,6 };
	int c[] = { 3,4,5,6,7 };
	int* arr[3] = { a,b,c };
	int i = 0;
	for (i = 0; i < 3; i++)
	{
		int j = 0;
		for (j = 0; j < 5; j++)
		{
			//print the strings
			printf("%d ", *(arr[i] + j));
			//or
			printf("%d ", arr[i][j]);
		}
	}
	return 0;
}
```

```
int main()
{
	int* arr1[10];//整形指针的数组
	char* arr2[4];//一级字符指针的数组
	char** arr3[5];//二级字符指针的数组
	return 0;
}
```

###### 数组指针

>  能够指向数组的指针

```
int main()
{
	double* d[5];//指针数组
	double* (*pd)[5] = &d;//pd就是数组指针
	int arr[10];
	int (*parr)[10] = &arr;//parr是一个数组指针，其中存放的是数组的地址，parr先与*结合，说明parr是一个指针变量，然后指向一个大小为10个整型的数组。这里注意，[]的优先级是高于*的，所以要加（）来保证parr先与*结合
	return 0;

}
```

```
int main()
{
	int arr[10] = { 0 };
	int* p1 = arr;//arr需要一个整型指针
	int (*p2)[10] = &arr;//&arr需要一个数组指针
	//arr与&arr结果相同，但是类型不同
	printf("%p\n", arr);
	printf("%p\n", &arr);
	printf("%p\n", p1);
	printf("%p\n", p2);//结果都是一致的
	
	printf("%p\n", p1);
	printf("%p\n", p1 + 1);//p1 和 p1+1 结果相差4个字节
	printf("%p\n", p2);
	printf("%p\n", p2 + 1);//p2 和 p2+1 结果相差40个字节
	//再次说明arr与&arr意义的不同，&arr表示的是数组的地址，而不是数组首元素的地址，整型地址+1向后移动一个整型，数组地址+1向后移动一个数组
	return 0;
}
```

###### 数组指针的使用

```
int main()
{
	int arr[10] = { 1,2,3,4,5,6,7,8,9,10 };
	int(*p)[10] = &arr;
	//把数组arr的地址赋值给数组指针变量p
	//但是我们一般很少这样写
	return 0;
}
```

```
//使用范例
#include <stdio.h>
void print_arr1(int arr[3][5],int row, int col)
{
	int i = 0;
	for (i = 0; i < row; i++)
	{
		for (j = 0; j < col; j++)
		{
			printf("%d", arr[i][j]);
		}
		printf("\n");
	}
}
void print_arr2(int(*arr)[5], int row, int col)
{
	int i = 0;
	int j = 0;
	for (i = 0; i < row; i++)
	{
		for (j = 0; j < col; j++)
		{
			printf("%d ", *(*(arr + i) + j));//????
		}
	}
}
int mian()
{
	int arr[3][5] = { {1,2,3,4,5},{6,7,8,9,10},{11,12,13,14,15} };
	print_arr1(arr, 3, 5);
	//数组名arr表示首元素的地址
	//但是二维数组的首元素是二维数组的第一行
	//所以这里传递的arr，其实相当于第一行的地址，是一维数组的地址
	//可以用数组指针来接收
	print_arr2(arr, 3, 5);
	return 0;
}
```

- int arr[5];整型数组
- int *parr1[10];指针数组
- int (*parr2)[10];数组指针
- int (*parr3[10])[5];parr3是一个存放数组指针的数组，该数组能够存放十个数组指针，每个数组指针能够指向一个数组，数组有5个元素

###### 数组传参与指针结合

```
//一维数组传参
#include <stdio.h>
void test (int arr[])//允许，因为传过来的也只是个地址，所以[]中的数字可加可不加
{}
void test(int arr[10])//写了[]中的数字，但是没有实质意义
{}
void test(int* arr)//整型指针，允许
{}
void test2(int* arr[20])//指针数组，允许
{}
void test2(int** arr)//传过来的是int*的地址，就是指针的地址，也就是二级指针，允许
{}
int main()
{
	int arr[10] = { 0 };
	int *arr2[20] = { 0 };
	test(arr);
	test2(arr2);
}
```

```
//二维数组传参
void test(int arr[3][5])//ok
{}
void test(int arr[][])//error,行可以省略，列绝对不能省略
{}
void test(int arr[][5])//ok
{}
void test(int* arr)//error,传过来的是第一行数组的地址，不可以用一个int接收
{}
void test(int* arr[5])//error,指针数组无法接收地址
{} 
void test(int (*arr)[5])//ok,指向一维数组的指针
{}
void test(int** arr)//error，传过去的是一维数组的地址，不能用int二级指针接收
{}
int main()
{
	int arr[3][5] = { 0 };
	test(arr);
}
```

```
#include <stdio.h>
void test(int** arr)//参数是二级指针
{
    
}
int main()
{
    int a=10;
    int* pa = &a;//pa是一级指针
    int** ppa = &pa;//ppa是二级指针
    test(&pa);
    test(ppa);
    int* arr[10] = { 0 };
    test(arr);//传存放一级指针的数组
    return 0;
}
```

###### 函数指针

>  存放函数地址的指针

有数组指针，数组每个元素是参数为int且返回值为int的函数指针: int ( * (*p)[10] )(int)

```
#include <stdio.h>
int Add(int x , int y)
{
    return x + y;
}
int main()
{
    //上下是等价的
    //&函数名，取到的就是函数的地址
    //而直接写函数名，结果和意义上也是一样的（与数组不同），因为函数名就是函数地址
    printf("%p\n", &Add);
    printf("%p\n", Add);
    //pf是一个函数指针变量,(int, int)交代清楚函数参数类型是什么，int交代返回类型
    int (*pf)(int, int) = &Add;
    return 0;
}
```

```
#include <stdio.h>
int Add(int x , int y)
{
    return x + y;
}
int main()
{
    int (*pf)(int, int) = &Add;
    //函数指针用法
    //三种写法结果都是一样的
    int ret = (*pf)(5, 3);//1
    int ret = pf(5, 3);//2
    int ret = Add(5, 3);//3
    //注意,第一种写法中的*其实是个摆设,加几颗都没问题,只是方便理解(只有函数指针可以省略*)
    //但是注意不能写成*pf(3, 5)，因为括号的优先级最大，会导致先进行pf(3, 5),再对8解引用
    printf("%d\n", ret);
    return 0;
}
```

```
//分析代码

(*(void (*p)())0)();
1.void (*p)() - 函数指针类型
2.(void (*p)())0 - 对0进行强制类型转换，被解释为一个函数地址
3.*(void (*p)())0 - 对0的地址进行了解引用操作
4.(*(void (*p)())0)() - 对0地址处的函数进行了调用
该函数无参，返回类型是void


void (* signal(int, void(*)(int)))(int);
1.signal先与()结合，说明signal是函数名
2.signal函数的第一个参数类型为int，第二个参数类型为函数指针，该函数指针指向一个参数为int，返回类型为void的函数
3.signal函数的返回类型也是一个函数指针
该函数指针，指向一个类型为int，返回类型为void的函数
4.signal是一个函数的声明

对其也可以进行简化写法
//typedef - 对类型进行重定义
typedef void(*pfun_t)(int)
//对void (*)(int)的函数指针类型重命名为pfun_t
pfun_t signal(int, pfun_t)
```

###### 函数指针数组

> 存放函数指针的数组

```
int Add(int x, int y)
{
    return x + y;
}
int Sub(int x, int y)
{
    return x - y;
}
int main()
{
    int(*pf1)(int, int) = Add;
    int(*pf2)(int, int) = Sub;
    int(*pfArr[2])(int, int) = {Add, Sub};//pfArr就是函数指针数组
}
```

函数指针数组的使用范例

```
#include <stdio.h>
int Add(int x, int y)
{
    return x + y;
}
int Sub(int x, int y)
{
    return x - y;
}
int Mul(int x, int y)
{
    return x * y;
}
int Div(int x, int y)
{
    return x / y;
}
int main()
{
    int x, y, ret, input;
    int (*pfarr[5])(int, int) = { NULL, Add, Sub, Mul, Div };
    printf("Please choose\n");
    scanf("%d",&input);
    printf("Please input\n");
    scanf("%d %d", &x, &y);
    ret = (pfarr[input])(x, y);
    printf("%d\n",ret);
    return 0;
}
```

&+函数指针数组:指向函数指针数组的指针(了解)

```
int(*p)(int, int);//函数指针
int(*p2[4])(int, int);//函数指针的数组
int(*(*p3)[4])(int, int) = &p2;//取出的是函数指针数组的地址
//p3就是一个指向函数指针数组的指针
```

###### 回调函数

> 回调函数就是一个通过函数指针调用的函数. 如果你把函数的指针(地址)作为参数传递给另一个函数, 当这个指针被用来调用其所指向的函数时, 我们就说这是回调函数. 回调函数不是由该函数的实现方直接调用, 而是在特定的事件或条件发生时由另外的一方调用的, 用于对该事件或条件进行响应. 

使用范例

```
#include <stdio.h>
int Add(int x, int y)
{
    return x + y;
}
int Sub(int x, int y)
{
    return x - y;
}
int Mul(int x, int y)
{
    return x * y;
}
int Div(int x, int y)
{
    return x / y;
}
int Calc(int (*pf)(int, int))
{
    int x, y;
    printf("Please Input\n");
    scanf("%d %d", &x, &y);
    return pf(x, y);
}
int main()
{
    int input, ret;
    do
    {
        printf("Please Choose\n");
        scanf("%d", &input);
        switch (input)
        {
        case 0:
            break;
        case 1:
            ret = Calc(Add);
            printf("%d\n", ret);
            break;
        case 2:
            ret = Calc(Sub);
            printf("%d\n", ret);
            break;
        case 3:
            ret = Calc(Mul);
            printf("%d\n", ret);
            break;
        case 4:
            ret = Calc(Div);
            printf("%d\n", ret);
            break;
        default:
            printf("Please Choose Again\n");
        }
    }while(input);
    return 0;
}
```

###### **qsort** 函数

Performs a quick sort.

void qsort( void *base, size_t num, size_t width, int  (__cdecl *compare )(const voide *lem1, const void *elem2 ));

**Required Header**v

<stdlib.h> and <search.h>

**Remarks**

The **qsort** function implements a quick-sort algorithm to sort an array  of *num* elements, each of *width* bytes. The argument *base* is  a pointer to the base of the array to be sorted. **qsort** overwrites this  array with the sorted elements. The argument *compare* is a pointer to a  user-supplied routine that compares two array elements and returns a value  specifying their relationship. **qsort** calls the *compare* routine one  or more times during the sort, passing pointers to two array elements on each  call:

compare**(** **(void** ***)** elem1**,**  **(void** ***)** elem2 **);**

The routine must compare the elements, then return one of the following  values:

(参考MSDN)

void *: 无类型指针，可以用来接收各种类型的指针

```
int main()
{
    int a = 0;
    char b = 'w';
    double c = 3.14;
    void* p = &a;
    void* p = &b;
    void* p = &c;
    
    //err!
    p++;
}
```

参数解读


```
void qsort(void *base,//base中存放的是待排序数据中第一个对象的地址
           size_t num,//排序数据元素的个数
           size_t width,//排序数据中一个元素的大小，单位是字节
           int (*compare)(const void*, const void*)//是用来比较待排序数据中的2个元素的函数
           )
```

使用范例

```
#include <stdlib.h>
int cmp_int_up(const void* e1, const void* e2)
{
    return *(int*)e1 - *(int*)e2;
}
int cmp_int_down(const void* e1, const void* e2)
{
    return *(int*)e2 - *(int*)e1;
}
int main()
{
    int arr[] = { 9,8,7,6,5,4,3,2,1 };
    int sz = sizeof(arr) / sizeof(arr[0]);
    qsort(arr, sz, sizeof(arr[0]), cmp_int_up);//按照数字大小进行升序排序
    qsort(arr, sz, sizeof(arr[0]), cmp_int_down);//按照数字大小进行降序排序
    return 0;
}
```

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct Stu 
{
    char name[20];
    int age;
};
int sort_by_age (const void* e1, const void* e2)
{
    return ((struct Stu*)e1)->age - ((struct Stu*)e2)->age;
}
int sort_by_name (const void* e1, const void* e2)
{
    return strcmp((struct Stu*)e1)->name - ((struct Stu*)e2)->name;
}
int main()
{
    struct Stu s[3] = {{"zhangsan", 13},{"lisi", 14},{"wangwu", 15}};
    int sz = sizeof(s) / sizeof(s[0]);
    qsort(s, sz, sizeof(s[0]), sort_by_age);//按照年龄排序
    qsort(arr, sz, sizeof(arr[0]), sort_by_name);//按照名字首字母大小排序
}
```

模拟实现qsort函数（回调函数）

```
#include <stdio.h>
int cmp_int(const void* e1, const void* e2)
{
    return *(int*)e1 - *(int*)e2;
}
void Swap(char* buf1, char* buf2, int width)
{
    for(int i = 0; i < width; i++)
    {
        char tmp = *buf1;
        *buf1 = *buf2;
        *buf2 = tmp;
        buf1++;
        buf2++;
    }
}
void bubble_sort(void* base, int sz, int width, int (*cmp)(const void*e1, const void*e2))
{
    int i=0;
    //趟数
    for(i = 0; i < sz - 1; i++)
    {
        //一趟的排序
        for(int j = 0; j < sz - 1 - i; j++)
        {
            //两个元素比较
            //arr[j] arr[j+1]
            if(cmp( (char*)base+j*width, (char*)base+(j+1)*width))
            {
                //交换
                Swap((char*)base+j*width, (char*)base+(j+1)*width, width);
            }
        }
    }
}
int main()
{
    int arr[] = { 1,3,5,7,9,2,4,6,8,0 };
    int sz = sizeof(arr) / sizeof(arr[0]);
    bubble_sort(arr, sz, sizeof(arr[0]), cmp_int);
    return 0;
}
```

###### 野指针

```
int *f2(void)
{
	int *ptr;//未初始化, 随机值
	*ptr = 10;//error
	return ptr;
}
```

###### 易错

```
#define INT_PTR int*
typedef int* int_ptr;
INT_PTR a,b;
int_ptr c,d;
//问四个变量哪个不是指针变量?
//b
//#define 的效果相当于替换, 即第一句可以看作 int* a,b
//此时*给了a定义, a被定义成指针类型, b在后面, 没有*, 被定义成了int类型, 若要将b也定义为int*, 应写成int *a, *b;
//但是typedef是类型重定义,也就是说是c,d都是int_ptr类型, 也就是int*类型
```























## 7.调试

**bug**

>  第一次被发现的导致计算机错误的飞蛾，也是第一个计算机程序错误

###### **调试**

>**调试**(英语: Debugging / Debug), 又称除错, 是发现和减少计算机程序或电子仪器设备中程序错误的一个过程

**Debug and Release**

>**Debug** **通常称为调试版本**，它包含调试信息，并且不作任何优化，便于程序员调试程序
>
>**Release** **称为发布版本**，它往往是进行了各种优化，使得程序在代码大小和运行速度上都是最优的，以便用户很好地使用
>
>调试就是在Debug版本中找代码潜伏错误的过程

**常用快捷键**

F5

启动调试，经常用来直接跳到下一个断点处。

F9

创建断点和取消断点

**断点**的重要作用，可以在程序的任意位置设置断点。

这样就可以使得程序在想要的位置随意停止执行，继而一步步执行下去。

F10

逐过程，通常用来处理一个过程，一个过程可以是一次函数调用，或者是一条语句。

F11

逐语句，就是每次都执行一条语句，但是这个快捷键可以使我们的执行逻辑**进入函数内部**（这是最

长用的）。

CTRL + F5

开始执行不调试，如果你想让程序直接运行起来而不调试就可以直接使用。

**调试基本步骤**

1. 发现程序错误的存在
2. 以隔离、消除等方式对错误进行定位
3. 确定错误产生的原因
4. 提出纠正错误的解决方法
5. 对程序错误予以纠正，重新测试

常见错误：编译型错误、链接型错误、运行时错误

tips: 代码中加上assert（断言）可以帮助快速找到代码的问题所在

**查看信息**

- 查看**临时变量**的值

- 查看**内存**信息

- 查看**调用堆栈**

- 查看**汇编信息**

  ```
  //调试开始之后, 有两种方式转到汇编
  (1)右击鼠标, 选择"转到反汇编"
  (2)调试-> 窗口-> 反汇编
  ```

- 查看**寄存器**信息

###### **常见coding技巧**

1. 使用assert
2. 尽量使用const
3. 养成良好的编码风格
4. 添加必要的注释
5. 避免编码的陷阱

> const修饰指针变量的时候：
>
> 1. const如果放在*的左边，修饰的是指针指向的内容，保证指针指向的内容不能通过指针来改
>
>    变。但是指针变量本身的内容可变.
>
> 2. const*如果放在*的右边，修饰的是指针变量本身，保证了指针变量的内容不能修改，但是指
>
>    针指向的内容，可以通过指针改变.

###### **编程常见错误**

**编译型**错误

> 直接看错误提示信息（双击），解决问题。或者凭借经验就可以搞定。相对来说简单。

**链接型**错误

> 看错误提示信息，主要在代码中找到错误信息中的标识符，然后定位问题所在。一般是**标识符名不**
>
> **存在**或者**拼写错误**。

**运行**时错误

> 借助调试, 逐步定位问题, 最难发现

## 8.自定义类型

#### 结构体

###### 定义

> 结构体是一些值的集合, 值的类型可以不同, 而这些值就称为成员变量	

###### 结构的声明

```
struct tag
{
    member-list;
}variable-list;
```

> 可以利用typedef来简化结构体变量名

```
typedef struct tag
{

}tag;

int main()
{
    //简化前
    struct tag a[10];
    //简化后
    tag a[10];
    return 0;
}
```

>  结构体的成员也可以是另一个结构体(嵌套)	

```
sturct A
{
    int a;
    char b;
};
struct B
{
    double c;
    struct A sa;
};
```

###### 特殊的声明

>  匿名结构体类型

```
//匿名结构体类型, 省略结构体标签(tag),且只能使用一次,有局限性
struct
{
    char c;
    int i;
    char ch;
    double d;
}s;
```

```
struct
{
    char c;
    int i;
    char ch;
    double d;
}s;
struct
{
    char c;
    int i;
    char ch;
    double d;
}*p;
int main()
{
    //编译器会把上面的两个声明当成完全不同的两个类型, 所以是非法的
    p = &s;//error
    return 0;
}
```

###### 结构的自引用

```
struct Node
{
    int data;
    struct Node* next;
};//数据结构中用于实现链表结构


//error
typedef struct
{
    int data;
    Node* next;//Node未被定义不能使用
}Node;
//accepted
typedef struct Node
{
    int data;
    Node* next;
}Node;
```

###### 结构体变量的定义和初始化

```
struct Stu
{
	struct B sb;//结构体的成员可以是标量、数组、指针，也可以是另一个结构体
	char name[20];//名字
	int age;//年龄
	char id[20];//学号
} s1, s2;//声明类型的同时定义s1和s2, 这里的s1和s2也是结构体变量, 但区别就是在这里是全局变量, 而下面的s是局部变量, 所以不同的创建方式带来的效果也不一样
		//在“01串排序”中有发现，对于在此处创建的变量，例如struct Str string[100]，若结构体第一个变量为int num，可以将所有           的num初始化为0，倘若在main函数中创建string[100]，num部分初始化为0，或者说是被随机赋值
//struct是结构体关键字, 注意大括号之后还有分号

struct B
{
	char c;
	short s;
	double d;
};

int main()
{
	struct Stu s = { { 'w', 20, 3.14 }, "zhangsan", 30, "202200202" };//struct Stu是类型, s是对象,对其进行初始化
	return 0;
}
```

```
struct Point
{
	int x;
	int y;
};

struct Node
{
	int data;
	struct Point p;
	struct Node* next;
}n1 = { 10, { 4, 5 }, NULL };//结构体嵌套初始化

struct Node n2 = { 20, { 4, 5 }, NULL };//结构体嵌套初始化
```

###### 结构体成员的访问

结构变量的成员是通过点操作符访问的, 点操作符接收两个操作数

当用结构体指针访问指向变量的成员, 会使用->

```
int main()
{
	struct Stu s = { { 'w', 20, 3.14 }, "zhangsan", 30, "202200202" };//struct Stu是类型, s是对象,对其进行初始化
	//.  ->
	printf("%c ", s.sb.c);
	printf("%s ", s.id);

	struct Stu *ps = &s;
	printf("%c ", (*ps).sb.c);//解引用已经得到结构体变量
	printf("%c ", ps->sb.c);//->用于指针
	return 0;

}
```

###### 结构体传参

> 结构体传参的时候, 要传结构体的==地址==

```
struct Stu
{
	struct B sb;
	char name[20];
	int age;
	char id[20];
};

struct B
{
	char c;
	short s;
	double d;
};

void print1(struct Stu t)
{
	printf("%c %d %lf %s %d %s", t.sb.c, t.sb.s, t.sb.d, t.name, t.age, t.id);
}

void print2(struct Stu *ps)
{
	printf("%c %d %lf %s %d %s", ps->sb.c, ps->sb.s, ps->sb.d, ps->name, ps->age, ps->id);
}

int main()
{
	struct Stu s = { { 'w', 20, 3.14 }, "zhangsan", 30, "202200202" };
	//写一个函数打印s的内容
	print1(s);//传值调用(在时间和空间上产生浪费)函数传参的时候, 参数是需要压栈的, 如果传递一个结构体对象的时候, 结构体过大, 参数压栈的系统开销比较大, 会导致性能的下降
	print2(&s);//传址调用(效率高且便于改变), 是最优选择
	return 0;
}
```





















###### 结构体大小与内存对齐

> 结构体==对齐规则== :
>
> 1.第一个成员先存放在与结构体变量在内存中存储位置偏移量为0的地址处
>
> 2.其他成员变量要存放到对应对齐数的整数倍的地址
>
> ​	**对齐数** = 编译器默认的一个对齐数与该成员变量的**较小值**
>
> ​	(vs中默认值为8   Linux没有默认对齐数)
>
> 3.结构体的总大小为结构体中所有成员的对齐数(每个成员变量都有一个对齐数)中最大对齐数的整数倍
>
> 4.如果嵌套了结构体的情况, 嵌套的结构体对齐到自己的最大对齐数的整数倍处, 结构体的整体大小就是所有最大对齐数(含嵌套结构体对齐数)的整数倍

```
struct S
{
   char c1;
   int i;
   char c2;
};
int main()
{
   struct S s = {0};
   printf("%d\n", sizeof(s));//12
   return 0;
}
```

```
struct S3
{
    double d;
    char c;
    int i;
};//16
struct S4
{
    char c1;
    struct S3 s3;
    double d;
};//32
```

> 为什么存在内存对齐?
>
> 1.平台原因(移植原因): 不是所有的硬件平台都能访问任意地址上的任意数据的, 某些硬件平台只能在某些地址处取某些特定类型的数据, 否则抛出硬件异常
>
> 2.性能原因: 数据结构(尤其是栈)应该尽可能地在自然边界上对齐, 原因在于,为了访问未对齐的内存, 处理器需要做两次内存访问, 而对齐的内存仅需要一次访问
>
> 总体来说: 结构体的内存对齐是拿空间换取时间.
>
> 那在设计结构体的时候, 既要满足对齐, 又要节省空间, 如何做到: 
>
> **让占用空间小的成员尽量集中在一起**.

```
//例如
struct S1
{
    char c1;
    int i;
    char c2;
};//12

struct S2
{
    char c1;
    char c2;
    int i;
};//8
```

> 修改默认对齐数
>
> ​	当结构在对齐方式不合适的时候, 我们可以自己更改默认对齐数
>
> #pragma 是预处理指令

```
//修改为2
#pragma pack(2)
struct S
{
    char c1;
    int i;
    char c2;
};//8
#pragma pack()

//修改为1(但是实际中不会设计为奇数, 一般为2的n次方)
#pragma pack(1)
struct S
{
    char c1;
    int i;
    char c2;
};//6
#pragma pack()
```

>  offsetof 宏的实现

***offsetof*** 

<stddef.h>

Retrieves the offset of a member from the beginning of its parent structure.

Remarks: The offsetof macro returns the offset in bytes of *memberName*  from the beginning of the structure specified by *structName*. You can  specify types with the struct keyword.

```
#include <std'def.h>
struct S
{
    char c1;
    int i;
    char c2;
};
int main()
{
    printf("%d\n", offsetof(struct S, c1));//0
    printf("%d\n", offsetof(struct S, i));//4
    printf("%d\n", offsetof(struct S, c2));//8
}
```

```
//模拟实现offsetof
#define OFFSETOF(struct_name, men_name) (int)&(((struct_name*)0)->men_name)
struct A
{
	int a;
	short b;
	int c;
	char d;
};
int main()
{
	printf("%d\n",OFFSETOF(struct A, a));
	return 0;
}
```

#### 位段

###### 位段的声明

> 位段的声明和结构是相似的, 有两个不同: 
>
> 1.位段的成员必须是 int      unsigned int  或  signed int
>
> 2. 位段的成员名后边有一个冒号和数字

```
//A就是一个位段类型
struct A
{
    int _a:2;
    int _b:5;
    int _c:10;
    int _d:30;
}
```

###### 位段的内存分配

>  1. 位段的成员可以是 int   unsigned int   signed int  或者是 char (属于整型家族) 类型
>2. 位段的空间上是按照需要以4个字节(int) 或者1个字节(char) 的方式来开辟的
> 3. 位段涉及很多不确定因素, 位段是不跨平台的, 注重可移植的程序应该避免使用位段

```
//位段结构体所占空间大小
struct A
{
    //按需求开辟空间, 可以尽可能节省空间
    int _a:2;//_a 成员占2个bit位
    int _b:5;//_b 成员占5个bit位
    int _c:10;//_c 成员占10个bit位
    int _d:30;//_d 成员占30个bit位
    //error  已经超过所设置的类型大小,即如果设置int, 最多开辟32个bit
    int _e:50;
}

int main()
{
    printf("%d\n", sizeof(struct A));//8
}
```

```
struct S
{
    char a:3;
    char b:4;
    char c:5;
    char d:4;
}
struct S s = {0};
//在内存中的存储方式
//以二进制形式存放, 且存放顺序是从内存的低地址到高地址
//先开辟一个char类型空间 00000000
s.a = 10;
//1010    存放3个bit位,即010    00000010
s.b = 12;
//1100    存放4个bit位,即1100   01100010
//c占5个bit位,上一个byte空间已经不够,重新开辟一个char
s.c = 3;
//11       存放5个bit位,即00000011
//再开辟一个char
s.d = 4;
//100      存放4个bit位,即00000100
//最后内存中存放的结果应该是01100010 00000011 00000100
//转化为十六进制是62 03 04
//此处无需讨论大小端存储不同, 因为大小端是字节存储顺序的不同,此处是存放进字节中
//特别注意: 此种存储方式是在VS编译器下,其他编译器不一定
```

###### 位段的跨平台问题

> 1. int位段被当成有符号数还是无符号数是不确定的
>2. 位段中最大位的数目不能确定. ( 16位机器 int类型是2个byte, 即16个bite, 若写27, 会导致在16位机器上出错 )很少的
> 3. 位段中的成员在内存中从左向右分配, 还是从右向左分配标准尚未定义
> 4. 当一个结构包含两个位段, 第二个位段成员比较大, 无法容纳第一个位段剩余的位时, 是舍弃还是利用剩余的位, 是不确定的

> **总结**: 跟结构相比, 位段可以达到同样的效果, 且可以很好的节省空间, 但是有跨平台的问题存在

#### 枚举

> 顾名思义就是一一列举, 把可能的取值一一列举

###### 枚举类型的声明

```
enum color
{
    blue,
    red,
    green
};
int main()
{
    //accepted
    enum color c = blue;
    //error
    //特别是在语法要求严格的CPP
    //想把blue赋给c, 这样写会报错, 提示无法将int类型转化为color类型
    enum color c = 0;
}
```

```
enum Day//枚举类型
{
    //枚举类型的可能取值,也叫枚举常量,区别于结构体的成员
    //枚举常量的值为int类型
    Mon,
    Tues,
    Wed,
    Thus,
    Fri,
    Sat,
    Sun
};
int main()
{
    //这些可能取值都是有值的, 默认从0开始, 依次递增1
    printf("%d\n", Mon);//0
    printf("%d\n", Tues);//1
    printf("%d\n", Wed);//2
    printf("%d\n", Thus);//3
    printf("%d\n", Fri);//4
    printf("%d\n", Sat);//5
    printf("%d\n", Sun);//6
    
    return 0;
}


//在定义的时候也可以对常量赋初值
enum Day
{
    Mon = 5,
    Tues,
    Wed,
    Thus,
    Fri,
    Sat,
    Sun
};
int main()
{
    printf("%d\n", Mon);//5
    printf("%d\n", Tues);//6
    printf("%d\n", Wed);//7
    printf("%d\n", Thus);//8
    printf("%d\n", Fri);//9
    printf("%d\n", Sat);//10
    printf("%d\n", Sun);//11
    
    return 0;
}
```

###### 枚举的优点

> 我们可以使用#define 定义常量, 为什么非要用枚举?
>
> 1. 增加代码的可读性和可维护性
>
>    将值与常量名联系与替换
>
> 2. 和#define 定义的标识符比较, 枚举有类型检查, 更加严谨
>
>    比如enum定义的常量在main函数里面想再次赋值会报错,参见上error内容
>
> 3. 防止命名污染(封装)
>
>    define定义的是全局量, 可能会导致我们后面创建变量的时候命名重复而造成命名污染, 但是enum不会
>
> 4. 便于调试, 预编译的时候不会改变代码. 
>
>    例如int a = Mon ,若用define定义,会导致在预编译的时候Mon已经替换为0, 后期生成.exe文件要调试的时候难以观察, 但是用enum则会保留,便于调试
>
> 5. 使用方便, 一次可以定义多个常量
>
>    不用多次#define

#### 联合(共用体)

###### 联合类型的定义

> 联合也是一种特殊的自定义类型,
>
> 这种类型定义的变量也包含一系列的成员, 特征是这些成员公用同一块空间(所以联合也叫共同体)

######  联合类型的使用

```
//联合类型的声明
union Un
{
    char c;
    int i;
};

int main()
{
    //创建联合体变量
    union Un un;
    return 0;
}
```

###### 联合的特点

```
union Un
{
    char c;
    int i;
};
int main()
{
    union Un un;
    
     //地址  三组打印的地址都相同, 说明有共同使用的一块内存
    printf("%p\n", &un);
    printf("%p\n", &(un.c);
    printf("%p\n", &(un.i);
    
    //初始化
    //c = 10; i = 10
    union Un un = {10};
    
    //改变联合体一个变量的值时, 会导致另外使用相同空间的变量的值被改变
    un.i = 0x11223344;
    un.c = 0x55;
    printf("%x\n", un.i);//0x55
    
    return 0;
}
```

```
//判断机器数据存储方式
int check_sys()
{
    union U
    {
        char c;
        int i;
    }u;
    u.i = 1;//00 00 00 01
    return u.c;
}
int main()
{
    int ret = check_sys();
    if(ret == 1) printf("小端\n");
    else printf("大端\n");
    return 0;
}
```

###### 联合大小的计算

>  联合的大小至少是最大成员的大小(因为联合至少得有能力保存最大的那个成员)
>  

```
union Un
{
    char c;
    int i;
};
int main()
{
    union Un un;

    //联合体大小
    printf("%d\n", sizeof(un));//4
    return 0;
}
```

>  当最大成员大小不是最大对齐数的整数倍时, 就要对齐到最大对齐数的整数倍

```
union Un
{
    char a[5];//1(对齐数)   大小为5个字节,但对齐数要看char, 仍为1
    int i;//4
};

int main()
{
    union Un un;
    printf("%d\n", sizeof(un));//8
}
```

## 9.数组

###### 定义

一组相同类型元素的集合

```
type_t arr_name [const_n]
//type_t 是指数组的元素类型
//const_n 是一个常量表达式, 用来指定数组大小
//注意:数组创建, 在C99标准之前, []中要给一个常量才可以, 不能使用变量, 在C99标准支持了变长数组的概念
```

###### 类型

```
int main()
{
	int arr[10];//整型数组——存放整形的数组就是整型数组
	char ch[5];//字符数组——存放字符的数组就是字符数组
	//指针数组——存放指针的数组
	int* parr[5];//整型指针的数组
	char* par[5];//字符指针的数组
	return 0;
}
```

###### 数组初始化

初始化是指在创建数组的同时给数组的内容一些合理初始值(初始化).

数组在创建的时候如果想不指定数组的确定大小就得初始化, 数组的元素个数根据初始化的内容来确定.

```
//后接'\0'
char arr1[] = "abc";
printf("%d", strlen(arr1));//3
//后n位才是'\0'
char arr2[3] = {'a', 'b', 'c'};
printf("%d", strlen(arr2));//randon
```

###### 数组越界

数组的下标是有范围限制的.

包含n个元素的数组下标从0开始, 最后一个元素的下标就是n-1, 如果数组的下标如果小于0, 或者大于n-1, 就是数组越界访问了, 超出了数组合法化空间的访问. 

C语言本身是不做数组下标的越界检查, 编译器也不一定报错, 但是编译器不报错, 并不意味着程序就是正确的, 所以必须做好越界检查. 

###### 一维数组

操作符: [] 是下标引用操作符, 用来进行数组访问

注意: 下标从0开始

**数组在内存中的存储**

数组在内存中是连续存放的, 由低地址到高地址

###### 二维数组

```
int arr[3][4] = {1, 2, 3, 4};
int arr[3][4] = {{1, 2}, {4, 5}};
int arr[][4] = {{2, 3}, {4, 5}};//二维数组如果有初始化, 行(row)可以省略, 列(column)不能省略
```

```
int main()
{
    //特别注意，此处是括号！属于逗号表达式，只保留最后一个数值，所以实际上相当于{ 1, 3, 5}
    int a[3][2] = { (0, 1), (2, 3), (4, 5) };
    int* p;
    p = a[0];
    printf("%d", p[0]);//1
    return 0;
}
```

```
int main()
{
    int a[5][5];
    int(*p)[4];
    //p是一个数组指针,对应存放4个int的数组，所以把a数组的地址存进去，会被以每4个int一行的方式进行读取
    //00000  00000  00000  00000   00000
    //0000/0 000/00 00/000 0/0000/ 0000/0
    p = a;
    //结果是-4,存进内存是补码,用%p会直接以地址形式打印
    printf("%p,%d", &p[4][2] - &a[4][2], &p[4][2] - &a[4][2]);//FFFFFFFC -4
}
```



###### 数组名

一般情况下，数组名是**首元素**地址，而且对于这个地址，是不可变的，即为**常量**，存放于**静态区**

>  特殊情况
> sizeof(数组名)  -  数组名表示整个数组，计算的是整个数组大小
> &+数组名  -  数组名表示整个数组，取出的是数组的地址
> 除此之外，所有数组名都是数组首元素的地址

```
int main()
{
    int a[] = { 1, 2, 3, 4 };
    printf("%d\n", sizeof(a));//16
    printf("%d\n", sizeof(a + 0));//4/8(特别注意,此处计算的是第一个地址的大小)
    printf("%d\n", sizeof(*a));//4 取的是数组首元素的地址，不是数组的地址，解引用得到1
    printf("%d\n", sizeof(a + 1));//4/8 a+1是第二个元素的地址，此处计算的是地址的大小
    printf("%d\n", sizeof(a[1]));//4 计算第二个元素的大小
    printf("%d\n", sizeof(&a));//4/8 取出数组的地址，但是仍然是一个地址
    // &a -- int (*pa)[4] = &a
    printf("%d\n", sizeof(* &a));//16 解引用得到数组
    printf("%d\n", sizeof(&a + 1));//4/8 跳过一整个数组，但仍是一个地址
    printf("%d\n", sizeof(&a[0]));//4/8
    printf("%d\n", sizeof(&a[0] + 1));//4/8
    
    
    char arr[] = { 'a', 'b', 'c', 'd', 'e', 'f' };
    //a b c d e f
    printf("%d\n", sizeof(arr));//6 此处不是7,因为是直接根据字母多少开辟的数组,没有加'\0'
    printf("%d\n", sizeof(arr + 0));//4/8
    printf("%d\n", sizeof(*arr));//1
    printf("%d\n", sizeof(arr));//1
    printf("%d\n", sizeof(&arr));//4/8
    printf("%d\n", sizeof(&arr + 1));//4/8
    printf("%d\n", sizeof(&arr[0] + 1));//4/8
    
    printf("%d\n", strlen(arr));//randon num  strlen会向后走直至找到'\0' 
    printf("%d\n", strlen(arr));//randon num
    printf("%d\n", strlen(*arr));//*arr是a,ASCII码值为97,而strlen接收的应该是地址,会报错
    printf("%d\n", strlen(arr[1]));//err
    //size_t strlen( const char *string );
    printf("%d\n", strlen(&arr));//randon 取出数组地址char(*)[6],传过去会被强制转化为char*
    printf("%d\n", strlen(&arr + 1));//randon
    printf("%d\n", strlen(arr));//randon
    
    
    char arr[] = "abcdef";
    //a b c d e f \0  (字符串结束标志是'\0')
    printf("%d\n", sizeof(arr));//7
    printf("%d\n", sizeof(arr + 0));//4/8
    printf("%d\n", sizeof(*arr));//1
    printf("%d\n", sizeof(arr[1]));//1
    printf("%d\n", sizeof(&arr));//4/8
    printf("%d\n", sizeof(&arr + 1));//4/8
    printf("%d\n", sizeof(&arr[0] + 1));//4/8
    
    printf("%d\n", strlen(arr));//6
    printf("%d\n", strlen(arr + 0));//6
    printf("%d\n", strlen(*arr));//err
    printf("%d\n", strlen(arr[1]));//err
    printf("%d\n", strlen(&arr));//6
    printf("%d\n", strlen(&arr + 1));//randon
    printf("%d\n", strlen(&arr[0] + 1));//5
    
    
    char* p = "abcdef";
    printf("%d\n", sizeof(p));//4/8
    printf("%d\n", sizeof(p + 1));//4/8
    printf("%d\n", sizeof(*p));//1
    printf("%d\n", sizeof(p[0]));//1
    printf("%d\n", sizeof(&p));//4/8
    printf("%d\n", sizeof(&p + 1));//4/8
    printf("%d\n", sizeof(&p[0] + 1));//4/8
    
    printf("%d\n", strlen(p));//6
    printf("%d\n", strlen(p + 1));//5
    printf("%d\n", strlen(*p));//err
    printf("%d\n", strlen(p[0]));//err
    printf("%d\n", strlen(&p));//randon  特别注意此处与&arr的区别,p在这里已经开辟了一个空间存放常量字符串的地址,这里取的是p的地址,也就是说解引用得到的是p,p是4/8个字节,这些字节里面可能就有'\0',比如0x11002248,所以后面什么时候有'\0'未知
    printf("%d\n", strlen(&p + 1));//randon,此处相比&p跳过了一个地址的大小，且此处的随机值与上一个随机值无联系
    printf("%d\n", strlen(&p[0] + 1));//5
    
    
    int a[3][4] = { 0 };
    printf("%d\n", sizeof(a));//48
    printf("%d\n", sizeof(a[0][0]));//4
    //在二维数组中，当a[i]单独放在sizeof中时，代表的是第一行的所有元素，但是不是单独时，是代表第一行第一个元素的地址
    printf("%d\n", sizeof(a[0]));//16
    printf("%d\n", sizeof(a[0] + 1));//4/8
    printf("%d\n", sizeof(*(a[0] + 1)));//4  第一行第二个元素
    printf("%d\n", sizeof(a + 1));//4/8 代表第二行的地址
    printf("%d\n", sizeof(*(a + 1)));//16  (a+1)<=>a[1]
    printf("%d\n", sizeof(&a[0] + 1));//4/8
    printf("%d\n", sizeof(*(&a[0] + 1)));//16
    printf("%d\n", sizeof(*a));//16
    printf("%d\n", sizeof(a[3]));//16  a[3]其实是第四行的数组名，不存在，但是sizeof内部的表达式是不计算的，所以系统不会关注值属性，也不会越界访问，只要能推出a[3]的大小，即类型属性，就可以得出结果
    return 0;
}
```



```
int main()
{
	int arr[10] = { 0 };
	printf("%p\n", arr);
	printf("%p\n", &arr[0]);  //数组名等于首元素（的首）地址
	return 0;
}
```

###### 数组与指针

```
int main()
{
	int arr[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
	int *p = arr;
	printf("%d\n", 2[arr]);
	printf("%d\n", arr[2]);//[]是个操作符，内外可交换
	printf("%d\n", p[2]);//说明p[2]也是转化为*（p+2）
	//因为编译器在处理arr[2]的时候，实际上是将arr[2]编译为*(arr+2),所以可以交换。

	//arr[2] --> *(arr+2) --> *(2+arr) --> 2[arr]
	//arr[2] <==> *(arr+2) <==> *(p+2) <==> *(2+p)
	//arr[2] <==> 2[arr]
	return 0;
}
```

```
int main()
{
	int arr[10] = { 0 };
	int *p = arr;
	int i = 0;
	for (i = 0; i < 10; i++)
	{
		//printf("%p <==> %p\n", &arr[i], p + i);//说明arr[i]和p+i结果一致
		//运用指针改变数组内容
		*(p+i)=i;
	}

	for (i = 0; i < 10; i++)
	{
	    //打印数组
		printf("%d\n", *(p + i));
	}

	return 0;
}
```

```
int main()
{
	for (vp = &values[5]; vp > &values[0];)
	{
		*--vp = 0;
	}

	for (vp = &values[5 - 1]; vp >= &values[0]; vp--)
	{
		*vp = 0;
	}
	//两种写法虽然结果都一样，但是应该避免第二种写法，因为标准并不可行，理由是标准规定允许指向数组元素的指针与指向数组最后一个元素后面的那个内存位置的指针比较，但是不允许与指向第一个元素之前的那个内存位置的指针进行比较。
}
```

```
int main()
{
    //涉及到类型转换与小端存储
    //01 00 00 00 02 00 00 00 03 00 00 00 04 00 00 00
    int a[4] = { 1, 2, 3, 4 };
    int* ptr1 = (int*)(&a + 1);
    int* ptr2 = (int*)((int)a + 1);//首元素地址被转换为int类型,加1代表地址加1,即向后移动1个字节,然后再以int*的类型进行访问
    //%x代表十六进制
    printf("%x,%x", ptr1[-1], *ptr2);//4, 2000000
    printf("%#x,%#x", ptr1[-1], *ptr2);//0x4, 0x02000000
    return 0;
}
```



## 10.动态内存管理

###### 存在意义

```
已掌握的内存开辟方式
int val = 20;//在栈上开辟4个字节
char arr[10] = {0};//在栈上开辟10个字节的连续空间
```

> 上述开辟方式有两个特点
>
> 1. 空间开辟的大小是固定的
> 2. 数组在声明的时候, 必须指定数组的长度, 它所需要的内存在编译时分配
>
> 但是对于空间的需求, 不仅仅是上述的情况, 有时候我们需要的空间大小在程序运行的时候才能知道, 那数组编译时开辟空间的方式就不能满足了, 需采用动态内存开辟

###### 函数介绍

***malloc***

<stdlib.h>

Allocates memory blocks.

void *malloc( size_t size );

Remarks: The malloc function allocates a memory block of at least *size*  bytes. The block may be larger than *size* bytes because of space required  for alignment and maintenance information.

> 这个函数向内存申请一块连续可用的空间, 并返回指向这块空间的指针
>
> - 如果开辟成功, 则返回一个指向开辟好空间的指针
> - 如果开辟失败, 则返回一个NULL指针, 因此malloc的返回值一定要做检查
> - 返回值的类型是void*, 所以malloc函数并不知道开辟空间的类型, 具体在使用的时候使用者自己决定
> - 如果参数size为0, malloc的行为是标准未定义的, 取决于编译器

***free***

<stdlib.h>

Deallocates or frees a memory block.

void free( void* memblock );

Remarks: to MSDN

> 专门用于做动态内存的释放和回收
>
> - 如果参数memblock指向的空间不是动态开辟的, 那free函数的行为是未定义的
> - 如果参数memblock是NULL指针, 则函数无作为

```
#include <stdlib.h>
int main()
{
    //假设开辟10个整型空间 - 10*sizeof(int)
    //int arr[10];栈区
    
    //动态内存开辟
    int* p = (int*)malloc(10*sizeof(int));//void*   堆区
    if(p == NULL)
    {
        perror("main");//main: xxxxxxxx  e.g. main: No enough space
        return 0;
    }
    //使用
    for(int i=0; i<10; i++)
    {
        *(p+i) = i;//访问方式 *(p+i)  or  p[i]
    }
    for(int i=0; i<10; i++)
    {
        printf("%d ", p[i]);//p[i] -> *(p+i)
    }
    //释放和回收
    free(p);
    //将p置为空指针
    p = NULL;
    
    return 0;
}
```

***calloc***

<stdlib.h> 

Allocates an array in memory with elements initialized to 0.

void* calloc( size_t num, size_t size );

Remarks: to MSDN

> - 函数的功能是为num个大小为size的元素开辟一块空间, 并且把空间的每个字节初始化为0
>
> - 与函数malloc的区别是calloc会在返回地址之前把申请的空间的每个字节**初始化为0**

***realloc***

<stdlib.h> 

Reallocate memory blocks.

void* realloc( void*  memblock, size_t size);

Remarks: to MSDN

> - realloc函数的出现让动态内存管理更加灵活
> - realloc函数用于对动态开辟内存大小的调整

> - memblock是要调整的内存地址
> - size是调整之后的大小
> - 返回值为调整之后的内存起始位置
> - realloc在调整内存空间的时候有两种情况:
>   1. 原有空间之后空间足够大: 在原有内存之后直接追加空间, 原来空间的数据不发生变化
>   2. 原有空间之后空间不足: 在堆空间上找另外一个适合大小的连续空间使用, 并返回一个新的内存地址

```
#include <stdlib.h>
int main()
{
    int *ptr = (int*)malloc(100);
    if(ptr != NULL)
    {
        //
    }
    else
    {
        exit(EXIT_FAILURE)
    }
    //扩展容量
    //error show  扩容失败会导致ptr被置空而丢失原地址
    ptr = (int*)realloc(ptr, 1000);
    
    //accepted
    int* p = NULL;
    p = realloc(ptr, 1000);
    if(p != NULL)
    {
        ptr = p;
    }
    //
    free(ptr);
    ptr = NULL;
    return 0;
}
```

```
#include <stdlib.h>
int main()
{    
    //这里功能相当于malloc, 就是直接在堆区开辟40个字节
    int* p = (int*)realloc(NULL, 40);
    return 0;
}
```

###### 常见动态内存错误

> 对NULL的解引用操作

```
int main()
{
    //error  开辟失败, 对NULL解引用操作
    int* p = (int*)malloc(10000000000000);//NULL
    for(int i=0; i<10; i++)    *(p+i) = i;
    free(p);
    return 0;
    
    //需对malloc函数返回值先做判断
    if(p == NULL)
}
```

> 对动态开辟空间的越界访问

```
#include <stdio.h>
int main()
{
    int* p = malloc(10*sizeof(int));
    if(p == NULL)
    {
        return 1;
    }
    for(int i=0; i<40; i++)
    {
        *(p+i) = i;//越界访问
    }
    free(p);
    return 0;
}
```

> 对非动态开辟内存使用free释放

```
void test()
{
    //error
    int a = 10;
    int* p = &a;
    free(p);
}
```

> 使用free释放一块动态开辟内存的一部分

```
void test()
{
    //error
    //p不再指向动态内存的起始位置
    
    int *p = (int*)malloc(100);
    p++;
    free(p);
    //or
    for(int i=0; i<10; i++)
    {
        *p++ = i;
    }
}
```

>对同一块动态内存多次释放

```
void test()
{
    int *P = (int*)malloc(100);
    free(p);
    free(p);//重复释放
}
```

> 动态开辟内存忘记释放(内存泄漏)
>
> > 动态开辟空间回收方式
> >
> > 1. 主动free
> > 2. 程序结束
>
> 切记: 动态开辟的空间一定要释放, 并且正确释放, 且最好在释放后再对指针置空

```
void test()
{
    int *p = (int*)malloc(100);
    if(NULL != p)
    {
        *p = 20;
    }
}
int main()
{
    test();
    while(1)
}
```

> 传值调用而发生错误

```
void GetMemory(char *p)
{
    p = (char*)malloc(100);
}
void test(void)
{
    char *str = NULL;
    GetMemory(str);//此处是传值调用,p只相当于临时str的临时拷贝, 动态内存开辟的地址存放在p中,不会影响外边的str,所以GetMemory函数返回之后,str仍然是NULL,会发生错误
    strcpy(str, "Hello world");
    printf(str);
}


//修改后
char* GerMemory(char* p)
{
    p = (char*)malloc(100);
    return p;
}
void test(void)
{
    char *str = NULL;
    str =  GetMemory(str);
    strcpy(str, "Hello world");
    printf(str);
    free(str);
    str = NULL;
}
//or 
//使用二级指针
```

> 在堆区和堆栈区开辟空间的区别

```
char *GetMemory(void)
{
	//返回栈空间地址问题
    char p[] = "Hello world";//创建的局部数组在栈区上, 此时p是栈空间地址, 确实会传给str, 但是出了此函数, p数组空间也将还给操作系统, 也就是生命周期结束, 返回的地址是没有意义的, 甚至被其他数据覆盖, 如果通过返回的地址去访问内存, 就是非法访问内存
    return p;
}
void Test(void)
{
    char *str = NULL;
    str = GetMemory();
    printf(str);
}
int main()
{
	test();
	return 0;
}


//
参见上一个malloc代码, 是在堆空间开辟的空间, 不会出现出了函数导致空间被回收的问题

//类似错误
int *f1(void)
{
	int x = 10;
	return (&x);
}
```

###### C/C++程序的内存开辟

<img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20221007185643969.png" alt="image-20221007185643969"  />

> 1. 栈区(stack): 在执行函数时, 函数内局部变量的存储单元都可以在栈上创建, 函数执行结束时这些存储单元自动被释放. 栈内存分配运算内置于处理器的指令集中, 效率很高, 但是分配的内存容量有限. 栈区主要存放运行函数而分配的局部变量, 函数参数, 返回数据, 返回地址等
> 2. 堆区(heap): 一般由程序员分配释放, 若程序员不释放, 程序结束时可能由OS回收, 分配方式类似于链表
> 3. 数据段(静态区)(static): 存放全局变量, 静态数据, 程序结束后由系统释放
> 4. 代码段: 存放函数体(类成员函数和全局函数)的二进制代码

> 实际上普通的的局部变量是在栈区分配空间的, 栈区的特点是在上面创建的变量出了作用域就销毁, 但是被static修饰的变量存放在数据段(静态区), 数据段的特点是在上面创建的变量, 直到程序结束才销毁, 所以生命周期变长

###### 柔性数组

> C99中, 结构中的最后一个元素允许是未知大小的数组, 这就叫做柔性数组成员

```
typedef struct st_type
{
	int i;
	int a[0];//柔性数组成员
}type_a;

//有些编译器会报错无法编译, 可以改成
typedef struct st_type
{
	int i;
	int a[];//柔性数组成员
}type_a;

```

> 特点:
>
> - 结构中的柔性数组成员前面必须至少有一个成员
> - sizeof返回的这种结构大小不包括柔性数组的内存, 直接计算前面成员的大小
> - 包含柔性数组成员的结构用malloc()函数进行内存的动态分配, 并且分配的内存应该**大于**结构的大小, 以适应柔性数组的预期大小

```
typedef struct st_type
{
	int i;
	int a[];//柔性数组成员
}type_a;
printf("%d\n", sizeof(type_a));//4
```

> 柔性数组的使用

```
//使用柔性数组
struct S
{
	int n;
	int arr[0];
};
int main()
{
	struct S*ps = (struct S*)malloc(sieof(struct S)+10*sizeof(int));
	ps-> = 10;
	int i=0;
	for(i = 0; i<10; i++)
	{
		ps->arr[i] = i;
	}
	//增加
	struct S* ptr = (strcut S*)realloc(ps, sieof(struct S)+20*sizeof(int));
	if(ptr != NULL)
	{
		ps = ptr;
	}
	//使用
	
	//释放
	free(ps);
	ps = NULL;
	return 0;
}


//相同功能,不使用柔性数组
struct S
{
	int n;
	int *arr;
};
int main()
{
	struct S* ps = (struct S*)malloc(sizeof(struct S));
	if(ps == NULL)	return 1;
	ps->arr = (int*)malloc(10*sizeof(int));
	if(ps->arr == NULL)	return1;
	for(int i = 0; i<10; i++)
	{
		ps->arr[i] = i;
	}
	//增加
	int*ptr = (int*)realloc(ps->arr, 20*sizeof(int));
	if(ptr != NULL)
	{
		ps->arr = ptr;
	}
	//使用
	//回收
	free(ps->arr);
	ps->arr = NULL;
	free(ps);
	ps = NULL;
	return 0;
}
```

> 代码1与代码2相比, 代码1使用柔性数组的优势:
>
> 1. 方便内存释放
>
>    如果我们的代码是在一个给别人用的函数中, 你在里面做了二次内存分配, 并把整个结构体返回给用户. 用户调用free可以释放结构体, 但是用户并不知道这个结构体的成员也需要free, 你不能指望用户来发现这个事, 所以如果我们把结构体的内存以及其它成员要的内存一次性分配好了, 并返回给用户一个结构体指针,用户做一次free就可以把所有的内存也给释放掉
>
> 2. 有利于提高访问速度
>
>    连续的内存有益于提高访问速度, 也有益于减少内存碎片(malloc用得越多, 内存碎片也会增多).

> [更多关于柔性数知识, 参见](https://coolshell.cn/articles/11377.html)

## 11.C语言文件操作

###### 为什么使用文件

> 我们一般对数据持久化的方法有: 把数据存到磁盘文件, 存放到数据库等方式
>
> 使用文件我们可以将数据直接存放到电脑的硬盘上, 做到了数据的持久化

###### 文件定义

> 磁盘上的文件就是文件.
>
> 但是在程序设计中, 我们一般谈的文件有两种: 程序文件和数据文件(从文件功能的角度来分类)
>
> - 程序文件: 包括源程序文件(后缀为.c), 目标文件(windows环境后缀为.obj), 可执行程序(windows环境后缀为.exe)
> - 数据文件: 文件的内容不一定是程序, 而是程序运行时读取的数据, 比如程序运行需要从中读取数据的文件, 或者输出内容的文件

###### 文件名

> 一个文件要有一个唯一的文件标识, 以便用户识别和引用
>
> 文件名包括三部分: 文件路径+文件名主干+文件后缀
>
> 例如: c:\code\test.txt
>
> 为了方便起见, 文件标识常被称为文件名

###### 文件指针

> 缓存文件系统中, 关键的概念是"文件类型指针", 简称"文件指针".
>
> 每个被使用的文件都在内存中开辟了一个相应的文件信息区， 用来存放文件的相关信息(如文件的名字, 文件状态及文件当前的位置等等). 这些信息是保存在一个结构体变量中的. 该结构体类型是有系统声明的, 取名FILE
>

```
//例如: VS2013编译环境提供的stdio.h头文件中有以下的文件类型声明
struct _iobuf{
	char *_ptr;
	int   _cnt;
	char *_base;
	int   _flag;
	int   _file;
	int   _charbuf;
	int   _bufsiz;
	char *_tmpfname;
};
typedef struct _iobuf FILE;
```

- 不同的C编译器的FILE类型包含的内容不完全相同, 但是大同小异

- 每当打开一个文件的时候, 系统会根据文件的情况自动创建一个FILE结构的变量, 并填充其中的信息, 使用者不必关心细节.

- 一般都是通过一个FILE指针来维护这个FILE结构的变量的, 这样使用起来更方便.

```
//下面我们可以创建一个FILE类型的变量
//文件指针变量
FILE* pf;
```

定义pf是一个指向FILE类型数据的指针变量, 可以使pf指向某个文件的文件信息区(是一个结构体变量), 通过该文件信息区中的信息就能够访问该文件, 也就是说, 通过文件指针变量就能够找到与它相关联的文件. 

###### 文件的打开和关闭

- 文件在读写之前应该先打开文件, 在使用结束之后应该关闭文件.

- 在编写程序的时候, 在打开文件的同时, 都会返回一个FILE*的指针变量指向该文件, 也相当于建立了指针与文件的关系.
- ANSIC规定使用fopen函数打开文件, fclose关闭文件.

***fopen***

<stdio.h>

Open a file.

FILE* fopen(const char* filename, cosnt char* mode);

More functions :to MSDN

| 文件使用方式  | 含义                                     | **如果指定文件不存在** |
| ------------- | ---------------------------------------- | ---------------------- |
| “r”（只读）   | 为了输入数据，打开一个已经存在的文本文件 | 出错                   |
| “w”（只写）   | 为了输出数据，打开一个文本文件           | 建立一个新的文件       |
| “a”（追加）   | 向文本文件尾添加数据                     | 建立一个新的文件       |
| “rb”（只读）  | 为了输入数据，打开一个二进制文件         | 出错                   |
| “wb”（只写）  | 为了输出数据，打开一个二进制文件         | 建立一个新的文件       |
| “ab”（追加）  | 向一个二进制文件尾添加数据               | 出错                   |
| “r+”（读写）  | 为了读和写，打开一个文本文件             | 出错                   |
| “w+”（读写）  | 为了读和写，建议一个新的文件             | 建立一个新的文件       |
| “a+”（读写）  | 打开一个文件，在文件尾进行读写           | 建立一个新的文件       |
| “rb+”（读写） | 为了读和写打开一个二进制文件             | 出错                   |
| “wb+”（读写） | 为了读和写，新建一个新的二进制文件       | 建立一个新的文件       |
| “ab+”（读写） | 打开一个二进制文件，在文件尾进行读和写   | 建立一个新的文件       |

***fclose***

<stdio.h>

Closes a stream (**fclose**) or closes all open streams  (**_fcloseall**).

int fclose(FILE* stream);

Remarks: to MSDN

```
//使用范例
#include <stdio.h>
int main()
{
	FILE* pf;
	//打开文件
	pf = fopen("myfile.txt", "W");
	if(pf == NULL)
	{
		perror("fopen");
	}
	//文件操作
	fputs("fopen example", pf);
	//关闭文件
	fclose(pf);
	pf = NULL;
	return 0;
}

//注意: 上面fopen中直接写文件名的写法是相对路径, 只能打开与源程序文件同一个文件夹的文件, 若要打开其他外部文件, 则要采用绝对路径
//e.g.  E:\Code.c\c_code\Test.c\test.c
//特别注意: 绝对路径写进fopen时, '\'要双写, 否则会被判定为转义字符
//E:\\Code.c\\c_code\\Test.c\\test.c
```

###### 文件的顺序读写

| **功能**       | **函数名** | **适用于** |
| -------------- | ---------- | ---------- |
| 字符输入函数   | fgetc      | 所有输入流 |
| 字符输出函数   | fputc      | 所有输出流 |
| 文本行输入函数 | fgets      | 所有输入流 |
| 文本行输出函数 | fputs      | 所有输出流 |
| 格式化输入函数 | fscanf     | 所有输入流 |
| 格式化输出函数 | fprintf    | 所有输出流 |
| 二进制输入     | fread      | 文件       |
| 二进制输出     | fwrite     | 文件       |

==**流**==

>  高度抽象的概念

c语言程序运行,会默认打开3个流: 

- stdin - 标准输入流 - 键盘
- stdout - 标准输出流 - 屏幕
- stderr - 标准错误流 - 屏幕

三个流都是FILE*类型

```
int main()
{
	fputc('h', stdout);
	fputc('h', stdout);
	fputc('h', stdout);
	return 0;
}
//会打印 hhh


//fgetc从标准输入流中读取
int main()
{
	int ret = fgetc(stdin);//手动在键盘输入h, 并被读取
	printf("%c\n", ret);//打印h
	return 0;
}
```

```
//使用fgetc从文件流中读取数据
int main()
{
	FILE* pf = fopen("test.exe", "r");
	if(pf = NULL)
	{
		perror("fopen");//abc
		return 1;
	}
	//读文件
	//每次读取后, 文件指针都会向后偏移一个字节
	int ret = fgetc(pf);
	printf("%c\n", ret);//a
	ret = fgetc(pf);
	printf("%c\n", ret);//b
	ret = fgetc(pf);
	printf("%c\n", ret);//c
	ret = fgetc(pf);
	printf("%c\n", ret);//-1  读取结束或者失败会返回EOF, EOF的ASCII值为-1
	
	fclose(pf);
	pf = NULL;
	return 0;
}
```

```
int main()
{
	FILE* pf = fopen("test.exe", "r");
	if(pf = NULL)
	{
		perror("fopen");
		return 1;
	}
	fputs("abcdefg", pf);
	fclose(pf);
	pf = NULL;
	return 0;
}
//abcdefg被写入文件
```

```
int main()
{
	char a[10] = "xxxxxx";
	FILE* pf = fopen("test.exe", "r");
	if(pf = NULL)
	{
		perror("fopen");//abcdef
		return 1;
	}
	//读文件
	fgets(arr, 4, pf);
	printf("%s\n", arr);//abc fgets中写读取4个,实际上只会读取3个, 因为还要在后面加上'\0'
	//此时arr内为 abc\0xx
	fgets(arr, 4, pf);//继续往后读取
	printf("%s\n", arr);//def
	
	fclose(pf);
	pf = NULL;
	return 0;
}
```

```
struct S
{
	char arr[10];
	int num;
	double sc;
};
int main()
{
	struct S s = {"abcdef", 10, 5.5f};
    FILE*pf = Fopen("test.exe", "w");
    if(pf == NULL)
    {
    	perror("fopen");
    	return 1;
    }
    //写文件
    fprintf(pf, "%s %d %f", s.arr, s.num, s.sc);
    //等价于printf
    fprintf(stdout, "%s %d %f", s.arr, s.num, s.sc);
    fclose(pf);
    pf = NULL;
    return 0;
}
```

```
struct S
{
	char arr[10];
	int num;
	double sc;
};
int main()
{
	struct S s = {0};
    FILE*pf = Fopen("test.exe", "r");//abcdef 10 5.500000
    if(pf == NULL)
    {
    	perror("fopen");
    	return 1;
    }
    //文件
    fscanf(pf, "%s %d %f", s.arr, &(s.num), &(s.sc));
    printf("%s %d %f\n", s.arr, s.num, s.sc);//abcdef 10 5.500000
    //等价于scanf
    fscanf(stdin, "%s %d %f", s.arr, &(s.num), &(s.sc));
    fclose(pf);
    pf = NULL;
    return 0;
}
```

```
struct S
{
	char arr[10];
	int num;
	double sc;
};
int main()
{
	struct S s = {0};
    FILE*pf = Fopen("test.exe", "r");abcdef 10 5.500000
    if(pf == NULL)
    {
    	perror("fopen");
    	return 1;
    }
    //单独用fwrite读出的是二进制内容, 难以读懂, 可配合上fread
    fwrite(&s, sizeof(struct S), 1,pf);
    fread(&s, sizeof(struct S), 1, pf);
    fclose(pf);
    pf = NULL;
    return 0;
}
```

Compare *scanf, fscanf ,sscanf* and *printf, fprintf, sprintf*

参数见MSDN

> scanf: 针对标准输入流的格式化输入语句  stdin
>
> fscanf: 针对所有输入流的格式化输入语句  stdin/文件
>
> sscanf: 从一个字符串中读取一个格式化的数据

> printf: 针对标准输出流的格式化输出语句  stdout
>
> fprintf: 针对所有输出流的格式化输出语句  stdout/文件
>
> sprintf: 把一个格式化的数据转换成字符串

```
#include <stdio.h>
strcut S
{
	char arr[10];
	int age;
	float f;
};
int main()
{
	struct S s = {"hello", 10, 5.5f};
	struct S tmp = {0};
	char buf[100] = {0};
	sprintf(buf, "%s %d %f", s.arr, s.age, s.f);
	printf("%s\n", buf);//hello 10 5.500000
	
	sscanf(buf, "%s %d %f", tmp.arr, &(tmp.age), &(tmp.f));
	printf("%s %d %f\n", tmp.arr, tmp.age, tmp.f);//hello 10 5.500000
	
	return 0;
}
```

###### 文件的随机读写

***fseek***

Moves the file pointer to a specified location.

int fseek( FILE *stream,  long offset, int *origin* );

Remarks: to MSDN

***ftell***

Gets the current position of a file pointer.

long ftell( FILE *stream);

Remarks: to MSDN

***rewind***

Repositions the file pointer to the beginning of a file.

voidrewind(FILEstream*);

Remarks: to MSDN

```
#include <stdio.h>
int main()
{
	FILE* pf = fopen("test.exe", "r");
	if(pf = NULL)
	{
		perror("fopen");//abcdef
		return 1;
	}
	//读文件
	int ch = fgetc(pf);
	printf("%c\n", ch);//a
	//调整文件指针
    fseek(pf, 2, SEEK_CUR);
	//继续读取
	ch = fgetc(pf);
	printf("%c\n", ch);//d
	ch = fgetc(pf);
	printf("%c\n", ch);//e
	
	//获取当前指针相对起始位置的偏移量
	int ret = ftell(pf);
	printf("%d\n",ret);//5
	
	//让文件指针回到起始位置
	rewind(pf);
	ch = fgetc(pf);
	printf("%c\n", ch);//a
	
	fclose(pf);
	pf = NULL;
	return 0;
}
```

###### 文本文件和二进制文件

根据数据的组织形式, 数据文件被称为**文本文件**或者**二进制文件**.

数据在内存中以二进制的形式存储, 如果不加转换地输出到外存, 就是二进制文件.

如果要求在外存上以ASCII码的形式存储, 则需要在存储前转换. 以ASCII字符的形式存储的文件就是文本文件.

数据在文件中, 字符一律以ASCII形式存储, 数值型数据既可以用ASCII形式存储, 也可以用二进制形式存储.

例如整数10000, 如果以ASCII码的形式输出到磁盘, 则磁盘中占5个字节(每个字符一个字节), 而以二进制形式输出, 则在磁盘上只占4个字节

```
//10
//内存中的存储形式(二进制)
//00000000 00000000 00100111 00010000
//转化为ASCII形式
//00110001 00110000 00110000 00110000 00110000
//   (1)      (0)       (0)      (0)     (0)
//二进制形式存储
//00000000 00000000 00100111 00010000
```

###### 文件读取结束的判定

被错误使用的**feof**

>注意: 在文件读取过程中, 不能用feof函数的返回值直接判断文件读取是否结束,而是应用于当文件读取结束时, 判断是读取失败结束还是遇到文件尾结束

判断方法

1. **文本文件**读取是否结束, 判断返回值是否为EOF(fgetc), 或者NULL(fgets)

   例如: fgetc判断是否为EOF; fgets判断返回值是否为NULL

2. **二进制文件**的读取结束判断, 判断返回值是否小于实际要读的数

   例如: fread判断返回值是否小于实际要读的数

```
//复制文件
#include <stdio.h>
int main()
{
	FILE* pfread = fopen("test.exe", "r");
	if(!pfread)
	{
		return 1;
	}
	FILE* pfwrite = fopen("test2.exe", "w");
	if(!pfwrite)
	{
		fclose(pfread);
		pfread = NULL;
		return 1;
	}
	int ret;
	while(ret = fgetc(pfread) != EOF)
	{
		fputc(ret, pfwrite);
	}
	//JUDGE
	if(feof(pfread))
	{
		printf("End of file reached successfully");
	}
	else if(ferror(pfread))
	{
		printf("I/O error when reading");
	}
	
	fclose(pfread);
	fclose(pfwrite);
	pfread = NULL;
	pfwrite = NULL;
	return0;
}
```

```
#include <stdio.h>
int main()
{
	double a[SIZE] = {1., 2., 3., 4., 5.};
	FILE *fp = fopen("test.bin", "wb");//二进制读取
	fwrite(a, sizeof *a, size, fp);//写double数组
	fclose(fp);
	double b[SIZE];
	fp = fopen("test.bin", "rb");
	size_t ret_code = fread(b, size *b, SIZE, fp)//读double数组
	//JUDGE
	if(ret_code == SIZE)
	{
		puts("Array read successfully, contents: ");
		for(int n=0; n < SIZE; ++n)
		putchar('\n');
	}
	else
	{
		//error handling
		if(feof(fp))
		printf("Error reading test.bin: unexpected end of file\n");
		else if(ferror(fp))
		perror("Error reading test.bin");
	}
	fclose(fp);
	fp = NULL;
	return 0;
}
```

###### 文件缓冲区

ANSIC 标准采用"缓冲文件系统"处理的数据文件的, 所谓缓冲文件系统是指系统自动地在内存中为程序

中每一个正在使用的文件开辟一块"**文件缓冲区**". 从内存向磁盘输出数据会先送到内存中的缓冲区, 装

满缓冲区后才一起送到磁盘上. 如果从磁盘向计算机读入数据, 则从磁盘文件中读取数据输入到内存缓

冲区(充满缓冲区), 然后再从缓冲区逐个地将数据送到程序数据区(程序变量等). 缓冲区的大小根

据C编译系统决定的.

<img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20221009163340899.png" alt="image-20221009163340899" style="zoom:67%;" />

```
#include <stdio.h>
#include <windows.h>
//VS2013 WIN10环境测试
int main()
{
 FILE*pf = fopen("test.txt", "w");
 fputs("abcdef", pf);//先将代码放在输出缓冲区
 printf("睡眠10秒-已经写数据了, 打开test.txt文件, 发现文件没有内容\n");
 Sleep(10000);
 printf("刷新缓冲区\n");
 fflush(pf);//刷新缓冲区时, 才将输出缓冲区的数据写到文件（磁盘）
 //注：fflush 在高版本的VS上不能使用了
 printf("再睡眠10秒-此时, 再次打开test.txt文件, 文件有内容了\n");
 Sleep(10000);
 fclose(pf);
 //注: fclose在关闭文件的时候, 也会刷新缓冲区
 pf = NULL;
 return 0;
 }
//可以得出一个结论: 因为有缓冲区的存在, C语言在操作文件的时候, 需要做刷新缓冲区或者在文件操作结束的时候关闭文件, 如果不做, 可能导致读写文件的问题.
```

## 12.程序环境和预处理

#### 程序环境

在ANSIC的任何一种实现中, 存在两个不同的环境

> 第一种是翻译环境, 在这个环境(如VSCode)中源代码被转换为可执行的机器指令
>
> 第二种是执行环境, 它用于实现执行代码

###### **程序翻译环境**

程序编译过程如图

<img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20221010232733697.png" alt="image-20221010232733697" style="zoom: 67%;" />

> - 组成一个程序的每个源文件通过编译过程分别转换成目标代码(object code).
>
> - 每个目标文件由链接器(linker)捆绑在一起, 形成一个单一而完整的可执行程序.
>
> - 链接器同时也会引入标准C函数库中任何被该程序所用到的函数, 而且它可以搜索程序员个人
>
>   的程序库, 将其需要的函数也链接到程序中.

**阶段分析**

<img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20221010233328614.png" alt="image-20221010233328614" style="zoom: 67%;" />

1. **预处理(预编译)** 选项 gcc -E test.c -o test.i, 预处理完成之后就停下来, 预处理之后产生的结果都放在test.i文件中.
   > 完成了头文件的包含#include
   > #define定义的符号和宏的替换
   > 注释删除
   > 文本操作
2. **编译** 选项 gcc -S test.c, 编译完成之后就停下来, 结果保存在test.s中. 
   
   > 把C语言代码转换为汇编代码
   > 语法分析
   > 词法分析
   > 语义分析
   > 符号汇总
3. **汇编** gcc -c test.c, 汇编完成之后就停下来, 结果保存在test.o中(elf格式). 
   
   > 把汇编代码转换成了机器指令(二进制指令)
   > 生成符号表

> VIM学习资料: 
>
> [简明VIM练级攻略](https://coolshell.cn/articles/5426.html)
>
> [给程序员的VIM速查卡](https://coolshell.cn/articles/5479.html)

 4.**链接**

> 把多个目标文件和链接库进行链接的
> 合并段表
> 符号表的合并和重定位

> Book: 程序员的自我修养

###### 程序运行环境

程序执行的过程:

1. 程序先载入内存中. 在有操作系统的环境中这个一般由操作系统完成; 在独立的环境中, 程序的载入必须由手工安排, 也可能是通过可执行代码置入只读内存来完成.
2. 程序的执行开始, 接着调用main函数
3. 开始执行程序代码, 这个时候程序将使用一个运行时堆栈(stack), 存储函数的局部变量和返回地址, 程序同时也可以使用静态(static)内存, 存储于静态内存中的变量在程序的整个执行过程一直保留他们的值.
4.  终止程序. 正常终止main函数; 也有可能是意外终止.

#### 预处理

###### **预定义符号**

```
__FILE__      //进行编译的源文件
__LINE__      //文件当前的行号
__DATE__      //文件被编译的日期
__TIME__      //文件被编译的时间
__STDC__      //如果编译器遵循ANSI C, 其值为1, 否则未定义
//这些预定义符号都是语言内置的
```

```
//例如
printf("file:%s line:%d\n", __FILE__, __LINE__);
```

###### #define

**#define定义标识符**

```
#define name stuff
```

```
#define MAX 1000
#define reg register           //为 register这个关键字，创建一个简短的名字
#define do_forever for(;;)     //用更形象的符号来替换一种实现, 例如此处的无限循环
#define CASE break;case        //在写case语句的时候自动把 break写上
//如果定义的stuff过长, 可以分成几行写, 除了最后一行外, 每行的后面都加一个反斜杠(续行符)
#define DEBUG_PRINT printf("file:%s\tline:%d\t \
                          date:%s\ttime:%s\n", \
                          __FILE__,__LINE__ ,  \
                          __DATE__,__TIME__ )  
```

> 在define定义标识符的时候，不必在最后加上 ;     否则容易导致问题或者语法错误

```
#define MAX 1000;
#define MAX 1000
```

**#define定义宏**

>  \#define 机制包括了一个规定, 允许把参数替换到文本中, 这种实现通常称为宏(macro)或定义宏(define macro)

```
#define name( parament-list ) stuff
//其中的 parament-list 是一个由逗号隔开的符号表, 它们可能出现在stuff中
//注意
//参数列表的左括号必须与name紧邻,如果两者之间有任何空白存在,参数列表就会被解释为stuff的一部分
```

```
#define SQUARE( x ) x * x
int a = 5;
printf("%d\n" ,SQUARE( a + 1) );
//此处容易错误理解为6*6等于36, 其实替换之后是 5+1*5+1, 即为11
//要达到理想效果, 可以改为
#define SQUARE( x ) (x) * (x)

//但是仍然会有问题
#define DOUBLE(x) (x) + (x)
int a = 5;
printf("%d\n" ,10 * DOUBLE(a));
//此处为 10*5+5
//欲打印100, 结果却是55
//可改进
#define DOUBLE( x)   ( ( x ) + ( x ) )
```

> 所以用于对数值表达式进行求值的宏定义都应该用这种方式加上括号, 或者结合实际情况调整, 避免在使用宏时由于参数中, 的操作符或邻近操作符之间不可预料的相互作用.

 **#define** **替换规则**

在程序中扩展#define定义符号和宏时，需要涉及几个步骤。

1. 在调用宏时, 首先对参数进行检查, 看看是否包含任何由#define定义的符号. 如果是, 它们首先被替换.
2. 替换文本随后被插入到程序中原来文本的位置. 对于宏, 参数名被他们的值替换. 
3. 最后, 再次对结果文件进行扫描, 看看它是否包含任何由#define定义的符号. 如果是, 就重复上述处理过程.

注意:

1. 宏参数和#define 定义中可以出现其他#define定义的变量, 但是对于宏, 不能出现递归. 
2. 当预处理器搜索#define定义的符号的时候, 字符串常量的内容并不被搜索. 

 **#和##**

```
//字符串是有自动连接的特点的
//下面打印结果都是hello world
char* p = "hello ""world\n";
printf("hello ", "world\n");
printf("%s", p);
```

```
//只有当字符串作为宏参数的时候才可以把字符串放在字符串中
#define PRINT(FORMAT, VALUE)\
 printf("the value is "FORMAT"\n", VALUE);
...
PRINT("%d", 10);

//使用 # , 把一个宏参数变成对应的字符串
int i = 10;
#define PRINT(FORMAT, VALUE)\
 printf("the value of " #VALUE "is "FORMAT "\n", VALUE);
 ...
PRINT("%d", i+3)//the value of i+3 is 13

//使用##, 可以把位于它两边的符号合成一个符号, 它允许宏定义从分离的文本片段创建标识符
#define ADD_TO_SUM(num, value) \
 sum##num += value;
...
int sum5 = 0;
ADD_TO_SUM(5, 10);//给sum5 增加10
//注意: 这样的连接必须产生一个合法的标识符, 否则其结果就是未定义的
```

**带副作用的宏参数**

当宏参数在宏的定义中出现超过一次的时候, 如果参数带有副作用, 那么你在使用这个宏的时候就可能

出现危险, 导致不可预测的后果. 

**副作用**就是表达式求值的时候出现的永久性效果.

```
x+1;//不带副作用
x++;//带有副作用

#define MAX(a, b) ( (a) > (b) ? (a) : (b) )
...
x = 5;
y = 8;
z = MAX(x++, y++);
printf("x=%d y=%d z=%d\n", x, y, z);
//预处理之后
z = ( (x++) > (y++) ? (x++) : (y++));
x=6 y=10 z=9
```

###### 宏和函数对比

宏通常被应用于执行简单的运算. 

```
//如在两个数中找出较大的一个。
#define MAX(a, b) ((a)>(b)?(a):(b))
```

此处不选择用函数的原因: 

1. 用于调用函数和从函数返回的代码可能比实际执行这个小型计算工作所需要的时间更多, 所以宏比函数在**程序的规模和速度**方面更胜一筹.
2. 更为重要的是函数的参数必须声明为特定的类型. 所以函数只能在类型合适的表达式上使用, 反之

这个宏怎可以适用于整形, 长整型, 浮点型等可以用>来比较的类型. **宏是类型无关的**

当然和宏相比函数也有劣势的地方: 

1. 每次使用宏的时候, 一份宏定义的代码将插入到程序中. 除非宏比较短, 否则可能大幅度增加程序的长度.
2. 宏是没法调试的
3. 宏由于类型无关, 也就不够严谨
4.  宏可能会带来运算符优先级的问题, 导致程容易出现错
5. 宏有时候可以做函数做不到的事情。比如：宏的参数可以出现**类型**，但是函数做不到。

```
#define MALLOC(num, type)\
 (type *)malloc(num * sizeof(type))
...
//使用
MALLOC(10, int);//类型作为参数
//预处理器替换之后：
(int *)malloc(10 * sizeof(int));
```

**对比**

| 属性             | #define定义宏                                                | 函数                                                         |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 代码长度         | 每次使用时，宏代码都会被插入到程序中, 除了非常小的宏之外，程序的长度会大幅度增长 | 函数代码只出现于一个地方；每次使用这个函数时，都调用那个地方的同一份代码 |
| 执行速度         | 更快                                                         | 存在函数的调用和返回的额外开销, 所以相对慢一些               |
| 操作符优先级     | 宏参数的求值宏参数的求值是在所有周围表达式的上下文环境里，除非加上括号，否则邻近操作符的优先级可能会产生不可预料的后果，所以建议宏在书写的时候多些括号 | 函数参数只在函数调用的时候求值一次，它的结果值传递给函数。表达式的求值结果更容易预测 |
| 带有副作用的参数 | 参数可能被替换到宏体中的多个位置，所以带有副作用的参数求值可能会产生不可预料的结果。 | 函数参数只在传参的时候求值一次，结果更容易控制。             |
| 参数类型         | 宏的参数与类型无关，只要对参数的操作是合法的，它就可以使用于任何参数类型。 | 函数的参数是与类型有关的，如果参数的类型不同，就需要不同的函数，即使他们执行的任务是不同的 |
| 调试             | 宏是不方便调试的                                             | 函数是可以逐语句调试的                                       |
| 递归             | 宏是不能递归的                                               | 函数是可以递归的                                             |
|                  |                                                              |                                                              |

**命名约定**

一般来讲函数的宏的使用语法很相似, 所以语言本身没法帮我们区分二者.

一般我们习惯:

>  把宏名全部大写
>
> 函数名不要全部大写

###### #undef

这条指令用于移除一个宏定义.

```
#undef NAME
//如果现存的一个名字需要被重新定义, 那么它的旧名字首先要被移除.
```

###### **命令行定义**

许多C 的编译器提供了一种能力, 允许在命令行中定义符号, 用于启动编译过程.

例如: 当我们根据同一个源文件要编译出不同的一个程序的不同版本的时候, 这个特性有点用处.(假

定某个程序中声明了一个某个长度的数组, 如果机器内存有限, 我们需要一个很小的数组, 但是另外一

个机器内存大写, 我们需要一个数组能够大写)

```
#include <stdio.h>
int main()
{
    int array [ARRAY_SIZE];
    int i = 0;
    for(i = 0; i< ARRAY_SIZE; i ++)
   {
        array[i] = i;
   }
    for(i = 0; i< ARRAY_SIZE; i ++)
   {
        printf("%d " ,array[i]);
   }
    printf("\n" );
    return 0; }
    
//编译指令
gcc -D ARRAY_SIZE=10 programe.c
```

###### **条件编译**

在编译一个程序的时候我们如果要将一条语句(一组语句)编译或者放弃是很方便的, 因为我们有条件编译指令.

```
//例如调试性的代码, 删除可惜, 保留又碍事, 所以我们可以选择性的编译.
#include <stdio.h>
#define __DEBUG__
int main()
{
 	int i = 0;
 	int arr[10] = {0};
 	for(i=0; i<10; i++)
 	{
 	arr[i] = i;
 	#ifdef __DEBUG__
 	printf("%d\n", arr[i]);//为了观察数组是否赋值成功。 
 	#endif //__DEBUG__
 	}
 	return 0; 
}

or
#if 0
...
#endif
```

常见的编译指令:

```
1.条件编译
#if 常量表达式
 //...
#endif
//常量表达式由预处理器求值。
//例如
#define __DEBUG__ 1
#if __DEBUG__
 	//..
#endif

#if 0
...
#enfif


2.多个分支的条件编译
#if 常量表达式
 	//...
#elif 常量表达式
	//...
#else
	//...
#endif
//出现表达式为真, 就会执行, 后面的elif/else不会再判断或执行


3.判断是否被定义
#if defined(symbol)
#ifdef symbol

#if !defined(symbol)
#ifndef symbol


4.嵌套指令
#if defined(OS_UNIX)
    #ifdef OPTION1
        unix_version_option1();
    #endif
    #ifdef OPTION2
        unix_version_option2();
    #endif
#elif defined(OS_MSDOS)
    #ifdef OPTION2
        msdos_version_option2();
    #endif
#endif
```

```
int main()
{
	//在编译器转到定义, 可以看到很多使用编译条件的语句
	EOF;
	return 0;
}
```

###### #include

 #include 指令是文件包含, 可以使另外一个文件被编译, 就像它实际出现于 #include 指令的地方一样.

这种替换的方式很简单:预处理器先删除这条指令, 并用包含文件的内容替换, 这样一个源文件被包含10次, 那就实际被编译10次.

**头文件被包含的方式**

- 本地文件包含

""查找策略: 先在源文件所在目录下查找, 如果该头文件未找到, 编译器就像查找库函数头文件一样在标准位置(即库函数头文件所在目录)查找头文件, 如果找不到就提示编译错误.

```
#include "filename"
```

Linux环境的标准头文件的路径: 

```
/usr/include
```

VS环境的标准头文件的路径:

```
int main()
{
	EOF;
	//右击鼠标转到定义, 再打开所在文件夹, 就会转到头文件所在目录
	//目录所在位置与编译器安装路径有关
}
```

- 库文件包含

```
#include <filename.h>
```

<>查找头文件直接去标准路径下去查找, 如果找不到就提示编译错误. 

> <>和""包含头文件的本质区别就是查找策略不同, 其实库文件也可以使用""包含, 但是这样做查找的效率就低些, 当然这样也不容易区分是库文件还是本地文件了.

**嵌套文件包含**

<img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20221013123825198.png" alt="image-20221013123825198" style="zoom:67%;" />

comm.h和comm.c是公共模块, test1.h和test1.c使用了公共模块, test2.h和test2.c使用了公共模块, test.h和test.c使用了test1模块和test2模块, 这样最终程序中就会出现两份comm.h的内容, 这样就造成了文件内容的重复.

可利用条件编译避免头文件的重复引入

```
#ifndef __TEST_H__
#define __TEST_H__
//头文件的内容
#endif   

//第一次执行第一句, __TEST_H__未被定义, 所以可以继续执行, 但是第二次执行时, 由于在第一次执行的内容中__TEST_H__被定义了, 所以无法执行, 避免了文件内容重复

or
#pragma once
```

注: 《高质量C/C++编程指南》中附录的考试试卷（重要）

```
笔试题中有:
1. 头文件中的 ifndef/define/endif是干什么用的?
2. #include <filename.h> 和 #include "filename.h"有什么区别?
```

###### **其他预处理指令**

```
#error
#pragma
#line
...
//参考《C语言深度解剖》进行了解学习
```


# 随记

- 压栈

涉及到关于“压栈”问题
栈是一种数据结构，是一种只能在一端进行插入和删除操作的特殊线性表。它按照先进后出的原则存储数据，先进入的数据被压入栈底，最后的数据在栈顶，需要读数据的时候从栈顶开始弹出数据（最后放入的数据被最先读出来）

栈帧：C语言中，每个栈帧对应着一个未运行完的函数；栈帧中保存了该函数的返回地址和局部变量

内存分区：内存中主要分为栈区，堆区，静态区，以及其他部分

​	栈区：由高地址往低地址增长，主要用来存放局部变量，函数调用开辟的空间，与堆共享一段空间

​	堆区：由低地址向高地址增长，动态开辟的空间就在这里（malloc，realloc，calloc，free），与栈共享一	段空间

​	静态区：主要存放全局变量和静态变量

栈帧创建与销毁
此处还需注意内存空间的栈和数据结构的栈是不同的，内存空间是真实存在的物理区，而数据结构的栈可以理解为是数据存储结构

数组随着下标的增长地址由低到高变化，栈区内存的使用习惯是由高到低

- 打印指定长度字符串

```
printf("%20s\t%5s\t%10s\t%10s","abc", "bcd", "cde", "def");
//%20s 打印20个字符, 如果不够则用空格填充
//\t   前后打印的数据之间有空白, 较美观
//默认是右对齐, 若要左对齐, 则在数字前加'-', 如"%-20s"
```

- 流

高度抽象的概念

c语言程序运行,会默认打开3个流: 

​	stdin - 标准输入流 - 键盘

​	stdout - 标准输出流 - 屏幕

​	stderr - 标准错误流 - 屏幕

三个流都是FILE*类型

```
int main()
{
	fputc('h', stdout);
	fputc('h', stdout);
	fputc('h', stdout);
	return 0;
}
//会打印 hhh
```

- 判断某个数在n进制表示方式下有几位
  最简方法: 如(15, 2), 先15%2, 得到的就是2^0^的n倍, 同时可以舍去, 并留下15/2, 而7已经是14除以2的结果, 即2^1^; 然后7/2, 得到的就是2^2^, 以此类推, 可得到二进制数. 

```c
int Cal(int x, int base)
{
    int res = 0;
    for(; x; x /= base)
        res += x % base;
    return res;
}
```

