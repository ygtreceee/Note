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

















#### sort

```c++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
bool myfunction(int i, int j)
{
    return i < j;
}
struct myclass
{
    bool operator() (int i, int j)
    {
        return i < j;
    }
}myobject;
int main()
{
    int myints[] = {32, 71, 12, 45, 26, 80, 53, 33};
    vector<int> myvector(myints, myints + 8);                // 32 71 12 45 26 80 53 33
     
    // using default comparison (operator <):
    sort(myvector.begin(), myvector.begin() + 4);           //(12 32 45 71)26 80 53 33

    // using function as comp
    sort(myvector.begin() + 4, myvector.end(), myfunction); // 12 32 45 71(26 33 53 80) 

    // using object as comp
    sort(myvector.begin(), myvector.end(), myobject);       //(12 26 32 33 45 53 71 80)

    // print out content
    cout << "myvector contains";
    for (vector<int>::iterator it = myvector.begin(); it != myvector.end(); it++)
        cout << ' ' << *it;
    cout << endl;

    return 0;
}
```



#### stable_sort

```c++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
// bool compare_as_ints(double i, double j)
// {
//     return int(i) < int(j);
// }
struct myclass
{
    bool operator()(double i, double j)
    {
        return int(i) < int(j);
    }
}myobject;
int main()
{
    double mydoubles[] = {3.14, 1.41, 2.72, 4.67, 1.73, 1.32, 1.62, 2.58};
    
    vector<double> myvector;

    myvector.assign(mydoubles, mydoubles + 8);

    cout << "using default comparison:";
    stable_sort(myvector.begin(), myvector.end());
    for (vector<double>::iterator it = myvector.begin(); it != myvector.end(); it++)
        cout << ' ' << *it;
    cout << endl;

    myvector.assign(mydoubles, mydoubles + 8);

    cout << "using 'compare_as_ints' :";
    // stable_sort(myvector.begin(), myvector.end(), compare_as_ints);
    stable_sort(myvector.begin(), myvector.end(), myobject);
    for (vector<double>::iterator it = myvector.begin(); it != myvector.end(); it++)
        cout << ' ' << *it;
    cout << endl;

    return 0;
}
```



#### priority_queue

```c++
#include <iostream>
#include <vector>
#include <stack>
#include <queue>
using namespace std;

//基本类型例子：

int main()
{
    priority_queue<int, vector<int>, greater<int>> que;
    //priority_queue<int, vector<int>, less<int>> que;
    //priority_queue<int> que;
    int a = 2, b = 1, c = 3;
    que.push(a);
    que.push(b);
    que.push(c);
    while (!que.empty())
    {
        cout << que.top() << endl;
        que.pop();
    }
    return 0;
}

//pari的比较，先比较第一个元素，第一个相等比较第二个

int main()
{
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> que;
    //priority_queue<pair<int, int>> que;
    pair<int, int> b(1, 2);
    pair<int, int> c(1, 2);
    pair<int, int> d(2, 5);
    que.push(b);
    que.push(c);
    que.push(d);
    while (!que.empty())
    {
        cout << que.top().first << " " << que.top().second << endl;
        que.pop();
    }
    return 0;
}

//对于自定义类型
struct tmp1 //运算符重载
{
    int x;
    tmp1(int a) {x = a;}
    bool operator<(const tmp1& a) const
    {
        return x < a.x;//大顶堆

    }
};

struct tmp2 //重写仿函数
{
    bool operator() (tmp1 a, tmp1 b)
    {
        return a.x < b.x;//大顶堆
    }
};
int main()
{
    tmp1 a(1);
    tmp1 b(2);
    tmp1 c(3);
    priority_queue<tmp1> que;
    que.push(a);
    que.push(b);
    que.push(c);
    while (!que.empty())
    {
        cout << que.top().x << endl;
        que.pop();
    }

    priority_queue<tmp1, vector<tmp1>, tmp2> quee;
    quee.push(a);
    quee.push(b);
    quee.push(c);
    while (!quee.empty())
    {
        cout << quee.top().x << endl;
        quee.pop();
    }
    return 0;
}
```



#### string

构造函数的形式

```c++
string str;                      //生成空字符串

string s(str);                   //生成字符串为str的复制品

string s(str, strbegin, strlen); //将字符串str中从下标strbegin开始, 长度为strlen的部分作为字符串初值

string s(str, strbegin);         //将字符串str从下标strbegin开始到字符串结束的位置作为字符串初值

string s(cstr, char_len);        //以C_string类型cstr的前char_len个字符串作为字符串s的初值

string s(num, c);                //生成num个c字符的字符串(字符c用单引号包括)



string str1;                   //生成空字符串
string str2("123456789");      //生成"1234456789"的复制品
string str3("123456789", 0, 3);//结果为"123"
string str4(str2, 0, 3);       //结果为"123"
string str5("012345", 2);      //结果为"01"
string str6(str2, 2);      	   //结果为"3456789"
string str7(5, '1');           //结果为"11111"
```

大小和容量

```c++
string str = "hello";

str.size(); 
str.length();   //都返回string对象的字符个数, 执行效果相同

str.max_size(); //返回string对象最多包含的字符数, 超出会抛出length_error异常

str.capacity(); //重新分配内存之前, string对象能包含的最大字符数


void test()
{
    string s("1234567"); 
    cout << "size=" << s.size() << endl;         //size=7
    cout << "length=" << s.length() << endl;     //length=7
    cout << "max_size=" << s.max_size() << endl; //max_size=9223372036854775807
    cout << "capacity=" << s.capacity() << endl; //capacity=15
}
```

字符串比较

```
1. C++字符串支持常见的比较操作符（>,>=,<,<=,==,!=），甚至支持string与C-string的比较(如 str<”hello”)。在使用>,>=,<,<=这些操作符的时候是根据“当前字符特性”将字符按字典顺序进行逐一比较。字典排序靠前的字符小，比较的顺序是从前向后比较，遇到不相等的字符就按这个位置上的两个字符的比较结果确定两个字符串的大小(前面减后面)
同时，string (“aaaa”) <string(aaaaa)

2. 另一个功能强大的比较函数是成员函数compare()。他支持多参数处理，支持用索引值和长度定位子串来进行比较。他返回一个整数来表示比较结果，返回值意义如下：0：相等 1：大于 -1：小于 (A的ASCII码是65，a的ASCII码是97)
```

```c++
void test()
{
    // (A的ASCII码是65，a的ASCII码是97)
    // 前面减去后面的ASCII码，>0返回1，<0返回-1，相同返回0
    string A("aBcd");
    string B("Abcd");
    string C("123456");
    string D("123dfg");

    // "aBcd" 和 "Abcd"比较------ a > A
    cout << "A.compare(B): " << A.compare(B) << endl;                       //1

    // "cd" 和 "Abcd"比较------- c > A
    cout << "A.compare(2, 3, B): " << A.compare(2, 3, B) << endl;           //1

    // "cd" 和 "cd"比较 
    cout << "A.compare(2, 3, B, 2, 3): " << A.compare(2, 3, B, 2, 3) << endl;//0

    // 由结果看出来：0表示下标，3表示长度
    // "123" 和 "123"比较 
    cout << "C.compare(0, 3, D, 0, 3)" << C.compare(0, 3, D, 0, 3) << endl;  //0
}
```

插入 push_back() 和 insert()

```c++
void  test4()
{
    string s1;

    // 尾插一个字符
    s1.push_back('a');
    s1.push_back('b');
    s1.push_back('c');
    cout<<"s1:"<<s1<<endl; // s1:abc

    // insert(pos,char):在制定的位置pos前插入字符char
    s1.insert(s1.begin(),'1');
    cout<<"s1:"<<s1<<endl; // s1:1abc
}
```

字符串拼接 append() & + 操作符

```c++
void test()
{
    // 方法一: append()   注意括号内必须是字符串
    string str1("hello");
    string str2(" world");
    str1.append(str2);
    str1.append("!");
    cout << "str1: " << str1 << endl; //hello world!
    
    //方法二:  + 操作符   注意加的可以是字符也可以是字符串
    string str3("how");
    string str4(" are you");
    str3 += str4;
    str3 += '!';
    str3 += "!";
    cout << "str3: " << str3 << endl; //how are you!!
}
```

借助迭代器或者下标法进行遍历

```c++
void test()
{
    string str("hello");
	
    //方法一: 下标法
    for (int i = 0; i < str.size(); i++)
        cout << str[i] << ' ';    //h e l l o 
    cout << endl;
	
    //方法二: 正向迭代器
    for (string::iterator it = str.begin(); it != str.end(); it++)
        cout << *it << ' ';       //h e l l o 
    cout << endl;
	
    //方法三: 反向迭代器
    for (string::reverse_iterator rit = str.rbegin(); rit != str.rend(); rit++)
        cout << *rit << ' ';      //o l l e h
    cout << endl;
}
```

删除 erase()

```
1. iterator erase(iterator p);//删除字符串中p所指的字符

2. iterator erase(iterator first, iterator last);//删除字符串中迭代器区间[first,last)上所有字符

3. string& erase(size_t pos = 0, size_t len = npos);//删除字符串中从索引位置pos开始的len个字符

4. void clear();//删除字符串中所有字符
```

```c++
void test()
{
    string s1 = "123456789";
	
    //迭代器删除法
    s1.erase(s1.begin()+1);              // 结果：13456789
    s1.erase(s1.begin()+1,s1.end()-2);   // 结果：189
    
    
    //下标删除法
    string s2 = "123456789";
    s2.erase(1,6);                       // 结果：189
    string::iterator it = s1.begin();
    while (it != s2.end())
    {
        cout << *it;
        *it++;
    }
    cout << endl;
}
```

字符替换

```
1. string& replace(size_t pos, size_t n, const char *s);//将当前字符串
从pos索引开始的n个字符，替换成字符串s

2. string& replace(size_t pos, size_t n, size_t n1, char c); //将当前字符串从pos索引开始的n个字符，替换成n1个字符c

3. string& replace(iterator i1, iterator i2, const char* s);//将当前字符串[i1,i2)区间中的字符串替换为字符串s
```

```c++
void test()
{
    string s1("hello,world!");

    cout<<s1.size()<<endl;                     // 结果：12
    s1.replace(s1.size()-1,1,1,'.');           // 结果：hello,world.

    // 这里的6表示下标  5表示长度
    s1.replace(6,5,"girl");                    // 结果：hello,girl.
    // s1.begin(),s1.begin()+5 是左闭右开区间
    s1.replace(s1.begin(),s1.begin()+5,"boy"); // 结果：boy,girl.
    cout<<s1<<endl;
}
```

string的大小写转换：tolower()和toupper()函数 或者 STL中的transform算法

```c++
//方法一：使用C语言之前的方法，使用函数，进行转换
#include <iostream>
#include <string>
using namespace std;
int main()
{
    string s = "ABCDEFG";

    for( int i = 0; i < s.size(); i++ )
    {
        s[i] = tolower(s[i]);
    }
    cout<<s<<endl;
    return 0;
}
```

```c++
//方法二：通过STL的transform算法配合的toupper和tolower来实现该功能
#include <iostream>
#include <algorithm>
#include <string>
using namespace std;
int main()
{
    string s1 = "ABCDEFG";
    string s2 = "abcdefg";
    transform(s1.begin(), s1.end(), s1.begin(), ::tolower);
    transform(s2.begin(), s2.end(), s2.begin(), ::toupper);
    
    string s3 = "ABC";
    string result = "EFG";
    transform(s3.begin(), s3.end(), result.begin(), ::tolower); //注意如果要把结果存到另一个string,另一个string类变量必须至少有相应的大小, 比如如果result为"E", 那只能存入"a", 打印出来也是a
    cout << s1 << endl;  //abcdefg
    cout << s2 << endl;  //ABCDEFG
    for (string::iterator it = result.begin(); it != result.end(); it++)
        cout << *it;     //abc
    return 0;
}
```

string的查找：find

```
1. size_t find (constchar* s, size_t pos = 0) const;
//在当前字符串的pos索引位置开始，查找子串s，返回找到的位置索引，-1表示查找不到子串

2. size_t find (charc, size_t pos = 0) const;
//在当前字符串的pos索引位置开始，查找字符c，返回找到的位置索引，-1表示查找不到字符

3. size_t rfind (constchar* s, size_t pos = npos) const;
//在当前字符串的pos索引位置开始，反向查找子串s，返回找到的位置索引，-1表示查找不到子串

4. size_t rfind (charc, size_t pos = npos) const;
//在当前字符串的pos索引位置开始，反向查找字符c，返回找到的位置索引，-1表示查找不到字符

5. size_tfind_first_of (const char* s, size_t pos = 0) const;
//在当前字符串的pos索引位置开始，查找子串s的字符，返回找到的位置索引，-1表示查找不到字符

6. size_tfind_first_not_of (const char* s, size_t pos = 0) const;
//在当前字符串的pos索引位置开始，查找第一个不位于子串s的字符，返回找到的位置索引，-1表示查找不到字符

7. size_t find_last_of(const char* s, size_t pos = npos) const;
//在当前字符串的pos索引位置开始，查找最后一个位于子串s的字符，返回找到的位置索引，-1表示查找不到字符

8. size_tfind_last_not_of (const char* s, size_t pos = npos) const;
//在当前字符串的pos索引位置开始，查找最后一个不位于子串s的字符，返回找到的位置索引，-1表示查找不到子串
```

```c++
void test()
{
    string s("dog bird chicken bird cat");

    //字符串查找-----找到后返回首字母在字符串中的下标

    // 1. 查找一个字符串
    cout << s.find("chicken") << endl;        // 结果是：9

    // 2. 从下标为6开始找字符'i'，返回找到的第一个i的下标
    cout << s.find('i',6) << endl;            // 结果是：11

    // 3. 从字符串的末尾开始查找字符串，返回的还是首字母在字符串中的下标
    cout << s.rfind("chicken") << endl;       // 结果是：9

    // 4. 从字符串的末尾开始查找字符
    cout << s.rfind('i') << endl;             // 结果是：18-------因为是从末尾开始查找，所以返回第一次找到的字符

    // 5. 在该字符串中查找第一个属于字符串s的字符
    cout << s.find_first_of("13br98") << endl;  // 结果是：4---b

    // 6. 在该字符串中查找第一个不属于字符串s的字符------先匹配dog，然后bird匹配不到，所以打印4
    cout << s.find_first_not_of("hello dog 2006") << endl; // 结果是：4
    cout << s.find_first_not_of("dog bird 2006") << endl;  // 结果是：9

    // 7. 在该字符串最后中查找第一个属于字符串s的字符
    cout << s.find_last_of("13r98") << endl;               // 结果是：19

    // 8. 在该字符串最后中查找第一个不属于字符串s的字符------先匹配t--a---c，然后空格匹配不到，所以打印21
    cout << s.find_last_not_of("teac") << endl;            // 结果是：21

}
```

string的排序 sort()

```c++
#include <iostream>
#include <algorithm>
#include <string>
using namespace std;
void test9()
{
    string s = "cdefba";
    sort(s.begin(),s.end());
    cout<<"s:"<<s<<endl;     // 结果：abcdef
}
```

string的分割/截取字符串：strtok() & substr()

```c++
// strtok()分割字符串
#include <iostream>
#include <cstring> //使用strtok要包含的头文件
using namespace std;
int main()
{
    char str[] = "I,Love,You.But,I,Love,Myself,Too!";
    
    const char *split = ",;.!";
    //or
    //const char split[] = ",;.!";
    char *p = strtok(str, split); //strtok只能截取字符数组, 不能截取string类型
    
    //or
    //char *p = strtok(str, ",;.!");
    
    while (p != NULL) 
    {
        cout << p << endl;
        p = strtok(NULL, split);
    }
    //I Love You But I Love Myself Too 
}


// substr()截取字符串
void test11()
{
    string s1("0123456789");
    string s2 = s1.substr(2, 5); // 结果：23456-----参数5表示：截取的字符串的长度
    cout << s2 << endl;
}
```

