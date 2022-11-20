OJ

```c
#include <stdio.h>
#include <math.h>
#include <stdlib.h>
#include <string.h>

//字符金字塔
void my_print(int n, char a)
{
    for(int i = n - 1; i >= 0; i--)
    {
        for(int j = 0; j < i; j++)  printf(" ");
        for(int j = 0; j < (n - i); j++)    printf("%c ", a);
        printf("\n");
    }
    return;
}
int main()
{
    int n;
    char a;
    scanf("%d %c", &n, &a);
    my_print(n, a);
    return 0;
}

//空心数字金字塔

void my_print(int n)
{
    for (int i = 1; i <= n; i++)
    {
        for (int j = 0; j < n - i; j++)  printf(" ");
        printf("%d", i);
        if(i == 1)  printf("\n");
        if (i > 1 && i < n)
        {
            for (int j = 0; j < 2 * (i - 1) - 1; j++)   printf(" ");
        }
        if(i > 1 && i < n)   printf("%d\n", i);
        if(i == n)
        {
            for(int j = 1; j < 2 * n - 1; j++)  printf("%d", n);
            printf("\n");
        }
    }
}
int main()
{
    int n;
    scanf("%d", &n);
    my_print(n);
    return 0;
}

//使用函数求素数和
int buf[1000];
int cnt = 0, sum = 0;
int Isprime(int a)
{
    if(a == 1)  return 0;
    for(int i = 2; i < a; i++)
        if(a % i == 0)  return 0;
    return 1;
}
void my_print(int m, int n)
{
    for(int i = m; i <= n; i++)
    {
        if(Isprime(i))
        {
            buf[cnt++] = i;
            sum += i;
        }
    }
    for(int i = 0; i < cnt; i++)
    {
        if(i == 0)  printf("Sum of ( ");
        printf(" %d" + !i, buf[i]);
        if(i == cnt - 1)    printf(" ) = %d", sum);
    }
    return;
}
int main()
{
    int m, n;
    scanf("%d %d", &m, &n);
    my_print(m, n);
    return 0;
}

//使用函数求数字个数
int main()
{
    char buf[1000], num;
    int cnt = 0;
    scanf("%s %c", buf, &num);
    int len = strlen(buf);
    for (int i = 0; i < len; i++)    
    {
        if (buf[i] == num) cnt++;
    }
    printf("Number of digit %c in ", num);
    for(int i = 0; i < len; i++)    printf("%c", buf[i]);
    printf(": %d", cnt);
    return 0;
}

//使用函数输出指定范围内完数
int buf[20000];
int cnt = 0, sum = 0, flag = 0;
int Judge(int a)
{
    for(int i = 1; i < a; i++)
    {
        if(a % i == 0)  
        {
            buf[cnt++] = i;
            sum += i;
        }
        if(i == a - 1 && sum == a)  return 1;
    }
    return 0;
}
void print(int m, int n)
{
    for(int i = m; i <= n; i++)
    {
        sum = 0;
        cnt = 0;
        memset(buf, 0, 20000);
        if(Judge(i))
        {
            flag = 1;
            printf("%d =", i);
            for(int j = 0; j < cnt; j++)
            {
                if(j != cnt - 1)    printf(" %d +", buf[j]);
                else printf(" %d\n", buf[j]);   
            }
        }
    }
    if(!flag)   printf("No perfect number");
    return;
}
int main()
{
    int m, n;
    scanf("%d %d", &m, &n);
    print(m, n);
    return 0;
}

//使用函数输出指定范围内的Fibonacci数
void Fib(int lib[])
{
    int i = 2;
    while(i < 10001)
    {
        lib[i] = lib[i - 1] + lib[i - 2];
        i++;
    }
    return;
}
int Judge(int a, int lib[])
{
    for(int i = 0; i < 10001; i++)
    {
        if(lib[i] == a) return 1;
    }
    return 0;
}
int main()
{
    int m, n, cnt = 0;
    int buf[8000];
    int lib[10000] = {1, 1};
    Fib(lib);
    scanf("%d %d", &m, &n);
    for(int i = m; i <= n; i++)
    {
        if(Judge(i, lib))    buf[cnt++] = i;
    }
    for(int i = 0; i < cnt; i++)
    {
        printf(" %d" + !i, buf[i]);
    }
    if(cnt == 0)    printf("No Fibonacci number");
    return 0;
}

//勤奋的大佬
int main()
{
    int t;
    scanf("%d", &t);
    while(t--)
    {
        int x, y, n, sum = 0;
        scanf("%d %d %d", &x, &y, &n);
        for(int i = 1; i <= n; i++)
        {
            if(!(i % (x + 1) || i % (y + 1)))  sum += 36;
        }
        printf("%d\n", sum);
    }
    return 0;
}

//字符合并
char ch[1000000];
int main()
{
    int n, cnt = 0, flag = 0;
    scanf("%d", &n);
    getchar();
    gets(ch);
    for(int i = 0; ch[i] != '#'; i++)
    {
        if(cnt >= n) break;
        if(ch[i] >= 'A' && ch[i] <= 'Z')  
        {
            printf(" %c" + !flag, ch[i]);
            cnt += 1 + flag;
            flag = 1;
        }
        else if(ch[i] != ' ')    
        {
            printf("%c", ch[i]);
            cnt++;
        }
    }
    return 0;
}
```



[百练题单][百练题单-热门题-从易到难 - Virtual Judge (csgrandeur.cn)](https://vjudge.csgrandeur.cn/article/3191)

```c++
//大整数除法
int main()
{
    char a[210] = {0}, b[210] = {0};
    cin >> a >> b;
    int aa[210], bb[210], tmp, flag = 0;
    memset(aa, 0, 210);
    memset(bb, 0, 210);
    int al = strlen(a), bl = strlen(b);
    for (int i = al; i > 0; i--)   aa[al - i + 1] = a[i - 1] - '0';
    for (int i = bl; i > 0; i--)   bb[bl - i + 1] = b[i - 1] - '0';
    int buf[100000] = {0};
    for (int i = 1; i <= bl; i++)
    {
        for (int j = 1; j <= al; j++)
        {
            tmp = bb[i] * aa[j] + buf[i + j - 1];
            buf[i + j - 1] = tmp % 10;
            buf[i + j]  += tmp / 10;
        }
    }
    for (int i = al + bl; i > 0; i--)
    {
        if (buf[i] != 0)  flag = 1;
        if (flag || i == 1)   cout << buf[i];
    }
    return 0;
}
```



[STL](https://vjudge.csgrandeur.cn/contest/529954#overview)

```c++
//单词数
#include <iostream>
#include <string>
#include <set>
using namespace std;
int main()
{
    string str;
    while (getline(cin, str))
    {
        set<string> se;
        if (str[0] == '#')  break;
        string t = "";
        for (int i = 0; i < str.size(); i++)
        {
            if (str[i] == ' ' || i == str.size() - 1)
            {
                if (t.size() == 0)  continue;
                else se.insert(t);
                t = "";
            }
            else
                t += str[i];
        }
        printf("%d\n", se.size());
    }
    return 0;
}

//操作栈
#include <iostream>
#include <stack>
using namespace std;
int main()
{
    stack<int> stk;
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        int op;
        scanf("%d", &op);
        if (op == 1)
        {
            int x;
            scanf("%d", &x);
            stk.push(x);
        }
        else
        {
            if (stk.empty())    printf("empty\n");
            else
            {
                printf("%d\n", stk.top());
                stk.pop();
            }
        }
    }
    return 0;
}

//操作队列
#include <iostream>
#include <string>
#include <queue>
using namespace std;
int main()
{
    queue<int> que;
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        int op;
        scanf("%d", &op);
        if (op == 1)
        {
            int a;
            scanf("%d", &a);
            que.push(a);
        }
        else
        {
            if(que.empty()) printf("empty\n");
            else
            {
                printf("%d\n", que.front());
                que.pop();
            }
        }
    }
    return 0;
}

//愚人节的礼物
#include <iostream>
#include <string>
#include <cstring>
#include <stack>
using namespace std;
char s[1005];
int main()
{
    stack<char> stk;
    while (scanf("%s", s) != EOF)
    {
        int len = strlen(s);
        for (int i = 0; i < len; i++)
        {
            if (s[i] == '(')    stk.push('(');
            else if (s[i] == ')')    stk.pop();
            else if (s[i] == 'B')   printf("%d\n", stk.size());
        }
    }
    return 0;
}

//Train Problem I
#include <iostream>
#include <string>
#include <cstring>
#include <queue>
#include <stack>
using namespace std;
const int N = 15;
char a[N], b[N];
int main()
{
    int n;
    while (scanf("%d%s%s", &n, a + 1, b + 1) != EOF)
    {
        vector<int> ve;
        int j = 1;
        stack<char> stk;
        int fl = 1;
        for (int i = 1; i <= n; i++)
        {
            stk.push(a[i]);
            ve.push_back(1);
            while (!stk.empty() && stk.top() == b[j])
            {
                stk.pop();
                j++;
                ve.push_back(0);
            }
        }
        if (j <= n) fl = 0;
        if (stk.empty() && fl)
        {
            printf("Yes.\n");
            for (int i = 0; i < ve.size(); i++)
            {
                if (ve[i] == 0) printf("out\n");
                else printf("in\n");
            }
        }
        else 
            printf("No.\n");
        printf("FINISH\n");
    }
    return 0;
}

//Let the Balloon Rise
#include <iostream>
#include <string>
#include <cstring>
#include <stack>
#include <map>
using namespace std;
int main()
{
    int n;
    while(cin >> n)
    {
        if(!n)	break;
        map<string, int> ma;
        for(int i = 0; i < n; i++)
        {
            string s;
            cin >> s;
            ma[s]++;
        }
        string ret;
        int cmp = 0;
        for(auto it = ma.begin(); it != ma.end(); it++)
        {
            if(it -> second > cmp)
            {
                cmp = it -> second;
                ret = it -> first;
            }
        }
        cout << ret << endl;
    }
    return 0;
}

//水果
#include <iostream>
#include <string>
#include <cstring>
#include <stack>
#include <map>
using namespace std;
int main()
{
    int t;
    cin >> t;
    while(t--)
    {
        int n;
        cin >> n;
        map<string, map<string, int>> ma;
        for(int i = 0; i < n; i++)
        {
            string fruits, area;
            int num;
            cin >> fruits >> area >> num;
            ma[area][fruits] += num;
        }
        for(auto it = ma.begin(); it != ma.end(); it++)
        {
            cout << it -> first << endl;
            for(auto itt = it -> second.begin(); itt != it -> second.end(); itt++)
            {
                cout << "   |----" << itt -> first << "(" << itt -> second << ")" << endl;
            }
        }
        if(t)   cout << endl;
    }
    return 0;
}

//stones
#include <iostream>
#include <string>
#include <cstring>
#include <queue>
using namespace std;
struct node
{
    int pos, dis;
    bool operator<(const node &t) const
    {
        if (pos != t.pos)
            return pos > t.pos;
        return dis > t.dis;
    }
};
int main()
{
    int t;
    cin >> t;
    while(t--)  
    {
        int n;
        cin >> n;
        priority_queue<node> que;
        for (int i = 0; i < n; i++)
        {
            node b;
            scanf("%d%d", &b.pos, &b.dis);
            que.push(b);
        }
        int res = 0;
        int flag = 0;
        while (que.size())
        {
            if (!flag)
            {
                node b;
                b.dis = que.top().dis;
                b.pos = que.top().dis + que.top().pos;
                que.pop();
                que.push(b);
                flag ^= 1;
                if(que.size() == 1)
                {
                    res = que.top().pos;
                    break;
                }
            }
            else 
            {
                que.pop();
                flag ^= 1;
            }
        }
        printf("%d\n", res);
    }
    return 0;
}

//Windows Message Queue
#include <iostream>
#include <string>
#include <cstring>
#include <queue>
using namespace std;
struct node
{
    int num;
    int val;
    int val2;
    string name;
    bool operator<(const node &t) const
    {
        if (val != t.val)
            return val > t.val;
        else 
            return val2 > t.val2;
    }
};
int main()
{
    string s;
    priority_queue<node> que;
    int id = 1;
    while (cin >> s)
    {
        if (s == "GET")
        {
            if (que.empty())
                cout << "EMPTY QUEUE!\n";
            else 
            {
                cout << que.top().name << " " << que.top().num << endl;
                que.pop();
            }
        }
        else 
        {
            string name;
            int num, val;
            cin >> name >> num >> val;
            que.push({num, val, id, name});
        }
        id++;
    }
    return 0;
}
```



