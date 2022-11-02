## Note

#### 第一章 预备知识

简介

C++融合了3重不同的编程方式: C语言代表的过程性语言, C++在C语言基础上添加的类代表的面向对象(Object Oriented Programming，OOP)语言, C++模板支持的泛型编程.

C语言: 结构化编程和过程性编程

面向对象编程

C++中, 类是一种规范, 它描述了这种新型数据格式,对象是根据这种规范构造的特定数据结构. 

C++和泛型编程

[Bjarne Stroustrup 的主页](http://www.research.att.com/-bs/)

#### 第二章 开始学习C++

#### 第三章 处理数据

使用头文件climits查看类型限制信息

```c++
#include <iostream>
#include <climits>
using namespace std;

int main()
{
    int n_int = INT_MAX;
    short n_short = SHRT_MAX;
    long n_long = LONG_MAX;
    long long n_llong = LLONG_MAX;
    
    cout << "int is " << sizeof(int) << " bytes." << endl;
    cout << "short is " << sizeof n_short << " bytes." << endl;
    cout << "long is " << sizeof n_long << " bytes." << endl;
    cout << "long long is " << sizeof n_llong << " bytes." << endl;
    cout << endl;

    cout << "Maximum values:" << endl;
    cout << "int: " << n_int << endl;
    cout << "short: " << n_short << endl;
    cout << "long: " << n_long << endl;
    cout << "long long is: " << n_llong << endl << endl;

    cout << "Minimum int value = " << INT_MIN << endl;
    cout <<"Bits per byte = " << CHAR_BIT << endl;

    return 0;
}

//输出结果

int is 4 bytes.
short is 2 bytes.
long is 4 bytes.
long long is 8 bytes.

Maximum values:
int: 2147483647
short: 32767
long: 2147483647
long long is: 9223372036854775807

Minimum int value = -2147483648
Bits per byte = 8
```



















[sort](https://cplusplus.com/reference/algorithm/sort/)

