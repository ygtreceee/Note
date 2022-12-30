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

#### 搜索剪枝

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
       a[i] = a[i - 1] + a[i];
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



#### 二分， 三分

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
	else r = mid + 1;
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

#### 单调栈

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



#### 单调队列

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



#### 双指针（尺取）

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



#### 数论分块

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

#### 分治

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

```
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

#### 动态规划

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
int w[maxn][maxn], c[maxn][maxn];
int dp[maxn];
int n, m;
int main()
{
    while (cin >> n >> m && n && m)
    {
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= m; j++)
            {
                cin >> w[i][j];
                c[i][j] = j;  //第i组第j个物品的体积，学j天才能得分，体积就是j
            }
        memset(dp, 0, sizeof dp);
        for (int i = 1; i <= n; i++)
            for (int j = m; j >= 0; j--)
                for (int k = 1; k <= m; k++)   //用k遍历第i组的所有物品
                    if (j >= c[i][k])
                        dp[j] = max(dp[j], dp[j - c[i][k]] + w[i][k]);  //第i组第k个
        cout << dp[m] << endl; 
    }
    return 0;
}
```

luogu P1776 宝物筛选

多重背包问题，可使用简单方法，或者二进制拆分优化，或者单调队列优化

```c++
//简单方法
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

//二进制拆分优化
#include <algorithm>
#include <iostream>
using namespace std;
const int maxn = 1e5 + 10;
int w[maxn], c[maxn], m[maxn];
int new_w[maxn], new_c[maxn], new_m[maxn];  //二进制拆分后的新物品
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

