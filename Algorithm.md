## Algorithm

#### 动态规划

[最长上升子序列(LIS)](https://vjudge.csgrandeur.cn/problem/OpenJ_Bailian-2757)	[Anlysis](https://blog.csdn.net/lxt_Lucia/article/details/81206439?ops_request_misc=%7B%22request%5Fid%22%3A%22166623480216800182771794%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=166623480216800182771794&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-2-81206439-null-null.142^v59^control_1,201^v3^control_2&utm_term=最长上升子序列&spm=1018.2226.3001.4187)

```c++
#include <iostream>
#include <cstdio>
#include <vector>
#include <iomanip>
#include <cstring>
#include <algorithm>
#include <cmath>
using namespace std;

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
```



#### 中国剩余定理

[Biorhythms](https://vjudge.csgrandeur.cn/problem/OpenJ_Bailian-1006)	[Analysis](https://www.cnblogs.com/MashiroSky/p/5918158.html)

#### DFS

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
#include <algorithm>
#include <cstring>
using namespace std;
int m, n;
char buf[110][110];
bool flag[110][110];
int step[8][2] = {{-1, 1}, {0, 1}, {1, 1}, {1, 0}, {1, -1}, {0, -1}, {-1, -1}, {-1, 0}};
void DFS(int x, int y)
{
    for (int i = 0; i < 8; i++)
    {
        int nx = x + step[i][0], ny = y + step[i][1];
        if (nx >= 0 && nx < m && ny >= 0 && ny < n && !flag[nx][ny] && buf[nx][ny] == '@')
        {
            flag[nx][ny] = true;
            DFS(nx, ny);
        }
    }
    return;
}
int main()
{
    int cnt;
    while(cin >> m >> n && n)
    {
        cnt = 0;
        memset(flag, 0, sizeof(flag));
        for (int i = 0; i < m; i++)    cin >> buf[i];
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++)
            {
                if (!flag[i][j] && buf[i][j] == '@')
                {
                    flag[i][j] = true;
                    DFS(i, j);
                    cnt++;
                }
            }
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



#### BFS

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
int flag[100005], step[100005]; //flag标记走过的坐标，避免重复；step记录到达每一个坐标需要的步数
int BFS(int p, int k)
{
    queue<int> que;
    que.push(p);
    flag[p] = 1;
    step[p] = 0;
    if (p >= k)  return p - k; //农民在奶牛前面，只能后退
    while (!que.empty())
    {
        int n = que.front();
        que.pop();
        if (n == k)   return step[n]; //结束
        else
        {
            if (!flag[n - 1] && n - 1 >= 0 && n - 1 <= 100000)
            {
                que.push(n - 1);
                step[n - 1] = step[n] + 1;
                flag[n - 1] = 1;
            }
            if (!flag[n + 1] && n + 1 >= 0 && n + 1 <= 100000)
            {
                que.push(n + 1);
                step[n + 1] = step[n] + 1;
                flag[n + 1] = 1;
            }
            if (!flag[n * 2] && n * 2 >= 0 && n * 2 <= 100000)
            {
                que.push(n * 2);
                step[n * 2] = step[n] + 1;
                flag[n * 2] = 1;
            }
        }
    }
    return 0;
}
int main()
{
    int p, k;
    while (cin >> p >> k)   
    {
        memset(flag, 0, sizeof flag); //初始化
        memset(step, 0, sizeof step);
        cout << BFS(p, k) << endl;
    }
    return 0;
}


//Prime Path
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


//迷宫问题
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
#include <string>
using namespace std;
int road[5][5];
int flag[10][10];
struct point
{
    int x;
    int y;
} Point[10][10];
int goo[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
void BFS()
{
    queue<point> que;
    point s;
    s.x = 0; s.y = 0;
    que.push(s);
    flag[0][0] = 1;
    while (!que.empty())
    {
        point p = que.front();
        que.pop();
        if (p.x == 4 && p.y == 4)  return;
        for (int i = 0; i < 4; i++)
        {
            int ax = p.x + goo[i][0];
            int ay = p.y + goo[i][1];
            if (!road[ax][ay] && !flag[ax][ay] && ax >= 0 && ax < 5 && ay >= 0 && ay < 5)
            {
                point t;
                t.x = ax;
                t.y = ay;
                que.push(t);
                flag[ax][ay] = 1;
                Point[ax][ay] = p;
            }
        }
    }
}
void output(point p)
{
    if (!p.x && !p.y)
    {
        cout << "(0, 0)" << endl;
        return;
    }
    output(Point[p.x][p.y]);
    cout << "(" << p.x << ", " << p.y << ")" << endl;
}
int main()
{
    for (int i = 0; i < 5; i++)
        for (int j = 0; j < 5; j++)
            cin >> road[i][j];
    BFS();
    point end;
    end.x = 4;
    end.y = 4;
    output(end);
    return 0;
}


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
```

#### 回溯与剪枝

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
```

#### IDA *

```

```



#### 贪心算法

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

