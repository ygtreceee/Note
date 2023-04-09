## Note

#### climits

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

#### cin

```
cin可以连续从键盘读取想要的数据，以空格、tab或换行作为分隔符

注意:
1. cin>>等价于cin.operator>>()，即调用成员函数operator>>()进行读取数据
2. 当cin>>从缓冲区中读取数据时，若缓冲区中第一个字符是空格、tab或换行这些分隔符时，cin>>会将其忽略并清除，继续读取下一个字符，若缓冲区为空，则继续等待。但是如果读取成功，字符后面的分隔符是残留在缓冲区的，cin>>不做处理。
3. 不想略过空白字符，那就使用 noskipws 流控制。比如cin>>noskipws>>input;
4. cin>>对缓冲区中的第一个换行符视而不见，采取的措施是忽略清除，继续阻塞等待缓冲区有效数据的到来。但是，getline()读取数据时，并非像cin>>那样忽略第一个换行符，getline()发现cin的缓冲区中有一个残留的换行符，不阻塞请求键盘输入，直接读取，送入目标字符串后，再将换行符替换为空字符’\0’
```

```c++
Cin.get()

读取一个字符
可以使用cin.get或者cin.get(var)
//
char a;
char b;
a=cin.get();
cin.get(b);
cout<<a<<b<<endl;

注意: 
1，cin.get()从输入缓冲区读取单个字符时不忽略分隔符，直接将其读取
2.cin.get()的返回值是int类型，成功：读取字符的ASCII码值，遇到文件结束符时，返回EOF，即-1，Windows下标准输入输入文件结束符为Ctrl+z，Linux为Ctrl+d。cin.get(char var)如果成功返回的是cin对象，因此可以支持链式操作，如cin.get(b).get(c)。


读取一行
可以使用istream& get(char* s, streamsize n)或者istream& get(char* s, size_t n, streamsize delim) ,二者的区别是前者默认以换行符结束，后者可指定结束符。n表示目标空间的大小
//
char a;
char array[20]={NULL}; 
cin.get(array,20);
cin.get(a);

注意：
1. cin.get(char* s, streamsize n);读取一行时，遇到换行符时结束读取，但是不对换行符进行处理，换行符仍然残留在输入缓冲区。第二次可由cin.get()将换行符读入，打印输入换行符的ASCII码值为10。这也是cin.get()读取一行与使用getline读取一行的区别所在. getline读取一行字符时，默认遇到’\n’时终止，并且将’\n’直接从输入缓冲区中删除掉，不会影响下面的输入处理。
（2）cin.get(str,size);读取一行时，只能将字符串读入C风格的字符串中，即char*，但是C++的getline函数可以将字符串读入C++风格的字符串中，即string类型。鉴于getline较cin.get()的这两种优点，建议使用getline进行行的读取。关于getline的用法，下文将进行详述。
    
    

    
cin.getline()
从标准输入设备键盘读取一串字符串，并以指定的结束符结束

函数原型: 
istream& getline(char* s, streamsize count); //默认以换行符结束
istream& getline(char* s, streamsize count, char delim);

//
char array[20]={NULL};
cin.getline(array,20); //或者指定结束符，使用下面一行
//cin.getline(array,20,'\n');
cout<<array<<endl;

注意，cin.getline与cin.get的区别是，cin.getline不会将结束符或者换行符残留在输入缓冲区中
```

```c++
getline()
    
C++中定义了一个在std名字空间的全局函数getline，因为这个getline函数的参数使用了string字符串，所以声明在了< string>头文件中。
getline利用cin可以从标准输入设备键盘读取一行，当遇到如下三种情况会结束读操作：1）到文件结束，2）遇到函数的定界符，3）输入达到最大限度。

函数原型有两种重载形式: 
istream& getline ( istream& is, string& str);//默认以换行符结束
istream& getline ( istream& is, string& str, char delim);

//
string str;
getline(cin,str);

注意，getline遇到结束符时，会将结束符一并读入指定的string中，再将结束符替换为空字符。因此，进行从键盘读取一行字符时，建议使用getline，较为安全。但是，最好还是要进行标准输入的安全检查，提高程序容错能力。
该函数与cin.getline()类似，但是cin.getline()属于istream流，而getline()属于string流，是不一样的两个函数
```

```c++
gets

gets是C中的库函数，在< stdio.h>申明，从标准输入设备读字符串，可以无限读取，不会判断上限，以回车结束或者EOF时停止读取，所以程序员应该确保buffer的空间足够大，以便在执行读操作时不发生溢出。

函数原型:
char *gets( char *buffer );

//
char array[20]={NULL};
gets(array);
cout<<array<<endl;

注意: 该函数是C的库函数，所以不建议使用，既然是C++程序，就尽量使用C++的库函数
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
    priority_queue<int, vector<int>, greater<int>> que;   //1 2 3
    //priority_queue<int, vector<int>, less<int>> que;    //3 2 1
    //priority_queue<int> que;                            //3 2 1
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
    pair<int, int> c(1, 3);
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
//1 2
//1 3
//2 5

//对于自定义类型
struct tmp1 //运算符重载
{
    int x;
    tmp1(int a) {x = a;}
    bool operator<(const tmp1 &a) const
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
    while (!que.empty())       //3 2 1
    {
        cout << que.top().x << endl;
        que.pop();
    }

    priority_queue<tmp1, vector<tmp1>, tmp2> quee;
    quee.push(a);
    quee.push(b);
    quee.push(c);
    while (!quee.empty())    //3 2 1
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

```c++
//常用
//find可以查找字符串，并返回第一个下标，而如果查找不到，string::find会返回string::npos，所以可以用!= 来判断能否找到
if (ret.find(name) != ret.npos) 
    action；

//
#include <iostream>
#include <string>
int main()
{
    string str("hello");
    if (str.find("he") != str.npos)
        cout << "hh"; //hh
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

#### set

```
关于set，必须说明的是set关联式容器。set作为一个容器也是用来存储同一数据类型的数据类型，并且能从一个数据集合中取出数据，在set中每个元素的值都唯一，而且系统能根据元素的值自动进行排序。应该注意的是set中数元素的值不能直接被改变。C++ STL中标准关联容器set, multiset, map, multimap内部采用的就是一种非常高效的平衡检索二叉树：红黑树，也成为RB树(Red-Black Tree)。RB树的统计性能要好于一般平衡二叉树，所以被STL选择作为了关联容器的内部结构
注意：
1. set中的元素都是排好序的
2. set集合中没有重复的元素
3. map和set的插入删除效率比用其他序列容器高
4. 每次insert之后，以前保存的iterator不会失效
5. 当数据元素增多时，set的插入和搜索速度仍为log2数量级，速度极快，搜索耗时短
```

基础关键字

```
begin()       返回set容器第一个元素的迭代器
end() 　      返回一个指向当前set末尾元素的下一位置的迭代器.
clear()       删除set容器中的所有的元素
empty() 　    判断set容器是否为空
max_size() 　 返回set容器可能包含的元素最大个数
size() 　　　 返回当前set容器中的元素个数
rbegin()　　  返回的值和end()相同
rend()　　　　返回的值和begin()相同
```

```c++
#include <iostream>
#include <algorithm>
#include <set>
using namespace std;
int main()
{
	set<int> s;
	s.insert(1);
	s.insert(2);
	s.insert(3);
	s.insert(4);
	cout << "size = " << s.size() << endl;
	cout << "maxsize = " << s.max_size() << endl;
	cout << "begin = " << *s.begin() << endl; //注意需要对迭代器解引用才能得到对应值
	cout << "end = " << *s.end() << endl;
	s.clear();
	if (s.empty()) cout << "set is empty!" << endl;
	cout << "size = " << s.size() << endl;
	return 0;
}
```

迭代遍历

```
注意begin() 和 end()函数是不检查set是否为空的，使用前最好使用empty()检验一下set是否为空
同时注意，set会自动排序
```

```c++
#include <iostream>
#include <algorithm>
#include <set>
using namespace std;
int main()
{
	set<int> s;
	s.insert(3);
	s.insert(1);
	s.insert(2);
	s.insert(4);
	for (set<int>::iterator it = s.begin(); it != s.end(); it++)
		cout << *it << endl;
	return 0;
}
```

**count()**

```
count() 用来查找set中某个某个键值出现的次数。这个函数在set并不是很实用，因为一个键值在set只可能出现0或1次，这样就变成了判断某一键值是否在set出现过了
```

```c++
#include <iostream>
#include <algorithm>
#include <set>
using namespace std;
int main()
{
	set<int> s;
	s.insert(1);
	if (s.count(1)) cout << "1 is being";
	else cout << "1 is not in this set";
	cout << endl;
	if (s.count(2)) cout << "2 is being";
	else cout << "2 is not in this set";
	return 0;
}

```

**equal_range()** 

```
返回一对定位器，分别表示第一个大于或等于给定关键值的元素和 第一个大于给定关键值的元素，这个返回值是一个pair类型，如果这一对定位器中哪个返回失败，就会等于end()的值
```

```c++
#include <iostream>
#include <set>
using namespace std;
int main(){
     set<int> s;
     set<int>::iterator iter;
     for(int i = 1 ; i <= 5; ++i)
         s.insert(i);
     for(iter = s.begin() ; iter != s.end() ; ++iter)
         cout<<*iter<<" ";
     cout<<endl;
     pair<set<int>::const_iterator,set<int>::const_iterator> pr;
     pr = s.equal_range(3);
     cout<<"第一个大于等于 3 的数是 ："<<*pr.first<<endl;
     cout<<"第一个大于 3的数是 ： "<<*pr.second<<endl;
     return 0;
}
```

**erase(iterator)**

**erase(first,second)**

**erase(key_value)**

```
set中的删除操作是不进行任何的错误检查的，比如定位器的是否合法等等，所以用的时候自己一定要注意
```

```
erase(iterator)      删除定位器iterator指向的值

erase(first,second)  删除定位器first和second之间的值

erase(key_value)     删除键值key_value的值
```

```c++
#include <iostream>
#include <set>
using namespace std;
int main(){
     set<int> s;
     set<int>::const_iterator iter;
     set<int>::iterator first;
     set<int>::iterator second;
     for(int i = 1 ; i <= 10 ; ++i) s.insert(i);
    
     //第一种删除
     s.erase(s.begin());       //2 3 4 5 6 7 8 9 10
    
     //第二种删除
     first = s.begin();
     second = s.begin();
     second++;
     second++;
    
     s.erase(first,second);    //4 5 6 7 8 9 10
    
     //第三种删除
     s.erase(8);               //4 5 6 7 9 10
    
     for(iter = s.begin() ; iter != s.end() ; ++iter) cout<<*iter<<" ";
     cout<<endl;
     return 0;
}
```

**find()** 

```
返回给定值值得定位器，如果没找到则返回end()
```

```c++
#include <iostream>
#include <set>
using namespace std;
int main()
{
     int a[] = {1,2,3};
     set<int> s(a,a+3);
     set<int>::iterator iter;
     if((iter = s.find(2)) != s.end())
         cout<<*iter<<endl;    //2
     return 0;
}
```

**insert(key_value)**

**inset(first,second)**

```
insert(key_value)  将key_value插入到set中 ，返回值是pair<set<int>::iterator,bool>，bool标志着插入是否成功，而iterator代表插入的位置，若key_value已经在set中，则iterator表示的key_value在set中的位置。

inset(first,second)  将定位器first到second之间的元素插入到set中，返回值是void.
```

```c++
#include <iostream>
#include <set>
using namespace std;
int main()
{
     int a[] = {1,2,3};
     set<int> s;
     set<int>::iterator iter;
     s.insert(a,a+3);
     for(iter = s.begin() ; iter != s.end() ; ++iter) cout<<*iter<<" ";
     cout<<endl;
     pair<set<int>::iterator,bool> pr;
     pr = s.insert(5);
     if(pr.second)
         cout<<*pr.first<<endl;
     return 0;
}

//1 2 3 
//5
```

#### lower_bound(key_value)

**upper_bound(key_value)**

```
lower_bound(key_value)  返回第一个大于等于key_value的定位器

upper_bound(key_value)  返回最后一个大于等于key_value的定位器
```

```c++
#include <iostream>
#include <set>
using namespace std;
int main()
{
     set<int> s;
     s.insert(1);
     s.insert(3);
     s.insert(4);
     cout<<*s.lower_bound(2)<<endl;
     cout<<*s.lower_bound(3)<<endl;
     cout<<*s.upper_bound(3)<<endl;
     return 0;
}

//3
//3
//4
```

自定义比较函数

```c++
//元素不是结构体：自定义比较函数myComp,重载“（）”操作符

struct myComp  
{  
    bool operator()(const your_type &a, const your_type &b)  
        return a.data - b.data > 0;  
}  
set<int, myComp> s;  
......  
set<int, myComp>::iterator it;  


//如果元素是结构体，可以直接将比较函数写在结构体内

struct Info
{  
    string name;  
    float score;  
    //重载“<”操作符，自定义排序规则  
    bool operator<(const Info &a) const
        return a.score < score;  //按score从大到小排列
}  
set<Info> s;  
......  
set<Info>::iterator it;  
```



lower_bound()    upper_bound()

```
lower_bound(查找的起始位置，查找的终止为止，需要查找的数)是返回第一个大于等于需要查找的数的数的地址
比如，要a[]数组中，从[1,n]中第一个大于s的数的下标
pos = lower_bound(a+1,a+n+1,s)-a;
upper_bound(查找的起始位置，查找的终止为止，需要查找的数 )是返回第一个大于需要查找的数的数的地址
注意上面的两种用法都需要原数组是小到大排列的有序数组(但是貌似无序也可)

可以通过修改比较器，查找第一个小于或小于等于某个数的地址
数组需要从大到小排列
首先需要比较函数
bool cmp(const int &a,const int &b){return a>b;}
比如，要a[]数组中，从[1,n]中第一个小于s的数的下标
pos = lower_bound(a+1,a+n+1,s，cmp)-a;
也可以不写cmp函数，将所有cmp的位置换成greater<int>()

这两种函数如果差找不到目标，就返回查找的最后一个元素的地址
```

```c++
//函数采用二分查找
//所需头文件为<algorithm>
#include <iostream>
#include <algorithm>
using namespace std;
bool cmp(const int a, const int b)
{
    return a > b;
}
int main()
{
    int a[] = {1, 5, 9, 11, 45, 69, 101};
    cout << "a[] = ";
    for (int i = 0; i < 7; i++) cout << a[i] << ' ';
    cout << endl;
    int p1 = lower_bound(a, a + 7, 9) - a;
    cout << "数组中第一个大于等于9的数的下标为 " << p1 << endl;
    int p2 = upper_bound(a, a + 7, 9) - a;
    cout << "数组中第一个大于9的数的下标为 " << p2 << endl;
    sort(a, a + 7, cmp);
    cout << "数组为 ";
    for (int i = 0; i < 7; i++) cout << a[i] << ' ';
    cout << endl;
    int p3 = lower_bound(a, a + 7, 9, cmp) - a;
    cout << "数组中第一个小于等于9的数的下标为 " << p3 << endl;
    int p4 = upper_bound(a, a + 7, 9, greater<int>()) - a;
    cout << "数组中第一个小于9的数的下标为 " << p4 << endl;

    return 0;
}
```

#### unique

```
1.unique函数的去重过程实际上就是不停的把后面不重复的元素移到前面来，也可以说是用不重复的元素占领重复元素的位置
2.unique函数通常和erase函数一起使用，来达到删除重复元素的目的。(注：此处的删除是真正的删除，即从容器中去除重复的元素，容器的长度也发生了变换；而单纯的使用unique函数的话，容器的长度并没有发生变化，只是元素的位置发生了变化)
```

```c++
//彻底去重
#include<iostream>
#include<algorithm>
#include<cassert>
using namespace std;
 
int main()
{
 
    vector<int> a ={1,3,3,4,5,6,6,7};
    vector<int>::iterator it_1 = a.begin();
    vector<int>::iterator it_2 = a.end();
    vector<int>::iterator new_end;
 
    new_end = unique(it_1,it_2); //注意unique的返回值
    a.erase(new_end,it_2);
    cout<<"删除重复元素后的 a : ";
    for(int i = 0 ; i < a.size(); i++)
        cout<<a[i];
    cout<<endl;
 
}
```

#### lcm()  gcd()

```c++
//lcm  返回两个数字的最小公倍数
template<class _Mn, class _Nn> constexpr std::common_type<_Mn, _Nn>::type std::lcm(_Mn __m, _Nn __n)
Least common multiple
    
//gcd 返回两个数字的最大公约数
template<class _Mn, class _Nn> constexpr std::common_type<_Mn, _Nn>::type std::gcd(_Mn __m, _Nn __n)
Greatest common divisor
```

#### c_str

```
可以将 const string* 类型 转化为 cons char* 类型
c_str()就是将C++的string转化为C的字符串数组，c_str()生成一个const char *指针，指向字符串的首地址
因为在c语言中没有string类型，必须通过string类对象的成员函数 c_str() 把 string 转换成c中的字符串样式
```

```c++
注意: c_str() 这个函数转换后返回的是一个临时指针，不能对其进行操作
所以因为这个数据是临时的，所以当有一个改变这些数据的成员函数被调用后，该数据就会改变失效

#include <iostream>
#include <cstring>
using namespace std;
int main()
{
    const char *ptr;
    string s = "12345";
    ptr = s.c_str();
    cout << "s改变前ptr为: " << ptr << endl;
    s = "66666";
    cout << "s改变后ptr为: " << ptr << endl;
    return 0;
}

//s改变前ptr为: 12345
//s改变后ptr为: 66666


要么直接将这个数据应用或输出，要么把它的数据用 strcpy() 函数复制到自己可以管理的内存中；
#include <iostream>
#include <cstring>
using namespace std;
int main()
{
    char ptr[5];
    string s = "12345";
    strcpy(ptr, s.c_str());
    cout << "s改变前ptr为: " << ptr << endl;
    s = "66666";
    cout << "s改变后ptr为: " << ptr << endl;
    return 0;
}

//s改变前ptr为: 12345
//s改变后ptr为: 12345
```

#### atoi atol atoll atoq

```c++
//头文件
#include <stdlib.h>

//函数声明
int atoi(const char *nptr);
long atol(const char *nptr);
long long atoll(const char *nptr);
long long atoq(const char *nptr);

//功能说明
atoi: 把字符串nptr转换为int
atol: 把字符串nptr转换为long int
atoll: 把字符串nptr转换为long long int
atoq: atoq() is an obsolete name for atoll()
    
//示例
int main()
{
    int ii = 0;
    ii = atoi("123");
    cout << ii;    //123
    
    ii = atoi("123abc");
    cout << ii;    //123, 合法数字后面的字母被忽略
    
    ii = atoi("abc123");
    cout << ii;    //0 数字前有字符为非法
    
    ii = atoi("+123");
    cout << ii;     //123 '+'是合法字符
    
    ii = atoi("-123");
    cout << ii;    //-123 '-'是合法字符
    
    string s = "123455";
    int a = atoi(s.substr(0, 3).c_str());
    //a = 123;
}


```

#### to_string

```c++
//将数字常量转换为字符串
inline std::__cxx11::string std::__cxx11::to_string(int __val)
    
//返回值是转换完成的string
    
//示例
#include <string>
using namespace std;
int main()
{
    string pi = "pi is " + to_string(3.1415926);
    cout << pi;
    return 0;
}

//pi is 3.1415926
```

#### % *s    %. *s

```c++
%*s:取决于在scanf中使用还是在printf中使用

1. 在scanf中使用, 则添加了*的部分会被忽略

int a;
char b[10];
scanf("%d%*s", &a, b);
//输入为：12 abc那么12将会读取到变量a中，但是后面的abc将在读取之后抛弃，不赋予任何变量(例如这里的字符数组b）

2.在printf中使用,表示用后面的形参替代的位置，实现动态格式输出
printf("%*s", 10, s);
//意思是输出字符串s，但至少占10个位置，不足的在字符串s左边补空格，这里等同于printf("%10s", s);


%.*s:  *用来指定宽度，对应一个整数。.（点）与后面的数合起来 是截取此宽度的字符，如果字符串长度大于这个数，则按此宽度输出，如果小于，则输出实际长度
int i;
for(i = 1; i <= 3; i++)
printf("%.*s\n", i, "******");
return 0;
//*
//**
//***
```

#### bitset

```c++
bitset可以说是一个多位二进制数，每八位占用一个字节，因为支持基本的位运算，所以可用于状态压缩，n位bitset执行一次位运算的时间复杂度可视为n/32.

定义
bitset<n> bs;   //表示一个n位的二进制数, n是位数

位运算操作符
~s      //返回对bs每一位取反后的结果
& | ^   //分别返回对两个位数相同的bieset执行按位与, 按位或, 按位异或的结果
<< >>   //返回把一个bitset左移, 右移若干位的结果(补零)

[]操作符
bs[i]   //表示bs的第i位, 即可取值也可赋值, 编号从0开始

any/none
若s所有位都为0, 则s.any()返回false，s.none()返回true
若s至少有一位为1, 则s.any()返回true，s.none()返回false

set/rest/flip
s.set()把s所有位变为1
s.set(k,v)把s的第k位改为v, 即s[k] = v
s.reset()把s的所有位变为0
s.reset(k)把s的第k位改为0, 即s[k] = 0
s.flip()把s所有位取反, 即s = ~s
s.flip(k)把s的第k位取反，即s[k] ^= 1
```

