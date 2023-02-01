# Algorithm

## 基础数据结构

#### 队列

###### 优先队列

```c++
//priority_queue

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

###### 单调队列

ACWing 154. 滑动窗口

```c++

#include <iostream>
#include <stack>
#include <cstring>
using namespace std;
const int N = 1e6 + 5;
int a[N], q[N];
int n, k;
int main()
{
    cin >> n >> k;
    for (int i = 1; i <= n; i++) cin >> a[i];
    int hh = 0, tt = -1; //hh表示队首，tt表示队尾
    for (int i = 1; i <= n; i++)
    {
        while (hh <= tt && i - k >= q[hh]) hh++;     //维护局部性
        while (hh <= tt && a[q[tt]] >= a[i]) tt--;   //维护单调性
        q[++tt] = i;
        if (i >= k) cout << a[q[hh]] << " ";
    }
    cout << endl;

    hh = 0; tt = -1;
    for (int i = 1; i <= n; i++)
    {
        while (hh <= tt && i - k >= q[hh]) hh++;
        while (hh <= tt && a[q[tt]] <= a[i]) tt--;
        q[++tt] = i;
        if (i >= k) cout <<a[q[hh]] << " ";
    }
    cout << endl;
    return 0;
}
```



```c++
//
//双端队列
#include <iostream>
#include <stack>
#include <queue>
#include <algorithm>
using namespace std;
const int N = 3e5 + 10;
int n, m;
int a[N], q[N];
int main()
{
    cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> a[i], a[i] += a[i - 1];
    deque<int> deq;
    int ans = 0;
    for (int i = 1; i <= n; i++)
    {

        while (!deq.empty() && a[deq.back()] > a[i]) deq.pop_back();
        deq.push_back(i);
        if (deq.back() - deq.front() > m) deq.pop_front();
        ans = max(ans, a[i] - a[deq.front()]);
    }
    cout << ans;
    return 0;
}
```

luogu P1886 滑动窗口 /【模板】单调队列

```c++
#include <iostream>
#include <queue>
#include <stack>
using namespace std;
const int maxn = 1e6 + 10;
int n, k, nums[maxn];
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    deque<int> s;
    vector<int> ans1;
    vector<int> ans2;
    cin >> n >> k;
    for (int i = 1; i <= n; i++) cin >> nums[i];
    for (int i = 1; i <= n; i++)
    {
        while (!s.empty() && i - s.front() >= k) s.pop_front();
        while (!s.empty() && nums[s.back()] > nums[i]) s.pop_back();
        s.push_back(i);
        if (i >= k) ans1.push_back(s.front());
    }
    s.clear();
    for (int i = 1; i <= n; i++)
    {
        while (!s.empty() && i - s.front() >= k) s.pop_front();
        while (!s.empty() && nums[s.back()] < nums[i]) s.pop_back();
        s.push_back(i);
        if (i >= k) ans2.push_back(s.front());
    }
    for (auto it = ans1.begin(); it != ans1.end(); it++)
    {
        if (it == ans1.begin()) cout << nums[(*it)];
        else cout << " " << nums[(*it)];
    }
    cout << endl;
    for (auto it = ans2.begin(); it != ans2.end(); it++)
    {
        if (it == ans2.begin()) cout << nums[(*it)];
        else cout << " " << nums[(*it)];
    }
    return 0;
}
```

luogu P1714 切蛋糕

求连续子序列和, 所以需要先储存前缀和; 然后遍历, 遍历的同时维护遍历到的元素之前的各前缀和所组成的单调递增队列, 在前面的始终是符合区间的同时是区间内最小的前缀和, 而求最大子区间不过就是遍历到的该前缀和减去前面最小的前缀和而已.

对于每一个`i`来讲, `sum[i]`是固定的，于是就转化成了`sum[i]-min(sum[j]) (i-m<=j && j<=i-1)`

```c++
#include <algorithm>
#include <iostream>
#include <queue>
using namespace std;
const int maxn = 5e5 + 10;
int n, m, a[maxn], ans;
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> a[i], a[i] += a[i - 1];
    deque<int> q;
    for (int i = 1; i <= n; i++)
    {
        while (!q.empty() && a[q.back()] > a[i - 1]) q.pop_back();
        while (!q.empty() && i - q.front() > m) q.pop_front();
        q.push_back(i - 1);
        ans = max(ans, a[i] - a[q.front()]); 
    }
    cout << ans;
    return 0;
}
```

luogu P2629 好消息，坏消息

心情值相加, 首先是想到前缀和, 然后是一个关键思想"断环为链", 出现前后数据的相连, 开双倍数组储存数据, 能够完美解决. 然后题意就是要使每一个子序列的前缀和都不小于0, 那就是前缀和最小值不小于0即可, 而且子序列长度固定为n, 可以联想到窗口, 构造单调递增队列, 维护窗口和单调性即可. 

```c++
#include <algorithm>
#include <iostream>
#include <queue>
using namespace std;
const int maxn = 2e6 + 10;
int a[maxn], n, ans;
int main()
{
    cin >> n;
    for (int i = 1; i <= 2 * n; i++)
    {
        if (i <= n) cin >> a[i], a[i] += a[i - 1];
        else a[i] = a[n] + a[i - n];
    }
    deque<int> q;
    for (int i = 1; i <= 2 * n - 1; i++)
    {
        while (!q.empty() && a[q.back()] >= a[i]) q.pop_back();
        while (!q.empty() && i - q.front() >= n) q.pop_front();
        q.push_back(i);
        if (i >= n && a[q.front()] - a[i - n] >= 0) ans++;
    }
    cout << ans;
    return 0;
}
```

hdu 3415 Max Sum of Max-K-sub-sequence

```c++
//不应该有问题的, 却TLE了,奇奇怪怪
#include <algorithm>
#include <iostream>
#include <queue>
using namespace std;
const int maxn = 2e5 + 10;
int t, k, n, a[maxn], x, y;
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0); cout.tie(0);
    for (cin >> t; t--; )
    {
        int ans = -0x3f3f3f3f;
        cin >> n >> k;
        for (int i = 1; i <= n + k - 1; i++)
        {
            if (i <= n) cin >> a[i], a[i] += a[i - 1];
            else a[i] = a[n] + a[i - n];
        }
        deque<int> q;
        for (int i = 1; i <= n + k - 1; i++)
        {
            while (!q.empty() && a[q.back()] >= a[i - 1]) q.pop_back();
            while (!q.empty() && i - q.front() > k) q.pop_front();
            q.push_back(i - 1);
            if (a[i] - a[q.front()] > ans)
            {
                ans = a[i] - a[q.front()];
                x = q.front() + 1;
                y = i > n ? i % n : i;
            }
        }
        cout << ans << " " << x << " " << y << " "  << endl;
    }
    return 0;
}
```

luogu P2216 [HAOI2007]理想的正方形

维护二维窗口的最值, 此题本质上和维护一维窗口最值是一样的, 或者说基于维护一维窗口之上, 例如想要维护一个`n * n`的窗口, 只需先维护每一行, 再对每一行的结果维护列最值, 即变成了维护二维窗口最值, 过程繁琐易混, 实现过程需要仔细

```c++
#include <algorithm>
#include <iostream>
#include <queue>
using namespace std;
const int maxn = 1e3 + 10;
int a, b, n, s1[maxn][maxn], s2[maxn][maxn], s3[maxn][maxn], s4[maxn][maxn], s5[maxn][maxn], ans = 0x3f3f3f3f;
int main()
{
    cin >> a >> b >> n;
    for (int i = 1; i <= a; i++)
        for (int j = 1; j <= b; j++)
            cin >> s1[i][j];
    for (int i = 1; i <= a; i++)
    {
        deque<int> q;
        for (int j = 1; j <= b; j++)
        {
            while (!q.empty() && s1[i][q.back()] <= s1[i][j]) q.pop_back();
            while (!q.empty() && j - q.front() >= n) q.pop_front();
            q.push_back(j);
            if (j >= n) s2[i][j - n + 1] = s1[i][q.front()];
        }
        q.clear();
        for (int j = 1; j <= b; j++)
        {
            while (!q.empty() && s1[i][q.back()] >= s1[i][j]) q.pop_back();
            while (!q.empty() && j - q.front() >= n) q.pop_front();
            q.push_back(j);
            if (j >= n) s3[i][j - n + 1] = s1[i][q.front()];
        }
    }
    for (int i = 1; i <= b - n + 1; i++)
    {
        deque<int> q;
        for (int j = 1; j <= a; j++)
        {
            while (!q.empty() && s2[j][i] >= s2[q.back()][i]) q.pop_back();
            while (!q.empty() && j - q.front() >= n) q.pop_front();
            q.push_back(j);
            if (j >= n) s4[j - n + 1][i] = s2[q.front()][i];
        }
        q.clear();
        for (int j = 1; j <= a; j++)
        {
            while (!q.empty() && s3[j][i] <= s3[q.back()][i]) q.pop_back();
            while (!q.empty() && j - q.front() >= n) q.pop_front();
            q.push_back(j);
            if (j >= n) s5[j - n + 1][i] = s3[q.front()][i];
        }
    }
    for (int i = 1; i <= a - n + 1; i++)
        for (int j = 1; j <= b - n + 1; j++)
            ans = min(ans, s4[i][j] - s5[i][j]);
    cout << ans << endl;
    return 0;
}
```

#### 栈

###### 单调栈

```
单调栈与单调队列
二者：都可将复杂度优化至O(n)


栈和队列的区别
栈是只有一端可以插入和删除的线性表，他是一个先进后出的结构，而队列则是有两个端口可以分别进行插入和删除，满足先进先出的特性。但是在实际情况中，我们维持的单调栈和栈的数据结构是吻合的，而维持的单调队列则大部分可能都是双端队列。
一个使用单调栈的问题往往需要我们维持的原始数组的区间变化情况是，只有一段增加或者减少，这个时候我们可以选择使用单调栈来维持原始数组给定区间内的最值问题。
而对于左右端点都发生变化的问题，就要使用单调队列进行维持，只有区间变化芒族类似于队列的元素流动的方向时，才使用单调队列。前面我们已经说过，单调栈因为左端点，不变，所以可以支持一个端点左移或者右移的操作，而之所以可以左移或者右移，是因为单调栈只插入满足条件的点，而不会对以及入栈的元素进行最优性剪枝，这样，就保证了右端点可以左移的条件；而单调队列在维持的过程中，整个要维持的区间是单向移动的，假设要维持的两个端点都是向右移动的，那么当左端点右移时，实际上最次最优值是会发生变化的，这样为了保证左端点右移时候选最优值的正确性，我们在右端点右移的过程中，必须把当前元素插入到单调队列中（单调栈则不用），这样插入时，为了维持单调性，我们就需要进行最优性剪枝，此时如果我们再将右端点左移，那么上一回合插入的元素实际上需要删除，但是上一回合中我们已经进行了最优性剪枝，这样即使我们将上一回合插入的元素删除，我们也不能将单调队列在恢复到之前的状态。
综上，我们得到使用单调队列的问题，要维持的区间一定是左右端点同时单向移动的；而使用单点栈的问题，则一定是只有一个端点左移或者右移的。
根据以上两个特征我们可以很轻松地判断一个问题到底是应该使用那个结构来维持，当然不过单调栈还是单调队列，我们都可以用双端队列维持，这是因为双端队列可以满足单调栈或者单调队列的所有要求。
最后，使用单调栈的问题，我们一定使用的是双端队列维持，有一个端点需要同时插入和删除，所以队列是不满足要求的。


单调队列与单调栈的区别：
单调栈只维护一端（栈顶）单调队列维护两端，它的头端可以出数，尾部可以进数。
单调栈通常维护全局的单调性，而单调队列通常维护局部的单调性。
单调栈大小没有上限，而单调队列通常有大小限制。
由于单调队列的对首可以出队以及前面的元素一定比后面的元素先入队的性质，使得它可以维护局部的单调性。因此单调队列通常用于解决局部性的最值问题
```

代码模板

```c++
//利用C++提供的stl模板库
//一个单调递减的单调栈
stack<int> sta;
...
//当栈为空时，无条件入栈，若新元素大于栈顶元素，则出站顶元素
while (!sta.empty() && sta.top() < x)
	sta.pop();
sta.push(x);
...
    
    
//C代码
int _stack[maxn];
int pi = 0; //可以看作一个指针（pointer），含义为栈顶位置以及栈元素
for (int i = 0; i < the_number_of_element; i++)
{
    while (pi && _stack[pi - 1] < element[i])
        pi--;
    _stack[pi++] = element[i];
}
```

luogu P5788 【模板】单调栈

```c++
#include <cstdio>
#include <stack>
using namespace std;
const int maxn = 3e6 + 10;
int a[maxn], n, ans[maxn];
stack<int> s;
int main()
{   
    scanf("%d", &n);
    for (int i = 1; i <= n; i++) scanf("%d", &a[i]);
    for (int i = 1; i <= n; i++)
    {
        while (!s.empty() && a[s.top()] < a[i])
        {
            ans[s.top()] = i;    
            s.pop();
        }
        s.push(i);
    }
    for (int i = 1; i <= n; i++) printf(" %d" + !(i - 1), ans[i]);
    return 0;
}
//or
#include <iostream>
#include <stack>
using namespace std;
const int N = 3e6 + 5;
int a[N], b[N];
int n;
int main()
{
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> a[i];
    stack<int> sta;
    for (int i = n; i >= 0; i--)
    {
        while (!sta.empty() && a[i] >= a[sta.top()]) sta.pop();
        b[i] = sta.empty() ? 0 : sta.top();
        sta.push(i);
    }
    for (int i = 1; i <= n; i++) cout << b[i] << " ";
    return 0;
}
```

luogu P1901 发射站

构造单调递减栈, 出栈的同时要将能量记录给入栈的元素, 算作是出栈元素向右发射的能量的归属, 而每一次入栈前, 入栈元素的能量要记录给栈顶元素, 算作是每一个入栈元素向左发射的能量的归属(注意要判断是否为空)

```c++
#include <cstdio>
#include <stack>
using namespace std;
const int maxn = 1e6 + 10;
int a[maxn], n, h, v, ans;
int main()
{
    stack<int> s;
    vector<pair<int, int>> vec;
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        scanf("%d%d", &h, &v);
        pair<int, int> p(h, v);
        vec.push_back(p);
    }
    for (int i = 0; i < n; i++)
    {
        while (!s.empty() && vec[s.top()].first < vec[i].first)
        {
            a[i] += vec[s.top()].second;
            s.pop();
        }
        if (!s.empty()) a[s.top()] += vec[i].second;
        s.push(i);
    }
    for (int i = 0; i < n; i++) ans = max(ans, a[i]);
    printf("%d", ans);
    return 0;
}
//or
#include <iostream>
#include <stack>
#include <algorithm>
using namespace std;
const int N = 1e6 + 5;
long long a[N], b[N], q[N], n, ans;
int main()
{
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> a[i] >> b[i];
    stack<int> sta;
    for (int i = 1; i <= n; i++)
    {
        while (!sta.empty() && a[sta.top()] < a[i])
        {
            q[i] += b[sta.top()];
            sta.pop();
        }
        if (!sta.empty()) q[sta.top()] += b[i];
        sta.push(i);
    }
    for (int i = 1; i <= n; i++)
        ans = max(ans, q[i]);
    cout << ans;
    return 0;
}
```

luogu P7399 [COCI2020-2021#5] Po

单调递增栈, 此题与**luogu p5019**铺设道路其实很像, 但又有不同之处, 此题是可以加任意整数, 道路题(也可转换为高度)是每次只能加1, 所以此题的高度不能涵盖后面连续比它小的高度, 但是道路题可以, 因为道路题是逐一增加高度, 能涵盖后面连续比它小的高度, 所以此题需要判断后面的高度有无与前面高度一致的, 一致的才能够被前面的操作所包含, 如果是新出现的高度, 那必须得增加一次操作, 单调栈的维护正好方便后面的高度与前面的高度进行比较, 如果一样直接`continue`即可. 但是两个题都有的特点就是高度在出现递减之后就无法再传递给后面的高度, 这在本题体现在无用的高度会被`pop`, 在另一题则体现在遇到更高的时候`ans += a[i] - a[i - 1]` .

```c++
#include <iostream>
#include <queue>
#include <stack>
#include <algorithm>
using namespace std;
const int N = 1e5 + 5;
int n, x, ans;
int main()
{
    cin >> n;
    stack<int> sta;
    for (int i = 1; i <= n; i++)
    {
        cin >> x;
        while (!sta.empty() && sta.top() > x) sta.pop();
        if (!sta.empty() && sta.top() == x) continue; 
        if (x) ans++, sta.push(x);
    }
    cout << ans;
    return 0;
}
```

luogu P1823 [COI2007] Patrik 音乐会的等待

与p1901相似, 但有一点不同, 相同高度的人是能相互看到的, 这引发两个问题: 如果全部人身高相同, 那么在$5×10^5$的情况下答案会超过int类型, 所以必须用`long long`存答案; 身高相同可以相互看到, 并且不会互相影响视线, 所以维护单调性的时候, 去掉相同身高的人的时候(必须去掉, 否则你会发现新入栈的人与原栈中更高的那一个能看到但却没有被算进去), 该身高必须储存起来, 否则比如`5 2 2 2 5`这种数据, 你会发现每个`2`都能看见后面的`5`, 却没有被你计入对数, 当然了, 没有任何关系的相同身高, 就不用考虑了, 例如`5 2 5 1 2`;  再仔细比较, 你还会发现, 发射站的说法是"发出的能量只被两边**最近的且比它高**的发射站接收", 音乐会是"如果他们是**相邻或他们之间没有人比 a 或 b 高**，那么他们是可以互相看得见的", 研究两个说法, 会发现能接收到的发射站与发射能量的发射站是能相互看见的, 只不过相对高度不同导致谁接收谁发射不同, 所以两道题的代码思路是基本一致的, 而且音乐会相同身高的人可能相互看见, 但相同高度的发射塔不会相互接收


```c++

#include <iostream>
#include <queue>
#include <stack>
#include <algorithm>
using namespace std;
long long ret, n, cnt;
int main()
{
    cin >> n;
    stack<pair<int, int>> s;
    for (int i = 1; i <= n; i++)
    {
        cin >> ret;
        pair<int, int> p(ret, 1);
        while (!s.empty() && s.top().first <= ret)
        {
            cnt += s.top().second;
            if (s.top().first == ret) p.second += s.top().second;
            s.pop();
        }
        if (!s.empty()) cnt++;
        s.push(p);
    }
    cout << cnt << endl;
    return 0;
}
```

poj 2559 **Largest Rectangle in a Histogram**

可用数组模拟构造单调递增栈, 也可以直接用STL栈. 思路:遇到比栈顶元素大的, 可以存进一个结构体数组, 该结构体保存目前某个矩形继承的长和宽, 初始宽度为1, 当遇到小于栈顶元素高度的元素时, 栈顶元素出栈, 并且继承上一个出栈元素的宽, 如此累加, 每次操作都需要维护面积最大值 

```c++
//AC
#include <algorithm>
#include <iostream>
#include <stack>
using namespace std;
const int maxn = 1e5 + 10;
long long n, ans, a[maxn], tmp;
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    stack<pair<int, int>> s;
    while (cin >> n && n)
    {
        ans = 0;
        for (int i = 1; i <= n; i++) cin >> a[i];
        for (int i = 1; i <= n; i++)
        {
            long long wide = 0;
            while (!s.empty() && s.top().first >= a[i])
            {
                tmp = s.top().first * (s.top().second + wide);
                ans = max(ans, tmp);
                wide += s.top().second;
                s.pop();
            }
            pair<int, int> p(a[i], 1 + wide);
            s.push(p);
        }
        long long wide = 0;
        while (!s.empty())
        {
            tmp = s.top().first * (s.top().second + wide);
            ans = max(ans, tmp);
            wide += s.top().second;
            s.pop();
        }
        cout << ans << endl;
    }
    return 0;
}
//TLE
#include <stack>
#include <vector>
#include <iostream>
using namespace std;
int n, h, ans;
int main()
{
    while(cin >> n && n)
    {
        ans = 0;
        vector<pair<int, int>> vec;
        for (int i = 0; i < n; i++)
        {
            cin >> h;
            pair<int, int> p(h, h);
            while (!vec.empty() && h < vec.back().first)
            {
                vec.pop_back();
                p.second += p.first;
            }
            vec.push_back(p);
            ans = max(ans, p.second);
            if (!vec.empty() && h >= vec.back().first)
            {
                for (auto it = vec.begin(); it != vec.end(); it++)
                {
                    if (it != vec.end() - 1) (*it).second += (*it).first;
                    ans = max(ans, (*it).second);
                }
            }
        }
        cout << ans << endl;
    }
    return 0;
}
```

## 基本算法

#### 尺取法

poj 2100 Graveyard Design

注意数据范围超`int`, 注意运算过程中对`int`的运算要在必要时候强转为`long long` (也可以全部使用`long long`), 特别注意的一点, 用`scanf`时, 若出现`long long`, 在`poj`系统下, `OS`为`Linux`, 类型需写为`%I64d`, 否则会`Wrong Answer`, 若其他情况下OS为`Windows`, 则`%lld` 和`%I64d`都可以

```c++
#include <algorithm>
#include <iostream>
#include <cstring>
#include <cstdio>
#include <queue>
#include <stack>
#include <map>
using namespace std;
int l, r, cnt;
long long sum = 1, n;
int main()
{
    vector<int> v;
    scanf("%lld", &n);
    l = r = 1;
    while (l <= r && r <= 1e7)
    {
        if (sum == n)
        {
            cnt++;
            v.push_back(r - l + 1);
            for (int i = l; i <= r; i++) v.push_back(i);
        }
        if (n < sum) sum -= 1LL * l * l, l++;
        else if (n >= sum) r++, sum += 1LL * r * r;
    }
    printf("%d\n", cnt);
    for (int i = 0; i < v.size(); i++)
    {
        int ret = v[i];
        printf("%d", ret);
        for (int j = 0; j < ret; i++, j++)
            printf(" %d", v[i + 1]);
        printf("\n");
    }
    return 0;
}
```

HDU 5178 pairs

```c++
//二分
#include <iostream>
#include <queue>
#include <stack>
#include <vector>
#include <algorithm>
using namespace std;
#define LL long long
const int N = 1e5 + 5;
LL n, k, cnt, t, a[N];
void solve()
{
    cnt = 0;
    for (int i = 1; i <= n; i++)
    {
        LL ret = a[i] - k;
        LL l = 1, r = i;
        while (l < r)
        {
            LL mid = (l + r) / 2;
            if (a[mid] >= ret) r = mid;
            else l = mid + 1; 
        }
        cnt += i - l;
    }
    cout << cnt << endl;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    for(cin >> t; t--; )
    {
        cin >> n >> k;
        for (int i = 1; i <= n; i++) cin >> a[i];
        sort(a + 1, a + 1 + n);
        solve();
    }
    return 0;
}
//尺取
#include <algorithm>
#include <cstdio>
using namespace std;
const int maxn = 1e5 + 10;
int t, n, k, a[maxn];
int main()
{
    for (scanf("%d", &t); t--; )
    {
        long long ans = 0;
        scanf("%d%d", &n, &k);
        for (int i = 1; i <= n; i++) scanf("%d", &a[i]);
        sort(a + 1, a + 1 + n);
        int l = 1, r = 1;
        while (r <= n)
        {
            while (l <= r && a[r] - a[l] > k) l++;
            ans += r - l;
            r++;
        }
        printf("%lld\n", ans);
    }
    return 0;
}
```

HDU 5672

此题不关闭流同步居然会`TLE`, 震惊

```c++
#include <iostream>
#include <string>
using namespace std;
int t, k;
int main()
{
    string s;
    ios::sync_with_stdio(false);
    for (cin >> t; t--; )
    {
        int flag[26] = {0};
        long long ans = 0;
        cin >> s >> k;
        int l = 0, r = 0, cnt = 0, len = s.size();
        while (l < len)
        {
            while (cnt < k && r < len)
            {
                if (!flag[s[r] - 'a']) cnt++;
                flag[s[r] - 'a']++;
                r++;
            }
            if (cnt == k) ans += len - r + 1;
            flag[s[l] - 'a']--;
            if (!flag[s[l] - 'a']) cnt--;
            l++;
        }
        cout << ans << endl;
    }
}
```

luogu P1381 单词背诵

本题的输入对象是字符串，而且又需要判断某个字符串是否出现过以及出现了几次，我们就应该想到使用**map + string**，尺取在本题中可以想象为一个**滑动窗口**（或蠕动窗口，但似乎不太好听）的维护，想象成一个窗口是十分恰当且易理解的，事实上一堆数据中寻找符合题目条件的某区间，就可以考虑选择使用滑动窗口，在本题中是向右探寻，然后左端不断维护更新，以维护ans2

```c++
#include <iostream>
#include <cstring>
#include <algorithm>
#include <map>
using namespace std;
map<string, int> sum; //存储出现的次数
map<string, bool> flag; //存储需要背诵的单词
int ans1, ans2, n, m, l;
string s[100005], s1; //因为后面要对字符串进行存储和操作，所以要用string二维数组来存储字符串
int main()
{
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> s1, flag[s1] = 1; //记录背诵单词
    cin >> m;
    l = 1; //尺取的特点，需要设左端点，右端点在本题中跟随i即可，类似于窗口滑动
    for (int i = 1; i <= m; i++)
    {
        cin >> s[i];
        if (flag[s[i]]) sum[s[i]]++; //记录出现次数
        if (sum[s[i]] == 1) ans1++, ans2 = i - l + 1; //为1，即此背诵单词首次出现，符合最多背诵单词的要求，应加入窗口
        while (l <= i) //窗口左端的维护
        {
            if (!flag[s[l]]) {l++; continue;} //非背诵单词，舍去
            if (sum[s[l]] > 1) {sum[s[l]]--; l++; continue;} //出现了两次而且一个在左端口的单词，也不能要
            break; //与continue完美结合
        }
        ans2 = min(ans2, i - l + 1); //保持最小值
    }
    cout << ans1 << endl << ans2 << endl;
    return 0;
}
```

luogu P3143 [USACO16OPEN] Diamond Collector S

本题的难点不在于求符合要求的区间内的元素个数，难的是题中出现两个陈列架，这意味着我们要找两个符合要求的区间，而且这两个区间元素个数和要最大，一开始我是只移动窗口，只想先找元素个数最大的区间，这其实无益于最终答案的求解，因为即便我找到了最大元素的区间，那加上另一个区间就能保证元素和最大吗？显然是行不通的。所以要换种思路，遍历每一个元素，存储每一个元素之前的区间中，符合要求的元素个数的最大值，然后加上该元素往后区间能符合要求的元素个数，得到该元素往左延申与往右延申的元素个数和，即将该元素作为分界点（当然，该元素在此处实际上隶属于右端符合条件的区间），左右是不同架子的元素，维护最大值即可。

当然了，也可以储存该元素往后的最大储存值，然后再遍历一遍，将某元素往后的符合条件区间元素个数加上此区间最后一个元素往后的最大储存值，此时区间最后一个元素就是分界，然后维护最大值即可。

```c++
#include <iostream>
#include <algorithm>
using namespace std;
int n, k, a[50005], c[50005], r = 2, maxn, ans;
int main()
{
    cin >> n >> k;
    a[n + 1] = INT32_MAX;
    for (int i = 1; i <= n; i++) cin >> a[i];
    sort(a + 1, a + 1 + n);
    for (int i = 1; i <= n; i++)
    {
        while (a[r] <= a[i] + k) r++;
        c[r] = max(r - i, c[r]);
        maxn = max(maxn, c[i]);
        ans = max(maxn + r - i, ans);
    }
    cout << ans;
    return 0;
}

//

#include <iostream>
#include <algorithm>
using namespace std;
const int N = 5e4 + 5;
int n, k, a[N], b[N], maxn[N], ans; 
int main()
{
    cin >> n >> k;
    for (int i = 1; i <= n; i++) cin >> a[i];
    sort(a + 1, a + 1 + n);
    int tt = 1, t = n;
    for (int i = n; i >= 1; i--)
    {
        while (a[t] > a[i] + k) t--;
        b[i] = t - i + 1;
        maxn[i] = max(b[i], maxn[i + 1]);
    }
    for (int i = 1; i <= n; i++)
    {
        while (a[tt] <= a[i] + k && tt <= n + 1) tt++;
        ans = max(ans, tt - i + maxn[tt]);
    }
    cout << ans;
    return 0;
}
```

 hdu 1937 Finding Seats

本题别无他法，必须遍历每一个矩形，因为题目给的行列长度数据小于300，这也注定这道题需要给到n^3的复杂度，需要注意的是，遍历每一个矩形，也不是真就从1到n*n的大小一个一个遍历，而是**给定上界和下界，再给定右界或者左界，形成一个二维滑动窗口**，维护最小值即可。

```c++
#include <iostream>
#include <algorithm>
using namespace std;
const int N = 305;
int r, c, k, ans;
char a;
int room[N][N];
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    while (cin >> r >> c >> k && r + c + k)
    {
        ans = INT32_MAX;
        for (int i = 1; i <= r; i++)
            for (int j = 1; j <= c; j++)
            {
                    cin >> a;
                    if (a == '.') room[i][j] = 1;
                    else room[i][j] = 0;
                    room[i][j] += room[i][j - 1] + room[i - 1][j] - room[i - 1][j - 1];
            }
        for (int i = 1; i <= r; i++) //(i, p) (j, l)
            for (int j = i; j <= r; j++)
            {
                int p = 1;
                for (int l = 1; l <= c; l++)
                {
                    while (room[j][l] - room[i - 1][l] - room[j][p - 1] + room[i - 1][p - 1] >= k)
                    {
                        ans = min(ans, (j - i + 1) * (l - p + 1));
                        p++;
                    }
                }
            }
        cout << ans << endl;
    }
    return 0;
}
```

#### 二分法

```
如何判断一个题是不是用二分答案做的?
1、答案在一个区间内（一般情况下，区间会很大，暴力超时）
2、直接搜索不好搜，但是容易判断一个答案可行不可行
3、该区间对题目具有单调性，即：在区间中的值越大或越小，题目中的某个量对应增加或减少。

此外可能还会有一个典型的特征：求...最大值的最小或求...最小值的最大
1、求...最大值的最小，我们二分答案（即二分最大值）的时候，判断条件满足后，尽量让答案往前来（即：让r=mid），对应模板1;
2、同样，求...最小值的最大时，我们二分答案（即二分最小值）的时候，判断条件满足后，尽量让答案往后走（即：让l=mid），对应模板2；

最大值最小，最小值最大 类 问题解题方向：
最短距离最大化问题：保证任意区间距离要比最短距离mid大或相等（这样，mid才是最短距离）即：区间的距离>=mid
最长距离最小化问题：保证任意区间距离要比最大距离mid小或相等（这样，mid才是最大距离）即：区间的距离<=mid
```

找数原理

```c++
//左闭右闭写法
#include <iostream>
#include <algorithm>
using namespace std;
int target;
int nums[] = {1, 3, 5, 7, 10, 33, 45, 67, 90};
int sz = sizeof(nums) / sizeof(int);
int Search(int nums[], int size, int target)
{
    int left = 0;
    int right = size - 1; //定义target在左闭右闭的区间内, [left, right]
    while (left <= right) //当left == right时，区间[left, right]仍然有效，此处必须是小于等于
    {
        int middle = (left + right) / 2; //取中点
        if (nums[middle] > target) right = middle - 1; //target在左区间，所以[left, middle - 1]
        else if (nums[middle] < target) left = middle + 1; //target在右区间，所以[middle + 1, right]
        else return middle; //即不在左边，也不在右边，那就是找到了
    }
    return -1; //没有找到目标值
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    cin >> target;
    cout << Search(nums, sz, target) << endl;
    return 0;
}


//左闭右开写法
#include <iostream>
#include <algorithm>
using namespace std;
int target;
int nums[] = {1, 3, 5, 7, 10, 33, 45, 67, 90};
int sz = sizeof(nums) / sizeof(int);
int Search(int nums[], int size, int target)
{
    int left = 0;
    int right = sz;
    while (left < right) //因为left == right的时候，在[left, right)区间上已经无意义，所以不能取等号
    {
        int middle = (left + right) / 2;
        if (nums[middle] > target) right = middle;
        else if (nums[middle] < target) left = middle + 1;
        else return middle;
    }
    return -1;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    cin >> target;
    cout << Search(nums, sz, target) << endl;
    return 0;
}


//两种方法的区别就是右区间的闭开会导致下面的while循环判断条件写法不同，需要特别注意
```

模板

```c++
注意事项：左端取1还是取0要特别注意！在二分搜不到答案的时候，倘若那个k值小于任何一个元素，那l最终会走到最左端点，所以你必须考虑在找不到答案的情况下，最终l会停留在哪里

//模板1 往左找答案
while (l < r)
{
	int mid = l + r >> 1;
	if (check(mid)) r = mid;
	else l = mid + 1;
}

//模板2 往右找答案
while (l < r)
{
	int mid = l + r + 1 >> 1; //此处mid加1
	if (check(mid)) l = mid;
	else r = mid - 1;
}

//模板3 浮点二分
while (r - l > 1e-5) //
{
	double mid = (l + r) / 2;
	if (check(mid)) l = mid;
	else r = mid;
}
```

luogu P7441 「EZEC-7」Erinnerung

```c++
#include <iostream>
#include <algorithm>
using namespace std;
long long t, x, y, k;
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    for (cin >> t; t--; )
    {
        cin >> x >> y >> k;
        if (x == 0 && y == 0) cout << 0 << endl;
        else if (x == 0) cout << (k % y == 0 ? 1 : 0) << endl;
        else if (y == 0) cout << (k % x == 0 ? 1 : 0) << endl;
        else cout << min(k / x, k / y) << endl;
    }
    return 0;
}
```

luogu P2249 【深基13.例1】查找

```c++
#include <iostream>
#include <algorithm>
using namespace std;
int nums[1000010];
int s;
bool check(int mid)
{
    if (nums[mid] >= s) return true;
    else return false;
}
int main()
{
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> nums[i];
    while (m--)
    {
        int l = 1, r = n;
        cin >> s;
        while (l < r)
        {
            int mid = l + r >> 1;
            if (check(mid)) r = mid;
            else l = mid + 1;
        }
        if (nums[l] == s) cout << l << ' ';
        else cout << "-1 ";
    }
    return 0;
}
```

luogu P1102 A-B 数对

```c++
#include <iostream>
#include <algorithm>
using namespace std;
long long nums[200010];
long long st, cnt;
int main()
{
    int n, c;
    cin >> n >> c;
    for (int i = 1; i <= n; i++) cin >> nums[i];
    sort(nums + 1, nums + 1 + n);
    for (int i = 1; i <= n; i++)
    {
        long long a = c + nums[i];
        int l = 1, r = n;
        while (l < r)
        {
            int mid = l + r >> 1;
            if (nums[mid] >= a) r = mid;
            else l = mid + 1;
        }
        if (nums[l] == a) st = l;
        else continue;
        l = st - 1, r = n;
        while (l < r)
        {
            int mid = l + r + 1 >> 1;
            if (nums[mid] <= a) l = mid;
            else r = mid - 1;
        }
        cnt += l - st + 1;
    }
    cout << cnt;
    return 0;
}
//
#include <iostream>
#include <algorithm>
using namespace std;
const int N = 2e5 + 5;
#define LL long long
LL nums[N], n, c, ans;
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    cin >> n >> c;
    for (int i = 1; i <= n; i++) cin >> nums[i];
    sort(nums + 1, nums + 1 + n);
    nums[n + 1] = INT64_MAX;
    for (int i = 1; i <= n; i++)
    {
        int ret = nums[i] + c;
        int x1 = lower_bound(nums + 1, nums + 2 + n, ret) - nums;
        int x2 = upper_bound(nums + 1, nums + 2 + n, ret) - nums;
        ans += x2 - x1;
    }
    cout << ans;
    return 0;
}


```

luogu P1678 烦恼的高考志愿

```c++
#include <iostream>
#include <algorithm>
using namespace std;
long long a[100010], sum, m, n, x;
int main()
{
    cin >> m >> n;
    for (int i = 1; i <= m; i++) cin >> a[i];
    sort(a + 1, a + 1 + m);
    a[0] = -1e12;
    a[m + 1] = 1e12;
    while (n--)
    {
        cin >> x;
        int l = 1, r = m + 1;
        while (l < r)
        {
            int mid = (l + r) / 2;
            if (a[mid] >= x) r = mid;
            else l = mid + 1;
        }
        sum += (a[l] - x) <= (x - a[l - 1]) ? (a[l] - x) : (x - a[l - 1]);
    }
    cout << sum;
    return 0;
}
```

luogu P1163 银行贷款

```c++
#include <iostream>
#include <algorithm>
using namespace std;
int sum, t, mon;
double sumt;
int check(double mid)
{
    sumt = sum;
    for (int i = 1; i <= mon; i++)
        sumt = sumt + sumt * mid - t;
    if (sumt > 0) return 1;
    else return 0;
}
int main()
{
    cin >> sum >> t >> mon;
    double l = 0, r = 500;
    while (r - l > 1e-5)
    {
        double mid = (r + l) / 2;
        if (check(mid)) r = mid;
        else l = mid;
    }
    printf("%.1f", l * 100);
    return 0;
}
```

luogu P2440 木材加工

```c++
#include <iostream>
#include <algorithm>
using namespace std;
int n, k, room[100010];
int check(int mid)
{
    int cnt = 0;
    for (int i = 1; i <= n; i++)
        cnt += room[i] / mid;
    if (cnt >= k) return true;
    else return false;
}
int main()
{
    cin >> n >> k;
    for (int i = 1; i <= n; i++) cin >> room[i];
    int l = 0, r = 1e8;
    while (l < r)
    {
        int mid = l + r + 1 >> 1;
        if (check(mid)) l = mid;
        else r = mid - 1;
    }
    cout << l;
    return 0;
}
```

luogu P1182 数列分段 Section II

```c++
#include <iostream>
#include <algorithm>
using namespace std;
long long n, m, room[100010], maxa;
int check(int mid)
{
    long long cnt = 0, sum = 0;
    for (int i = 1; i <= n - 1; i++)
    {
        sum += room[i];
        if (sum + room[i + 1] > mid) cnt++, sum = 0;
    }
    if (cnt + 1 <= m) return true;
    else return false;
}
int main()
{
    cin >> n >> m;
    for (int i = 1; i <= n; i++)
    {
        cin >> room[i];
        if (room[i] > maxa) maxa = room[i];
    }
    int l = maxa, r = 1e9;
    while (l < r)
    {
        int mid = l + r >> 1;
        if (check(mid)) r = mid;
        else l = mid + 1;
    }
    cout << l;
    return 0;
}
//l必须有意义，否则会出现无意义区间
//例如当样例为
//5 5
//4 2 4 5 1
//当mid为4时，cnt会变成5，导致r = mid, 此时区间为(1, 4],是无意义区间，会导致答案错误
```

luogu P8647 分巧克力

```c++
#include <iostream>
#include <algorithm>
using namespace std;
const int N = 2e5 + 5;
struct str
{
    int x, y;
}area[N];
int n, k, sum;
bool check(int mid)
{
    sum = 0;
    for (int i = 1; i <= n; i++)
        sum += (area[i].x / mid) * (area[i].y / mid);
    if (sum >= k) return true;
    else return false;
}
int main()
{
    cin >> n >> k;
    for (int i = 1; i <= n; i++) cin >> area[i].x >> area[i].y;
    int l = 1, r = 100000;
    while (l < r)
    {
        int mid = l + r + 1 >> 1;
        if (check(mid)) l = mid;
        else r = mid - 1;
    }
    cout << l << endl;
    return 0;
}
```

voj 跳石头

```c++
#include <iostream>
#include <algorithm>
using namespace std;
int d, n, m, ans, mid;
int a[50005];
bool Judge(int x)
{
    int sum = 0, i = 0, now = 0;
    while (i < n + 1)
    {
        i++;
        if (a[i] - a[now] < x)
            sum++;
        else now = i;
    }
    if (sum > m) return false;
    else return true;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    cin >> d >> n >> m;
    for (int i = 1; i <= n; i++) cin >> a[i];
    a[n + 1] = d; // 注意n并不包含头尾石头
    int l = 1, r = d;
    while (l <= r) // 二分法
    {
        mid = (l + r) / 2;
        if (Judge(mid))
        {
            ans = mid;
            l = mid + 1;
        }
        else r = mid - 1;
    }
    cout << ans << endl;
    return 0;
}
// // 0 1  2  3  4  5  6
// // 0 2 11 14 17 21 25
// //x = 12  5 2 3 4
// //r = 25 11 4 4 4
// //l = 0   0 0 3 4
```

Cable master

```c++
#include <iostream>
#include <algorithm>
#include <cmath>
using namespace std;
#define INT32_MAX 2147483647
int k, n;
double buf[10010], mid;
bool Judge(double a)
{
	int cnt = 0;
	for (int i = 0; i < k; i++)
		cnt += int(buf[i] / a);
	return cnt >= n;
}
int main()
{
	scanf("%d %d", &k, &n);
	for (int i = 0; i < k; i++)
		scanf("%lf", &buf[i]);
	double l = 0, r = INT32_MAX;
	while (r - l > 1e-5)
	{
		mid = (l + r) / 2;
		if (!Judge(mid)) r = mid;
		else l = mid;
	}
	printf("%.2f", floor(mid * 100) / 100); //注意必须利用floor向下取整，不能四舍五入
	return 0;
}
```

voj Freefall

此题之所以前面不过，是因为在最后没有考虑取整，因为用的是double算，而能过掉一些案例，是因为可能取的小数算的答案和正确结果相差不大，但是事实上我们是需要对它作向下取整和向上取整的判断的，因为你算的小数，两侧附近的整数点都可能是答案

```c++
//三分
//?
#include <iostream>
#include <algorithm>
#include <cmath>
using namespace std;
double a, b;
#define eps 1e-10
bool check(double lmid, double rmid)
{
	if ((lmid * b + a / sqrt(lmid + 1)) - (rmid * b + a / sqrt(rmid + 1)) > eps)
		return true;
	else return false;
}
int main()
{
	scanf("%lf%lf", &a, &b);
	double l = 0, r = a, lmid, rmid; //!
	while (l <= r)
	{
		lmid = l + (r - l) / 3;
		rmid = r - (r - l) / 3;
		if (check(lmid, rmid)) l = lmid + 1;
		else r = rmid - 1;
	}
	printf("%.10lf", l * b + a / sqrt(l + 1));
	return 0;
}
//AC
#include <iostream>
#include <algorithm>
#include <cmath>
using namespace std;
double a, b;
#define eps 1e-10
double f(double x)
{
    return x * b + a / sqrt(x + 1);
}
int main()
{
	scanf("%lf%lf", &a, &b);
	double l = 0, r = a, lmid, rmid; //!
	while (r - l > eps)
	{
		lmid = l + (r - l) / 3;
		rmid = r - (r - l) / 3;
		if (f(lmid) - f(rmid) > eps) l = lmid + 1;
		else r = rmid - 1;
	}
	printf("%.10f", min(f(ceil(l)), f(floor(l))));
	return 0;
}
//参考代码
#include <iostream>
#include <iomanip>
#include <cmath>
using namespace std;
using LL = long long;
int main()
{
    LL a, b;
    cin >> a >> b;
    auto f = [&](LL n) -> double 
    { 
        return (double) a / sqrt(n + 1) + (double) b * n;
    };
    LL l = 0, r = a / b;
    while (r - l > 2)
    {
        LL m1 = (l * 2 + r) / 3;
        LL m2 = (l + r * 2) / 3;
        //LL m1 = l + (r - l) / 3;  //这种分发也可以,有些小误差,但也能ac
        //LL m2 = r - (r - l) / 3;
        if (f(m1) > f(m2)) l = m1;
        else r = m2;
    }
    double ans = a;
    for (LL i = l; i <= r; i++)
    {
        ans = min(ans, f(i));
    }
    cout << fixed << setprecision(10) << ans << endl;
    return 0;
}

```

voj Last Rook

```c++
//TLE
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
int n, num, ax, ay, cnt, flag = 1;
int main()
{
	scanf("%d", &n);
	int up = 1, down = n; 
	while (up < down && flag)
	{
		int mid = up + (down - up) / 2;
		printf("? %d %d %d %d\n", up, mid, 1, n);
		cnt++;
		scanf("%d", &num);
		if (cnt > 20 || num == -1)
		{
			flag = 0;
			break;
		}
		if (num != (mid - up + 1)) down = mid;
		else up = mid + 1;
	}
	int l = 1, r = n;
	while (l < r && flag)
	{
		int mid = l + (r - l) / 2;
		printf("? %d %d %d %d\n", 1, up, l, mid);
		cnt++;
		scanf("%d", &num);
		if (cnt > 20 || num == -1)
		{
			flag = 0;
			break;
		}
		if (num != (mid - l + 1)) r = mid;
		else l = mid + 1;
	}
	if (flag) printf("! %d %d\n", up, l);
	return 0;
}
```

voj Pie

```c++
#include <iostream>
#include <algorithm>
#include <cmath>
using namespace std;
const double pi = acos(-1.0);
int t, m, f, buf[10010];
double ans;
bool check(double mid)
{
	int cnt = 0;
	for (int i = 0; i < m; i++)
		cnt += int((buf[i] * buf[i] * pi * 1.0) / mid);
	if (cnt >= f) return false;
	else return true;
}
int main()
{
	for (scanf("%d", &t); t--; )
	{
		scanf("%d%d", &m, &f);
		f++;
		for (int i = 0; i < m; i++) scanf("%d", &buf[i]);
		double l = 0, r = pi * 1e10;
		while (r - l >= 1e-6)
		{
			double mid = l + (r - l) / 2;
			if (check(mid))
			{
				ans = mid;
				r = mid;
			}
			else l = mid;
		}
		printf("%.4f\n", ans);
	}
	return 0;
}
```

voj Monthly Expense

```c++
#include <iostream>
#include <algorithm>
using namespace std;
int m, n, ans, nums[100010], bot = 0;
bool check(int mid)
{
	int cnt = 1, last = 0;
	for (int i = 1; i <= m; i++)
		if (nums[i] - nums[last] > mid) cnt++, last = i - 1;
	if (cnt > n) return false;
	else return true;
}
int main()
{
	while (scanf("%d%d", &m, &n) !=EOF)
	{
		bot = 0;
		for (int i = 1; i <= m; i++)
		{
			scanf("%d", &nums[i]);
			bot = max(bot, nums[i]);
			nums[i] += nums[i - 1];
		}
		int l = bot, r = nums[m]; //注意此处l不能是0或1，必须至少等于最大的序列和，否则会被压缩到无意义的区间
		while (l <= r)
		{
			int mid = l + (r - l) / 2;
			if (check(mid))
			{
				ans = mid;
				r = mid - 1;
			}
			else l = mid + 1;
		}
		printf("%d\n", ans);
	}
	return 0;
}

```

voj Yukari's Birthday

```c++
//？？？
#include <iostream>
#include <algorithm>
#include <cmath>
using namespace std;
#define LL long long
LL n, r, k, s;
LL binary(LL x)
{
    LL left = 2, right = n, sum = 0;
    while (left <= right)
    {
        sum = 0, s = 1;
        LL mid = left + (right - left) / 2;
        for (int i = 1; i <= x; i++)
        {
            s *= mid;
            sum += s;
            if (sum > n) break;
        }
        if (sum == n || sum == n - 1) return mid;
        else if (sum < n - 1) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    while (~scanf("%d", &n))
    {
        r = 1, k = n - 1;
        for (int i = 2; i <= 40; i++)
        {
            LL tmp = binary(i);
            if (tmp != -1 && tmp * i < r * k)
            {
                r = i;
                k = tmp;
            }
        }
        cout << r << " " << k << endl;
    }
    return 0;
}
```

voj Last Rock

```
注意点：
题中出现的刷新缓存区，这意味着要使用endl,这是C++交互代码必须要注意的,而且若使用'\n'代替endl,缓存区可能不会刷新,所以务必注意,但是有时使用'\n'也能ac,不必太在意.
与示例代码一样,将二叉搜索的段管理为半开放段可能很有用, [1, n + 1)以减少条件分支并帮助实现更容易(也取决于偏好)
此题中的超过20次会自动输出-1意味着提交错误,这个系统自己完成的,无需在程序中完成,这是个比较特别的判定,需要特别注意.
```

```c++
#include <iostream>
using namespace std;
int send(int a, int b, int c, int d)
{
    cout << "? " << a << " " << b << " " << c << " " << d << endl;
    cin >> a;
    return a;
}
int main()
{
    int N; 
    cin >> N;
    int u = 1, d = N + 1;
    while (u + 1 != d)
    {
        int m = (u + d) >> 1;
        int c = send(u, m - 1, 1, N);
        (c == m - u ? u : d) = m;
    }
    int l = 1, r = N + 1;
    while (l + 1 != r)
    {
        int m = (l + r) >> 1;
        int c = send(1, N, l, m - 1);
        (c == m - l ? l : r) = m;
    }
    cout << "!" << u << " " << l << endl;
    return 0;
}
//
#include <iostream>
using namespace std;
int n, num;
int main()
{
    cin >> n;
	int up = 1, down = n; 
	while (up < down)
	{
		int mid = up + (down - up) / 2;
        cout << "? " << up << ' ' <<  mid << ' ' << 1 << ' ' << n << endl;
        cin >> num;
		if (num != (mid - up + 1)) down = mid;
		else up = mid + 1;
	}
	int l = 1, r = n;
	while (l < r)
	{
		int mid = l + (r - l) / 2;
        cout << "? " << 1 << ' ' << n << ' ' << l << ' ' << mid << endl;
        cin >> num;
		if (num != (mid - l + 1)) r = mid;
		else l = mid + 1;
	}
    cout << "! " << up << ' ' << l << endl;
	return 0;
}
```

#### 三分法

P3382 【模板】三分法

```c++
#include<iostream>
#include<algorithm>
#include<cmath>
using namespace std;
double q[15];
double n, l, r;
#define eps 1e-6
double f(double x)
{
	double sum=0;
	for (int i = 1; i <= n + 1; i++)
        sum = sum * x + q[i];
	return sum;
}
int main()
{
	cin >> n >> l >> r;
	for (int i = 1;i <= n + 1;i++)
		cin >> q[i];
	while (r - l > eps)
    {
		double mid1 = l + (r - l) / 3;
		double mid2 = r - (r - l) / 3;
		if (f(mid1) < f(mid2)) l = mid1;
		else r = mid2;
	}
	printf("%.5f", l);
    return 0;
}
```

#### 前缀和与差分

```c++
#include <iostream>
using namespace std;


//一维前缀和
const int N = 1e5 + 10;
int m, n, l, r, sum[N], a[N];
int main()
{
   cin >> n >> m;
   for (int i = 1; i <= n; i++) cin >> a[i];
   for (int i = 1; i <= n; i++) //前缀和的初始化
       sum[i] = sum[i - 1] + a[i];
   //or 直接改变数组
   //for (int i = 1; i <= n; i++)
   //   a[i] = a[i - 1] + a[i];
    while (m--)
   {
       cin >> l >> r;
       cout << sum[r] - sum[l - 1] << endl; //区间和的计算
   }
   return 0;
}


//二维前缀和
const int N = 1010;
int n, m, q;
int s[N][N];
int main()
{
    scanf("%d%d%d", &n, &m, &q);
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= n; j++)
            scanf("%d", &s[i][j]);
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= n; j++)
            s[i][j] = s[i - 1][j] + s[i][j - 1] - s[i - 1][j - 1];
    while (q--)
    {
        int x1, x2, y1, y2;
        scanf("%d%d%d%d", &x1, &x2, &y1, &y2);
        printf("%d\n", s[x2][y2] - s[x1 - 1][y2] - s[x2][y1 - 1] + s[x1 - 1][y1 - 1]); 
    }
    return 0;
}


//一维差分
#include <iostream>
using namespace std;
const int N = 1e5 + 10;
int a[N], b[N];
int main()
{
    int n, m;
    scanf("%d%d", &n, &m);
    for (int i = 1; i <= n; i++)
    {
        scanf("%d", &a[i]);
        b[i] = a[i] - a[i - 1]; //构建差分数组
    }
    int l, r, c;
    while (m--)
    {
        scanf("%d%d%d", &l, &r, &c);
        b[l] += c; //表示将序列中[l, r]之间的每个数加上c
        b[r + 1] -= c;
    }
    for (int i = 1; i <= n; i++)
    {
        b[i] += b[i - 1]; //求前缀和运算
        printf("%d ", b[i]);
    }
    return 0;
}


//二维差分
#include <iostream>
using namespace std;
const int N = 1e3 + 10;
int a[N][N], b[N][N];
void insert(int x1, int x2, int y1, int y2, int c)
{
    b[x1][y1] += c;
    b[x2 + 1][y1] -= c;
    b[x1][y2 + 1] -= c;
    b[x2 + 1][y2 + 1] += c;
}
int main()
{
    int n, m, q;
    scanf("%d%d%d", &n, &m, &q);
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++)
            scanf("%d", &a[i][j]);
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++)
        {
            insert(i, j, i, j, a[i][j]); //构建差分数组
        }
    while (q--)
    {
        int x1, x2, y1, y2, c;
        scanf("%d%d%d%d", &x1, &x2, &y1, &y2);
        insert(x1, y1, x2, y2, c);
    }
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++)
        {
            b[i][j] += b[i - 1][j] + b[i][j - 1] - b[i - 1][j - 1]; //二维前缀和
        }
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            printf("%d", b[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```

[【新手课堂训练】前缀和、差分 - Virtual Judge (csgrandeur.cn)](https://vjudge.csgrandeur.cn/contest/532263#overview)

```c++
//Olympiad
#include <iostream>
using namespace std;
const int N = 1e5 + 10;
int buf[N];
int t, m, n;
bool Judge(int a)
{
    int cnt = 0, lib[10];
    while (a)
    {
        lib[cnt++] = a % 10;
        a /= 10;
    }
    for (int i = 0; i < cnt; i++)
        for (int j = i + 1; j < cnt; j++)
            if (lib[i] == lib[j]) return false;
    return true;
}
int main()
{
    for (int i = 0; i <= N; i++) if(Judge(i)) buf[i] = 1;
    for (int i = 1; i <= N; i++) buf[i] += buf[i - 1]; //构造前缀和
    for (scanf("%d", &t); t--; )
    {
        scanf("%d%d", &m, &n);
        printf("%d\n", buf[n] - buf[m - 1]);
    }
    return 0;
}
//本题中判断是否出现相同数字的方法
//本方法的关键在于明白，%的优先级大于>>大于&, %的优先级大于<<大于|=
bool Judge(int i)
{
    int flag = 0;
    for ( ; i; i / 10)
    {
        if (flag >> i % 10 & 1) return false; //先检查是否重复
        flag |= 1 << i % 10 ; //将1的二进制位向右移动i%10位，相当于储存了这个位的数
    }
    return true;
}
//可以用set或者map判断是否重复,此方法还不局限于判断不同位的数,可以用于判断数组的元素是否重复
//set
bool Judge(int i, set<int> &s)
{
    if (!i) return true;
    if(!s.count(i % 10)) s.insert(i % 10), Judge(i / 10);
    else return false;
}
int main()
{
    for (int i = 0; i <= N; i++) 
    {
        set<int> s; //注意set不能放在全局变量, 否则会出现奇怪错误
        if(Judge(i)) buf[i] = 1;
    }
    for (int i = 1; i <= N; i++) buf[i] += buf[i - 1]; //构造前缀和
    for (scanf("%d", &t); t--; )
    {
        scanf("%d%d", &m, &n);
        printf("%d\n", buf[n] - buf[m - 1]);
    }
    return 0;
}
//map
#include <iostream>
#include <map>
using namespace std;
const int N = 1e5 + 10;
int buf[N];
int t, m, n;
bool Judge(int i)
{
    map<int, bool> m;
    while (i)
    {
        if (m[i % 10]) return false;
        m[i % 10] = true;
        i /= 10;
    }
    return true;
}
int main()
{
    for (int i = 0; i <= N; i++) 
    {
        
        if(Judge(i)) buf[i] = 1;
    }
    for (int i = 1; i <= N; i++) buf[i] += buf[i - 1]; //构造前缀和
    for (scanf("%d", &t); t--; )
    {
        scanf("%d%d", &m, &n);
        printf("%d\n", buf[n] - buf[m - 1]);
    }
    return 0;
}


//Intense Heat
#include <iostream>
using namespace std;
const int N = 5010;
int num[N], buf[N];
int t, a, i;
double ans;
int main()
{
    scanf("%d%d", &t, &a);
    for (i = 1; i <= t; i++)
    {
        scanf("%d", &num[i]);
        num[i] += num[i - 1];
    }
    for (int h = a; h <= t; h++)
        for (int i = h; i <= t; i++)
            ans = max(ans, 1.0 * (num[i] - num[i - h]) / h);
    printf("%.8f", ans);
    return 0;
}



//Color the ball
#include <iostream>
#include <cstring>
using namespace std;
const int N = 1e5 + 10;
int t, ret, a, b, room[N];
int main()
{
    while (scanf("%d", &t), ret = t)
    {
        memset(room, 0, sizeof room);
        while (ret--)
        {
            scanf("%d%d", &a, &b);
            room[a] += 1;
            room[b + 1] -= 1;
        }
        for (int i = 1; i <= t; i++)
        {
            room[i] += room[i - 1];
            printf(" %d" + !(i - 1), room[i]);
        }
        printf("\n");
    }
    return 0;
}


//Tallest Cow
#include <cstdio>
#include <cstring>
#include <map>
#include <iostream>
#include <algorithm>
using namespace std;
const int N = 1e5 + 10;
int room[N], n, i, h, r, a, b;
map<pair<int, int>, bool> existed;
int main()
{
    scanf("%d%d%d%d", &n, &i, &h, &r);
    while (r--)
    {
        scanf("%d%d", &a, &b);
        if (a > b) swap(a, b);
        if (existed[make_pair(a, b)]) continue;
        room[a + 1] -= 1;
        room[b] += 1;
        existed[make_pair(a, b)] = true;
    }
    for (int i = 1; i <= n; i++)
    {
        room[i] += room[i - 1];
        printf("%d\n", room[i] + h);
    }
    return 0;
}
//set
#include<cstdio>
#include<cstring>
#include<cstdlib>
#include<algorithm>
#include<queue>
#include<set>
const int maxn = 1e4 + 10;
int N, I, H, R, a, b;
int ms[maxn];
int main() {
    while(scanf("%d%d%d%d", &N, &I, &H, &R) != EOF) {
        memset(ms, 0, sizeof(ms));
        std::set<int> s;
        for(int i = 0; i < R; i ++) {
            scanf("%d%d", &a, &b);
            if(a > b) std::swap(a, b);
            if(s.count(a * maxn + b)) continue; //用*maxn巧妙化两个数为一个数储存
            s.insert(a * maxn + b); // 重复的a, b只算一次
            ms[a + 1] --;
            ms[b] ++;
        }
        for(int i = 1; i <= N; i ++)
            ms[i] += ms[i - 1];
        for(int i = 1; i <= N; i ++)
            printf("%d\n", ms[i] + H);
    }
    return 0;
}



//最大子矩阵
#include <cstdio>
#include <cstring>
#include <map>
#include <iostream>
#include <algorithm>
using namespace std;
const int N = 1e3 + 10;
int buf[N][N], t, m, n, x, y, tmp, res;
int main()
{
    for (scanf("%d", &t); t--; )
    {
        scanf("%d%d%d%d", &m, &n, &x, &y);
        for (int i = 1; i <= m; i++)
            for (int j = 1; j <= n; j++)
                scanf("%d", &buf[i][j]);
        for (int i = 1; i <= m; i++)
            for (int j = 1; j <= n; j++)
                buf[i][j] += buf[i][j - 1] + buf[i - 1][j] - buf[i - 1][j - 1];
        x--;y--;
        for (int i = 1; i <= m - x; i++)
            for (int j = 1; j <= n - y; j++)
            {
                tmp = buf[i + x][j + y] - buf[i + x][j - 1] - buf[i - 1][j + y] + buf[i - 1][j - 1]; 
                res = max(tmp, res);
            }
        printf("%d\n", res);
    }
    return 0;
}


//sum
#include <cstdio>
#include <cstring>
#include <map>
#include <iostream>
#include <algorithm>
using namespace std;
const int N = 1e5 + 10;
int buf[N], t, n, m;
bool Judge()
{
    if (n > m) return true;
    for (int i = 1; i <= n; i++)
        for (int j = 0; j < i; j++)
            if (buf[i] - buf[j] == m) return true;
    return false;
}
int main()
{
    for (scanf("%d", &t); t--; )
    {
        scanf("%d%d", &n, &m);
        for (int i = 1; i <= n; i++)
        {
            scanf("%d", &buf[i]);
            buf[i] += buf[i - 1];
        }
        printf(Judge() ? "YES\n" : "NO\n");
    }
    return 0;
}
//TLE
#include <cstdio>
#include <iostream>
#include <algorithm>
using namespace std;
const int N = 1e5 + 10;
int buf[N], t, n, m;
bool Judge()
{
    for (int i = 1; i <= n; i++)
        for (int j = i; j <= n; j++)
         //if (!((buf[j] - buf[j - i]) % m)) return true;  TLE
    	//if (!((buf[j] - buf[i - 1]) % m)) return true;  AC
        //暴搜在处理顺序上不同造成超时
    return false;
}
int main()
{
    for (scanf("%d", &t); t--; )
    {
        scanf("%d%d", &n, &m);
        for (int i = 1; i <= n; i++)
        {
            scanf("%d", &buf[i]);
            buf[i] += buf[i - 1];
        }
        if (Judge()) printf("YES\n");
        else printf("NO\n");
    }
    return 0;
}



//Monitor HDU
#include <cstdio>
#include <cstring>
#include <vector>
#include <iostream>
#include <algorithm>
const int N = 1e7;//题目中n*m <= 10^7, 所以可能会出现1 * 1e7的情况, 但是不能开辟[1e7][1e7]的二维数组,因为会爆堆栈,必须采用动态数组vector
using namespace std;
int n, m, p, q;
int main()
{
    int x1, x2, y1, y2;//注意：由于cmath头文件里面定义了y1,j0,j1,jn,y0,yn(均用于贝塞尔函数解)，所以这些变量尽量不用在全局变量中，例如这里的y1，如果定义在全局变量，会报错
    while(~scanf("%d%d", &n, &m))
    {
        vector<vector<int> > buf(n + 10, vector<int>(m + 10, 0));//vector嵌套, 相当于动态二维数组
        for (scanf("%d", &p); p--; )
        {
            scanf("%d%d%d%d", &x1, &y1, &x2, &y2);
            buf[x1][y1] += 1;
            buf[x2 + 1][y1] -= 1;
            buf[x1][y2 + 1] -= 1;
            buf[x2 + 1][y2 + 1] += 1;
        }
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= m; j++)
                    buf[i][j] += buf[i - 1][j] + buf[i][j - 1] - buf[i - 1][j - 1];
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= m; j++)
                buf[i][j] = (!!buf[i][j]) + buf[i][j - 1] + buf[i - 1][j] - buf[i - 1][j - 1];
                //巧妙双取反, 直接使非零数变为1
        for (scanf("%d", &q); q--; )
        {
            scanf("%d%d%d%d", &x1, &y1, &x2, &y2);
            int sum = buf[x2][y2] + buf[x1 - 1][y1 - 1] - buf[x2][y1 - 1] - buf[x1 - 1][y2];
            printf(sum == (x2 - x1 + 1) * (y2 - y1 + 1) ? "YES\n" : "NO\n");
        }
    }
    return 0;
}
//* * * * * *
//* + + + * *
//* + + + + +
//* + + + + +
//+ + + + + +
//+ + * * * *
```

#### 分治法

大整数乘法

```c++
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <cmath>
using namespace std;
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

[【寒期集训-入门组】复杂度分析、分治思想 - Virtual Judge (csgrandeur.cn)](https://vjudge.csgrandeur.cn/contest/535280#overview)

A - 汉诺塔问题(Tower of Hanoi)

```c++
#include <iostream>
using namespace std;
char a, b, c;
int n;
void print(int n, char a, char b, char c)
{
    printf("%d:%c->%c\n", n, a, c);
}
void solve(int n, char a, char b, char c)
{
    if (!n) return;
    solve(n - 1, a, c, b);
    print(n, a, b, c);
    solve(n - 1, b, a, c);
}
int main()
{
    cin >> n >> a >> b >> c;
    solve(n, a, b, c);
    return 0;
}
```

B - 快速排序

```c++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
vector<int> v;
int n, tmp;
void my_sort(int tmp)
{
    int a = lower_bound(v.begin(), v.begin() + v.size(), tmp) - v.begin();
    v.insert(v.begin() + a, tmp);
}
int main()
{
    cin >> n;
    for (int i = 1; i <= n; i++)
    {
        cin >> tmp;
        my_sort(tmp);
    }
    
    for (auto it = v.begin(); it != v.end(); it++)
    {
        if (it == v.begin()) cout << *it;
        else cout << " " << *it;
        if (it == v.end() - 1) cout << endl;
    }
}
```

C - 逆序对

**归并排序: 查找逆序对的对数, 建立在归并操作上的一种有效排序算法, 采用的是分治法(二分法)**

**时间复杂度: O(nlogn)**		**空间复杂度: O(n)**

该算法首先将一个序列进行二分, 直到分解成n个元素(l == r); 从最小长度的区间(2)开始对子序列排序(二分到最后的时候一个元素一定是有序的) , 同时要把每个子序列的逆序列对数加起来, 然后合并已经有序的子序列, 有序的子序列便于后面再找逆序列, 同时该子序列内的数不再参与和自身序列的数的结合, 注意每次都要将已有序的b数组复制到a数组(原数组)中, 这就是排序与合并的体现.

```c++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
const int N = 5e5 + 1;
int n, a[N], b[N];
long long ans;
void msort(int l, int r)
{
    int mid = (l + r) / 2;
    if (l == r) return;
    else
    {
        msort(l, mid);
        msort(mid + 1, r);
    }
    int i = l, j = mid + 1, t = l;
    while (i <= mid && j <= r)
    {
        if (a[i] > a[j])
        {
            ans += mid - i + 1;
            b[t++] = a[j];
            j++;
        }
        else
        {
            b[t++] = a[i];
            i++;
        }
    }
    while (i <= mid)
    {
        b[t++] = a[i];
        i++;
    }
    while (j <= r)
    {
        b[t++] = a[j];
        j++;
    }
    for (int i = l; i <= r; i++) a[i] = b[i];
    return;
}
int main()
{
    cin >> n;
    for (int i = 1; i <= n; i++)
        cin >> a[i];
    msort(1, n);
    cout << ans;
    return 0;
}
```

D - 最大子段和

```c++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
int n, ans = -1e4, ret, sum;
int main()
{
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        cin >> ret;
        sum = sum > 0 ? sum : 0;
        sum += ret;
        ans = max(ans, sum);
    }
    cout << ans;
    return 0;
}
```

E - Fractal

尽量不要使用pow函数再使用除法吧, 感觉会出现很多问题, 手写pow函数或许更安全

```c++
#include <iostream>
#include <algorithm>
#include <cmath>
using namespace std;
char room[1005][1005];
void solve(int n, int a, int b)
{
    if (n == 1)
    {
        room[a][b] = 'X';
        return;
    }
    int d = pow(3.0, n - 2);
    solve(n - 1, a, b);
    solve(n - 1, a, b + d * 2);
    solve(n - 1, a + d, b + d);
    solve(n - 1, a + d * 2, b);
    solve(n - 1, a + d * 2, b + d * 2);
}
int main()
{
    int n;
    for (int i = 0; i <= 750; i++)
        for (int j = 0; j <= 750; j++)
            room[i][j] = ' ';
    while (cin >> n && n != -1)
    {
        solve(n, 0, 0);
        for (int i = 0; i < pow(3.0, n - 1); i++)
            {
                for(int j = 0; j < pow(3.0, n - 1); j++)
                    cout << room[i][j];
                cout << endl;
            }
        cout << "-" << endl;
    }
    return 0;
}
```

F - 很大的数组的第k小

**快速排序: 用于寻找第k大(第k小)的数, 时间复杂度为O(n)**

这道题可作为**快速排序**的模板题, 需要记忆. 快速排序的核心思想是在要排序的数组中选择一个数, 然后将数组中比这个数小的放在这个数的左边, 比这个数大的放在他的右边, 现在我们要找第k小的数, 那么如果在数组中选了一个数, 用快排的方法, 将比这个数小的数都放在它的左边, 而左边的数(加标签个数), 若小于k个, 说明这个数应该在标签的右边,  若大于k个, 说明在标签左边, 若刚好等于k, 说明这个标签正是我们要找的数. 

```c++
#include<cstdio>
#include<cstring>
#include<cstdlib>
using namespace std;
const int mod = 1e9 + 7;
const int maxn = 5e7 + 10;
int n, m, k, a[maxn];
int Quickfind(int l, int r, int k)
{
    if (l >= r - 1) return a[l];
    int low = l, high = r - 1, center = a[low];
    while (low < high)
    {
        while (low < high && a[high] >= center) high--;
        a[low] = a[high];
        while (low < high && a[low] <= center) low++;
        a[high] = a[low];
    }
    a[low] = center;
    if (k == low - l + 1) return a[low];
    if (k < low - l + 1) return Quickfind(l, low, k);
    return Quickfind(low + 1, r ,k - low + l - 1);
}
int main()
{
    while (scanf("%d%d%d", &n, &m, &k) != EOF)
    {
        a[0] = m;
        for (int i = 1; i < n; i++)
            a[i] = 1LL * a[i - 1] * m % mod;
        printf("%d\n", Quickfind(0, n, k));
    }
    return 0;
}
```

G - 地毯填补问题

考虑`2*2`的情况，一个地毯可以搞定.

考虑`4*4`的情况，是`4`个`2*2`的子问题拼成的，且只有一个子问题里包含公主的位置.

如果在中间的`4`个格子放一块地毯，形状是覆盖三个不包含公主的子问题，相当于这三个子问题各被占据了一个格子，都把被占据的格子当作公主的话，那么`4`个子问题就都是有一个公主的子问题了.

![img](https://user-images.githubusercontent.com/5326601/209115340-158f67a9-879b-41d0-a958-e76db6323d50.png)

那么分治策略就是，不断把问题分成`4`个子问题，每次都将中间`4`个格子放一块地毯，缺口留给有公主的那个子问题.

```c++
//CSGrandeur
#include<cstdio>
#include<cstring>
#include<cstdlib>
int k, px, py;
void DFS(int cur, int x, int y, int tpx, int tpy) {
    int ps = (tpx - x) / cur << 1 | (tpy - y) / cur, c = ps ^ 3;
    printf("%d %d %d\n", x + cur + (c >> 1), y + cur + (c & 1), ps + 1);
    if(cur == 1) return;
    DFS(cur >> 1, x, y, ps == 0 ? tpx : x + cur - 1, ps == 0 ? tpy : y + cur - 1);
    DFS(cur >> 1, x, y + cur, ps == 1 ? tpx : x + cur - 1, ps == 1 ? tpy : y + cur);
    DFS(cur >> 1, x + cur, y, ps == 2 ? tpx : x + cur, ps == 2 ? tpy : y + cur - 1);
    DFS(cur >> 1, x + cur, y + cur, ps == 3 ? tpx : x + cur, ps == 3 ? tpy : y + cur);
}
int main() {
    while(scanf("%d", &k) != EOF) {
        scanf("%d%d", &px, &py);
        px --, py --;
        DFS(1 << k - 1, 0, 0, px, py);        
    }
    return 0;
}

//
#include <algorithm>
#include <iostream>
#include <cstring>
#include <queue>
#include <map>
using namespace std;
int n, k, a[1201][1201];
void dfs(int x1, int y1, int x2, int y2, int X, int Y)
{
    if (x2 - x1 == 1 && y2 - y1 == 1)
    {
        if (X == x1 && Y == y1) printf("%d %d 1\n", x2, y2);
        if (X == x1 && Y == y2) printf("%d %d 2\n", x2, y1);
        if (X == x2 && Y == y1) printf("%d %d 3\n", x1, y2);
        if (X == x2 && Y == y2) printf("%d %d 4\n", x1, y1);
        return;
    }
    int x = (x2 - x1 + 1) / 2 + x1 - 1;
    int y = (y2 - y1 + 1) / 2 + y1 - 1;
    if (X <= x && Y <= y)
    {
        dfs(x1, y1, x, y, X, Y);
        printf("%d %d 1\n", x + 1, y + 1);
        dfs(x + 1, y1, x2, y, x + 1, y);
        dfs(x + 1, y + 1, x2, y2, x + 1, y + 1);
        dfs(x1, y + 1, x, y2, x, y + 1);
    }
    if (X <= x && Y > y)
    {
        dfs(x1, y + 1, x, y2, X, Y);
        printf("%d %d 2\n", x + 1, y);
        dfs(x1, y1, x, y, x, y);
        dfs(x + 1, y1, x2, y, x + 1, y);
        dfs(x + 1, y + 1, x2, y2, x + 1, y + 1);
    }
    if (X > x && Y <= y)
    {
        dfs(x + 1, y1, x2, y, X, Y);
        printf("%d %d 3\n", x, y + 1);
        dfs(x + 1, y + 1, x2, y2, x + 1, y + 1);
        dfs(x1, y1, x, y, x, y);
        dfs(x1, y + 1, x, y2, x, y + 1);
    }
    if (X > x && Y > y)
    {
        dfs(x + 1, y + 1, x2, y2, X, Y);
        printf("%d %d 4\n", x, y);
        dfs(x1, y1, x, y, x, y);
        dfs(x1, y + 1, x, y2, x, y + 1);
        dfs(x + 1, y1, x2, y, x + 1, y);
    }
}
int main()
{
    int x, y;
    scanf("%d%d%d", &k, &x, &y);
    dfs(1, 1, 1 << k, 1 << k, x, y);
    return 0;
}
```

H - 快速幂||取余运算

快速幂，就是快速计算某个数的n次幂。其时间复杂度为 O(log₂N)， 与朴素的O(N)相比效率有了极大的提高

```c++
#include <iostream>
using namespace std;
int PowMod(int a, int n, int mod)
{
    int ret = 1;
    for ( ; n; n >>= 1, a = 1LL * a * a % mod)
        if (n & 1) ret = 1LL * ret * a % mod;
    return ret;
}
int main()
{
    int a, b, p;
    while (scanf("%d%d%d", &a, &b, &p) != EOF)
        printf("%d^%d mod %d=%d\n", a, b, p, PowMod(a, b, p));
    return 0;
}
```

I - 矩阵快速幂

矩阵的快速幂与整数快速幂原理相同，只不过答案矩阵的初始状态不再是1，而是一个单位矩阵，因为单位矩阵在矩阵中的作用等同于整数中的1。因此矩阵快速幂的思路就是先定义好矩阵类型，再定义矩阵乘法，然后定义矩阵快速幂的函数。

```c++
//ygtrece
#include <iostream>
#include <cstring>
using namespace std;
#define LL long long
const LL mod = 1e9 + 7;
LL n, k;
struct matrix
{
    LL mat[100][100];
    void init ()
    {
        memset(mat, 0, sizeof mat);
    }
};
matrix mul(matrix a, matrix b) //return a * b
{
    matrix c;
    c.init();
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            for (int k = 0; k < n; k++)
            {
                c.mat[i][j] += ((a.mat[i][k] % mod) * (b.mat[k][j] % mod)) % mod;
                c.mat[i][j] %= mod;
            }
    return c;
}
matrix fast_pow(matrix A, LL k) //return A ^ k % mod
{
    matrix B;
    B.init();
    for (int i = 0; i < n; i++) B.mat[i][i] = 1; //单位矩阵
    for ( ; k; k >>= 1, A = mul(A, A))
        if (k & 1) B = mul(A, B);
    return B;
}
int main()
{
    while (scanf("%lld%lld", &n, &k) != EOF)
    {
        matrix M;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                cin >> M.mat[i][j];
        matrix T = fast_pow(M, k);
        for (int i = 0; i < n; i++, printf("\n"))
            for (int j = 0; j < n; j++)
                printf(" %d" + !j, T.mat[i][j]);
    }
    return 0;
}
//CSGrandeur
#include <cstdio>
#include <vector>
using namespace std;
long long n, k;
const int mod =1e9 + 7;
struct Mat
{
    vector<vector<int>> v;
    int n;
    Mat(int n_, int val = 0)
    {
        n = n_;
        v = vector<vector<int>>(n + 10, vector<int>(n + 10, val));
    }
    Mat operator*=(const Mat &that)
    {
        vector<vector<int>> c(n + 10, vector<int>(n + 10, 0));
        for (int i = 0; i < n; i++)
            for (int k = 0; k < n; k++)
            {
                int tmp = v[i][k];
                for (int j = 0; j < n; j++)
                    c[i][j] = (c[i][j] + 1LL * tmp * that.v[i][j] % mod) % mod;
            }
            v.swap(c);
            return *this;
    }
};
Mat PowMat(Mat &a, long long k)
{
    Mat ret(n);
    for (int i = 0; i < n; i++) ret.v[i][i] = 1;
    for (; k; k >>= 1, a *= a)
        if (k & 1) ret *= a;
    return ret;
}
int main()
{
    while (scanf("%lld%lld", &n, &k) != EOF)
    {
        Mat a(n);
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                scanf("%d", &a.v[i][j]);
        a = PowMat(a, k);
        for (int i = 0; i < n; i++, printf("\n"))
            for (int j = 0; j < n; j++)
                printf(" %d" + !j, a.v[i][j]);
    }
    return 0;
}
```

J - Fibonacci

计算**斐波那契数列**的重要方法: 矩阵快速幂

```c++
//ygtrece
#include <cstdio>
#include <cstring>
using namespace std;
long long n, k;
const int mod = 1e4;
struct matrix
{
    long long mat[2][2];
    void init()
    {
        memset(mat, 0, sizeof mat);
    }
};
matrix mul(matrix A, matrix B)
{
    matrix C;
    C.init();
    for (int i = 0; i < 2; i++)
        for (int j = 0; j < 2; j++)
            for (int k = 0; k < 2; k++)
            {
                C.mat[i][j] += ((A.mat[i][k] % mod) * (B.mat[k][j] % mod)) % mod;
                C.mat[i][j] %= mod;  
            }
    return C;
}
matrix fast_pow(matrix A, long long k)
{
    matrix B;
    B.init();
    for (int i = 0; i < 2; i++) B.mat[i][i] = 1;
    for (; k; k >>= 1, A = mul(A, A))
        if (k & 1) B = mul(A, B);
    return B;
}
int main()
{
    while (scanf("%lld", &n) != EOF && n != -1)
    {
        matrix A;
        A.mat[0][0] = 1; A.mat[1][0] = 1;
        A.mat[0][1] = 1; A.mat[1][1] = 0;
        matrix M = fast_pow(A, n + 1);
        printf("%lld\n", M.mat[1][1]);
    }
    return 0;
}
//1 1
//1 0

//2 1
//1 1

//3 2
//2 1

//5 3
//3 2


//CSGrandeur
#include<cstdio>
#include<cstring>
#include<cstdlib>
#include<vector>
const int mod = 10000;
using std::vector;
struct Mat {
    vector<vector<int> > v;
    int n;
    Mat(int n_, int val=0){
        n = n_;
        v = vector<vector<int> >(n + 10, vector<int>(n + 10, val));
    }
    Mat operator*=(const Mat &that) {
        vector<vector<int> > c(n + 10, vector<int>(n + 10, 0));
        for(int i = 0; i < n; i ++){
            for(int k = 0; k < n; k ++) {
                int tmp = v[i][k];
                for(int j = 0; j < n; j ++)
                    c[i][j] = (c[i][j] + 1LL * tmp * that.v[k][j] % mod) % mod;
            }
        }
        v.swap(c);
        return *this;
    }
};
int n;
Mat PowMat(Mat &a, int k)
{
    Mat ret(2);
    for(int i = 0; i < 2; i ++) {
        ret.v[i][i] = 1;
    }
    for(; k; k >>= 1, a *= a)
        if(k & 1) ret *= a;
    return ret;
}
int main() {
    while(scanf("%d", &n) != EOF && n != -1) {
        Mat a(2);
        a.v[0][0] = 1, a.v[0][1] = 1; 
        a.v[1][0] = 1, a.v[1][1] = 0; 
        a = PowMat(a, n + 1);
        printf("%d\n", a.v[1][1]);
    }
    return 0;
}
```

#### 贪心法与拟阵

[校题](https://vjudge.csgrandeur.cn/contest/526923)

```c++

//find amir
int main()
{
    int n;
    cin >> n;
    if(n % 2 == 0)  cout << n / 2 - 1;
    else cout << n / 2;
    return 0;
}

//智力大冲浪
struct str
{
    int time;
    int money;
}game[600];

bool cmp(str a, str b)
{
    return a.money > b.money;
}
int main()
{
    int m, n, sum = 0, save = 0;
    cin >> m >> n;
    for(int i = 1; i <= n; i++)  cin >> game[i].time;
    for(int i = 1; i <= n; i++)  cin >> game[i].money;
    int lib[600] = {0};
    sort(game + 1, game + n + 1, cmp);
    for(int i = 1; i <= n; i++)
    {
        for(int j = game[i].time; j >= 0; j--)
        {
            if(lib[j] == 0) 
            {
                lib[j] = game[i].money;
                break;
            }
        }
    }
    for(int i = 1; i <= n; i++)
    {
        save += lib[i];
        sum  += game[i].money;
        if(i == n)  m -= sum - save; 
    }
    cout << m << endl;
    return 0;
}

//数组
struct str
{
    int b;
    int e;
}line[1000000];

bool cmp(str a, str b)
{
    return a.e < b.e;
}

int main()
{
    int n;
    cin >> n;
    for(int i = 0; i < n; i++)  cin >> line[i].b >> line[i].e;
    sort(line, line + n, cmp);
    int cnt = 0, endline = 0;
    for(int i = 0; i < n; i++)
    {
        if(line[i].b >= endline)
        {
            cnt++;
            endline = line[i].e;
        }
    }
    cout << cnt;
    return 0;
}

//田忌赛马
int Race(int a[], int b[], int n, int flag)
{
    int fa = 1, fb = 1;
    int la = n, lb = n;
    int as = 0, bs = 0;
    for(int i = 1; i <= n; i++)
    {
        if(a[fa] > b[fb])
        {
            fa++;   fb++;
            as += 3;    bs += 1;
        }
        else if(a[la] > b[lb])
        {
            la--;   lb--;
            as += 3;    bs += 1;
        }
        else if(a[la] < b[fb])
        {
            la--;   fb++;
            as += 1;    bs += 3;   
        }
        else if(a[la] == b[fb])
        {
            as += 2;    bs += 2;
        }
    }
    if(!flag)   return as;
    else    return bs;
}
bool cmp(int a, int b)
{
    return a > b;
}
int main()
{
    int n, fa, fb,la, lb, flag = 0, max, min;
    int c[10000], s[10000];
    while(cin >> n && n != 0)
    {
        flag = 0;
        for(int i = 1; i <= n; i++) cin >> c[i];
        for(int i = 1; i <= n; i++) cin >> s[i];
        sort(c + 1, c + 1 + n, cmp);
        sort(s + 1, s + 1 + n, cmp);
        max = Race(s, c, n, flag++);
        min = Race(c, s, n, flag);
        cout << max << ' ' << min << endl;
    }
    return 0;
}

//最大整数
int main()
{
    int t;
    char lib[100];
    cin >> t;
    while (t--)
    {
        memset(lib, '\0', 100);
        int k;
        cin >> lib >> k;
        int len = strlen(lib);
        while(k--)
        {
            for(int i = 0; i < len; i++)
            {
                if(lib[i] > lib[i + 1])
                {
                    for(int j = i; j < len; j++)    lib[j] = lib[j + 1];
                    break;
                }
            }
        }
        cout << lib << endl;
    }
    return 0;
}


//电池的寿命
bool comparision(int a, int b)
{
    return a < b;
}
int main()
{
    int n;
    double sum = 0;
    int time[1010];
    while (scanf("%d", &n) != EOF)
    {
        sum = 0;
        for (int i = 0; i < n; i++)
            cin >> time[i];
        sort(time, time + n, comparision);
        for(int i = 0; i < n; i++)
        {
            sum += time[i];
            if(i == n - 1 && sum <= 2 * time[n - 1])   sum -= time[n - 1];
            else if(i == n - 1 && sum > 2 * time[n - 1])    sum /= 2;
        }
        cout << fixed << setprecision(1) << sum << endl;
    }
    return 0;
}


//种树
struct str
{
    int b;
    int e;
    int cnt;
};

bool comparition(str a, str b)
{
    return a.e < b.e;
}
int main()
{
    int path, n, sum = 0;
    cin >> path >> n;
    str adv[5100];
    for(int i = 0; i < n; i++)  cin >> adv[i].b >> adv[i].e >> adv[i].cnt;
    sort(adv, adv + n, comparition);
    int book[31000] = {0};
    for(int i = 0; i < n; i++)
    {
        for(int j = adv[i].e; j >= adv[i].b; j--)
        {
            if(book[j] == 1)    adv[i].cnt--;    
        }
        for(int j = adv[i].e; j >= adv[i].b; j--)
        {
            if(adv[i].cnt <= 0) break;
            if(book[j] == 0)
            {
                adv[i].cnt--;
                sum++;
                book[j] = 1;
            }
        }
    }
    cout << sum;
    return 0;
}


//圣诞老人的礼物
struct str
{
    int value;
    int  weigh;
};

bool myfunction(str i, str j)
{
    return (1.0 * i.value / i.weigh) >(1.0 * j.value / j.weigh);
}
int main()
{
    int m, n;
    double sum = 0;
    cin >> m >> n;
    str gift[1000];
    for(int i = 0; i < m; i++)  cin >> gift[i].value >> gift[i].weigh;
    sort(gift, gift + m, myfunction);
    for(int i = 0; i < m; i++)
    {
        if(n > gift[i].weigh)   
        {
            sum += gift[i].value;
            n = n - gift[i].weigh;
        }
        else    
        {
            sum += gift[i].value / gift[i].weigh * n* 1.0;
            break;
        }
    }
    cout << fixed << setprecision(1) << sum << endl;
    return 0;
}


//电影节
struct Film
{
    int f;
    int e;
};
bool operator<(const Film &t, const Film &c)
{
    if (t.e == c.e)
        return t.f < c.f;
    else
        return t.e < c.e;
}
int main()
{
    struct Film film[1100];
    int n;
    while (scanf("%d", &n) && n != 0)
    {
        for (int i = 0; i < 1100; i++)
            film[i].e = film[i].f = 0;
        for (int i = 0; i < n; i++)
            cin >> film[i].f >> film[i].e;
        sort(film, film + n);
        int total = 0;
        int first = 0;
        for (int i = 0; i < n; i++)
            if (film[i].f >= first)
            {
                total++;
                first = film[i].e;
            }
        cout << total << endl;
    }
    return 0;
}

```

[11. 盛最多水的容器 - 力扣（Leetcode）](https://leetcode.cn/problems/container-with-most-water/discussion/)

```c++
class Solution {
public:
    int maxArea(vector<int>& height) {
        int i = 0, j = height.size() - 1, res = 0;
        while(i < j) {
            res = height[i] < height[j] ? 
                max(res, (j - i) * height[i++]): 
                max(res, (j - i) * height[j--]); 
        }
        return res;
    }
};
```

[45. 跳跃游戏 II - 力扣（Leetcode）](https://leetcode.cn/problems/jump-game-ii/)

```c++
class Solution {
public:
int jump(vector<int>& nums) 
{
    int cnt = 0, fin = nums.size() - 1; 
    while (true)
    {
        if (fin == 0)   break;
        for (int i = 0; i < fin; i++)
        {
            if (i + nums[i] >= fin)
            {
                fin = i;
                cnt++;
                break;
            }
        }
    }
    return cnt;
}
};

//

class Solution {
public:
    int jump(vector<int>& nums) 
{
    int maxPos = 0, bar = 0, n = nums.size(), cnt = 0;
    for (int i = 0; i < n - 1; i++)
    {
        maxPos = max(maxPos, i + nums[i]);
        if (i == bar)    
        {
            bar = maxPos;
            cnt++;
        }
    }
    return cnt;
}
};
```

[55. 跳跃游戏 - 力扣（Leetcode）](https://leetcode.cn/problems/jump-game/description/)

```c++
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int k = 0;
        for(int i = 0; i < nums.size(); i++)
        {
            if(i > k)   return false;
            k = max(k, i + nums[i]);
        }
        return true;
    }
};
```

[122. 买卖股票的最佳时机 II - 力扣（Leetcode）](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/discussion/)

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) 
    {
        int i = 0, sum = 0, min;
        while(i < prices.size() - 1)
        {
            if(prices[i + 1] > prices[i])   sum += prices[i + 1] - prices[i];
            i++;
        }
        return sum;
    }
};
```

[ 洛谷 ](https://www.luogu.com.cn/problem/list?keyword=贪心&page=1)

```c++
//P1614 爱与愁的心痛
int main()
{
    int n, m, a, res = 1<<30;
    cin >> n >> m;
    vector<int> vec;
    for (int i = 0; i < n; i++)
    {
        cin >> a;
        vec.push_back(a);
    }
    for (int i = 0; i < n - m + 1; i++)
    {
        int sum = 0;
        for (int j = 0; j < m; j++)
        {
            sum += vec[j + i];
        }
        res = min(res, sum);
    }
    cout << res;
    return 0;
}

//P7814 「小窝 R3」心の記憶
#include <cstdio>
#include <vector>
using namespace std;
int main()
{
    int T;
    scanf("%d", &T);
    while (T--)
    {
        int m, n;
        scanf("%d%d", &n, &m);
        vector<bool> a(m + 10);
        for (int i = 1; i <= n; i++)
        {
            int x;
            scanf("%1d", &x);
            a[i] = x;
        }
        if (n == m || n == 1 || (n == 2 && (a[1] ^ a[2])))
        {
            puts("-1");
            continue;
        }
        int cnt0 = 0, cnt1 = 0;
        for (int i = 1; i <= n; i++)
            a[i] ? cnt1++ : cnt0++;
        bool f = false;
        for (int i = 1; i <= n; i++)
        {
            printf("%d", int(a[i]));
            if (!f && (cnt1 < cnt0 ? !a[i] : a[i]))
            {
                for (int j = 1; j <= m - n; j++)
                    printf("%d", int(cnt1 < cnt0));
                f = true;
            }
        }
        putchar('\n');
    }
    return 0;
}
```

## 搜索

#### BFS和DFS基础

[城堡问题](https://vjudge.csgrandeur.cn/problem/OpenJ_Bailian-2815)

```c
#include <stdio.h>
#include <math.h>
#include <string.h>

int col, row;
int book[100][100];
int room[100][100];
int maxroom, num = 0, anum = 0;
void Search(int i, int j)
{
    if(book[i][j])  return;
    anum++;
    book[i][j] = 1;
    if((room[i][j] & 1) == 0)   Search(i, j - 1);
    if((room[i][j] & 2) == 0)   Search(i - 1, j);
    if((room[i][j] & 4) == 0)   Search(i, j + 1);
    if((room[i][j] & 8) == 0)   Search(i + 1, j);
}
int main()
{
    scanf("%d %d", &col, &row);
    memset(book, 0, sizeof(book));
    for(int i = 0; i < col; i++)
        for(int j = 0; j < row; j++)
            scanf("%d", &room[i][j]);
    for(int i = 0; i < col; i++)   
        for(int j = 0; j < row; j++)
        {
            if(!book[i][j])
            {
                num++;
                anum = 0;
                Search(i, j);
                maxroom = maxroom > anum ? maxroom : anum;
            }
        }
    printf("%d\n%d", num, maxroom);
    return 0;
}
```

[校题](https://vjudge.csgrandeur.cn/contest/531260#overview)

```c++
//马走日
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
#define LENTH 12
bool board[LENTH][LENTH];
int step[8][2] = {{2, 1}, {2, -1}, {1, -2}, {-1, -2}, {-2, -1}, {-2, 1}, {-1, 2}, {1, 2}};
int n, m, maxn, sum;
void DFS(int x, int y, int num)
{
    if (num >= maxn) //边界
    {
        sum++;
        return;
    }
    for (int i = 0; i < 8; i++) //八个方向
    {
        int nx = x + step[i][0];
        int ny = y + step[i][1];
        if (nx >= 0 && nx < n && ny >= 0 && ny < m && !board[nx][ny]) //判断是否已走过
        {
            board[nx][ny] = true;
            DFS(nx, ny, num + 1);
            board[nx][ny] = false;
        }
    }
    return;
}
int main()
{
    int t, x, y;
    cin >> t;
    while (t--)
    {
        memset(board, 0, sizeof(board));
        cin >> n >> m >> x >> y;
        board[x][y] = 1;
        maxn = n * m;
        sum = 0;
        DFS(x, y, 1);
        cout << sum << endl;
    }
    return 0;
}


//红与黑
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
#define LENTH 20
char buf[LENTH][LENTH];
int step[4][2] = {{1, 0}, {0, -1}, {-1, 0}, {0, 1}};
int res, x, y;
int DFS(int m, int n)
{
    int res = 1;
    buf[m][n] = '#';
    for (int i = 0; i < 4; i++)
    {
        int nm = m + step[i][0];
        int nn = n + step[i][1];
        if (nm >= 0 && nm < x && nn >= 0 && nn < y && buf[nm][nn] == '.')
            res += DFS(nm, nn);
    }
    return res;
}
int main()
{
    int m, n, cnt = 0;
    while (cin >> y >> x && x && y)
    {
        for (int i = 0; i < x; i++) cin >> buf[i];
        for (int i = 0; i < x; i++)
            for (int j = 0; j < y; j++)
                if (buf[i][j] == '@') {m = i; n = j;}
        cout << DFS(m, n) << endl;
    }
    return 0;
}


//棋盘问题
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
int n, k, cnt, num;
char buf[10][10];
int flag[10];
void DFS(int col)
{
    if (num == k) //边界
    {
        cnt++;
        return;
    }
    if (col >= n)   return; //超出边界
    for (int i = 0; i < n; i++) //此行放棋子的情况：对一行中的所有可能进行搜索
    {
        if (!flag[i] && buf[col][i] == '#')
        {
            flag[i] = 1;
            num++;
            DFS(col + 1);
            flag[i] = 0;
            num--; //对每种情况依次搜索，搜索结束后要num--，便于继续下一种情况
        }
    }
    DFS(col + 1); //此行不放棋子的情况
}
int main()
{
    while (cin >> n >> k && n != -1 && k != -1)
    {
        for (int i = 0; i < n; i++) cin >> buf[i];
        cnt = num = 0;
        DFS(0);
        cout << cnt << endl;
    }
    return 0;
}


//Oil Deposits
#include <iostream>
#include <queue>
using namespace std;
int cnt, m, n;
char room[110][110];
int dir[8][2] = {{1, 1}, {1, 0}, {1, -1}, {0, -1}, {-1, -1}, {-1, 0}, {-1, 1}, {0, 1}};
#define CHECK(x, y) (x >= 0 && x < m && y >= 0 && y < n && room[y][x] == '@')
void dfs(int x, int y)
{
    for (int i = 0; i < 8; i++)
    {
        int nextx = x + dir[i][0];
        int nexty = y + dir[i][1];
        if (CHECK(nextx, nexty))
        {
            room[nexty][nextx] = '#';
            dfs(nextx, nexty);
        }
    }
}
int main()
{
    while (cin >> n >> m && m)
    {
        cnt = 0;
        for (int i = 0; i < n; i++)  cin >> room[i];
        for (int x = 0; x < m; x++)
            for (int y = 0; y < n; y++)
                if (room[y][x] == '@') cnt++, dfs(x, y); //此处巧用逗号表达式，同时完成了计数和消除
        cout << cnt << endl;
    }
    return 0;
}

```

```c++
//hdu 1312 "Red and Black"
#include <iostream>
using namespace std;
char room[23][23];
int dir[4][2] = {{-1, 0}, {0, -1}, {1, 0}, {0, 1}};
int Wx, Hy, num;
#define CHECK(x, y) (x < Wx && x >= 0 && y < Hy && y >= 0)
struct node {int x, y;};
void DFS(int dx, int dy)
{
    room[dx][dy] = '#'; //标记这个位置，代表已经走过
    //cout << "walk:" << dx << dy << endl; //在此处打印走过的位置，验证是否符合
    num++;
    for (int i = 0; i < 4; i++) //左上右下4个方向顺时针给深搜
    {
        int newx = dx + dir[i][0];
        int newy = dy + dir[i][1];
        if (CHECK(newx, newy) && room[newx][newy] == '.')
        {
            DFS(newx, newy);
            // cout << "    back:" << dx << dy << endl;
            //在此处打印回退的点的坐标，观察深搜到底后回退的情况
            //例如到达最后的15这个位置会一直回退到起点
            //即打印出14-11-10-9-8-7-6-5-4-3-2-1，这也是递归程序返回的过程
        }
    }
}
int main()
{
    int x, y, dx, dy;
    while (cin >> Wx >> Hy)
    {
        if (Wx == 0 && Hy == 0)  break;
        for (y = 0; y < Hy; y++)
        {
            for (x = 0; x < Wx; x++)
            {
                cin >> room[x][y];
                if (room[x][y] == '@') //读入起点
                {
                    dx = x;
                    dy = y;
                }
            }
        }
        num = 0;
        DFS(dx, dy);
        cout << num << endl;
    }
    return 0;
}
```

POJ 2531 Network Saboteur

此题n很小，直接暴搜做，从第一个数开始遍历，分成两个集合，`vis[i] = true`代表一个集合，`vis[i] = false`代表另一个集合，同时用一个`tmp`先计算若存入的情况，后面再依据两种分类传入新的`tmp`或者原本的`sum`，本题非常灵活的就是将两个集合设为集合`0`和集合`1`，方便了分类也方便了计算

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <cmath>
#include <queue>
using namespace std;
int n, ans;
int a[22][22];
bool vis[22];
void dfs(int now, int sum)
{
    if (now == n + 1) return;
    ans = max(ans, sum);
    int tmp = sum;
    for (int i = 1; i <= n; i++)
    {
        if (vis[i]) tmp -= a[now][i];
        else tmp += a[now][i];
    }
    vis[now] = true;
    dfs(now + 1, tmp);
    vis[now] = false;
    dfs(now + 1, sum);
}
int main()
{
    cin >> n;
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= n; j++)
            cin >> a[i][j];
    dfs(1, 0);
    cout << ans << endl;
    return 0;
}
```

BFS

```c++
//Find The Multiple
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
using namespace std;
void BFS(int n)
{
    long long top;
    queue<long long> que;
    que.push(1);
    while (!que.empty())
    {
        top = que.front();
        que.pop();
        if (top % n == 0) break;
        que.push(top * 10);
        que.push(top * 10 + 1);
    }
    cout << top << endl;
}
int main()
{
    int n;
    while(cin >> n && n) BFS(n);
    return 0;
}


//Catch That Cow
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
using namespace std;
int step[100010];
int n, m;
int BFS()
{
    queue<int> q;
    q.push(n);
    step[n] = 0;
    if (n >= m)  return n - m;
    while (!q.empty())
    {
        int s = q.front();
        q.pop();
        if (s == m)  return step[m];
        if (s - 1 >= 0 && step[s - 1] == -1)  //判断数字要在前面，否则会越界访问
        {
            q.push(s - 1);
            step[s - 1] = step[s] + 1;
        }
        if (s + 1 <= 100000 && step[s + 1] == -1)  
        {
            q.push(s + 1);
            step[s + 1] = step[s] + 1;
        }
        if (s * 2 <= 100000 && step[s * 2] == -1)  
        {
            q.push(s * 2);
            step[s * 2] = step[s] + 1;
        }
    }
    return 0;
}
int main()
{
    while(cin >> n >> m)
    {
        memset(step, -1, sizeof step);
        cout << BFS() << endl;
    }
    return 0;
}


//Prime Path
//ygtrece
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
#include <string>
using namespace std;
const int N = 10010;
int step[N];
bool check[N];
int p[N], tot = 0;
int my_stoi(string str) //字符型转换为整型
{
    int num = 0;
    for (int i = 0; i < 4; i++)
    {
        num = num * 10 + str[i] - '0'; //巧妙
    }
    return num;
}
string my_to_string(int n) //整型转换为字符型
{
    string s;
    int t = 1000;
    for (int i = 0; i < 4; i++)
    {
        s += n / t % 10 + '0'; //注意此处将各个位数存入string类型的s是用+=，也就是说可以用+存入s
        t /= 10;
    }
    return s;
}
int BFS(int a, int b) //操作
{
    queue<int> que;
    que.push(a); //初始状态入列
    string str;
    step[a] = 0;
    while (!que.empty())
    {
        int top = que.front();
        que.pop();
        if (top == b)   return step[top];
        for (int i = 0; i < 4; i++) //不同位数
            for (int j = 0; j < 10; j++) //改变为
                {
                    str = my_to_string(top); //转换为字符类型便于改变
                    str[i] = j + '0'; //改变某一位， 注意要加‘0’
                    int ret = my_stoi(str); //新数字
                    if (ret < 1000 || ret > 9999) continue; //越界
                    if (step[ret] != -1) continue; //已走过
                    if (check[ret]) continue; //非素数
                    que.push(ret); //符合条件入列
                    step[ret] = step[top] + 1;
                }
    }
    return -1; //没有找到符合条件的叔
}
void set_prime()
{
    for (int i = 2; i <= 9999; i++)
    {
        if (!check[i]) p[tot++] = i;
        for (int j = 0; j < tot && i * p[j] <= 9999; j++)
        {
            check[i * p[j]] = true;
            if (!(i % p[j])) break;
        }
    }
}
int main()
{
    int t;
    cin >> t;
    set_prime(); //筛选素数
    while (t--)
    {
        int a, b;
        cin >> a >> b;
        memset(step, -1, sizeof step);
        int tmp = BFS(a, b);
        if (tmp == -1)  cout << "Impossible" << endl;
        else    cout << tmp << endl;
    }
    return 0;
}
//CSGrandeur
#include<cstdio>
#include<cstring>
#include<cstdlib>
#include<algorithm>
#include<queue>
const int maxn = 1e5 + 10;
int step[maxn], a, b, t, ans;
bool isPrime[maxn];
void SetPrime()
{
    memset(isPrime, 1, sizeof(isPrime));
    isPrime[0] = isPrime[1] = false;
    for(int i = 2; i * i < maxn; i ++)
    {
        if(!isPrime[i])
            continue;
        for(int j = i * i; j < maxn; j += i)
            isPrime[j] = false;
    }
}
int BFS() {
    memset(step, 0, sizeof(step));
    std::queue<int> q;
    q.push(a);
    step[a] = 1;
    while(!q.empty()) {
        int now = q.front();
        q.pop();
        if(now == b) return step[now] - 1;
        for(int i = 0; i < 4; i ++) {
            for(int j = 0; j < 10; j ++) {
                if(!j && i == 3) continue;
                int nex = now, tmp = j;
                for(int k = 0; k < i; k ++)
                    nex /= 10;
                nex %= 10;
                for(int k = 0; k < i; k ++)
                    nex *= 10, tmp *= 10;
                nex = now - nex + tmp;
                if(!step[nex] && isPrime[nex]) {
                    q.push(nex);
                    step[nex] = step[now] + 1;
                }
            }
        }
    }
    return -1;
}
int main() {
    SetPrime();
    for(scanf("%d", &t); t --; ) {
        scanf("%d%d", &a, &b);
        if((ans = BFS()) == -1) printf("Impossible\n");
        else printf("%d\n", ans);
    }
    return 0;
}


//Oil Deposits
//CSGrandeur BFS
#include<cstdio>
#include<cstring>
#include<cstdlib>
#include<queue>
typedef std::pair<int, int> pii;
int n, m, ans;
int dx[8] = {-1, 0, 1, -1, 1, -1, 0, 1};
int dy[8] = {-1, -1, -1, 0, 0, 1, 1, 1};
char g[111][111];
void BFS(int y, int x) {
    std::queue<pii> q;
    q.push(pii(y, x));
    g[y][x] = '.';
    while(!q.empty()) {
        pii now = q.front();
        q.pop();
        for(int i = 0; i < 8; i ++) {
            int ny = now.first + dy[i];
            int nx = now.second + dx[i];
            if(ny < 0 || ny >= n || nx < 0 || nx >= m || g[ny][nx] != '@') 
                continue;
            g[ny][nx] = '.';
            q.push(pii(ny, nx));            
        }
    }
}
int main()
{
    while(scanf("%d%d", &n, &m) != EOF && (n != 0 || m != 0)) {
        for(int i = 0; i < n; i ++)
            scanf("%s", g[i]);
        ans = 0;
        for(int i = 0; i < n; i ++)
            for(int j = 0; j < m; j ++)
                if(g[i][j] == '@') ans ++, BFS(i, j);
        printf("%d\n", ans);
    }
    return 0;
}


//Find a way
//TLE code
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
#include <string>
using namespace std;
int n, m, fx, fy, mx, my, nx, ny;
char road[220][220];
priority_queue<int, vector<int>, greater<int>> time;
int step[220][220];
int goo[4][2] = {{0, 1}, {-1, 0}, {1, 0}, {0, -1}};
struct point
{
    int x;
    int y;
};
int BFS(int x, int y)
{
    queue<point> que;
    step[x][y] = 0;
    point p = {x, y};
    que.push(p);
    while (!que.empty())
    {
        p = que.front();
        que.pop();
        if (p.x == nx && p.y == ny)  
        {
            return step[p.x][p.y];
        }
        for (int i = 0; i < 4; i++)
        {
            int ax = p.x + goo[i][0]; 
            int ay = p.y + goo[i][1];
            if (ax >= 0 && ax < n && ay >= 0 && ay < m && step[ax][ay] == -1 && (road[ax][ay] == '.' || road[ax][ay] == '@'))
            {
                step[ax][ay] = step[p.x][p.y] + 1;
                point tmp = {ax, ay};
                que.push(tmp);
            }
        }
    }
    return 0x3f3f3f;
}
int main()
{
    while (cin >> n >> m)
    {
        while (!time.empty())  time.pop();
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
                {
                    cin >> road[i][j];
                    if (road[i][j] == 'Y')
                        {fx = i; fy = j;}
                    if (road[i][j] == 'M')
                        {mx = i; my = j;}
                }
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
            {
                if (road[i][j] == '@')
                {
                    nx = i; ny = j;
                    memset(step, -1, sizeof step);
                    int ftime = 11 * BFS(fx, fy);
                    memset(step, -1, sizeof step);
                    int mtime = 11 * BFS(mx, my);
                    int sum = ftime + mtime;
                    time.push(sum);
                }
            }
        cout << time.top() << endl;
    }
    return 0;
}
//failure try
int n, m, yx, yy, mx, my, rx, ry, tot, nextx, nexty, num;
char room[220][220];
int time[50000];
int step[220][220];
int dir[4][2] = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
struct node {int x, y;};
#define CHECK(x, y) (x >= 0 && x < m && y >= 0 && y < n && room[y][x] != '#')
void bfs(int x, int y)
{
    queue<node> q;
    node start, next;
    start = {x, y};
    step[y][x] = 0;
    q.push(start);
    while (!q.empty())
    {
        start = q.front();
        q.pop();
        if (start.x == rx && start.y == ry) return;
        for (int i = 0; i < 4; i++)
        {
            nextx = start.x + dir[i][0];
            nexty = start.y + dir[i][1];
            if (CHECK(nextx, nexty))
            {
                next = {nextx, nexty};
                step[nexty][nextx] = step[start.y][start.x] + 1;
                q.push(next);
                num++;
            }
        }
        if (num >= n * m)
        {
            step[ry][rx] = 0x3f3f3f;
            return;
        }
    }
}
bool cmp(int x, int y)
{
    return x < y;
}
int main()
{
    while (cin >> n >> m)
    {
        tot = 0;
        memset(time, 0, sizeof time);
        for (int i = 0; i < n; i++)  cin >> room[i];
        for (int x = 0; x < m; x++)
            for (int y = 0; y < n; y++)
            {
                if (room[y][x] == 'Y')  {yx = x; yy = y;}
                if (room[y][x] == 'M')  {mx = x; my = y;}
            }
        for (int x = 0; x < m; x++)
            for (int y = 0; y < n; y++)
            {
                if (room[y][x] == '@')
                    {
                        rx = x;
                        ry = y;
                        num = 0;
                        memset(step, 0, sizeof step);
                        bfs(yx, yy);
                        time[tot++] += step[y][x] * 11;
                        memset(step, 0, sizeof step);
                        tot--;
                        num = 0;
                        bfs(mx, my);
                        time[tot++] += step[y][x] * 11;
                    }
            }
        sort(time, time + tot, cmp);
        cout << time[0] << endl;
    }
    return 0;
}
//DFS尝试失败
void dfs(int x, int y, int px, int py)
{
    if (room[py][px] == room[y][x])
    {
        time[tot++] += num;
        return;
    }
    for (int i = 0; i < 4; i++)
    {
        nextx = px + dir[i][0];
        nexty = py + dir[i][1];
        if (CHECK(nextx, nexty))
        {
            num++;
            room[py][px] = '#';
            dfs(x, y, nextx, nexty);
            num--;
            room[py][px] = '.';
        }
    }
}
//DragonKingA
#include <iostream>
#include <cstring>
#include <queue>
#define N 205
using namespace std;
typedef pair<int, int> p;
typedef pair<p, int> pp;
int RES = 0, n, m, dx, dy, store[N][N], dir[4][2] = {{-1, 0}, {0, 1}, {1, 0}, {0, -1}};
char road[N][N];
bool vis[N][N];
void BFS(int x, int y)
{
    queue<pp> q;
    q.push(pp(p(x, y), 0));
    memset(vis, 0, sizeof(vis));
    while (q.size())
    {
        pp temp = q.front();
        q.pop();
        dx = temp.first.first;
        dy = temp.first.second;
        if (store[dy][dx] != -1)
        {
            store[dy][dx] += temp.second;
            RES = store[dy][dx];
        }
        for (int i = 0, nx, ny; i < 4; i++)
        {
            nx = dx + dir[i][0];
            ny = dy + dir[i][1];
            if (nx >= 0 && nx < m && ny >= 0 && ny < n && road[ny][nx] != '#' && !vis[ny][nx])
            {
                vis[ny][nx] = 1;
                q.push(pp(p(nx, ny), temp.second + 11));
            }
        }
    }
}
int main()
{
    p pY, pM;
    while (cin >> n >> m)
    {
        memset(store, -1, sizeof(store));
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
            {
                cin >> road[i][j];
                switch (road[i][j])
                {
                case 'Y':
                    pY = {j, i};
                    break;
                case 'M':
                    pM = {j, i};
                    break;
                case '@':
                    store[i][j] = 0;
                    break;
                }
            }
        BFS(pY.first, pY.second);
        BFS(pM.first, pM.second);
        for (int i = 0; i < N; i++)
            for (auto x : store[i])
                if (x != -1 && x != 0)
                    RES = RES < x ? RES : x;
        cout << RES << endl;
    }
    return 0;
}
//ygtrece
#include <iostream>
#include <cstring>
#include <queue>
using namespace std;
#define N 205
#define CHECK(x, y) (x >= 0 && x < m && y >= 0 && y < n && room[y][x] != '#' && !vis[y][x])
int n, m, yx, yy, mx, my, res;
char room[N][N];
int buf[N][N], vis[N][N];
struct node {int x, y;};
int dir[4][2] = {{0, 1}, {1, 0}, {-1, 0}, {0, -1}};
void BFS(node p)
{
    memset(vis, 0, sizeof vis);
    queue<pair<node, int>> q;
    pair<node, int> start(p, 0), next;
    q.push(start);
    while (!q.empty())
    {
        start = q.front();
        q.pop();
        if (buf[start.first.y][start.first.x] != -1)
        {
            buf[start.first.y][start.first.x] += start.second;
            res = buf[start.first.y][start.first.x];
        }
        for (int i = 0; i < 4; i++)
        {
            next.first = {start.first.x + dir[i][0], start.first.y + dir[i][1]};
            if (CHECK(next.first.x, next.first.y))
            {
                next.second = start.second + 1;
                vis[next.first.y][next.first.x] = 1;
                q.push(next);
            }
        }
    }
}
int main()
{
    while (cin >> n >> m)
    {
        node pY, pM;
        memset(buf, -1, sizeof buf);
        for (int y = 0; y < n; y++)
            for (int x = 0; x < m; x++)
            {
                cin >> room[y][x];
                switch(room[y][x])
                {
                    case 'Y': {pY = {x, y}; break;}
                    case 'M': {pM = {x, y}; break;}
                    case '@': {buf[y][x] = 0; break;}
                }
            }
        BFS(pY);
        BFS(pM);
        for (int i = 0; i < n; i++)
            for (auto x : buf[i])
                if (x != 0 && x != -1)
                    res = x > res ? res : x;
        cout << res * 11 << endl;
    }
    return 0;
}
//CSGrandeur
#include<cstdio>
#include<cstring>
#include<cstdlib>
#include<queue>
typedef std::pair<int, int> pii;
const int maxn = 222;
char g[maxn][maxn];
int step1[maxn][maxn], step2[maxn][maxn];
int dx[4] = {-1, 1, 0, 0};
int dy[4] = {0, 0, -1, 1};
int n, m, yi, yj, mi, mj;
void BFS(int si, int sj, int step[][maxn]) {
    std::queue<pii> q;
    q.push(pii(si, sj));
    memset(step, 0, sizeof(int) * maxn * maxn);
    step[si][sj] = 1;
    while(!q.empty()) {
        pii now = q.front();
        q.pop();
        for(int i = 0; i < 4; i ++) {
            int di = now.first + dx[i];
            int dj = now.second + dy[i];
            if(di >= 0 && di < n && dj >= 0 && dj < m && g[di][dj] != '#' && !step[di][dj]) {
                step[di][dj] = step[now.first][now.second] + 1;
                q.push(pii(di, dj));
            }
        }
    }
}
int main() {
    while(scanf("%d%d", &n, &m) != EOF) {
        for(int i = 0; i < n; i ++) {
            scanf("%s", g[i]);
            char *tmp;
            if((tmp = strstr(g[i], "Y")) != NULL) { //用指针和strstr找坐标
                yi = i;
                yj = tmp - g[i];
            }
            if((tmp = strstr(g[i], "M")) != NULL) {
                mi = i;
                mj = tmp - g[i];
            }
        }
        BFS(yi, yj, step1);
        BFS(mi, mj, step2);
        int ans = 0x3f3f3f3f;
        for(int i = 0; i < n; i ++) {
            for(int j = 0; j < m; j ++) {
                if(g[i][j] != '@' || !step1[i][j] || !step2[i][j]) continue;//注意考虑到达不了的情况
                ans = std::min(ans, (step1[i][j] + step2[i][j] - 2) * 11);
            }
        }
        printf("%d\n", ans);
    }
    return 0;
}


//迷宫问题
#include <iostream>
#include <queue>
using namespace std;
int room[10][10];
struct node {int x, y;}buf[20][20];
int dir[4][2] = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
#define CHECK(x, y) (x >= 0 && x < 5 && y >= 0 && y < 5 && !room[x][y])
void BFS()
{
    queue<node> q;
    node start, next;
    start = {0, 0};
    q.push(start);
    while (!q.empty())
    {
        start = q.front();
        q.pop();
        if (start.x == 4 && start.y == 4)  break;
        for (int i = 0; i < 4; i++)
        {
            next.x = start.x + dir[i][0];
            next.y = start.y + dir[i][1];
            if (CHECK(next.x, next.y))
            {
                buf[next.x][next.y] = start;
                room[next.x][next.y] = 1;
                q.push(next);
            }
        }
    }
}
void Output(node n) //打印
{
    if (!n.x && !n.y)
    {
        printf("(0, 0)\n");
        return;
    }
    Output(buf[n.x][n.y]);
    printf("(%d, %d)\n", n.x, n.y);
}
int main()
{
    for (int x = 0; x < 5; x++)
        for (int y = 0; y < 5; y++)
            cin >> room[x][y];
    BFS();
    node end = {4, 4};
    Output(end);
    return 0;
}


//Pots
//CSDN
#include <iostream>
#include <string.h>
#include <stdio.h>
#include <queue>
using namespace std;
int f[105][105]; //用来标记当前状态是否已经有过
int A, B, C;
struct node
{
    int a, b;   //两个容器中的水
    int sa, sb; //上个状态
    int way;    //操作1到6
    int step;   //当前步数
} lu[105][105];
queue<node> q;
void print(int a, int b)
{
    if (lu[a][b].a == 0 && lu[a][b].b == 0) // 到达初始状态
        return;
    print(lu[a][b].sa, lu[a][b].sb);
    switch (lu[a][b].way)
    {
    case 1:
        cout << "FILL(1)" << endl;
        break;
    case 2:
        cout << "FILL(2)" << endl;
        break;
    case 3:
        cout << "DROP(1)" << endl;
        break;
    case 4:
        cout << "DROP(2)" << endl;
        break;
    case 5:
        cout << "POUR(1,2)" << endl;
        break;
    case 6:
        cout << "POUR(2,1)" << endl;
        break;
    }
}
void push(node d)
{ //入队操作
    if (f[d.a][d.b] == 0)
    {
        q.push(d);
        lu[d.a][d.b] = d;
        f[d.a][d.b] = 1;
    }
}
void bfs()
{
    q.push(lu[0][0]);
    while (!q.empty())
    {
        node u = q.front();
        q.pop();
        if (u.a == C || u.b == C)
        {
            printf("%d\n", u.step);
            print(u.a, u.b);
            return;
        }
        node v;
        v.sa = u.a;
        v.sb = u.b;
        v.step = u.step + 1;

        if (u.a != A)
        { //把1加满
            v.a = A;
            v.b = u.b;
            v.way = 1;
            push(v);
        }

        if (u.b != B)
        { //把2加满
            v.b = B;
            v.a = u.a;
            v.way = 2;
            push(v);
        }

        if (u.a != 0)
        { //倒光3
            v.a = 0;
            v.b = u.b;
            v.way = 3;
            push(v);
        }

        if (u.b != 0)
        { //倒光4
            v.a = u.a;
            v.b = 0;
            v.way = 4;
            push(v);
        }

        if (u.a != 0 && u.b != B)
        { //把1倒给2
            if (u.a + u.b >= B)
            {
                v.b = B;
                v.a = u.a + u.b - B;
            }
            else
            {
                v.a = 0;
                v.b = u.a + u.b;
            }
            v.way = 5;
            push(v);
        }

        if (u.a != A && u.b != 0)
        { //把2倒给1
            if (u.a + u.b >= A)
            {
                v.a = A;
                v.b = u.a + u.b - A;
            }
            else
            {
                v.a = u.a + u.b;
                v.b = 0;
            }
            v.way = 6;
            push(v);
        }
    }
    printf("impossible\n");
}
int main()
{
    memset(f, 0, sizeof(f));
    lu[0][0].a = lu[0][0].b = 0;
    lu[0][0].sa = lu[0][0].sb = -1;
    lu[0][0].step = 0;
    scanf("%d %d %d", &A, &B, &C);
    bfs();
    return 0;
}
//ygtrece‘s AC Code
//如果题目需要记录整个过程，那么开一个结构体，每一个点储存上一个位置的信息是最好的选择
//用搜索一定要记得判断是否走过
//对于无法实现，即不可能的情况，在BFS函数后加上不可能的情况所需要应对的情况即可，因为BFS在搜索走完全部区域的时候，还没有找到符合的情况时，while就会结束，继续走到后面，如果中途实现了，就会有return，所以巧妙地解决了不可能的情况
#include <iostream>
#include <string.h>
#include <stdio.h>
#include <queue>
using namespace std;
#define N 205
int flag[N][N];
int A, B, C;
struct node
{
    int a, b;
    int way;
    int step;
}buf[N][N];
node s, n;
queue<node> q;
void print(node d)
{
    if (d.a == 0 && d.b == 0)  return;
    print(buf[d.a][d.b]);
    switch(d.way)
    {
        case 1: cout << "FILL(1)" << endl; 
                break;
        case 2: cout << "FILL(2)" << endl;
                break;
        case 3: cout << "DROP(1)" << endl;
                break;
        case 4: cout << "DROP(2)" << endl;
                break;
        case 5: cout << "POUR(1,2)" << endl;
                break;
        case 6: cout << "POUR(2,1)" << endl;
                break;
    }
}
void push(node d)
{
    if (!flag[d.a][d.b])
    {
        flag[d.a][d.b] = 1;
        buf[d.a][d.b] = s;
        q.push(d);
    }
}
void bfs()
{
    buf[0][0].a = buf[0][0].b = buf[0][0].step = 0;
    s = buf[0][0];
    q.push(s);
    while (!q.empty())
    {
        s = q.front();
        q.pop();
        if (s.a == C || s.b == C)
        {
            cout << s.step << endl;
            print(s);
            return;
        }
        n.step = s.step + 1;
        if (s.a != A) //fill(1)
        {
            n.a = A;
            n.b = s.b;
            n.way = 1;
            push(n);
        }
        if (s.b != B) //fill(2)
        {
            n.b = B;
            n.a = s.a;
            n.way = 2;
            push(n);
        }
        if (s.a != 0) //drop(1)
        {
            n.a = 0;
            n.b = s.b;
            n.way = 3;
            push(n);
        }
        if (s.b != 0) //drop(2)
        {
            n.b = 0;
            n.a = s.a;
            n.way = 4;
            push(n);
        }
        if (s.a != 0 && s.b != B) //pour(1, 2)
        {
            if (s.a + s.b >= B)
            {
                n.b = B;
                n.a = s.a - (B - s.b);
            }
            else
            {
                n.b = s.a + s.b;
                n.a = 0;
            }
            n.way = 5;
            push(n);
        }
        if (s.b != 0 && s.a != A) //pour(2, 1)
        {
            if (s.a + s.b >= A)
            {
                n.a = A;
                n.b = s.b - (A - s.a);
            }
            else
            {
                n.a = s.a + s.b;
                n.b = 0;
            }
            n.way = 6;
            push(n);
        }
    }
    cout << "impossible" << endl;
}
int main()
{
    cin >> A >> B >> C;
    memset(flag, 0, sizeof flag);
    bfs();
    return 0;
}
//CSGrandeur

//Failure Try
//没判断走过的路
//如何判断无可能？
//三个及以上变量，还是选择结构体吧，用pari实在过于繁琐且杂乱
#include <iostream>
#include <cstring>
#include <queue>
using namespace std;
int a, b, c;
typedef pair<int, int> p;
typedef pair<p, int> pp;
typedef pair<pp, string> ppp;
ppp = <<<int, int>, int>, string>
int bfs()
{
    queue<ppp> q;
    ppp start, next;
    start.first.first = {0, 0};
    start.first.second = 0;
    q.push(start);
    while (!q.empty())
    {
        start = q.front();
        q.pop();
        if (start.first.first.first == c || start.first.first.second == c)
        {
            return start.first.second;
        }
        for (int i = 0, na, nb; i < 6; i++)
        {
            next = start;
            switch(i)
            {
                //pull(1)
                case 1: next.first.first.first = a;
                        next.second = "PULL(1)";
                        break;
                //pull(2)
                case 2: next.first.first.second = b;
                        next.second = "PULL(2)";
                        break;
                //drop(1)
                case 3: next.first.first.first = 0;
                        next.second = "DROP(1)";
                        break;
                //drop(2)
                case 4: next.first.first.second = 0;
                        next.second = "DROP(2)";
                        break;
                //pour(1, 2)
                case 5: if (next.first.first.first < (b - next.first.first.second))
                        {
                            next.first.first.second += next.first.first.first;
                            next.first.first.first = 0;
                        }
                        else
                        {
                            next.first.first.first -= b - next.first.first.second;
                            next.first.first.second = b;
                        }
                        next.second = "POUR(1, 2)";
                        break;
                //pour(2, 1)
                case 6: if (next.first.first.second < (a - next.first.first.first))
                        {
                            next.first.first.first += next.first.first.second;
                            next.first.first.second= 0;
                        }
                        else
                        {
                            next.first.first.second -= a - next.first.first.first;
                            next.first.first.second = a;
                        }
                        next.second = "POUR(2, 1)";
                        break;
            }
            next.first.second += 1;
            q.push(next);
        }
    }
}
int main()
{
    cin >> a >> b >> c;
    cout << bfs() << endl;
    return 0;
}
//


//hdu 1312 “Red and Black”
#include <algorithm>
#include <queue>
#include <ctime>
using namespace std;
char room[23][23];
int dir[4][2] = {{-1, 0}, {0, -1}, {1, 0}, {0, 1}};
int Wx, Hy, num;
#define CHECK(x, y) (x < Wx && x >= 0 && y < Hy && y >= 0)
struct node {int x, y;};
void BFS(int dx, int dy)
{
    num = 1;
    queue<node> q;
    node start, next;
    start.x = dx;
    start.y = dy;
    q.push(start);
    while (!q.empty())
    {
        start = q.front();
        q.pop();
        //cout << "out" << start.x << start.y << endl; //打印出队列情况进行验证
        for (int i = 0; i < 4; i++) //按左上右下四个方向顺时针逐一搜索
        {
            next.x = start.x + dir[i][0];
            next.y = start.y + dir[i][1];
            if (CHECK(next.x, next.y) && room[next.x][next.y] == '.')
            {
                room[next.x][next.y] = '#'; //标记已经处理过
                num++;
                q.push(next);
            } 
        }
    }
}
int main()
{
    int x, y, dx, dy;
    while (cin >> Wx >> Hy)
    {
        if (Wx == 0 && Hy == 0)  break;
        for (y = 0; y < Hy; y++)
        {
            for (x = 0; x < Wx; x++)
            {
                cin >> room[x][y];
                if (room[x][y] == '@') //读入起点
                {
                    dx = x;
                    dy = y;
                }
            }
        }
        num = 0;
        BFS(dx, dy);
        cout << num << endl;
    }
    return 0;
}


//BFS+Cantor 解决八数码问题
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
#include <string>
#include <ctime>
using namespace std;
const int LEN = 362880; //状态一共9！= 362880种
struct node
{
    int state[9]; //记录一个八数码的排列，即一个状态
    int dis; //记录到起点的位置
};
int dir[4][2] = {{-1, 0}, {0, -1}, {1, 0}, {0, 1}}; //左上右下顺时针方向，左上角的坐标是(0, 0)
int visited[LEN] = {0}; //与每个状态对应的记录，Cantor()函数对它置数，并判重
int start[9]; //开始状态
int goal[9]; //目标状态
long int factory[] = {1, 1, 2, 6, 24, 120, 720, 5040, 40320, 362880}; //Cantor()用到的常数
bool Cantor(int str[], int n) //用Cantor()展开判重
{
    long result = 0;
    for (int i = 0; i < n; i++)
    {
        int counted = 0;
        for (int j = i + 1; j < n; j++)
        {
            if (str[i] > str[j])  //当前未出现的元素排在第几个
                counted++;
        }
        result += counted * factory[n - i - 1];
    }
    if (!visited[result])  //没有被访问过
    {
        visited[result] = 1;
        return 1;
    }
    else
        return 0;
}
int bfs()
{
    node head;
    memcpy(head.state, start, sizeof(head.state)); //复制起点的状态
    head.dis = 0;
    queue<node> q; //队列中的内容是记录状态
    Cantor(head.state, 9); //用康托展开判重，目的是对起点的visited[]赋初值
    q.push(head); //第一个进队列的是起点状态

    while (!q.empty()) //处理队列
    {
        head = q.front();
        if (memcmp(head.state, goal, sizeof(goal)) == 0) //与目标状态对比
            return head.dis; //到达目标状态，返回距离，结束
        q.pop(); //可在此处打印head.state,看弹出队列的情况
        int z;
        for (z = 0; z < 9; z++) //找到这个状态中0的位置
            if (head.state[z] == 0) break; //找到了
            //转化为二维，左上角是原点(0, 0)
        int x = z % 3; //横坐标
        int y = z / 3; //纵坐标
        for (int i = 0; i < 4; i++) //上下左右最多可能有4个新的状态
        {
            int newx = x + dir[i][0]; //元素0转移后的新坐标
            int newy = y + dir[i][1];
            int nz = newx + 3 * newy; //转化为一维
            if (newx >= 0 && newx < 3 && newy >= 0 && newy < 3) //判断是否越界
            {
                node newnode;
                memcpy(&newnode, &head, sizeof(struct node)); //复制这个新的状态
                swap(newnode.state[z], newnode.state[nz]); //把0移动到新的位置
                newnode.dis++;
                if (Cantor(newnode.state, 9)) //用康托展开判重
                    q.push(newnode); //把新的状态放入队列
            }
        }
    }
    return -1; //没找到
}
int main()
{
    for (int i = 0; i < 9; i++)  cin >> start[i]; //初始状态
    for (int i = 0; i < 9; i++)  cin >> goal[i]; //目标状态
    int num = bfs();
    if (num != -1)  cout << num << endl;
    else  cout << "Impossible" << endl;
    return 0;
}


//马走日--判断能否走完整个棋盘
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
#include <string>
#include <cmath>
using namespace std;
#define CHECK(x, y) (x >= 0 && x < m && y >= 0 && y < n && !flag[x][y])
int dir[8][2] = {{2, 1}, {2, -1}, {1, -2}, {-1, -2}, {-2, -1}, {-2, 1}, {-1, 2}, {1, 2}};
bool flag[12][12];
int cnt = 1, n, m, x, y, t;
struct node {int x, y;};
void BFS(int nx, int ny)
{
    queue<node> q;
    node top;
    flag[nx][ny] = true;
    top.x = nx;
    top.y = ny;
    q.push(top);
    while (!q.empty())
    {
        top = q.front();
        q.pop();
        for (int i = 0; i < 8; i++)
        {
            int newx = top.x + dir[i][0];
            int newy = top.y + dir[i][1];
            if (CHECK(newx, newy))
            {
                flag[newx][newy] = true;
                node nd;
                nd.x = newx;
                nd.y = newy;
                q.push(nd);
                cnt++;
            }
        }
    }
}
int main()
{
    cin >> t;
    while (t--)
    {
        cnt = 1;
        memset(flag, 0, sizeof flag);
        cin >> n >> m >> x >> y;
        BFS(x, y);
        if (cnt == n * m)  cout << "Successful!\n";
        else  cout << "Sorry, you can't do it!\n";
    }
    return 0;
}


//Oil Deposits
#include <iostream>
#include <queue>
using namespace std;
int cnt, m, n;
char room[110][110];
struct node {int x, y;};
int dir[8][2] = {{1, 1}, {1, 0}, {1, -1}, {0, -1}, {-1, -1}, {-1, 0}, {-1, 1}, {0, 1}};
#define CHECK(x, y) (x >= 0 && x < m && y >= 0 && y < n && room[y][x] == '@')
void bfs(int x, int y)
{
    node start, next;
    queue<node> q;
    start = {x, y};
    q.push(start);
    while (!q.empty())
    {
        start = q.front();
        q.pop();
        for (int i = 0; i < 8; i++)
        {
            next.x = start.x + dir[i][0];
            next.y = start.y + dir[i][1];
            if (CHECK(next.x, next.y))
            {
                q.push(next);
                room[next.y][next.x] = '*';
            }
        }
    }
    cnt++;
}
int main()
{
    while (cin >> n >> m && m)
    {
        cnt = 0;
        for (int i = 0; i < n; i++)  cin >> room[i];
        for (int x = 0; x < m; x++)
            for (int y = 0; y < n; y++)
            {
                if (room[y][x] == '@')  bfs(x, y);
            }
        cout << cnt << endl;
    }
    return 0;
}
```

#### 剪枝

```c++
BFS剪枝通常使用判重，如果搜索到某一层时，出现重复状态就剪枝
如何判重？用STL的map和set效率都很好，另外还有一种数学方法叫康托判重，竞赛时一般不用

//康托判重
//例如九宫最多有9！种排列组合，既362880中排列组合方式，使用数组state[362880]可以用来判断是否出现重复的元素
bool state[362880];       //N的阶乘 
int kangtuo(int x[])  //康拓展开进行判重， x[]储存该数的各个位的数字
{
    int fac[] = {1, 1, 2, 6, 24, 120, 720, 5040, 40320}; //位数阶乘
    int sum = 0;
    for (int i = 0; i < 9; i++)
    {
        int t = 0;
        for (int j = i + 1; j < 9; j++)
            if (x[j] < x[i]) t++;
        sum += t * fac[8 - i];
    }
    if (state[sum]) return 0;
    else return state[sum] = 1;
}

DFS剪枝技术较多
1.可行性剪枝
2.搜索顺序剪枝
3.最优性剪枝
4.排除等效冗余
5.记忆化搜索
```

lanqiao 642 跳蚂蚱

化圆为线；巧妙转换

```c++
#include <algorithm>
#include <iostream>
#include <string>
#include <map>
using namespace std;
const int maxn = 5e4 + 10;
struct node
{
    node(){}
    node(string ss, int tt){s = ss, t = tt;}
    string s;
    int t;
};
map<string, bool> mp;
queue<node> q;
void bfs()
{
    string s = "012345678";
    mp[s] = true;
    q.push(node(s, 0));
    while (!q.empty())
    {
        node now = q.front();
        q.pop();
        string s = now.s;
        int step = now.t;
        if (s == "087654321")
        {
            cout << step << endl;
            break;
        }
        int i;
        for (i = 0; i < 10; i++)
            if (s[i] == '0') break;
        for (int j = i - 2; j <= i + 2; j++)
        {
            int k = (j + 9) % 9;
            if (k == i) continue;
            string news = s;
            char tmp = news[i];
            news[i] = news[k];
            news[k] = tmp;
            if (!mp[news])
            {
                mp[news] = true;
                q.push(node(news, step + 1));
            }
        }
    }
}
int main()
{
    bfs();
    return 0;
}

//set
set<string> vis;
...
if (!vis.count(news))
{
    vis.insert(news);
    q.push(node(news, step + 1));
}
```

hdu 2553 "N皇后问题"  N <= 10

```c++
#include <iostream>
#include <algorithm>
#include <cmath>
using namespace std;
int n, tot = 0;
int col[12] = {0}; //储存放置的皇后的位置信息
bool check(int c, int r)
{
    for (int i = 0; i < r; i++)
        if (col[i] == c || (abs(col[i] - c) == abs(i - r)))
            return false;
    return true;
}
void DFS(int r) //一行一行地放皇后，这一次是第r行
{
    if (r == n) //所有皇后都放好了，递归返回
    {
        tot++; //统计合法的棋局个数
        return;
    }
    for (int c = 0; c < r; c++) //在每一列放皇后
        if (check(c, r)) //检查是否合法
        {
            col[r] = c; //在第r行的c列放皇后
            DFS(r + 1);//继续放下一行皇后
        }
}
int main()
{
    int ans[12] = {0};
    for (n = 0; n <= 10; n++) //算出所有N皇后的答案，先打表，不然会超时
    {
        memset(col, 0, sizeof col); //清空，准备计算下一个N皇后问题
        tot = 0;
        DFS(0);
        ans[n] = tot; //打表
    }
    while (cin >> n)
    {
        if (n == 0)  return 0;
        cout << ans[n] << endl;
    }
    return 0;
}

//尝试用BFS
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
#include <string>
#include <cmath>
using namespace std;

int n, tot;
int col[12];
struct node {int x, y;};
bool check(int x, int y)
{
    //？
}
void BFS()
{
    queue<node> q;
    node start, next;
    for (int i = 0; i < n; i++)
    {
        start = {i, 0};
        q.push(start);
    }
    while (!q.empty())
    {
        start = q.front();
        q.pop();
        for (int i = 0; i < n; i++)
        {
            next.x = i;
            next.y = start.y + 1;
            if (check(next.x, next.y))
            {
                q.push(next);
                //？
            }
        }
    }
}
int main()
{
    int ans[12] = {0};
    for (n = 0; n < 12; n++)
    {
        memset(col, 0, sizeof col);
        tot = 0;
        BFS();
        ans[n] = tot;
    }
    while (cin >> n)  cout << ans[n] << endl;
    return 0;
}
```

Find The Multiple

```c++
#include <iostream>
using namespace std;
int n, i;
bool flag;
long long ans[220];
void bfs(long long num, int times)
{
    if (times > 19 || flag) return; //回溯剪枝
    else if (!(num % i))
    {
        flag = true;
        ans[i] = num;
        return;
    }
    else
    {
        bfs(num * 10, times + 1);
        bfs(num * 10 + 1, times + 1);
    }
}
int main()
{
    for (i = 1; i <= 200; i++)  //打表
    {
        bfs(1, 1);
        flag = false;
    }
    while (cin >> n && n)
        cout << ans[n] << endl;
    return 0;
}
```

luogu P1036 [NOIP2002 普及组] 选数

DFS + 不降原则，注意方法

```c++
#include <iostream>
using namespace std;
int n, k, a[22], ans;
bool check(int x)
{
    for (int i = 2; i * i <= x; i++)
        if (x % i == 0) return false;
    return true;
}
void dfs(int now, int sum, int last)
{
    if (now == k + 1)
    {
        if (check(sum)) ans++;
        return;
    }
    for (int i = last; i <= n; i++)    //不降原则的搜索
        dfs(now + 1, sum + a[i], i + 1);
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    cin >> n >> k;
    for (int i = 1; i <= n; i++) cin >> a[i];
    dfs(1, 0, 1);
    cout << ans;
    return 0;
}
```

[HDU 1495 非常可乐](https://www.cnblogs.com/DM11/p/17001261.html)

出现最短路径至少应首选BFS

```c++
#include <algorithm>
#include <iostream>
#include <queue>
#include <cstring>
#include <map>
using namespace std;
const int maxn = 1e2 + 10;
int w[3];
int vis[maxn][maxn][maxn];  //判重
struct node
{
    int v[3];  //三个杯子当前状态
    int step;
};
void bfs()
{
    memset(vis, 0, sizeof vis);
    queue<node> q;
    q.push({w[0], 0, 0});
    vis[w[0]][0][0] = 1;
    while (!q.empty())
    {
        node s = q.front();
        q.pop();
        if (s.v[0] == s.v[2] && s.v[1] == 0) //平分判断
        {
            cout << s.step << endl;
            return;
        }
        for (int i = 0; i < 3; i++)
            for (int j = 0; j < 3; j++)
            {
                if (i != j)
                {
                    node temp = s;
                    //完美解决两种情况，即倒出的杯子空了或者倒入的杯子满了
                    int minn = min(temp.v[i], w[j] - temp.v[j]);  
                    temp.v[i] -= minn; temp.v[j] += minn;
                    if (!vis[temp.v[0]][temp.v[1]][temp.v[2]])
                    {
                        temp.step++;
                        q.push(temp);
                        vis[temp.v[0]][temp.v[1]][temp.v[2]] = 1;
                    }
                }
            }
    }
    cout << "NO\n";
}
int main()
{
    while (cin >> w[0] >> w[1] >> w[2])
    {
        if (!w[0] && !w[1] && !w[2]) break;
        if (w[1] > w[2]) swap(w[1], w[2]);   //默认杯2的容量大于杯1，减少编码量
        if (w[0] % 2) cout << "NO\n";        //可行性剪枝，若容量为奇数，无法平分
        else bfs();
    }
    return 0;
}
```

luogu P1379 八数码难题

BFS + 二维转一维

```c++
#include <algorithm>
#include <iostream>
#include <queue>
#include <map>
using namespace std;
const int maxn = 3;
struct node
{
    string str;
    int step;
};
map<string, bool> m;
queue<node> q;
int step[4] = {1, -1, 3, -3};
void bfs()
{
    string s;
    cin >> s;
    node start = {s, 0};
    q.push(start);
    m[s] = true;
    while (!q.empty())
    {
        start = q.front();
        q.pop();
        if (start.str == "123804765")
        {
            cout << start.step;
            return;
        }
        int tmp = start.str.find("0");
        for (int i = 0; i < 4; i++)
        {
            if ((tmp == 0 || tmp == 3 || tmp == 6) && i == 1) continue;
            if ((tmp == 2 || tmp == 5 || tmp == 8) && i == 0) continue;
            if ((tmp == 0 || tmp == 1 || tmp == 2) && i == 3) continue;
            if ((tmp == 6 || tmp == 7 || tmp == 8) && i == 2) continue;
            node next = start;
            char word = next.str[tmp + step[i]];
            next.str[tmp + step[i]] = '0';
            next.str[tmp] = word;
            if (!m[next.str])
            {
                m[next.str] = true;
                next.step++;
                q.push(next);
            }
        }
    }
}
int main()
{
    bfs();
    return 0;
}
```

E？

```
int n, m, t, room[10][10];
int ste[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
int vis[10][10];
bool check(int x, int y) 
{
    if (x >= 0 && x < n && y >= 0 && y < m && !vis[x][y]) return true; 
    return false;
}
struct node
{
    int x;
    int y;
    int step;
};
queue<node> q;
void bfs(int x, int y)
{
    node start = {x, y, 0};
    q.push(start);
    vis[x][y] = 1;
    while (!q.empty())
    {
        start = q.front();
        q.pop();
        if (room[start.x][start.y] == 'D')
        {
            cout << "YES" << endl;
            return;
        }
        if (start.step == t)
        {
            cout << "NO" << endl;
            return;
        }
        for (int i = 0; i < 4; i++)
        {
            int nx = start.x + ste[i][0];
            int ny = start.y + ste[i][1];
            if (check(nx, ny))
            {
                vis[nx][ny] = 1;
                node next = {nx, ny, start.step + 1};
                q.push(next);
            }
        }
    }
}
int main()
{
    while (cin >> n >> m >> t)
    {
        if (n == m && m == t && t == 0) break;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
                cin >> room[i][j];
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
                if (room[i][j] == 'S') bfs(i, j);
    }
}
```

HDU 1010 Tempter of the Bone

DFS+方格图奇偶性判断+可行性剪枝，“方格图中两点之间的曼哈顿距离的奇偶性，必然与两点之间任意路径的奇偶性相同”

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <cmath>
#include <queue>
using namespace std;
const int N = 10;
int n, m, k, flag;
char map[N][N];
bool vis[N][N];
int sx, sy, ex, ey;
int step[4][2] = {{1, 0}, {0, 1}, {-1, 0}, {0, -1}};
void init() {memset(vis, 0, sizeof vis); flag = 0;}
bool check(int x, int y) {if (x >= 1 && x <= n && y >= 1  && y <= m) return true; return false;}
void dfs(int x, int y, int tot)
{
    if (flag) return;
    if (map[x][y] == 'D')
    {
        if (tot == k) flag = true;
        return;
    }
    if (tot + abs(x - ex) + abs(y - ey) > k) return;  //可行性剪枝：如果当前加上最短距离之后大于k，显然无效
    for (int i = 0; i < 4; i++)
    {
        int nx = x + step[i][0], ny = y + step[i][1];
        if (check(nx, ny) && !vis[nx][ny] && map[nx][ny] != 'X')
        {
            vis[nx][ny] = true;
            dfs(nx, ny, tot + 1);
            vis[nx][ny] = false;//回溯
        }
    }
}
int main()
{
    while (cin >> n >> m >> k)
    {
        if (!n && !m && !k) break;
        for (int i = 1; i <= n; i++) cin >> map[i] + 1;
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= m; j++)
            {
                if (map[i][j] == 'S') sx = i, sy = j;
                if (map[i][j] == 'D') ex = i, ey = j;
            }
        int dis = abs(sx - ex) + abs(sy - ey);   //曼哈顿距离公式
        if (k - dis < 0 || dis % 2 != k % 2)     //曼哈顿距离和最短步数奇偶性必然相同
        {
            cout << "NO" << endl;
            continue;
        }
        init();
        vis[sx][sy] = true;
        dfs(sx, sy, 0);
        if (flag) cout << "YES" << endl;
        else cout << "NO" << endl;
    }
    return 0;
}
```



#### BFS与最短路径



## 高级数据结构

#### 并查集

```c++
//合并优化  少用
int find_set(int x)
{
    return x == s[x] ? x : find_set(s[x]);
}
void init_set()
{
    for (int i = 1; i <= n; i++)
    {
        s[i] = i;
        height[i] = 0;  //树的高度
    }
}
void merge_set(int x, int y)
{
    x = find_set(x);
    y = find_set(y);
    if (hegiht[x] == height[y])
    {
        height[x] = height[x] + 1;
        s[y] = x;      //合并，树的高度加1
    }
    else               //把矮树合并到高树上，高树的高度保持不变
    {
        if (height[x] < height[y]) s[x] = y;
        else s[y] = x;
    }
}

//查询优化(路径压缩) 常用
int find_set(int x)
{
    if (x != s[x]) s[x] = find_set(s[x]);
    return s[x];
}

//带权值的路径压缩
int find_set(int x)
{
    if (x != s[x])
    {
        int t = s[x];            //记录父节点
        s[x] = find_set(s[x]);   //路径压缩，递归最后返回的是根节点
        d[x] += d[t];            //权值更新为x到根节点的权值
    }
    return s[x];
}

//带权值的路径压缩
int find_set(int x)
{
    if (x != s[x])
    {
        int t = s[x];           //记录父节点
        s[x] = find_set(s[x]);  //路径压缩，递归最后返回的是根节点
        d[x] += d[t];           //权值更新为x到根节点的权值
    }
    return s[x];
}
```

hdu 1213 How many tables

```c++
#include <iostream>
#include <queue>
#include <algorithm>
using namespace std;
const int N = 1050;
int s[N];
void init_set()
{
    for (int i = 1; i <= N; i++) s[i] = i;
}
int find_set(int x)
{
    return x == s[x] ? x : find_set(s[x]);
}
void merge_set(int x, int y)
{
    x = find_set(x);
    y = find_set(y);
    if (x != y) s[x] = s[y];
}
int main()
{
    int t, n, m, x, y;
    for (cin >> t; t--; )
    {
        cin >> n >> m;
        init_set();
        for (int i = 1; i <= m; i++)
        {
            cin >> x >> y;
            merge_set(x, y);
        }
        int ans = 0;
        for (int i = 1; i <= n; i++)
            if (s[i] == i) ans++;
        cout << ans << endl;
    }
    return 0;
}
```

hdu 3038 How many answers are wrong

```c++
#include <iostream>
using namespace std;
const int maxn = 2e5 + 10;
int s[maxn];   //集
int d[maxn];   //权值，记录当前节点到根节点的权值
int ans;
void init_set()
{
    for (int i = 0; i <= maxn; i++) {s[i] = i; d[i] = 0;}
}
int find_set(int x)
{
    if (x != s[x])
    {
        int t = s[x];
        s[x] = find_set(s[x]);
        d[x] += d[t];
    }
    return s[x];
}
void merge_set(int a, int b, int v)
{
    int roota = find_set(a), rootb = find_set(b);
    if (roota == rootb)
    {
        if (d[a] - d[b] != v) ans++;
    }
    else
    {
        s[roota] = rootb;
        d[roota] = d[b] - d[a] + v;
    }
}
int main()
{
    int n, m;
    while (cin >> n >> m)
    {
        init_set();
        ans = 0;
        while (m--)
        {
            int a, b, v;
            cin >> a >> b >> v;
            a--;
            merge_set(a, b, v);
        }
        cout << " " << ans << endl;
    }
    return 0;
}
```

poj 1182 食物链

```c++
#include <algorithm>
#include <iostream>
using namespace std;
const int maxn = 5e4 + 10;
int s[maxn];   //集
int d[maxn];   //0：同类； 1：吃； 2：被吃
int ans;
void init_set()
{
    for (int i = 0; i <= maxn; i++) {s[i] = i; d[i] = 0;}
}
int find_set(int x)
{
    if (x != s[x])
    {
        int t = s[x];
        s[x] = find_set(s[x]);
        d[x] = (d[x] + d[t]) % 3;
    }
    return s[x];
}
void merge_set(int x, int y, int relation)
{
    int rootx = find_set(x), rooty = find_set(y);
    if (rootx == rooty)
    {
        if ((relation - 1) != ((d[x] - d[y] + 3) % 3)) ans++; //判断矛盾
    }
    else
    {
        s[rootx] = rooty;                                     //合并
        d[rootx] = (d[y] - d[x] + relation - 1) % 3;          //更新权值
    }
}
int main()
{
    int n, k;
    cin >> n >> k;
    init_set();
    ans = 0;
    while (k--)
    {
        int relation, x, y;
        cin >> relation >> x >> y;
        if (x > n || y > n || (relation == 2 && x == y)) ans++;
        else merge_set(x, y, relation);
    }
    cout << ans;
    return 0;
}
```

luogu p3367 

```c++
#include <iostream>
#include <queue>
#include <algorithm>
using namespace std;
int n, m, a, b, c, nums[10010];
void init_set()
{
    for (int i = 1; i <= n; i++) nums[i] = i;
}
int find_set(int x)
{
    if (x != nums[x]) nums[x] = find_set(nums[x]);
    return nums[x];
}
void merge_set(int x, int y)
{
    x = find_set(x);
    y = find_set(y);
    if (x != y) nums[x] = nums[y];
}
int main()
{
    cin >> n >> m;
    init_set();
    for (int i = 0; i < m; i++)
    {
        cin >> a >> b >> c;
        if (a & 1) merge_set(b, c);
        else
        {
            b = find_set(b);
            c = find_set(c);
            if (b == c) cout << "Y\n";
            else cout << "N\n";
        }
    }
    return 0;
}
```

B - 修复公路

```c++
#include <iostream>
#include <queue>
#include <algorithm>
using namespace std;
struct str
{
    int x;
    int y;
    int t;
}buf[100010];
int n, m, x, y, t, cnt = 1, sum, s[1010];
void init_set()
{
    for (int i = 1; i <= n; i++) s[i] = i;
}
int find_set(int x)
{
    if (x != s[x]) s[x] = find_set(s[x]);
    return s[x];
}
void merge_set(int x, int y)
{
    x = find_set(x);
    y = find_set(y);
    if (x != y)
    {
        cnt++;
        s[x] = s[y];
    }
}
bool cmp(str a, str b)
{
    return a.t < b.t;
}
int main()
{
    cin >> n >> m;
    init_set();
    for (int i = 0; i < m; i++)
    {
        cin >> x >> y >> t;
        buf[i] = {x, y, t};
    }
    sort(buf, buf + m, cmp);
    for (int i = 0; i < m; i++)
    {
        merge_set(buf[i].x, buf[i].y);
        if (cnt == n)
        {
            cout << buf[i].t << endl;
            break;
        }
        if (i == m - 1) cout << "-1";
    }
    return 0;
}
```

C - 亲戚

```c++
#include <iostream>
#include <queue>
#include <algorithm>
using namespace std;
int n, m, p, x, y, s[5010];
void init_set()
{
    for (int i = 1; i <= n; i++) s[i] = i;
}
int find_set(int x)
{
    if (x != s[x]) s[x] = find_set(s[x]);
    return s[x];
}
void merge_set(int x, int y)
{
    x = find_set(x);
    y = find_set(y);
    if (x != y) s[x] = s[y];
}
int main()
{
    cin >> n >> m >> p;
    init_set();
    while (m--)
    {
        cin >> x >> y;
        merge_set(x, y);
    }
    while (p--)
    {
        cin >> x >> y;
        x = find_set(x);
        y = find_set(y);
        if (x == y) cout << "Yes\n";
        else cout << "No\n";
    }
    return 0;
}
```

D - 一中校运会之百米跑

```c++
#include <iostream>
#include <cstring>
#include <queue>
#include <map>
using namespace std;
map<string, string> s;
int n, m, k;
string name, a, b;
string find_set(string str)
{
    if (str != s[str]) s[str] = find_set(s[str]);
    return s[str];
}
void merge_set(string x, string y)
{
    x = find_set(x);
    y = find_set(y);
    if (x != y) s[x] = s[y];
}
int main()
{
    cin >> n >> m;
    for (int i = 1; i <= n; i++)
    {
        cin >> name;
        s[name] = name;
    }
    for (int i = 0; i < m; i++)
    {
        cin >> a >> b;
        merge_set(a, b);
    }
    cin >> k;
    for (int i = 0; i < k; i++)
    {
        cin >> a >> b;
        a = find_set(a);
        b = find_set(b);
        if (a == b) cout << "Yes.\n";
        else cout << "No.\n";
    }
    return 0;
}
```

E - 朋友

```c++
#include <iostream>
#include <cstring>
#include <queue>
#include <map>
#include <algorithm>
using namespace std;
const int maxn = 1e4 + 10;
int m, n, p, q, a, b, cnta, cntb, ret;
int sa[maxn], sb[maxn];
void init_set(int s[], int n)
{
    for (int i = 1; i <= n; i++) s[i] = i;
}
int find_set(int s[], int x)
{
    if (x != s[x]) s[x] = find_set(s, s[x]);
    return s[x];
}
void merge_set(int x, int y, int s[])
{
    x = find_set(s, x);
    y = find_set(s, y);
    if (x != y && x == 1) s[y] = s[x];
    else if (x != y) s[x] = s[y];
}
int Search_set(int s[], int n)
{
    int cnt = 0;
    for (int i = 1; i <= n; i++)
        if ((ret = find_set(s, i)) == 1) cnt++;
    return cnt;
}
int main()
{
    cin >> n >> m >> p >> q;
    init_set(sa, n);
    init_set(sb, m);
    while (p--)
    {
        cin >> a >> b;
        merge_set(a, b, sa);
    }
    while (q--)
    {
        cin >> a >> b;
        merge_set(a * (-1), b * (-1), sb);
    }
    cnta = Search_set(sa, n);
    cntb = Search_set(sb, m);
    cout << min(cnta, cntb) << endl;
    return 0;
}
```

F - 家谱

```c++
#include <iostream>
#include <cstring>
#include <queue>
#include <map>
#include <algorithm>
using namespace std;
map<string, string> m;
string s, ret, name;
string find_set(string x)
{
    if (x != m[x]) m[x] = find_set(m[x]);
    return m[x];
}
int main()
{
    while (cin >> s && s[0] != '?')
    {
        name = s.substr(1, 6);
        if (s[0] == '#')
        {
            ret = name;
            if (!(m.count(name))) m[name] = name;
        }
        if (s[0] == '+') m[name] = ret;
    }
    while (s[0] != '$')
    {
        name = s.substr(1, 6);
        cout << name << " " << find_set(name) << endl;
        cin >> s;
    }
    return 0;
}
```

G - 合并果子 / [USACO06NOV] Fence Repair G

注意要将新生成的元素继续push进去

```c++
#include <iostream>
#include <cstring>
#include <queue>
#include <map>
#include <algorithm>
using namespace std;
int main()
{
    int n, a, sum = 0;
    priority_queue<int, vector<int>, greater<int>> q;
    for (cin >> n; n--; ) cin >> a, q.push(a);
    while (q.size() > 1)
    {
        int x = q.top(); q.pop();
        int y = q.top(); q.pop();
        sum += x + y;
        q.push(x + y);
    }
    cout << sum;
    return 0;
}
```

H - 世界杯

```c++
#include <iostream>
#include <cstring>
#include <queue>
#include <map>
#include <algorithm>
using namespace std;
int a, b, c, d, s;
int main()
{
    cin >> a >> b >> c >> d;
    priority_queue<int, vector<int>, less<int>> as;
    priority_queue<int, vector<int>, less<int>> bs;
    priority_queue<int, vector<int>, less<int>> cs;
    priority_queue<int, vector<int>, less<int>> ds;
    for (int i = 0; i < a; i++) cin >> s, as.push(s);
    for (int i = 0; i < b; i++) cin >> s, bs.push(s);
    for (int i = 0; i < c; i++) cin >> s, cs.push(s);
    for (int i = 0; i < d; i++) cin >> s, ds.push(s);
    for (cin >> a; a--; )
    {
        int sum = as.top();
        as.pop();
        cin >> b >> c >> d;
        while (b--) sum += bs.top(), bs.pop();
        while (c--) sum += cs.top(), cs.pop();
        while (d--) sum += ds.top(), ds.pop();
        printf("%.2f\n", sum / 11.0);
    }
    return 0;
}
```

I - 序列合并

`n`达到$10^5$, 使用枚举会超时. 先把A序列第一个和B序列所有数相加加入优先队列, 此时第一个数必定是对最小的, 因为它由A和B序列各自第一个元素组成, 后面的`n-1`的元素是第几小暂时不确定, 所以此题需要动态维护最小值, 每次操作, 都加进去上一个已知最小值的下一个可能的最小值, 注意优先队列的`pair`第一个元素储存和, 第二个元素储存的是该和对应的B序列的位置, 而`step[]`表示b序列位置对应上方走了多少步, 都是为了避免重复.

```c++
#include <algorithm>
#include <iostream>
#include <cstring>
#include <queue>
#include <map>
using namespace std;
const int maxn = 1e5 + 10;
int a[maxn], b[maxn], step[maxn], n, ret;
priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> q;
int main()
{
    scanf("%d", &n);
    for (int i = 1; i <= n; i++) scanf("%d", &a[i]);
    for (int i = 1; i <= n; i++)
    {
        scanf("%d", &b[i]);
        step[i] = 1;
        q.push(pair<int, int>(a[1] + b[i], i));
    }
    while (n--)
    {
        printf("%d ", q.top().first);
        ret = q.top().second;
        q.pop();
        q.push(pair<int, int>(a[++step[ret]] + b[ret], ret));
    }
    return 0;
}
```



J - Cow Dance Show S

"求表演时间不大于$T_{max}$ 时的K的最小可能值" 纯纯二分味道, 但是理解题意时需要特别注意，此题奶牛的出场顺序已经被固定了, 所以不用考虑什么最优组合方案, 直接加入优先队列, 按表演时间长短排序, 下一只母牛接上最先结束的母牛即可.

```c++
#include <algorithm>
#include <iostream>
#include <cstring>
#include <queue>
#include <map>
using namespace std;
int k, t, ret, a[10010];
priority_queue<int, vector<int>, greater<int>> q;
bool check(int x)
{
    for (int i = 1; i <= x; i++) q.push(a[i]);
    int sum;
    for (int i = x + 1; i <= k; i++)
    {
        int tmp = q.top() + a[i];
        q.pop(); q.push(tmp);
    }   
    while (!q.empty())
        sum = q.top(), q.pop();
    return sum <= t;
}
int main()
{
    scanf("%d%d", &k, &t);
    for (int i = 1; i <= k; i++) scanf("%d", &a[i]);
    int l = 1, r = 10000;
    while (l < r)
    {
        int mid = l + r >> 1;
        if (check(mid)) r = mid;
        else l = mid + 1;
    }
    printf("%d", l);
    return 0;
}
```

#### 树状数组

```
经典应用: 区间修改+单调查询, 区间修改+区间查询, 二维区间修改+区间查询, 区间最值
树状数组(Binary Indexed Tree, BIT)是利用数的二进制特征进行检索的一种树状结构

lowbit(x)
lowbit(x) = x&(-x), 功能是找到x的二进制数的最后一个1, 其原理是利用了负数的补码表示, 补码是原码取反加1, 令m = lowbit(x), tree[x]的值是把ax和她前面的的m个数相加的结果, 如lowbit(6) = 2, 则tree[6] = a5 + a6

tree[x]是通过lowbit()计算出的树状数组, 她能够以二分的复杂度存储一个数列的数据, 具体地, tree[x]中存储的是区间[x - lowbit(x) + 1, x]中每个数的和
```

```C++
//简单应用"单点修改+区间查询"
//复杂度都为O(logn)
#include <bits/stdc++.h>
using namespace std;
const int N = 1000;
#define lowbit(x) ((x)&-(x))
int tree[N];
void update(int x, int d)   //单点修改, 修改元素a[x]. a[x] = a[x] + d;
{
    while (x <= N)
    {
        tree[x] += d;
        x += lowbit(x);
    }
} 
int sum(int x)             //查询前缀和, 返回前缀和sum = a[1] + a[2] + ... + a[x]
{
    int ans = 0;
    while (x > 0)
    {
        ans += tree[x];
        x -= lowbie(x);
	}
    return ans;
}
int a[11] = {0, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13};   //注意a[0]不用
int main()
{
    for (int i = 1; i <= 10; i++) update(i, a[i]);  //初始化计算tree[]数组
    cout << "old: [5, 8] = " << sum(8) - sum(4) << endl;  //查询
    update(5, 100);                                       //修改
    cout << "now: [5, 8] = " << sum(8) - sum(4) << endl;
    return 0;
}
```

HDU 1556

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
#define lowbit(x) ((x) & -(x))
const int N = 100010;
int tree[N];
void update(int x, int d)
{
    while (x <= N)
    {
        tree[x] += d;
        x += lowbit(x);
    }
}
int sum(int x)
{
    int ans = 0;
    while (x > 0)
    {
        ans += tree[x];
        x -= lowbit(x);
    }
    return ans;
}
int main()
{
    int n;
    while (~scanf("%d", &n))
    {
        memset(tree, 0, sizeof tree);
        for (int i = 1; i <= n; i++)
        {
            int L, R; cin >> L >> R;
            update(L, 1);
            update(R + 1, -1);
        }
        for (int i = 1; i <= n; i++)
        {
            if (i != n) cout << sum(i) << " ";
            else cout << sum(i) << endl;
        }
    }
    return 0;
}
```

[P3372 【模板】线段树 1 - 洛谷](https://www.luogu.com.cn/problem/P3372)

$D[k]=a[k]-a[k-1]$

$a[k]=D[1]+D[2]+...+D[k]$ 

可推导得出公式 $a_1+a_2+...+a_k=k\sum_{i=1}^{k}{D_i}-\sum_{i=1}^{k}(i-1)D_i$ 

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#define lowbit(x) ((x) & -(x))
typedef long long LL;
const int N = 500010;
using namespace std;

LL tree1[N], tree2[N];
void update1(LL x, LL d) {while (x <= N) {tree1[x] += d; x += lowbit(x);}}
void update2(LL x, LL d) {while (x <= N) {tree2[x] += d; x += lowbit(x);}}
LL sum1(LL x) {LL ans = 0; while (x > 0) {ans += tree1[x]; x -= lowbit(x);} return ans;}
LL sum2(LL x) {LL ans = 0; while (x > 0) {ans += tree2[x]; x -= lowbit(x);} return ans;}
void Solve()
{
    LL n, m; cin >> n >> m;
    LL old = 0, a;
    for (int i = 1; i <= n; i++)
    {
        cin >> a;
        update1(i, a - old);
        update2(i, (i - 1) * (a - old));
        old = a;
    }
    while (m--)
    {
        LL q, L, R, d; cin >> q;
        if (q == 1)
        {
            cin >> L >> d; R = L;
            update1(L, d); update1(R + 1, -d);
            update2(L, (L - 1) * d); update2(R + 1, R * (-d));
        }
        else
        {
            cin >> L >> R;
            cout << R * sum1(R) - sum2(R) - (L - 1) * sum1(L - 1) + sum2(L - 1) << endl;
        }
    }
    return;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie();
        Solve();
    return 0;
}
```

[P4514 上帝造题的七分钟 - 洛谷](https://www.luogu.com.cn/problem/P4514)

**二维区间修改+区间查询**   利用4个二维数组完成

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#define lowbit(x) ((x) & -(x))
const int N = 2050;
using namespace std;
int n, m;
int t1[N][N], t2[N][N], t3[N][N], t4[N][N];
void update(int x, int y, int d)
{
    for (int i = x; i <= n; i += lowbit(i))
        for (int j = y; j <= m; j += lowbit(j))
        {
            t1[i][j] += d; t2[i][j] += x * d;
            t3[i][j] += y * d; t4[i][j] += x * y * d;
        }
}
int sum(int x, int y)
{
    int ans = 0;
    for (int i = x; i > 0; i -= lowbit(i))
        for (int j = y; j > 0; j -= lowbit(j))
            ans += (x + 1) * (y + 1) * t1[i][j] - (y + 1) * t2[i][j] - (x + 1) * t3[i][j] + t4[i][j];
    return ans;
}
void Solve()
{
    char ch[2]; cin >> ch;
    cin >> n >> m;
    while (cin >> ch)
    {
        int a, b, c, d, delta; cin >> a >> b >> c >> d;
        if (ch[0] == 'L')
        {
            cin >> delta;
            update(a, b, delta); update(c + 1, d + 1, delta);
            update(a, d + 1, -delta); update(c + 1, b, -delta);
        }
        else cout << sum(c, d) + sum(a - 1, b - 1) - sum(a - 1, d) - sum(c, b - 1) << endl;
    }
    return;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie();
        Solve();
    return 0;
}
```

[P1908 逆序对 - 洛谷](https://www.luogu.com.cn/problem/P1908)

**偏序问题(逆序对+离散化)**

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#define lowbit(x) ((x) & -(x))
typedef long long LL;
const int N = 500010;
using namespace std;
int tree[N], rankk[N], n;  //注意rank是C++保留字, 如果加了using namespace std, 编译不能通过, 可以使用std::或修改变量名
struct point{int num, val;}a[N];
bool cmp(point x, point y)
{
    if (x.val == y.val) return x.num < y.num;  //如果相等, 则先出现的更小
    return x.val < y.val;
}
void update(int x, int d)
{
    while (x <= N)
    {
        tree[x] += d;
        x += lowbit(x);
    }
}
LL sum(int x)
{
    LL ans = 0;
    while (x > 0)
    {
        ans += tree[x];
        x -= lowbit(x);
    }
    return ans;
}
void Solve()
{
    cin >> n;
    for (int i = 1; i <= n; i++) {cin >> a[i].val; a[i].num = i;}  //记录顺序, 用于离散化
    sort(a + 1, a + 1 + n, cmp);
    for (int i = 1; i <= n; i++) rankk[a[i].num] = i;              //离散化, 得到新的数字序列rankk()
    long long ans = 0;
    /*for (int i = 1; i <= n; i++)   //正序处理
    {
    	update(rankk[i], 1);
    	ans += i - sum(rankk[i]);
	} */
    for (int i = n; i > 0; i--)      //倒序处理
    {
        update(rankk[i], 1);
        ans += sum(rankk[i] - 1);
    }
    cout << ans;
    return;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie();
        Solve();
    return 0;
}
```

HDU 1754

**区间最值**

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#define lowbit(x) ((x) & -(x))
const int N = 2e5 + 10;
using namespace std;
int n, m, a[N], tree[N];
void update(int x, int value)
{
    while (x <= n)
    {
        tree[x] = value;
        for (int i = 1; i < lowbit(x); i <<= 1)  //用子节点更新自己
            tree[x] = max(tree[x], tree[x - i]);
        x += lowbit(x);  //父节点
    }
}
int query(int L, int R)
{
    int ans = 0;
    while (L <= R)
    {
        ans = max(ans, a[R]);
        R--;
        while (R - L >= lowbit(R))
        {
            ans = max(ans, tree[R]);
            R -= lowbit(R);
        }
    }
    return ans;
}
void Solve()
{
    while (cin >> n >> m)
    {
        memset(tree, 0, sizeof tree);
        for (int i = 1; i <= n; i++) {cin >> a[i]; update(i, a[i]);}
        while (m--)
        {
            char s[5]; int A, B; cin >> s >> A >> B;
            if (s[0] == 'Q') cout << query(A, B) << endl;
            else {a[A] = B; update(A, B);}
        }
    }
    return;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie();
        Solve();
    return 0;
}
```

HDU 4630 No pains no game

**离线处理**

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <string>
#include <vector>
#include <queue>
#include <cmath>
#include <set>
#include <map>
#define lowbit(x) ((x) & -(x))
typedef long long LL;
const int N = 5e4 + 10;//
const long long INF = 0x3f3f3f3f3f3f3f3fLL;
const int inf = 0x3f3f3f3f;
using namespace std;

int n;
vector<int> v[N];
int b[N], res[N], pos[N], maxx[N];
struct node
{
    int l, r, id;
    bool operator < (const node &a) const
    {return r < a.id;}
}a[N];
void add(int x, int d)
{
    for (; x; x -= lowbit(x))
        maxx[x] = max(maxx[x], d);   //传入的最大公因数不仅适用于该位置, 还适用于该位置前面所有的位置, 最大值要不断更新
}
int ask(int x)
{
    int res = 0;
    for ( ; x <= n; x += lowbit(x))
        res = max(res, maxx[x]);    //由于只操作了[1, r]位置的数的最大公约数, 所以取[l, r]的最大公约数直接取[l, n]即可
    return res;
}
void Solve()
{
    for (int i = 1; i <= 50000; i++)
        for (int j = i; j <= 50000; j += i)
            v[j].push_back(i);            //存储每个数的因子
    int t, q, x, y, val;
    for (cin >> t; t--; )
    {
        memset(maxx, 0, sizeof maxx);
        memset(res, 0, sizeof res);
        memset(pos, 0, sizeof pos);
        cin >> n;
        for (int i = 1; i <= n; i++) cin >> b[i];
        cin >> q;
        for (int i = 1; i <= q; i++)    //离线处理, 先存储问题, 再按照排序后的顺序分别求的答案, 最后一起输出
        {
            cin >> a[i].l >> a[i].r;
            a[i].id = i;
        }
        sort(a + 1, a + 1 + q);     //按r从小到大排列
        for (int i = 1, j = 1; i <= n; i++)
        {
            for (int k = 0; k < v[b[i]].size(); k++)
            {
                if (pos[v[b[i]][k]])
                    add(pos[v[b[i]][k]], v[b[i]][k]);
                pos[v[b[i]][k]] = i;
            }
            while (j <= q && a[j].r == i)
            {
                if (a[j].l == a[j].r) res[a[j].id] = 0;
                else res[a[j].id] = ask(a[j].l);
                j++;
            }
        }
        for (int i = 1; i <= q; i++)     //统一输出
            cout << res[i] << endl;
    }
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie();
        Solve();
    return 0;
}
```



#### 线段树

```c++
线段树(Segment Tree)和树状数组都是用于解决区间问题的数据结构
可以概括为：“分治思想 + 二叉树结构 + Lazy-Tag技术”
基础应用场景：
1.区间最值问题，包括求最值和修改元素，单点修改直接修改叶子节点上的元素值即可，区间修改需要使用Lazy-Tag技术
2.区间和问题
线段树适合解决的问题的特征是：大区间的解可以从小区间的解合并而来，且适用于动态维护的数组

线段树的构造
编码时可以定义标准的二叉树数据结构储存线段树，不过竞赛中一般使用静态数组实现满二叉树，虽然比较浪费空间，但是编码时较简单
下面代码都使用静态分配的数组tree[]，父节点与子节点之间的访问非常简单，缺点是最后一行有大量节点被浪费
    
//定义根节点是tree[1], 即编号为1的节点是根
//第1种方法：定义二叉树数据结构
struct 
{
	int L, R, data;     //用tree[i].data记录线段i的最值或者区间和
}tree[N * 4];           //静态分配数组，开4倍空间
//第2种方法：直接用数组表示二叉树，更节省空间
int tree[N * 4]         //用tree[i]记录线段i的最值或区间和
//以上两种方法都满足下面的父子关系，p是父节点，ls(p)是左儿子，rs(p)是右儿子
int ls(int p) {return p << 1;}     //左儿子，编号是p * 2
int rs(int p) {return p << 1|1;}   //右儿子，编号是p * 2 + 1

构造线段树代码如下
void push_up(int p)                               //从上向下传递区间值
{
    tree[p] = tree[ls(p)] + tree[rs(p)];          //区间和
    //tree[p] = min(tree[ls(p)], tree[rs(p)]);    //求最小值
}
void build(int p, int pl, int pr)                 //节点编号p指向区间[pl, pr]
{
    if (pl == pr) {tree[p] = a[p1]; return;}      //最底层叶子节点，有叶子节点的值
    int mid = (pl + pr) >> 1;					//分治：折半
    build(ls(p), pl, mid);                        //递归左儿子
    buiild(rs(p), mid + 1, pr);                   //递归右儿子
    push_up(p);                                   //从下往上传递区间值
}


区间查询代码
int query(int L, int R, int p, int pl, int pr)
{
    if (L <= pl && R >= pr) return tree[p];       //完全覆盖
    int mid = (pl + pr) >> 1;
    if (L <= mid) res += query(L, R, ls(p), pl, mid);     //L与左子节点有重叠
    if (R > mid) ret += query(L, R, rs(p), mid + 1, pr);  //R与右子节点有重叠
    return res;
}   //调用方式：query(L, R, l, l, n);
```

luogu P3372 【模板】线段树 1

**区间修改和查询区间和**

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
using namespace std;
using LL = long long;
const int N = 1e5 + 10;
LL a[N];
LL tree[N << 2];
LL tag[N << 2];
LL ls(LL p) {return p << 1;}
LL rs(LL p) {return p << 1|1;}
void push_up(LL p)
{
    tree[p] = tree[ls(p)] + tree[rs(p)];
}
void build(LL p, LL pl, LL pr)
{
    tag[p] = 0;
    if (pl == pr) {tree[p] = a[pl]; return;}
    LL mid = (pl + pr) >> 1;
    build(ls(p), pl, mid);
    build(rs(p), mid + 1, pr);
    push_up(p);
}
void addtag(LL p, LL pl, LL pr, LL d)
{
    tag[p] += d;
    tree[p] += d * (pr - pl + 1);
}
void push_down(LL p, LL pl, LL pr)
{
    if (tag[p])
    {
        LL mid = (pl + pr) >> 1;
        addtag(ls(p), pl, mid, tag[p]);
        addtag(rs(p), mid + 1, pr, tag[p]);
        tag[p] = 0;
    }
}
void update(LL L, LL R, LL p, LL pl, LL pr, LL d)
{
    if (L <= pl && pr <= R)
    {
        addtag(p, pl, pr, d);
        return;
    }
    push_down(p, pl, pr);
    LL mid = (pl + pr) >> 1;
    if (L <= mid) update(L, R, ls(p), pl, mid, d);
    if (R > mid) update(L, R, rs(p), mid + 1, pr, d);
    push_up(p); 
}
LL query(LL L, LL R, LL p, LL pl, LL pr)
{
    if (pl >= L && pr <= R) return tree[p];
    push_down(p, pl, pr);
    LL res = 0;
    LL mid = (pl + pr) >> 1;
    if (L <= mid) res += query(L, R, ls(p), pl, mid);
    if (R > mid) res += query(L, R, rs(p), mid + 1, pr);
    return res;
}
int main()
{
    LL n, m; cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> a[i];
    build(1, 1, n);    //建树
    while (m--)
    {
        LL q, L, R, d; cin >> q;
        if (q == 1)
        {
            cin >> L >> R >> d;
            update(L, R, 1, 1, n, d);
        }
        else
        {
            cin >> L >> R;
            cout << query(L, R, 1, 1, n) << endl;
        }
    }
    return 0;
}
```

luogu P1868 忠诚

**查询区间最小值**

```c++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
using LL = long long;
const LL N = 1e5 + 10, INF = 0x3f3f3f3f3f3f3f3fLL;
LL a[N], tree[N << 2];
LL ls(LL p) {return p << 1;}
LL rs(LL p) {return p << 1|1;}
void push_up(LL p)
{
    tree[p] = min(tree[ls(p)], tree[rs(p)]);
}
void build(LL p, LL pl, LL pr)
{
    if (pl == pr) {tree[p] = a[pl]; return;}
    LL mid = (pl + pr) >> 1;
    build(ls(p), pl, mid);
    build(rs(p), mid + 1, pr);
    push_up(p);
}
LL findmin(LL L, LL R, LL p, LL pl, LL pr)
{
    if (pl >= L && pr <= R) return tree[p];
    LL mid = (pl + pr) >> 1, a = INF, b = INF;
    if (L <= mid) a = findmin(L, R, ls(p), pl, mid); 
    if (R > mid) b = findmin(L, R, rs(p), mid + 1, pr);
    return min(a, b);
}
vector<LL> ans;
int main()
{
    LL m, n; cin >> m >> n;
    for (LL i = 1; i <= m; i++) cin >> a[i];
    build(1, 1, m);
    while (n--)
    {
        LL L, R; cin >> L >> R;
        ans.push_back(findmin(L, R, 1, 1, m));
    }
    for (LL i = 0; i < ans.size(); i++) printf(" %lld" + !i, ans[i]);
    return 0;
}
```

[P3870 TJOI2009 开关 - 洛谷](https://www.luogu.com.cn/problem/P3870)

异或

```c++
#include <bits/stdc++.h>
const int N = 1e5 + 10;
using namespace std;
int tree[N << 2], tag[N << 2];
int ls(int p) {return p << 1;}
int rs(int p) {return p << 1|1; } 
int n, m, c, L, R;
void addtag(int p, int pl, int pr)
{
    tag[p] ^= 1;
    tree[p] = (pr - pl + 1) - tree[p];
}
void push_up(int p)
{
    tree[p] = tree[ls(p)] + tree[rs(p)];
}
void push_down(int p, int pl, int pr)
{
    if (tag[p])
    {
        int mid = (pl + pr) >> 1;
        addtag(ls(p), pl, mid);
        addtag(rs(p), mid + 1, pr);
        tag[p] = 0;
    }
}
void update(int L, int R, int p, int pl, int pr)
{
    if (L <= pl && pr <= R)
    {
        addtag(p, pl, pr);
        return;
    }
    push_down(p, pl, pr);
    int mid = (pl + pr) >> 1;
    if (L <= mid) update(L, R, ls(p), pl, mid);
    if (R > mid) update(L, R, rs(p), mid + 1, pr);
    push_up(p);
}
int query(int L, int R, int p, int pl, int pr)
{
    if (L <= pl && pr <= R) return tree[p];
    push_down(p, pl, pr);
    int res = 0;
    int mid = (pl + pr) >> 1;
    if (L <= mid) res += query(L, R, ls(p), pl, mid);
    if (R > mid) res += query(L, R, rs(p), mid + 1, pr);
    return res;
}
void Solve()
{
    cin >> n >> m;
    while (m--)
    {
        cin >> c >> L >> R;
        if (c) cout << query(L, R, 1, 1, n) << endl;
        else update(L, R, 1, 1, n);
    }
    return;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie();
        Solve();
    return 0;
}
```

[P3373 【模板】线段树 2 - 洛谷](https://www.luogu.com.cn/problem/P3373)

此题关键在于有两个修改操作, 而且两个操作是存在影响关系的, 因为乘法操作会使得所有数都被乘, 也就是说包括"增加"的部分, 所以在更新的时候, 修改乘法tag的时候也要同时修改已经存在的加法tag, 这是最容易忽略的地方, 此题一开始使用两个tag, 但是一直wa, 理论上不应该, 换用struct能ac

```c++
#include <bits/stdc++.h>
const int N = 1e5 + 10;
using LL = long long;
using namespace std;
LL n, m, mod;
LL a[N];
struct str
{
    LL val, add, mul;
}tr[N << 2];
LL ls(LL p) {return p << 1;}
LL rs(LL p) {return p << 1|1;}
void push_up(LL p)
{
    tr[p].val = (tr[ls(p)].val + tr[rs(p)].val) % mod;
}
void build(LL p, LL pl, LL pr)
{
    tr[p].mul = 1; tr[p].add = 0;
    if (pl == pr) {tr[p].val = a[pl]; return;}
    LL mid = (pl + pr) >> 1;
    build(ls(p), pl, mid);
    build(rs(p), mid + 1, pr);
    push_up(p);
}
void addtag1(LL p, LL pl, LL pr, LL k)
{
    tr[p].mul = tr[p].mul * k % mod;
    tr[p].val = k * tr[p].val % mod;
    tr[p].add = tr[p].add * k % mod;   //关键
}
//核心代码push_down
void push_down(LL p, LL pl, LL pr)
{
    LL mid = (pl + pr) >> 1;
    tr[ls(p)].val = (tr[ls(p)].val * tr[p].mul + tr[p].add * (mid - pl + 1)) % mod;
    tr[rs(p)].val = (tr[rs(p)].val * tr[p].mul + tr[p].add * (pr - mid)) % mod;
    tr[ls(p)].mul = tr[ls(p)].mul * tr[p].mul % mod;
    tr[rs(p)].mul = tr[rs(p)].mul * tr[p].mul % mod;
    tr[ls(p)].add = (tr[ls(p)].add * tr[p].mul + tr[p].add) % mod;
    tr[rs(p)].add = (tr[rs(p)].add * tr[p].mul + tr[p].add) % mod;
    tr[p].mul = 1; tr[p].add = 0;
    return;
}

void update1(LL L, LL R, LL p, LL pl, LL pr, LL k)
{
    if (L <= pl && pr <= R)
    {
        addtag1(p, pl, pr, k);
        return;
    }
    push_down(p, pl, pr);
    LL mid = (pl + pr) >> 1;
    if (L <= mid) update1(L, R, ls(p), pl, mid, k);
    if (R > mid) update1(L, R, rs(p), mid + 1, pr, k);
    push_up(p);
}
void addtag2(LL p, LL pl, LL pr, LL k)
{
    (tr[p].add += k) % mod;
    (tr[p].val += (pr - pl + 1) * k) % mod;
}
void update2(LL L, LL R, LL p, LL pl, LL pr, LL k)
{
    if (L <= pl && pr <= R)
    {
        addtag2(p, pl, pr, k);
        return;
    }
    push_down(p, pl, pr);
    LL mid = (pl + pr) >> 1;
    if (L <= mid) update2(L, R, ls(p), pl, mid, k);
    if (R > mid) update2(L, R, rs(p), mid + 1, pr, k);
    push_up(p); 
}
LL query(LL L, LL R, LL p, LL pl, LL pr)
{
    if (L <= pl && pr <= R) return tr[p].val;
    push_down(p, pl, pr);
    LL mid = (pl + pr) >> 1, res = 0;
    if (L <= mid) res += query(L, R, ls(p), pl, mid);
    if (R > mid) res += query(L, R, rs(p), mid + 1, pr);
    return res % mod;
}
void Solve()
{
    cin >> n >> m >> mod;
    for (int i = 1; i <= n; i++) cin >> a[i];
    build(1, 1, n);
    while (m--)
    {
        LL num, x, y, k; cin >> num;
        if (num == 1)
        {
            cin >> x >> y >> k;
            update1(x, y, 1, 1, n, k);
        }
        else if (num == 2)
        {
            cin >> x >> y >> k;
            update2(x, y, 1, 1, n, k);
        }
        else
        {
            cin >> x >> y;
            cout << query(x, y, 1, 1, n) << endl;
        }
    }
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie();
        Solve();
    return 0;
}
```

[P1438 无聊的数列 - 洛谷](https://www.luogu.com.cn/problem/P1438)

称差分序列首项为`s`，末项为`e`，公差为`d`，要将$[l-r]$这段区间加上等差序列, 如果要在差分序列上加一个等差序列，则要在$a_l$加上s, $[a_{l+1},a_r]$ 加上`d`, $a_{r+1}$ 加上`-e`, 注意根据l和r的关系判断一些特殊情况, 比如`l=r`, 或者`r=n`, 用线段树即可, 答案即为$\sum_{n}^{i=1}a[i]$

```c++
#include <bits/stdc++.h>
const int N = 2e5 + 10;
using LL = long long;
using namespace std;

LL tree[N << 2], tag[N << 2];
int a[N], b[N];
int n, m, opt, l, r, k, d, q;
void push_up(int p)
{
    tree[p] = tree[p << 1] + tree[p << 1|1];
}
void build(int p, int pl, int pr)
{
    if (pl == pr) {tree[p] = b[pl]; return;}
    int mid = (pl + pr) >> 1;
    build(p << 1, pl, mid);
    build(p << 1|1, mid + 1, pr);
    push_up(p);
}
void addtag(int p, int pl, int pr, int d)
{
    tag[p] += d;
    tree[p] += (pr - pl + 1) * d;
}
void push_down(int p, int pl, int pr)
{
    if (tag[p])
    {
        int mid = (pl + pr) >> 1;
        addtag(p << 1, pl, mid, tag[p]);
        addtag(p << 1|1, mid + 1, pr, tag[p]);
        tag[p] = 0;
    }
}
void update(int L, int R, int p, int pl, int pr, int d)
{
    if (L <= pl && R >= pr)
    {addtag(p, pl, pr, d); return;}
    push_down(p, pl, pr);
    int mid = (pl + pr) >> 1;
    if (L <= mid) update(L, R, p << 1, pl, mid, d);
    if (R > mid) update(L, R, p << 1|1, mid + 1, pr, d);
    push_up(p);
}
LL query(int L, int R, int p, int pl, int pr)
{
    if (L <= pl && R >= pr) {return tree[p];}
    push_down(p, pl, pr);
    int mid = (pl + pr) >> 1;
    LL res = 0;
    if (L <= mid) res += query(L, R, p << 1, pl, mid);
    if (R > mid) res += query(L, R, p << 1|1, mid + 1, pr);
    return res;
}   
void Solve()
{
    cin >> n >> m;
    for (int i = 1; i <= n; i++) 
        {cin >> a[i]; b[i] = a[i] - a[i - 1];}
    build(1, 1, n);
    while (m--)
    {
        cin >> opt;
        if (opt == 1)
        {
            cin >> l >> r >> k >> d;
            update(l, l, 1, 1, n, k);
            if (l + 1 <= r) update(l + 1, r, 1, 1, n, d);
            if (r + 1 <= n) update(r + 1, r + 1, 1, 1, n, -(k + (r - l) * d));
        }
        else
        {
            cin >> q;
            cout << query(1, q, 1, 1, n) << endl;
        }
    }
    return;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie();
    // int t;
    // for (cin >> t; t--; )
        Solve();
    return 0;
}
```

[P4588 TJOI2018 数学计算 - 洛谷](https://www.luogu.com.cn/problem/P4588)

区间乘

```c++
#include <bits/stdc++.h>
const int N = 1e5 + 10;
using LL = long long;
using namespace std;
#define int long long
int n, m, op, M;
int tree[N << 2];
void push_up(int p)
{
    tree[p] = tree[p << 1] * tree[p << 1|1] % m;
}
void build(int p, int pl, int pr)
{
    if (pl == pr) {tree[p] = 1; return;}
    int mid = pl + pr >> 1;
    build(p << 1, pl, mid);
    build(p << 1|1, mid + 1, pr);
    push_up(p);
}
void update(int L, int R, int p, int pl, int pr, int d)
{
    if (L <= pl && R >= pr) {tree[p] = d; return;}
    int mid = pl + pr >> 1;
    if (L <= mid) update(L, R, p << 1, pl, mid, d);
    if (R > mid) update(L, R, p << 1|1, mid + 1, pr, d);
    push_up(p);
}
void Solve()
{
    memset(tree, 0, sizeof tree);
    cin >> n >> m;
    build(1, 1, n);
    for (int i = 1; i <= n; i++)
    {
        cin >> op >> M;
        if (op == 1) update(i, i, 1, 1, n, M);
        else update(M, M, 1, 1, n, 1);
        cout << tree[1] % m << endl;
    }
    return;
}
signed main()
{
    ios::sync_with_stdio(false);
    cin.tie();
    int t;
    for (cin >> t; t--; )
        Solve();
    // return 0;
}
```

[P2184 贪婪大陆 - 洛谷](https://www.luogu.com.cn/problem/P2184)

记录左端点和右端点个数即可, `[l, r]`区间内地雷种类数等于`[1, r]`区间内左端点个数减去`[1, L - 1]`区间内右端点个数

```c++
#include <bits/stdc++.h>
const int N = 1e5 + 10;
using LL = long long;
using namespace std;

int n, m, q, L, R;
struct node
{
    int l, r;
}tree[N << 2];
void push_up(int p)
{
    tree[p].l = tree[p << 1].l + tree[p << 1|1].l;
    tree[p].r = tree[p << 1].r + tree[p << 1|1].r;
}
void update(int opt, int L, int R, int p, int pl, int pr)
{
    if (L <= pl && R >= pr)
    {
        if (opt == 1) tree[p].l += 1;
        else tree[p].r += 1;    
        return;
    }
    int mid = pl + pr >> 1;
    if (L <= mid) update(opt, L, R, p << 1, pl, mid);
    if (R > mid) update(opt, L, R, p << 1|1, mid + 1, pr);
    push_up(p);
}
int query(int opt, int L, int R, int p, int pl, int pr)
{
    if (L <= pl && R >= pr)
    {
        if (opt == 1) return tree[p].l;
        else return tree[p].r;
    }
    int mid = pl + pr >> 1, res = 0;
    if (L <= mid) res += query(opt, L, R, p << 1, pl, mid);
    if (R > mid) res += query(opt, L, R, p << 1|1, mid + 1, pr);
    return res;
}
void Solve()
{
    cin >> n >> m;
    while (m--)
    {
        cin >> q >> L >> R;
        if (q == 1)
        {
            update(1, L, L, 1, 1, n);
            update(2, R, R, 1, 1, n);
        }
        else
        {
            int x = query(1, R, R, 1, 1, n);
            int y = query(2, L - 1, L - 1, 1, 1, n);
            cout << query(1, 1, R, 1, 1, n) - query(2, 1, L - 1, 1, 1, n) << endl;
        }
    }
    return;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie();
        Solve();
    return 0;
}
```

[P2572 SCOI2010 序列操作 - 洛谷](https://www.luogu.com.cn/problem/P2572)   **%%%**

出现区间取反操作, 不仅要记录1的信息, 也要记录0的信息, 对于一个点要维护8个信息, 1/0的个数, 左/右边起1/0的最长长度, 整段区间中1/0的连续最长长度, 使用结构体更加便利, 注意更新的时候细节的处理, 此题的操作方法值得学习

```c++
#include <bits/stdc++.h>
const int N = 1e5 + 10;
using LL = long long;
using namespace std;

int n, q, a[N];
struct node  //构建结构体的同时, 写载入函数
{
    int w, b, lw, lb, rw, rb, mw, mb;
    node(int a1 = 0, int a2 = 0, int a3 = 0, int a4 = 0, int a5 = 0, int a6 = 0, int a7 = 0, int a8 = 0)
    {w = a1; b = a2; lw = a3; lb = a4; rw = a5; rb = a6; mw = a7; mb = a8;}
};
node push_up(node i, node j)  //不同以往的push_up函数, 返回的是tree[i]
{
    return node(
        i.w + j.w, i.b + j.b,
        (i.b ? i.lw : i.w + j.lw), (i.w ? i.lb : i.b + j.lb),
        (j.b ? j.rw : j.w + i.rw), (j.w ? j.rb : j.b + i.rb),
        max(max(i.mw, j.mw), i.rw + j.lw),
        max(max(i.mb, j.mb), i.rb + j.lb));
}
node tree[N << 2];
int len[N << 2], tag1[N << 2], tag2[N << 2];
void P(int i, int typ)
{
    node &t = tree[i];   //细节取地址, 减少码量, 便于修改
    if (typ == 0)
        tag2[i] = 0, tag1[i] = 0, t = node(0, len[i], 0, len[i], 0, len[i], 0, len[i]);
    if (typ == 1)
        tag2[i] = 0, tag1[i] = 1, t = node(len[i], 0, len[i], 0, len[i], 0, len[i], 0);
    if (typ == 2)
        tag2[i] ^= 1, swap(t.w, t.b), swap(t.lw, t.lb), swap(t.rw, t.rb), swap(t.mw, t.mb);
}
void push_down(int i)
{
    if (~tag1[i])
        P(i << 1, tag1[i]), P(i << 1 | 1, tag1[i]);
    if (tag2[i])
        P(i << 1, 2), P(i << 1 | 1, 2);
    tag1[i] = -1, tag2[i] = 0;
}
void build(int i, int l, int r)
{
    len[i] = r - l + 1;
    tag1[i] = -1;    //区间赋值,没有标记时为-1,有标记时为0或1
    if (l == r)
    {
        int t = a[l];
        tree[i] = node(t, t ^ 1, t, t ^ 1, t, t ^ 1, t, t ^ 1);
        return;
    }
    build(i << 1, l, l + r >> 1);
    build(i << 1 | 1, (l + r >> 1) + 1, r);
    tree[i] = push_up(tree[i << 1], tree[i << 1 | 1]);
}
void update(int i, int l, int r, int a, int b, int t)
{
    if (b < l || r < a)
        return;
    if (a <= l && r <= b)
    {
        P(i, t);
        return;
    }
    push_down(i);
    update(i << 1, l, l + r >> 1, a, b, t), update(i << 1 | 1, (l + r >> 1) + 1, r, a, b, t);
    tree[i] = push_up(tree[i << 1], tree[i << 1 | 1]);
}
node query(int i, int l, int r, int a, int b)  //不同以往的query()函数,
{
    if (b < l || r < a)
        return node();  //如果不在此区间, 返回一个全为0的node()即可
    if (a <= l && r <= b)
        return tree[i];
    push_down(i);
    return push_up(query(i << 1, l, l + r >> 1, a, b), query(i << 1 | 1, (l + r >> 1) + 1, r, a, b));
}
int main()
{
    cin >> n >> q;
    for (int i = 1; i <= n; ++i) cin >> a[i];
    build(1, 1, n);
    for (int i = 1; i <= q; ++i)
    {
        int opt, l, r;
        cin >> opt >> l >> r;
        l++; r++;
        if (opt < 3) update(1, 1, n, l, r, opt);
        else
        {
            node t = query(1, 1, n, l, r);
            cout << (opt == 3 ? t.w : t.mw) << endl;
        }
    }
    return 0;
}
```

```
//failed try
int n, m;
int a[N];
struct node
{
    int l_0, r_0, l_1, r_1, a0, a1, cnt0, cnt1;
    int tag1, tag2, len;
    node(int l_0 = 0, int r_0 = 0, int l_1 = 0, int r_1 = 0, int a0 = 0, int a1 = 0, int cnt0 = 0, int cnt1 = 0, int tag1 = -1, int tag2 = 0, int len = 0):
    l_0(l_0), r_0(r_0), l_1(l_0), r_1(r_1), a0(a0), a1(a1), cnt0(cnt0), cnt1(cnt1), tag1(tag1), tag2(tag2), len(len) {}
};
node tree[N << 2];
node push_up(node i, node j)
{
    return node(
        i.cnt1 ? i.l_0 : i.l_0 + j.l_0, j.cnt1 ? j.r_0 : j.r_0 + i.r_0,
        i.cnt0 ? i.l_1 : i.l_1 + j.l_1, j.cnt0 ? j.r_1 : j.r_1 + i.r_1,
        max(max(i.a0, j.a0), i.r_0 + j.l_0), max(max(i.a1, j.a1), i.r_1 + j.l_1),
        i.cnt0 + j.cnt0, i.cnt1 + j.cnt1, -1, 0, i.len + j.len);
}
void build(int p, int pl, int pr)
{
    tree[p].len = pr - pl + 1;
    tree[p].tag1 = -1; tree[p].tag2 = 0;
    if (pl == pr)
    {int t = a[pl]; tree[p] = node(t^1, t^1, t, t, t^1, t, t^1, t); return;}
    int mid = pl + pr >> 1;
    build(p << 1, pl, mid);
    build(p << 1|1, mid + 1, pr);
    tree[p] = push_up(tree[p << 1], tree[p << 1|1]);
}
void addtag(int p, int opt)
{
    node&t = tree[p];
    if (opt == 0) {t.tag2 = t.tag1 = 0; t = node(t.len, t.len, 0, 0, t.len, 0, t.len, 0);}
    if (opt == 1) {t.tag2 = 0; t.tag1 = 1; t = node(0, 0, t.len, t.len, 0, t.len, 0, t.len);}
    if (opt == 2) {t.tag2 ^= 1; swap(t.l_0, t.l_1); swap(t.r_0, t.r_1); swap(t.a0, t.a1); swap(t.cnt0, t.cnt1);}
}
void push_down(int p)
{
    if (~tree[p].tag1) addtag(p << 1, tree[p].tag1), addtag(p << 1|1, tree[p].tag1);
    if (tree[p].tag2) addtag(p << 1, 2), addtag(p << 1|1, 2);
    tree[p].tag1 = -1; tree[p].tag2 = 0;
}
void update(int L, int R, int p, int pl, int pr, int opt)
{
    if (L <= pl && R >= pr) {addtag(p, opt); return;}
    push_down(p);
    int mid = pl + pr >> 1;
    if (L <= mid) update(L, R, p << 1, pl, mid, opt);
    if (R > mid) update(L, R, p << 1|1, mid + 1, pr, opt);
    tree[p] = push_up(tree[p << 1], tree[p << 1|1]);
}
node query(int L, int R, int p, int pl, int pr)
{
    if (L > pr || R < pl) return node();
    if (L <= pl && R >= pr) return tree[p];
    push_down(p);
    int mid = pl + pr >> 1;
    return push_up(query(L, R, p << 1, pl, mid), query(L, R, p << 1|1, mid + 1, pr));
    // if (L <= mid && R > mid) return push_up(query(L, mid, p << 1, pl, mid), query(mid + 1, R, p << 1|1, mid + 1, pr));
    // else if (L <= mid) return query(L, R, p << 1, pl, pr);
    // else if (R > mid) return query(L, R, p << 1|1, mid + 1, pr);
}
void Solve()
{
    cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> a[i];
    build(1, 1, n);
    while (m--)
    {
        int opt, l, r;
        cin >> opt >> l >> r; l++; r++;
        if (opt < 3) update(l, r, 1, 1, n, opt);
        else {node t = query(l, r, 1, 1, n); cout << (opt == 3 ? t.cnt1 : t.a1) << endl;}
    }
    return;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie();
    // int t;
    // for (cin >> t; t--; )
        Solve();
    return 0;
}

```

[P4215 踩气球 - 洛谷](https://www.luogu.com.cn/problem/P4215)

此题若简单使用区间修改和查询区间和是否为`0`, 会导致`TLE`, 而且题目强制在线, 所以我们采用另一种方法, 对于每一个查询区间, 在其所有子区间记录下该区间的编号, 并且记录该查询区间的子区间数目. 后续每一次操作, 如果出现某一个`tree[p].val == 0`, 则将这个`tree[p]`上所有的区间编号的子区间数目减`1`, 直到子区间数目为`0`, 则说明该区间已经变为`0`, 符合题目要求, `ans += 1`即可.

```c++
#include <bits/stdc++.h>
const int N = 1e5 + 10;
using LL = long long;
using namespace std;
int n, m, q, ans;
int a[N];
struct str {int l, r, s;}itval[N];
struct strr {int val; vector<int> v;}tree[N << 2];
void push_up(int p)
{
    tree[p].val = tree[p << 1].val + tree[p << 1|1].val;
}
void build(int p, int pl, int pr)
{
    if (pl == pr) {tree[p].val = a[pl]; return;}
    int mid = pl + pr >> 1;
    build(p << 1, pl, mid);
    build(p << 1|1, mid + 1, pr);
    push_up(p);
}
void split(int L, int R, int p, int pl, int pr, int i)
{
    if (L <= pl && R >= pr)
    {tree[p].v.push_back(i); itval[i].s++; return;}
    int mid = pl + pr >> 1;
    if (L <= mid) split(L, R, p << 1, pl, mid, i);
    if (R > mid) split(L, R, p << 1|1, mid + 1, pr, i);
}
void update(int L, int R, int p, int pl, int pr, int d)
{
    if (L <= pl && R >= pr)
    {
        tree[p].val += d;
        if (tree[p].val == 0)
        {
            for (auto i : tree[p].v)
            {
                itval[i].s--;
                if (itval[i].s == 0) ans++;
            }
        }
        return;
    }
    int mid = pl + pr >> 1;
    if (L <= mid) update(L, R, p << 1, pl, mid, -1);
    if (R > mid) update(L, R, p << 1|1, mid + 1, pr, -1);
    push_up(p);
    if (tree[p].val == 0)
    {
        for (auto i : tree[p].v)
        {
            itval[i].s--;
            if (itval[i].s == 0) ans++;
        }
    }
}
void Solve()
{
    cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> a[i];
    for (int i = 1; i <= m; i++) cin >> itval[i].l >> itval[i].r;
    build(1, 1, n);
    for (int i = 1; i <= m; i++) split(itval[i].l, itval[i].r, 1, 1, n, i);
    cin >> q;
    for (int i = 1; i <= q; i++)
    {
        int x; cin >> x;
        x = (x + ans - 1) % n + 1;
        update(x, x, 1, 1, n, -1);
        cout << ans << endl;
    }
    return;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie();
    // int t;
    // for (cin >> t; t--; )
        Solve();
    return 0;
}



//TLE and Wa try
#include <bits/stdc++.h>
const int N = 1e5 + 10;//
using LL = long long;
using namespace std;
int n, m, q;
int a[N], tree[N << 2];
map<pair<int, int>, bool> ma;
void push_up(int p)
{tree[p] = tree[p << 1] + tree[p << 1|1];}
void update(int L, int R, int p, int pl, int pr)
{
    if (L <= pl && R >= pr)
    {tree[p] = 1; return;}
    int mid = pl + pr >> 1;
    if (L <= mid) update(L, R, p << 1, pl, mid);
    if (R > mid) update(L, R, p << 1|1, mid + 1, pr);
    push_up(p);
}
int query(int L, int R, int p, int pl,int pr)
{
    if (L <= pl && R >= pr) {return tree[p];}
    int mid = pl + pr >> 1, res = 0;
    if (L <= mid) res += query(L, R, p << 1, pl, mid);
    if (R > mid) res += query(L, R, p << 1|1, mid + 1, pr);
    return res;
}
void Solve()
{
    cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> a[i];
    for (int i = 1; i <= m; i++)
    {
        pair<int, int> p; cin >> p.first >> p.second;
        ma[p] = true;
    }
    cin >> q;
    int ret = 0;
    while (q--)
    {   
        int x; cin >> x;
        x = (x + ret - 1) % n + 1;
        a[x]--;
        if (a[x] == 0) update(x, x, 1, 1, n);
        for (auto i : ma)
        {
            if (i.second)
            {
                int tmp = query(i.first.first, i.first.second, 1, 1, n);
                if (tmp == i.first.second - i.first.first + 1) ma[i.first] = false, ret++;
            }
        }
        cout << ret << endl;
    }
    return;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie();
    // int t;
    // for (cin >> t; t--; )
        Solve();
    return 0;
}
```



## 动态规划

#### DP概念和编码方法

```
dp特征：重叠子问题，最优子结构

两种编程方法：
1.自顶向下与记忆化
2.自底向上与制表递推

空间优化技术：滚动数组
能减少一维复杂度，但是它覆盖了中间状态只留下了最后的状态，所以损失了很多信息
1.交替滚动
2.自我滚动
```

#### 经典线性DP问题


hdu 2602 Bone collector

```c++
//递推代码，自底向上
#include <algorithm>
#include <iostream>
#include <cstring>
using namespace std;
const int maxn = 1010;
int w[maxn], c[maxn];
int dp[maxn][maxn];
int solve(int n, int C)
{
    for (int i = 1; i <= n; i++)
        for (int j = 0; j <= C; j++)
        {
            if (c[i] > j) dp[i][j] = dp[i - 1][j];
            else dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - c[i]] + w[i]);
        }
    return dp[n][C];
}
int main()
{
    int t;
    for (cin >> t; t--; )
    {
        int n, C;
        cin >> n >> C;
        for (int i = 1; i <= n; i++) cin >> w[i];
        for (int i = 1; i <= n; i++) cin >> c[i];
        memset(dp, 0, sizeof dp);
        cout << solve(n, C) << endl;
    }
    return 0;
}

//记忆化代码，自顶向下
int solve(int i, int j)
{
    if (dp[i][j] != 0) return dp[i][j];
    if (i == 0) return 0;
    int res;
    if (c[i] > j) res = solve(i - 1, j);
    else res = max(solve(i - 1, j), solve(i - 1, j - c[i]) + w[i]);
    return dp[i][j] = res;
}
int main()
{
    int t;
    for (cin >> t; t--; )
    {
        int n, C;
        cin >> n >> C;
        for (int i = 1; i <= n; i++) cin >> w[i];
        for (int i = 1; i <= n; i++) cin >> c[i];
        memset(dp, 0, sizeof dp);
        cout << solve(n, C) << endl;
    }
    return 0;
}

//使用交替滚动优化
int dp[2][maxn];   //替换int dp[][]
int solve(int n, int C)
{
    int now = 0, old = 1;  //now指向当前正在计算的一行，old指向旧的一行
    for (int i = 1; i <= n; i++)
    {
        swap(old, now);   //交替滚动，now始终指向最新的一行
        for (int j = 0; j <= C; j++)
        {
            if (c[i] > j) dp[now][j] = dp[old][i];
            else dp[now][i] = max(dp[old][j], dp[old][i - c[i]] + w[i]);
        }
    }
    return dp[now][C];   //返回最新行
}

//使用自我滚动优化
int dp[maxn];
int sovle(itn n, int C)
{
    for (int i = 1; i <= n; i++)
        for (int j = C; j >= c[i]; j--)   //必须反过来循环，即从后向前覆盖
            dp[j] = max(dp[j], dp[j - c[i]] + w[i]);
    return dp[C];
}
```

hdu 1712 ACboy needs your help

分组背包问题

```c++
#include <algorithm>
#include <iostream>
#include <cstring>
using namespace std;
const int maxn = 105;
int n, m;
int a[maxn][maxn];
int dp[maxn];
int main()
{
    while (cin >> n >> m && n && m)
    {
        memset(dp, 0, sizeof dp);
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= m; j++)
                cin >> a[i][j];
        for (int i = 1; i <= n; i++)
            for (int j = m; j > 0; j--)
                for (int k = 1; k <= j; k++)
                    dp[j] = max(dp[j], dp[j - k] + a[i][k]);
        cout << dp[m] << endl;
    }
    return 0;
}
```

luogu P1776 宝物筛选

多重背包问题，可使用简单方法，或者二进制拆分优化，或者单调队列优化

```c++
//简单方法（超时）
#include <algorithm>
#include <iostream>
using namespace std;
const int maxn = 1e5 + 10;
int w[maxn], c[maxn], m[maxn];
int dp[maxn];
int n, C;
int main()
{
    cin >> n >> C;
    for (int i = 1; i <= n; i++) cin >> w[i] >> c[i] >> m[i];
    for (int i = 1; i <= n; i++)
        for (int j = C; j >= c[i]; j--)
            for (int k = 1; k <= m[i] && k * c[i] <= j; k++)
                dp[j] = max(dp[j], dp[j - k * c[i]] + k * w[i]);
    cout << dp[C] << endl;
    return 0;
}

//二进制拆分优化（常用）
#include <algorithm>
#include <iostream>
using namespace std;
const int maxn = 1e5 + 10;
int w[maxn], c[maxn], m[maxn];
int new_w[maxn], new_c[maxn];  //二进制拆分后的新物品
int dp[maxn];
int n, C；
int new_n;   //二进制拆分后的新物品总数量
int main()
{
    cin >> n >> C;
    for (int i = 1; i <= n; i++) cin >> w[i] >> c[i] >> m[i];
    //二进制拆分
    int new_n = 0;
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m[i]; j <<= 1)  //二进制枚举：1，2，4...
        {
            m[i] -= j;		//减去已拆分的
            new_c[++new_n] = j * c[i];   //新物品
            new_w[new_n] = j * w[i];     //新物品对应价值
        } 
        if (m[i])   //储存余数
        {
            new_c[++new_n] = m[i] * c[i];
            new_w[new_n] = m[i] * w[i];
        }
    }
	//滚动数组版本0/1背包
    for (int i = 1; i <= new_n; i++)     //同样枚举即可
        for (int j = C; j >= new_c[i]; j--)
            dp[j] = max(dp[j], dp[j - new_c[i]] + new_w[i]);
    cout << dp[C] << endl;
    return 0;
}

//单调队列优化

```

hdu 1159  Common Subsequence

```c++
#include <algorithm>
#include <iostream>
using namespace std;
const int maxn = 1e3 + 10;
string x, y;
int dp[maxn][maxn];
int main()
{
    while (cin >> x >> y)
    {
        memset(dp, 0, sizeof dp);
        for (int i = 1; i <= x.size(); i++)
            for (int j = 1; j <= y.size(); j++)
            {
                if (x[i - 1] == y[j - 1]) dp[i][j] = dp[i - 1][j - 1] + 1;
                else dp[i][j] = max(dp[i][j - 1], dp[i - 1][j]);
            }
        cout << dp[x.size()][y.size()] << endl;
    }
    return 0;
}
```

Longest Ordered Subsequence

luogu p1020 最少拦截系统      [偏序集，哈斯图与Dilworth定理 - Tofu 的博客 - 洛谷博客 (luogu.org)](https://tofu.blog.luogu.org/pian-xu-ji-ha-si-tu-yu-dilworth-ding-li)

```c++
#include <algorithm>
#include <iostream>
using namespace std;
const int maxn = 3e4 + 10;
int dp[maxn];
int n, a[maxn], ans;
int main()
{
    while (cin >> n)
    {
        ans = 0;
        for (int i = 1; i <= n; i++) dp[i] = 1, cin >> a[i];
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= i; j++)
            {
                if (a[i] > a[j]) dp[i] = max(dp[i], dp[j] + 1);
                ans = max(ans, dp[i]);
            }
        cout << ans << endl;
    }
        return 0;
}
```

luogu P2758 编辑距离

```c++
#include <algorithm>
#include <iostream>
using namespace std;
const int maxn = 2e3 + 10;
int dp[maxn][maxn];
string x, y;
int n, a[maxn], ans;
int main()
{
    cin >> x >> y;
    for (int i = 1; i <= x.size(); i++) dp[i][0] = i;
    for (int i = 1; i <= y.size(); i++) dp[0][i] = i;
    for (int i = 1; i <= x.size(); i++)
        for (int j = 1; j <= y.size(); j++)
        {
            if (x[i - 1] == y[j - 1]) dp[i][j] = dp[i - 1][j - 1];
            else dp[i][j] = min(dp[i - 1][j - 1], min(dp[i][j - 1], dp[i - 1][j])) + 1;
        }
    cout << dp[x.size()][y.size()] << endl;
    return 0;
}
```

POJ 1088 滑雪

遍历每一个点，向四周搜索以得到该点能获得的最长递减路径，储存起来，即为该点的最优解，注意dfs过程也是对每个点的最优解进行了记忆化，所以实际上每个点只需遍历一次即可

```c++
//dfs，动态规划，记忆化搜索
#include <algorithm>
#include <iostream>
using namespace std;
const int maxn = 1e2 + 10;
int dp[maxn][maxn];
int step[4][2] = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
int r, c, a[maxn][maxn], ans;
bool check(int i, int j)
{
    if (i > 0 && i <= r && j > 0 && j <= c) return true;
    return false;
}
int dfs(int x, int y)
{
    if (dp[x][y]) return dp[x][y];
    dp[x][y] = 1;
    for (int i = 0; i < 4; i++)
    {
        int nx = x + step[i][0];
        int ny = y + step[i][1];
        if (check(nx, ny) && a[nx][ny] < a[x][y])
            dp[x][y] = max(dp[x][y], dfs(nx, ny) + 1);
    }
    return dp[x][y];
}
int main()
{
    cin >> r >> c;
    for (int i = 1; i <= r; i++)
        for (int j = 1; j <= c; j++)
            cin >> a[i][j];
    for (int i = 1; i <= r; i++)
        for (int j = 1; j <= c; j++)
            ans = max(ans, dfs(i, j));
    cout << ans << endl;
    return 0;
}
```

luogu P1868 饥饿的奶牛

按照右区间大小先排序，遍历每个区间，每个子问题就是遍历到的区间的选择，可以不选，若是选择应该先从前面二分寻找最合适的一个区间并在其后面加上该区间，从而就可以得到动态规划的状态转移方程，得到的结果也是该区间即子问题的最优解，此题需要注意有个二分搜索减少时间复杂度，使用二分的时候注意左端点不能设为1，必须为0，因为有可能是0，而且不必担心只对结束时间排序会不会有什么其他问题，因为我们用的是尽量右找的，而最右端其实已经是其所有情况的最优解

```c++
#include <algorithm>
#include <iostream>
using namespace std;
const int maxn = 2e5 + 10;
struct node
{
    int b, e;
    int dis;
}a[maxn];
int n;
int dp[maxn];
bool cmp(node x, node y)
{
    return x.e < y.e;
}
int my_binary(int l, int r, int k)
{
	while(l < r) 
    {
		int mid = l + r + 1 >> 1;
		if(a[mid].e < k) l = mid;
		else r = mid - 1;
	}
	return l;
}
int main()
{
    cin >> n;
    for (int i = 1; i <= n; i++)
    {
        cin >> a[i].b >> a[i].e;
        a[i].dis = a[i].e - a[i].b + 1;
    }
    sort(a + 1, a + 1 + n, cmp);
    for (int i = 1; i <= n; i++)
        dp[i] = max(dp[i - 1], dp[my_binary(0, i - 1, a[i].b)] + a[i].dis);  //起始为0
    cout << dp[n] << endl;
    return 0;
}
```

codeforces 189A Cut Ribbon

```c++
#include <algorithm>
#include <iostream>
using namespace std;
int n, p, q, r;
int dp[4010];
int a[4];
int main()
{
    cin >> n >> a[1] >> a[2] >> a[3];
    dp[a[1]] = dp[a[2]] = dp[a[3]] = 1;
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= 3; j++)
            if (i > a[j] && dp[i - a[j]])
                dp[i] = max(dp[i], dp[i - a[j]] + 1);
    cout << dp[n] << endl;
    return 0;
}
```

The Triangle

```c++
#include <algorithm>
#include <iostream>
using namespace std;
int nums[105][105];
int dp[105];
int n, ans;
int main()
{
    cin >> n;
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= i; j++)
            cin >> nums[i][j];
    for (int i = 1; i <= n; i++)
        for (int j = i; j >= 1; j--)
            {
                dp[j] = max(dp[j] + nums[i][j], dp[j - 1] + nums[i][j]);
                ans = max(ans, dp[j]);
            }
    cout << ans << endl;
    return 0;
}
```

luogu P1091 [NOIP2004 提高组] 合唱队形

从左往右记忆最长递增子序列，从右往左记忆最长递增子序列，和最大即为所求

```c++
#include <algorithm>
#include <iostream>
using namespace std;
int a[105];
int dp[2][105];
int n, ans;
int main()
{
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> a[i];
    for (int i = 1; i <= n; i++)
        for (int j = 0; j < i; j++)
            if (a[i] > a[j]) dp[0][i] = max(dp[0][i], dp[0][j] + 1);
    for (int i = n; i >= 1; i--)
        for (int j = n + 1; j > i; j--)
            if (a[i] > a[j]) dp[1][i] = max(dp[1][i], dp[1][j] + 1);
    for (int i = 1; i <= n; i++) ans = max(ans, dp[0][i] + dp[1][i]);
    cout << n - ans + 1 << endl;
    return 0;
}
```

luogu P1616 疯狂的采药

本题的重点是每种草药的数量是无限的，起初我想再加一个`for`循环，但是造成超时了，事实上在自我滚动数组的基础上不要从后面往回维护，改成从前面往后面维护，就可以巧妙地避免重新开一个循环，减少了时间复杂度，因为以前的题从后面开始循环是因为在该循环中每次维护需要互不影响，但是此题的数量无限，所以每次结果可以在上一个结果的基础上进行最优解维护；此题还有一个注意的点就是极端情况下结果会爆`int`所以必须开`long long`

```c++
#include <algorithm>
#include <iostream>
using namespace std;
const int maxn = 1e7 + 10;
long long t, n;
long long c[maxn], w[maxn];
long long dp[maxn];
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    cin >> t >> n;
    for (int i = 1; i <= n; i++) cin >> c[i] >> w[i];
    for (int i = 1; i <= n; i++)
        for (int j = c[i]; j <= t; j++)
                dp[j] = max(dp[j], dp[j - c[i]] + w[i]);
    cout << dp[t];
    return 0;
}
```

luogu P1507 NASA的食物计划

本题出现两个限制条件，最大体积和最大质量，因此dp状态数组也应开到多维，其他思路与常规无异

```c++
#include <algorithm>
#include <iostream>
using namespace std;
const int maxn = 550;
int H, T, n;
int h[maxn], t[maxn], k[maxn];
int dp[maxn][maxn];
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    cin >> H >> T >> n;
    for (int i = 1; i <= n; i++) cin >> h[i] >> t[i] >> k[i];
    for (int i = 1; i <= n; i++)
        for (int j = H; j >= h[i]; j--)
            for (int p = T; p >= t[i]; p--)
                dp[j][p] = max(dp[j][p], dp[j - h[i]][p - t[i]] + k[i]);
    cout << dp[H][T];
    return 0; 
}
```

luogu P1757 通天之分组背包

用`vector`超时，甚至无法编译，用数组模拟

```c++
#include <algorithm>
#include <iostream>
using namespace std;
const int maxn = 1e3 + 10;
int n, m, s, g_num;
int dp[maxn];
int nums[maxn], w[maxn], c[maxn], room[maxn][maxn];
int main()
{
    cin >> m >> n;
    for (int i = 1; i <= n; i++)
    {
        cin >> c[i] >> w[i] >> s; 
        g_num = max(g_num, s);
        room[s][++nums[s]] = i;
    }
    for (int i = 1; i <= g_num; i++)
        for (int j = m; j > 0; j--)
            for (int k = 1; k <= nums[i]; k++)
                if (j >= c[room[i][k]]) dp[j] = max(dp[j], dp[j - c[room[i][k]]] + w[room[i][k]]);
    cout << dp[m];
    return 0;
}
```

luogu P1064 [NOIP2006 提高组] 金明的预算方案

**有依赖性的背包问题**  此题需要多个状态转移方程，对每种可能都设一个状态转移方程即可

```c++
#include <algorithm>
#include <iostream>
using namespace std;
const int maxn = 4e4 + 10;
int n, m, v, p, q;
int dp[maxn];
int main_w[maxn], main_c[maxn];
int sub_w[maxn][3], sub_c[maxn][3];
int main()
{
    cin >> n >> m;
    for (int i = 1; i <= m; i++)                                                   
    {
        cin >> v >> p >> q;
        if (!q)
        {
            main_c[i] = v;
            main_w[i] = v * p;
        }
        else
        {
            sub_c[q][0]++;
            sub_c[q][sub_c[q][0]] = v;
            sub_w[q][sub_c[q][0]] = v * p;
        }                               
    }
    for (int i = 1; i <= m; i++)
        for (int j = n; main_c[i] && j >= main_c[i]; j--)
        {
            dp[j] = max(dp[j], dp[j - main_c[i]] + main_w[i]);
            if (j >= main_c[i] + sub_c[i][1])
                dp[j] = max(dp[j], dp[j - main_c[i] - sub_c[i][1]] + main_w[i] + sub_w[i][1]);
            if (j >= main_c[i] + sub_c[i][2])
                dp[j] = max(dp[j], dp[j - main_c[i] - sub_c[i][2]] + main_w[i] + sub_w[i][2]);
            if (j >= main_c[i] + sub_c[i][1] + sub_c[i][2])
                dp[j] = max(dp[j], dp[j - main_c[i] - sub_c[i][1] - sub_c[i][2]] + main_w[i] + sub_w[i][1] + sub_w[i][2]);
        }
    cout << dp[n];
    return 0;
}
```

HDU 2639 Bone Collector II

**第`k`优解问题**：当我们计算正常求最优解时我们只取我们所需要的解，一般是最优解，这导致我们摒弃了很多不优解，而计算第`k`优解时，就需要把原先摒弃的解按顺序放入一个数组，也就是说在原来求最优解的基础上再加一维数组，代表前`k`优解。而每次遍历时，在先前的基础上，我们要对前`k`的优解的操作结果都储存起来，而且存的是两种操作情况，因为我们还不知道得到的结果的前k种是什么，但是对于两种操作都储存前k种，一定能包括总答案的前`k`种，极端情况下是前`k`种都在`a[maxn]`或`b[maxn]`。存完之后，我们利用存进去`a[maxn]`和`b[maxn]`的都是递减的序列，所以求前k优解相当于合并两个数组然后取前`k`个值，并不需要真正合并，给两个指针进行移动就行

```c++
#include <algorithm>
#include <iostream>
#include <cstring>
using namespace std;
const int maxn = 105;
int t, n, v, k;
int c[maxn], w[maxn];
int dp[1010][35];
int a[maxn], b[maxn];
int main()
{
    for (cin >> t; t--; )
    {
        cin >> n >> v >> k;
        memset(dp, 0, sizeof dp);
        for (int i = 1; i <= n; i++) cin >> w[i];
        for (int i = 1; i <= n; i++) cin >> c[i];
        for (int i = 1; i <= n; i++)
            for (int j = v; j >= c[i]; j--)
            {
                int p;
                for (p = 1; p <= k; p++) //把所有情况都存起来
                {
                    a[p] = dp[j - c[i]][p] + w[i];
                    b[p] = dp[j][p];
                }
                a[p] = -1; b[p] = -1;
                int x = 1, y = 1, z = 1;
                while (z <= k && (a[x] != -1 || b[y] != -1)) //所有解由最优到不优排列
                {
                    if (a[x] > b[y]) dp[j][z] = a[x++];
                    else dp[j][z] = b[y++];
                    if (dp[j][z] != dp[j][z - 1]) z++; //注意去掉重复解
                }
            }
        cout << dp[v][k] << endl;
    }
    return 0;
}
```

 luogu P1853 投资的最大效益

```c++
#include <algorithm>
#include <iostream>
#include <cstring>
using namespace std;
const int maxn = 5e6 + 10;
int s, n, d;
int c[15], w[15];
int dp[maxn];
int main()
{
    cin >> s >> n >> d;
    for (int i = 1; i <= d; i++) cin >> c[i] >> w[i];
    for (int i = 1; i <= n; i++)
    {
        memset(dp, 0, sizeof dp);
        for (int j = 1; j <= d; j++)
            for (int k = c[j]; k <= s; k++)
                dp[k] = max(dp[k], dp[k - c[j]] + w[j]); 
        s += dp[s];
    }
    cout << s << endl;
    return 0;
}
```

luogu P1833 樱花

读取输入的时间的方式很有意思，值得学习

```c++
#include <algorithm>
#include <iostream>
using namespace std;
const int maxn = 5e5 + 10;
int a1, a2, b1, b2;
int n, new_n;
int c[maxn], w[maxn], m[maxn];
int new_c[maxn], new_w[maxn];
int dp[1010];
int main()
{
    scanf("%d:%d%d:%d%d", &a1, &a2, &b1, &b2, &n);   //直接读取时间
    int t = (b1 * 60 + b2) - (a1 * 60 + a2);
    for (int i = 1; i <= n; i++) cin >> c[i] >> w[i] >> m[i];
    for (int i = 1; i <= n; i++)
    {
        if (!m[i]) m[i] = t / c[i];
        for (int j = 1; j <= m[i]; j++)
        {
            m[i] -= j;
            new_c[++new_n] = j * c[i];
            new_w[new_n] = j * w[i];
        }
        if (m[i])
        {
            new_c[++new_n] = m[i] * c[i];
            new_w[new_n] = m[i] * w[i];
        }
    }
    for (int i = 1; i <= new_n; i++)
        for (int j = t; j >= new_c[i]; j--)
            dp[j] = max(dp[j], dp[j - new_c[i]] + new_w[i]);
    cout << dp[t];
    return 0;
}
```

luogu P1164 小A点菜

dp**解决有k个解的问题**, `dp[maxn]`储存的是方案数, 不需要状态转移方程, 只需将每种情况下的方案数储存起来即可, 特别注意要使得`dp[0] = 1` 

```c++
#include <algorithm>
#include <iostream>
using namespace std;
int n, m;
int a[105];
int dp[10010];
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    cin >> n >> m;
    dp[0] = 1;
    for (int i = 1; i <= n; i++) cin >> a[i];
    for (int i = 1; i <= n; i++)
        for (int j = m; j >= a[i]; j--)
            dp[j] += dp[j - a[i]];
    cout << dp[m];
    return 0;
}
```

 [HDU-1024 Max Sum Plus Plus](https://vjudge.csgrandeur.cn/problem/HDU-1024)

本题难点在于如何思考子问题，即构造最优子结构。首先题目说一共`n`个人，要截取m组，那自然要想到设为行代表组数，列代表人数，即`dp[m][n]`, 然后就是如何列状态方程呢? 按照以往的惯例应该是分为`a[j]`这个数要不要选, 在最优情况下进行选择, 当时此题却是设一个`a[j]`必须选, 有两种选择方式的状态转移方程, 即`dp[i][j] = min(dp[i][j - 1], dp[i - 1][k]) + a[j], i <= k <= i - 1`, 后面的`a[j]`是必须加的, 而第一种情况是这个数直接加入最后的那个区间, 总组数`i`不变, 第二种情况是这个数自成为一个组, 那就要从` d[i - 1]` 中取一个最大的数,  在此题中`dp[]`的每一个值并不是代表`(dp[i][1], dp[i][j]) `的最大值, 而是你必须选那个数而能得到的最大值, 事实上可以不选, 数组如此设计是为后面可能出现的更大值保留连续性, 所以我们第二种情况需要找上一行的最小值; 又考虑到此题`n`的范围达到$10^6$级别, 所以m也不确定, 所以不能简单二维数组, 考虑滚动, 而且另外开一个数组储存前`j - 1`个数的最大值, dp数组直接自我滚动即可, 特别注意, 状态方程需要利用同一行中之前计算的数据, 所以自我滚动时从前往后遍历,同时注意 `pre[]`的更新时机, 必须状态转移后再更新`pre[j - 1]`

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
const int N = 1e6 + 10;
const int INF = 0x3f3f3f3f;
int dp[N], pre[N], a[N];
int n, m;
int main()
{
    while (cin >> m >> n)
    {
        for (int i = 1; i <= n; i++) cin >> a[i];
        int tmp;
        memset(dp, 0, sizeof dp);
        memset(pre, 0, sizeof pre);
        for (int i = 1; i <= m; i++)
        {
            tmp = -INF;
            for (int j = i; j <= n; j++)
            {
                dp[j] = max(dp[j - 1], pre[j - 1]) + a[j];
                pre[j - 1] = tmp;
                tmp = max(tmp, dp[j]);
            }
        }
        cout << tmp << endl;
    }
    return 0;
}
```

HDU 1069 Monkey and Banana

关键是先对其排序，三个维度就储存三个不同基底的矩阵即可，用一维`dp[]`不断更新即可	

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
int n, cnt, tmp[3], tot;
int dp[105];
struct tec {int x, y, z;}t[105];
bool cmp(tec a, tec b)
{
    if (a.x != b.x) return a.x > b.x;
    else return a.y > b.y;
}
int main()
{
    while (cin >> n && n)
    {
        int cnt = 0, ans = 0;
        memset(dp, 0, sizeof dp);
        memset(t, 0, sizeof t);
        for (int i = 0; i < n; i++)
        {
            cin >> tmp[0] >> tmp[1] >> tmp[2];
            sort(tmp, tmp + 3);
            t[++cnt].x = tmp[2]; t[cnt].y = tmp[1]; t[cnt].z = tmp[0];
            t[++cnt].x = tmp[2]; t[cnt].y = tmp[0]; t[cnt].z = tmp[1];
            t[++cnt].x = tmp[1]; t[cnt].y = tmp[0]; t[cnt].z = tmp[2];
        }
        sort(t + 1, t + 1 + cnt, cmp);
        for (int i = 1; i <= cnt; i++)
        {
            dp[i] = t[i].z;
            for (int j = 1; j <= i; j++)
                if (t[j].x > t[i].x && t[j].y > t[i].y) dp[i] = max(dp[i], dp[j] + t[i].z);
            ans = max(ans, dp[i]);
        }
        printf("Case %d: maximum height = %d\n", ++tot, ans);
    }
    return 0;
}
```



```

```

HDU 1087 Super Jumping! Jumping! Jumping!

```c++
#include <iostream>
#include <algorithm>
using namespace std;
int n;
int dp[1020], a[1020];
int main()
{
    while (cin >> n && n)
    {
        int ans = 0;
        for (int i = 1; i <= n; i++) cin >> a[i];
        for (int i = 1; i <= n; i++)
        {
            dp[i] = a[i];
            for (int j = 1; j < i; j++)
                if (a[i] > a[j]) dp[i] = max(dp[i], dp[j] + a[i]);
            ans = max(ans, dp[i]);
        }
        cout << ans << endl;
    }
    return 0;
}
```

HDU 1114 Piggy-Bank

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
int t, e, f, n;
struct str{int v, w;}a[510];
int dp[10010];
int main()
{
    for (cin >> t; t--; )
    {
        memset(dp, 0x3f, sizeof dp);
        cin >> e >> f >> n;
        for (int i = 1; i <= n; i++) cin >> a[i].v >> a[i].w;
        dp[0] = 0;
        for (int i = 1; i <= n; i++)
            for (int j = a[i].w; j <= f - e; j++)
                dp[j] = min(dp[j], dp[j - a[i].w] + a[i].v);
        if (dp[f- e] == 0x3f3f3f3f) printf("This is impossible.\n");
        else printf("The minimum amount of money in the piggy-bank is %d.\n", dp[f - e]);
    }
    return 0;
}
```

HDU 1176 免费馅饼

此题实际上是数塔类型的dp, 把`t`秒落在`x`点上的馅饼数记录作为数塔值, 然后求总和最大的路径即可, 但是在这里巧妙使用逆推的思路最后输出`dp[0][5]`也是可行的, 注意防止数组越界

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
int n, maxn;
int dp[100010][12];
int main()
{
    while (cin >> n && n)
    {
        memset(dp, 0, sizeof dp); maxn = 0;
        for (int i = 1; i <= n; i++)
        {
            int a, b; cin >> a >> b;
            dp[b][a]++;
            maxn = max(maxn, b);
        }
        for (int i = maxn - 1; i >= 0; i--)
        {
            dp[i][0] += max(dp[i + 1][0], dp[i + 1][1]);
            for (int j = 1; j < 11; j++)
                dp[i][j] += max(dp[i + 1][j], max(dp[i + 1][j - 1], dp[i + 1][j + 1]));
        }
        cout << dp[0][5] << endl;
    }
    return 0;
}
```

HDU 1260 Tickets

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
int n, t, dp[2010];
int a[2010], b[2010];
int main()
{
    for (cin >> t; t--; )
    {
        memset(dp, 0, sizeof dp);
        cin >> n;
        for (int i = 1; i <= n; i++) cin >> a[i];
        for (int i = 2; i <= n; i++) cin >> b[i];
        dp[1] = a[1];
        for (int i = 2; i <= n; i++)
            dp[i] = min(dp[i - 1] + a[i], dp[i - 2] + b[i]);
        int ans = dp[n];
        int x = ans / 60, y = x / 60;
        printf("%.2d:%.2d:%.2d", 8 + y, x % 60, ans % 60);
        printf(y >= 4 ? " pm\n" : " am\n"); 
    }
    return 0;
}
```

HDU 1160 FatMouse's Speed

此题的重点在于题目中"take the data on a **collection** of mice", **collection**是集合的意思, 集合是无序的, 所以可以对老鼠先进行排序再求子序列 

```c++
#include <iostream>
#include <algorithm>
using namespace std;
const int N = 2e5 + 10;
struct str{int w, s, num;}mou[1010];
int cnt, ans, ed;
int dp[1010], pre[1010];
bool cmp(str a, str b)
{
    if (a.w != b.w) return a.w < b.w;
    else return a.s > b.s;
}
void print(int x)
{
    if (pre[x] != 0) print(pre[x]);
    printf("%d\n", mou[x].num);
}
int main()
{
    while (cin >> mou[++cnt].w >> mou[cnt].s) mou[cnt].num = cnt;
    sort(mou, mou + cnt, cmp);
    for (int i = 1; i <= cnt; i++) dp[i] = 1;
    for (int i = 1; i <= cnt; i++)
        for (int j = 1; j < i; j++)
            if (mou[i].s < mou[j].s && mou[i].w > mou[j].w)
                if (dp[i] < dp[j] + 1) dp[i] = dp[j] + 1, pre[i] = j;
    for (int i = 1; i <= cnt; i++) if (ans < dp[i]) ans = dp[i], ed = i;
    cout << ans << endl;
    print(ed);
    return 0;
}
```

[Jury Compromise - POJ 1015 ](https://vjudge.csgrandeur.cn/problem/POJ-1015#author=0)

此题用`dp[25][805]`来储存序列和, 第一个维度代表的是序列的人的个数, 第二个维度代表的是序列差的和, 因为有可能出现负数, 所以在这里使用修正值`fix = m * 20`, 然后再使用`vector<int> path[25][805]`来储存路径, 每个维度的意义与`dp[][]`相同, 循环部分按照"选哪个人" -> "选的第几人" -> "差值之和"遍历. 若是"选的第几人" -> "选哪个人"的顺序, 则为了避免选重复的人需要判断, 但是储存路径的方式会覆盖掉一些情况, 所以是错误的. 

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
int n, m, cas = 1, fix, p, d, S, A, P, D;
int dp[25][805], sub[205], add[205];
vector<int> path[25][805];
int main()
{
    while (cin >> n >> m && n)
    {
        memset(dp, -1, sizeof dp);
        for (int i = 1; i <= m; i++)
            for (int j = 0; j < 805; j++)
                path[i][j].clear();
        fix = 20 * m;     //修正值
        dp[0][fix] = 0;   //起点
        for (int i = 1; i <= n; i++)
        {
            cin >> p >> d;
            sub[i] = p - d; add[i] = p + d;
        }
        for (int i = 1; i <= n; i++)
            for (int j = m - 1; j >= 0; j--)   //倒序
                for (int k = 0; k <= 2 * fix; k++)
                    if (dp[j][k] >= 0 && dp[j][k] + add[i] > dp[j + 1][k + sub[i]])
                        {
                        dp[j + 1][k + sub[i]] = dp[j][k] + add[i];
                        path[j + 1][k + sub[i]] = path[j][k];
                        path[j + 1][k + sub[i]].push_back(i);
                        }
        int i;
        for (i = 0; i <= fix; i++)
            if (dp[m][fix + i] >= 0 || dp[m][fix - i] >= 0) break;
        S = dp[m][fix + i] > dp[m][fix - i] ? fix + i : fix - i;
        A = dp[m][S];
        P = (A + (S - fix)) / 2; D = (A - (S - fix)) / 2;
        printf("Jury #%d\n",cas++);
        printf("Best jury has value %d for prosecution and value %d for defence:\n",P,D);
        for (int i = 0; i < m; i++) cout << " " << path[m][S][i]; cout << endl << endl;
    }
    return 0;
}
```

POJ 1661 Help Jimmy

该题本质是dp的记忆化搜索, 从上而下递归编码, 可以使得本题的思路十分清晰, 将每次的跳跃分为两个雷同的子问题, 即跳到左端点和跳到右端点, 将跳到左端点的时间加上该左端点到底层的最短时间, 跳到右端点的时间加上该右端点到底层的最短时间, 比较取最小值, 这就是每一个子问题的过程, 对于无法跳跃的, 赋予无穷大数即可. 此题还有另一种思路, 就是从底层往上跳, 巧妙地将`dp[i][0]`当作左端点到底部的最短时间, `dp[i][1]`当作右端点到底部的最短时间, 然后正常`dp`加判断可行性即可

```c++
//自顶向下
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
const int INF = 0x3f3f3f3f;
int t, n, x, y, maxn;
int ltime[1010], rtime[1010];   //分别记录左右点到底层的最短时间
struct str
{
    int lx, rx, high;
    bool operator < (const str &a) const 
    {return a.high < high;}     //对平台的高度排序
}edge[1010];
int dfs(int L, bool Isleft)     //分成两个子问题,从左点到右点, Isleft用于区分左右点
{
    int y = edge[L].high, x;
    if (Isleft) x = edge[L].lx;
    else x = edge[L].rx;
    int i;
    for (i = L + 1; i <= n; i++)  //找出下方有无平台可跳跃
        if (edge[i].lx <= x && edge[i].rx >= x) break;
    if (i <= n)   //若有还要判断是否安全
    {
        if (y - edge[i].high > maxn) return INF;
    }
    else       //若没有则判断是否可以直接跳到底层
    {
        if (y > maxn) return INF;
        else return y;
    }
    int nltime = y - edge[i].high + x - edge[i].lx;   //到下一个平台左端点所需的时间
    int nrtime = y - edge[i].high + edge[i].rx - x;   //到下一个平台右端点所需的时间
    if (!ltime[i]) ltime[i] = dfs(i, true);          //记忆化搜索
    if (!rtime[i]) rtime[i] = dfs(i, false);
    nltime += ltime[i];       //加上到达的端点到底层的最短时间
    nrtime += rtime[i];
    if (nltime < nrtime) return nltime;  //判断最优
    else return nrtime;
}
int main()
{
    for (cin >> t; t--; )
    {
        memset(ltime, 0, sizeof ltime);
        memset(rtime, 0, sizeof rtime);
        cin >> n >> x >> y >> maxn;
        edge[0].lx = edge[0].rx = x; edge[0].high = y;
        for (int i = 1; i <= n; i++)
            cin >> edge[i].lx >> edge[i].rx >> edge[i].high;
        sort(edge, edge + 1 + n);
        cout << dfs(0, true) << endl;
    }
    return 0;
}


//自底向上
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
const int INF = 0x3f3f3f3f;
int dp[1010][2];
int t, n, x, y, maxn;
struct edge
{
    int lx, rx, h;
    bool operator < (const edge &a) const
    {return h < a.h;}
}e[1010];
int main()
{
    for (cin >> t; t--; )
    {
        memset(dp, 0x3f, sizeof dp);  //去最小值, 初始值应设为无穷大
        dp[0][0] = dp[0][1] = 0;   //底部时间默认为0, 也方便后续操作
        cin >> n >> x >> y >> maxn;
        e[0].lx = -INF; e[0].rx = INF; e[0].h = 0;
        for (int i = 1; i <= n; i++)
            cin >> e[i].lx >> e[i].rx >> e[i].h;
        e[n + 1].lx = e[n + 1].rx = x; e[n + 1].h = y;    //注意加上底部与顶部"平台"
        sort(e, e + n + 2);
        for (int i = 1; i <= n + 1; i++)
            for (int j = 0; j < 2; j++)
                for (int k = i - 1; k >= 0; k--)    //注意此处必须从大到小, 否则会出现穿模的情况
                {
                    int flag = e[i].h - e[k].h - maxn;
                    if (k == 0 && flag <= 0)
                        dp[i][j] = e[i].h - e[k].h;
                    else if (j == 0)
                    {
                        if (flag <= 0 && e[k].lx <= e[i].lx && e[k].rx >= e[i].lx)
                            {
                                int ret = min(e[i].h - e[k].h + e[i].lx - e[k].lx + dp[k][0], e[i].h - e[k].h + e[k].rx - e[i].lx + dp[k][1]);
                                dp[i][j] = min(dp[i][j], ret);
                                break;
                            }
                    }
                    else if (j == 1)
                    {
                        if (flag <= 0 && e[k].rx >= e[i].rx && e[k].lx <= e[i].rx)
                            {
                                int ret = min(e[i].h - e[k].h + e[i].rx - e[k].lx + dp[k][0], e[i].h - e[k].h + e[k].rx - e[i].rx + dp[k][1]);
                                dp[i][j] = min(dp[i][j], ret);
                                break;
                            }
                    }
        }
        cout << dp[n + 1][0] << endl;
    }
    return 0;
}
```

[FatMouse and Cheese - HDU 1078 ](https://vjudge.csgrandeur.cn/problem/HDU-1078#author=0)

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
int n, k;
int a[105][105];
int dp[105][105];
int step[4][2] = {1, 0, 0, 1, -1, 0, 0, -1};
int dfs(int x, int y)
{
    if (dp[x][y]) return dp[x][y];
    dp[x][y] = a[x][y];
    for (int i = 1; i <= k; i++)
        for (int j = 0; j < 4; j++)
        {
            int nx = x + i * step[j][0];
            int ny = y + i * step[j][1];
            if (nx >= 0 && nx <= n && ny >= 0 && ny <= n && a[nx][ny] > a[x][y])
                dp[x][y] = max(dp[x][y], a[x][y] + dfs(nx, ny));
        }
    return dp[x][y];
}
int main()
{
    while (cin >> n >> k)
    {
        memset(dp, 0, sizeof dp);
        if(n == -1 && k == -1) break;
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= n; j++)
                cin >> a[i][j];
        cout << dfs(1, 1) << endl;
    }
    return 0;
}
```

[Phalanx - HDU 2859](https://vjudge.csgrandeur.cn/problem/HDU-2859#author=0)

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
int n;
char s[1010][1010];
int dp[1010][1010]; 
int main()
{
    while (cin >> n && n)
    {
        int ans = 0;
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= n; j++)
                dp[i][j] = 1, cin >> s[i][j];
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= n; j++)
            {
                int tmp = dp[i - 1][j + 1], tx = i, ty = j;
                while (tmp)
                {
                    tx--; ty++;
                    if (s[tx][j] != s[i][ty]) break;
                    tmp--;
                }
                dp[i][j] += dp[i - 1][j + 1] - tmp;
                ans = max(ans, dp[i][j]);
            }
        cout << ans << endl;
    }
    return 0;
}
```

[Milking Time - POJ 3616](https://vjudge.csgrandeur.cn/problem/POJ-3616)

```c++
#include <iostream>
#include <algorithm>
using namespace std;
const int N = 1e6 + 10, M = 1010;
int n, m, r, ans;
int dp[N];
struct str
{
    int s, e, w;
    bool operator < (const str &a) const
    {
        if (e != a.e) return e < a.e;
        else return s < a.s; 
    }
}a[M];
int main()
{
    cin >> n >> m >> r;
    for (int i = 1; i <= m; i++)
    {
        cin >> a[i].s >> a[i].e >> a[i].w;
        a[i].e += r;
    }
    sort(a + 1, a + 1 + m);
    for (int i = 1; i <= m; i++) dp[i] = a[i].w;
    for (int i = 1; i <= m; i++)
        for (int j = 1; j <= i; j++)
            {
                if (a[j].e <= a[i].s) dp[i] = max(dp[i], dp[j] + a[i].w);
                ans = max(ans, dp[i]);
            }
    cout << ans;
    return 0;
}
```

[Making the Grade - POJ 3666](https://vjudge.csgrandeur.cn/problem/POJ-3666#author=0258)

本题需要使用离散化+dp的思想, `dp[i][j]`代表的是前`a[i]`个数按照前`b[j]`的有序集合的子集的顺序(必须包括`b[j]`)需要付出的代价, 需要注意的是此处用`minn`维护前`dp[i - 1][j]`的最小值, 可以减少一层循环, 减少时间复杂度, 状态转移方程为`dp[i][j] = minn + abs(a[i] - b[j])`

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <cmath>
using namespace std;
const int INF = 0x3f3f3f3f;
const int N = 2010;
int n, m;
int a[N], b[N];
int dp[N][N];
int nondown()  //变为不降序列
{
    memset(dp, 0, sizeof dp);
    sort(b + 1, b + 1 + n);  //b数组排序
    m = unique(b + 1, b + 1 + n) - (b + 1);   //去重函数
    for (int i = 1; i <= n; i++)   //前i个数以b[j]结尾的最小花费
    {
        int minn = INF;  //Min优化:f[i-1][k](1<=k<=j)中的最小值
        for (int j = 1; j <= m; j++)
        {
            minn = min(minn, dp[i - 1][j]);  //更新最小值
            dp[i][j] = minn + abs(a[i] - b[j]);  //状态转移
        }
    }
    int ans = INF;
    for (int i = 1; i <= m; i++)
        ans = min(ans, dp[n][i]);
    return ans;
}
bool cmp(int x, int y) {return x > y;}
int nonup()
{
    memset(dp, 0, sizeof dp);
    sort(b + 1, b + 1 + m, cmp);    
    for (int i = 1; i <= n; i++)   
    {
        int minn = INF;
        for (int j = 1; j <= m; j++)
        {
            minn = min(minn, dp[i - 1][j]);
            dp[i][j] = minn + abs(a[i] - b[j]);
        }
    }
    int ans = INF;
    for (int i = 1; i <= m; i++)
        ans = min(ans, dp[n][i]);
    return ans;
}
int main()
{
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> a[i], b[i] = a[i];
    cout << min(nondown(), nonup()) << endl;
    return 0;
}
```

[724 · 最小划分 - LintCode](https://www.lintcode.com/problem/724/)

转化为背包容量为`sum/2`, 把数组中每个数字看作物品的体积, 求出背包最多可以放`res`体积的物体, 返回结果`|res - (sum - res)|`

```c++
class Solution {
public:
    int findMin(vector<int> &nums)
    {
        int sum = 0, n = nums.size();
        int dp[100010] = {0};
        for (auto i: nums) sum += i;
        int lim = sum / 2;
        for (int i = 0; i < n; i++)
        for (int j = lim; j >= nums[i]; j--)
            dp[j] = max(dp[j], dp[j - nums[i]] + nums[i]);
        return abs(dp[lim] - (sum - dp[lim]));
    }
};
```

**子集和问题**(Subset Sum Problem)

```c++
//简单判断
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
const int N = 1e5 + 10;
vector<int> a;
int dp[N];
void Solve()
{
    int n, m, x;
    cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> x, a.push_back(x);
    for (int i = 0; i < n; i++) 
        for (int j = m; j >= 0; j--)
        {
            if (a[i] > j) break;
            else if (a[i] == j) dp[j] = 1;
            else dp[j] = dp[j] ? dp[j] : dp[j - a[i]];
        }
    cout << dp[m] << endl;
}
int main()
{
    Solve();
    return 0;
}

//vector存储路径打印子集, 若是有多个答案
#include <iostream>
#include <algorithm>
using namespace std;
const int N = 1e3 + 10;
vector<int> a;
vector<int> sub[N];   //存路径
int dp[N];
void Solve()
{
    int n, m, x;
    cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> x, a.push_back(x);
    for (int i = 0; i < n; i++) 
        for (int j = m; j >= 0; j--)
        {
            if (a[i] > j) break;
            else if (a[i] == j) dp[j] = 1, sub[j].push_back(j);
            else
            {
                if (dp[j] == 1) continue;
                else if (dp[j - a[i]] == 1)
                {
                    dp[j] = 1;
                    sub[j] = sub[j - a[i]];
                    sub[j].push_back(a[i]);
                }
            }
        }
    cout << dp[m] << endl;
    for (auto i: sub[m]) cout << i << " ";
    cout << endl;
}
int main()
{
    Solve();
    return 0;
}


//逆状态转移方程回溯打印子集, 若是有多个答案只会打印从后往前得到的第一个答案, 失败
#include <iostream>
#include <algorithm>
using namespace std;
const int N = 1e3 + 10;
int a[N];
int dp[N][N];
int n, m, x;
void print(int x, int y)
{
    if (!y) return;
    for (int i = x; i >= 1; i--)
        for (int j = y; j >= 0; j--)
        {
            if (a[i] > y) break;
            if (dp[i][j])
            {
                print(i - 1, j - a[i]);
                cout << a[i] << " ";
                return;
            }
        }
}
void Solve()
{
    cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> a[i];
    for (int i = 1; i <= n; i++) 
        for (int j = 0; j <= m; j++)
        {
            if (a[i] > j) dp[i][j] = dp[i - 1][j];
            else if (a[i] == j) dp[i][j] = 1;
            else if (a[i] < j) dp[i][j] = dp[i - 1][j] ? dp[i - 1][j] : dp[i - 1][j - a[i]];
        }
    cout << dp[n][m] << endl;
    print(n, m);
}
int main()
{
    Solve();
    return 0;
}
```

**最优游戏策略**(Optimal Strategy for a Game)

```c++
//状态转移方程
dp[i][j] = max{V[i] + min(dp[i + 2][j], dp[i + 1][j - 1]), V[j] + min(dp[i + 1][j - 1], dp[i][j - 2])}
dp[i][j] = V[i], j = i
dp[i][j] = max(V[i], V[j]), j = i + 1
    
//zxr
#include <bits/stdc++.h>
using namespace std;
const int N = 105, Min = -1e9;
int a[N], n;
int f[N][N];
int dfs(int u, int i, int j)
{
    if (i == j)
    {
        if (u)
            return f[i][j] = a[i];
        else
            return f[i][j] = -a[i];
    }

    if (f[i][j] != Min)
        return f[i][j];

    if (u)
        f[i][j] = max(dfs(u ^ 1, i + 1, j) + a[i], dfs(u ^ 1, i, j - 1) + a[j]);
    else
        f[i][j] = min(dfs(u ^ 1, i + 1, j) - a[i], dfs(u ^ 1, i, j - 1) - a[j]);

    return f[i][j];
}

int main()
{
    scanf("%d", &n);
    int sum = 0;
    for (int i = 1; i <= n; i++)
    {
        scanf("%d", &a[i]);
        sum += a[i];
    }
    for (int j = 0; j <= n; j++)
        for (int k = 0; k <= n; k++)
            f[j][k] = Min;

    dfs(1, 1, n);
    int dif = f[1][n];
    int rex = (sum + dif) / 2;
    printf("%d %d\n", rex, sum - rex);
    return 0;
}
```

**最短公共超序列**(Shortest Common Supersequence)

方法和求最长公共子序列相似

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
int dp[105][105];
char a[105], b[105], c[105];
int al, bl;
int main()
{
    cin >> a + 1 >> b + 1;
    al = strlen(a + 1);
    bl = strlen(b + 1);
    for (int i = 1; i <= max(al, bl); i++)
        dp[0][i] = dp[i][0] = i;
    for (int i = 1; i <= al; i++)
        for (int j = 1; j <= bl; j++)
        {
            if (a[i] == b[j]) dp[i][j] = dp[i - 1][j - 1] + 1;
            else dp[i][j] = min(dp[i][j - 1], dp[i - 1][j]) + 1;
        }
    cout << dp[al][bl] << endl;  //最短超序列长度
    int i = al, j = bl, cnt = 0;    //逆状态方程记录最短超序列
    while (i > 0 && j > 0)  
    {
        if (dp[i][j] == dp[i - 1][j - 1] + 1 && a[i] == b[j])
        {c[cnt] = a[i]; cnt++; i--; j--;}
        else if (dp[i][j] == dp[i - 1][j] + 1 && a[i] != b[j])
        {c[cnt] = a[i]; cnt++; i--;}
        else if (dp[i][j] == dp[i][j - 1] + 1 && a[i] != b[j])
        {c[cnt] = b[j]; cnt++; j--;}
    }
    while (i > 0) {c[cnt] = a[i]; i--; cnt++;}
    while (j > 0) {c[cnt] = b[j]; j--; cnt++;}
    int cl = strlen(c);
    for (int i = cl - 1; i >= 0; i--) cout << c[i];   //逆序输出, 得到最短超序列
    cout << endl;
    return 0;
}
```

**输出方案**

`01`背包问题，但是要求输出 **字典序最小的方案数** ; 一般而言，背包问题是要求一个最优值，如果要求输出这个最优值的方案，可以参照一般动态规划问题输出方案的方法: 记录下每个状态的最优质是由状态转移方程的哪一项推出来的。然后就可以根据这个状态继续往前推导。显然求字典序最小的时候，我们需要优先考虑编号小的物品，但是找方案的时候，又是从 `f[n][m]` 开始回推的，所以我们在求解 `01` 背包的时候，从后往前推，就可以从 `f[1][m]` 开始往前推了，这样的话，就和求字典序最小的顺序一致了。

```c++
//按字典序最小
#include <bits/stdc++.h>
using namespace std;
const int N = 1e3 + 5;
int f[N][N], n, m, w[N], v[N];
int main()
{
    scanf("%d%d", &n, &m);
    for (int i = 1; i <= n; i++)
        scanf("%d%d", &v[i], &w[i]);

    for (int i = n; i >= 1; i--)   //逆序储存
        for (int j = 0; j <= m; j++)
        {
            f[i][j] = f[i + 1][j];
            if (j >= v[i])
                f[i][j] = max(f[i][j], f[i + 1][j - v[i]] + w[i]);
        }

    int j = m;
    for (int i = 1; i <= n; i++)   //正序贪心, 对于出现的第一个物品若可选可不选则一定要选, 因此能按照字典序最小
    {
        if (j - v[i] >= 0 && f[i][j] == f[i + 1][j - v[i]] + w[i])
        {
            printf("%d ", i);
            j -= v[i];
        }
    }
    return 0;
}

//不能按照字典序最小
const int maxn = 1010;
int w[maxn], c[maxn];
int dp[maxn][maxn];
vector<int> path;
int solve(int n, int C)
{
    for (int i = 1; i <= n; i++)
        for (int j = 0; j <= C; j++)
        {
            if (c[i] > j) dp[i][j] = dp[i - 1][j];
            else dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - c[i]] + w[i]);
        }
    int i = n, j = C;
    while (i > 0 && j > 0)
    {
        if (c[i] <= j && dp[i][j] == dp[i - 1][j - c[i]] + w[i])
        {path.push_back(i); j -= c[i]; i--;}
        else i--;
    }
    return dp[n][C];
}
int main()
{
    int t;
    for (cin >> t; t--; )
    {
        int n, C;
        cin >> n >> C;
        for (int i = 1; i <= n; i++) cin >> w[i];
        for (int i = 1; i <= n; i++) cin >> c[i];
        memset(dp, 0, sizeof dp);
        cout << solve(n, C) << endl;
        for (auto i = path.end() - 1; i >= path.begin(); i--) cout << *i << " ";
    }
    return 0;
}
```



#### 状态压缩DP

```
DP技巧之一, 一般应用在集合问题中, 当DP状态是集合时, 把集合的组合或排列用一个二进制数表示, 这个二进制数的0/1组合表示集合的一个子集, 从而把DP状态的处理转换成为二进制的位操作, 使得代码简洁, 提高算法效率, 从二进制简化集合处理的角度看也是一种DP优化方法.
应用背景是以集合为状态, 且集合一般用二进制表示, 用二进制的位运算处理, 所以又可以称为"集合DP"
集合问题一般是指数复杂度的(NP问题), 例如:
1.子集问题, 设n个元素无先后关系, 那么共有2^n个子集;
2.排列问题, 对所有n个元素进行全排列, 共有n!个全排列
可以这样概括状压DP思想: 如果用二进制表示集合的状态(子集或排列), 并用二进制的位运算便利和操作, 又简单又快. 当然, 由于集合问题是NP问题, 所以状压DP的复杂度仍然是指数级的, 只能用于小规模问题的求解, 而且时间复杂度实际上取决于DP算法, 与状态压缩关系不大, 它只是处理集合的工具.
```

```c++
用位运算对集合进行操作
1 << (i - 1) & a         //判断a的第i位(从最低位开始数)是否等于1
a | (1 << (i - 1))       //把a的第i位改为1
a & ( ~ (1 << (i - 1))   //把a的第i位改为0
a & (a - 1)              //把a的最后一个1去掉
```

[91. 最短Hamilton路径 - AcWing题库](https://www.acwing.com/problem/content/description/93/)

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
int n, dp[1 << 20][21];
int dist[21][21];
int main()
{
    memset(dp, 0x3f, sizeof dp);  //初始化最大值
    cin >> n;
    for (int i = 0; i < n; i++)   //输入图
        for (int j = 0; j < n; j++)
            cin >> dist[i][j];    //输入点之间的距离
    dp[1][0] = 0;                 //开始时集合中只有点0, 起点和终点都是0
    for (int S = 1; S < (1 << n); S++) //从小集合扩展到大集合, 集合用S的二进制表示
        for (int j = 0; j < n; j++)   //枚举点j
            if ((S >> j) & 1)      //判断当前集合中是否含有j点
                for (int k = 0; k < n; k++)  //枚举到达j的点k, k属于集合S - j
                    if ((S ^ (1 << j)) >> k & 1)  //判断k是否属于S - j
                        dp[S][j] = min(dp[S][j], dp[S ^ (1 << j)][k] + dist[k][j]);  //状态转移
    cout << dp[(1 << n) - 1][n - 1];   //输出: 路径包含了所有的点, 终点是n - 1
    return 0;
}
```

[2411 -- Mondriaan's Dream (poj.org)](http://poj.org/problem?id=2411)

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
long long dp[2][1 << 11];
int n, m, now, old;
int main()
{
    while (cin >> n >> m && n)
    {
        if (m > n) swap(n, m);    //复杂度为O(nm*2^m), m较小有利
        memset(dp, 0, sizeof dp);
        now = 0, old = 1;   //滚动数组
        dp[now][(1 << m) - 1] = 1;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
            {
                swap(now, old);
                memset(dp[now], 0, sizeof(dp[now]));
                for (int k = 0; k < (1 << m); k++)  //k为轮廓线上的m格
                {
                    if (k & 1 << (m - 1))          //情况1: 要求k(m-1) = 1
                        dp[now][(k << 1) & ( ~ (1 << m))] += dp[old][k];
                    if (i && !(k & 1 << (m - 1)))  //情况2: 要求k(m-1)=0, 而且i不能为第一行
                        dp[now][(k << 1) ^ 1] += dp[old][k];
                    if (j && (!(k & 1)) && (k & 1 << (m - 1)))   //情况3: 要求k0=0, k(m-1)=1, 且j不能为第一列 
                        dp[now][((k << 1) | 3) & ( ~ (1 << m))] += dp[old][k];
                }
            }
        cout << dp[now][(1 << m) - 1] << endl;
    }
    return 0;
}
```

HDU 4539 排兵布阵

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <cmath>
#include <queue>
#include <map>
using namespace std;
int mp[105][12];
int dp[105][200][200];
int n, m;
int sta[200];   //预计算一行的合法情况并储存, m = 10时只有169种合法情况
int init_line(int n)    //预计算出一行的合法情况
{
    int M = 0;
    for (int i = 0; i < n; i++)
        if (i & (i << 2) == 0 && i & (i >> 2) == 0)  //左右间隔2的位置没人就是合法
            sta[M++] = i;
    return M;   //返回合法情况有多少种
}
int count_line(int i, int x)      //计算第i行的士兵数量
{
    int sum = 0;
    for (int j = m - 1; j >= 0; j--)   //x是预计算过的合法安排
        if (x & 1) sum += mp[i][j];    //把x与地形匹配
        x >>= 1;
    return sum;
}
int main()
{
    while (cin >> n >> m)
    {
        int M = init_line(1 << m);   //预计算一行的合法情况, 有M种
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
                cin >> mp[i][j];     //输入地图
        int ans = 0;
        memset(dp, 0, sizeof dp);
        for (int i = 0; i < n; i++)   //第i行
            for (int j = 0; j < M; j++) //枚举第i行的合法安排
                for (int k = 0; k < M; k++)  //枚举第i - 1行的合法安排
                {
                    if (i == 0)   //计算第1行
                    {
                        dp[i][j][k] = count_line(i, sta[i]);
                        ans = max(ans, dp[i][j][k]);
                        continue;
                    }
                    if ((sta[j] & (sta[k] >> 1))||(sta[j] & (sta[k] << 1)))
                        continue;   //第i行和第i - 1行冲突
                    int tmp = 0;
                    for (int p = 0; p < M; p++)      //接着枚举第i - 2行的合法状态
                    {
                        if ((sta[p] & (sta[k] >> 1)) || (sta[p] & (sta[k] << 1)))
                            continue;     //第i - 1行和第i - 2行冲突
                        if (sta[j] & sta[p]) continue;   //第i - 2行和第i行冲突
                        tmp = max(tmp, dp[i - 1][k][p]);  //状态转移, 从第i - 1行递推到第i行
                    }
                    dp[i][j][k] = tmp + count_line(i, sta[j]); //加上第i行的士兵数量
                    ans = max(ans, dp[i][j][k]);
                }
        cout << ans << endl;
    }
    return 0;
}
```

HDU 3001 

**三进制状态压缩DP**, 此题和Hamilton路径问题很相似, 只是此题是需要给定任意起点, 找遍历城市的最小费用, 而Hamilton是从起点到终点, 也就是说已经给定了终点, 所以在dp意义的设计上有略微不同, 此题时间复杂度为$O(nM^3)$ , 对于**除二进制以外的N进制问题**的处理方式需要特别注意

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
const int INF = 0x3f3f3f3f;
int n, m;
int bit[12] = {0, 1, 3, 9, 27, 81, 243, 729, 2187, 6561, 19683, 59049};  //三进制每位的权值
int tri[60000][11];
int dp[11][60000];
int graph[11][11];       //存图
void make_trb()          //初始化, 存所有可能的路径
{
    for (int i = 0; i < 59050; i++)   //共59050种路径状态
    {
        int t = i;
        for (int j = 1; j <= 10; j++)
        {tri[i][j] = t % 3; t /= 3;}
    }
}
int comp_dp()
{
    int ans = INF;
    memset(dp, 0, sizeof dp);
    for (int j = 0; j <= n; j++) dp[j][bit[j]] = 0;    //初始化, 从第j座城市出发, 只访问j, 费用为0
    for (int i = 0; i < bit[n + 1]; i++)         //遍历所有路径, 每个i是一条路径
    {
        int flag = 1;             //所有城市都遍历一次以上
        for (int j = 1; j <= n; j++)   //遍历城市, 以j为起点
        {
            if (tri[i][j] == 0)   //是否有一座城市访问次数为0
            {
                flag = 0;      //还没有经过所有点
                continue;
            }
            for (int k = 1; k <= n; k++)    //遍历路径i - j的所有城市
            {
                int l = i - bit[j];  //从路径i中去掉第j座城市
                dp[j][i] = min(dp[j][i], dp[k][l] + graph[k][j]);
            }
        }
        if (flag)        //找最小费用
            for (int j = 1; j <= n; j++)
                ans = min(ans, dp[j][i]);   //路径i上最小的总费用
    }
    return ans;
}
int main()
{
    make_trb();
    while (cin >> n >> m)
    {
        memset(graph, INF, sizeof graph);
        while (m--)
        {
            int a, b, c; cin >> a >> b >> c;
            if (c < graph[a][b]) graph[a][b] = graph[b][a] = c;
        }
        int ans = comp_dp();
        if (ans == INF) cout << "-1" << endl;
        else cout << ans << endl;
    }
    return 0;
}
```

#### 区间DP

```
区间DP也是线性DP, 它把区间当作DP的阶段, 用区间的两个端点描述状态和处理状态的转移, 主要思想就是现在小区间进行DP得到最优解, 然后在合并小区间的最优解求得大区间的最优解. 解题时先解决小区间问题, 然后合并小区间, 得到更大的区间, 直到解决最后的大区间问题. 合并的操作一般是把左右两个相邻的子区间合并.
区间DP的复杂度大于O(n^2), 一般为O(n^3)
```

石子合并


```c++
//定义dp[i][j]为合并第i堆到第j堆的最小花费
//dp[i][j] = min(dp[i][j], dp[i][k] + dp[k + 1][j] + w[i][j]);
//
for (int i = 1; i <= n; i++) dp[i][i] = 0;   //n为石子堆数, 初始化
for (int j = 2; j <= n; j++)
    for (int i = j - 1; j >= 1; j--)
    {
        dp[i][j] = INF;
        for (int k = i; k < j; k++)
        	dp[i][j] = min(dp[i][j], dp[i][k] + dp[k + i] + w[i][j]);
    }

//

for (int i = 1; i <= n; i++)
for (int len = 2; len <= n; len++)
	for (int i = 1; i <= n - len + 1; i++)
    {
        int j = i + len - 1;
        dp[i][j] = INF;
        for (int k = i; k < j; k++)
            dp[i][j] = min(dp[i][j], dp[i][k] + dp[k + 1][j] + w[i][j]);
	}
```

HDU 2476

```c++
#include <iostream>
#include <algorithm>
const int inf = 0x3f3f3f3f;
using namespace std;
char A[105], B[105];
int dp[105][105];
void Solve()
{
    while (~scanf("%s%s", A + 1, B + 1))
    {
        int n = strlen(A + 1);
        for (int i = 1; i <= n; i++) dp[i][i] = 1;
        for (int len = 2; len <= n; len++)
            for (int i = 1; i <= n - len + 1; i++)
            {
                int j = i + len - 1;
                dp[i][j] = inf;
                if (B[i] = B[j]) dp[i][j] = dp[i - 1][j];
                else
                    for (int k = i; k < j; k++)
                        dp[i][j] = min(dp[i][j], dp[i][k] + dp[k + 1][j]);
            }
        for (int j = 1; j <= n; j++)
        {
            if (A[j] == B[j]) dp[1][j] = dp[1][j - 1];
            else
            {
                for (int k = 1; k < j; k++)
                    dp[1][j] = min(dp[1][j], dp[1][k] + dp[k + 1][j]);
            }
        }
        cout << dp[1][n] << endl;
    }
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie();
        Solve();
    return 0;
}
```





## 数论和线性代数

#### 整除分块（数论分块）

soj [1433 : 除法向下取整求和](https://soj.csgrandeur.cn/csgoj/problemset/problem?pid=1433)

```c++
#include <iostream>
#include <algorithm>
using namespace std;
#define LL long long
LL n, cnt;
int main()
{
    while (cin >> n)
    {
        cnt = 0;
        for (int l = 1, r; l <= n; l = r + 1)
        {
            r = n / (n / l);
            cnt += n / l * (r - l + 1);
        }
        cout << cnt << endl;
    }
    return 0;
}
```

soj [1434 : 两个除法向下取整求和](https://soj.csgrandeur.cn/csgoj/problemset/problem?pid=1434)

```c++
#include <iostream>
#include <algorithm>
using namespace std;
#define LL long long
LL n, m, cnt;
int main()
{
    while (cin >> n >> m)
    {
        cnt = 0;
        for (int l = 1, r; l <= n; l = r + 1)
        {
            r = min(n / (n / l), m / (m / l));
            cnt += (n / l) * (m / l) * (r - l + 1);
        }
        cout << cnt << endl;
    }
    return 0;
}
```

soj [1435 : 等差数列与除法向下取整之积求和](https://soj.csgrandeur.cn/csgoj/problemset/problem?pid=1435)

```c++
#include <iostream>
#include <algorithm>
using namespace std;
#define LL long long
LL n, m, cnt;
int main()
{
    while (cin >> n)
    {
        cnt = 0;
        for (int l = 1, r; l <= n; l = r + 1)
        {
            r = n / (n / l);
            cnt += (n / l) * (l + r) * (r - l + 1) / 2; 
        }
        cout << cnt << endl;
    }
}
```

soj [1436 : 稍显复杂的数论分块](https://soj.csgrandeur.cn/csgoj/problemset/problem?pid=1436)

```
此题确实是将数论分块用到了极致，可以以3 10 20 30 为例，在纸上列出每个数对应不同i的取整数，会发现在i固定的情况下，当n递增时，相同余数的分块的长度越来越小，但在7之后也能出现相同余数
 
 ... 5  6  7  8  9  10
10    2  1  1  1  1   1   //5个1
20    4  3  2  2  2   2   //4个2
30    6  5  4  3  3   3   //3个3
注意上面的相同余数区间段的长度,而8 9 10 出现了重复的区间段,所以他们的对应的取整数能相等,也就是连乘积能相等,但是遗憾的是,只有某些区间是如此而已,有些没有相同连乘积,确实是需要一个一个慢慢算,判断是否有相等连乘积的方法就是判断他们的右区间,取最小右区间即是相等的长度
除此以外,此题还需要注意的是,取模类的题目,不但要注意超int的时候临时转long long,还要随时控制不要超long long,比如三个数连乘的时候,每次都取一下模,控制数据范围, a * b % mod * c % mod
```

```c++
#include <iostream>
#include <algorithm>
using namespace std;
#define LL long long
const int N = 1e6 + 10;
const int mod = 1e9 + 7;
int fib[N], m, nums[110], minn;
int Solve()
{
    int ret = 0, tmp;
    for (int i = 1, j; i <= minn; i = j + 1)
    {
        j = nums[0] / (nums[0] / i);
        for (int k = 0; k < m; k++)
            j = min(j, nums[k] / (nums[k] / i)); //取最小右区间
        tmp = 1;
        for (int k = 0; k < m; k++)
            tmp = 1LL * tmp * (nums[k] / i) % mod; //1LL可以临时转化为long long,防止超int范围,再次取模防止超LL
        ret = (ret + 1LL * tmp * (fib[j] - fib[i - 1]) % mod) % mod;
    }
    return (ret + mod) % mod; //取模类题目需要特别注意的!不管是否需要,最后结果都给它加个mod再取模,防止ret为负数
}
void Set_Fib()
{
    fib[0] = 1; fib[1] = 1;
    for (int i = 2; i < N; i++)
        fib[i] = (fib[i - 1] + fib[i - 2]) % mod;
    for (int i = 1; i < N; i++)
        fib[i] = (fib[i] + fib[i - 1]) % mod;
}
int main()
{
    Set_Fib();
    while (cin >> m)
    {   
        minn = INT32_MAX;
        for (int i = 0; i < m; i++)
        {
            cin >> nums[i];
            minn = min(minn, nums[i]);
        }
        int r = Solve();
        cout << r << endl;
    }
    return 0;
}
```

[1437 : 数论分块之小小的变通](https://soj.csgrandeur.cn/csgoj/problemset/problem?pid=1437)

本题看似取模，实际上就是在整除分块，然后利用所得模是等差数列，用等差数列求和公式即可

```c++
#include <iostream>
#include <algorithm>
using namespace std;
#define LL long long
int main()
{
    LL n, k;
    while (cin >> n >> k)
    {
        LL left = 1, right, rest, ans = 0;
        while (left <= n && left <= k)
        {
            right = min(k / (k / left), n);
            rest = k % left;
            ans += (rest + rest - (right - left) * (k / left)) * (right - left + 1) / 2;
            left = right + 1;
        }
        if (n > k) ans += k * (n - k);
        cout << ans << endl;
    }
    return 0;
}
```

G ([1467](https://soj.csgrandeur.cn/csgoj/problemset/problem?pid=1467)) : 没有题面的神秘题目-2

**除法向上取整求和**

<img src="https://camo.githubusercontent.com/2080c1169a009b852b035361ed89e26a8ba1bc9ca8e0895f4500a94c795aa4a5/68747470733a2f2f646f63696d67362e646f63732e71712e636f6d2f696d6167652f41674141427163327349705374757a686744354545356661585f4947625336562e706e673f696d6167654d6f6772322f7468756d626e61696c2f31363030782533452f69676e6f72652d6572726f722f31" alt="img" style="zoom: 33%;" />

```c++
#include <iostream>
#include <algorithm>
using namespace std;
using LL = long long;
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    LL n; 
    while (cin >> n)
    {
        LL ans = n;
        n -= 1;
        for (LL l = 1, r; l <= n; l = r + 1)
        {
            r = n / (n / l);
            ans += (n / l) * (r - l + 1);
        }
        cout << ans << endl;
    }
    return 0;
}
```



## 图论

#### 图的存储

```c++
图的存储方法有3种：邻接矩阵，邻接表，链式前向星
稀疏图的储存用邻接表或链式前向星，稠密图用邻接矩阵
    
邻接矩阵
int graph[maxn][maxn];


邻接表 常用STL vector实现
struct edge                                              //定义边
{
    int from, to, w;                                     //边：起点为from，终点为to，权值为w
    edge(int a, int b, int c){from = a; to = b; w = c;}  //对边赋值
};
vector<edge> e[N];                                       //e[i]: 存储第i个节点连接的所有边
//初始化
for (int i = 1; i <= n; i++) e[i].clear();
//存边
e[a].push_back(edge(a, b, c));                           //把边(a, b)存到节点a的邻接表中
//遍历节点u的所有邻居
for (int i = 0; i < e[u].size(); i++)
{
	int v = e[u][i].to, w = e[u][i].w;
    ...
}
//上一个for循环另一种写法
for (int  v : e[u])
{
    ...
}


链式前向星
#include <bits/stdc++.h>
using namespace std;
const int N = 1e6 + 5, M = 2e6 + 5;
int head[N], cnt;    //cnt记录当前存储位置
struct
{
    int from, to, next;  //from为边的起点u, to为边的终点v, next为u的下一个邻居
    int w;               //边权, 类型可以由题目而不同
}edge[M];                //存储边
void init()              //链式前向星初始化
{
    for (int i = 0; i < N; i++) head[i] = -1;      //点初始化
    for (int i = 0; i < M; i++) edge[i].next = -1; //边初始化
    cnt = 0; 
}
void addedge(int u, int v, int w)
{
    edge[cnt].from = u;    //一般情况下这一句是多余的
    edge[cnt].to = v;
    edge[cnt].w = w;
    edge[cnt].next = head[u];
    head[u] = cnt++;
}
int main()
{
    init();
    int n, m; cin >> n >> m;
    for (int i = 0; i < m; i++) {int u, v, w; cin >> u >> v >> w; addedge(u, v, w);}  //输入n个点, m条边
    //打印
    for (int i = 0; i <= n; i++) printf("h[%d] = %d, ", i, head[i]); printf("\n");
    for (int i = 0; i < m; i++) printf("e[%d].to = %d, ", i, edge[i].to); printf("\n");
    for (int i = 0; i < m; i++) printf("e[%d].nex = %d, ", i, edge[i].next); printf("\n");
    for (int i = head[2]; ~i; i = edge[i].next)  //遍历点2的所有邻居, ~i可以写成 i != -1
        printf("%d ", edge[i].to); //printf("%d - %d", edge[i].from, edge[i].to);
    return 0;
}
//Output
6 11
1 2 24
2 1 54
5 2 34
6 3 87
2 3 124
1 4 675
2 4 245
4 1 321
2 5 587
4 5 87
5 6 956
h[0] = -1, h[1] = 5, h[2] = 8, h[3] = -1, h[4] = 9, h[5] = 10, h[6] = 3, 
e[0].to = 2, e[1].to = 1, e[2].to = 2, e[3].to = 3, e[4].to = 3, e[5].to = 4, e[6].to = 4, e[7].to = 1, e[8].to = 5, e[9].to = 5, e[10].to = 6,
e[0].nex = -1, e[1].nex = -1, e[2].nex = -1, e[3].nex = -1, e[4].nex = 1, e[5].nex = 0, e[6].nex = 4, e[7].nex = -1, e[8].nex = 6, e[9].nex = 7, e[10].nex = 2,
5 4 3 1

    
链式前向星代码简化
#include <bits/stdc++.h>
using namespace std;
const int N = 1e6 + 5, M = 2e6 + 5;
int cnt = 0, head[N];  //cnt可根据题目要求赋值
struct
{
    int to, next, w;
}edge[M];
void addedge(int u, int v, int w)
{
    cnt++;   //如果head初始化为0，注意cnt必须从1开始存，
    edge[cnt].to = v;
    edge[cnt].w = w;
    edge[cnt].next = head[u];
    head[u] = cnt;
}
int main()
{
    int n, m; cin >> n >> m;
    for (int i = 0; i < m; i++) {int u, v, w; cin >> u >> v >> w; addedge(u, v, w);}
    for (int i = head[2]; i; i = edge[i].next) printf("%d", edge[i].to); //遍历节点二的所有邻居
    return 0;
}
```

luogu P3916 图的遍历

```c++
//TLE 遍历每一种情况到结束，储存走过的最大值，但是会TLE，因为要走遍每一种情况，时间复杂度太大
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;
const int maxn = 1e5 + 10;
int n, m, a, b;
int vis[maxn];
int ans[maxn];
vector<int> v[maxn];
void dfs(int now, int flag)
{
    ans[flag] = max(ans[flag], now);
    vis[now] = 1;
    for (int i = 0; i < v[now].size(); i++)
        if (!vis[v[now][i]])  dfs(v[now][i], flag);
    vis[now] = 0;
    return;
}
int main()
{
    cin >> n >> m;
    for (int i = 0; i < m; i++)
    {
        int from, to;
        cin >> from >> to;
        v[from].push_back(to);
    }
    for (int i = 1; i <= n; i++) dfs(i, i);
    for (int i = 1; i <= n; i++) cout << ans[i] << " ";
    return 0;
}

//AC 转化思维，考虑每个点可以到达的最大值，不如从最大的点开始，记录较大的点能到的点，前提是要反向存边
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;
const int maxn = 1e5 + 10;
int n, m, a, b;
int ans[maxn];
vector<int> v[maxn];
void dfs(int now, int flag)
{
    if (ans[now]) return;
    ans[now] = flag;
    for (int i = 0; i < v[now].size(); i++)
        dfs(v[now][i], flag);
}
int main()
{
    cin >> n >> m;
    for (int i = 0; i < m; i++)
    {
        int from, to;
        cin >> from >> to;
        v[to].push_back(from);
    }
    for (int i = n; i > 0; i--) dfs(i, i);
    for (int i = 1; i <= n; i++) cout << ans[i] << " ";
    return 0;
}
```

hdu 2094 产生冠军

```c++
#include <algorithm>
#include <iostream>
#include <string>
#include <map>
using namespace std;
int n;
map<string, int> m;
int main()
{
    while (cin >> n && n)
    {
        m.clear();
        int cnt = 0;
        for (int i = 0; i < n; i++)
        {
            string a, b;
            cin >> a >> b;
            m[b]++;
            if (!m.count(a)) m[a] = 0;
        }
        for (auto it = m.begin(); it != m.end(); it++)
            if (it -> second == 0) cnt++;
        if (cnt == 1) cout << "Yes" << endl;
        else cout << "No" << endl; 
    }
    return 0;
}
```



#### 拓扑排序

```
两种方法
1.基于BFS的拓扑排序
分为无前驱的顶点优先，无后继的顶点优先，然而第二种无后继可用无前驱的反向存储逆序输出解决，但是特别注意第一种可以处理最小字典序和，第二种可以处理小的编号尽量往前的问题，不可混淆
无需处理重复情况

2.基于DFS的拓扑排序
需要处理重复情况，即重复有向线不能再次计入
```

poj 1270 Following orders

```c++
#include <algorithm>
#include <iostream>
#include <cstring>
using namespace std;
int n, a[25], dir[30][30];
int topo[25], vis[30], indegree[30];
void dfs(int z, int cnt)
{
    int i;
    topo[cnt] = z;                           //记录拓扑排序
    if (cnt == n - 1)                        //所有点取完了，输出一个拓扑排序
    {
        for (i = 0; i < n; i++) printf("%c", topo[i] + 'a');
        printf("\n");
        return;
    }
    vis[z] = 1;                              //标记为已访问
    for (i = 0; i < n; i++)
        if (!vis[a[i]] && dir[z][a[i]]) indegree[a[i]]--;      //把所有下属的入度减1
    for (i = 0; i < n; i++)
        if (!vis[a[i]] && !indegree[a[i]]) dfs(a[i], cnt + 1); //入度为0的点继续取
    for (i = 0; i < n; i++)
        if (!vis[a[i]] && dir[z][a[i]]) indegree[a[i]]++;
    vis[z] = 0;                                                //恢复
}
int main()
{
    char s[100];
    int len;
    while (gets(s) != NULL)
    {
        memset(dir, 0, sizeof dir);
        memset(vis, 0, sizeof vis);
        memset(indegree, 0, sizeof indegree);
        len = strlen(s);
        n = 0;
        for (int i = 0; i < len; i++)        //存字母到a[]
            if (s[i] <= 'z' && s[i] >= 'a') a[n++] = s[i] - 'a';
        sort(a, a + n);                      //对字母排序，能按字典序输出
        gets(s);
        len = strlen(s);
        int first = 1;                       //first = 1表示当前字母是起点
        for (int i = 0; i < len; i++)        //处理先后关系
        {
            int st, ed;
            if (first && s[i] <= 'z' && s[i] >= 'a')  //起点
            {
                first = 0;
                st = s[i] - 'a';              //把字母转化为数字
                continue;
            }
            if (!first && s[i] <= 'z' && s[i] >= 'a')  //终点
            {
                first = 1;
                ed = s[i] - 'a';
                dir[st][ed] = 1;              //记录先后关系
                indegree[ed]++;               //记录入度，终点入度+1
                continue;
            }
        }
        for (int i = 0; i < n; i++)
            if (!indegree[a[i]]) dfs(a[i], 0); //从所有入度为0的点开始
        printf("\n");
    }
    return 0;
}
```

hdu 1285 确定比赛名次

```c++
//基于DFS的拓扑排序
#include <algorithm>
#include <iostream>
#include <cstring>
using namespace std;
const int maxn = 510;
int n, m, x, y;
int dir[maxn][maxn];
int vis[maxn];
int indegree[maxn];
int topo[maxn];
int a[maxn];
void dfs(int z, int cnt)
{
    topo[cnt] = z;
    if (cnt == n - 1)
    {
        for (int i = 0; i < n; i++) printf(" %d" + !i, topo[i]);
        printf("\n");
        return;
    }
    vis[z] = 1;
    for (int i = 1; i <= n; i++)
        if (!vis[i] && dir[z][i]) indegree[i]--;
    for (int i = 1; i <= n; i++)
        if (!vis[i] && !indegree[i]) dfs(i, cnt + 1);
}
int main()
{
    while (cin >> n >> m)
    {
        memset(dir, 0, sizeof dir);
        memset(indegree, 0, sizeof indegree);
        memset(vis, 0, sizeof vis);
        for (int i = 0; i < m; i++)
        {
            cin >> x >> y;
            if (dir[x][y]) continue;  //出现过的不能再记录
            dir[x][y] = 1;
            indegree[y]++;
        }
        for (int i = 1; i <= n; i++)
            if (!indegree[i]) dfs(i, 0);
    }
    return 0;
}


//无前驱的顶点优先拓扑排序，BFS
#include <algorithm>
#include <iostream>
#include <cstring>
#include <vector>
#include <queue>
using namespace std;
int n, m;
int indegree[510];
int main()
{
    while (cin >> n >> m)
    {
        vector<int> v[510];
        memset(indegree, 0, sizeof indegree);
        for (int i = 1; i <= m; i++)   //重复记录无所谓，因为vector会出手
        {
            int x, y;
            cin >> x >> y;
            v[x].push_back(y);
            indegree[y]++;
        }
        priority_queue<int, vector<int>, greater<int>> q;
        for (int i = 1; i <= n; i++)
            if (!indegree[i]) q.push(i);
        while (!q.empty())
        {
            int tmp = q.top();
            q.pop();
            for (int i: v[tmp])
            {
                indegree[i]--;
                if (!indegree[i]) q.push(i);
            }
            cout << tmp;
            if (!q.empty()) cout << " ";
            else cout << endl;
        }
    }
    return 0;
}
```

HDU 4857 逃生

题意：如果有多种情况，必须考虑`1`先走，即`1`要尽可能的靠在最前，然后再考虑`2，3`等等，**此题要求编号小的尽量在前**，而不是字典序最小，**与字典序是两回事，不可以混淆**（字典序是让前面的编号尽量小，两者对于靠前和编号尽量小的优先级不同），但要注意，编号小的尽可能在前也不能保证全部无联系的编号都按照顺序，甚至可以说是牺牲较大编号的有序性保证小编号尽量靠前，能保一个是一个

此题若采用**无前驱的顶点优先**，会导致`WA`，因为无前驱顶点优先得到的结果是**总体字典序最小**的拓扑排序，在此题中最小字典序不是最优解，因为还要保证没有任何联系的两个元素要保持最小字典序，尽管可能在总体上它并非最小字典序，例如输入 `(1 4), (4 2), (5 3), (3 2)` 时，无前驱顶点优先会得到`1 4 5 3 2`，但是正确答案是`1 5 3 4 2`，因为`4`和`3`没有任何联系，必须按照字典序，让`3`在`4`的前面，所以在此题可以采用**无后继的顶点优先**，也就是说**逆序存放将可以优先实现无联系的元素符合条件**，同时优先队列采用默认的`less<int>` ,但是事实上实现的时候只需要**反向存边**，按照原来**无前驱顶点优先实现**即可，队列要换成`less<int>`, 输出的时候需要**倒序**

<img src="C:\Users\ygtrece\AppData\Roaming\Typora\typora-user-images\image-20230103192836219.png" alt="image-20230103192836219" style="zoom:50%;" />

”我们发现，每一次都取入度为0的并且最小的点输出不能使得最小的点排在尽可能靠前的位置，也就是局部最优不能使得全局最优。所以可以考虑从后往前思考，就是**反向操作，以避开优先队列的缺陷**。我们发现，最后一个输出的一定是出度为0的数。相同时间如果存在多个出度为0的数，则数值大的一定是后输出的。借用一句别人总结的话小的头部不一定排在前面，但是大的尾部一定排在后面。"


```c++
//无前驱的顶点优先，wrong answer
#include <algorithm>
#include <iostream>
#include <cstring>
#include <queue>
using namespace std;
const int N = 3e4 + 10, M = 1e5 + 10;
int t;
int n, m, cnt;
int head[N];
int indegree[N];
struct {int to, next;} edge[M];
void addedge(int u, int v)
{
    cnt++;
    indegree[v]++;
    edge[cnt].to = v;
    edge[cnt].next = head[u];
    head[u] = cnt;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    for (cin >> t; t--; )
    {
        cnt = 0;  //不要忘记初始化！
        memset(indegree, 0, sizeof indegree);
        memset(head, 0, sizeof head);
        memset(edge, 0, sizeof edge);
        int n, m;
        cin >> n >> m;
        for (int i = 0; i < m; i++) {int u, v; cin >> u >> v; addedge(u, v);};
        priority_queue <int, vector<int>, greater<int>> q;
        for (int i = 1; i <= n; i++) if (!indegree[i]) q.push(i);
        while (!q.empty())
        {
            int t = q.top();
            q.pop();
            for (int i = head[t]; i; i = edge[i].next)
            {
                indegree[edge[i].to]--;
                if (!indegree[edge[i].to]) q.push(edge[i].to);
            }
            cout << t;
            if (!q.empty()) cout << " ";
            else cout << endl;
        }
    }
    return 0;
}

//反向存边倒序输出
#include <algorithm>
#include <iostream>
#include <cstring>
#include <vector>
#include <queue>
using namespace std;
const int N = 3e4 + 10, M = 1e5 + 10;
int t;
int n, m, cnt;
int head[N];
int indegree[N];
struct {int to, next;} edge[M];
void addedge(int u, int v)
{
    cnt++;
    indegree[v]++;
    edge[cnt].to = v;
    edge[cnt].next = head[u];
    head[u] = cnt;
}
vector<int> topo;
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    for (cin >> t; t--; )
    {
        cnt = 0;
        memset(indegree, 0, sizeof indegree);
        memset(head, 0, sizeof head);
        memset(edge, 0, sizeof edge);
        int n, m;
        topo.clear();
        cin >> n >> m;
        for (int i = 0; i < m; i++) {int u, v; cin >> u >> v; addedge(v, u);};
        priority_queue <int> q;
        for (int i = 1; i <= n; i++) if (!indegree[i]) q.push(i);
        while (!q.empty())
        {
            int t = q.top();
            q.pop();
            topo.push_back(t);
            for (int i = head[t]; i; i = edge[i].next)
                if (--indegree[edge[i].to] == 0) q.push(edge[i].to);
        }
        for (int i = n - 1; i >= 0; i--)
        {
            if (i != n - 1) cout << " " << topo[i];
            else cout << topo[i];
        }
        cout << endl;
    }
    return 0;
}
```

[P1462 通往奥格瑞玛的道路 - 洛谷](https://www.luogu.com.cn/problem/P1462)

此题的信息是损失的血量和过路费, 关键是明白要找的是血量最短路还是过路费最短路, 如果求过路费最短路, 我们需要从最短的开始求得符合血量要求的路径, 但是实现起来有难度, 所以不妨考虑求血量最短路, 同时**二分过路费用**, 令`l`等于起点和终点过路费的最大值, 令`r`等于所有过路费的最大值, 找尽量小的过路费, 对于大于`mid`的过路费则忽略, 倘若到达终点的血量符合要求则说明该`mid`是符合要求的, 二分思想是解决本题的关键

```c++
#include <bits/stdc++.h>
const int N = 1e4 + 10, M = 5e5 + 10;  //注意存边的容量
using LL = long long;
using namespace std;

int n, m, b, cnt;
int f[N];
int head[N];
struct node
{
    int id; long long n_dis;
    node(int a, long long b) {id = a; n_dis = b;}
    bool operator < (const node &a) const
    {return a.n_dis < n_dis;}
};
struct {int to, next; long long w;} edge[M];
void addedge(int u, int v, int w)
{
    cnt++;
    edge[cnt].to = v;
    edge[cnt].w = w;
    edge[cnt].next = head[u];
    head[u] = cnt;
}
long long dis[N];
bool vis[N];
void Dijkstra(int x)
{
    memset(dis, 0x3f, sizeof dis);
    memset(vis, 0, sizeof vis);
    dis[1] = 0;   //注意此处不可以有vis[1] = 1
    priority_queue<node> q;
    q.push(node(1, dis[1]));
    while (!q.empty())
    {
        node now = q.top(); q.pop();
        int ret = now.id;
        if (vis[ret]) continue; vis[ret] = 1;
        for (int i = head[ret]; i; i = edge[i].next)
        {
            if (vis[edge[i].to] || f[edge[i].to] > x) continue;
            if (dis[edge[i].to] > dis[ret] + edge[i].w)
            {
                dis[edge[i].to] = dis[ret] + edge[i].w;
                q.push(node(edge[i].to, dis[edge[i].to]));
            }
        }
    }
    return;
}
void Solve()
{
    cin >> n >> m >> b;
    int l = 0, r = 0;
    for (int i = 1; i <= n; i++) cin >> f[i], r = max(r, f[i]);
    l = max(f[1], f[n]);
    for (int i = 1; i <= m; i++)
    {
        int u, v, w; cin >> u >> v >> w;
        addedge(u, v, w);
        addedge(v, u, w);
    }
    while (l < r)
    {
        int mid = l + r >> 1;
        Dijkstra(mid);
        if (dis[n] <= b) r = mid;
        else l = mid + 1;
    }
    Dijkstra(l);  //注意这里需要处理一次, 因为可能一开始就有l = r
    if (dis[n] > b) cout << "AFK" << endl;
    else cout << l << endl;
    return;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
        Solve();
    return 0;
}
```



#### 最短路径

| 问题                 | 边权                        | 算法 | 时间复杂度 |
| -------------------- | --------------------------- | ---- | ---- |
| 一个起点，一个终点   | 非负数；无边权（或边权为1） | `A*`算法 | $<O((m+n)log_2n)$ |
|  |  | 双向广搜 | $<O((m+n)log_2n)$ |
|  |  | 贪心最优搜索 | $<O((m+n))$ |
| 一个起点到其他所有点                              | 无边权（或边权为1） | `BFS` |$O(m+n)$|
|                                                   | 非负数 | `Dijkstra`(堆优化优先队列) |$O((m+n)log_2n)$|
|                                                   | 允许有负数 | `SPFA` |$<O(mn)$|
| 所有点对之间         | 允许有负数 | `Floyd-Warshall` | $O(n^3)$ |

```
Floyd-Warshall算法
核心思想：
用DP方法遍历中转点计算最短路径
特征：
1.能一次性求得所有节点之间的最短距离
2.代码简单
3.效率低下，只适用于 n<300 的小规模图
4.用邻接矩阵dp[][]存图
5.判断负环，dp[i][i] < 0 则说明出现负环
适用场景：
1.图的规模小 n<300
2.问题解决和中转点有关
3.路径在“兜圈子”，一个点可能多次经过
4.可能多次查询不同点对之间的最短路径
模板
for (int k = 1; k <= n; k++)       //k循环在i，j循环外边
	for (int i = 1; i <= n; i++)
		for (int j = 1; j <= n; j++)
			dp[i][j] = min(dp[i][j], dp[i][k] + dp[k][j]);   //比较经过k和不经过k
			

用Floyd算法求解传递闭包
1.普通写法
for (int k = 1; k <= n; k++)
	for (int i = 1; i <= n; i++) 
		for (int j = 1; j <= n; j++)
			dp[i][j] |= dp[i][k] & dp[k][j];
2.简单优化
for (int k = 1; k <= n; k++)
	for (int i = 1; i <= n; i++)
		if (dp[i][k])
			for (int j = 1; j <= n; j++)
				if (dp[k][j]) dp[i][j] = 1;
3.用bitset优化
bitset <N> d[N];
for (int k = 1; k <= n; k++)
	for (int i = 1; i <= n; i++)
		if (d[i][k]) d[i] |= d[k];    //其实与前两个方法是等价的，只是用bitset优化能加速
```

```
Dijkstra算法
在大多数最短路径问题中是最常用且效率最高的，是一种“单源”最短路径算法，一次计算能得到一个起点到其他所有点的最短距离长度和最短路径的途径点，本质就是“BFS+优先队列”
局限性：
```

```
Bellman-Ford算法
单源最短路径算法，求一个起点s到其他所有点的最短路径，在算法竞赛中不常用，虽然比Floyd好，但也只能用于小图，Bellman-Ford算法能用于边权为负数的图，这是它比Dijkstra算法具有的优势
```

```
SPFA
是Bellman-Ford算法的改进，可以说是队列优化的Bellman-Ford算法
特点：不稳定，有时需要使用更稳定的Dijkstra算法，但它的优势是边的权值可以为负
简单优化：
1.入队优化: SLF(Small Label First)
使用双端队列，入队的点u与新队头v进行比较，如果dis[u]<dis[v]，将u插入对头，否则插入队尾
2.出队的优化: LLL(Large Label Last)
计算队列中所有点的距离的平均值x, 每次选一个小于x的点出队，如果队头u的dis[u]>x，把u弹出然后放到队尾去，然后继续检查新的队头v，直到找到一个dis[v]<x为止
两种优化可以一起使用
```

lanqiao 1121 计算最短路径

```c++
//Floyd
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
using LL = long long;
const long long INF = 0x3f3f3f3f3f3f3f3fLL;
const int N = 405;
long long dp[N][N];
int n, m, q;
void input()
{
    memset(dp, 0x3f, sizeof dp);
    for (int i = 1; i <= m; i++)
    {
        int u, v;
        long long w;
        cin >> u >> v >> w;
        dp[u][v] = dp[v][u] = min(dp[u][v], w);
    }
}
void floyd()
{
    for (int k = 1; k <= n; k++)
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= n; j++)
                dp[i][j] = min(dp[i][j], dp[i][k] + dp[k][j]);
}
void output()
{
    int s, t;
    while (q--)
    {
        cin >> s >> t;
        if (dp[s][t] == INF) cout << "-1" << endl;
        else if (s == t) cout << "0" << endl;
        else cout << dp[s][t] << endl;
    }
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    cin >> n >> m >> q;
    input();
    floyd();
    output();
    return 0;
}
```

hdu 1385 Minimum Transport Cost

```c++
//Floyd
#include <iostream>
#include <algorithm>
using namespace std;
const int INF = 0x3f3f3f3f;
const int N = 505;
int n, dp[N][N], tax[N], path[N][N];
void input()
{
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= n; j++)
        {
            cin >> dp[i][j];
            if (dp[i][j] == -1) dp[i][j] = INF;
            path[i][j] = j;      //path[i][j]: 此时i, j相邻或者断开
        }
    for (int i = 1; i <= n; i++) cin >> tax[i];  //交税
}
void floyd()
{
    for (int k = 1; k <= n; k++)
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= n; j++)
            {
                int len = dp[i][k] + dp[k][j] + tax[k];   //计算最短路
                if (len < dp[i][j])
                {
                    dp[i][j] = len;
                    path[i][j] = path[i][k];   //标记走向该点需要去向的下一个点
                }
                else if (len == dp[i][j] && path[i][j] > path[i][k])
                    path[i][j] = path[i][k];   //若距离相同，按字典序
            }
}
void output()
{
    int s, t;
    while (cin >> s >> t)
    {
        if (s == -1 && t == -1) break;
        cout << "From " << s << " to " << t << ":" << endl;
        cout << "Path: " << s;
        int k = s;
        while (k != t)          //输出路径从起点到终点
        {
            cout << " --> " << path[k][t];
            k = path[k][t];     //一步一步走向终点
        }
        cout << endl;
        cout << "Total cost : " << dp[s][t] << endl << endl;
    }
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    while (cin >> n && n)
    {
        input(); floyd(); output();
    }
    return 0;
}
```

luogu P1119 灾后重建

```c++
//Floyd
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
const int INF = 0x3f3f3f3f;
int n, m, q, u, v, w, now;
int t[210];
int dp[210][210];
void floyd(int now)
{
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            dp[i][j] = min(dp[i][j], dp[i][now] + dp[now][j]);
}
int main()
{
    memset(dp, 0x3f, sizeof dp);
    cin >> n >> m;
    for (int i = 0; i < n; i++) cin >> t[i];
    for (int i = 0; i < m; i++)
    {
        cin >> u >> v >> w;
        dp[u][v] = dp[v][u] = w;
    }
    for (cin >> q; q--; )
    {
        cin >> u >> v >> w;
        while (t[now] <= w && now < n)
        {
            floyd(now);
            now++;
        }
        if (u == v) cout << "0" << endl;
        else if (t[u] > w || t[v] > w || dp[u][v] == INF) cout << "-1" << endl;
        else cout << dp[u][v] << endl;
    }
    return 0;
}
```

luogu P1613 跑路

利用的是`p[i][j][t] = p[i][k][t - 1] + p[k][j][t - 1]`

```c++
//Floyd
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
const int N = 55;
bool p[N][N][34];
int dp[N][N];
int main()
{
    memset(dp, 0x3f, sizeof dp);
    int n, m; cin >> n >> m;
    for (int i = 1; i <= m; i++)
    {
        int u, v; cin >> u >> v;
        dp[u][v] = 1;
        p[u][v][0] = true;
    }
    for (int t = 1; t <= 32; t++)       //长度为2^t的路径
        for (int k = 1; k <= n; k++)
            for (int i = 1; i <= n; i++)
                for (int j = 1; j <= n; j++)
                    if (p[i][k][t - 1] && p[k][j][t - 1])
                    {
                        p[i][j][t] = true;
                        dp[i][j] = 1;
                    }
    for (int k = 1; k <= n; k++)
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= n; j++)
                dp[i][j] = min(dp[i][j], dp[i][k] + dp[k][j]);
    cout << dp[1][n] << endl;
    return 0;
}
```

hdu 1704 Rank

```c++
//Floyd
#include <iostream>
#include <algorithm>
#include <bitset>
using namespace std;
const int N = 510;
int t, n, m, u, v;
bitset <N> d[N];
void Floyd()   //用bitset加速，能解决N=1000的问题
{
    for (int k = 1; k <= n; k++)
        for (int i = 1; i <= n; i++)
            if (d[i][k]) d[i] |= d[k];
}
int main()
{
    for (cin >> t; t--; )
    {
        cin >> n >> m;
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= n; j++)
                d[i][j] = (i == j);
        for (int i = 0; i < m; i++) {cin >> u >> v; d[u][v] = 1;}
        Floyd();
        int tot = 0;
        for (int i = 1; i <= n; i++)
            for (int j = i + 1; j <= n; j++)
                if (!d[i][j] && !d[j][i]) tot++;
        cout << tot << endl;
    }
    return 0;
}
```

[E - Souvenir (atcoder.jp)](https://atcoder.jp/contests/abc286/tasks/abc286_e)

Floyd, 在中转最小的情况下再考虑最大值路径, 使用`pair<int, long long> dp[N][N]`

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <cmath>
#include <vector>
#include <queue>
#include <map>
typedef long long LL;
const int N = 55;
const long long INF = 0x3f3f3f3f3f3f3f3fLL;
const long long inf = 0x3f3f3f3f;
using namespace std;

int n;
int a[310], graph[310][310];
string s[310];
pair<LL, LL> dp[310][310];
void Floyd()
{
    for (int k = 1; k <= n; k++)
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= n; j++)
            {
                if (dp[i][j].first == dp[i][k].first + dp[k][j].first)
                    dp[i][j].second = max(dp[i][j].second, dp[i][k].second + dp[k][j].second - a[k]);
                else if (dp[i][j].first > dp[i][k].first + dp[k][j].first)
                {
                    dp[i][j].first = dp[i][k].first + dp[k][j].first;
                    dp[i][j].second = dp[i][k].second + dp[k][j].second - a[k];
                }
            }
}
void Solve()
{
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> a[i];
    for (int i = 1; i <= n; i++) cin >> s[i], s[i] = " " + s[i];
    for (int i = 1; i <= n; i++) 
        for (int j = 1; j <= n; j++)
            {
                if (i == j) dp[i][j].first = 0, dp[i][j].second = a[i];
                else if (s[i][j] == 'Y') dp[i][j].first = 1, dp[i][j].second = a[i] + a[j];
                else dp[i][j].first = inf, dp[i][j].second = 0;
            }
    Floyd();
    cin >> n;
    for (int i = 1; i <= n; i++)
    {
        int x, y; cin >> x >> y;
        if (dp[x][y].first == inf) cout << "Impossible" << endl;
        else cout << dp[x][y].first << " " << dp[x][y].second << endl;
    }
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie();
    // int t;
    // for (cin >> t; t--; )
        Solve();
    return 0;
}
```

lanqiao 1122 最短路径

```c++
//Dijkstra
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
#include <vector>
using namespace std;
const long long INF = 0x3f3f3f3f3f3f3f3fLL;
const int N = 3e5 + 2;
struct edge           
{
    int to;           //邻居点
    long long w;      //权值
    edge(int a, long long b){to = a; w = b;}
};
vector<edge> e[N];    //邻接表储存图
struct node
{
    int id; long long n_dis;  //id：节点   n_dis：该节点到起点的距离
    node(int b, long long c){id = b; n_dis = c;}
    bool operator < (const node &a) const    //操作符重载，按照节点到起点的距离大小由小到大排序
    {return a.n_dis < n_dis;}
};
int n, m;
int pre[N];
void print_path(int s, int t)
{
    if (s == t) {printf("%d", s); return;}
    print_path(s, pre[t]);
    printf("%d", t);
}
long long dis[N];    //记录所有节点到起点的距离
bool done[N];        //true表示到节点i的最短路径已经找到
void dijkstra()
{
    int s = 1;          //起点为1
    for (int i = 1; i <= n; i++) {dis[i] = INF; done[i] = false;}  //初始化
    dis[s] = 0;         //起点到自己的距离为0
    priority_queue <node> Q;   //优先队列，存节点信息
    Q.push(node(s, dis[s]));   //起点进队列
    while (!Q.empty())
    {
        node u = Q.top();
        Q.pop();
        if (done[u.id]) continue;  //丢弃已经找到最短路径的节点
        done[u.id] = true;
        for (int i = 0; i < e[u.id].size(); i++)   //检查节点u的所有邻居
        {
            edge y = e[u.id][i];    //u.id的第i个邻居是y.to
            if (done[y.to]) continue;    //丢弃已经找到最短路径的邻居节点
            if (dis[y.to] > y.w + u.n_dis)       //既能用于加入新节点，也可以更新已加入队列的节点的距离
            {
                dis[y.to] = y.w + u.n_dis;
                Q.push(node(y.to, dis[y.to]));   //扩展新邻居放入优先队列
                pre[y.to] = u.id;            //记录路径
            } 
        }
    }
    //print_path(s, n);
}
int main()
{
    cin >> n >> m;
    for (int i = 1; i <= n; i++) e[i].clear();
    while (m--)
    {
        int u, v, w; cin >> u >> v >> w;
        e[u].push_back(edge(v, w));
        //e[v].push_back(edge(v, u, w));   //本题是单向边
    }
    dijkstra();
    for (int i = 1; i <= n; i++)
    {
        if (dis[i] >= INF) cout << "-1";
        else cout << dis[i];
    }
    return 0;
}



// Dijkstra未优化版 O(n^2)
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
using namespace std;
int a[3010][3010], d[3010];
bool v[3010];
int n, m;

void dijkstra() {
	memset(d, 0x3f, sizeof(d)); // dist数组
	memset(v, 0, sizeof(v)); // 节点标记
	d[1] = 0;
	for (int i = 1; i < n; i++) { // 重复进行n-1次
		int x = 0;
		// 找到未标记节点中dist最小的
		for (int j = 1; j <= n; j++)
			if (!v[j] && (x == 0 || d[j] < d[x])) x = j;
		v[x] = 1;
		// 用全局最小值点x更新其它节点
		for (int y = 1; y <= n; y++)
			d[y] = min(d[y], d[x] + a[x][y]);
	}
}

int main() {
	cin >> n >> m;
	// 构建邻接矩阵
	memset(a, 0x3f, sizeof(a));
	for (int i = 1; i <= n; i++) a[i][i] = 0;
	for (int i = 1; i <= m; i++) {
		int x, y, z;
		scanf("%d%d%d", &x, &y, &z);
		a[x][y] = min(a[x][y], z);
	}
	// 求单源最短路径
	dijkstra();
	for (int i = 1; i <= n; i++)
		printf("%d\n", d[i]);
}
```

hdu 2544 最短路径

```c++
//Bellman-Ford
#include <iostream>
#include <algorithm>
using namespace std;
const int INF = 1e6;
const int N = 105;
struct Edge{int u, v, w;} e[10005];
int n, m, cnt;
int pre[N];//记录前驱节点，用于打印路径，pre[x] = y, 在最短路径上节点x的前一个节点为y
void print_path(int s, int t)   //记录前驱式打印函数
{
    if (s == t) {cout << s << " "; return;}
    print_path(s, pre[t]);
    cout << t << " ";
}
void bellman()
{
    int s = 1;   //定义起点
    int d[N];    //记录第i个节点到起点s的最短距离
    for (int i = 1; i <= n; i++) d[i] = INF;   //初始化为无穷大
    d[s] = 0;
    for (int k = 1; k <= n; k++)
        for (int i = 0; i < cnt; i++)
        {
            int x = e[i].u, y = e[i].v;
            if (d[x] > d[y] + e[i].w)  //x通过y到达起点s， 如果距离更短就更新
            {
                d[x] = d[y] + e[i].w;
                //pre[x] = y; //记录每个点的前驱
            }
        }
    cout << d[n] << endl;
    //print_path(s, n);   //如果有需要，打印路径
}
int main()
{
    while (cin >> n >> m)
    {
        if (!n && !m) break;
        cnt = 0;
        while (m--)
        {
            int a, b, c; cin >> a >> b >> c;
            e[cnt].u = a; e[cnt].v = b; e[cnt].w = c; cnt++;
            e[cnt].u = b; e[cnt].v = a; e[cnt].w = c; cnt++;
        }
        bellman();
    }
    return 0;
}


//SPFA
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
using namespace std;
const int INF = 0x3f3f3f3f;
const int N = 1e6 + 5, M = 2e6 + 5;
int n, m;
int pre[N];
void print_path(int s, int t)
{
    if (s == t) {cout << s; return;}
    print_path(s, pre[t]);
    cout << t;
}
int head[N], cnt;
struct {int to, next, w;}edge[M];
void addedge(int u, int v, int w)
{
    cnt++;
    edge[cnt].to = v;
    edge[cnt].w = w;
    edge[cnt].next = head[u];
    head[u] = cnt;
}
void init()
{
    memset(head, 0, sizeof head);
    memset(edge, 0, sizeof edge);
    cnt = 0;
}
int dis[N];
bool inq[N];
int Neg[N];  //如果需要判断负环
int spfa(int s)
{
    memset(Neg, 0, sizeof Neg);
    Neg[s] = 1;
    for (int i = 1; i <= n; i++) {dis[i] = INF; inq[i] = false;}
    dis[s] = 0;
    queue<int> Q;
    Q.push(s); inq[s] = true;
    while (!Q.empty())
    {
        int u = Q.front(); Q.pop();
        inq[u] = false;
        for (int i = head[u]; i; i = edge[i].next)
        {
            int v = edge[i].to, w = edge[i].w;
            if (dis[u] + w < dis[v])
            {
                dis[v] = dis[u] + w;
                pre[v] = u;
                if (!inq[v])
                {
                    inq[v] = true;
                    Q.push(v);
                    Neg[v]++;
                    if (Neg[v] > n) return 1;   //出现负环
                }
            }
        }
    }
    return 0;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    while (cin >> n >> m && n && m)
    {
        init();
        while (m--)
        {
            int u, v, w; cin >> u >> v >> w;
            addedge(u, v, w); addedge(v, u, w);
        }
        spfa(1);
        cout << dis[n] << endl;
        // cout << "path: "; print_path(1, n); cout << endl;
    }
    return 0;
}
```

luogu P2868 Sightseeing cows

最优比率环？？？

```
const int N = 1e4 +5, M = 5e4 + 5;
const int INF = 0x3f3f3f3f;
double dis[N];
int f[N], head[N], cnt, n, m;
int u[M], v[M], w[M];
struct {int to, next, w;}edge[M];
void addedge(int u, int v, int w)
{
    cnt++;
    edge[cnt].to = v;
    edge[cnt].w = w;
    edge[cnt].next = head[u];
    head[u] = cnt;
}
bool inq[N];
int Neg[N];
int spfa(int s)
{
    Neg[s] = 1;
    for (int i = 1; i <= n; i++) {dis[i] = INF; inq[i] = false;}
    dis[s] = 0;
    queue<int> Q;
    Q.push(s); inq[s] = true;
    while (!Q.empty())
    {
        int u = Q.front(); Q.pop();
        inq[u] = false;
        for (int i = head[u]; i; i = edge[i].next)
        {
            int v = edge[i].to, w = edge[i].w;
            if (dis[u] + w < dis[v])
            {
                dis[v] = dis[u] + w;
                if (!inq[v])
                {
                    inq[v] = true;
                    Q.push(v);
                    Neg[v]++;
                    if (Neg[v] > n) return 1;   
                }
            }
        }
    }
    return 0;
}
bool check(double x)
{
    for (int i = 1; i <= n; i++) addedge(u[i], v[i], x * w[i] - f[u[i]]);
    return spfa(1);
}
int main()
{
    cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> f[i];
    for (int i = 1; i <= m; i++) {cin >> u[i] >> v[i] >> w[i];}
    double L = 0, R = 0;
    for (int i = 1; i <= n; i++) R += f[i];
    for (int i = 0; i < 30; i++)
    {
        double mid = L + (R - L) / 2;
        if (check(mid)) L = mid;
        else R = mid;
    }
    printf("%.2f", L);
    return 0;
}
```

luogu 	P3371 【模板】单源最短路径（弱化版）

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
using namespace std;
const int N = 1e4 + 10, M = 5e5 + 10;
const int INF = 0x3f3f3f3f;
struct {int to, next, w;}edge[M];
int head[N], cnt, n, m, s;
void addedge(int u, int v, int w)
{
    edge[++cnt].to = v;
    edge[cnt].w = w;
    edge[cnt].next = head[u];
    head[u] = cnt;
}
bool inq[N];
int dis[N];
void spfa(int s)
{
    for (int i = 1; i <= n; i++) {dis[i] = INF; inq[i] = false;}
    dis[s] = 0;
    queue<int> Q;
    Q.push(s); inq[s] = true;
    while (!Q.empty())
    {
        int u = Q.front(); Q.pop();
        inq[u] = false;
        for (int i = head[u]; i; i = edge[i].next)
        {
            int v = edge[i].to, w = edge[i].w;
            if (dis[v] > dis[u] + w)
            {
                dis[v] = dis[u] + w;
                if (!inq[v])
                {
                    Q.push(v);
                    inq[v] = true;
                }
            }
        }
    }
}
int main()
{
    cin >> n >> m >> s;
    for (int i = 1; i <= m; i++) {int u, v, w; cin >> u >> v >> w; addedge(u, v, w);}
    spfa(s);
    for (int i = 1; i <= n; i++)
    {
        if (dis[i] == INF) cout << "2147483647 ";
        else cout << dis[i] << " "; 
    }
    return 0;
}
```

luogu P4779 【模板】单源最短路径（标准版）

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
using namespace std;
const int INF = 0x3f3f3f3f;
const int N = 1e5 + 10, M = 2e5 + 10;
int n, m, s;
struct edge
{
    int to, w;
    edge(int a, int b) {to = a; w = b;}
};
vector<edge> e[M];
struct node
{
    int id, n_dis;
    node(int a, int b) {id = a; n_dis = b;}
    bool operator < (const node &a) const
    {return n_dis > a.n_dis;}
};
int dis[N];
bool done[N];
void dijstra()
{
    int s = 1;
    for (int i = 1; i <= n; i++) {dis[i] = INF; done[i] = false;}
    dis[s] = 0;
    priority_queue<node> Q;
    Q.push(node(s, dis[s]));
    while (!Q.empty())
    {
        node u = Q.top(); Q.pop();
        if (done[u.id]) continue;
        done[u.id] = true;
        for (int i = 0; i < e[u.id].size(); i++)
        {
            edge y = e[u.id][i];
            if (done[y.to]) continue;
            if (dis[y.to] > u.n_dis + y.w)
            {
                dis[y.to] = u.n_dis + y.w;
                Q.push(node(y.to, dis[y.to]));
            }
        }
    }
}
int main()
{
    cin >> n >> m >> s;
    for (int i = 1; i <= n; i++) e[i].clear();
    while (m--)
    {
        int u, v, w; cin >> u >> v >> w;
        e[u].push_back(edge(v, w));
    }
    dijstra();
    for (int i = 1; i <= n; i++) cout << dis[i] << " ";
    return 0;
}
```

POJ 2387 Til the Cows Come Home

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
using namespace std;
const int N = 1e4 + 10, M = 2e4 + 10;
const int INF = 0x3f3f3f3f;
int n, m;
struct edge
{
    int v, w;
    edge(int a, int b) {v = a; w = b;}
};
vector<edge> e[M];
struct node
{
    int id, n_dis;
    node(int a, int b) {id = a; n_dis = b;}
    bool operator < (const node &a) const
    {return a.n_dis < n_dis;}
};
bool done[N];
int dis[N];
void dijstra()
{
    int s = 1;
    for (int i = 1; i <= n; i++) {dis[i] = INF; done[i] = false;}
    priority_queue<node> Q;
    dis[s] = 0;
    Q.push(node(s, dis[s]));
    while (!Q.empty())
    {
        node u = Q.top(); Q.pop();
        if (done[u.id]) continue;
        done[u.id] = true;
        for (int i = 0; i < e[u.id].size(); i++)
        {
            edge y = e[u.id][i];
            if (done[y.v]) continue;
            if (dis[y.v] > u.n_dis + y.w)
            {
                dis[y.v] = u.n_dis + y.w;
                Q.push(node(y.v, dis[y.v]));
            }
        }
    }
}
int main()
{
    cin >> m >> n;
    for (int i = 1; i <= m; i++) 
    {
        int u, v, w; cin >> u >> v >> w; 
        e[u].push_back(edge(v, w));
        e[v].push_back(edge(u, w));
    }
    dijstra();
    cout << dis[n];
    return 0;
}
```

POJ 1797 Heavy Transportation

此题是**Dijkstra变式**，与先前不同的是，它的松弛是`dis[y.to] < min(dis[u.id], y.w)`,如果成立就进行更新，原因是此题是想寻找`1`到`n`的**所有路径的最小权值的最大值**，以前的dis[N]是用来存放当前节点到起点的最短距离，现在的`dis[N]`是用来存放当前节点到起点的路径的最小权值，而且我们始终要保持这个权值取最大，使用的方法就是上面的松弛公式，如果从另一路径过来能使得某个节点的最小权值能更大，那我们就需要更新，否则就不必更新，视作抛弃该路径；如此一直操作至`dis[n]`，则`dis[n]`就是答案；值得特别注意的是，本题的优先队列采用的是大根堆，即从大到小排序，因为我们如果先操作`n_dis`较小的节点，就默认该节点已经找到最大的权值，这可能会导致有另一条能使权值更大的路径因为我们还没走，所以该节点的最大权值并不是真正的最大，而即使存在一条权值更大的，也是从权值大的边走过来的，所以我们优先操作权值大的边能避免这种情况

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
using namespace std;
const int N = 1e3 + 10, M = 2e3 + 10;
const int INF = 0x3f3f3f3f;
int t, n, m;
struct edge
{
    int to, w;
    edge(int a, int b) {to = a; w = b;}
};
vector <edge> e[N];
struct node
{
    int id, n_dis;
    node(int a, int b) {id = a; n_dis = b;}
    bool operator < (const node &a) const
    {return a.n_dis > n_dis;}   //大根堆
};
int dis[N];
bool done[N];
void dijkstra()
{
    int s = 1;
    priority_queue<node> Q;
    for (int i = 1; i <= n; i++) {dis[i] = 0; done[i] = false;}
    dis[s] = INF;
    Q.push(node(s, dis[s]));
    while (!Q.empty())
    {
        node u = Q.top(); Q.pop();
        if (done[u.id]) continue;
        done[u.id] = true;
        for (int i = 0; i < e[u.id].size(); i++)
        {
            edge y = e[u.id][i];
            if (done[y.to]) continue;
            if (dis[y.to] < min(dis[u.id], y.w))    //新的松弛方式
            {
                dis[y.to] = min(dis[u.id], y.w);
                Q.push(node(y.to, dis[y.to]));
            }
        }
    }
}
int main()
{
    cin >> t;
    for (int i = 1; i <= t; i++)
    {
        for (int i = 0; i < N; i++) e[i].clear();
        cin >> n >> m;
        for (int j = 1; j <= m; j++)
        {
            int u, v, w; cin >> u >> v >> w;
            e[u].push_back(edge(v, w));
            e[v].push_back(edge(u, w));
        }
        dijkstra();
        printf("Scenario #%d:\n%d\n\n", i, dis[n]);
    }
    return 0;
}
```

POJ 3660 Cow Contest

**Floyd传递闭包**

```c++
#include <iostream>
#include <algorithm>
#include <bitset>
using namespace std;
const int N = 105;
int n, m, tot;
bool flag[N];
bitset <N> d[N];
void Floyd()
{
    for (int k = 1; k <= n; k++)
        for (int i = 1; i <= n; i++)
            if (d[i][k]) d[i] |= d[k];
}
int main()
{
    cin >> n >> m;
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= n; j++)
            d[i][j] = (i == j);
    for (int i = 1; i <= m; i++)
    {
        int u, v; cin >> u >> v; 
        d[u][v] = 1;
    }
    Floyd();
    for (int i = 1; i <= n; i++)
        for (int j = i + 1; j <= n; j++)
            if (d[i][j] == 0 && d[j][i] == 0) flag[i] = 1, flag[j] = 1;
    for (int i = 1; i <= n; i++) if (!flag[i]) tot++;
    cout << tot << endl;
    return 0;
}
```

POJ 1502 MPI Maelstrom

此题的输入处理比较特殊，可以先采用`scanf`接收到字符串，然后再用`sscanf()`或者`atoi()`进行转换,他们的作用都是将字符串转换为数字， 注意while后也不必加getchar(), 因为`%d`和`%s`自动跳过空字符，只有`%c`不跳过，`cin()`也能跳过

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
const int N = 105;
const int INF = 0x3f3f3f3f;
int n, tmp;
int dp[N][N];
int main()
{
    while (~scanf("%d", &n))
    {
        //getchar();
        memset(dp, 0x3f, sizeof dp);
        for (int i = 2; i <= n; i++) 
            for (int j = 1; j <= i - 1; j++)
                {
                    char ret[10]; 
                    scanf("%s", &ret);
                    if (ret[0] == 'x') dp[i][j] = dp[j][i] = INF;
                    else  //转换
                    {
                        // sscanf(ret, "%d", &tmp);
                        // dp[i][j] = dp[j][i] = tmp;
                        dp[i][j] = dp[j][i] = atoi(ret);
                    }
                }
        for (int k = 1; k <= n; k++)
            for (int i = 1; i <= n; i++) 
                for (int j = 1; j <= n; j++)
                    dp[i][j] = min(dp[i][j], dp[i][k] + dp[k][j]);
        int ans = 0;
        for (int i = 2; i <= n; i++) ans = max(ans, dp[1][i]);
        cout << ans << endl;
    } 
    return 0;
}
```

POJ 1062 昂贵的聘礼

本题需要对符合条件的区间进行枚举，并对子区间进行`Dijkstra`

```c++
#include <iostream>
#include <algorithm>
#include <queue>
using namespace std;
const int N = 110, M = 1e5 + 10;
const int INF = 0x3f3f3f3f;
int n, ans = INF, lim, cnt, num;
int mon[N], lev[N];
int head[N];
struct edge{int to, next, w;}e[M];
void addedge(int u, int v, int w)
{
    e[++cnt].to = v;
    e[cnt].w = w;
    e[cnt].next = head[u];
    head[u] = cnt;
}
int dis[N];
bool done[N];
struct node
{
    int id, n_dis;
    node(int a, int b) {id = a; n_dis = b;}
    bool operator < (const node &a) const
    {return a.n_dis < n_dis;}
};
int dijkstra(int l, int r)
{
    int s = 1;
    for (int i = 1; i <= n; i++) {dis[i] = INF; done[i] = false;}
    priority_queue<node> q;
    dis[s] = 0; q.push(node(s, dis[s]));
    while (q.size())
    {
        node u = q.top(); q.pop();
        if (done[u.id] || lev[u.id] > r || lev[u.id] < l) continue;
        done[u.id] = true;
        for (int i = head[u.id]; i; i = e[i].next)
        {
            int v = e[i].to, w = e[i].w;
            if (lev[v] > r || lev[v] < l || done[v]) continue;
            if (dis[v] > u.n_dis + w)
            {
                dis[v] = u.n_dis + w;
                q.push(node(v, dis[v]));
            }
        }
    }
    int tmp = mon[1];  //为什么设为INF，从i = 1开始不行？
    for (int i = 2; i <= n; i++)
    {
        if (lev[i] > r || lev[i] < l) continue;
        dis[i] += mon[i];
        tmp = min(tmp, dis[i]);
    }
    return tmp;
}
int main()
{
    cin >> lim >> n;
    for (int i = 1; i <= n; i++)
    {
        cin >> mon[i] >> lev[i] >> num;
        for (int j = 1; j <= num; j++)
        {
            int v, w; cin >> v >> w;
            addedge(i, v, w);        
        }
    }
    for (int i = 1; i <= n; i++)
    {
        int ret = dijkstra(i, i + lim);
        ans = min(ans, ret);
    }
    cout << ans;
    return 0;
}
```

POJ 2253 Frogger

```c++
//Dijkstra
#include<iostream>
#include<cstdio>
#include<cmath>
#include<stdlib.h>
#include<algorithm>
using namespace std;
int n;
const int N = 210;
const double INF = 1e5;
typedef pair<int, int> P;
double dis[N];	//代表从1号到i号石头的青蛙距离
int visit[N];
P point[N];

double getLength(double x1, double y1, double x2, double y2)
{
	double len = sqrt((x1 - x2)*(x1 - x2) + (y1 - y2)*(y1 - y2));
	return len;
}
void init()
{
	for (int i = 1; i <= n; i++)
		visit[i] = 0;
	for (int i = 2; i <= n; i++)	//初始化各个石头到1号石头的青蛙距离
			dis[i] = getLength(point[1].first, point[1].second, point[i].first, point[i].second);
}
void dijkstra()
{
	visit[1] = 1;	//1号石头起点，标记
	for (int i = 2; i <= n; i++)
	{
		int t = -1;
		for (int j = 2; j <= n; j++)
		{
			//得到距离最小的点
			if (!visit[j] && (t==-1 || dis[j] < dis[t])) {
				t = j;
			}
		}
		visit[t] = 1;		//标记
		for (int j = 1; j <= n; j++)
		{
			if (!visit[j]) {
				double len = getLength(point[t].first, point[t].second, point[j].first, point[j].second);
				if (dis[j] > max(len, dis[t]))dis[j] = max(len, dis[t]);
				//松驰操作，dis[j]表示1到j的青蛙距离，max(len, dis[t])表示1通过t到达j的青蛙距离，两者取最小值
			}
		}
	}
}
int main()
{
	int cnt = 1;
	while (cin >> n, n)
	{
		for (int i = 1; i <= n; i++)
		{
			int x, y;
			cin >> x >> y ;
			point[i].first = x, point[i].second = y;
		}
		init();
		dijkstra();
		printf("Scenario #%d\n", cnt);
		printf("Frog Distance = %.3lf\n", dis[2]);
		printf("\n");
		cnt++;
	}
	return 0;
}
```

luogu P1144 最短路计数

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
using namespace std;
const int N = 1e6 + 10, M = 2e6 + 10;
const int INF = 0x3f3f3f3f;
const int mod = 1e5 + 3;
int n, m, cnt, ans[N];
int head[N];
struct {int to, next;}edge[M];
void addedge(int u, int v)
{
    edge[++cnt].to = v;
    edge[cnt].next = head[u];
    head[u] = cnt; 
}
int dis[N];
bool inq[N];
void spfa()
{
    for (int i = 1; i <= n; i++) {dis[i] = INF; inq[i] = false;}
    queue<int> q;
    int s = 1;
    dis[s] = 0; inq[s] = true;
    q.push(s);
    while (q.size())
    {
        int f = q.front(); q.pop(); inq[f] = false;
        for (int i = head[f]; i; i = edge[i].next)
        {
            if (dis[f] + 1 < dis[edge[i].to])
            {
                dis[edge[i].to] = dis[f] + 1;
                if (!inq[edge[i].to]) {q.push(edge[i].to); inq[edge[i].to] = true;}
            }
        }
    }
}
int dfs(int x)  //记忆化搜索
{
    if (ans[x]) return ans[x];
    for (int i = head[x]; i; i = edge[i].next)
        if (dis[x] == 1 + dis[edge[i].to]) ans[x] = (ans[x] + dfs(edge[i].to)) % mod;
    return ans[x];
}
int main()
{
    cin >> n >> m;
    for (int i = 1; i <= m; i++) {int u, v; cin >> u >> v; addedge(u, v); addedge(v, u);}
    spfa();
    ans[1] = 1;
    for (int i = 1; i <= n; i++) cout << dfs(i) << endl;
    return 0;
}
```



```

```



#### 最小生成树

```
最小生成树是有边权的无向图的一个问题，也很常见
在无向图G(V, E)中，把连通而且不含有圈(环路)的一个子图称为一棵生成树
边权之和最小的树称为最小生成树(MST)

有两种算法可以构造MST，都基于贪心算法
1.Kruskal算法
2.Prim算法
区别：
1.Prim算法效率高，算法复杂度为O(mlogn), Kruskal算法复杂度为O(mlogm), n为点数，m为边数，且图的边数一般比点数多
2.Kruskal算法编码简单，如果题目给的数据规模不太大，就用Kruskal算法编码
```

luogu P3366 【模板】最小生成树

```c++
#include <algorithm>
#include <iostream>
using namespace std;
const int N = 5005, M = 2e5 + 1;
struct Edge{int u, v, w;}edge[M];
bool cmp(Edge a, Edge b) {return a.w < b.w;}
int s[N];
int n, m;
int find_set(int x)
{
    if (x != s[x]) s[x] = find_set(s[x]);
    return s[x];
}
void kruskal()
{
    sort(edge + 1, edge + m + 1, cmp);
    for (int i = 1; i <= n; i++) s[i] = i;
    int ans = 0, cnt = 0;
    for (int i = 1; i <= m; i++)
    {
        if (cnt == n - 1) break;
        int e1 = find_set(edge[i].u);
        int e2 = find_set(edge[i].v);
        if (e1 == e2) continue;
        else
        {
            ans += edge[i].w;
            s[e1] = e2;
            cnt++;
        }
    }
    if (cnt == n - 1) cout << ans;
    else cout << "orz";
}
int main()
{
    cin >> n >> m;
    for (int i = 1; i <= m; i++) cin >> edge[i].u >> edge[i].v >> edge[i].w;
    kruskal();
    return 0;
}
```

luogu P2330 [SCOI2005]繁忙的都市

```c++
#include <algorithm>
#include <iostream>
using namespace std;
const int N = 319, M = 1e5 + 10;
int s[N], n, m;
struct Edge {int u, v, w;} edge[M];
bool cmp(Edge a, Edge b) {return a.w < b.w;}
int find_set(int x)
{
    if (x != s[x]) s[x] = find_set(s[x]);
    return s[x];
}
void kruskal()
{
    sort(edge + 1, edge + 1 + m, cmp);
    for (int i = 1; i <= n; i++) s[i] = i;
    int ans = 0, cnt = 0;
    for (int i = 1; i <= m; i++)
    {
        if (cnt == n - 1) break;
        int e1 = find_set(edge[i].u);
        int e2 = find_set(edge[i].v);
        if (e1 == e2) continue;
        else
        {
            cnt++;
            ans = max(ans, edge[i].w);
            s[e1] = e2;
        }
    }
    cout << cnt << " " << ans;
}
int main()
{
    cin >> n >> m;
    for (int i = 1; i <= m; i++) cin >> edge[i].u >> edge[i].v >> edge[i].w;
    kruskal();
    return 0;
}
```

luogu P1195 口袋的天空

```c++
#include <algorithm>
#include <iostream>
using namespace std;
const int N = 1e3 + 10, M = 1e4 + 10;
int s[N], n, m, k;
struct Edge{int u , v, w;}edge[M];
bool cmp(Edge a, Edge b) {return a.w < b.w;}
int find_set(int x)
{
    if (x != s[x]) s[x] = find_set(s[x]);
    return s[x];
}
void kruskal()
{
    sort(edge + 1, edge + 1 + m, cmp);
    for (int i = 1; i <= n; i++) s[i] = i;
    int cnt = n, ans = 0;
    for (int i = 1; i <= m; i++)
    {
        int e1 = find_set(edge[i].u);
        int e2 = find_set(edge[i].v);
        if (e1 == e2) continue;
        else
        {
            s[e1] = e2;
            cnt--;
            ans += edge[i].w; 
        }
        if (cnt == k) {cout << ans; return;}
    }
    cout << "No Answer";
    return;
}
int main()
{
    cin >> n >> m >> k;
    for (int i = 1; i <= m; i++) cin >> edge[i].u >> edge[i].v >> edge[i].w;
    kruskal();
    return 0;
}
```

luogu P1194 买礼物

？

```c++
#include <algorithm>
#include <iostream>
using namespace std;
const int N = 550, M = 3e5 + 10;
int a, b, cnt;
int s[N];
struct Edge{int u, v, w;}edge[M];
bool cmp(Edge a, Edge b) {return a.w < b.w;}
int find_set(int x)
{
    if (x != s[x]) s[x] = find_set(s[x]);
    return s[x];
}
void kruskal()
{
    sort(edge + 1, edge + 1 + cnt, cmp);
    for (int i = 1; i <= b; i++) s[i] = i;
    int ans = 0, n = 0;
    for (int i = 1; i <= cnt; i++)
    {
        if (n == b) break;
        int e1 = find_set(edge[i].u);
        int e2 = find_set(edge[i].v);
        if (e1 == e2) continue;
        else
        {
            s[e1] = e2;
            ans += edge[i].w;
            n++;
        }
    }
    cout << ans << endl;
}
int main()
{
    cin >> a >> b;
    for (int i = 1; i <= b; i++)
        for (int j = 1; j <= b; j++)
        {
            int ret;
            cin >> ret;
            if (!ret || j > i) continue;
            edge[++cnt].u = i;
            edge[cnt].v = j;
            edge[cnt].w = ret;
        }
    for (int i = 1; i <= b; i++)  //与0建立权值关系
    {
        edge[++cnt].u = 0;
        edge[cnt].v = i;
        edge[cnt].w = a;
    }
    kruskal();
    return 0;
}
```

luogu P2820 局域网

```c++
#include <algorithm>
#include <iostream>
using namespace std;
const int N = 105, M = 3e5 + 10;
int s[N];
int n, k, sum;
struct Edge{int u, v, w;}edge[M];
bool cmp(Edge a, Edge b) {return a.w < b.w;}
int find_set(int x)
{
    if (x != s[x]) s[x] = find_set(s[x]);
    return s[x];
}
void kruskal()
{
    sort(edge + 1, edge + 1 + k, cmp);
    for (int i = 1; i <= n; i++) s[i] = i;
    int ans = 0, cnt = 0;
    for (int i = 1; i <= k; i++)
    {
        int e1 = find_set(edge[i].u);
        int e2 = find_set(edge[i].v);
        if (e1 == e2) continue;
        else
        {
            s[e1] = e2;
            ans += edge[i].w;
            cnt++;
        }
        if (cnt == n - 1) break;
    }
    cout << sum - ans << endl;
}
int main()
{
    cin >> n >> k;
    for (int i = 1; i <= k; i++)
    {
        cin >> edge[i].u >> edge[i].v >> edge[i].w;
        sum += edge[i].w;
    }
    kruskal();
    return 0;
}
```

洛谷 P4047 JSOI2010 部落划分 

二分?

[题解【二分答案】【生成树】【并查集】 - wjyyy 博客](http://www.wjyyy.top/735.html)

```c++
#include <algorithm>
#include <iostream>
#include <cmath>
using namespace std;
const int N = 1e3 + 10, M = 1e6 + 10;
int n, k, m;
int s[N], x[N], y[N];
struct Edge{int u, v, w;}edge[M];
bool cmp(Edge a, Edge b) {return a.w < b.w;}
int find_set(int x)
{
    if (x != s[x]) s[x] = find_set(s[x]);
    return s[x];
}
void kruskal()
{
    sort(edge + 1, edge + 1 + m, cmp);
    for (int i = 1; i <= n; i++) s[i] = i;
    int cnt = n;
    for (int i = 1; i <= m; i++)
    {
        int e1 = find_set(edge[i].u);
        int e2 = find_set(edge[i].v);
        if (e1 == e2) continue;
        else
        {
            cnt--;
            s[e1] = e2;
        }
        if (cnt == k - 1)
        {
            printf("%.2f", sqrt(edge[i].w));
            break;
        }
    }
}
int main()
{
    cin >> n >> k;
    for (int i = 1; i <= n; i++)
    {
        cin >> x[i] >> y[i];
        for (int j = 1; j < i; j++)
        {
            edge[++m].u = i;
            edge[m].v = j;
            edge[m].w = (x[i] - x[j]) * (x[i] - x[j]) + (y[i] - y[j]) * (y[i] - y[j]);
        }
    }
    kruskal();
    return 0;
}
```

[P2632 Explorer - 洛谷](https://www.luogu.com.cn/problem/P2632)

分布处理, 首先处理点, 注意一条直线上同一个位置可能有多个相同点, 所以要判重; 然后建图, 如果把每个点和其他所有点连接起来显然是行不通的, 复杂度太高, 因此我们先将同一条直线上的每一个点连接起来, 然后对于一条直线上的点, **三分**出另一条直线上距离该点最近的两个点进行连边, 此处需要用到三分的原因是两边指针和该点的距离都是逐渐减少, 所以是一个先单调递减再单调递增的图, 用三分先确定两个点, 然后根据两个点的对应的距离大小调整左右指针即可, 同时为了防止特殊情况, 也把旁边`[l, r]`两个点连接起来, 

```c++
#include <bits/stdc++.h>
const int N = 3e5 + 10, M = 2e6 + 10;
using LL = long long;
using namespace std;

struct point
{
    double x, y;
    int id;
    point() {}
    point(double a, double b, int c)
    {
        x = a;
        y = b;
        id = c;
    }
} p[N], q[N];
void input(point *a)
{
    scanf("%lf%lf", &(a->x), &(a->y));
}
double getdis(point a, point b)
{
    return sqrt((a.x - b.x) * (a.x - b.x) + (a.y - b.y) * (a.y - b.y));
}

struct edge_table
{
    int from, to;
    double value;
    bool operator < (const edge_table &a) const
    {
        return a.value > value;
    }
} edge[M];
int edge_cnt = 0;
void add_edge(int u, int v, double w)
{
    edge[++edge_cnt].from = u;
    edge[edge_cnt].to = v;
    edge[edge_cnt].value = w;
}
int n, m;
double t1[N], t2[N];
void delete_same() // 判重函数
{ 
    sort(t1, t1 + n);
    sort(t2, t2 + m);
    int ptr = 0;
    for (int i = 0; i < n; i++)
    {
        if (i == n - 1 || t1[i] != t1[i + 1])
            t1[ptr++] = t1[i];
    }
    n = ptr; // 将n重置为判重后点的数目
    ptr = 0;
    for (int i = 0; i < m; i++)
    {
        if (i == m - 1 || t2[i] != t2[i + 1])
            t2[ptr++] = t2[i];
    }
    m = ptr;
}

int father[N]; // 建立并查集
int find(int x)
{ // 并查集的查找函数
    if (father[x] != x)
        father[x] = find(father[x]); // 路径压缩
    return father[x];
}
double kruskal()
{
    for (int i = 0; i <= n + m; i++)
        father[i] = i; // 初始化并查集，让每一个点自成一个独立的连通分量
    double sum = 0;
    sort(edge + 1, edge + edge_cnt + 1); // 按边的长度从小到大排序
    for (int i = 1; i <= edge_cnt; i++)
    {
        int tx = find(edge[i].from);
        int ty = find(edge[i].to);
        if (tx != ty)
        {                         // 如果两个点在两个不同的连通分量
            father[tx] = ty;      // 合并两个连通分量
            sum += edge[i].value; // 将边加入最小生成树
        }
    }
    return sum;
}
int main()
{
    point a, b, c, d;
    cin >> n >> m;
    input(&a);
    input(&b);
    input(&c);
    input(&d);
    for (int i = 0; i < n; i++)
        cin >> t1[i];
    for (int i = 0; i < m; i++)
        cin >> t2[i];
    delete_same();
    for (int i = 0; i < n; i++)
        p[i] = point(a.x * t1[i] + b.x * (1 - t1[i]), a.y * t1[i] + b.y * (1 - t1[i]), i + 1);
    for (int i = 0; i < m; i++)
        q[i] = point(c.x * t2[i] + d.x * (1 - t2[i]), c.y * t2[i] + d.y * (1 - t2[i]), i + n + 1);

    edge_cnt = 0;
    for (int i = 0; i < n - 1; i++)
    {
        double l = getdis(p[i], p[i + 1]);
        add_edge(p[i].id, p[i + 1].id, l);
        add_edge(p[i + 1].id, p[i].id, l);
    }
    for (int i = 0; i < m - 1; i++)
    {
        double l = getdis(q[i], q[i + 1]);
        add_edge(q[i].id, q[i + 1].id, l);
        add_edge(q[i + 1].id, q[i].id, l);
    }
    for (int i = 0; i < n; i++)
    {
        int l, r;
        l = 0;
        r = m - 1;
        while (r - l > 1)   //三分, 注意循环条件和取点细节
        {
            int mid1 = (r + l) / 2;
            int mid2 = (mid1 + r) / 2;
            if (getdis(p[i], q[mid1]) > getdis(p[i], q[mid2]))
                l = mid1;
            else
                r = mid2;
        }
        add_edge(p[i].id, q[l].id, getdis(p[i], q[l]));  //将距离最短的两条边加入邻接表
        add_edge(q[l].id, p[i].id, getdis(p[i], q[l]));
        add_edge(p[i].id, q[r].id, getdis(p[i], q[r]));
        add_edge(q[r].id, p[i].id, getdis(p[i], q[r]));
        if (l - 1 >= 0)  //将距离第二短的两条边加入邻接表
        {
            add_edge(p[i].id, q[l - 1].id, getdis(p[i], q[l - 1]));
            add_edge(q[l - 1].id, p[i].id, getdis(p[i], q[l - 1]));
        }
        if (r + 1 <= m - 1)
        {
            add_edge(p[i].id, q[r + 1].id, getdis(p[i], q[r + 1]));
            add_edge(q[r + 1].id, p[i].id, getdis(p[i], q[r + 1]));
        }
    }
    printf("%.3f", kruskal());
    return 0;
}
```



## Others

#### 递归

[校题](https://vjudge.csgrandeur.cn/contest/528411#overview)

```c++
#include <iostream>
#include <cstdio>
#include <vector>
#include <iomanip>
#include <cstring>
#include <algorithm>
#include <cmath>
using namespace std;

//斐波那契数列

int Fib(int a)
{
    int arr[30] = {0, 1, 1, 2, 3, 5};
    if(a == 1 || a == 2)    return arr[a];
    else if(arr[a - 1] != 0 && arr[a - 2] != 0)  return arr[a - 2] + arr[a - 1];    
    else   return Fib(a - 1) + Fib(a - 2);
}

int main()
{
    int n, a;
    cin >> n;
    while(n--)
    {
        cin >> a;
        cout << Fib(a) << endl;
    }
    return 0;
}

//Pell数列
 
int arr[1000001] = {0, 1, 2};

int Pell(int k)
{
    if(arr[k] != 0) return arr[k];
    return arr[k] = (2 * Pell(k - 1) + Pell(k - 2)) % 32767;   
}

int main()
{
    int n, k;
    cin >> n;
    for(int i = 1; i <= 1000000; i++)    Pell(i);
    while(n--)
    {
        cin >> k;
        cout << arr[k] << endl;
    }
    return 0;
}

//阶乘
int Fact(int n)
{
    int sum = 1;
    for(int i = 1; i <= n; i++) sum *= i;
    return sum;
}
int main()
{
    int n;
    cin >> n;
    cout << Fact(n) << endl;
    return 0;
}

//爬楼梯
int lib[40] = {0, 1, 2};
int Stairs(int i)
{
    if(lib[i] != 0) return lib[i];
    else return lib[i] = lib[i - 1] + lib[i - 2];
}
int main()
{
    int n;
    for(int i = 1; i <= 30; i++)    Stairs(i);
    while(scanf("%d", &n) != EOF)
        cout << lib[n] << endl;
    return 0;
}


//Function Run Fun
int lib[21][21][21];

int w(int a, int b, int c)
{
    if (a <= 0 || b <= 0 || c <= 0)
        return 1;
    else if (a > 20 || b > 20 || c > 20)
        return w(20, 20, 20);
    else if(lib[a][b][c])  //记录数据，减少运行时间 
        return lib[a][b][c];
    else if (a < b && b < c)
        return lib[a][b][c] = w(a, b, c - 1) + w(a, b - 1, c - 1) - w(a, b - 1, c);
    else
        return lib[a][b][c] = w(a - 1, b, c) + w(a - 1, b - 1, c) + w(a - 1, b, c - 1) - w(a - 1, b - 1, c - 1);
}

int main()
{
    int a, b, c;
    while (1)
    {
        cin >> a >> b >> c;
        if (a == b && b == c && a == -1)
            break;
        printf("w(%d, %d, %d) = %d\n", a, b, c, w(a, b, c));
    }
    return 0;
}

//The Triangle
int main()
{
    int arr[105][105];
    int lib[105][105];
    memset(arr, 0, sizeof(arr));
    memset(lib, 0, sizeof(lib));
    int n, maxnum = 0;
    cin >> n;
    for(int i = 1; i <= n; i++)
        for(int j = 1; j <= i; j++)
        {
            cin >> arr[i][j];
            lib[i][j] = max(lib[i - 1][j], lib[i - 1][j - 1]) + arr[i][j];
            if(lib[i][j] > maxnum)  maxnum = lib[i][j];
        }
    cout << maxnum << endl;
    return 0;
}

//分解因数
int Devide(int a, int k)
{
    int cnt = 1;
    for(int i = k; i <= sqrt(a); i++)
    {
        if(a % i == 0)  
        {
            cnt += Devide(a / i, i);
        }
    }
    return cnt;
}

int main()
{
    int n, a;
    cin >> n;
    while(n--)
    {
        cin >> a;
        cout << Devide(a, 2) << endl;
    }
    return 0;
}

//算24
#define EPS 1e-6;

double a[5];
bool Iszero(double x)
{
    //浮点数比较不能用==
    return fabs(x) <= EPS;
}
bool count24(double a[], int n)
{
    if (n == 1)  
    {
        if (Iszero(a[0] - 24))   return true;
        else return false;
    }
    double b[5];
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
        {
            int m = 0;//计算剩余数个数
            for (int k = 0; k < n; k++)
            {
                //储存剩余的数
                if (k != j && k != i)   b[m++] = a[k];
            }
            //add
            b[m] = a[i] + a[j];
            if (count24(b, m + 1))  return true;
            //sub
            b[m] = a[i] - a[j];
            if (count24(b, m + 1))  return true;
            b[m] = a[j] - a[i];
            if (count24(b, m + 1))  return true;
            //mul
            b[m] = a[i] * a[j];
            if (count24(b, m + 1))  return true;
            //div
            if (!Iszero(a[i]))
            {
                b[m] = a[j] / a[i];
                if (count24(b, m + 1))  return true;
            }
            if (!Iszero(a[j]))
            {
                b[m] = a[i] / a[j];
                if (count24(b, m + 1))  return true;
            }
        }
    return false;
}
int main()
{
    while(true)
    {
        for (int i = 0; i < 4; i++)  cin >> a[i];
        if (Iszero(a[0]))    break;
        if (count24(a, 4))   cout << "YES" << endl;
        else cout << "NO" << endl;
    }
    return 0;
}

//Placing apple
int lib[20][20];
int Placing(int m, int n)
{
    if (lib[m][n])   return lib[m][n];
    else
    {
        if (m == 0 || n == 1)   return lib[m][n] = 1;
        else if (n > m)    return lib[m][n] = Placing(m, m);
        else    return lib[m][n] = Placing(m - n, n) + Placing(m, n - 1);
    }
}
int main()
{
    int t;
    cin >> t;
    while(t--)
    {
        int m, n;
        cin >> m >> n;
        cout << Placing(m, n) << endl;
    }
    return 0;
}

//Tower of Hanoi
int n;
char a[2], b[2], c[2];
void Move(int n, int a, int c){printf("%d:%c->%c\n", n, a, c);}
void DFS(int n, int a, int b, int c)
{
    if(n == 1)
    {
        Move(n, a, c);
        return;
    }
    DFS(n - 1, a, c, b);
    Move(n, a, c);
    DFS(n - 1, b, a, c);
}
int main()
{
    while(scanf("%d%s%s%s", &n, a, b, c) != EOF)
        DFS(n, a[0], b[0], c[0]);
    return 0;
}

//The Sierpinski Fractal
char base[2][5] = {
    " /\\",
    "/__\\"
};
char buf[1500][2500];
void DFS(int sz, int y, int x)
{
    if (sz == 2)
    {
        for(int i = y, ii = 0; ii < 2; i++, ii++)
            for(int j = x, jj = 0; jj < 4; j++, jj++)
                buf[i][j] = base[ii][jj];
        return;
    }
    DFS(sz >> 1, y, x + (sz >> 1));
    DFS(sz >> 1, y + (sz >> 1), x);
    DFS(sz >> 1, y + (sz >> 1), x + sz);
}
int main()
{
    int n;
    while(cin >> n && n)
    {
        memset(buf, 0, sizeof(buf));
        int sz = (int)(pow(2.0, n) + 1e-8);
        DFS(sz, 0, 0);
        for(int i = 0; i < sz; i++)
        {
            int j = sz << 1;
            for(; !buf[i][j]; j--);
            for(int k = 0; k <= j; k++)
                printf("%c", buf[i][k] ? buf[i][k] : ' ');
            printf("\n");
        }
        printf("\n");
    }
    return 0;
}
```
