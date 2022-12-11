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

原理

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

洛谷

```c++
//P7441 「EZEC-7」Erinnerung
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

vjudge

```c++
//跳石头
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


//Cable master
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
	printf("%.2f", floor(mid * 100) / 100);
	return 0;
}


//Freefall
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


//Last Rook
//
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


//Pie
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


//Monthly Expense
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

