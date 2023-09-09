#### OJ

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

//简化的插入排序
int main()
{
    int n, num, flag = 0, ret;
    scanf("%d", &n);
    int arr[100];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    scanf("%d", &num);
    for (int i = 0; i < n; i++)
    {
        if (!flag && arr[i] > num)  printf("%d " + flag++, num);
        printf("%d ", arr[i]);
        if (i == n - 1 && !flag)    printf("%d ", num); 
    }
    return 0;
}

//交换最小值和最大值
int main()
{
    int n, ret;
    scanf("%d", &n);
    int arr[100];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    int min = 0, max = 0;
    for (int i = 0; i < n; i++) min = arr[i]<arr[min]?i:min;
    ret = arr[0];
    arr[0] = arr[min];
    arr[min] = ret;
    for (int i = 0; i < n; i++) max = arr[i]>arr[max]?i:max;   
    ret = arr[n - 1];
    arr[n - 1] = arr[max];
    arr[max] = ret;
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    return 0;
}

//求一批整数中出现最多的各位数字
int main()
{
    int n, ret, max = 0;
    char num[10] = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9'};
    int buf[10] = {0};
    char ch[20];
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {   
        scanf("%s", ch);
        for (int k = 0; ch[k] != '\0'; k++)
            for (int j = 0; j < 10; j++)
                if (num[j] == ch[k])   buf[j]++;
    }
    for (int i = 0; i < 10; i++)    max = buf[i]>buf[max]?i:max;
    printf("%d:", buf[max]);
    for (int i = 0; i < 10; i++)    if (buf[i] == buf[max]) printf(" %c", num[i]);
    return 0;   
}

//找出不是两个数组共有的元素
#include <stdio.h>
#include <string.h>
int main()
{
    int a, b, aarr[2][100], barr[2][100], flag = 0;
    memset(aarr, 0, sizeof(aarr));
    memset(barr, 0, sizeof(barr));
    scanf("%d", &a);
    for (int i = 0; i < a; i++) scanf("%d", &aarr[0][i]);
    scanf("%d", &b);
    for (int i = 0; i < b; i++) scanf("%d", &barr[0][i]);
    for (int i = 0; i < a; i++)
    {
        for (int j = 0; j < b; j++)
                if (aarr[0][i] == barr[0][j])
                {
                    aarr[1][i] = 1;
                    barr[1][j] = 1;
                }
    }
    for (int i = 0; i < a; i++) 
    {
        for (int j = i + 1; j < a; j++)
            if (aarr[0][i] == aarr[0][j])  aarr[1][j] = 1;
    }
    for (int i = 0; i < b; i++) 
    {
        for (int j = i + 1; j < b; j++)
            if (barr[0][i] == barr[0][j])  barr[1][j] = 1;
    }
    for (int i = 0; i < a; i++) 
    {
        if (!aarr[1][i])  
        {
            printf(" %d" + !flag, aarr[0][i]);
            flag = 1;
        }
    }
    for (int i = 0; i < b; i++)
    {
        if (!barr[1][i])  
        {
            printf(" %d" + !flag, barr[0][i]);
            flag = 1;
        }
    }
    return 0;
}

//求整数序列中出现次数最多的数
int main()
{
    int n, a, cnt = 0, max = 0, arr[2][1500];
    memset(arr, 0, sizeof(arr));
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        int flag = 1;
        scanf("%d", &a);
        for (int j = 0; j < cnt; j++)
        {
            if (arr[0][j] == a) 
            {
                arr[1][j]++;
                flag = 0;
                break;
            }
        }
        if (flag == 1)  
        {
            arr[1][cnt] = 1;
            arr[0][cnt++] = a;
        }
    }
    for (int i = 0; i < cnt; i++)
        max = arr[1][i]>arr[1][max]?i:max;
    printf("%d %d", arr[0][max], arr[1][max]);
    return 0;
}

//奖金提成
double Awd(int mon)
{
    double sum;
    switch(mon/10000)
    {
        case 0: sum = mon * 0.1;
                break;
        case 1: sum = 10000 * 0.1 + (mon - 10000) *0.075;
                break;
        case 2:
        case 3: sum = 10000 * 0.1 + 10000 * 0.075 + (mon - 20000) * 0.05;
                break;
        case 4: 
        case 5: sum = 10000 * 0.1 + 10000 * 0.075 + 20000 * 0.05 + (mon - 40000) * 0.03;
                break;
        case 6:
        case 7:
        case 8:
        case 9: sum = 10000 * 0.1 + 10000 * 0.075 + 20000 * 0.05 + 20000 * 0.03 + (mon - 60000) * 0.015;
                break;
        default:
                sum = 10000 * 0.1 + 10000 * 0.075 + 20000 * 0.05 + 20000 * 0.03 + 40000 * 0.015 + (mon - 100000) * 0.01;
                break;
    }
    return sum;
}
int main()
{
    int t, mon;
    scanf("%d", &t);
    while (t--)
    {
        scanf("%d", &mon);
        printf("%0.lf\n", Awd(mon));
    }
    return 0;
}

//扫雪挑战
int buf[1000100] = {0};
int main()
{
    int len, t, cnt = 0;
    scanf("%d %d", &len, &t);
    while (t--)
    {
        int m, n;
        scanf("%d %d", &m, &n);
        for (int i = m; i <= n; i++) buf[i] = 1;
    }
    for (int i = 1; i <= len; i++)   if (!buf[i]) cnt++;
    printf("%d", cnt);
    return 0;
}

//判断上三角矩阵
#include <stdio.h>
#include <string.h>
int Judge(int a[15][15], int m)
{
    for (int i = 0; i < m; i++)
        for (int j = 0; j < i; j++)
            if (a[i][j]) return 0;
    return 1;
}
int main()
{
    int t, m, a[15][15];
    scanf("%d", &t);
    while (t--)
    {
        scanf("%d", &m);
        for (int i = 0; i < m; i++)
            for (int j = 0; j < m; j++)
                scanf("%d", &a[i][j]);
        if(Judge(a, m)) printf("YES\n");
        else printf("NO\n");
    }
    return 0;
}

//打印杨辉三角
#include <stdio.h>
#include <string.h>
void set(int a[20][20])
{
    a[0][0] = 1;
    for (int i = 1; i < 20; i++)
        for (int j = 0; j <= i; j++) 
            a[i][j] = a[i - 1][j] +  a[i - 1][j - 1];
}
int main()
{
    int a[20][20] = {0};
    int n;
    set(a);
    scanf("%d", &n);
    for (int i = 1; i <= n; i++)
    {
        for (int j = n - i; j > 0; j--) printf(" ");
        for (int j = 1; j <= i; j++) printf("%4.d", a[i - 1][j - 1]);
        printf("\n");
    }
    return 0;
}

//方阵循环右移
#include <stdio.h>
#include <string.h>
int n, m, tmp, a[10][10];
void action()
{
    for (int i = 0; i < m; i++)
        for (int k = 0; k < n; k++)
            {
                tmp = a[i][m - 1];
                for (int j = m - 1; j >= 0; j--)
                    a[i][j] = a[i][j - 1];
                a[i][0] = tmp;
            }
}
int main()
{
    scanf("%d %d", &n, &m);
    for (int i = 0; i < m; i++)
        for (int j = 0; j < m; j++)
            scanf("%d", &a[i][j]);
    action();
    for (int i = 0; i < m; i++)
    {
        for (int j = 0; j < m; j++)
            printf("%d ", a[i][j]);
        printf("\n");
    }
    return 0;
}

//找鞍点
#include <stdio.h>
#include <string.h>
int n, max, ret, a[10][10], flag = 1, ffl = 0;
int main()
{
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            scanf("%d", &a[i][j]);
    for (int i = 0; i < n; i++)
    {
        max = 0;
        flag = 1;
        for (int j = 0; j < n; j++) 
        {
            if (a[i][j] > max)
            {
                max = a[i][j];
                ret = j;
            }
        }
        for (int j = 0; j < n; j++)
        {
            if (a[j][ret] < max)
            {
                flag = 0;
                break;
            }
        }
        if (flag)
        {
            ffl = 1;
            printf("%d %d", i, ret);
            break;
        }
        if (!ffl && i == n - 1) printf("NONE");
    }
}

//螺旋方阵
#include <stdio.h>
#include <string.h>
int main()
{
    int n, num = 1, a[15][15];
    scanf("%d", &n);
    for (int i = 1; i <= n; i++) //n = 5 
    {
        for (int j = i; j <= n + 1 - i; j++) a[i][j] = num++;
        for (int j = i + 1; j <= n + 1 - (i + 1); j++) a[j][n + 1 - i] = num++;
        if (n % 2 == 1 && i == n - n/2) break;
        for (int j = n + 1 - i; j >= i; j--) a[n + 1 - i][j] = num++;
        for (int j = n + 1 - (i + 1); j >= i + 1; j--) a[j][i] = num++;
    }
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
            printf("%3.d", a[i][j]);
        printf("\n");
    }
    return 0;
}

//简易连连看
#include <stdio.h>
#include <string.h>
char room[15][15];
int n, m, x1, x2, y1, y2, cnt = 0, flag = 1, ffl = 0;
void print()
{
    for (int i = 1; i <= 2 * n; i++)
        for (int j = 1; j <= 2 * n; j++)
            if (room[i][j] != '*') 
            {
                flag = 0;
                break;
            }
    if (flag)
    {
        printf("Congratulations!\n");
        ffl = 1;
        return;
    }
    for (int i = 1; i <= 2 * n; i++)
    {
        for (int j = 1; j <= 2 * n; j++) printf(" %c" + !(j - 1), room[i][j]);
        printf("\n");
    }      
}
int main()
{
    scanf("%d", &n);
    getchar();
    for (int i = 1; i <= 2 * n; i++)
        for (int j = 1; j <= 2 * n; j++)
        {
            scanf("%c", &room[i][j]);
            getchar();
        }
    scanf("%d", &m);
    while (m--)
    {
        scanf("%d %d %d %d", &x1, &y1, &x2, &y2);
        flag = 1;
        if (ffl) break;
        if (cnt == 3)
        {
            printf("Game Over\n");
            break;
        }
        if (room[x1][y1] == room[x2][y2] && room[x1][y1] != '*')
        {
            room[x1][y1] = room[x2][y2] = '*';
            print();
        }
        else if (cnt < 4 && (room[x1][y1] != room[x2][y2] || room[x1][y1] == '*'))
        {
            printf("Uh-oh\n");
            cnt++;
        }
    }
    return 0;
}

//单月的日历
#include <stdio.h>
#include <string.h>
int main()
{
    int n, m;
    scanf("%d %d", &n, &m);
    int cnt = m - 1;
    for (int j = 1; j < m; j++) printf("   " + !(j - 1));
    for (int i = 1; i <= n; i++)
    {
        printf(" %2.d" + !cnt, i);
        cnt++;
        if (cnt == 7)
        {
            printf("\n");
            cnt = 0;
        }
    }
    return 0;
}


//英文字母替换加密
#include <stdio.h>
#include <string.h>
char words[10000];
int main()
{
    gets(words);
    for (int i = 0; words[i] != '\0'; i++)
    {
        char a = words[i];
        if (a >= 'a' && a < 'z')
            words[i] = a - 31;
        if (a >= 'A' && a < 'Z')
            words[i] = a + 33;
        if (a == 'z') words[i] = 'A';
        if (a == 'Z') words[i] = 'a';
    }
    printf("%s", words);
    return 0;
}


//近似求PI
#include <stdio.h>
#include <string.h>
int main()
{
    double eps;
    scanf("%le", &eps);
    double sum=1;
    double temp=1;
    for(int i=1;temp>=eps;i++)
	{
        temp = temp*i/(2*i+1);
        sum += temp;
    }
    printf("PI = %.5f\n", 2*sum);
    return 0;
}


//简单计算器
#include <stdio.h>
#include <string.h>
int main()
{
    int a, b, flag = 1;
    char c;
    scanf("%d%c", &a, &c);
    int res = a;
    while (c != '=')
    {
        scanf("%d", &b);
        if (c == '/' && b == 0)
        {
            printf("ERROR\n");
            flag = 0;
            break;
        }
        switch(c)
        {
            case '+': res += b;
            break;
            case '-': res -= b;
            break;
            case '*': res *= b;
            break;
            case '/': res /= b;
            break;
            default: printf("ERROR\n");
                     flag = 0;
        }
        if (!flag) break;
        scanf("%c", &c);
    }
    if (flag) printf("%d", res);
    return 0;
}


//单词首字母大写
#include <stdio.h>
#include <string.h>
char words[10000];
int main()
{
    gets(words);
    for (int i = 0; words[i] != '\0'; i++)
    {
        if (i == 0 && words[i] != ' ' && words[i] >= 'a' && words[i] <= 'z')
            words[i] -= 32;
        if (words[i] == ' ' && words[i + 1] != ' ' && words[i + 1] >= 'a' && words[i + 1] <= 'z')
            words[i + 1] -= 32;
    }
    printf("%s", words);
    return 0;
}


//统计单词的长度
#include <stdio.h>
#include <string.h>
char words[10000];
int main()
{
    char a;
    int cnt = 0, flag = 1;
    while (1)
    {
        scanf("%c", &a);
        if (a != ' ' && a!= '\n')
        {
            flag = 1;
            cnt++;
        }
        if (a == ' ' || a == '\n')
        {
            if (flag) printf("%d ", cnt);
            cnt = 0;
            flag = 0;
        }
        if (a == '\n') break;
    }
    return 0;
}


//使用函数输出水仙花数
#include <stdio.h>
#include <string.h>
#include <math.h>
int m, n;
int Judge(int i)
{
    int tmp = i, sum = 0, cnt = 0;
    while (tmp)
    {
        cnt++;
        tmp /= 10;
    }
    tmp = i;
    while (tmp)
    {
        int ret = tmp % 10;
        sum += pow(ret, cnt);
        tmp /= 10;
    }
    if (sum == i) return 1;
    else return 0;
}
int main()
{
    scanf("%d %d", &m, &n);
    for (int i = m + 1; i < n; i++)
        if (Judge(i)) printf("%d\n", i);
    return 0;
}


//转化数为英文单词
#include <stdio.h>
#include <string.h>
#include <math.h>
int main()
{
    int a;
    scanf("%d", &a);
    if (a > 99 || a < 10)
    {
        printf("Illegal number!");
        a = 0;
    }
    switch (a / 10)
    {
    case 2:
        printf("twenty");
        break;
    case 3:
        printf("thirty");
        break;
    case 4:
        printf("forty");
        break;
    case 5:
        printf("fifty");
        break;
    case 6:
        printf("sixty");
        break;
    case 7:
        printf("seventy");
        break;
    case 8:
        printf("eighty");
        break;
    case 9:
        printf("ninety");
    }
    if (a / 10 != 1)
    {
        switch (a % 10)
        {
        case 1:
            printf("-one");
            break;
        case 2:
            printf("-two");
            break;
        case 3:
            printf("-three");
            break;
        case 4:
            printf("-four");
            break;
        case 5:
            printf("-five");
            break;
        case 6:
            printf("-six");
            break;
        case 7:
            printf("-seven");
            break;
        case 8:
            printf("-eight");
            break;
        case 9:
            printf("-nine");
        }
    }
    if (a / 10 == 1)
    {
        switch (a % 10)
        {
        case 0:
            printf("ten");
            break;
        case 1:
            printf("eleven");
            break;
        case 2:
            printf("twelve");
            break;
        case 3:
            printf("thirteen");
            break;
        case 4:
            printf("fourteen");
            break;
        case 5:
            printf("fifteen");
            break;
        case 6:
            printf("sixteen");
            break;
        case 7:
            printf("seventeen");
            break;
        case 8:
            printf("eighteen");
            break;
        case 9:
            printf("nineteen");
        }
    }
    return 0;
}


//碰撞检测
#include <stdio.h>
#include <string.h>
#include <math.h>
int main()
{
    int t, x1, x2, x3, x4, y1, y2, y3, y4, flag = 0;
    for (scanf("%d", &t); t--; )
    {
        flag = 0;
        scanf("%d%d%d%d", &x1, &y1, &x2, &y2);
        scanf("%d%d%d%d", &x3, &y3, &x4, &y4);
        int col = x2 - x1 + x4 - x3;
        int row = y2 - y1 + y4 - y3;
        if (col >= x4 - x1 && row >= y4 - y1)
            flag = 1;
        printf(flag ? "YES\n" : "NO\n");
    }
    return 0;
}


//字符串逆序
#include <stdio.h>
#include <string.h>
int main()
{
    char words[100];
    gets(words);
    for (int i = strlen(words) - 1; i >= 0; i--)
        printf("%c", words[i]);
    return 0;
}


//查找指定字符
#include <stdio.h>
#include <string.h>
int main()
{
    char words[100], k;
    scanf("%c", &k);
    getchar();
    gets(words);
    for (int i = strlen(words) - 1; i >= 0; i--)
    {
        if (words[i] == k)
        {
            printf("index = %d", i);
            break;
        }
        if (i == 0) printf("Not Found");
    }
    return 0;
}


//凯撒密码
#include <stdio.h>
#include <string.h>
int main()
{
    char words[100];
    gets(words);
    int a;
    scanf("%d", &a);
    for (int i = 0; i < strlen(words); i++)
    {
        char ret = words[i];
        if (ret >= 'A' && ret <= 'Z' && a >= 0) words[i] = 64 + (words[i] - 64 + a) % 26;
        if (ret >= 'a' && ret <= 'z' && a >= 0) words[i] = 96 + (words[i] - 96 + a) % 26;
        if (ret >= 'A' && ret <= 'Z' && a < 0)
        {
            if ((91 - words[i] - a) == 26) words[i] = 91 -26;
            else words[i] = 91 - (91 - words[i] - a) % 26;
        }
        if (ret >= 'a' && ret <= 'z' && a < 0)
        {
            if((123 - words[i] - a) == 26) words[i] = 123 -26;
            else words[i] = 123 - (123 - words[i] - a) % 26;
        }
        printf("%c", words[i]);
    }
    return 0;
}


//字符串转换成十进制整数
#include <stdio.h>
#include <string.h>
#include <math.h>
int main()
{
    char words[100], room[100] = {0};
    int cnt = 0, flag = 1, ans = 0;
    gets(words);
    for (int i = 0; words[i] != '#'; i++)
    {
        if (words[i] == '-' && !cnt) flag = 0;
        if ((words[i] >= '0' && words[i] <= '9'))  
            room[cnt++] = words[i] - 48;
        if (words[i] >= 'A' && words[i] <= 'F')
            room[cnt++] = words[i] - 55;
        if (words[i] >= 'a' && words[i] <= 'f')
            room[cnt++] = words[i] - 87;
    }
    for (int i = 0; i < cnt; i++)
        ans += room[i] * pow(16, (cnt - i - 1));
    printf("-%d" + flag, ans);
    return 0;
}


//输出大写英文字母
#include <stdio.h>
#include <string.h>
#include <math.h>
int main()
{
    char words[100];
    gets(words);
    char vis[100] = {0};
    for (int i = 0; i < strlen(words); i++)
    {
        if (words[i] >= 'A' && words[i] <= 'Z' && !vis[words[i]])
            vis[words[i]] = 1, printf("%c", words[i]);
    }
    for (int i = 0; i < 100; i++)
    {
        if (vis[i]) break;
        if (i == 99) printf("Not Found");
    }
    return 0;
}


//删除重复字符
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>
int cmp(const void *a, const void *b)
{
    return *(char *)a - *(char *)b;
}
int main()
{
    char words[100];
    char room[100];
    int cnt = 0;
    gets(words);
    char vis[200] = {0};
    for (int i = 0; i < strlen(words); i++)
    {
        if (!vis[words[i]]) room[cnt++] = words[i];
        vis[words[i]] = 1;
    }
    qsort(room, cnt, sizeof(char), cmp);
    for (int i = 0; i < cnt; i++) printf("%c", room[i]);
    return 0;
}
```

23.4.7

总结

```c++
class Point
{
private:
	//
public:
	//
};
```

题目代码

```c++
//A
#include <bits/stdc++.h>
using namesapce std;
int n;
class student
{
	public:
	void init()
	{
		cin >> name >> id >> sex >> fr >> phn;
	}
	void print()
	{
		cout << name << endl;
	}
	private:
		char name[100], sex[100], fr[100];
		long long id, phn;
};
int main()
{
	cin >> n;
	student *p = (student*)malloc(sizeof (student) * n);
	for (int i = 0; i < n; i++)
	{
		p[i].init();
	}
	for (int i = 0; i < n; i++)
	{
		p[i].print();
	}
	free(p);
	p = NULL;
	return 0;
}


//B
#include <bits/stdc++.h>
using namesapce std;
class CAccount
{
	public:
		void init()
		{
			cin >> id >> name >> mon;
			printf("%s's balance is %d\n", name, mon);
		}
		void save()
		{
			cout << "saving ok!" << endl;
			long long x; cin >> x;
			mon += x;
			printf("%s's balance is %d\n", name, mon);
		}
		void withdraw()
		{
			long long x; cin >> x;
			if (x > mon)
			{
				printf("sorry! over limit!\n");
				printf("%s's balance is %d\n", name, mon);
			}
			else
			{
				printf("withdraw ok!\n");
				mon -= x;
				printf("%s's balance is %d\n", name, mon);
			}
		}
	private:
		char id[100], name[100];
		long long mon;
};
int main()
{
	CAccount ca[2];
	for (int i = 0; i < 2; i++)
	{
		ca[i].init();
		ca[i].save();
		ca[i].withdraw();
	}
	return 0;
}


//C
#include <bits/stdc++.h>
using namespace std;
class Point
{
	public:
		void setPoint();
		double getx() {return x;}
		double gety() {return y;}
	private:
		double x, y;
};
void Point::setPoint() {cin >> x >> y;}
class Circle
{
	public:
		void setCircle();
		double getArea();
		double getLength();
		void check(double px, double py);
	private:
		double x, y, r;
};
void Circle::setCircle() {cin >> x >> y >> r;}
double Circle::getArea() {cout << fixed << setprecision(2) << 3.14 * r * r;}
double Circle::getLength() {cout << fixed << setprecision(2) << 2 * 3.14 * r;}
void Circle::check(double px, double py) {cout << (sqrt((px - x) * (px - x) + (py - y) * (py - y)) <= r ? "yes" : "no") << endl; }
int main()
{
	Point p; Circle c;
	c.setCircle(); p.setPoint(); 
	c.getArea(); cout << ' '; c.getLength(); cout << endl;
	c.check(p.getx(), p.gety());
	return 0;
}


//D
#include <bits/stdc++.h>
using namesapce std;
struct Cat
{
	public:
		void init()
		{
			cin >> name >> w;
		}
		bool operator < (const Cat &x) const
		{
			return w < x.w;
		}
		void getname()
		{
			cout << name;
		}
	private:
		char name[1000];
		int w;
};
int main()
{
	int n; cin >> n;
	Cat *p = (Cat *)malloc(sizeof (Cat) * n);
	for (int i = 0; i < n; i++) p[i].init();
	sort(p, p + n);
	for (int i = 0; i < n; i++)
	{
		if (i) cout << ' ';
		p[i].getname();
	}
	return 0;
}


//E
#include <bits/stdc++.h>
using namesapce std;
struct man
{
	public:
		void init() {cin >> name >> h >> we >> wr;}
		void solve()
		{
			int bmi = int(we / (h * h) + 0.5);
			double a = wr * 0.74, b = we * 0.082 + 34.89;
			double r = (a - b) / we;
			printf("%s的BMI指数为%d--体脂率为%.2f", name, bmi, r); 
			cout << '\n';
		}
	private:
		char name[100];
		double h, we, wr;
};
int main()
{
	int n; cin >> n;
	man *p = (man *)malloc(sizeof(man) * n);
	for (int i = 0; i < n; i++)
	{
		p[i].init(); p[i].solve();
	}
	free(p);
	p = NULL;
	return 0;
}

```
23.4.14

总结

```c++
构造函数和析构函数
//特别注意operator new和operator delete的使用, 以及与new (&p[i])的结合使用
//关于动态开辟mallac, new和构造函数, 析构函数的本质联系参见Notecpp.md文档
class Point
{
private:
	int a, b;
public:
	Point() : a(0), b(0) {};              //成员函数默认赋值为0
	Point(int _a, int _b) : a(_a), b(_b); //传参构造函数
	~Point() {};
};
int main()
{
    int n; cin >> n;
    Point *p = (Point *)operator new[](n * sizeof(Point));  //动态开辟, 在此处不会引用构造函数, 因为operator new本质是malloc
    for (int i = 0; i < n; i++)
    {
        int x, y;
        cin >> x >> y;
        new (&p[i]) Point(x, y);  //构造对象, 在此处才会引用构造函数
	}
    //
    for (int i = 0; i < n; i++)
		p[i].~point();  //析构对象
   operator delete(p);  //释放空间, 在此处也不会调用析构函数, 因为operator delete本质是free
}



this的使用
this在一个成员函数中可以表示该成员
Point::Point(const Point &x)
{
    *this = x;
};
//
Point::set_value(int _a, int _b)
{
    this->a = _a;
    this->b = _b;
};
```

题目代码

```c++
//A
#include <bits/stdc++.h>
using namespace std;
class Point
{
    double x, y;
public:
    Point();
    Point(double x_value, double y_value);
    double getX();
    double getY();
    void setX(double x_value);
    void setY(double y_value);
    double getDisto(Point p);
};
Point::Point()
{
    this->x = 0;
    this->y = 0;
}
Point::Point(double x_value, double y_value)
{
    this->x = x_value;
    this->y = y_value;
}
double Point::getX()
{
    return x;
}
double Point::getY()
{
    return y;
}
void Point::setX(double x_value)
{
    this->x = x_value;
}
void Point::setY(double y_value)
{
    this->y = y_value;
}
double Point::getDistoo(Point p)
{
    return sqrt((x - p.x) * (x - p.x) + (y - p.y) * (y - p.y));
}
int main()
{
    int t; cin >> t;
    while (t--)
    {
        double _x1, _x2, _y1, _y2;
        cin >> _x1 >> _y1 >> _x2 >> _y2;
        Point p1(_x1, _y1), p2(_x2, _y2);
        printf("Distance of Point(%.2f,%.2f) to Point(%.2f,%.2f) is %.2f\n", p1.getX(), p1.getY(), p2.getX(), p2.getY(), p1.getDisto  o(p2));
    }
    return 0;
}



//B
#include <bits/stdc++.h>
using namespace std;
int mon[13] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
bool check(int x)
{
    if ((x % 4 == 0 && x % 100 != 0) || x % 400 == 0) return true;
    return false;
}
class Date
{
    int year, month, day;
public:
    Date();
    Date(int y, int m, int d);
    int getYear();
    int getMonth();
    int getDay();
    void setDate(int y, int m, int d);
    void print();
    void addOneday();
};
Date::Date()
{
    this->year = 1900;
    this->month = 1;
    this->day = 1;
}
Date::Date(int y, int m, int d)
{
    this->year = y;
    this->month = m;
    this->day = d;
}
int Date::getYear()
{
    return year;
}
int Date::getMonth()
{
    return month;
}
int Date::getDay()
{
    return day;
}
void Date::setDate(int y, int m, int d)
{
    this->year = y;
    this->month = m;
    this->day = d;
}
void Date::print()
{
    printf("Today is %0.2d/%0.2d/%0.2d\n", year, month, day);
    addOneday();
    printf("Tomorrow is %0.2d/%0.2d/%0.2d\n", year, month, day);
}
void Date::addOneday()
{
    day++;
    if (day > mon[month] && month != 2) month++, day = 1;
    else if (day > mon[month] && month == 2)
    {
        if (!check(year) || (check(year) && day == 30)) month++, day = 1;
    }
    if (month > 12)
    {
        year++;
        month = day = 1;
    }
}
int main()
{
    int t; cin >> t;
    while (t--)
    {
        int y, m, d; cin >> y >> m >> d;
        Date da(y, m, d);
        da.print();
    }
    return 0;
}



//C
#include <bits/stdc++.h>
using namespace std;
class CFraction
{
    int fz, fm;
public:
    CFraction(int fz_val, int fm_val);
    CFraction add(const CFraction& r);
    CFraction sub(const CFraction& r);
    CFraction mul(const CFraction& r);
    CFraction div(const CFraction& r);
    int getGCD();
    void print();
};
CFraction::CFraction(int fz_val, int fm_val)
{
    fz = fz_val;
    fm = fm_val;
}
CFraction CFraction::add(const CFraction& r)
{
    return CFraction(fz * r.fm + fm * r.fz, fm * r.fm);
}
CFraction CFraction::sub(const CFraction& r)
{
    return CFraction(fz * r.fm - fm * r.fz, fm * r.fm);
}
CFraction CFraction::mul(const CFraction& r)
{
    return CFraction(fz * r.fz, fm * r.fm);
}
CFraction CFraction::div(const CFraction& r)
{
    return CFraction(fz * r.fm,fm * r.fz);
}
int CFraction::getGCD()
{
    int r = fm;
    int a = fabs(fz), b = fabs(fm);
    while (a % b != 0)
    {
        r = a % b;
        a = b;
        b = r;
    }
    return b;
}
void CFraction::print()
{
    int gcd = getGCD();
    fz /= gcd;
    fm /= gcd;
    string signal;
    if (fz / fz == fm / fm)
        signal = "";
    else
        signal = "-";
    cout << signal << fz << "/" << fm << endl;
}
int main()
{
    int t; cin >> t;
    int fz1, fm1, fz2, fm2;
    char c;
    while (t--)
    {
        cin >> fz1 >> c >>  fm1 >> fz2 >> c >> fm2;
        CFraction cs1(fz1, fm1);
        CFraction cs2(fz2, fm2);
        CFraction cs3 = cs1.add(cs2);
        cs3.print();
        cs3 = cs1.sub(cs2);
        cs3.print();
        cs3 = cs1.mul(cs2);
        cs3.print();
        cs3 = cs1.div(cs2);
        cs3.print();
        cout << endl;
    }
    return 0;
}


//D
//特别注意构造方法和析构方法	
#include <bits/stdc++.h>
using namespace std;
class Point
{
private:
    double x, y;
public:
    Point() : x(0), y(0){};                                                                     //缺省构造函数
    Point(double x_val, double y_val) : x(x_val), y(y_val) { cout << "Constructor." << endl; }; //有参构造函数
    double getX() { return x; };
    double getY() { return y; };
    void setXY(double x_val, double y_val)
    {
        x = x_val;
        y = y_val;
    };
    void sexX(double x_val) { x = x_val; };
    void sexY(double y_val) { y = y_val; };
    double getDisTo(const Point &p); //计算当前点到参数点p的距离
    ~Point() { cout << "Distructor." << endl; };
};
double Point::getDisTo(const Point &p)
{
    return sqrt((x - p.x) * (x - p.x) + (y - p.y) * (y - p.y));
}
int main()
{
    int t;
    cin >> t;
    while (t--)
    {
        int n;
        cin >> n;
        int x, y, i, j;

        Point *p = (Point *)operator new[](n * sizeof(Point));
        for (int i = 0; i < n; i++)
        {
            cin >> x >> y;
            new (&p[i]) Point(x, y);
        }

        int max1 = 0, max2 = 0;
        double max = 0;
        for (i = 0; i < n; i++)
            for (j = 0; j < n; j++)
                if (p[i].getDisTo(p[j]) > max)
                {
                    max = p[i].getDisTo(p[j]);
                    max1 = i;
                    max2 = j;
                }

        cout << "The longeset distance is " << fixed << setprecision(2) << max;
        cout << ",between p[" << max1 << "] and p[" << max2 << "]." << endl;

        for (int i = 0; i < n; i++)
            p[i].~Point();  //析构对象
        operator delete(p); //释放空间
    }
    return 0;
}



//E
#include <bits/stdc++.h>
using namespace std;
class CStack
{
    int *a;
    int size;
    int top;
public:
    CStack()
    {
        a = new int[10];
        top = 0; size = 10;
        cout << "Constructor." << endl;
    }
    CStack(int s)
    {
        a = new int[s];
        top = 0; size = s;
        cout << "Constructor." << endl;
    }
    int get(int index)
    {
        return a[index];
    }
    void push(int n)
    {
        a[top++] = n;
    }
    int isEmpty()
    {
        return top == 0;
    }
    int isFull()
    {
        return top == size;
    }
    int pop()
    {
        return a[--top];
    }
    ~CStack()
    {
        delete []a;
        cout << "Destructor." << endl;
    }
};
int main()
{
    int t; cin >> t;
    while (t--)
    {
        int n; cin >> n;
        CStack s(n);   
        for (int i = 0; i < n; i++)
        {
            int x; cin >> x; s.push(x);
        }
        for (int j = 0;j < n - 1; j++)
            cout << s.pop() << " ";
        cout << s.pop() << endl;
    }
    return 0;
}
```

23.4.21

总结

```c++
拷贝构造函数
浅拷贝: 系统自动生成的拷贝构造函数, 可以处理一般的赋值拷贝;
(1)不会处理静态数据成员, 如 const 或者 static;
(2)当类成员里面有动态成员时, 也会出现问题;
例如
class Rect
{
public:
    Rect()      // 构造函数，p指向堆中分配的一空间
    {
        p = new int(100);
    }
    ~Rect()     // 析构函数，释放动态分配的空间
    {
        if(p != NULL)
        {
            delete p;
        }
    }
private:
    int width;
    int height;
    int *p;     // 一指针成员
};
int main()
{
    Rect rect1;
    Rect rect2(rect1);   // 复制对象
    return 0;
}
上面代码的rect2的*p, 其实和rect1的*p指向的是同一块地址, 也就是说两个变量共用了同一块地址, 这就是浅拷贝的弊端
    
深拷贝: 我们自己定义的拷贝构造函数, 通过new开辟新的空间, 并使新成员的指针指向该空间, 然后再赋值, 除了下面函数的 *p=*(r.p),在遇到字符数组时使用strcpy
class Rect
{
public:
    Rect()      // 构造函数，p指向堆中分配的一空间
    {
        p = new int(100);
    }
    Rect(const Rect& r)
    {
        width = r.width;
        height = r.height;
        p = new int;    // 为新对象重新动态分配空间
        *p = *(r.p);
    }
    ~Rect()     // 析构函数，释放动态分配的空间
    {
        if(p != NULL)
        {
            delete p;
        }
    }
private:
    int width;
    int height;
    int *p;     // 一指针成员
};
//字符数组的拷贝
soft(soft &s1)
{
    name = new char[strlen(s1.name) + 1];
    strcpy(name, s1.name);
}
```

题目代码

```c++
//A
class Equation
{
    double a, b, c;

public:
    Equation(double _a, double _b, double _c) : a(_a), b(_b), c(_c){};
    Equation() : a(1.0), b(1.0), c(0){};
    void set(double _a, double _b, double _c) { a = _a, b = _b, c = _c; }
    void getRoot()
    {
        double delta = b * b - 4 * a * c;
        if (delta > 0)
        {
            cout << fixed << setprecision(2) << "x1=" << (-b + sqrt(delta)) / (2 * a) << " x2=" << (-b - sqrt(delta)) / (2 * a) << endl;
        }
        else if (delta == 0)
        {
            cout << "x1=x2=" << fixed << setprecision(2) << (-b / (2 * a)) << endl;
        }
        else
        {
            double real = -b / (2 * a), ima = sqrt(-delta) / (2 * a);
            cout << fixed << setprecision(2) << "x1=" << real << "+" << ima << "i x2=" << real << "-" << ima << "i" << endl;
        }
    }
};
int main()
{
    int t;
    cin >> t;
    double a, b, c;
    while (t--)
    {
        cin >> a >> b >> c;
        Equation equ(a, b, c);
        equ.getRoot();
    }
    return 0;
}


//B
class Cla
{
    int value;

public:
    Cla() : value(0) { cout << "Constructed by default, value = 0" << endl; }
    Cla(int _value) : value(_value) { cout << "Constructed using one argument constructor, value = " << _value << endl; }
    Cla(const Cla &last)
    {
        *this = last;
        cout << "Constructed using copy constructor, value = " << this->value << endl;
    }
};
int main()
{
    int t;
    cin >> t;
    Cla *ret;
    while (t--)
    {
        int op, x;
        cin >> op;
        if (op == 0)
        {
            Cla cla = Cla();
        }
        else if (op == 1)
        {
            cin >> x;
            Cla cla(x);
        }
        else if (op == 2)
        {
            cin >> x;
            Cla cla(x);
            Cla claa(cla);
        }
    }
    return 0;
}


//C
class CTelNumber
{
    string s;

public:
    CTelNumber(){};
    CTelNumber(string _s) : s(_s){};
    bool check()
    {
        if (s.size() != 7 || !(s[0] >= '2' && s[0] <= '8'))
            return 0;
        for (int i = 0; i < s.size(); i++)
            if (s[i] > '9' || s[i] < '0')
                return 0;
        return 1;
    }
    void solve()
    {
        if (!check())
            cout << "Illegal phone number" << endl;
        else if (s[0] <= '4')
            cout << '8' << s << endl;
        else
            cout << '2' << s << endl;
    }
};
int main()
{
    int t;
    cin >> t;
    while (t--)
    {
        string num;
        cin >> num;
        CTelNumber ctel(num);
        ctel.solve();
    }
    return 0;
}


//D
class CDate
{
private:
    int year, month, day;
public:
    CDate() {}
    CDate(int _year, int _month, int _day) : year(_year), month(_month), day(_day) {};
    void set(int y, int m, int d) {year = y; month = m; day = d;}
    bool isLeapYear(int _year) { return (_year % 4 == 0 && _year % 100 != 0) || _year % 400 == 0; }
    int getYear() { return year; }
    int getMonth() { return month; }
    int getDay() { return day; }
    int getDayofYear()
    {

        int i, sum = day;
        int a[13] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
        int b[13] = {0, 31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
        for (int i = 2015; i < year; i++)
            sum += (365 + isLeapYear(i));
        if (isLeapYear(year))
            for (i = 1; i < month; i++)
                sum += b[i];
        else
            for (i = 1; i < month; i++)
                sum += a[i];
        return sum;
    }
};

class soft
{
private:
    char *name;
    char type;
    CDate d1;
    char store;
public:
    soft(char *n, char t, char s, int y, int m, int d)
    {
        name = new char[strlen(n) + 1];
        strcpy(name, n);
        type = t;
        store = s;
        d1.set(y, m, d);
    }
    soft(soft &s1)
    {
        // *this = s1;
        name = new char[strlen(s1.name) + 1];
        strcpy(name, s1.name);
        type = 'B';
        store = 'H';
        d1 = s1.d1;
    }
    void print()
    {
        cout << "name:" << name << endl;
        switch (type)
        {
        case 'O':
            cout << "type:original" << endl;
            break;
        case 'T':
            cout << "type:trial" << endl;
            break;
        case 'B':
            cout << "type:backup" << endl;
            break;
        }
        switch (store)
        {
        case 'D':
            cout << "media:optical disk" << endl;
            break;
        case 'H':
            cout << "media:hard disk" << endl;
            break;
        case 'U':
            cout << "media:USB disk" << endl;
            break;
        }
        if (d1.getDay() == 0 && d1.getMonth() == 0 && d1.getYear() == 0)
            cout << "this software has unlimited use" << endl;
        else if ((d1.getYear() >= 2015 && d1.getMonth() >= 4 && d1.getDay() >= 7) || (d1.getYear() >= 2015 && d1.getMonth() > 4))
        {
            cout << "this software is going to be expired in " << d1.getDayofYear() - 98 << " days" << endl;
        }
        else
        {
            cout << "this software has expired" << endl;
        }
    }

    ~soft() {delete[] name;}
};
int main()
{
    int t;
    cin >> t;
    int y, d, m;
    char name[100], type, store;

    while (t--)
    {
        cin >> name >> type >> store >> y >> m >> d;
        soft s2(name, type, store, y, m, d);
        s2.print();
        cout << endl;
        soft s3(s2);
        s3.print();
        cout << endl;
    }
}


//E
class Date
{
    int year, month, day;
public:
    Date() {};
    Date(int _year, int _month, int _day) : year(_year), month(_month), day(_day) {};
    void print()
    {
        cout << year << '.' << month << '.' << day << endl;
    }
};
class TeleNumber
{
    char a; 
    string s;
    int c;
    Date *d;
public:
    TeleNumber() {};
    TeleNumber(char _a, string _s, int _c, Date _d) : a(_a), s(_s), c(_c), d(&_d) {};
    void print_type()
    {
        if (a == 'A') cout << "类型=机构||";
        else if (a == 'B') cout << "类型=企业||";
        else if (a == 'C') cout << "类型=个人||";
    }
    void print_status()
    {
        cout << "||State=";
        if (c == 1) cout << "在用";
        else if (c == 2) cout << "未用";
        else if (c == 3) cout << "停用";
    }
    void solve(int op)
    {
        if (op == 1) cout << "Construct a new phone " << s << endl;
        else if (op == 2) cout << "Construct a copy of phone " << s << endl;
        else if (op == 3) cout << "Stop the phone " << s << endl;
        if (op == 1 || op == 3) print_type();
        else cout << "类型=备份||";
        cout << "号码=" << s;
        if (op == 2) cout << 'X';
        if (op == 1 || op == 2) print_status();
        else cout << "||State=停用";
        if (op == 3)
        {
            cout << "||停机日期=";
            d->print();
        }
        if (op == 3) cout << "----";
        cout << endl;
    }
};
int main()
{
    int t; cin >> t;
    char a; string s; int c; int year, month, day;
    while (t--)
    {
        cin >> a >> s >> c >> year >> month >> day;
        Date dat(year, month, day);
        TeleNumber tele(a, s, c, dat);
        for (int i = 1; i <= 3; i++) tele.solve(i);
    }
    return 0;
}
```

*23.4.28*

总结

**静态成员函数**

作用: 如果希望各对象中的某个变量值是一样的, 就可以用 `static`把它定义为静态数据成员, 这样它就为各对象所共有, 而不只属于某个对象的成员

- 使用**静态成员**数据需要两条语句: 一条在类中, 用 `static` 关键字声明, 一条在类外; 且静态数据成员的初始化应该在主函数调用之前, 并且不能在类的声明中初始化; 定义和初始化格式如下：

  ```c++
  //初始化格式
  //不必在初始化语句中加static; 如果未对静态数据成员赋初值，则编译系统会自动赋予初值0
  <数据类型> <类名>::<静态数据成员名> = <值>；
  int Point::score = 10;
  ```

- 在类外引用公有静态数据成员时, 可采用如下格式: `<类名>::<静态数据成员名>` , 用类名来引用静态数据成员, 表示该成员是属于某个类的, 而不是属于某个类的特定的对象的,从而提高可理解性

- 用关键字 `static` 声明的成员函数为**静态成员函数**

- 静态成员函数主要用于表示该函数逻辑上是属于某个类的, 它只访问逻辑上属于一个类的静态数据成员, 全局变量和静态成员函数的参数, 而不访问描述该类各对象状态的非静态数据成员

- 由于静态成员函数不访问非静态数据成员, 因而静态成员函数不能被声明为 `const`. 静态成员函数没有 `this` 指针, 由此决定了静态成员函数不能默认访问本类中的非静态成员

- 静态成员函数的作用是为了能处理静态数据成员

- 调用静态成员函数

  ```c++
  //格式
  //既可用目标对象名, 也可用类名采用如下格式调用:
  <类名>::<静态成员函数名>(<参数表>)
  //实际上也允许通过对象名调用静态成员函数, 但这并不意味着此函数是属于对象的, 而只是用对象的类型而已
  <对象名>.<静态成员函数名>(<参数表>) 
  ```

**友元和友元函数**

在一个类中可以有公用的 `public` 成员和私有的 `private` 成员, 在类外可以访问公用成员, 只有本类中的函数可以访问本类的私有成员, 但是C++即存在严格性也存在灵活性, 严格性体现在强类型检查, 类的私有和受保护数据访问的控制(类, 封装), 灵活性体现在打破类型检查的隐式和强制类型转换, 打破访问控制的友元. 

C++允许使用关键字 `friend` 在一个类的内部将一个全局非成员函数, 另一个类的成员函数, 或另外一个类说明为该类的友元; 作为一个类的友元, 可以访问该类的所有成员(包括公有和私有的数据成员和成员函数)

- 友元函数不是类的成员函数, 不能被声明为 `const`, 也没有 `this` 指针

- 在友元函数体内只能通过作为友元函数参数传递进来的对象名, 对象指针或对象引用来访问对象成员

- 定义格式

  ```C++
  //友元函数在类定义花括号内声明的一般格式为：
  friend 函数返回类型 友元函数名(类名 & 对象名，…)
  //友元函数定义的格式为
  函数返回类型 友元函数名(类名 & 对象名，…)
  {函数体}
  ```

- 在友元函数中引用私有数据成员时, 必须加上对象名, 不能直接引用私有数据成员, 因为友元函数不算是该类的成员函数, 不能默认引用该类的数据成员

  ```C++
  //格式
  对象.私有数据成员
  ```

- `friend` 函数不仅可以是一般函数(非成员函数), 而且可以是另一个类中的成员函数, 与普通函数不同, 成员函数的原型必须先被定义, 才能被有效地声明为友元函数

- 不仅可以将一个函数声明为一个类的“朋友”,  而且可以将一个类(例如B类)声明为另一个类(例如A类)的“朋友”. 这时B类就是A类的友元类. 友元类B中所有函数都是A类的友元函数, 可以访问A类中所有成员; 在A类的定义体中用以下语句声明B类为其友元类: `friend B` ; 声明友元类的一般形式为 `friend 类名`

-  友元的关系是单向的而不是双向的

- 友元的关系不能传递

- 在实际工作中, 除非确有必要, 一般并不把整个类声明为友元类, 而只将确实有需要的成员函数声明为友元函数, 这样更安全一些; 友元利弊分析: 面向对象程序设计的一个基本原则是封装性和信息隐蔽, 而友元却可以访问其他类中的私有成员, 不能不说这是对封装原则的一个小的破坏. 但是它能有助于数据共享, 能提高程序的效率, 在使用友元时, 要注意到它的副作用, 不要过多地使用友元, 只有在使用它能使程序精炼, 并能大大提高程序的效率时才用友元



实验代码

```C++
//A
#include <bits/stdc++.h>
using namespace std;
class Point
{
    friend double Distance(Point &p1, Point &p2);
    double x, y;
public: 
    Point(double xx, double yy) : x(xx), y(yy) {};
};
double Distance(Point &p1, Point &p2)
{
    return sqrt((p1.x - p2.x) * (p1.x - p2.x) + (p1.y - p2.y) * (p1.y - p2.y));
}
int main()
{
    int t; cin >> t;
    while (t--)
    {
        double _x1, _x2, _y1, _y2; cin >> _x1 >> _y1 >> _x2 >> _y2;
        Point p1(_x1, _y1), p2(_x2, _y2);
        cout << (int)Distance(p1, p2) << endl;
    }
    return 0;
}


//B
#include <bits/stdc++.h>
using namespace std;

class Account
{
private:
    static float total;
    static int count; //银行账户数量
    static float InterestRate; //利率
    float _balance;
    string _accno, _accname; 
    // friend void Update(Account& a);

public:
    Account() {};
    Account(string accno, string name, float balance) :_accno(accno), _accname(name) ,_balance(balance)
    {
        count ++;
        total += _balance;
    }
    void Deposit(float account)  {_balance += account,total += account;} //存款
    void Withdraw(float ammount) {_balance -= ammount; total -= ammount;} //取款
    float GetBalance() {return _balance;} //获取账户余额
    void Show() {cout << _accno << " " << _accname << " " << _balance << " ";}   //显示账户所有基本信息
    static float GetTotal() {return total;} //获取总额
    static float GetInterestRate() {return InterestRate;}    //获取利率
    static void SetInterestRate(float rate) {InterestRate = rate;} //设置利率

    friend void Update(Account &a) 
    {
        total += a._balance * Account :: InterestRate;
        a._balance += a._balance * Account :: InterestRate;
    }
    static int GetCount() {return count;}
    ~Account() 
    {
        count --;
        total -= _balance;
    }
};

int Account :: count = 0;
float Account :: InterestRate = 0;
float Account :: total = 0;

int main()
{
    float rate;
    cin >> rate;
    Account :: SetInterestRate(rate);
    int t;
    cin >> t;
    Account *p = new Account[t];
    for(int i = 0; i < t; i++)
    {
        string id, name;
        float balance, account, ammount;
        cin >> id >> name >> balance >> account >> ammount;
        new (&p[i]) Account(id, name, balance);
        p[i].Deposit(account);
        p[i].Show();
        Update(p[i]);
        cout << p[i].GetBalance() << " ";
        p[i].Withdraw(ammount);
        cout << p[i].GetBalance() << endl;
    }
    cout << Account :: GetTotal() << endl;
    delete []p;
    return 0;
}


//C
#include <iostream>
using namespace std;
class Complex
{
private:
	double real; // 实部
	double imag; // 虚部
public:
	Complex(){}
	Complex(double r, double i)
    {
        real = r, imag = i;
    }
	friend Complex addCom(const Complex& c1, const Complex& c2)
    {
        Complex t(c1.real + c2.real, c1.imag + c2.imag);
        return t;
    }
    friend Complex minusCom(const Complex& c1, const Complex& c2)
    {
        Complex t(c1.real - c2.real, c1.imag - c2.imag);
        return t;
    }
	friend void outCom(const Complex& c)
    {
        cout << "(" << c.real <<"," << c.imag << ")\n";
    }
    
};

int main()
{
    double rl, ig;
    cin >> rl >> ig;
    Complex c(rl, ig);
    int n;
    cin >> n;
    while(n--)
    {
        char op[5];
        cin >> op >> rl >> ig;
        Complex ct(rl, ig);
        if(op[0] == '+') c = addCom(c, ct);
        else c = minusCom(c, ct);
        outCom(c);
    }
    return 0;
}


//D
#include <bits/stdc++.h>
using namespace std;
class Hotel
{
    private:
        static int totalCustNum; // 顾客总人数
        static float totalEarning; // 旅店总收入
        static float rent; // 每个顾客的房租
        char *customerName; // 顾客姓名
        int customerId; // 顾客编号
    public:
        Hotel(){}
        Hotel(char* customer)
        {
            Hotel::totalCustNum++;
            Hotel::totalEarning += rent;
            customerName = new char[strlen(customer) + 10];
            strcpy(customerName, customer);
        }
        ~Hotel()
        {
            delete customerName;
        }
        void Display()
        {
            printf("%s %04d %d %d\n", customerName, 20150000 + Hotel::totalCustNum, Hotel::totalCustNum, (int)totalEarning);
        }
        static void setRent(float rt)
        {
            Hotel::rent = rt;
        }
};

int Hotel::totalCustNum = 0;
float Hotel::totalEarning = 0;
float Hotel::rent = 0;

int main()
{
    float rt;
    cin >> rt;
    Hotel::setRent(rt);
    char s[50];
    while(cin >> s)
    {
        if(s[0] == '0') break;
        Hotel h(s);
        h.Display();
    }
    return 0;
}


//E
#include <bits/stdc++.h>
using namespace std;
class CDate;
class CTime
{
	private:
		int hour, min, sec;
	public:
		friend void Display(CDate &, CTime &);
		void input()
		{
			cin >> hour >> min >> sec;
		}
};
class CDate
{
	private:
		int year,month,day;
	public:
		friend void Display(CDate &,CTime &);
		void input()
		{
			cin >> year >> month >> day;
		}
};
void Display(CDate & date,CTime & time)
{
	cout << date.year << '-' << setfill('0') << setw(2) << date.month << '-' << setw(2) << date.day << ' ' << setw(2) << time.hour << ':' << setw(2) << time.min << ':' << setw(2) << time.sec << '\n';
}
int main()
{
	int t;
	CDate date;
	CTime time;
	cin >> t;
	while(t--)
	{
		date.input();
		time.input();
		Display(date, time);
	}
    return 0;
}
```

23.5.3

总结: 

当我们创建的类中有适用于动态开辟空间的指针, 且析构函数写了 `delete` 时, 我们在整个程序中的任何地方, 都不适宜用浅拷贝, 而是要采用深拷贝, 当一个类中存在另一个类的对象时, 在构造函数中我们要使用一个 `: name(v1, v2) ` , 具体请看 `D` 题

代码

```c++
//A
#include <bits/stdc++.h>
using namespace std;
class CVector
{
    int *data;
    int n;
public:
    CVector()
    {
        n = 5;
        data = new int[5];
        for (int i = 0; i < n; i++) data[i] = i;
    }
    CVector(int _n, int *_data)
    {
        n = _n;
        data = new int[n];
        for (int i = 0; i < n; i++)
            data[i] = _data[i];
    }
    void myPrint()
    {
        for (int i = 0; i < n; i++) 
            printf(" %d" + !i, data[i]);
        printf("\n");
    }
    ~CVector() {};
};
int main()
{
    int n; cin >> n;
    int *p;
    p = new int[n];
    for (int i = 0; i < n; i++) cin >> p[i];
    CVector c1 = CVector();
    c1.myPrint();
    CVector c2 = CVector(n, p);
    c2.myPrint();
    return 0;
}


//B
#include <bits/stdc++.h>
using namespace std;
class CVector
{
    int *data;
    int n;
public:
    CVector()
    {
        n = 5;
        data = new int[5];
        for (int i = 0; i < n; i++) data[i] = i;
    }
    CVector(int _n, int *_data)
    {
        n = _n;
        data = new int[n];
        for (int i = 0; i < n; i++)
            data[i] = _data[i];
    }
    void myPrint()
    {
        for (int i = 0; i < n; i++) 
            printf(" %d" + !i, data[i]);
        printf("\n");
    }
    friend void add(const CVector v1, const CVector v2)
    {
        for (int i = 0; i < v1.n; i++)
            v1.data[i] += v2.data[i];
        print(v1);
    }
    friend void print(CVector c)
    {
        for (int i = 0; i < c.n; i++)
            printf(" %d" + !i, c.data[i]);
        printf("\n");
    }
    ~CVector() {};
};
int main()
{
    int t; cin >> t;
    while (t--)
    {    
        int n; cin >> n;
        int *p;
        p = new int[n];
        for (int i = 0; i < n; i++) cin >> p[i];
        CVector c1 = CVector(n, p);
        c1.myPrint();
        for (int i = 0; i < n; i++) cin >> p[i];
        CVector c2 = CVector(n, p);
        c2.myPrint();
        add(c1, c2);
    }
    return 0;
}



//C
#include <bits/stdc++.h>
using namespace std;
class CVector
{
    static int sum;
    int *data;
    int n;
public:
    CVector()
    {
        n = 5;
        data = new int[5];
        for (int i = 0; i < n; i++) data[i] = i;
    }
    CVector(int _n, int *_data)
    {
        n = _n;
        data = new int[n];
        for (int i = 0; i < n; i++)
            data[i] = _data[i], sum += data[i];
    }
    void myPrint()
    {
        for (int i = 0; i < n; i++) 
            printf(" %d" + !i, data[i]);
        printf("\n");
    }
    // friend void add(const CVector v1, const CVector v2)
    // {
    //     for (int i = 0; i < v1.n; i++)
    //         v1.data[i] += v2.data[i];
    //     print(v1);
    // }
    // friend void print(CVector c)
    // {
    //     for (int i = 0; i < c.n; i++)
    //         printf(" %d" + !i, c.data[i]);
    //     printf("\n");
    // }
    static void print() {cout << sum << endl;}
    static void init() {sum = 0;}
    ~CVector() {};
};

int CVector::sum = 0;


int main()
{
    int t; cin >> t;
    while (t--)
    {   
        CVector::init();
        int m; cin >> m;
        while (m--)
        {
            int n; cin >> n;
            int *p;
            p = new int[n];
            for (int i = 0; i < n; i++) cin >> p[i];
            CVector c1 = CVector(n, p);
            c1.myPrint();
        }
        CVector::print();
    }
    return 0;
}



//D
#include <bits/stdc++.h>
using namespace std;

class CVector
{
    friend class CStudent;
    double sum;
    int *data;
    int n;
public:
    CVector()
    {
        n = 5;
        sum = 0;
        data = new int[5];
        for (int i = 0; i < n; i++) data[i] = i;
    }
    CVector(int _n, int *_data, double sum = 0)
    {
        n = _n;
        data = new int[n];
        for (int i = 0; i < n; i++)
            data[i] = _data[i], sum += data[i];
    }
    void myPrint()
    {
        for (int i = 0; i < n; i++) 
            printf("%d ", data[i]);
    }
    void print() {cout << fixed << setprecision(2) << sum / n << endl;}
    ~CVector() {delete []data;};
};

class CStudent
{
    string name;
    CVector score;
public:
    CStudent() {}
    CStudent(string _name, int _n, int *_data): score(_n, _data)   //深拷贝
    {
        // CVector score = CVector(n, a);   浅拷贝: 错误!
        name = _name;
        score.sum = 0;
        for (int i = 0; i < _n; i++)
            score.sum += _data[i];
    }
    void print()
    {
        cout << name << ' ';
        score.myPrint();
        score.print();
    }
};


int main()
{
    string s;
    while (cin >> s)
    {   
        int n; cin >> n;
        int *p;
        p = new int[n];
        for (int i = 0; i < n; i++) cin >> p[i];
        CStudent(s, n, p).print();
    }
    return 0;
}



//E
#include <bits/stdc++.h>
using namespace std;

class CVector;
class CMatrix
{
    friend class CVector;
    int n;
    int **data;
public:
    CMatrix() {}
    CMatrix(int _n, int **_data)
    {
        n = _n;
        data = new int *[n];
        for (int i = 0; i < n; i++)
            data[i] = new int[n];
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                // data[i][j] = _data[i][j];
                *(*(data + i) + j) = *(*(_data + i) + j);
    }
    friend void mul(CVector _cv, CMatrix _cm);
};

class CVector
{
    int *data;
    int n;
public:
    CVector()
    {
        n = 5;
        data = new int[5];
        for (int i = 0; i < n; i++)
            data[i] = i;
    }
    CVector(int _n, int *_data)
    {
        n = _n;
        data = new int[n];
        for (int i = 0; i < n; i++)
            data[i] = _data[i];
    }
    friend void mul(CVector _cv, CMatrix _cm)
    {
        for (int i = 0; i < _cv.n; i++)
        {
            int sum = 0;
            for (int j = 0; j < _cv.n; j++)
            {
                // cout << _cv.data[j] << ' ' << _cm.data[i][j] << endl;
                sum += (_cv.data[j] * _cm.data[i][j]);
            }
            printf(" %d" + !i, sum);
        }
        printf("\n");
    }
    ~CVector(){};
};




int main()
{
    int t;
    cin >> t;
    while (t--)
    {
        int n, m;
        int **data, *p;
        cin >> n;
        // 先创建n行
        data = new int *[n];
        // 再创建n列
        for (int i = 0; i < n; i++)
            data[i] = new int[n];
        // 打印矩阵
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                cin >> data[i][j];
        CMatrix cm = CMatrix(n, data);
        cin >> m;
        p = new int[m];
        for (int i = 0; i < m; i++) cin >> p[i];
        if (n != m)
            cout << "error" << endl;
        else
        {
            CVector cv = CVector(n, p);
            mul(cv, cm);
        }
    }
    return 0;
}
```

23.5.10

代码

```c++
//A
#include <bits/stdc++.h>
using namespace std;
class CRobot
{
    string name;
    char type;
    int blood, att, def, grd;
public:
    CRobot() {}
    CRobot(string _name, char _type, int _grd)
    {
        name = _name;
        type = _type;
        grd = _grd;
        blood = att = def = 5 * grd;
        switch (_type)
        {
        case 'A':
            att = 10 * grd;
            break;
        case 'D':
            def = 10 * grd;
            break;
        case 'H':
            blood = 50 * grd;
            break;
        default:
            break;
        }
    }
    void print()
    {
        cout << name;
        printf("--%c--%d--%d--%d--%d\n", type, grd, blood, att, def);
    }
    friend bool change(CRobot &rob, char type)
    {
        if (type == rob.type) return false;
        else
        {
            rob = CRobot(rob.name, type, rob.grd);
            return true;
        }
    }
};
int main()
{
    int t; cin >> t;
    int cnt = 0;
    while (t--)
    {
        string name;
        char type, ch;
        int grd;
        cin >> name >> type >> grd;
        CRobot rob = CRobot(name, type, grd);
        cin >> ch;
        if (change(rob, ch)) cnt++;
        rob.print();
    }
    printf("The number of robot transform is %d\n", cnt);
    return 0;
}


//B
#include <bits/stdc++.h>
using namespace std;
class CVirNum;
class CNum
{
    friend CVirNum;
    int num;
    char type;
public:
    CNum() {}
    CNum(int _num, char _type): num(_num), type(_type) {}
    friend bool _find(CVirNum &cv, int num);
};
class CVirNum
{
    CNum tnum;
    bool status;
    string name;
public:
    CVirNum() {}
    CVirNum(int _num, char _type, bool _status, string _name): tnum(_num, _type), status(_status), name(_name)
    {
        cout << _num << " constructed." << endl;
    }
    ~CVirNum()
    {
        cout << tnum.num << " destructed." << endl;
    }
    friend bool _find(CVirNum &cv, int num)
    {
        if (cv.tnum.num == num)
        {
            printf("Phone=%d--Type=%c--State=%s--Owner=", num, cv.tnum.type, cv.status ? "use" : "unuse");
            cout << cv.name << endl;
            return true;
        }
        else return false;
    }
};
int main()
{
    string _name;
    char _type;
    bool _status;
    int _num;
    CVirNum *p = (CVirNum *)operator new[](3 * sizeof(CVirNum));
    for (int i = 0; i < 3; i++)
    {
        cin >> _num >> _type >> _status >> _name;
        new (&p[i]) CVirNum(_num, _type, _status, _name);
    }
    int t; cin >> t;
    while (t--)
    {
        int ret; cin >> ret;
        for (int i = 0; i < 3; i++)
        {
            if (_find(p[i], ret)) break;
            if (i == 2) cout << "wrong number." << endl;
        }
    }
    for (int i = 2; i >= 0; i--)
        p[i].~CVirNum();
    operator delete(p);
    return 0;
}


//C
#include <bits/stdc++.h>
using namespace std;
class cBankAccount
{
    int balance;
    double rate;
    int id;
    char type;
public:
    cBankAccount() {}
    cBankAccount(int _balance, double _rate, int _id, char _type): balance(_balance), rate(_rate), id(_id), type(_type) {}
    cBankAccount(const cBankAccount &c)   // 此处不加const会报错
    {
        balance = c.balance;
        rate = 0.015;
        id = c.id + 5e7;
        type = c.type;
    }
    void cal()
    {
        balance += balance * rate;
        printf("Account=%d--sum=%d\n", id, balance);
    }
    void print()
    {
        printf("Account=%d--%s--sum=%d--rate=%.3f\n", id, type == 'P' ? "Person": "Enterprise", balance, rate);
    }
    friend void solve(cBankAccount &c, char op)
    {
        if (op == 'C') c.cal();
        else c.print();
    }
};
int main()
{
    int t; cin >> t;
    while (t--)
    {
        int id, balance;
        char type;
        cin >> id >> type >> balance;
        cBankAccount c1 = cBankAccount(balance, 0.005, id, type);
        // cBankAccount c2 = cBankAccount(balance, 0.015, id + 5e7, type);
        cBankAccount c2 = cBankAccount(c1);
        char op1, op2;
        cin >> op1 >> op2;
        solve(c1, op1);
        solve(c2, op2);
    }
    return 0;
}



//D
#include <bits/stdc++.h>
using namespace std;
class cTV
{
    static int cnt1, cnt2;
    int voice;
    int status;
    int channel;
public:
    cTV() {}
    cTV(int _chanenl)
    {
        channel = -channel;
        voice = 50;
        status = 1;
        cnt1++; 
    }
    friend void change(cTV &c, int status, int channel, int voice, int id)
    {
        c.channel = channel;
        c.voice += voice;
        c.voice = min(c.voice, 100);
        c.voice = max(c.voice, 0);
        if (c.status != status)
        {
            if (c.status == 1) cnt1--, cnt2++;
            else cnt2--, cnt1++;
            c.status = status;
        }
        printf("第%d号电视机--%s模式--频道%d--音量%d\n", id, c.status == 1 ? "TV" : "DVD", c.channel, c.voice);
    }
    static void print()
    {
        printf("播放电视的电视机数量为%d\n", cnt1);
        printf("播放DVD的电视机数量为%d\n", cnt2);
    }
};
int cTV::cnt1 = 0;
int cTV::cnt2 = 0;
int main()
{
    int n; cin >> n;
    cTV *p = new cTV[n];
    for (int i = 0; i < n; i++) p[i] = cTV(i + 1);
    int t; cin >> t;
    while (t--)
    {
        int id, status, channel, voice;
        cin >> id >> status >> channel >> voice;
        change(p[id], status, channel, voice, id);
    }
    cTV::print();
    delete []p;
    return 0;
}
```

23.5.12

总结

**继承**

1. 定义：继承(inheritance)机制是面向对象程序设计中使代码可以复用的最重要的手段，它允许程序员在保持原有类特性的基础上进行扩展，增加功能。这样产生的新类，称派生类（或子类），被继承的类称基类（或父类）。继承呈现了面向对象程序设计的层次结构，体现了由简单到复杂的认知过程。之前接触的复用都是函数复用，继承是类设计层次的复用。

   语法: `class 新类的名字:继承方式 继承类的名字{};`

   ```c++
   class student:public human{}；
   //student是新类的名字，public是继承方式，human是要继承的类
   //意思就是说我定义了一个名叫 student的类 以public的方式 来继承你human
   ```

2. 继承后的子类成员访问权限

![在这里插入图片描述](https://img-blog.csdnimg.cn/5a485e017c514125b2697eca37cb08be.png)

​		可以理解为 `public>protectd>private`

3. 注意: 

   - 基类private成员无论以什么方式继承到派生类中都是不可见的。这里的不可见是指基类的私有成员还是被继承到了派生类对象中，但是语法上限制派生类对象不管在类里面还是类外面都不能去访问它。

   - 基类private成员在派生类中不能被访问，如果基类成员不想在派生类外直接被访问，但需要在派生类中访问，就定义为protected。可以看出保护成员限定符是因继承才出现的。

   - 基类的私有成员在子类都是不可见；基类的其他成员在子类的访问方式就是访问限定符和继承方式中权限更小的那个（权限排序：public>protected>private）。

   - 使用关键字class时默认的继承方式是private，使用struct时默认的继承方式是public，但最好显式地写出继承方式。


4. 子类和父类的相互赋值

   - 方式1: 使用 `=` , 按照**切片原则**

     ```c++
     student st;//子类
     human hm;//父类
     hm = st;
     ```


   - 方式2: 引用

     ```c++
     student st;//子类
     human& hm=st;//父类
     ```


   - 方式3: 指针

     ```C++
     student st;//子类
     human* hm=&st;//父类
     ```


5. 同名的成员变量, 以子类优先, 如果要访问子类的该成员变量, 则需要加上修饰 `父类::变量` 

6. 同名成员函数, 会构成隐藏, 函数的隐藏, 编译器会默认调用子类中匹配的函数. 虽然成员函数的隐藏, 只需要函数名相同就构成隐藏, 对参数列表没有要求, 如果没有编译器就会报错

7. 子类中默认的成员函数

   - 构造函数

     编译器会默认先调用父类的构造函数, 再调用子类的构造函数. 若自行编写了父类构造函数, 则要保证父类构造函数有效, 否则会导致父类构造失效


   - 析构函数

     析构函数和构造函数相反, 编译器默认先调用子类的析构函数, 再调用父类的析构函数. 注意, 千万不要在子类中调用父类的析构, 如果是指针类型, 那么同一块区域被析构两次就会造成野指针问题


   - 拷贝构造

     子类中调用父类的拷贝构造时, 直接传入子类对象即可, 父类的拷贝构造会通过“切片”拿到父类的那一部分


   - 赋值运算符重载

     子类的 `operator=` 必须要显式调用父类的 `operator=` 完成父类的赋值

     因为子类和父类的运算符, 编译器默认给与了同一个名字, 所以构成了隐藏, 所以每次调用 `=` 这个赋值运算符都会一直调用子类, 会造成循环, 所以这里的赋值要直接修饰限定父类

代码

```c++
//A
#include <bits/stdc++.h>
using namespace std;
class CPoint
{
protected:
    int x, y;

public:
    CPoint(int _x, int _y) : x(_x), y(_y) {}
};
class CCircle : public CPoint
{
protected:
    int r;

public:
    CCircle(int _x, int _y, int _r) : CPoint(_x, _y), r(_r) {}
    double Area()
    {
        return 3.14 * r * r;
    }
    void print()
    {
        cout << "Circle:(" << x << "," << y << ")," << r << endl;
        cout << "Area:" << Area() << endl;
    }
};
class CCylinder : public CCircle
{
protected:
    int h;

public:
    CCylinder(int _x, int _y, int _r, int _h) : CCircle(_x, _y, _r), h(_h) {}
    double Volume()
    {
        return 3.14 * r * r * h;
    }
    void print()
    {
        cout << "Cylinder:(" << x << "," << y << ")," << r << "," << h << endl;
        cout << "Volume:" << Volume() << endl;
    }
};
int main()
{
    int x, y, r, h;
    cin >> x >> y >> r;
    CCircle c1(x, y, r);
    c1.print();
    cin >> x >> y >> r >> h;
    CCylinder c2(x, y, r, h);
    c2.print();
    return 0;
}



//B
#include <bits/stdc++.h>
using namespace std;
class C2D
{
protected:
    int x, y;
public:
    C2D(int _x, int _y): x(_x), y(_y) {}
    double getDistance()
    {
        return sqrt(x * x + y * y);
    }
    void print()
    {
        cout << getDistance() << endl;
    }
};
class C3D: public C2D
{
protected:
    int z;
public:
    C3D(int _x, int _y, int _z): C2D(_x, _y), z(_z) {}
    double getDistance()
    {
        return sqrt(x * x + y * y + z * z);
    }
    void print()
    {
        cout << setw(7) << getDistance() << endl;
        // printf("%f\n", getDistance());
    }
};
int main()
{
    int x, y, z;
    cin >> x >> y;
    C2D p1(x, y);
    p1.print();
    cin >> x >> y >> z;
    C3D p2(x, y, z);
    p2.print();
    cin >> x >> y >> z;
    C3D p3(x, y, z);
    p3.print();
    C2D p4 = p3;
    p4.print();
    return 0;
}



//C
#include <bits/stdc++.h>
using namespace std;
class CCounter
{
protected:
    int value;

public:
    CCounter(int v) : value(v) {}
    void increment() { value++; }
    int getvalue() { return value; }
};
class CCyclecounter : public CCounter
{
private:
    int min_value, max_value;

public:
    CCyclecounter(int minv, int maxv, int v) : min_value(minv), max_value(maxv), CCounter(v) {}
    void increment()
    {
        if (++value == max_value)
            value = min_value;
    }
};
class CCLOCK
{
private:
    CCyclecounter hour, minute, second;

public:
    CCLOCK(int h, int m, int s) : hour(0, 24, h), minute(0, 60, m), second(0, 60, s) {}
    void time(int s)
    {
        while (s--)
        {
            second.increment();
            if (second.getvalue() == 0)
            {
                minute.increment();
                if (minute.getvalue() == 0)
                    hour.increment();
            }
        }
    }
    void showoff() { cout << hour.getvalue() << ':' << minute.getvalue() << ':' << second.getvalue() << endl; }
};
int main()
{
    int t, hour, min, sec, s;
    cin >> t;
    while (t--)
    {
        cin >> hour >> min >> sec >> s;
        CCLOCK Clock(hour, min, sec);
        Clock.time(s);
        Clock.showoff();
    }
    return 0;
}



//D
#include <bits/stdc++.h>
using namespace std;
int leap[12] = {31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
int common[12] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
int digitpower[17] = {7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2};
char checkcode[11] = {'1', '0', 'X', '9', '8', '7', '6', '5', '4', '3', '2'};
class CDate
{
private:
    int year, month, day;

public:
    CDate(){};
    CDate(int _year, int _month, int _day) : year(_year), month(_month), day(_day) {}
    void datain()
    {
        cin >> year >> month >> day;
    }
    int getyear()
    {
        return year;
    }
    int getmonth()
    {
        return month;
    }
    int getday()
    {
        return day;
    }
    bool check()
    {
        if (year > 2021 || year == 2021 && month > 11 || year == 2021 && month == 11 && day > 9)
            return false;
        if (isLeap())
        {
            if (leap[month - 1] < day)
                return false;
        }
        else
        {
            if (common[month - 1] < day)
                return false;
        }
        return true;
    } // 检验日期是否合法
    string tostring()
    {
        string a = to_string(year), b = to_string(month), c = to_string(day);
        if (b.length() == 1) b = '0' + b;
        if (c.length() == 1) c = '0' + c;
        a = a + b + c;
        return a;
    }
    bool isLeap()
    {
        if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0)
            return true;
        return false;
    }
    void print()
    {
        cout << year << "年" << month << "月" << day << "日 ";
    }
};
class COldID
{
protected:
    string p_id15, p_name; // 15位身份证号码，姓名
    CDate birthday;        // 出生日期
public:
    COldID() {}
    void datain()       
    {
        cin >> p_name;
        birthday.datain();
        cin >> p_id15;
    }
    //		COldID(char *p_idval, char *p_nameval, CDate &day){};
    bool check()
    {
        cout << p_name << endl;
        if (!birthday.check())
            return false;
        if (p_id15.length() != 15)
            return false;
        for (int i = 0; i < 15; i++)
        {
            if (!isdigit(p_id15[i]))
                return false;
        }
        return true;
    } // 验证15位身份证是否合法
    void print() {}
    ~COldID() {}
};
class CNewID : public COldID
{
    string p_id18;
    CDate issueday;
    int validyear;

public:
    CNewID()
    {
        COldID::datain();
        cin >> p_id18;
        issueday.datain();
        cin >> validyear;
    }
    bool check()
    {
        if (!COldID::check())
            return false;
        if (p_id18.substr(0, 5) != p_id15.substr(0, 5) || p_id18.substr(8, 8) != p_id15.substr(6, 8)) // 比较子串
            return false;
        if (p_id18.find(birthday.tostring()) == p_id18.npos) // 判断身份证号码里面的出生日期是不是和所给的一样
            return false;
        if (!issueday.check()) // 判断签发日期是不是有效的
            return false;
        if (p_id18.length() != 18)
            return false;
        int temp = 0;
        for (int i = 0; i < 17; i++)
        {
            temp += (p_id18[i] - '0') * digitpower[i];
        }
        temp %= 11;
        if (checkcode[temp] != p_id18[17])
            return false;
        if (issueday.getyear() + validyear < 2021 || issueday.getyear() + validyear == 2021 && issueday.getmonth() > 11 || issueday.getyear() + validyear == 2021 && issueday.getmonth() == 11 && issueday.getday() > 9)
            return false;
        return true;
    }
    void print()
    {
        COldID::print();
        cout << p_id18 << ' ';
        issueday.print();
        if (validyear < 100)
            cout << validyear << "年" << endl;
        else
            cout << "长期" << endl;
    }
};

int main()
{
    int t;
    cin >> t;
    while (t--)
    {
        CNewID test;
        if (test.check()) test.print();
        else cout << "illegal id" << endl;
    }
    return 0;
}




//E
#include <bits/stdc++.h>
using namespace std;
class Person
{
protected:
    string name;
    int age;
public:
    Person() {}
    Person(string _name, int _age) : name(_name), age(_age) {}
    void base_print()
    {
        cout << name << ' ' << age << ' ';
    }
    char cal(double fscore)
    {
        char grade;
        switch ((int)fscore)
        {
        case 0 ... 59: grade = 'F'; break;
        case 60 ... 64: grade = 'D'; break;
        case 65 ... 74: grade = 'C'; break;
        case 75 ... 84: grade = 'B'; break;
        default: grade = 'A'; break;
        }
        return grade;
    }
};
class Rstu : public Person
{
    double uscore, escore;
    char grade;
public:
    Rstu(string _name, int _age, double _uscore, double _escore) : Person(_name, _age), uscore(_uscore), escore(_escore) {}
    void print()
    {
        base_print();
        cout << cal(uscore * 0.4 + escore * 0.6) << endl;
    }
};
class Sstu : public Person
{
    double fscore;
    char grade;
public:
    Sstu(string _name, int _age, double _fscore) : Person(_name, _age), fscore(_fscore) {}
    void print()
    {
        base_print();
        cout << cal(fscore) << endl;
    }
};
int main()
{
    int n; cin >> n;
    for (int i = 0; i < n; i++)
    {
        char ch; 
        string name;
        int a; double b, c;
        cin >> ch >> name;
        if (ch == 'R')
        {
            cin >> a >> b >> c;
            Rstu rs(name, a, b, c);
            rs.print();
        }
        else 
        {
            cin >> a >> b;
            Sstu ss(name, a, b);
            ss.print();
        }
    }
    return 0;
}
```

23.5.19

总结

**继承与多态**



代码

```c++
//A
#include <bits/stdc++.h>
using namespace std;
class Shape
{
public:
    virtual void area() {}
};
class Circle : public Shape
{
private:
    float r;
public:
    Circle(double _r): r(_r) {}
    virtual void area() {cout << fixed << setprecision(2) << r * r * 3.14 << endl;}
};
class Square : public Shape
{
private:
    double l;
public:
    Square(double l_) : l(l_) {}
    virtual void area() {cout << fixed << setprecision(2) << l * l << endl;}
};
class Rectangle : public Shape
{
private:
    double l, w;
public:
    Rectangle(double l_, double w_) : l(l_), w(w_) {}
    virtual void area() {cout << fixed << setprecision(2) << l * w << endl;}
};
int main()
{
    int t;
    Shape *sh;
    double l, w, r;
    for (cin >> t; t--; )
    {
        cin >> r;
        Circle c(r); sh = &c;
        sh->area();
        cin >> l;
        Square sq(l); sh = &sq;
        sh->area();
        cin >> l >> w;
        Rectangle rec(l, w); sh = &rec;
        sh->area();
    }
    return 0;
}



//B
#include <bits/stdc++.h>
using namespace std;
class Vehicle
{
protected:
    string no;
public:
    Vehicle(string no_) : no(no_) {}
    virtual void display() = 0;
};
class Car : virtual public Vehicle
{
protected:
    int num, weight;
public:
    Car(string no_, int num_, int weight_) : Vehicle(no_), num(num_), weight(weight_) {}
    virtual void display() {cout << no << ' ' << num * 8 + weight * 2 << endl;}
};
class Truck : public Vehicle
{
protected:
    int weight;
public:
    Truck(string no_, int weight_) : Vehicle(no_), weight(weight_) {}
    virtual void display() {cout << no << ' ' << weight * 5 << endl;}
};
class Bus : public Vehicle
{
protected:
    int num;
public:
    Bus(string no_, int num_) : Vehicle(no_), num(num_) {}
    virtual void display() {cout << no << ' ' << num * 30 << endl;}
};
int main()
{
    int t;
    string no;
    int type, num, weight;
    Vehicle *ve;
    for (cin >> t; t--; )
    {
        cin >> type >> no; 
        if (type == 1)
        {
            cin >> num >> weight;
            Car ca(no, num, weight);
            ve = &ca;
            ve->display();
        }
        else if (type == 2)
        {
            cin >> weight;
            Truck tr(no, weight);
            ve = &tr;
            ve->display();
        }
        else
        {
            cin >> num;
            Bus bs(no, num);
            ve = &bs;
            ve->display();
        } 
    }
    return 0;
}



//C
#include <bits/stdc++.h>
using namespace std;
class BaseAccount
{
protected:
    string name, account;
    int balance;
public:
    BaseAccount(string name_, string account_, int balance_) : name(name_), account(account_), balance(balance_) {}
    void deposit(int money)
    {
        balance += money;
    }
    virtual void withdraw(int money)
    {
        if (money > balance) cout << "insufficient" << endl;
        else balance -= money;
    }
    virtual void display()
    {
        cout << name << ' ' << account << ' ' << "Balance:" << balance << endl;
    }
};
class BasePlus : public BaseAccount
{
private:
    int limit;
    int limitSum;
public:
    BasePlus(string name_, string account_, int balance_) : BaseAccount(name_, account_, balance_), limit(5000), limitSum(0) {}
    virtual void withdraw(int money)
    {
        if (money > balance)
        {
            if (money - balance > limit - limitSum)
            {
                cout << "insufficient" << endl;
            }
            else limitSum += (money - balance), balance = 0;
        }
        else balance -= money;
    }
    virtual void display()
    {
        cout << name << ' ' << account << ' ' << "Balance:" << balance << ' ';
        cout << "limit:" << limit - limitSum << endl;
    }
};
int main()
{
    int t; 
    string name, account;
    int balance, money;
    BaseAccount *ba;
    for (cin >> t; t--; )
    {
        cin >> name >> account >> balance;
        if (account[1] == 'A')
        {
            BaseAccount baa(name, account, balance);
            ba = &baa;
            for (int j = 0; j < 4; j++)
            {
                cin >> money;
                if (j % 2) ba->withdraw(money);
                else ba->deposit(money);
            }
            ba->display();
        }
        else
        {
            BasePlus bap(name, account, balance);
            ba = &bap;
            for (int j = 0; j < 4; j++)
            {
                cin >> money;
                if (j % 2) ba->withdraw(money);
                else ba->deposit(money);
            }
            ba->display();
        }

        
    }
    return 0;
}



//D
#include <bits/stdc++.h>
using namespace std;
class Group
{
public:
    virtual int add(int x, int y) = 0;
    virtual int sub(int x, int y) = 0;
};
class GroupA : public Group
{
public:
    virtual int add(int x, int y) {return x + y;}
    virtual int sub(int x, int y) {return x - y;}
};
class GroupB : public GroupA
{
public:
    virtual int sub(int x, int y)
    {
        string ans;
        if (x < y) swap(x, y);
        while (x)
        {
            ans = to_string((x % 10 + 10 - y % 10) % 10) + ans;
            x /= 10; y /= 10;
        }
        return atoi(ans.c_str());
    }
};
class GroupC : public GroupB
{
public:
    virtual int add(int x, int y)
    {
        string ans;
        if (x < y) swap(x, y);
        while (x)
        {
            ans = to_string((x % 10 + y % 10) % 10) + ans;
            x /= 10; y /= 10;
        }
        return atoi(ans.c_str());
    }
};
int main()
{
    int t, op, x, y;
    char ch;
    Group *g;
    for (cin >> t; t--; )
    {
        cin >> op;
        scanf("%d%c%d", &x, &ch, &y);
        if (op == 1)
        {
            GroupA ga;
            g = &ga;
            if (ch == '+') cout << g->add(x, y);
            else cout << g->sub(x, y);
        }
        else if (op == 2)
        {
            GroupB gb;
            g = &gb;
            if (ch == '+') cout << g->add(x, y);
            else cout << g->sub(x, y);
        }
        else if (op == 3)
        {
            GroupC gc;
            g = &gc;
            if (ch == '+') cout << g->add(x, y);
            else cout << g->sub(x, y);
        }
        cout << endl;
    }
    return 0;
}



//E
#include <bits/stdc++.h>
using namespace std;
class Animal
{
protected:
    int age;
    string name;
public:
    Animal(int age_, string name_) : age(age_), name(name_) {}
    virtual void Speak() = 0;
};
class Tiger : public Animal
{
public:
    Tiger(int age_, string name_) : Animal(age_, name_) {}
    virtual void Speak() {cout << "Hello,I am " << name << ",AOOO." << endl;}
};
class Dog : public Animal
{
public:
    Dog(int age_, string name_) : Animal(age_, name_) {}
    virtual void Speak() {cout << "Hello,I am " << name << ",WangWang." << endl;}
};
class Duck : public Animal
{
public:
    Duck(int age_, string name_) : Animal(age_, name_) {}
    virtual void Speak() {cout << "Hello,I am " << name << ",GAGA." << endl;}
};
class Pig : public Animal
{
public:
    Pig(int age_, string name_) : Animal(age_, name_) {}
    virtual void Speak() {cout << "Hello,I am " << name << ",HENGHENG." << endl;}
};
int main()
{
    int t;
    Animal *a;
    for (cin >> t; t--; )
    {
        string type, name;
        int age;
        cin >> type >> name >> age;
        if (type == "Tiger")
        {
            Tiger t(age, name);
            a = &t;
            a->Speak();
        }
        else if (type == "Pig")
        {
            Pig p(age, name);
            a = &p;
            a->Speak();
        }
        else if (type == "Dog")
        {
            Dog d(age, name);
            a = &d;
            a->Speak();
        }
        else if (type == "Duck")
        {
            Duck d(age, name);
            a = &d;
            a->Speak();
        }
        else 
        cout << "There is no " << type << " in our Zoo." << endl;
    }
    return 0;
}
```

23.5.26

总结：

菱形继承

代码

```C++
//A
#include <bits/stdc++.h>
using namespace std;
class Student
{
protected:
    string name;
    string type;
    int courses[3];
    string courseGreade;
public:
    Student(string n, int t, int a1, int a2, int a3) : name(n)
    {
        courses[0] = a1; courses[1] = a2; courses[2] = a3;
        if (t == 1) type = "本科生";
        else type = "研究生";
    }
    virtual void calculateGrade() = 0;
    void print()
    {
        cout << name << ',' << type << ',' << courseGreade << endl;
    }
};
class Undergraduate : public Student
{
public:
    Undergraduate(string n, int t, int a1, int a2, int a3) : Student(n, t, a1, a2, a3) {}
    virtual void calculateGrade()
    {
        int ret = (courses[0] + courses[1] + courses[2]);
        ret /= 3;
        if (ret > 80) courseGreade = "优秀";
        else if (ret > 70 && ret <= 80) courseGreade = "良好";
        else if (ret > 60 && ret <= 70) courseGreade = "一般";
        else if (ret > 50 && ret <= 60) courseGreade = "及格";
        else courseGreade = "不及格";
    }
};
class Postgraduate : public Student
{
public:
    Postgraduate(string n, int t, int a1, int a2, int a3) : Student(n, t, a1, a2, a3) {}
    virtual void calculateGrade()
    {
        int ret = (courses[0] + courses[1] + courses[2]);
        ret /= 3;
        if (ret > 90) courseGreade = "优秀";
        else if (ret > 80 && ret <= 90) courseGreade = "良好";
        else if (ret > 70 && ret <= 80) courseGreade = "一般";
        else if (ret > 60 && ret <= 70) courseGreade = "及格";
        else courseGreade = "不及格";
    }
};
int main()
{
    Student *s;
    int n; cin >> n;
    string name;
    int type, a1, a2, a3;
    for (int i = 0; i < n; i++)
    {
        cin >> name >> type >> a1 >> a2 >> a3;
        if (type == 1)
        {
            Undergraduate u(name, type, a1, a2, a3);
            s = &u;
            s->calculateGrade();
            s->print();
        }
        else
        {
            Postgraduate p(name, type, a1, a2, a3);
            s = &p;
            s->calculateGrade();
            s->print();
        }
    }
    return 0;
}



//B
//这道题涉及到类的多重继承，CPeople作为基类派生出CStudent和CTeacher，然后由这两个子类共同派生出CGradOnWork类。
//问题是CStudent和CTeacher都分别继承了CPeople的属性，而CGradOnWork同时把它们相同的属性都继承了，这就导致了CGradOnWork在访问CPeople的属性时会不知道是去找CStudent的还是去找CTeacher的。
//因此，需要在父类继承的时候加上virtual修饰，这样多重继承的时候就只会继承一个相同的属性。
//还有一个问题就是在多重继承的类的构造函数带参数的时候，需要把所有父辈的构造函数的参数带上，包括祖辈的。
#include <bits/stdc++.h>
using namespace std;
class CPeople
{
protected:
    string name;
    char gender;
    int age;
public:
    CPeople(string name_, char gender_, int age_) : name(name_), gender(gender_), age(age_) {}
    void print() {cout << "People:" << endl << "Name: " << name << endl <<  "Sex: " << gender << endl <<  "Age: " << age << endl << endl;}
};
class CStudent : virtual public CPeople
{
protected:
    string id;
    double grade;
public:
    CStudent(string name_, char gender_, int age_, string id_, double grade_) : CPeople(name_, gender_, age_), id(id_), grade(grade_) {}
    void print() {cout << "Student:" << endl << "Name: " << name << endl <<  "Sex: " << gender << endl <<  "Age: " << age << endl << "No.: " << id << endl << "Score: " << grade << endl << endl;}

};
class CTeacher : virtual public CPeople
{
protected:
    string work;
    string room;
public:
    CTeacher(string name_, char gender_, int age_, string work_, string room_) : CPeople(name_, gender_, age_), work(work_), room(room_) {}
    void print() {cout << "Teacher:" << endl << "Name: " << name << endl <<  "Sex: " << gender << endl <<  "Age: " << age << endl << "Position: " << work << endl << "Department: " << room << endl << endl;}
};
class CGradOnWord : public CTeacher, public CStudent
{
protected:
    string item;
    string teacher;
public:
    CGradOnWord(string name_, char gender_, int age_, string id_, double grade_, string work_, string room_, string item_, string teacher_) : CPeople(name_, gender_, age_), CStudent(name_, gender_, age_, id_, grade_), CTeacher(name_, gender_, age_, work_, room_), item(item_), teacher(teacher_) {}
    void print() {cout << "GradOnWork:" << endl << "Name: " << name << endl <<  "Sex: " << gender << endl <<  "Age: " << age << endl << "No.: " << id << endl << "Score: " << grade << endl << "Position: " << work << endl << "Department: " << room << endl << "Direction: " << item << endl << "Tutor: " << teacher << endl << endl;}
};
int main()
{
    string name, id, work, room, item, teacher;
    char gender;
    double grades; int age;
    cin >> name >> gender >> age >> id >> grades >> work >> room >> item >> teacher;
    CPeople p(name, gender, age);
    p.print();
    CStudent s(name, gender, age, id, grades);
    s.print();
    CTeacher t(name, gender, age, work, room);
    t.print();
    CGradOnWord g(name ,gender, age, id, grades, work, room, item, teacher);
    g.print();
    return 0;
}



//C
#include <bits/stdc++.h>
using namespace std;
class CVehicle
{
protected:
    int max_speed, speed, weight;
public:
    CVehicle(int ms, int s, int w) : max_speed(ms), speed(s), weight(w) {};
    void display() {cout << "Vehicle:" << endl << "max_speed:" << max_speed << endl << "speed:" << speed << endl << "weight:" << weight << endl << endl;}
};
class CBicycle : virtual public CVehicle
{
protected:
    int height;
public:
    CBicycle(int ms, int s, int w, int h) : CVehicle(ms, s, w), height(h) {}
    void display() {cout << "Bicycle:" << endl << "max_speed:" << max_speed << endl << "speed:" << speed << endl << "weight:" << weight << endl << "height:" << height << endl << endl;}
};
class CMotomcar : virtual public CVehicle
{
protected:
    int seat_num;
public:
    CMotomcar(int ms, int s, int w, int sn) : CVehicle(ms, s, w), seat_num(sn) {}
    void display() {cout << "Motocar:" << endl << "max_speed:" << max_speed << endl << "speed:" << speed << endl << "weight:" << weight << endl << "seat_num:" << seat_num << endl << endl;}
};
class CMotocycle : public CBicycle, public CMotomcar
{
public:
    CMotocycle(int ms, int s, int w, int h, int sn) : CVehicle(ms, s, w), CBicycle(ms, s, w, h), CMotomcar(ms, s, w, sn) {}
    void display() {cout << "Motocycle:" << endl << "max_speed:" << max_speed << endl << "speed:" << speed << endl << "weight:" << weight << endl << "height:" << height << endl << "seat_num:" << seat_num << endl << endl;}
};
int main()
{
    int max_speed, speed, weight, height, seat_num;
    cin >> max_speed >> speed >> weight >> height >> seat_num;
    CVehicle cv(max_speed, speed, weight);
    cv.display();
    CBicycle cb(max_speed, speed, weight, height);
    cb.display();
    CMotomcar cm(max_speed, speed, weight, seat_num);
    cm.display();
    CMotocycle cmc(max_speed, speed, weight, height, seat_num);
    cmc.display();
    return 0;
}



//D
#include <bits/stdc++.h>
using namespace std;

class vip
{
protected:
    int num, points;
public:
    vip() : points(0) {}
    vip(int n) : num(n), points(0) {}
};

class credit
{
protected:
    int num2, limit;
    int points2;
    string name;
    double money;
public:
    credit() : money(0), points2(0) {}
    credit(int n, string na, int l) : num2(n), name(na), limit(l), points2(0) {}
};

class vipcredit : public vip, public credit
{
public:
    vipcredit(int n, int n2, string s, int l) : vip(n), credit(n2, s, l) {}
    void refund(double m)
    {
        if (m <= money)
        {
            money -= m;
            points2 -= (int)m;
        }
    }
    void order(double m)
    {
        points += (int)m;
        points2 += (int)m;
        money += m;
    }
    void consume(double m)
    {
        if (m + money <= limit)
        {
            money += m;
            points2 += (int)m;
        }
    }
    void exchange(double m)
    {
        if (m <= points2)
        {
            points2 -= (int)m;
            points += (int)m / 2;
        }
    }
    void display()
    {
        cout << num << " " << points << endl;
        cout << num2 << " " << name << " " << money << " " << points2 << endl;
    }
};

int main()
{
    int num, num2, limit, n;
    string name, command;

    cin >> num >> num2 >> name >> limit >> n;
    vipcredit v(num, num2, name, limit);
    while (n--)
    {
        double m;
        cin >> command >> m;
        if (command == "o") v.order(m);
        else if (command == "c") v.consume(m);
        else if (command == "q") v.refund(m);
        else if (command == "t") v.exchange(m);
    }
    v.display();
    return 0;
}


//E
#include <bits/stdc++.h>
using namespace std;
class CPeople
{
	protected:
		char id[20],name[10];
	public:
		CPeople(){}
}; 
class CInternetUser:public CPeople
{
	protected:
		char password[20];
	public:
		CInternetUser(){}
		void registerUser(char *name,char * id,char * password)
		{
			strcpy(this->id,id);
			strcpy(this->name,name);
			strcpy(this->password,password);
		}
		bool login(char *id,char *password)
		{
			return (!strcmp(this->id,id))&&(!strcmp(this->password,password));
		}
}; 
class CBankCustomer:public CPeople
{
	protected:
		double balance=0;
	public:
		CBankCustomer(){}
		void openAccount(char *name,char *id)
		{
			strcpy(this->name,name);
			strcpy(this->id,id);
		}
		void deposit(double money){balance+=money;}
		bool withdraw(double money)
		{
			if(money>balance)
			return 0;
			balance-=money;	
			return 1;		
		}		
};
class CInternetBankCustomer:public CBankCustomer,public CInternetUser
{
	protected:
		double balance=0,lastbalance=0,todayprofit,interest,lastinterest=0;
	public:
		CInternetBankCustomer(){}
		void setInterest(double interest)
		{
			lastinterest=this->interest;
			this->interest=interest;
		}
		void calculateProfit()
		{
			todayprofit=lastbalance*lastinterest*0.0001;
			balance+=todayprofit;
			lastbalance=balance;
		}
		bool login(char * id,char *password)
		{
			return (!strcmp(id,CInternetUser::id))&&(!strcmp(password,this->password))&&(!strcmp(CBankCustomer::name,CInternetUser::name))&&(!strcmp(CBankCustomer::id,CInternetUser::id));
		}
		bool deposit(double money)
		{
			if(money>CBankCustomer::balance)
			return 0;
			balance+=money;
			CBankCustomer::withdraw(money);
			return 1;			
		}
		bool withdraw(double money)
		{
			if(money>balance)
			return 0;
			balance-=money;
			CBankCustomer::deposit(money);	
			return 1;			
		}		
		void print()
		{
			cout<<"Name: "<<CBankCustomer::name<<" ID: "<<CBankCustomer::id<<endl<<"Bank balance: "<<CBankCustomer::balance<<endl<<"Internet bank balance: "<<balance<<endl;
		}
};
int main() {
    int t, no_of_days, i;
    char i_xm[10], i_id[20], i_mm[20], b_xm[10], b_id[20], ib_id[20], ib_mm[20];
    double money, interest;char op_code;//输入测试案例数t
    cin >> t;
    while (t--){//输入互联网用户注册时的用户名,id,登陆密码
       cin >> i_xm >> i_id >> i_mm;//输入银行开户用户名,id
       cin >> b_xm >> b_id;//输入互联网用户登陆时的id,登陆密码
       cin >> ib_id >> ib_mm;
       CInternetBankCustomer ib_user;
       ib_user.registerUser(i_xm, i_id, i_mm);
       ib_user.openAccount(b_xm, b_id);
       if (!ib_user.login(ib_id, ib_mm)) //互联网用户登陆,若id与密码不符;以及银行开户姓名和id与互联网开户姓名和id不同
        { cout << "Password or ID incorrect" << endl;
          continue;
        }//输入天数
        cin >> no_of_days;
        for (i=0; i < no_of_days; i++){//输入操作代码, 金额, 当日万元收益
          cin >> op_code >> money >> interest;
          switch (op_code){
              case 'S': //从银行向互联网金融帐户存入
              case 's': if (!ib_user.deposit(money)){
                            cout << "Bank balance not enough" << endl;
                            continue;
                         }
                         break;
               case 'T': //从互联网金融转入银行帐户
               case 't':if (!ib_user.withdraw(money)){
                            cout << "Internet bank balance not enough" << endl;
                            continue;
                         }
                         break;
               case 'D': //直接向银行帐户存款
               case 'd':ib_user.CBankCustomer::deposit(money);
                        break;
               case 'W': //直接从银行帐户取款
               case 'w':if (!ib_user.CBankCustomer::withdraw(money)){
                            cout << "Bank balance not enough" << endl;
                            continue;
                        }
                        break;
               default:cout << "Illegal input" << endl;
                       continue;
           }
           ib_user.setInterest(interest);
           ib_user.calculateProfit();//输出用户名,id//输出银行余额 //输出互联网金融账户余额
           ib_user.print();
           cout << endl;
        }
    }
    return 0;
}
```

23.6.2

总结

**类的操作符重载**

关于前缀++和后缀++的返回类型是`const` 或者是引用类型`&` , 大概率是根据需求, 但是又或许有所规范, 结合实际应用场景吧!

```C++
#include <bits/stdc++.h>
using namespace std;
class Distance
{
private:
	int feet, inches;
	int arr[10];
public:
	Distance() {feet = inches = 0;}
	Distance(int f, int i)
	{
		feet = f; inches = i;
		for (int i = 0; i < 10; i++) arr[i] = i;
	}
	int dis() {return feet * inches;}
	//重载负运算符（-）
	Distance operator-()
	{
		Distance temp = *this;
		temp.feet = -feet;
		temp.inches = -inches;
		return temp;
	}
	//重载加运算符（+）
	Distance operator+(const Distance d)
	{
		Distance temp = *this;
		temp.feet += d.feet;
		temp.inches += d.inches;
		return temp;
	}
	//重载减运算符（ - ）
	Distance operator-(const Distance d)
	{
		Distance temp = *this;
		temp.feet -= d.feet;
		temp.inches -= d.inches;
		return temp;
	}
	//重载乘运算符（*）
	Distance operator*(const Distance d)
	{
		Distance temp = *this;
		temp.feet *= d.feet;
		temp.inches *= d.inches;
		return temp;
	}
	//重载除运算符（/）
	Distance operator/(const Distance d)
	{
		Distance temp = *this;
		temp.feet /= d.feet;
		temp.inches /= d.inches;
		return temp;
	}
	//重载前缀递增运算符（++），前缀--同理
	Distance& operator++()
	{
		feet++; inches++;
		return *this;
	}
	//重载后缀递增运算符（++）， 后缀--同理
	const Distance operator++(int)
	{
		Distance temp = *this;
		++*this;
		return temp;
	}
	//重载关系运算符（<），>, <=, >=, == 同理
	bool operator<(Distance& d)   //此处的Distance&可以写成Distance即可
	{
		return this->dis() < d.dis();
	}
	//重载赋值运算符（=）
	void operator=(const Distance &d)
	{
		feet = d.feet;
		inches = d.inches;
	}
	//重载调用运算符（）
	void operator()()
	{
		cout << "This distance object is " << feet << " feet" << " and " << inches << " inches." << endl; 
	}
	//重载下标运算符[]
	int& operator[](unsigned int i)
	{
		//You can check whether the i is out of the size or not.
		if (i > sizeof(arr))
		{
			cout << "Error!" << endl;
			return arr[0];
		}
		return arr[i];
	}
	//重载逻辑非运算符
	bool operator!()
	{
		if (feet <= 0 || inches <= 0) return true;
		return false;
	}
	//输入输出运算符重载
	friend istream& operator>>(istream &input, Distance &d)
	{
		input >> d.feet >> d.inches;
		return input;
	}
	friend ostream& operator<<(ostream &output, Distance &d)
	{
		output << d.feet << ' ' << d.inches << ' ';
		return output;
	}
};
int main()
{
	Distance d1(2, 3), d2(3, 4);
	cout << d1 << d2 << endl;
	Distance d3 = -d1;
	cout << d3 << endl;
	Distance d4 = d1 + d2;
	cout << d4 << endl;
	d4 = d2 - d1;
	cout << d4 << endl;
	d4 = d2 * d1;
	cout << d4 << endl;
	d4 = d1 * d2 / d1;
	cout << d4 << endl;
	if (d1 < d2) {cout << "d1 < d2" << endl;}
	// Distance d5;
	// cin >> d5;
	// cout << d5 << endl;
	d1 = d2;
	cout << d1 << endl;
	cout << ++d1 << endl;
	d1();
	cout << d1[3] << endl;
	d1 = -d1;
	if (!d1) cout << "It is not narrow" << endl;
	return 0;
}
```

代码实现

```C++
//A
#include <bits/stdc++.h>
using namespace std;
class myclock
{
	int hour, minute, second;
public:
	myclock(int hour, int minute, int second) : hour(hour), minute(minute), second(second) {}
	myclock& operator++()
	{
		second++;
		if (second > 59) {second = 0; minute++;}
		if (minute > 59) {minute = 0; hour++;}
		if (hour > 11) {hour = 0;}
		return *this;
	}
	myclock operator--(int)
	{
		myclock temp(hour, minute, second);
		second--;
		if (second < 0) {second = 59; minute--;}
		if (minute < 0) {minute = 59; hour--;}
		if (hour < 0) {hour = 11;}
		return temp;
	}
	void print()
	{
		cout << hour << ":" << minute << ":" << second << endl;
	}
};
int main()
{
	int hour, minute, second, t, cnt;
	cin >> hour >> minute >> second;
	myclock mc(hour, minute, second);
	for (cin >> t; t--; )
	{
		cin >> cnt;
		if (cnt > 0)
		{
			for ( ; cnt--; ++mc);
			mc.print();
		}
		else
		{
			for (cnt = -cnt; cnt--; mc--);
			mc.print();
		}
	}
	return 0;
}


//B
#include <bits/stdc++.h>
using namespace std;

// 定义矩阵类
class CMatrix
{
private:
    int n, m; // n-行，m-列
    int** data; // 存储矩阵数据
public:
    CMatrix()
	{
		n = m = 0;
		data = NULL;
	}
    CMatrix(int n1, int m1);
	CMatrix &operator = (const CMatrix &a)
	{
		if (data != NULL)
		{
			for (int i = 0; i < n; i++)
				delete []data[i];
			delete []data;
		}
		n = a.n; m = a.m;
		data = new int*[n];
		for (int i = 0; i < n; i++)
			data[i] = new int[m];
		for (int i = 0; i < n; i++)
			for (int j = 0; j < m; j++)
				data[i][j] = a.data[i][j];
		return *this;
	}
	int *const operator[] (const int k)
	{
		return data[k];
	}
	int operator() (int i, int j)
	{
		return data[i][j];
	}
    ~CMatrix();
};

CMatrix::CMatrix(int n1, int m1)
{
    n = n1;
    m = m1;
    // 分配n行m列的二维数组空间
    data = new int* [n];
    for (int i = 0; i < n; i++)
    {
        data[i] = new int[m];
    }
}

CMatrix::~CMatrix()
{
    // 释放空间
    for (int i = 0; i < n; i++)
    {
        delete[] data[i];
    }
    delete[] data;
}

int main()
{
    int t, n, m, i, j;
    cin >> t;
    while (t--)
    {
        cin >> n >> m;
        // 定义矩阵对象matrixA
        CMatrix matrixA(n, m);
        for (i = 0; i < n; i++)
        {
            for (j = 0; j < m; j++)
            {
                // 输入第i行第j列的数据
                cin >> matrixA[i][j];
            }
        }
        // 输出matrixA中的数据
        cout << "matrixA:" << endl;
        for (i = 0; i < n; i++)
        {
            for (j = 0; j < m; j++)
            {
                cout << matrixA(i, j) << " ";
            }
            cout << endl;
        }
        // 定义矩阵对象matrixB
        CMatrix matrixB;
        matrixB = matrixA;
        // 输出marixB中的数据
        cout << "matrixB:" << endl;
        for (i = 0; i < n; i++)
        {
            for (j = 0; j < m; j++)
            {
                cout << matrixB[i][j] << " ";
            }
            cout << endl;
        }
    }
    return 0;
}



//C
#include <bits/stdc++.h>
using namespace std;

class CPoint
{
	int x, y;
public:
	CPoint() {}
	CPoint(int x, int y) : x(x), y(y) {}
	int getX() {return x;}
	int getY() {return y;}
	bool operator == (const CPoint &cp)
	{
		return x == cp.x && y == cp.y;
	}
};
class CRectangle
{
private:
	CPoint leftPoint, rightPoint;
public:
	CRectangle () {}
	CRectangle(int x1, int y1, int x2, int y2) : leftPoint(x1, y1), rightPoint(x2, y2) {}
	bool operator > (CPoint & c)
	{
		return c.getY() >= rightPoint.getY() && c.getY() <= leftPoint.getY() && c.getX() >= leftPoint.getX() && c.getX() <= rightPoint.getX();
	}
	bool operator > (CRectangle &c)
	{
		return *this > c.leftPoint && *this > c.rightPoint;
	}
	bool operator == (CRectangle &c)
	{
		return leftPoint == c.leftPoint && rightPoint == c.rightPoint;
	}
	bool operator * (CRectangle &c)
	{
		return !(c.rightPoint.getY() > leftPoint.getY() || c.leftPoint.getY() < rightPoint.getY() || c.leftPoint.getX() > rightPoint.getX() || c.rightPoint.getX() < leftPoint.getX());
	}
	operator int()
	{
		return (leftPoint.getY() - rightPoint.getY()) * (rightPoint.getX() - leftPoint.getX());
	}
	friend ostream& operator << (ostream& os, CRectangle &d)
	{
		os << d.leftPoint.getX() << " " << d.leftPoint.getY() << " " << d.rightPoint.getX() << " " << d.rightPoint.getY();
		return os;
	}
};
int main()
{
    int t, x1, x2, y1, y2;
    cin >> t;
    while (t--)
    {
        // 矩形1的左上角、右下角
        cin >> x1 >> y1 >> x2 >> y2;
        CRectangle rect1(x1, y1, x2, y2);
        // 矩形2的左上角、右下角
        cin >> x1 >> y1 >> x2 >> y2;
        CRectangle rect2(x1, y1, x2, y2);
        // 输出矩形1的坐标及面积
        cout << "矩形1:" << rect1 << " " << (int)rect1 << endl;
        // 输出矩形2的坐标及面积
        cout << "矩形2:" << rect2 << " " << (int)rect2 << endl;
        if (rect1 == rect2)
        {
            cout << "矩形1和矩形2相等" << endl;
        }
        else if (rect2 > rect1)
        {
            cout << "矩形2包含矩形1" << endl;
        }
        else if (rect1 > rect2)
        {
            cout << "矩形1包含矩形2" << endl;
        }
        else if (rect1 * rect2)
        {
            cout << "矩形1和矩形2相交" << endl;
        }
        else
        {
            cout << "矩形1和矩形2不相交" << endl;
        }
        cout << endl;
    }
    return 0;
}



//D
#include <bits/stdc++.h>
using namespace std;
class CMoney
{
	int yuan, fen, jiao;
public:
	CMoney(int yuan, int jiao, int fen) : yuan(yuan), fen(fen), jiao(jiao) {}
	friend CMoney operator + (CMoney &c1, CMoney &c2)
	{
		int y, j, f;
		y = c1.yuan + c2.yuan;
		f = c1.fen + c2.fen;
		j = c1.jiao + c2.jiao;
		if (f > 9) {f %= 10; j++;}
		if (j > 9) {j %= 10; y++;}
		return CMoney(y, j, f);
	}
	friend CMoney operator - (CMoney &c1, CMoney &c2)
	{
		int y, j, f;
		if (c1.fen < c2.fen) {c1.jiao--; c1.fen += 10;}
		f = c1.fen - c2.fen;
		if (c1.jiao < c2.jiao) {c1.yuan--; c1.jiao += 10;}
		j = c1.jiao - c2.jiao;
		y = c1.yuan - c2.yuan;
		return CMoney(y, j, f);
	}
	void print()
	{
		cout << yuan << "元" << jiao << "角" << fen << "分" << endl;
	}
};
int main()
{
	int t;
	int yuan, jiao, fen;
	string s;
	for (cin >> t; t--; )
	{
		cin >> yuan >> jiao >> fen;
		CMoney cm(yuan, jiao, fen);
		int y, j, f;
		while (cin >> s && s != "stop")
		{
			if (s == "add")
			{
				cin >> y >> j >> f;
				CMoney ret(y, j, f);
				cm = cm + ret;
			}
			else 
			{
				cin >> y >> j >> f;
				CMoney ret(y, j, f);
				cm = cm - ret;
			}
		}
		cm.print();
	}
	return 0;
}




//E
#include <bits/stdc++.h>
using namespace std;
class CXGraph
{
	int w;
public:

	CXGraph(int w) : w(w) {}
	CXGraph& operator++()
	{
		if (w < 21) w += 2;
		return *this;
	}
	CXGraph& operator--()
	{
		if (w > 1) w -= 2;
		return *this;
	}
	CXGraph operator++(int)
	{
		CXGraph temp(w);
		if (w < 21) this->w += 2;
		return temp;
	}
	CXGraph operator--(int)
	{
		CXGraph temp(w);
		if (w > 1) this->w -= 2;
		return temp;
	}
	friend ostream& operator << (ostream& os, const CXGraph &c)
	{
		for (int i = 0; i < c.w; i++)
		{
			int cnt = c.w / 2 - abs(i - c.w / 2);
			for (int i = 0; i < cnt; i++) os << " ";
			for (int i = 0; i < (c.w - cnt - cnt); i++) os << "X";
			os << endl;
		}
		return os;
	}
};
int main()
{
    int t, n;
    string command;
    cin >> n;
    CXGraph xGraph(n);
    cin >> t;
    while (t--)
    {
        cin >> command;
        if (command == "show++")
        {
            cout << xGraph++ << endl;
        }
        else if(command == "++show")
        {
            cout << ++xGraph << endl;
        }
        else if (command == "show--")
        {
            cout << xGraph-- << endl;
        }
        else if (command == "--show")
        {
            cout << --xGraph << endl;
        }
        else if (command == "show")
        {
            cout << xGraph << endl;
        }
    }
    return 0;
}

```

22.6.9

代码实现

```C++
//A
#include <bits/stdc++.h>
using namespace std;
class Fraction
{
private:
    int fz, fm;
    int commonDivisor(int c1, int c2); // 计算最大公约数
	void contracted() {if (fm < 0) {fz = -fz; fm = -fm;}}
public:
    Fraction(int = 0, int = 1);
    Fraction(Fraction& f)
	{
		this->fz = f.fz;
		this->fm = f.fm;
	}
    Fraction operator+(Fraction f)
	{
		Fraction temp = *this;
		temp.fz = fz * f.fm + fm * f.fz;
		temp.fm = fm * f.fm;
		temp.contracted();
		return temp;
	}
    Fraction operator-(Fraction f)
	{
		Fraction temp = *this;
		temp.fz = fz * f.fm - fm * f.fz;
		temp.fm = fm * f.fm;
		temp.contracted();
		return temp;
	}
    Fraction operator*(Fraction f)
	{
		Fraction temp = *this;
		temp.fz *= f.fz;
		temp.fm *= f.fm;
		temp.contracted();
		return temp;
	}
    Fraction operator/(Fraction f)
	{
		Fraction temp = *this;
		temp.fz *= f.fm;
		temp.fm *= f.fz;
		temp.contracted();
		return temp;		
	}
    void Set(int = 0, int = 1);
	void disp() {cout << "fraction=" << fz << "/" << fm << endl;}
};
Fraction::Fraction(int c1, int c2) : fz(c1), fm(c2) {}
int main()
{
	int a, b, c, d;
	cin >> a >> b >> c >> d;
	Fraction f1(a, b), f2(c, d);
	Fraction f3;
	f3 = f1 + f2;
	f3.disp();
	f3 = f1 - f2; f3.disp();
	f3 = f1 * f2; f3.disp();
	f3 = f1 / f2; f3.disp();
	return 0;
}


//B
#include <bits/stdc++.h>
using namespace std;
class Complex
{
private:
    double real, image;
public:
    Complex(double x = 0, double y = 0);
    friend Complex operator+(Complex& c1, Complex& c2)
	{
		Complex t = c1;
		t.real = c1.real + c2.real;
		t.image = c1.image + c2.image;
		return t;
	}
    friend Complex operator-(Complex& c1, Complex& c2)
	{
		Complex t = c1;
		t.real = c1.real - c2.real;
		t.image = c1.image - c2.image;
		return t;		
	}
    friend Complex operator*(Complex& c1, Complex& c2)
	{
		Complex t = c1;
		t.real = c1.real * c2.real - c1.image * c2.image;
		t.image = c1.image * c2.real + c2.image * c1.real;
		return t;
	}
    void show() {cout << "Real=" << real << " Image=" << image << endl;}
};
Complex::Complex(double r, double i) : real(r), image(i) {}
int main()
{
	double real, image;
	cin >> real >> image; Complex c1(real, image);
	cin >> real >> image; Complex c2(real, image);
	Complex c3;
	c3 = c1 + c2; c3.show();
	c3 = c1 - c2; c3.show();
	c3 = c1 * c2; c3.show();
	return 0;
}



//C
#include <bits/stdc++.h>
using namespace std;
class Point
{
	int x, y, z;
public:
	Point(int x = 0, int y = 0, int z = 0) : x(x), y(y), z(z) {}
	friend Point operator++(Point &a) {a.x++; a.y++; a.z++; return a;}
	friend Point operator++(Point &a, int)
	{
		Point t = a;
		a.x++; a.y++; a.z++;
		return t;
	}
	friend Point operator--(Point &a) {a.x--; a.y--; a.z--; return a;}
	friend Point operator--(Point &a, int)
	{
		Point t = a;
		a.x--; a.y--; a.z--;
		return t;
	}
	void show() {cout << "x=" << x << " y=" << y << " z=" << z << endl;}
};
int main()
{
	int x, y, z; cin >> x >> y >> z;
	Point p1(x, y, z), p2;
	p2 = p1++; p1.show(); p2.show(); p1--;
	p2 = ++p1; p1.show(); p2.show(); p1--;
	p2 = p1--; p1.show(); p2.show(); p1++; 
	p2 = --p1; p1.show(); p2.show(); p1++;
	return 0;
}



//D
#include <bits/stdc++.h>
using namespace std;

// 定义矩阵类
class CMatrix
{
private:
    int n, m; // n-行，m-列
    int** data; // 存储矩阵数据
public:
    CMatrix()
	{
		n = m = 0;
		data = NULL;
	}
    CMatrix(int n1, int m1);
	CMatrix &operator = (const CMatrix &a)
	{
		if (data != NULL)
		{
			for (int i = 0; i < n; i++)
				delete []data[i];
			delete []data;
		}	
		n = a.n; m = a.m;
		data = new int*[n];
		for (int i = 0; i < n; i++)
			data[i] = new int[m];
		for (int i = 0; i < n; i++)
			for (int j = 0; j < m; j++)
				data[i][j] = a.data[i][j];
		return *this;
	}
	friend CMatrix operator*(CMatrix &a, CMatrix &b)
	{
		int n = a.n;
		CMatrix t(n, n);
		for (int i = 0; i < n; i++)
		{
			for (int j = 0; j < n; j++)
			{
				int sum = 0;
				for (int k = 0; k < n; k++)
				sum += a[i][k] * b[k][j];
				t[i][j] = sum;
			}
		}
		return t;
	}
	int *const operator[] (const int k)
	{
		return data[k];
	}
	int operator() (int i, int j)
	{
		return data[i][j];
	}
	friend ostream& operator<<(ostream &output, CMatrix c)
	{
		for (int i = 0; i < c.n; i++)
		{
			for (int j = 0; j < c.n; j++) cout << c[i][j] << " \n"[j == c.n - 1];
		}
		return output;
	}
    // ~CMatrix();
};

CMatrix::CMatrix(int n1, int m1)
{
    n = n1;
    m = m1;
    // 分配n行m列的二维数组空间
    data = new int* [n];
    for (int i = 0; i < n; i++)
        data[i] = new int[m];
	for (int i = 0; i < n; i++)
		for (int j = 0; j < n; j++)
			data[i][j] = (i == j);
}

// CMatrix::~CMatrix()
// {
//     // 释放空间
//     for (int i = 0; i < n; i++)
//     {
//         delete[] data[i];
//     }
//     delete[] data;
// }

int main()
{
    int t, n;
    cin >> t >> n;
	CMatrix e(n, n);
    while (t--)
    {
        CMatrix matrixA(n, n);
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                cin >> matrixA[i][j];
            }
        }
		e = e * matrixA;
    }
	cout << e;
    return 0;
}



//E
#include <bits/stdc++.h>
using namespace std;
int check(int y)
{
	if (y % 4 == 0 && y % 100 || y % 400) return true;
	return false;
}
int mon[12] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
class Student
{
	int id;
	string name;
	int year, month, day;
public:
	Student() {}
	Student(string name_, int y, int m, int d, int i) : name(name_), year(y), month(m), day(d), id(i) {}
	int cal()
	{
		int sum = 0;
		for (int i = 1; i < year; i++) sum += check(year) + 365;
		for (int i = 0; i < month; i++) sum += mon[i];
		if (month > 2 && check(year)) sum++;
		sum += day;
		return sum;
	}
	friend int operator-(Student &s1, Student &s2)
	{
		return s1.cal() - s2.cal();
	}
	bool operator<(const Student s)
	{
		if (year != s.year) return year < s.year;
		else if (month != s.month) return month < s.month;
		else return day < s.day;
	}
	static void print(Student s1, Student s2)
	{
		if (s1.id > s2.id) swap(s1.name, s2.name);
		cout << s1.name << "和" << s2.name << "年龄相差最大，为" << (s2 - s1 - 1) << "天。" << endl;
	}
};
int main()
{
	string name; int year, month, day;
	int n; cin >> n;
	Student *p;
	p = (Student*) operator new(n * sizeof(Student));
	for (int i = 0; i < n; i++)
	{
		cin >> name >> year >> month >> day;
		new(&p[i]) Student(name, year, month, day, i);
	}
	sort(p, p + n);
	Student::print(p[0], p[n - 1]);
	return 0;
}
```

23.6.16

**类模板和函数模板**

```
template< > 
```

代码实现

```C++
//A
#include <iostream>
using namespace std;
template<class T>
void findout(int n)
{
	T* a = new T[n];
	for (int i = 0; i < n; i++) cin >> a[i];
	T key;  cin >> key;
	for (int i = 0; i < n; i++)
	{
		if (a[i] == key)
		{
			cout << i + 1 << endl;
			break;
		}
		if (i == n - 1) cout << "0" << endl;
	}
}
int main()
{
	int t, n; 
	char ch;
	for (cin >> t; t--; )
	{
		cin >> ch >> n;
		if (ch == 'I') findout<int>(n);
		else if (ch == 'D') findout<double>(n);
		else if (ch == 'C') findout<char>(n);
		else if (ch == 'S') findout<string>(n);
	}
	return 0;
}


//B
#include <iostream>
#include <map>
#include <algorithm>
using namespace std;
template<class T>
void Judge(int n)
{
	T* a = new T[n];
	map<T, int> ma;
	T ret;
	for (int i = 0; i < n; i++)
	{
		cin >> ret;
		ma[ret]++;
	}
	int maxn = 0;
	for (auto v : ma)
	{
		if (v.second > maxn)
		{
			maxn = v.second;
			ret = v.first;
		}
	}
	cout << ret << " " << ma[ret] << endl;
}
int main()
{
	int t, n;
	char ch;
	for (cin >> t; t--; )
	{
		cin >> ch >> n;
		if (ch == 'I') Judge<int>(n);
		else if (ch == 'C') Judge<char>(n);
		else if (ch == 'S') Judge<string>(n);
	}
	return 0;
}


//C
#include <iostream>
#include <map>
#include <algorithm>
using namespace std;
template<class T>
void check()
{
	T* a = new T[6];
	for (int i = 0; i < 6; i++) cin >> a[i];
	for (int i = 0; i < 6; i++)
	{
		if (a[i] < a[i - 1])
		{
			cout << "Invalid" << endl;
			break;
		}
		if (i == 5) cout << "Valid" << endl;
	}
	delete[]a;
}
int main()
{

	char ch;
	while (cin >> ch)
	{
		if (ch == 'i') check<int>();
		else if (ch == 'f') check<double>();
		else if (ch == 'c') check<char>();
	}
	return 0;
}



//D
#include <bits/stdc++.h>
using namespace std;
template<typename T>
class CMatrix
{
private:
    int n, m;
    T** data; 
public:
    CMatrix()
	{
		n = m = 0;
		data = NULL;
	}
    CMatrix(int n1, int m1)
	{
    	n = n1;
    	m = m1;
		data = new T* [n];
		for (int i = 0; i < n; i++) data[i] = new T[m];
		for (int i = 0; i < n; i++)
			for (int j = 0; j < m; j++)
				cin >> data[i][j];
	}
	void transpose()
	{
		int tn = m, tm = n;
		T** tdata;
		tdata = new T*[tn];
		for (int i = 0; i < tn; i++) tdata[i] = new T[tm];
		for (int i = 0; i < tn; i++)
			for (int j = 0; j < tm; j++)
				tdata[i][j] = data[j][i];
		data = tdata;
		n = tn; m = tm;
	}
	void print()
	{
		for (int i = 0; i < n; i++)
			for (int j = 0; j < m; j++)
				cout << data[i][j] << " \n"[j == m - 1];
	}
    ~CMatrix()
	{
		for (int i = 0; i < n; i++)
		{
			delete[] data[i];
		}
		delete[] data;
	}
};
int main()
{
    int t, n, m;
	char ch;
	for (cin >> t; t--; )
	{
		cin >> ch >> n >> m;
		if (ch == 'I') {CMatrix<int> ma(n, m); ma.transpose(); ma.print();}
		else if (ch == 'C') {CMatrix<char> ma(n, m); ma.transpose(); ma.print();}
		else if (ch == 'D') {CMatrix<double> ma(n, m); ma.transpose(); ma.print();}
	}
    return 0;
}

//E
#include <bits/stdc++.h>
using namespace std;
template<typename T>
class List
{
private:
	T arr[100];
	int n;
public:
	List(int _n) : n(_n) 
	{
		for (int i = 0; i < n; i++) cin >> arr[i];
		for (int i = n; i < 100; i++) arr[i] = -1;
	}
	void Insert()
	{
		int pos; T key; cin >> pos >> key;
		n++;
		for (int i = n - 1; i > pos; i--) arr[i] = arr[i - 1];
		arr[pos] = key;
	}
	void Delete()
	{
		int pos; cin >> pos;
		n--;
		for (int i = pos; i < n; i++) arr[i] = arr[i + 1];
	}
	void Print()
	{
		for (int i = 0; i < n; i++) cout << arr[i] << " \n"[i == n - 1]; 
	}
};
int main()
{
	int n;
	cin >> n;
	List<int> li(n);
	li.Insert(); li.Delete(); li.Print();
	cin >> n;
	List<double> ld(n);
	ld.Insert(); ld.Delete(); ld.Print();
	return 0;
	
}
```

22.6.23

代码实现

```C++
//A
#include <bits/stdc++.h>
using namespace std;
class Audio
{
private:
	int type;
	string name;
	int price;
	bool status;
public:
	Audio(int t, string na, int p, bool s) : type(t), name(na), price(p), status(s) {}
	void query(int op)
	{
		if (op == 0) show();
		else
		{
			show();
			if (status == 0) cout << "未产生租金" << endl;
			else cout << "当前租金为" << price * op << endl; 
		}
	}
	void show()
	{
		string s[5] = {" ", "黑胶片", "CD", "VCD", "DVD"};
		cout << s[type] << "[" << name << "]";
		if (status == 0) cout << "未出租" << endl;
		else cout << "已出租" << endl;
	}
};
int main()
{
	int t, op;
	int type, price;
	string name;
	bool status;
	for (cin >> t; t--; )
	{
		cin >> type >> name >> price >> status >> op;
		Audio au(type, name, price, status);
		au.query(op);
	}
	return 0;
}


//B
#include <bits/stdc++.h>
using namespace std;
class Data
{
protected:
	int year, month, day;
public:
	Data(int y, int m, int d) : year(y), month(m), day(d) {}
};
class Time
{
protected:
	int hour, minute, second;
public:
	Time(int h, int m, int s) : hour(h), minute(m), second(s) {}
};
class Work : public Data, Time
{
	int id;
public:
	Work(int i, int y, int m, int d, int h, int mi, int s) : id(i), Data(y, m, d), Time(h, mi, s) {}
	bool operator < (const Work w) const
	{
		if (year != w.year) return year < w.year;
		else if (month != w.month) return month < w.month;
		else if (day != w.day) return day < w.day;
		else if (hour != w.hour) return hour < w.hour;
		else if (minute != w.minute) return minute < w.minute;
		else if (second != w.second) return second < w.second;
		return id < w.id;
	}
	void show()
	{
		printf("No.%d: %d/%.2d/%.2d %.2d:%.2d:%.2d\n", id, year, month, day, hour, minute, second);
	}
};
int main()
{
	int id, year, month, day, hour, minute, second;
	vector<Work> v;
	while (cin >> id && id)
	{
		cin >> year >> month >> day >> hour >> minute >> second;
		Work w(id, year, month, day, hour, minute, second);
		v.push_back(w);
	}
	sort(v.begin(), v.end());
	cout << "The urgent Work is ";
	v[0].show();
}


//C
#include <bits/stdc++.h>
using namespace std;
class CDate
{
	int year, month, day;
public:
	CDate() {}
	CDate(int y, int m, int d) : year(y), month(m), day(d) {}
	bool operator < (const CDate c) const
	{
		if (year != c.year) return year < c.year;
		else if (month != c.month) return month < c.month;
		else if (day != c.day) return day < c.day;
		return true;
	}
	bool check(int x)
	{
		if (x % 4 == 0 && x % 100 != 0 || x % 400 == 0) return true;
		return false;
	}
	int cal()
	{
		int mon[13] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
		int sum = 0;
		for (int i = 1; i < year; i++) sum += 365 + check(i);
		for (int i = 1; i < month; i++) sum += mon[i];
		sum += day;
		if (check(year) && month > 2) sum++;
		return sum;
	}
	int operator - (CDate c) {return this->cal() - c.cal();}
};
class Pet
{
protected:
	string name;//姓名
	float length;//身长
	float weight;//体重
	CDate current;//开始记录时间
public:
	Pet(string na,  float l, float w, CDate c) : name(na), length(l), weight(w), current(c) {}
	virtual void display(CDate day)=0;//输出目标日期时宠物的身长和体重
};
class Cat : public Pet
{
	float unit[2] = {0.1, 0.2};
public:
	Cat(string na, float l, float w, CDate c) : Pet(na, l, w, c) {}
	virtual void display(CDate day)
	{
		if (day < current) cout << "error" << endl;
		else
		{
			int days = day - current;
			cout << name << " after " << days << " day: ";
			printf("length=%.2f,weight=%.2f\n", days * unit[0] + length, days * unit[1] + weight);
		}
	}
};
class Dog : public Pet
{
	float unit[2] = {0.2, 0.1};
public:
	Dog(string na, float l, float w, CDate c) : Pet(na, l, w, c) {}
	virtual void display(CDate day)
	{
		if (day < current) cout << "error" << endl;
		else
		{
			int days = day - current;
			cout << name << " after " << days << " day: ";
			printf("length=%.2f,weight=%.2f\n", days * unit[0] + length, days * unit[1] + weight);
		}
	}
};
int main()
{
	int t, type, year, month, day;
	string name;
	float length, weight;
	cin >> t >> year >> month >> day;
	CDate bgt(year, month, day);
	Pet *pt;
	while (t--)
	{
		cin >> type >> name >> length >> weight >> year >> month >> day;
		CDate now(year, month, day);
		if (type == 1)
		{
			Cat cat(name, length, weight, bgt);
			pt = &cat;
			(*pt).display(now);
		}
		else
		{
			Dog dog(name, length, weight, bgt);
			pt = &dog;
			(*pt).display(now);
		}
	}
	return 0;
}



//D
#include <bits/stdc++.h>
using namespace std;
class CSet
{
	int n;
	vector<int> ve;
public:
	CSet(int _n) : n(_n)
	{
		for (int i = 0; i < n; i++) 
		{
			int x; cin >> x;
			ve.push_back(x);
		}
	}
	CSet operator + (CSet c)
	{
		CSet ret = *this;
		map<int, bool> ma;
		for (auto v : this->ve) ma[v] = 1;
		for (auto v : c.ve)
		{
			if (ma.find(v) == ma.end())
			{
				ma[v] = 1;
				ret.ve.push_back(v);
			} 
		}
		ret.n = ret.ve.size();
		return ret;
	}
	CSet operator - (CSet c)
	{
		CSet tmp = *this, inte = (*this)*c;
		tmp.ve.clear();
		map<int, bool> ma;
		for (auto v : inte.ve) ma[v] = 1;
		for (auto v : this->ve)
			if (ma.find(v) == ma.end())
				tmp.ve.push_back(v);
		return tmp;
	}
	CSet operator * (CSet c)
	{
		CSet ret = *this;
		map<int, bool> ma;
		for (auto v : c.ve) ma[v] = 1;
		ret.ve.clear();
		for (auto v : this->ve)
			if (ma.find(v) != ma.end())
				ret.ve.push_back(v);
		ret.n = ret.ve.size();
		return ret;
	}
	void print()
	{
		for (vector<int>::iterator v = ve.begin(); v != ve.end(); v++)
			cout << *v << " \n"[v + 1 == ve.end()];
	}
};
int main()
{
	int t;
	int n;
	for (cin >> t; t--; )
	{
		cin >> n; CSet c1(n);
		cin >> n; CSet c2(n);
		cout << "A:"; c1.print();
		cout << "B:"; c2.print();
		cout << "A+B:"; (c1 + c2).print();
		cout << "A*B:"; (c1 * c2).print();
		cout << "(A-B)+(B-A):"; ((c1 - c2) + (c2 - c1)).print();
		cout << endl;
	}
	return 0;
}



//E
#include <bits/stdc++.h>
using namespace std;
class CBook
{
	string name, author, phouse;
	double price;
public:
	CBook() {}
	CBook(string n, string a, string ph, double pr) : name(n), author(a), phouse(ph), price(pr) {}
	bool operator < (const CBook c) const
	{
		return price > c.price;
	}
	friend istream& operator>>(istream &intput, CBook &c)
	{	
		string inf[4];
		for (int i = 0; i < 4; i++) getline(intput, inf[i], i == 3 ? '\n' : ',');
		c = CBook(inf[0], inf[1], inf[3], stod(inf[2]));
		return intput;
	}
	friend void find(CBook *book, int n, int &max1index,int &max2index)
	{
		double m1 = 0, m2 = 0;
		for (int i = 0; i < n; i++)
			if (book[i].price > m1) m1 = book[i].price, max1index = i;
		for (int i = 0; i < n; i++)
			if (book[i].price > m2 && i != max1index) m2 = book[i].price, max2index = i;
	}
	friend ostream& operator<<(ostream &output, CBook c)
	{
		output << c.name << endl << c.author << endl << c.price << endl << c.phouse << endl;
		return output;
	}
};
int main()
{
	int t, n;
    cout << fixed << setprecision(2);
	for (cin >> t; t--; )
	{
		cin >> n;
		CBook *cp;
		cp = new CBook[n];
		int max1index, max2index;
		for (int i = 0; i < n; i++) cin >> cp[i];
		find(cp, n, max1index, max2index);
		cout << cp[max1index] << endl << cp[max2index];
	}
	return 0;
}

```

23.6.25

代码

```C++
//A
#include <bits/stdc++.h>
using namespace std;
// 普通会员类
class Member 
{  
	// ....代码自行编写
protected:
	int id, num;
	string name;
public:
	Member(int id, int num, string name) : id(id), num(num), name(name) {}
	virtual void add(int d) {num += d;}
	virtual int exchange(int d)
	{
		num -= (d - d % 100);
		return d / 100;
	}
	virtual void print() {cout << "普通会员" << id << "--" << name << "--" << num << endl;}
};

// 贵宾会员类
class VIP : public Member
{  
	// ....代码自行编写
	int addrate, exrate;
public: 
	VIP(int a, int e, int i, int n, string na) : addrate(a), exrate(e), Member(i, n, na) {}
	virtual void add(int d) {num += d * addrate;}
	virtual int exchange(int d)
	{
		num -= (d - d % exrate);
		return d / exrate;
	}
	virtual void print() {cout << "贵宾会员" << id << "--" << name << "--" << num << endl;}
};

int main()
{
	// 创建一个基类对象指针
	Member* pm;
	// ....其他变量自行编写
	int id, num, addrate, exrate, mon, exval;
	string name;
	cin >> id >> name >> num >> mon >> exval;
	Member mm(id, num, name);
	pm = &mm;
	pm -> add(mon); pm -> exchange(exval); pm -> print();
	// 输入数据，创建普通会员对象mm
	// 使用指针pm执行以下操作：
	// 1、pm指向普通会员对象mm
	// 2、输入数据，通过pm执行积分累加和积分兑换
	// 3、通过pm调用打印方法输出

	cin >> id >> name >> num >> addrate >> exrate >> mon >> exval;
	VIP vv(addrate, exrate, id, num, name);
	pm = &vv; 
	pm -> add(mon); pm -> exchange(exval); pm -> print();
	// 输入数据，创建贵宾会员对象vv
	// 使用指针pm执行以下操作：
	// 1、pm指向贵宾会员对象vv
	// 2、输入数据，通过pm执行积分累加和积分兑换
	// 3、通过pm调用打印方法输出

	return 0;
}



//B
#include <bits/stdc++.h>
using namespace std;
class Metal
{
	int hard, weight, volumn;
public:
	Metal(int h, int w, int v) : hard(h), weight(w), volumn(v) {}
	Metal operator++(int)
	{
		Metal tmp = *this;
		(*this).hard++;
		(*this).weight *= 1.1;
		(*this).volumn *= 1.1;
		return tmp;
	}
	Metal operator--(int)
	{
		Metal tmp = *this;
		(*this).hard--;
		(*this).weight *= 0.9;
		(*this).volumn *= 0.9;
		return tmp;
	}
	friend Metal operator+(Metal m1, Metal m2)
	{
		Metal tmp = m1;
		tmp.hard = m1.hard + m2.hard;
		tmp.weight = m1.weight + m2.weight;
		tmp.volumn = m1.volumn + m2.volumn;
		return tmp;
	}
	friend Metal operator*(Metal m, int x)
	{
		Metal tmp = m;
		tmp.volumn = m.volumn * x;
		return tmp;
	}
	void print() {cout << "硬度" << hard << "--重量" << weight << "--体积" << volumn << endl;}
};
int main()
{
	int hard, weight, volumn, n;
	cin >> hard >> weight >> volumn;
	Metal m1(hard, weight, volumn);
	cin >> hard >> weight >> volumn >> n;
	Metal m2(hard, weight, volumn);
	Metal m = m1 + m2; m.print();
	m = m1 * n; m.print();
	m1++; m1.print();
	m2--; m2.print();
	return 0;
}



//C
#include <bits/stdc++.h>
using namespace std;
template<class T>
T max(T arr[], int n)
{
	T maxn = -1;
	for (int i = 0; i < n; i++)
	{
		if (arr[i] > maxn) maxn = arr[i];
	}
	return maxn;
}
template<class T>
class Cryption
{
private:
	T ptxt[100]; //明文
	T ctxt[100]; //密文
	T key; //密钥
	int len; //长度
public:
	Cryption(T tk, T tt[], int n) : key(tk), len(n)
	{
		for (int i = 0; i < len; i++) ptxt[i] = tt[i];
	} //参数依次对应密钥、明文、长度
	void encrypt()
	{
		T maxn = max(ptxt, len);
		for (int i = 0; i < len; i++) ctxt[i] = maxn - ptxt[i] + key;
	}
	void print() //打印，无需改造
	{
		int i;
		for (i = 0; i < len - 1; i++)
		{
			cout << ctxt[i] << " ";
		}
		cout << ctxt[i] << endl;
	}
};

//支持三种类型的主函数
int main()
{
	int i;
	int length; //长度
	int ik, itxt[100];
	double dk, dtxt[100];
	char ck, ctxt[100];
	//整数加密
	cin >> ik >> length;
	for (i = 0; i < length; i++)
	{
		cin >> itxt[i];
	}
	Cryption<int> ic(ik, itxt, length);
	ic.encrypt();
	ic.print();
	//浮点数加密
	cin >> dk >> length;
	for (i = 0; i < length; i++)
	{
		cin >> dtxt[i];
	}
	Cryption<double> dc(dk, dtxt, length);
	dc.encrypt();
	dc.print();
	//字符加密
	cin >> ck >> length;
	for (i = 0; i < length; i++)
	{
		cin >> ctxt[i];
	}
	Cryption<char> cc(ck, ctxt, length);
	cc.encrypt();
	cc.print();

	return 0;
}



//D
#include <bits/stdc++.h>
using namespace std;
class appliance
{
protected:
	int id, power;
public:
	appliance(int i, int p) : id(i), power(p) {}
	virtual void print() = 0;
};
class fan : virtual public appliance
{
protected:
	int dir, wind;
public:
	fan(int i, int p, int d, int w) : appliance(i, p), dir(d), wind(w) {}
	void condir(int x) {dir = x;}
	void conwind(int x) {wind = x;}
};
class humidifier : virtual public appliance
{
protected:
	double actcap, maxcap;
public:
	humidifier(int i, int p, double a, double m) : appliance(i, p), actcap(a), maxcap(m) {}
	int alarm()
	{
		double ratio = actcap / maxcap;
		if (ratio >= 0.5) return 1;
		else if (ratio < 0.1) return 3;
		else return 2;
	}
};
class humidfan : public fan, public humidifier
{
	int gear;
public:
	humidfan(int i, int p, int d, int w, double a, double m) : appliance(i, p), fan(i, p, d, w), humidifier(i, p, a, m) {}
	void adjust(int x)
	{
		gear = x;
		if (x == 1) dir = 0, wind = 1;
		else if (x == 2) dir = 1, wind = 2;
		else if (x == 3) dir = 1, wind = 3;
	}
	virtual void print()
	{
		cout << fixed << setprecision(0);
		cout << "加湿风扇--档位" << gear << endl;
		cout << "编号" << id << "--功率" << power << "W" << endl;
		cout << (dir == 1 ? "旋转吹风" : "定向吹风") << "--风力" << wind << "级" << endl;
		cout << "实际水容量" << actcap << "升--";
		int tmp = alarm();
		if (tmp == 1) cout << "水量正常" << endl;
		else if (tmp == 2) cout << "水量偏低" << endl;
		else cout << "水量不足" << endl;  
	}
};
int main()
{
	int t; 
	int id, power, dir, wind, x;
	double accap, maxcap;
	for (cin >> t; t--; )
	{
		cin >> id >> power >> dir >> wind >> accap >> maxcap >> x >> x;
		humidfan h(id, power, dir, wind, accap, maxcap);
		h.adjust(x); h.print();
	}
	return 0;
}



//E
#include <bits/stdc++.h>
using namespace std;
class CN; //提前声明
class EN; //提前声明

// 抽象类
class Weight
{
protected:
	char kind[20]; //计重类型
	int gram; // 克
public:
	Weight(const char tk[] = "no name", int tg = 0)
	{
		strcpy(kind, tk);
		gram = tg;
	}
	virtual void print(ostream& out) = 0; // 输出不同类型的计重信息
};

// 中国计重
class CN : public Weight
{
	int jin, liang, qian;
public:
	CN(int j, int l, int q, int g, char ty[]) : Weight(ty, g), jin(j), liang(l), qian(q) {}
	void Convert(int x)
	{
		jin = x / 500;
		liang = x % 500 / 50;
		qian = x % 50 / 5;
		gram = x % 5;
	}
	virtual void print(ostream& out)
	{
		out << kind << ":" << jin << "斤" << liang << "两" << qian << "钱" << gram << "克" << endl;
	}
	friend ostream& operator<<(ostream &output, CN &c)
	{
		c.print(output);
		return output;
	}
	CN& operator=(EN &en);
};

// 英国计重
class EN : public Weight
{
	int pound, ounce, taran;
public:
	EN(int p, int o, int t, int g, char ty[]) : Weight(ty, g), pound(p), ounce(o), taran(t) {}
	void Convert(int x)
	{
		pound = x / 512;
		ounce = x % 512 / 32;
		taran = x % 32 / 2;
		gram = x % 2;
	}
	friend ostream& operator<<(ostream &output, EN &e)
	{
		e.print(output);
		return output;
	}
	int getsum()
	{
		return pound * 512 + ounce * 32 + taran * 2 + gram;
	}
	virtual void print(ostream& out)
	{
		out << kind << ":" << pound << "磅" << ounce << "盎司" << taran << "打兰" << gram << "克" << endl;
	}
};

CN& CN::operator=(EN &en)
{
	int sum = 0;
	sum = en.getsum();
	this -> Convert(sum);
	return *this;
}
// 以全局函数方式重载输出运算符，代码3-5行....自行编写
// 重载函数包含两个参数：ostream流对象、Weight类对象，参数可以是对象或对象引用
// 重载函数必须调用参数Weight对象的print方法

// 主函数
int main()
{
	int tw;
	char ch1[] = "中国计重";
	// 创建一个中国计重类对象cn
	// 构造参数对应斤、两、钱、克、类型，其中克和类型是对应基类属性gram和kind
	CN cn(0, 0, 0, 0, ch1);
	cin >> tw;
	cn.Convert(tw); // 把输入的克数转成中国计重
	cout << cn;

	// 创建英国计重类对象en
	// 构造参数对应磅、盎司、打兰、克、类型，其中克和类型是对应基类属性gram和kind
	char ch2[] = "英国计重";
	EN en(0, 0, 0, 0, ch2);
	cin >> tw;
	en.Convert(tw); // 把输入的克数转成英国计重
	cout << en;
	cn = en; // 把英国计重转成中国计重
	cout << cn;
	return 0;
}
```



#### 校赛

SZTU Monthly 2022 Oct.

```c++

//A + B
#include <iostream>
using namespace std;
#define ull unsigned long long
int main()
{
    ull a, b;
    scanf("%llu%llu", &a, &b);
    printf("%llu", a + b);
    return 0;
}


//梦里什么都有
//
#include <iostream>
#include <algorithm>
#include <string> //注意string头文件，虽然iostream会隐式包含，但是还是要养成好习惯，写上头文件
using namespace std;
int n, m;
string name, s;
int Judge(int a)
{
    for (int i = 0; i < m - 2; i++)
    {
        if (s[a + i] == name[0])
        {
            int flag = 0;
            for (int j = 0; j < 3; j++)
            {
                if (s[i + j + a] != name[j])
                {
                    flag = 1;
                    break;
                }
            }
            if (!flag) return 1;
        }
    }
    return 0;
}
int main()
{
    scanf("%d %d", &n, &m);
    cin >> n >> m;
    cin >> name >> s; //输入输出string类最好使用cin和cout
    //若使用scanf，要在变量名后加上[0]，甚至有的时候需要预先分配好空间
    //s.resize(100);
    //name.resize(100);
    //scanf("%s", &name[0]); 
    //scanf("%s", &s[0]);
    
    for (int i = 1, j = i + m - 1; j <= n; i++, j++)
    {
        if (Judge(i))
        {
            for (int k = i; k <= j; k++) cout << s[k];
            cout << endl;
        }
    }
    return 0;
}
//
#include <iostream>
#include <algorithm>
#include <string>
using namespace std;
int main()
{
    int n, m;
    cin >> n >> m;
    string name, s;
    cin >> name >> s;
    for (int i = m; i <= s.length(); i++) //s.length()可以返回该字符串的长度
    {
        int flag = 0;
        for (int j = i - m + 3; j <= i && !flag; j++)
        {
            string ret = string(s, j - 3, 3); //string类字符串可以直接用=进行赋值，也可以用==进行直接比较
            if (ret == name) flag = 1;
        }
        if (flag) cout << string(s, i - m, m) << endl; //可以对string类字符串截断输出，第一个参数是该string类变量的名字，第二个参数是起始下标，第三个参数是所要截取的字符串大小
    }
    return 0;
}
//
#include <iostream>
#include <algorithm>
#include <string>
using namespace std;
int main()
{
    cin.tie(0) -> sync_with_stdio(false);
    int n, m;
    cin >> n >> m;
    string name, s;
    cin >> name >> s;
    for (int i = 0; i < n - m + 1; i++)
    {
        string ret = s.substr(i, m); //substr可以用于截断，第一个参数是索引值，第二个是字符串长度
        if (ret.find(name) != ret.npos) //find可以查找字符串，并返回第一个下标，而如果查找不到，string::find会返回string::npos，所以可以用!= 来判断能否找到
            cout << ret << endl;
    }
    return 0;
}


//关于我转生成为一匹赛马娘这档事
//由于马可以走不同形状的日字，又因为只能向右下方移动。可设方程2x1 + x2 = dis(x), x1 + 2x2 = dis(y)，合并方程可得3(x1+x2)=两点间曼哈顿距离，所以只要终点与起点之间曼哈顿距离可以被3整除，就可以达到。但此题还有一个关键点是马不能往上走，所以需要再加入个限定条件判断一下，最终走的趋势是一个扇形。 关于曼哈顿距离，点i和点j之间的曼哈顿距离为:d(i,j) = |xi−xj| + |yi−yj|。
#include <iostream>
#include <algorithm>
using namespace std;
int main()
{
    int n, res = 0;
    for (scanf("%d", &n); n--; )
    {
        int x, y;
        scanf("%d%d", &x, &y);
        int a = (x + y - 2);
        if (a % 3 == 0 && x > a / 3 && y > a / 3) res++;
    }
    printf("%d\n", res);
    return 0;
}
//此代码是利用 bitset 强行 bfs 暴力搜索过的(?)
#include <iostream>
#include <bitset>
using namespace std;
bitset<20010>st[20010];
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    int n;
    cin >> n;
    st[1][1] = 1;
    for(int i=1; i<=20000; i++)
    {
        st[i + 2] |= (st[i] << 1);
        st[i + 1] |= (st[i] << 2);
    }
    int ans = 0;
    while(n--)
    {
        int a, b;
        cin >> a >> b;
        if(st[a][b]) ans++;
    }
    cout << ans << "\n";
    return 0;
}


//封校之我想吃麦当劳


//面基大作战
#include <iostream>
#include <algorithm>
using namespace std;
const int N = 1e5 + 100;
struct node
{
    string s;
    int xg, cf, atc, yan, sc, id;
}a[N];
bool cmp(node a, node b)
{
    if (a.xg != b.xg) return a.xg > b.xg;
    if (a.cf != b.cf) return a.cf > b.cf;
    if (a.atc != b.atc) return a.atc > b.atc;
    if (a.yan != b.yan) return a.yan > b.yan;
    if (a.sc != b.sc) return a.sc > b.sc;
    return a.id < b.id;
}
int n;
int main()
{
    ios::sync_with_stdio(false);//用于打消iostream的输入输出缓存，节省许多时间，使得cin与cout 的效率和scanf与printf相差无几
    cin.tie(0);//0代表cin解绑
    cout.tie(0);
    
    cin >> n;
    for (int i = 1; i <= n; i++)
    {
        cin >> a[i].s >> a[i].xg >> a[i].cf >> a[i].atc >> a[i].yan >> a[i].sc;
        a[i].id = i;
    }
    sort(a + 1, a + 1 + n, cmp); //sort排序速度快
    for (int i = 1; i <= n; i++)
    {
        cout << a[i].s << " " << a[i].xg << " " << a[i].cf << " " << a[i].atc << " " << a[i].yan << " " << a[i].sc << endl;
    }
    return 0;
}


//删库跑路
#include <bits/stdc++.h>
using namespace std;
const int N = 3e4 + 100;
int a[N];
int main()
{
    long long n, x, y, sum;
    sum = 0;
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> a[i];
    cin >> x >> y;
    for (int i = 1; i <= n; i++) {
        sum += a[i] * x <= y ? a[i] * x : y;
    }
    cout << sum;
}

```



22/12/4	迎新赛网络选拔

总结：

- 一定要浏览所有题目，防止后面出现简单题； 

- 数据范围一定要注意！

- 审题时要小心细心！
          

```c++
//缺失的数字
#include <iostream>
#include <algorithm>
#include <string>
using namespace std;
int main()
{
    int flag = 1;
    char num[10];
    char buf[10] = {'1', '2', '3', '4', '5', '6', '7', '8', '9', '0'};
    scanf("%s", num);
    for (int i = 0; i < 10 && flag; i++)
    {
        for (int j = 0; j < 9 && flag; j++)
        {
            if (buf[i] == num[j]) break;
            if (j == 8)
            {
                printf("%c", buf[i]);
                flag = 0;
            }
        }
    }
    return 0;
}



//“本”
#include <iostream>
#include <algorithm>
#include <string>
using namespace std;
int main()
{
    int n;
    cin >> n;
    switch(n % 10)
    {
        case 0:
        case 1:
        case 6:
        case 8: cout << "pon";
                break;
        case 2:
        case 4:
        case 5:
        case 7:
        case 9: cout << "hon";
                break;
        case 3: cout << "bon";
                break;
    }
    return 0;
}


//取数
int main()
{
    int n, m, sum, a = 0, b = 0;
    cin >> n >> m;
    if (n > 1) a = n * (n - 1) / 2;
    if (m > 1) b = m * (m - 1) / 2;
    cout << a + b;
    return 0;
}


//When？
#include <iostream>
#include <algorithm>
#include <string>
using namespace std;
int main()
{
    int n;
    cin >> n;
    if (n != 120) printf("%d:%.2d", 22 + n / 60, 0 + n % 60);
    else printf("00:00");
    return 0;
}


//摆木棍
#include <iostream>
#include <algorithm>
#include <string>
#include <set>
using namespace std;
int num[100001];
int n, a, i;
int main()
{
    set<int> s;
    for (scanf("%d", &n); n--; )
    {
        scanf("%d", &a);
        if (s.count(a))
        {
            num[i++] = a;
            s.erase(a);
        }
        else s.insert(a);
    }
    sort(num, num + i);
    if (i < 2) printf("-1");
    else printf("%lld", num[0] * num[1]);
    return 0;
}


//开趴
//TLE
#include <iostream>
#include <algorithm>
#include <string>
#include <set>
using namespace std;
int n, num[100010], dis[100010];
long long int sum, ans;
int main()
{
    scanf("%d", &n);
    for (int i = 1; i <= n; i++)
    {
        scanf("%d", &num[i]);
    }
    sort(num + 1, num + 1 + n);
    for (int i = 1; i <= n; i++)
    {
        if (i == 1) dis[i] = 0;
        else dis[i] = num[i] - num[i - 1];
    }
    for (int i = 1; i <= n; i++) dis[i] += dis[i - 1];
    for (int i = n / 2; i <= n / 2 + 1; i++)
    {
        sum = 0;
        for (int j = 1; j <= n; j++)
        {
            if (j == i) continue;
            if (j > i) sum += dis[j] - dis[i];
            else sum += dis[i] - dis[j];
            if (sum > ans && i > 1) break;
            if (i == 1 && j == n) ans = sum;
            else if (i != 1 && j == n) ans = min(sum, ans);
        }
    }
    printf("%lld", ans);
    return 0;
}
//？
#include <iostream>
#include <algorithm>
#include <string>
#include <set>
using namespace std;
int n, num[100010], dis[100010];
long long int sum, ans = INT64_MAX;
int main()
{
    scanf("%d", &n);
    for (int i = 1; i <= n; i++)
    {
        scanf("%d", &num[i]);
    }
    sort(num + 1, num + 1 + n);
    for (int i = 1; i <= n; i++)
    {
        if (i == 1) dis[i] = 0;
        else dis[i] = num[i] - num[i - 1];
    }
    for (int i = 1; i <= n; i++) dis[i] += dis[i - 1];
    for (int i = n / 2; i <= n / 2 + 1; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            if (j > i) sum += dis[j] - dis[i];
            else sum += dis[i] - dis[j];
        }
        ans = min(sum, ans);
    }
    printf("%lld", ans);
    return 0;
}
//巧妙取中点
int main()
{
    std::ios::sync_with_stdio(false);
    cin.tie(NULL):cout.tie(NULL);
    int n;
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> a[i];
    sort(a + 1, a + 1 + n);
    for (int i = 1, r = n; 1 < r; l++, r--) ans += a[r] - a[i];
    cout << ans << endl;
    return 0;
}
//


//复合函数
#include <iostream>
#include <algorithm>
#include <string>
#include <set>
using namespace std;
int n, q, val[110], a, b;
int alg(int a, int b)
{
    if (b == 1) return val[a];
    if (b > 1) return val[alg(a, b - 1)];
}
int main()
{
    scanf("%d", &n);
    for (int i = 1; i <= n; i++) scanf("%d", &val[i]);
    for (scanf("%d", &q); q--; )
    {
        scanf("%d%d", &a, &b);
        printf("%d\n", alg(a, b));
    }
    return 0;
}
```

22/12/7	迎新赛

总结：

- 比赛前一定要先适应比赛环境，包括编译器，要争取早到，而不是很赶
- 比赛的时候，遇到意料之外的情况，要沉着冷静，调整心态，只有稳住心态才能发挥实力
- 提交的时候再次检查数据范围，再次浏览题目
- 要善于从每道题的提交与ac次数，推测题目难度，从而避免死磕难题，没时间做简单题
- 阅读题目不要图快！把题目大意和出题者意图理解好才是最关键的，否则思路错，写错重改反而浪费时间
- 有些题目可以尝试列出所有可能，也是解题的一种方法

```c++
//阶梯数
//枚举
#include <iostream>
#include <vector>
using namespace std;
int k;
bool Judge(int i)
{
    int a = 10;
    while (i)
    {
        if (a <= (i % 10)) return false;
        a = i % 10;
        i /= 10;
    }
    return true;
}
int main()
{
    vector<int> v;
    cin >> k;
    for (int i = 0; i <= 123456789; i++)
        if (Judge(i)) v.push_back(i);
    cout << v[v.size() - k];
}
//递归
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
vector<int> v;
void dfs(int x, int lst)
{
    v.push_back(x);
    for (int i = lst + 1; i < 10; i++)
        dfs(x * 10 + i, i);
}
int main()
{
    dfs(0, 0);
    sort(v.begin(), v.end());
    int k;
    cin >> k;
    cout << v[512 - k];
    return 0;
}


//宝石冒险
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
long long ar[100005];

int main()
{
	int n,k;
	cin >> n >> k;
	long long ans = 0;
	for (int i = 1; i <= n; ++i)
	{
		long long a, b;
		scanf("%lld %lld", &a, &b);
		ans += a;
		ar[i] = b-a;
	}
    sort(ar + 1, ar + n + 1);
	for (int i = n - k + 1; i <= n; ++i)
        ans += ar[i];
	cout << ans;
}


//快来玩2048！
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
const int maxn = 2e5 + 5;
int G[105][105], n;
void left()
{
    for (int i = 1; i <= n; ++i)
    {
        int a = 1, b = 2;
        while (b <= n)
        {
            int t = G[i][b];
            G[i][b++] = 0;
            if (t == 0)
                continue;
            if (G[i][a] == t)
                G[i][a++] += t;
            else if (G[i][a] == 0)
                G[i][a] = t;
            else
                G[i][++a] = t;
        }
    }
}

void right()
{
    for (int i = 1; i <= n; ++i)
    {
        int a = n, b = n - 1;
        while (b >= 1)
        {
            int t = G[i][b];
            G[i][b--] = 0;
            if (t == 0)
                continue;
            if (G[i][a] == t)
                G[i][a--] += t;
            else if (G[i][a] == 0)
                G[i][a] = t;
            else
                G[i][--a] = t;
        }
    }
}

void up()
{
    for (int i = 1; i <= n; ++i)
    {
        int a = 1, b = 2;
        while (b <= n)
        {
            int t = G[b][i];
            G[b++][i] = 0;
            if (t == 0)
                continue;
            if (G[a][i] == t)
                G[a++][i] += t;
            else if (G[a][i] == 0)
                G[a][i] = t;
            else
                G[++a][i] = t;
        }
    }
}

void down()
{
    for (int i = 1; i <= n; ++i)
    {
        int a = n, b = n - 1;
        while (b >= 1)
        {
            int t = G[b][i];
            G[b--][i] = 0;
            if (t == 0)
                continue;
            if (G[a][i] == t)
                G[a--][i] += t;
            else if (G[a][i] == 0)
                G[a][i] = t;
            else
                G[--a][i] = t;
        }
    }
}

int main()
{
    int m;
    cin >> n >> m;
    for (int i = 1; i <= n; ++i)
    {
        for (int j = 1; j <= n; ++j)
            cin >> G[i][j];
    }
    int ok = 0;
    for (int k = 1; k <= m; ++k)
    {
        char op;
        int x, y;
        cin >> op >> x >> y;
        if (op == 'L')
            left();
        if (op == 'R')
            right();
        if (op == 'U')
            up();
        if (op == 'D')
            down();
        if (!G[x][y])
            G[x][y] = 2;

        for (int i = 1; i <= n; ++i)
            for (int j = 1; j <= n; ++j)
                if (G[i][j] == 2048)
                    ok = 1, k = m + 1;
    }
    if (ok)
        cout << "Yes\n";
    else
        cout << "No\n";
    for (int i = 1; i <= n; ++i)
    {
        for (int j = 1; j <= n; ++j)
        {
            cout << G[i][j];
            if (j == n)
                cout << "\n";
            else
                cout << " ";
        }
    }
}

//卡牌游戏
//前缀差
#include <iostream>
#include <vector>
#include <algorithm>
#include <cmath>
using namespace std;
const int N = 1e5 + 5;
int d[N];
int main()
{
    cin.tie(0) -> sync_with_stdio(false);
    int n, m, X, q;
    cin >> n >> X >> m >> q;
    int a = 0, b = 0;
    while (m--)
    {
        int l, r, c;
        cin >> l >> r >> c;
        d[l] += c;
        d[r + 1] -= c;
    }
    for (int i = 2; i <= n; i++)
    {
        if (d[i] > 0) a += d[i];
        else b += d[i];
    }
    int ans = max(a, abs(b));
    if (ans > q) cout << "-1";
    else cout << ans;
    return 0;
}

//新年好
//二分法
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
long long ans, n, m, a[200010];
bool check(long long x)
{
    if (x == 0) return 1; 
    long long cnt = 0, sum = 0;
    for (int i = 1; i <= n; i++)
    {
        if (a[i] >= x) cnt++;
        else sum += a[i];
    }
    cnt += sum / x;
    if (cnt >= m) return 1;
    else return 0;
}
int main()
{
    scanf("%d%d", &n, &m);
    for (int i = 1; i <= n; i++)
        scanf("%lld", &a[i]);
    long long l = 0, r = 1e18;
    while (l <= r)
    {
        long long mid = l + (r - l) / 2;
        if (check(mid))
        {
            l = mid + 1;
            ans = mid;
        }
        else r = mid - 1;
    }
    printf("%lld", ans);
    return 0;
}


//要是不难，也挺简单的
```











#### ACM

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

#### Game1

```c++
//头文件的包含
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

//函数的定义
#define ROW 3
#define COL 3


//函数的声明


//初始化棋盘
void Initboard(char board[ROW][COL],int row,int col);

//打印棋盘的函数
void Displayboard(char board[ROW][COL], int row, int col);

//玩家下棋
void PlayerMove(char board[ROW][COL], int row, int col);

//电脑下棋
void ComputerMove(char board[ROW][COL], int row, int col);

//判断输赢
char Iswin(char board[ROW][COL], int row, int col);

 void Initboard(char board[ROW][COL], int row, int col)
{
	 int i = 0;
	 int j = 0;
	 for (i = 0; i < row; i++)
	 {
		 for (j = 0; j < col; j++)
		 {
			 board[i][j] = ' ';
		 }
	 }
}


 void Displayboard(char board[ROW][COL], int row, int col)
 {
	 int i = 0;
	 for (i = 0; i < row; i++)
	 {
		 int j = 0;
		 for (j = 0; j < col;j++)
		 {
			 printf(" %c ",board[i][j]);
			 if (j < col - 1)
				 printf("|");
		 }
		 printf("\n");
		 if (i < row - 1)
		 {
			 int j = 0;
			 for (j = 0; j < col; j++)
			 {
				 printf("---");
				 if (j < col - 1)
					 printf("|");
			 }
		 }
		 printf("\n");
	 }
 }



 void PlayerMove(char board[ROW][COL], int row, int col)
 {
	 int x = 0;
	 int y = 0;
	 printf("Player Move\n");
	 printf("Please enter coordinates\n");
	 while (1)
	 {
		 scanf("%d %d", &x, &y);
		 //判断坐标合法性
		 if (x >= 1 && x <= row && y >= 1 && y <= col)
		 {
			 //下棋
			 //判断是否被占用
			 if (board[x - 1][y - 1]==' ')
			 {
				 board[x - 1][y - 1] = '*';
				 break;
			 }
			 else
			 {
				 printf("Coordinates have been occupied,please re-enter.\n");
			 }
		 }
		 else
		 {
			 printf("The coordinates are illegal,please re-enter.\n");
		 }
	 }
 }

 void ComputerMove(char board[ROW][COL], int row, int col)
 {
	 printf("Turn to computer\n");
	 while (1)
	 {
		 int x = rand() % row;
		 int y = rand() % col;
		 //判断占用
		 if (board[x][y] == ' ')
		 {
			 board[x][y] = '#';
			 break;
		 }
	 }
 }




 int Isfull(char board[ROW][COL], int row, int col)
 {
	 int i = 0;
	 int j = 0;
	 for (i = 0; i < row; i++)
	 {
		 for (j = 0; j < col; j++)
		 {
			 if (board[i][j] == ' ')
				 return 0;//棋盘没满
		 }
	 }
	 return 1;//棋盘已满
 }

 char Iswin(char board[ROW][COL], int row, int col)
 {
	 int i = 0;
	 //判断行
	 for (i = 0; i < row; i++)
	 {
		 if (board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][1] != ' ')
		 {
			 return board[i][1];
		 }
	 }
	 //判断列
	 for (i = 0; i< col; i++)
	 {
		 if (board[0][i] == board[1][i] && board[1][i] == board[2][i] && board[0][i] != ' ')
		 {
			 return board[1][i];
		 }
	 }
	 //判断对角线
	 if (board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[0][0] != ' ')
	 {
		 return board[0][0];
	 }
	 if (board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[0][2] != ' ')
	 {
		 return board[0][2];
	 }
	 //判断是否平局
	 int ret=Isfull(board, row, col);
	 if (ret == 1)
	 {
		 return 'Q';
	 }
	 return 'c';
 }

void menu()
{
	printf("1.play\n");
	printf("0.exit\n");
}

void game()
{
	//储存数据-二维数组
	char board[ROW][COL];
	//初始化棋盘-初始化空格
	Initboard(board, ROW, COL);
	//打印棋盘-本质是打印数组内容
	Displayboard(board, ROW, COL);
	char ret = 0;
	while (1)
	{
		//玩家下棋
		PlayerMove(board, ROW, COL);
		Displayboard(board, ROW, COL);
		//判断玩家是否赢得游戏
		ret = Iswin(board, ROW, COL);
		if (ret != 'c')
			break;
		//电脑下棋
		ComputerMove(board, ROW, COL);
		Displayboard(board, ROW, COL);
		//判断电脑是否赢得游戏
		ret = Iswin(board, ROW, COL);
		if (ret != 'c')
			break;
	}
	if (ret == '*')
	{
		printf("Player Win!\n");
	}
	else if (ret == '#')
	{
		printf("Computer Win!\n");
	}
	else
	{
		printf("Q.\n");  
	}
	Displayboard(board, ROW, COL);

}


int main()
{
	int input = 0;
	srand((unsigned int)time(NULL));	//设置随机值
	do
	{
		menu();
		scanf("%d", &input);
		switch(input)
		{
		case 1:
			    game();
				break;
		case 0:
				printf("Quit the game\n");
				break;
		default :
				printf("Incorrect selection,please reselect\n");
				break;
		}
	} while (input);

	return 0;
}//
```

#### Others

[约瑟夫问题](https://vjudge.csgrandeur.cn/problem/OpenJ_Bailian-2746)

```c++
#include <stdio.h>
#include <math.h>
#define MAX 10010

    int main()
    {
        int mon[300] = {0};
        int n, m, cnt;
        int out;
        while(scanf("%d %d", &n, &m) && n != 0 && m != 0)//111111
        {
            out = 0;
            cnt = 0;
            for(int i = 0; i < n; i ++)   mon[i] = 1;
            for(int i = 0; i < n && n != 1; i ++)
            {
                if(out == n-1 && i == n - 1)    break;
                if(mon[i] != 0) cnt++;
                if(cnt == m)    
                {
                    mon[i] = 0;
                    cnt = 0;
                    out++;
                }
                if(out != n-1 && i == n - 1)
                {
                    i = -1;
                }
            }
            for(int i = 0; i< n; i ++)
                if(mon[i] == 1) printf("%d\n", i+1);
        }
        return 0;
    }
```

hdu 4841 圆桌问题

```c++
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> table;
    int n, m;
    while (cin >> n >> m)
    {
        table.clear();
        int pos = 0;
        for (int i = 0; i < n; i++)
        {
            pos = (pos + m - 1) % table.size();
            table.erase(table.begin() + pos);
        }
        int j = 0;
        for (int i = 0; i < 2 * n; i++)
        {
            if (!(i % 50) && i) cout << endl;
            if (j < table.size() && i == table[j])
            {
                j++;
                cout << "G";
            }
            else
                cout << "B";
        }
        cout << endl << endl;
    }
    return 0;
}
```

hdu 1062 “Text Reverse"

```c++
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

int main()
{
    int n;
    char ch;
    cin >> n;
    cin.get();
    while (n--)
    {
        stack<char> s;
        while (true)
        {
            ch = cin.get();
            if (ch == ' ' || ch == '\n' || ch == EOF)
            {
                while (!s.empty())
                {
                    cout << s.top();
                    s.pop();
                }
                if (ch == '\n' || ch == EOF)    break;
                cout << ' ';            
            }
            else    s.push(ch);
        }
        cout << endl;
    }
    return 0;
}
```

hdu 1702 "ACboy needs your help again!"

```c++
//模拟栈和队列
#include <iostream>
#include <vector>
#include <stack>
#include <queue>
using namespace std;

int main()
{
    int t, n, temp;
    cin >> t;
    while (t--)
    {
        string str, str1;
        queue<int> Q;
        stack<int> S;
        cin >> n >> str;
        for (int i = 0; i < n; i++)
        {
            if (str == "FIFO")          //队列
            {
                cin >> str1;
                if (str1 == "IN")
                {
                    cin >> temp;
                    Q.push(temp);
                }
                if (str1 == "OUT")
                {
                    if (Q.empty())  cout << "None" << endl;
                    else{
                        cout << Q.front() << endl;
                        Q.pop();
                    }
                }
            }
            else                        //栈
            {
                if (str1 == "IN")
                {
                    cin >> temp;
                    S.push(temp);
                }
                if (str1 == "OUT")
                {
                    if (S.empty())  cout << "None" << endl;
                    else
                    {
                        cout << S.top() << endl;
                        S.pop();
                    }
                }
            }
        }
    }
    return 0;
}
```

hdu 1276 士兵队列训练问题

```c++
#include <iostream>
#include <vector>
#include <stack>
#include <queue>
#include <list>
using namespace std;

int main()
{
    int t, n;
    cin >> t;
    while (t--)
    {
        cin >> n;
        int k = 2;
        list<int> mylist;
        list<int>::iterator it;
        for (int i = 1; i <= n; i++)
            mylist.push_back(i);
        while (mylist.size() > 3)
        {
            int num = 1;
            for (it = mylist.begin(); it != mylist.end(); )
            {
                if (num++ % k == 0)  it = mylist.erase(it);
                else  it++;
            }
            k == 2 ? k = 3 : k = 2;
        }
        for (it = mylist.begin(); it != mylist.end(); it++)
        {
            if (it != mylist.begin())  cout << ' ';
            cout << * it;
        }
        cout << endl;
    }
    return 0;
}
```

hdu 2094 产生冠军

```c++
#include <iostream>
#include <vector>
#include <stack>
#include <queue>
#include <list>
#include <set>
using namespace std;

int main()
{
    set<string> A, B;
    string s1, s2;
    int n;
    while (cin >> n && n)
    {
        for (int i = 0; i < n; i++)
        {
            cin >> s1 >> s2;
            A.insert(s1);
            A.insert(s2);
            B.insert(s2);
        }
        if (A.size() - B.size() == 1)
            cout << "Yes" << endl;
        else
            cout << "No" << endl;
        A.clear();
        B.clear();
    }
    return 0;
}
```

hdu 2648 “shopping"

```c++
#include <iostream>
#include <map>
using namespace std;

int main()
{
    int n, m, p;
    map<string, int> shop;
    while (cin >> n)
    {
        string s;
        for (int i = 1; i <= n; i++)  cin >> s;
        cin >> m;
        while (m--)
        {
            for (int i = 1; i <= n; i++)
            {
                cin >> p >> s;
                shop[s] += p;
            }
            int rank = 1;
            map<string, int>::iterator it;
            for (it = shop.begin(); it != shop.end(); it++)
                if (it -> second > shop["memory"])
                    rank++;
            cout << rank << endl;
        }
        shop.clear();
    }
    return 0;
}
```

hdu 1027 "Ignatius and the Princess II"

```c++
#include <iostream>
#include <algorithm>
using namespace std;

int a[1001];
int main()
{
    int n, m;
    while (cin >> n >> m)
    {
        for (int i = 1; i <= n; i++)    a[i] = i;
        int b = 1;
        do
        {
            if (b == m) break;
            b++;
        } while (next_permutation(a + 1, a + n + 1));
        for (int i = 1; i < n; i++)
            cout << a[i] << ' ';
        cout << a[n] << endl;
    }
    return 0;
}
```

递归打印全排列

```c++
#include <iostream>
#include <ctime>
using namespace std;

//递归打印全排列
#define Swap(a, b) {int temp = a; a = b; b = temp;}
int dt[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
int num = 0;
void Perm(int begin, int end)
{
    int i;
    if (begin == end)  num++;
    //打印n个数中任意m个数的全排列
    //m = 3  n = 10
    //if (begin == 3)
    //    cout << dt[0] << dt[1] << dt[2] << endl;
    else
        for (i = begin; i <= end; i++)
        {
            Swap(dt[begin], dt[i]);
            Perm(begin + 1, end);
            Swap(dt[begin], dt[i]);
        }
}
int main()
{
    clock_t start, end; //统计时间
    start = clock();
    Perm(0, 11);
    end = clock();
    cout << num << endl;
    cout << (double)(end - start) / CLOCKS_PER_SEC << endl;
    return 0;
}//
```

2021 RoboCom世界机器人开发者大赛 - 本科组(初赛)

[7 - 1 懂的都懂](https://pintia.cn/problem-sets/1446838676759703552/exam/problems/1446838732288094208)

```c++
#include <bits/stdc++.h>
using namespace std;
int main()
{
	ios::sync_with_stdio(false);
	cin.tie(NULL);
	int n, m; cin >> n >> m;
	set<int> se;
	vector<int> ve(n);
	for (int i = 0; i < n; i++) cin >> ve[i];
	for (int i = 0; i < n; i++)
	{
		int sum = ve[i];
		for (int j = i + 1; j < n; j++)
		{
			sum += ve[j];
			for (int k = j + 1; k < n; k++)
			{
				sum += ve[k];
				for (int l = k + 1; l < n; l++)
				{
					sum += ve[l];
					se.insert(sum);
					sum -= ve[l];
				}
				sum -= ve[k];
			}
			sum -= ve[j];
		}
		sum -= ve[i];
	}
	for (int i = 0; i < m; i++)
	{
		int cnt = 0; cin >> cnt;
		vector<int> val(cnt);
		for (int j = 0; j < cnt; j++) cin >> val[j];
		for (int j = 0; j < cnt; j++)
		{
			if (se.count(val[j] * 4) == 0) {cout << "No" << endl; break;}
			if (j == cnt - 1) cout << "Yes" << endl;
		}
	}
	return 0;
}
```

[7-2 芬兰木棋](https://pintia.cn/problem-sets/1446838676759703552/exam/problems/1446838732288094209)

```c++
#include <bits/stdc++.h>
using namespace std;
typedef pair<int, int> PLL;
typedef long long LL;
int n, s;
LL x, y;
map<PLL, vector<pair<LL, int>>> ma;

int main()
{
	cin >> n;
	int sum = 0, cnt = 0;
	for (int i = 0; i < n; i++)
	{
		cin >> x >> y >> s;
		sum += s;
		LL d = x * x + y * y;
		LL c = abs(__gcd(x, y));
		x /= c; y /= c;
		ma[{x, y}].push_back({d, s});
	}

	for (auto v : ma)
	{
		vector<pair<LL, int>> ve = v.second;
		sort(ve.begin(), ve.end());
		for (int i = 0; i < ve.size(); i++)
		{
			if (i && ve[i - 1].second == 1 && ve[i].second == 1) continue;
			cnt++;
		}
	}
	cout << sum << ' ' << cnt << endl;
	return 0;
}
```

[7 - 3 打怪升级](https://pintia.cn/problem-sets/1446838676759703552/exam/problems/1446838732288094210)

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 1010;

bool vis[N];
int n, m, max_s[N];
int min_s[N], max_d[N];
int a, b, s, d, pre[N];
int S[N][N], D[N][N];
int dijkstra(int f)
{
	memset(vis, 0, sizeof vis);
	memset(min_s, 0x3f, sizeof min_s);
	memset(max_d, 0, sizeof max_d);

	min_s[f] = 0;
	while (true)
	{
		int t = -1;
		for (int i = 1; i <= n; i++)
			if (!vis[i] && (t == -1 || min_s[t] > min_s[i]))
				t = i;

		if (t == -1) break;
		vis[t] = true;

		for (int i = 1; i <= n; i++)
		{
			if (min_s[i] > min_s[t] + S[t][i])
			{
				pre[i] = t;
				min_s[i] = min_s[t] + S[t][i];
				max_d[i] = max_d[t] + D[t][i];
			}
			else if (min_s[i] == min_s[t] + S[t][i])
			{
				if (max_d[i] < max_d[i] + D[t][i])
				{
					pre[i] = t;
					max_d[i] = max_d[t] + D[t][i];
				}
			}
		}
	}

	int ms = 0;
	for (int i = 1; i <= n; i++)
		if (ms < min_s[i])
			ms = min_s[i];
	return ms;
}

void dfs(int x, int id)
{
	if (x == id) return;
	dfs(pre[x], id);
	printf("->%d", x);
}

int main()
{
	memset(S, 0x3f, sizeof S);
	scanf("%d %d", &n, &m);
	while (m--)
	{
		scanf("%d %d %d %d", &a, &b, &s, &d);
		S[a][b] = S[b][a] = min(S[a][b], s);
		D[a][b] = D[b][a] = max(D[a][b], d);
	}
	for (int i = 1; i <= n; i++)
		max_s[i] = dijkstra(i);

	int id = 1;
	for (int i = 1; i <= n; i++)
		if (max_s[id] > max_s[i])
			id = i;
	
	printf("%d\n", id);
	dijkstra(id);

	int k, x;
	scanf("%d", &k);
	while (k--)
	{
		scanf("%d", &x);
		printf("%d", id);
		dfs(x, id);
		printf("\n");
		printf("%d %d\n", min_s[x], max_d[x]);
	}
	return 0;
}
```

[7-4 疫情防控](https://pintia.cn/problem-sets/1446838676759703552/exam/problems/1446838732288094211)

```c++
#include <bits/stdc++.h>
using namespace std;

const int N = 5e4 + 10;
typedef pair<int, int> PII;

int n, m, d;
int c, q, a, b, x, y;
int f[N];
bool st[N];
vector<vector<PII>> plls;
vector<int> G[N], ps, res;

void init()
{
	for (int i = 0; i < N; i++)
		f[i] = i;
}

int find(int x)
{
	return f[x] = f[x] == x ? x : find(f[x]);
}

int main()
{
	init();
	scanf("%d %d %d", &n, &m, &d);
	for (int i = 0; i < m; i++)
	{
		scanf("%d %d", &x, &y);
		G[x].push_back(y);
		G[y].push_back(x);
	}
	while (d--)
	{
		scanf("%d %d", &c, &q);
		st[c] = true;
		ps.push_back(c);

		vector<PII> pll;
		while (q--)
		{
			scanf("%d %d", &a, &b);
			pll.push_back({a, b});
		}
		plls.push_back(pll);
	}
	for (int i = 1; i <= n; i++)
	{
		if (st[i]) continue;
		for (int j = 0; j < G[i].size(); j++)
		{
			int x = G[i][j];
			if (st[x]) continue;
			f[find(i)] = find(x);
		}
	}
	for (int i = plls.size() - 1; i >= 0; i--)
	{
		int cnt = 0;
		vector<PII> pll = plls[i];
		for (PII p : pll)
			if (find(p.first) != find(p.second))
				cnt++;
		
		res.push_back(cnt);

		int u = ps[i];
		for (int x : G[u])
		{
			if (st[x]) continue;
			f[find(x)] = find(u);
		}
		st[u] = false;
	}


	reverse(res.begin(), res.end());
	for (int x : res)
		printf("%d\n", x);
	return 0;
}
```



#### luogu

P7441「EZEC-7」Erinnerung

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

P7909 [CSP-J 2021] 分糖果

```c++
#include <iostream>
using namespace std;
int main()
{
    int n, l, r;
    cin >> n >> l >> r;
    if (l / n == r / n) cout << r % n;
    else cout << n - 1;
    return 0;
}
```

P2637 第一次，第二次，成交！

```c++
#include <iostream>
#include <algorithm>
using namespace std;
int m, n, prices[100], ma, ans, sum, ret;
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    cin >> m >> n;
    for (int i = 0; i < n; i++) cin >> prices[i];
    sort(prices, prices + n);
    for (int i = 0; i < n; i++)
    {
        ret = m < (n - i) ? m : (n - i);
        if (prices[i] * ret > ma) ans = i, ma = prices[i] * ret;
    }
    cout << prices[ans] << ' ' << ma;
    return 0;
}
```

P1321 单词覆盖还原

```c++
#include <iostream>
#include <stack>
#include <queue>
#include <algorithm>
#include <cstring>
using namespace std;
int main()
{
    int boy = 0, girl = 0;
    string str;
    cin >> str;
    for (int i = 0; i < str.size(); i++)
    {
        if (str[i] == 'b' || str[i + 1] == 'o' || str[i + 2] == 'y') boy++;
        if (str[i] == 'g' || str[i + 1] == 'i' || str[i + 2] == 'r' || str[i + 3] == 'l') girl++;
    }
    cout << boy << endl << girl;
    return 0;
}
```

P1427 小鱼的数字游戏

```c++
#include <iostream>
#include <stack>
#include <queue>
#include <algorithm>
using namespace std;
int main()
{
    int a;
    stack<int> sta;
    while (cin >> a && a) sta.push(a);
    while (!sta.empty())
    {
        a = sta.top();
        cout << a;
        sta.pop();
        if (!sta.empty()) cout << " ";
    }
    return 0;
}
```

P1739 表达式括号匹配

```c++
#include <iostream>
#include <stack>
#include <queue>
#include <algorithm>
using namespace std;
int main()
{
    char a;
    stack<int> sta;
    while (cin >> a && a != '@')
    {
        if (a == '(') sta.push(1);
        if (a == ')')
        {
            if (!sta.empty()) sta.pop();
            else
            {
                cout << "NO";
                break;
            }
        }
    }
    if (sta.empty() && a != ')') cout << "YES";
    else if(!sta.empty() && a != ')') cout << "NO";
    return 0;
}
```

#### 2022寒假训练赛

*22/12/19第一场*

**总结:**

- 不要被英文吓到,题目内容多不代表题目难,保持耐心和细心才是最重要的
- 仔细读题,把题读懂再写!

[A - Count Distinct Integers](https://vjudge.net/problem/AtCoder-abc240_b)

```c++
#include <iostream>
#include <algorithm>
#include <set>
using namespace std;
int main()
{
    int n, a, cnt = 0;
    cin >> n;
    set<int> s;
    for (int i = 1; i <= n; i++)
    {
        cin >> a;
        if (!s.count(a)) cnt++, s.insert(a);
    }
    cout << cnt;
    return 0;
}
```

[B - Better Students Are Needed!](https://vjudge.net/problem/AtCoder-abc260_b)

```c++
#include <iostream>
#include <algorithm>
#include <string>
#include <set>
#include <map>
using namespace std;
struct str
{
    int x;
    int y;
    int t;
    int f;
    int w;
}scores[1010];
bool cmp1(str a, str b)
{
    if (a.x != b.x)
        return a.x > b.x;
    else return a.w < b.w;
}
bool cmp2(str a, str b)
{
    if (a.y != b.y) return a.y > b.y;
    else return a.w < b.w;
}
bool cmp3(str a, str b)
{
    if (a.t != b.t) return a.t > b.t;
    else return a.w < b.w;
}
bool cmp4(str a, str b)
{
    return a.w < b.w;
}
int n, x, y, z, cnt;
int main()
{
    cin >> n >> x >> y >> z;
    for (int i = 1; i <= n; i++) cin >> scores[i].x;
    for (int i = 1; i <= n; i++)
    {
        cin >> scores[i].y;
        scores[i].t = scores[i].x + scores[i].y;
        scores[i].f = 0;
        scores[i].w = i;
    }
    sort(scores + 1, scores + 1 + n, cmp1);
    cnt = 0;
    for (int i = 1; i <= x; i++)
    {
        scores[i].f = 1;
    }
    sort(scores + 1, scores + 1 + n, cmp2);
    cnt = 0;
    for (int i = 1; cnt != y; i++)
    {
        if (scores[i].f == 0)
        {
            scores[i].f = 1;
            cnt++;
        }
    }
    sort(scores + 1, scores + 1 + n, cmp3);
    cnt = 0;
    for (int i = 1; cnt != z; i++)
    {
        if (scores[i].f == 0)
        {
            scores[i].f = 1;
            cnt++;
        }
    }
    sort(scores + 1, scores + 1 + n, cmp4);
    for (int i = 1; i <= n; i++)
    {
        if (scores[i].f) cout << scores[i].w << endl;
    }
    return 0;
}
//
#include <stdio.h>
#include <algorithm>
#include <vector>
using namespace std;
const int N = 1005;
int a[N], b[N];
int id[N], vis[N];

bool cmp1(int &t1, int &t2)
{
    if (a[t1] != a[t2])
        return a[t1] > a[t2];
    return t1 < t2;
}

bool cmp2(int &t1, int &t2)
{
    if (b[t1] != b[t2])
        return b[t1] > b[t2];
    return t1 < t2;
}

bool cmp3(int &t1, int &t2)
{
    if (b[t1] + a[t1] != a[t2] + b[t2])
        return b[t1] + a[t1] > a[t2] + b[t2];
    return t1 < t2;
}

int main()
{
    int n, x, y, z;
    vector<int> ve;
    scanf("%d%d%d%d", &n, &x, &y, &z);
    for (int i = 1; i <= n; i++)
        scanf("%d", &a[i]);
    for (int i = 1; i <= n; i++)
        scanf("%d", &b[i]);
    for (int i = 1; i <= n; i++)
        id[i] = i;

    sort(id + 1, id + 1 + n, cmp1);

    for (int i = 1; i <= n && x; i++)
    {
        if (!vis[id[i]])
        {
            ve.push_back(id[i]);
            vis[id[i]] = 1;
            x--;
        }
    }

    sort(id + 1, id + 1 + n, cmp2);

    for (int i = 1; i <= n && y; i++)
    {
        if (!vis[id[i]])
        {
            ve.push_back(id[i]);
            vis[id[i]] = 1;
            y--;
        }
    }

    sort(id + 1, id + 1 + n, cmp3);

    for (int i = 1; i <= n && z; i++)
    {
        if (!vis[id[i]])
        {
            ve.push_back(id[i]);
            vis[id[i]] = 1;
            z--;
        }
    }
    sort(ve.begin(), ve.end());
    for (int i = 0; i < ve.size(); i++)
        printf("%d\n", ve[i]);

    return 0;
}
```

[C - ±1 Operation 2](https://vjudge.net/problem/AtCoder-abc255_d)

前缀和加二分

```c++

#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
#define LL long long
const int N = 2e5 + 5;
int n, q;
LL a[N], b[N], num, sum;
int main()
{
    cin >> n >> q;
    for (int i = 1; i <= n; i++) cin >> a[i];
    sort(a + 1, a + 1 + n);
    for (int i = 1; i <= n; i++) b[i] = a[i] + b[i - 1];
    for (int i = 1; i <= q; i++)
    {   
        sum = 0;
        cin >> num;
        LL x = lower_bound(a + 1, a + 1 + n, num) - a;
        sum = (x - 1) * num - (b[x - 1]) + (b[n] - b[x - 1]) - (n - x + 1) * num;
        cout << sum << endl;
    }
    return 0;
}
```

[D - Submask](https://vjudge.net/problem/AtCoder-abc269_c)

列子集

```
#include <iostream>
#include <algorithm>
#include <set>
using namespace std;
#define LL long long
int vis[100], n;
set<LL> s;
void dfs(int u, LL x)
{
    if (u == n + 1)
    {
        s.insert(x);
        return;
    }
    dfs(u + 1, x);  //当前位置不选
    if (vis[u])     //若为1，则选
    {
        x += (1LL << u);
        dfs(u + 1, x);
    }
}
int main()
{
    LL x;
    cin >> x;
    int ed = 0;
    while (x)
    {
        vis[ed] = x % 2;
        x /= 2;
        ed++;
    }
    n = ed - 1;
    dfs(0, 0);
    for (auto it = s.begin(); it != s.end(); it++)
        cout << *it << endl;
    return 0;
}
```

[E - Equal Candies](https://vjudge.net/problem/CodeForces-1676B)

```c++
#include <iostream>
#include <algorithm>
#include <string>
#include <set>
#include <map>
using namespace std;
int main()
{
    int n, nums[1010], cnt, t;
    for (cin >> t; t--;)
    {
        cin >> n;
        cnt = 0;
        for (int i = 1; i <= n; i++)
            cin >> nums[i];
        sort(nums + 1, nums + 1 + n);
        if (nums[1] == nums[n])
            cout << "0\n";
        else
        {
            for (int i = 1; i <= n; i++)
                cnt += nums[i] - nums[1];
            cout << cnt << endl;
        }
    }
    return 0;
}
```

[F - Spell Check](https://vjudge.net/problem/CodeForces-1722A)

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
int main()
{
    int t; cin >> t;
    while (t--)
    {
        int n; cin >> n;
        string s;
        cin >> s;
        sort(s.begin(), s.end());
        if (s == "Timru") cout << "YES\n";
        else cout << "NO\n";
    }
    return 0;
}
```

*22/12/21第二场*

**总结:**

第一还是要读懂题,至少要知道百分之八九十的思路才可以开始写,然后就是知识点的回顾,我似乎有点忘记`STL`的一些知识点了,事实证明不对知识点进行回顾是很难把知识点一直留在脑海的,更别说什么熟练运用,还有就是遇到什么细碎知识点就记起来吧

[A - "atcoder".substr()](https://vjudge.csgrandeur.cn/problem/AtCoder-abc264_a)

```c++
#include <iostream>
#include <string>
using namespace std;
int main()
{
    string s = "atcoder";
    int l, r;
    cin >> l >> r;
    cout << s.substr(l - 1, r - l + 1);
    return 0;
}
```

 [B - NewFolder(1)](https://vjudge.csgrandeur.cn/problem/AtCoder-abc261_c)

```c++
#include <iostream>
#include <string>
#include <map>
using namespace std;
map<string, int> ma;
int main()
{
    int n;
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        string s;
        cin >> s;
        if (!ma[s])
        {
            cout << s << endl;
            ma[s]++; 
        }
        else
        {
            cout << s << "(" << ma[s] << ")" << endl;
            ma[s]++;
        }
    }
    return 0;
}
```

[C - Counting Arrays](https://vjudge.csgrandeur.cn/problem/AtCoder-abc226_b)

getline  与 getchar

不过也可以用 `set<vector<int>>` 直接判重

```c++
#include <iostream>
#include <string>
#include <map>
using namespace std;
map<string, int> m;
int main()
{
    int n, cnt = 0;
    cin >> n;
    cin.get();
    for (int i = 0; i < n; i++)
    {
        string s;
        getline(cin, s);
        if (!m[s]) m[s]++, cnt++;
    }
    cout << cnt;
    return 0;
}
```

[D - 激光炸弹](https://vjudge.csgrandeur.cn/problem/洛谷-P2280)

题目中那句边长上的目标不会被摧毁完全是唬人.

```c++
#include <iostream>
#include <string>
#include <map>
using namespace std;
int nums[5005][5005];
int n, m, x, y, s, ans;
int main()
{
    cin >> n >> m;
    for (int i = 1; i <= n; i++)
    {
        cin >> x >> y >> s;
        nums[++x][++y] = s;
    }
    for (int i = 1; i <= 5001; i++)
        for (int j = 1; j <= 5001; j++)
            nums[i][j] += nums[i][j - 1] + nums[i - 1][j] - nums[i - 1][j - 1];
    for (int i = 1; i <= 5001 - m + 1; i++)
        for (int j = 1; j <= 5001 - m + 1; j++)
            ans = max(ans, nums[i + m - 1][j + m - 1] - nums[i - 1][j + m - 1] - nums[i + m - 1][j - 1] + nums[i - 1][j - 1]);
    cout << ans;
    return 0;
}
```

[E - Buy an Integer](https://vjudge.csgrandeur.cn/problem/AtCoder-abc146_c)

二分

```c++
#include <iostream>
#include <string>
#include <map>
using namespace std;
#define LL long long 
LL a, b, x;
LL check(LL mid)
{
    LL ret = mid;
    int cnt = 0;
    while (ret)
    {
        cnt++;
        ret /= 10;
    }
    if (a * mid + b * cnt > x) return true;
    else return false;
}
int main()
{
    cin >> a >> b >> x;
    LL l = 0, r = 1e9;
    while (l < r)
    {
        LL mid = (l + r + 1) / 2;
        if (check(mid)) r = mid - 1;
        else l = mid;
    }
    cout << l;
    return 0;
}
```

[F - Full House](https://vjudge.csgrandeur.cn/problem/AtCoder-abc263_a)

```c++
#include <iostream>
#include <string>
#include <map>
using namespace std;
int main()
{
    map<int, int> m;
    int a;
    for (int i = 1; i <= 5; i++)
    {
        cin >> a;
        m[a]++;  
    }
    if (m.size() == 2 && (m[a] == 2 || m[a] == 3))
        cout << "Yes";
    else cout << "No";
    return 0;
}
```

22/12/23第三场

总结: 理清思路再写题!!! 不然都会是浪费时间!!! 写完每一小块代码最好能浏览检查一下, 特别是代码量多的时候.

A - 语文成绩

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>
using namespace std;
int nums[5000010], scores[5000010];
int n, t, a, b, s, ans = 0x3f3f3f3f;
int main()
{
    cin >> n >> t;
    for (int i = 1; i <= n; i++)
        cin >> scores[i];
    while (t--)
    {
        cin >> a >> b >> s;
        nums[a] += s;
        nums[b + 1] -= s;
    }
    for (int i = 1; i <= n; i++) nums[i] += nums[i - 1];
    for (int i = 1; i <= n; i++)
    {
        scores[i] += nums[i];
        ans = min(scores[i], ans);
    }
    cout << ans;
    return 0;
}
```

B - Do use hexagon grid

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>
using namespace std;
int room[2010][2010];
int n, x, y, cnt;
int step[6][2] = {{1, 1}, {1, 0}, {0, -1}, {-1, -1}, {-1, 0}, {0, 1}};
bool check(int m, int n)
{
    if (room[m][n] && m >= 0 && m < 2001 && n >= 0 && n < 2001) return true;
    else return false;
}
struct str
{
    int a;
    int b;
}node[1000];
void dfs(int m, int n)
{
    for (int i = 0; i < 6; i++)
    {
        int nx = m + step[i][0];
        int ny = n + step[i][1];
        if (check(nx, ny))
        {
            room[nx][ny] = 0;
            dfs(nx, ny);
        }
    }
}
int main()
{
    cin >> n;
    memset(room, 0, sizeof room);
    for (int i = 0; i < n; i++)
    {
        cin >> x >> y;
        node[i].a = x + 1000;
        node[i].b = y + 1000; 
        room[x + 1000][y + 1000] = 1;
    }
    for (int i = 0; i < n; i++)
    {
        if (room[node[i].a][node[i].b])
            cnt++, dfs(node[i].a , node[i].b);
    }
    cout << cnt;
    return 0;
}
```

C - Minimum Varied Number

```c++
#include <iostream>
using namespace std;
int num;
long long ans;
void solve(int num, int k)
{

    if (num >= (9 - k) && num)
    {
        ans += (9 - k) * pow(10, k);
        solve(num - (9 - k), k + 1);
    }
    else
    {
        ans += num * pow(10, k);
        return;
    }
}
int main()
{
    int t;
    for (scanf("%d", &t); t--; )
    {
        ans = 0;
        cin >> num;
        solve(num, 0);
        cout << ans << endl;
    }
    return 0;
}
```

D - EKO / 砍树

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>
using namespace std;
#define LL long long
LL n, sum, h[1000010];
bool check(LL x)
{
    LL ret = 0;
    for (int i = 0; i < n; i++)
        ret += (h[i] - x > 0 ? h[i] - x : 0);
    if (ret >= sum) return true;
    else return false;
}
int main()
{
    cin >> n >> sum;
    for (int i = 0; i < n; i++) cin >> h[i];
    LL l = 0, r = 2e9;
    while (l < r)
    {
        LL mid = (r + l + 1) / 2;
        if (check(mid)) l = mid;
        else r = mid - 1;
    }
    cout << l << endl;
    return 0;
}
```

E - Atilla's Favorite Problem

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>
using namespace std;
int n, sz;
string s;
int main()
{
    cin >> n;
    while (n--)
    {
        cin >> sz;
        cin >> s;
        sort(s.begin(), s.end());
        cout << s[sz - 1] - 96 << endl;
    }
    return 0;
}
```

F - Belt Conveyor

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>
using namespace std;
char room[510][510];
int h, w, ax, ay;
int vis[510][510];
bool check(int x, int y)
{
    if (x < 1 || x > h || y > w || y < 1) return false;
    else return true;
}
void move(int x, int y)
{
    if (vis[x][y])
    {
        ax = 0;
        return;
    }
    vis[x][y] = 1;
    if (room[x][y] == 'R' && check(x, y + 1))
        move(x, y + 1);
    else if (room[x][y] == 'L' && check(x, y - 1))
        move(x, y - 1);
    else if (room[x][y] == 'U' && check(x - 1, y))
        move(x - 1, y);
    else if (room[x][y] == 'D' && check(x + 1, y))
        move(x + 1, y);
    else
    {
        ax = x; ay = y;
        return;
    }
}
int main()
{
    cin >> h >> w;
    for (int i = 1; i <= h; i++)
        for (int j = 1; j <= w; j++)
            cin >> room[i][j];
    move(1, 1);
    if (ax && ay) cout << ax  << ' ' << ay;
    else cout << -1;
    return 0;
}
```

22/12/25第四场

总结: 读题做的还行, 面对一些看似简单的题, 不妨多考虑一下反例; 还有就是能力欠缺

[A - Misjudge the Time](https://vjudge.csgrandeur.cn/problem/AtCoder-abc278_b)

```c++
#include <iostream>
#include <map>
#include <algorithm>
using namespace std;
int h, m, k;
bool Judge(int h, int m)
{
    int a = h % 10;
    int b = m / 10;
    h = h / 10 * 10 + b;
    m = a * 10 + m % 10;
    if (h >= 0 && h <= 23 && m >= 0 && m <= 59) return true;
    else return false;
}
int main()
{   
    cin >> h >> m;
    while (1)
    {
        if (Judge(h, m))
        {
            cout << h << " " << m;
            break;
        }
        m++;
        if (m == 60) h++, m = 0;
        if (h == 24) h = 0;
    }
    return 0;
}
```

[B - 铺设道路](https://vjudge.csgrandeur.cn/problem/洛谷-P5019)

转化为高度，解决一个高度，可以顺带解决其后的单调递减连续子序列，倘若遇到后一个比前一个高的，只需补充高出的那一部分就好了，因为高出的那一部分需要它自己解决，本体的本质就是所有单调递减连续子序列可以看作一个整体解决。

```c++
#include <iostream>
#include <cstring>
#include <queue>
using namespace std;
int a[100010];
int main()
{
    int n, ans = 0;
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> a[i];
    for (int i = 2; i <= n; i++) if (a[i] > a[i - 1]) ans += a[i] - a[i - 1];
    cout << ans + a[1] << endl;
    return 0;
}
```

[C - Cypher](https://vjudge.csgrandeur.cn/problem/CodeForces-1703C)

```c++
#include <iostream>
#include <map>
#include <algorithm>
using namespace std;
int t, n, m, a[105], step, ans[105];
char c;
int main()
{
    for (cin >> t; t--; )
    {
        cin >> n;
        for (int i = 0; i < n; i++) cin >> a[i];
        for (int i = 0; i < n; i++)
        {
            cin >> m;
            step = 0;
            while (cin.get(c) && c != '\n')
            {
                if (c == 'U') step--;
                else step++;
            }
            ans[i] = step + a[i] - 1 + 20;
        }
        for (int i = 0; i < n; i++)
            printf(" %d" + !i, ans[i] % 10);
        printf("\n");
    }
    return 0;
}

```

[D - Prime Path](https://vjudge.csgrandeur.cn/problem/POJ-3126)

```c++
#include <cstdio>
#include <cstring>
#include <cstdlib>
#include <algorithm>
#include <queue>
using namespace std;
const int N = 1e5 + 10;
int step[N], a, b, t, ans;
bool IsPrime[N];
void SetPrime()
{
    memset(IsPrime, 1, sizeof(IsPrime));
    IsPrime[0] = IsPrime[1] = false;
    for (int i = 2; i * i < N; i++)
    {
        if (!IsPrime[i])
            continue;
        for (int j = i * i; j < N; j += i)
            IsPrime[j] = false;
    }
}
int BFS()
{
    memset(step, 0, sizeof(step));
    queue<int> q;
    q.push(a);
    step[a] = 1;
    while (!q.empty())
    {
        int now = q.front();
        q.pop();
        if (now == b)
            return step[now] - 1;
        for (int i = 0; i < 4; i++)
        {
            for (int j = 0; j < 10; j++)
            {
                if (!j && i == 3)
                    continue;
                int nex = now, tmp = j;
                for (int k = 0; k < i; k++)
                    nex /= 10;
                nex %= 10;
                for (int k = 0; k < i; k++)
                    nex *= 10, tmp *= 10;
                nex = now - nex + tmp;
                if (!step[nex] && IsPrime[nex])
                {
                    q.push(nex);
                    step[nex] = step[now] + 1;
                }
            }
        }
    }
    return -1;
}
int main()
{
    SetPrime();
    for (scanf("%d", &t); t--;)
    {
        scanf("%d%d", &a, &b);
        if ((ans = BFS()) == -1)
            printf("Impossible\n");
        else
            printf("%d\n", ans);
    }
    return 0;
}
```

[E - Ladder Takahashi](https://vjudge.csgrandeur.cn/problem/AtCoder-abc277_c)

```

```

[F - Stripes](https://vjudge.csgrandeur.cn/problem/CodeForces-1742C)

```c++
#include <iostream>
using namespace std;
int n, a, b;
char room[10][10], ans;
int main()
{
    for (cin >> n; n--; )
    {
        // cin.get();
        // cin.get();
        for (int i = 0; i < 8; i++) cin >> room[i];
        for (int i = 0; i < 8; i++)
            {
                char ret = room[i][0];
                if (ret == '.') continue;
                for (int j = 0; j < 8; j++)
                {
                    if (room[i][j] != ret) break;
                    if (j == 7 && ret == 'R') ans = ret;
                }
            }
        for (int i = 0; i < 8; i++)
            {
                char ret = room[0][i];
                if (ret == '.') continue;
                for (int j = 0; j < 8; j++)
                {
                    if (room[j][i] != ret) break;
                    if (j == 7 && ret == 'B') ans = ret;
                }
            }
        cout << ans << endl;
    }
    return 0;
}
```

22/12/29 第五场

总结：你缺乏对细节的关注，太过想当然；写题前养成先看一遍题单的习惯。

[A - Function Run Fun](https://vjudge.csgrandeur.cn/problem/POJ-1579)

```c++
#include <algorithm>
#include <iostream>
using namespace std;
int a, b, c;
int room[30][30][30];
int cal(int x, int y, int z)
{
    if (x <= 0 || y <= 0 || z <= 0) return 1;
    else if (x > 20 || y > 20 || z > 20) return cal(20, 20, 20);
    else if (room[x][y][z]) return room[x][y][z];
    else if (a < b && b < c) return room[x][y][z] = cal(x, y, z - 1) + cal(x, y - 1, z - 1) - cal(x, y - 1, z);
    else return room[x][y][z] = cal(x - 1, y, z) + cal(x - 1, y - 1, z) + cal(x - 1, y, z - 1) - cal(x - 1, y - 1, z - 1);
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    while (cin >> a >> b >> c)
    {
        if (a == -1 && b == -1 && c == -1) break;
        printf("w(%d, %d, %d) = %d\n", a, b, c, cal(a, b, c));
    }
    return 0;
}
```

 [B - Inversion Graph](https://vjudge.csgrandeur.cn/problem/CodeForces-1638C)

```c++
#include <algorithm>
#include <iostream>
using namespace std;
int t, n, a, ans, maxn;
int main()
{
    cin >> t;
    while (t--)
    {
        cin >> n;
        maxn = 0, ans = 0;
        for (int i = 1; i <= n; i++)
        {
            cin >> a;
            maxn = max(maxn, a);
            if (maxn == i) ans++;
        }
        cout << ans << endl;
    }
    return 0;
}
```

[C - 村村通](https://vjudge.csgrandeur.cn/problem/洛谷-P1536)

```c++
#include <algorithm>
#include <iostream>
#include <set>
using namespace std;
int n, m, s[1010], x, y;
void init_set()
{
    for (int i = 1; i <= 1010; i++) s[i] = i;
}
int find_set(int x)
{
    if (s[x] != x) s[x] = find_set(s[x]);
    return s[x]; 
}
void merge_set(int x, int y)
{
    x = find_set(x); y = find_set(y);
    if (x != y) s[x] = s[y];
}
int main()
{
    while (cin >> n)
    {
        int ans = 0;
        set<int> se;
        if (!n) break;
        init_set();
        cin >> m;
        for (int i = 0; i < m; i++)
        {
            cin >> x >> y;
            merge_set(x, y);
        }
        for (int i = 1; i <= n; i++)
        {
            find_set(i);
            if (!se.count(s[i])) se.insert(s[i]);
        }
        ans = se.size() - 1;
        cout << ans << endl;
    }
}
```

[D - Caesar's Legions](https://vjudge.csgrandeur.cn/problem/CodeForces-118D)

dp ？

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>
#define INF 0x3f3f3f3f
#define MOD 100000000
using namespace std;
typedef long long LL;

int N1, N2, K1, K2;
const int maxn = 110;
int dp[maxn][maxn][2];

int main() {
    scanf("%d%d%d%d", &N1, &N2, &K1, &K2);
    for (int i = 0; i <= K1; i++) dp[i][0][0] = 1;
    for (int i = 0; i <= K2; i++) dp[0][i][1] = 1;
    for (int i = 1; i <= N1; i++) {
        for (int j = 1; j <= N2; j++) {
            for (int k = 1; k <= min(i, K1); k++) {
                dp[i][j][0] = (dp[i][j][0] + dp[i - k][j][1]) % MOD;
            }
            for (int k = 1; k <= min(j, K2); k++) {
                dp[i][j][1] = (dp[i][j][1] + dp[i][j - k][0]) % MOD;
            }
        }
    }
    int ans = (dp[N1][N2][0] + dp[N1][N2][1]) % MOD;
    printf("%d\n", ans);

    return 0;
}

//乱写？
#include <algorithm>
#include <iostream>
#include <stack>
#include <string>
#include <set>
#include <map>
using namespace std;
int n1, n2, k1, k2, ans;
map<string, bool> m;
string s, f1, f2, ret;
void dfs(string str)
{
    if (str.find(f1) != str.npos || str.find(f2) != str.npos) return;
    if (str.size() == n1 + n2)
    {
        cout << str << endl;
        ans++;
        return;
    }
    for (int i = 0; i < 2; i++)
    {
        str += ret[i];
        dfs(str);
    }
}
int main()
{
    cin >> n1 >> n2 >> k1 >> k2;
    f1.append(k1 + 1, '1');
    f2.append(k2 + 1, '2');
    ret.append("12");
    string tmp;
    dfs(tmp);
    cout << ans;
    return 0;
}
```

 [E - pb的游戏（1）](https://vjudge.csgrandeur.cn/problem/洛谷-P3150)

```c++
#include <algorithm>
#include <iostream>
using namespace std;
int main()
{
    int t, a;
    for (cin >> t; t--; )
    {
        cin >> a;
        if (a % 2) cout << "zs wins" << endl;
        else cout << "pb wins" << endl;
    }
    return 0;
}
```

[F - 超级玛丽游戏](https://vjudge.csgrandeur.cn/problem/洛谷-P1000)

```c++
#include <algorithm>
#include <iostream>
using namespace std;
int main()
{
    printf(
    "                ********\n"
    "               ************\n"
    "               ####....#.\n"
    "             #..###.....##....\n"
    "             ###.......######              ###            ###\n"
    "                ...........               #...#          #...#\n"
    "               ##*#######                 #.#.#          #.#.#\n"
    "            ####*******######             #.#.#          #.#.#\n"
    "           ...#***.****.*###....          #...#          #...#\n"
    "           ....**********##.....           ###            ###\n"
    "           ....****    *****....\n"
    "             ####        ####\n"
    "           ######        ######\n"
    "##############################################################\n"
    "#...#......#.##...#......#.##...#......#.##------------------#\n"
    "###########################################------------------#\n"
    "#..#....#....##..#....#....##..#....#....#####################\n"
    "##########################################    #----------#\n"
    "#.....#......##.....#......##.....#......#    #----------#\n"
    "##########################################    #----------#\n"
    "#.#..#....#..##.#..#....#..##.#..#....#..#    #----------#\n"
    "##########################################    ############"
    );
    return 0;
}
```

23/1/2 第五场

总结: 题目没有理解好, 递归细节也没有做好, 而且学过的东西都不能学会用

A - At Most 3 (Judge ver.)

```c++
#include <algorithm>
#include <iostream>
using namespace std;
int n, w, ans;
int a[310];
set<int> s;
void dfs(int begin, int sum, int tot)
{
    if (tot > 4 || sum > w) return;
    if (tot > 1)
        if (!s.count(sum)) s.insert(sum), ans++;
    for (int i = begin; i <= n; i++)
        dfs(i + 1, sum + a[i], tot + 1);
}
int main()
{
    cin >> n >> w;
    for (int i = 1; i <= n; i++) cin >> a[i];
    dfs(1, 0, 1);
    cout << ans;
    return 0;
}
```

B - Palindrome

最长公共子序列

```c++
#include <algorithm>
#include <iostream>
using namespace std;
int n;
char a[5010], b[5010];
int dp[2][5010];
int main()
{
    cin >> n >> a;
    for (int i = 0; i < n; i++) b[i] = a[n - 1 - i];
    int now = 0, old = 1;
    for (int i = 0; i < n; i++)
    {
        swap(now, old);
        for (int j = 0; j < n; j++)
            if (a[i] == b[j]) dp[now][j] = dp[old][j - 1] + 1;
            else dp[now][j] = max(dp[old][j], dp[now][j - 1]);
    }
    cout << n - dp[now][n - 1] << endl;
    return 0;
}
```

C - Cow Bowling

```c++
#include <algorithm>
#include <iostream>
using namespace std;
int nums[400][400];
int ans, n;
int dp[400];
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

D - ASCII code

```c++
#include <algorithm>
#include <iostream>
using namespace std;
int n;
int main()
{
    cin >> n;
    printf("%c", n);
    return 0;
}
```

E - Charm Bracelet

```c++
#include <algorithm>
#include <iostream>
using namespace std;
int n, m;
int dp[13000];
int w[3500], c[3500];
int main()
{
    cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> c[i] >> w[i];
    for (int i = 1; i <= n; i++) 
        for (int j = m; j >= c[i]; j--)
            dp[j] = max(dp[j], dp[j - c[i]] + w[i]);
    cout << dp[m];
    return 0;
}
```

F - 小A点菜

用暴搜直接超时, 必须使用dp

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

23/1/5 结训赛

总结：失误太多，很多细节没处理好，比如说数组出界直接导致WA，函数名写错，思路没有想清楚，以及思考时不能很专注地一步到位，教训就是，出bug时，在检查时就认认真真地检查一次，争取一次找出问题，这比粗略的检查十次都有用，还有就是要顺正正确的思路去思考，保持头脑清晰。

A ([1461](https://soj.csgrandeur.cn/csgoj/problemset/problem?pid=1461)) : 秘密关系

```c++
#include <iostream>
#include <algorithm>
#include <map>
#include <set>
using namespace std;
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    map<int, set<int>> gra;
    int n;
    cin >> n;
    while (n--)
    {
        int a, b;
        cin >> a >> b;
        gra[a].insert(b);
        gra[a].insert(a);
    }
    cin >> n;
    while (n--)
    {
        int x;
        cin >> x;
        int ans = 0;
        if (gra.find(x) != gra.end()) ans = gra[x].size();
        cout << ans << endl;
    }
    return 0;
}
```

D ([1464](https://soj.csgrandeur.cn/csgoj/problemset/problem?pid=1464)) : 小组作业

数组越界直接导致wa，吸取教训！

```c++
#include <iostream>
#include <algorithm>
#include <vector>
#include <cstring>
#include <map>
#include <set>
using namespace std;
const int maxn = 1e7 + 10;
int n, m, a, b, cnt;
int s[maxn];
bool flag[maxn];
int find_set(int x)
{
    if (x != s[x]) s[x] = find_set(s[x]);
    return s[x];
}
void add_merge(int x, int y)
{
    int e1 = find_set(x);
    int e2 = find_set(y);
    if ((e1 != e2) && (!flag[x] || !flag[y]))
    {
        cnt--;
        s[e1] = s[e2];
        flag[x] = 1;
        flag[y] = 1;
    }
}
int main()
{
    cin >> n >> m;
    cnt = n;
    for (int i = 0; i < maxn; i++) s[i] = i;
    for (int i = 1; i <= m; i++)
    {
        cin >> a >> b;
        add_merge(a, b);
    }
    cout << cnt;
    return 0;
}
```

G ([1467](https://soj.csgrandeur.cn/csgoj/problemset/problem?pid=1467)) : 没有题面的神秘题目-2

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

K ([1471](https://soj.csgrandeur.cn/csgoj/problemset/problem?pid=1471)) : Coupon Collector’s Problem

**数学期望公式**  $\sum_{i=1}^{n}{\frac{n}{i}}$ 

```c++
#include <iostream>
#include <algorithm>
using namespace std;
using LL = long long;
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    double n;
    cin >> n;
    double ans = 0;
    for (double i = 1; i <= n; i++)
        ans += 1.0 * n / i;
    printf("%.6f\n", ans);
    return 0;
}
```

L ([1472](https://soj.csgrandeur.cn/csgoj/problemset/problem?pid=1472)) : Blover的花店

```c++
#include <iostream>
#include <algorithm>
#include <set>
using namespace std;
using LL = long long;
const int maxn = 1e5 + 10;
int a[maxn], n;
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    set<int> se;
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> a[i];
    int l = 1, r = 1, ans = 0;
    while (r <= n)
    {
        if (se.find(a[r]) == se.end()) se.insert(a[r++]);
        else se.erase(se.find(a[l++]));
        ans = max(ans, r - l);
    }
    cout << ans;
    return 0;
}
```

2021GDCPC广东省大学生程序设计竞赛(重现赛)

[A-An Easy Problem](https://ac.nowcoder.com/acm/contest/50921/A)

特别注意类型转换

```c++
//
#include <iostream>
#include <algorithm>
#include <queue>
using namespace std;
int n, m, k;
int main()
{
    cin >> n >> m >> k;
    priority_queue<pair<long long, int>> q;
    for (int i = 1; i <= n; i++) q.push(pair(1LL * i * m, i));
    while (--k)
    {
        pair<long long, int> tmp = q.top(); q.pop();
        tmp.first -= 1LL * tmp.second;
        q.push(tmp);
    }
    cout << q.top().first << endl;
    return 0;
}


//二分法
#include <iostream>
#include <algorithm>
using namespace std;
int n, m;
long long k;
bool check(long long x)  //<= mid的有几个数
{
    long long ans = 0;
    for (int i = 1; i <= n; i++)  //遍历每行
    {
        long long t = x / i;
        if (t > m) ans += m;
        else ans += t;
    }
    return ans >= k;
}
void find_bin()
{
    long long l = 1, r = 1LL * n * m;
    k = 1LL * n * m - k + 1;  //第k大就是第n*m-k+1小
    while (l < r)
    {
        long long mid = (l + r) / 2;
        if (check(mid)) r = mid;
        else l = mid + 1;
    }
    cout << l << endl;
}
int main()
{
    cin >> n >> m >> k;
    find_bin();
    return 0;
}
```

[B-Byfibonacci](https://ac.nowcoder.com/acm/contest/50921/B)

```c++
//Failed Trying
#include <iostream>
#include <algorithm>
#include <cstring>
#include <cmath>
#include <queue>
#include <map>
using namespace std;
const int INF = 0x3f3f3f3f;
const int N = 2e5 + 10;
long long t, sum, ret;
map<int, int> fibo;
void set_fibo()
{
    fibo[1] = 1; fibo[2] = 1;
    int a = 1, b = 2;
    while (b <= 1e7)
    {
        int c = a + b;
        fibo[c] = 1;
        a = b; b = c;
    }
}
void val()
{
    int n; cin >> n;
    sum = 0; ret = n;
    queue<int> q;
    q.push(n);
    while (q.size())
    {
        int tmp = q.front(); q.pop();
        ret /= tmp;
        if (tmp == 1) continue;
        if (fibo[tmp]) fibo[tmp] = 1;
        for (int i = 1; i <= tmp; i++)
        {
            if (fibo[i] == 1 && fibo[tmp - i] == 1)
            {
                q.push(i); q.push(tmp - i);
                fibo[i] = fibo[tmp - i] = 2;
                ret *= (1LL * i * (tmp - i));
                sum += ret % 998244353;
                break;             
            }
        }
    }
}
int main()
{
    set_fibo();
    for (cin >> t; t--; )
    {
        val();
        cout << sum % 998244353 << endl;
    }
    return 0;
}
```

[D-Double](https://ac.nowcoder.com/acm/contest/50921/D)

```

```

[L-League of Legends](https://ac.nowcoder.com/acm/contest/50921/L)

数学期望计算

```c++
#include <iostream>
using namespace std;
int main()
{
    cout << "3.5";
    return 0;
}
```



#### Atcoder

[D - Change Usernames (atcoder.jp)](https://atcoder.jp/contests/abc285/tasks/abc285_d)

```c++
#include <iostream>
#include <algorithm>
#include <queue>
#include <map>
using namespace std;
const int N = 2e5 + 10;
int n, cnt;
map<string, int> m;
vector<int> e[N];
int indegree[N];
int main()
{
    cin >> n;
    for (int i = 1; i <= n; i++)
    {
        string a, b;
        cin >> a >> b;
        int u, v;
        if (m[a]) u = m[a];
        else u = m[a] = ++cnt;
        if (m[b]) u = m[b];
        else v = m[b] = ++cnt;
        e[u].push_back(v);
        indegree[v]++
    }
    priority_queue<int, vector<int>, greater<int>> q;
    int num = cnt;
    for (int i = 1; i <= cnt; i++)
        if (!indegree[i]) num--, q.push(i);
    while (q.size())
    {
        int tmp = q.top(); q.pop();
        for (int i: e[tmp])
        {
            indegree[i]--;
            if (!indegree[i]) num--, q.push(i);
        }
    }
    if (num) cout << "Yes";
    else cout << "No";
}
```

[C - Rotate and Palindrome (atcoder.jp)](https://atcoder.jp/contests/abc286/tasks/abc286_c)

只有调换和修改的操作, 调换直接双倍字符串遍历即可, 修改直接两边比较

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
using namespace std;

void Solve()
{
    int n; LL a, b;
    cin >> n >> a >> b;
    string s; cin >> s;
    s = s + s;
    LL ans = INF;
    for (int i = 0; i < n; i++)
    {
        LL sum = a * i;
        for (int j = 0; j < n / 2; j++)
        {
            int le = j + i; 
            int ri = n - 1 - j + i;
            if (s[le] != s[ri]) sum += b;
        }
        ans = ans > sum ? sum : ans;
    }
    cout << ans << endl;
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

[A - CAPS LOCK (atcoder.jp)](https://atcoder.jp/contests/abc292/tasks/abc292_a)

学习`toupper()`函数, 接受一个字符, 并返回其大写; 同理还有`tolower`

```c++
// Let C be uppercased c
//char C = toupper(c);

#include <bits/stdc++.h>
using namespace std;
LL ans;
int n;
int main()
{
    string s; cin >> s;
    string T;
    for (int i = 0; i < s.size(); i++)
        s[i] = toupper(s[i]);
        // T += toupper(s[i]);
    cout << s;
    // cout << T;
    return 0;
}
```

[D - Tying Rope (atcoder.jp)](https://atcoder.jp/contests/abc293/tasks/abc293_d)

```c++
#include <bits/stdc++.h>
const int N = 4010;
using namespace std;

int s[N];
int f[N];
int find_set(int x)
{
    if (x != s[x]) s[x] = find_set(s[x]);
    return s[x];
}
void merge_set(int x, int y)
{
    int nx = find_set(x);
    int ny = find_set(y);
    if (nx != ny)
    {
        f[nx] += f[ny];
        s[ny] = nx;
    }
}
int main()
{
    int aa = 0, ab = 0;
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <= 2 * n; i++)  s[i] = i, f[i] = -1;
    for (int i = 1; i <= n; i++)  merge_set(i, i + n);
    for (int i = 1; i <= m; i++)
    {
        int a, b; char c, d;
        cin >> a >> c >> b >> d;
        if (c == 'B') a += n; if (d == 'B') b += n; 
        merge_set(a, b);
        f[find_set(a)] += 2;
    }
    for (int i = 1; i <= 2 * n; i++) if (find_set(i) == i) {if (f[i] == 0) aa++; else ab++;}
    cout << aa << ' ' << ab;
    return 0;
}   
```

[E - 2xN Grid (atcoder.jp)](https://atcoder.jp/contests/abc294/tasks/abc294_e)

类似于指针，根据上下长度的大小关系移动指针即可

```c++
#include <bits/stdc++.h>
using namespace std;
typedef long long LL;
const int maxn = 2e5 + 10;
int v[3][maxn];
LL l[3][maxn];
int main()
{
    LL a; cin >> a;
    int n1, n2; cin >> n1 >> n2;
    for (int i = 1; i <= n1; i++)
        cin >> v[1][i] >> l[1][i];
    for (int i = 1; i <= n2; i++)
        cin >> v[2][i] >> l[2][i];
    int x = 1, y = 1, v1 = 0, v2 = 0;
    LL t, ans = 0, tot1 = 0, tot2 = 0;
    while (x <= n1 || y <= n2)
    {
        while (x <= n1 && tot1 <= tot2)
        {
            t = tot1;
            tot1 += l[1][x];
            v1 = v[1][x];
            if (v1 == v2) ans += min(tot1 - t, tot2 - t);
            x++;
        }
        while (y <= n2 && tot2 <= tot1)
        {
            t = tot2;
            tot2 += l[2][y];
            v2 = v[2][y];
            if (v1 == v2) ans += min(tot1 - t, tot2 - t);
            y++;
        }
    }
    cout << ans << endl;
    return 0;
    
}
```

[D - Three Days Ago (atcoder.jp)](https://atcoder.jp/contests/abc295/tasks/abc295_d)

```c++
#include<bits/stdc++.h>
using namespace std;
using ll = long long;
const int mod = 1e9 + 7;
const int N = 5e5 + 10;
int dp[2][2][2][2][2][2][2][2][2][2];
int a[10];
ll ans;
int cnt, n;
string s;
int main()
{ 
    cin >> s;
    n = s.length();
    dp[0][0][0][0][0][0][0][0][0][0] = 1;
    s = '?' + s;
    for (int i = 1; i <= n; i++)
    {
        a[s[i] - '0']++;
        a[s[i] - '0'] %= 2;
        ans += dp[a[0]][a[1]][a[2]][a[3]][a[4]][a[5]][a[6]][a[7]][a[8]][a[9]];
        dp[a[0]][a[1]][a[2]][a[3]][a[4]][a[5]][a[6]][a[7]][a[8]][a[9]]++;
    }
    cout << ans <<"\n";
}
```

[E - Kth Takoyaki Set (atcoder.jp)](https://atcoder.jp/contests/abc297/tasks/abc297_e)

题目大意: 任意组合得到的价格的第 `k` 小 (每种价格不限数量)

思路: 一开始想用 `dp` , 但是明显开不了那么大的数组, 所以换一种思路, 使用小顶堆的 `priority_queue` , 每次取当前最小价格, 并与所有价格结合一次, 放入队列, 重复操作直到得到第 `k` 小, 注意还要判断价格是否已经出现过. 

```c++
#include <bits/stdc++.h>
using namespace std;
typedef long long LL;
LL num[12];
int main()
{
    int n, k; cin >> n >> k;
    for (int i = 1; i <= n; i++) cin >> num[i];
    priority_queue<LL, vector<LL>, greater<LL>> p;
    set<LL> s;
    int cnt = 0;
    p.push(0);
    while (1)
    {
        LL now = p.top(); p.pop();
        if (s.count(now)) continue;
        for (int i = 1; i <= n; i++) p.push(now + num[i]);
        cnt++;
        s.insert(now);
        if (cnt == k + 1) {cout << now; break;}
    }
    return 0;
}
```

[E - Isolation (atcoder.jp)](https://atcoder.jp/contests/abc302/tasks/abc302_e)

```c++
#include <bits/stdc++.h>
using namespace std;
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0); cout.tie(0);
    int n, q;
    cin >> n >> q;
    vector<int> del(n, 0), del_time(n, -1);
    vector<vector<array<int, 2>>>gra(n);
    int ans = n;
    for (int i = 0; i < q; i++)
    {
        int k, u, v;
        cin >> k >> u;
        u--;
        if (k == 1)
        {
            cin >> v;
            v--;
            gra[u].push_back({v, i});
            gra[v].push_back({u, i});
            if (gra[v].size() - del[v] == 1) ans--;
            if (gra[u].size() - del[u] == 1) ans--;
        }
        else
        {
            if (gra[u].size() - del[u] != 0) ans++;
            for (auto [nex, t] : gra[u])
            {
                if (t < del_time[nex]) continue;
                del[nex]++;
                if (gra[nex].size() - del[nex] == 0) ans++;
            }
            gra[u].clear();
            del_time[u] = i;
            del[u] = 0;
        }
        cout << ans << endl;
    }
    return 0;
}
```

[C - Standings](https://atcoder.jp/contests/abc308/tasks/abc308_c)

```C++
#include <iostream>
#include <algorithm>
using namespace std;
int n, a[2 << 17], b[2 << 17], idx[2 << 17];
int main()
{
	ios::sync_with_stdio(false);
	cin.tie(nullptr);
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		cin >> a[i] >> b[i];
		idx[i] = i;
	}
	sort(idx, idx + n, [](int l, int r)   // worth learning
	{
		if ((long)a[l] * (a[r] + b[r]) != (long)a[r] * (a[l] + b[l]))
			return (long) a[l] * (a[r] + b[r]) > (long) a[r] * (a[l] + b[l]);
		return l < r;
	});
	for (int i = 0; i < n; i++) cout << idx[i] + 1 << (i + 1 == n ? "\n" : " ");
	return 0;
}
```

[D - Snuke Maze](https://atcoder.jp/contests/abc308/tasks/abc308_d)

```c++
#include <iostream>
#include <algorithm>
#include <queue>
using namespace std;
int h, w;
string s[500];
bool dp[500][500][5];
const int d[5] = {0, 1, 0, -1};
int main()
{
	ios::sync_with_stdio(false);
	cin.tie(nullptr);
	cin >> h >> w;
	for (int i = 0; i < h; i++) cin >> s[i];
	dp[0][0][0] = true;
	queue<pair<pair<int, int>, int>> Q;
	Q.push(make_pair(make_pair(0, 0), 0));
	bool ans = false;
	while (!Q.empty())
	{
		int x = Q.front().first.first , y = Q.front().first.second;
		int k = Q.front().second;
		Q.pop();
		if ("snuke"[k % 5] != s[x][y]) continue;
		if (x == h - 1 && y == w - 1) ans = true;
		for (int r = 0; r < 4; r++)
		{
			int tx = x + d[r], ty = y + d[r + 1];
			if (tx < 0 || tx >= h || ty < 0 || ty >= w) continue;
			int nk = (k + 1) % 5;
			if (dp[tx][ty][nk]) continue;
			dp[tx][ty][nk] = true;
			Q.push(make_pair(make_pair(tx, ty), nk));
		}
	}
	cout << (ans ? "Yes" : "No");
	return 0;

}
```

[E - MEX](https://atcoder.jp/contests/abc308/tasks/abc308_e)

```c++
#include <iostream>
#include <cassert>
#include <vector>
using namespace std;
const int maxn = 2e5 + 10;
int n;
int num[200010];
string str;
int cal(int a, int b, int c)
{
	for (int i = 0; i <= 3; i++)
		if (i != a && i != b && i != c)
			return i;
}
int main()
{
	cin >> n;
	for (int i = 1; i <= n; i++) cin >> num[i];
	cin >> str; str = ' ' + str;
	vector<vector<int>> v1(maxn, vector<int>(3)), v2(maxn, vector<int>(3));
	for (int i = 1; i <= n; i++)
	{
		v1[i] = v1[i - 1];
		if (str[i] == 'M') v1[i][num[i]]++;
	}
	for (int i = n; i >= 1; i--)
	{
		v2[i] = v2[i + 1];
		if (str[i] == 'X') v2[i][num[i]]++;
	}
	long long ans = 0;
	for (int i = 1; i <= n; i++)
	{
		if (str[i] != 'E') continue;
		for (int j = 0; j <= 2; j++)
			for (int k = 0; k <= 2; k++)
				ans += 1LL * v1[i][j] * v2[i][k] * cal(num[i], j, k);
	}
	cout << ans << endl;
	return 0;
}
```

[A - Divide String](https://atcoder.jp/contests/arc163/tasks/arc163_a)

```c++
#include <bits/stdc++.h>
using namespace std;
int main()
{
	int t;
	for (cin >> t; t--; )
	{
		auto ac = []()
		{
			string s; cin >> s;
			for(int i = 1; i < s.size(); ++i)
				if(s.substr(0, i) < s.substr(i)) {cout << "Yes\n"; return;}	
			cout << "No\n";
		};
		ac();
	}
	return 0;
}
```



#### Codeforces

[Problem - C - Codeforces](https://codeforces.com/contest/1792/problem/C)

```c++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
void Solve()
{
    int n;
    cin >> n;
    vector<int> p(n);
    for (int i = 0; i < n; i++)
    {
        int x;
        cin >> x;
        x--;
        p[x] = i;
    }
    
    int l = n / 2, r = n - l;
    while (l > 0 && p[l - 1] < p[l] && p[r] > p[r - 1])
    {
        l--, r++;
    }
    cout << l << "\n";
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie();
    int t;
    for (cin >> t; t--; )
        Solve();
    return 0;
}
```

[Problem - G2 -Subsequence Addition (Hard Version) Codeforces](https://codeforces.com/contest/1807/problem/G2)

很有意思的数学结论, 例如 $1, 1, 2, 3, 5$ , 往后取的每一个数, 只要不大于前面的数的总和, 就一定能被前面若干数取和而得到. 也就是说, 从数字 $1$ 开始, 往后取的每一个数范围在 $[1, sum]$ 之间, 则该数一定可以被前面数的子集求和得到, `sum`是从1开始到该数前一个数的所有数的总和. 每次都取最小值, 数列将是 $1, 1, 1, 1, 1, 1...$ , 每次都取最大值, 数列将是 $1, 1, 2, 4, 8, 16, 32, 64...$ , 这两个数列最容易理解, 而取中间的数也是同样适用的

```c++
#include <bits/stdc++.h>
using namespace std;
 
vector<int> num;
int main()
{
	int t; cin >> t;
	while (t--)
	{
		int n; cin >> n;
		num.clear();
		for (int i = 1; i <= n; i++)
		{
			int x; cin >> x; 
			num.push_back(x);
		}
		sort(num.begin(), num.end(), less<int> ());
		long long sum = 1;
		int flag = 0;
		if (n == 1 && num[0] != 1) 
			{cout << "NO" << endl; continue;}
		for (int i = 1; i < n; i++)
		{
			if (num[i] > sum) {flag = 1; break;}
			else sum += num[i];
		}
		if (flag) cout << "NO"; else cout << "YES";
		cout << endl;
	}
	return 0;
}
```

[Problem - E - Living Sequence - Codeforces](https://codeforces.com/contest/1811/problem/E)

题意: 求数位中不包括数字 $4$ 的所有数字的第 `k` 个; 求解此问题之前, 我们先思考一个问题, 数位中只包括 $0$ 和 $1$ 的所有数字的第 `k` 个 (从 $0$ 开始) 是多少, 显然, 把 `k` 转换为二进制数字, 那就是我们所求的第 `k` 个数. 那么同样的道理, 如果我们要求数位只含 $0 ~ 8$ 这九个数的数字的第 `k` 个是多少, 也需要将其转换为九进制数, 便是我们所要求的答案, 而题目要求的不是 $[0,8]$, 而是 $[0,3], [5,9]$, 所以求出后, 我们需要将 $[4,8]$ 的数都向上移动 $1$ 位, 即 $+ 1$, 便是答案. 

```c++
#include <bits/stdc++.h>
using namespace std;
void Solve(long long x)
{
    vector <int> num;
    while (x)
    {
        num.push_back(x % 9LL);
        x /= 9LL;
    }
    reverse(num.begin(), num.end());
    for (auto v : num)
    {
        if (v > 3) cout << v + 1;
        else cout << v;
    }
    cout << endl;
}
int main()
{
    int t; cin >> t;
    while (t--)
    {
        long long n; cin >> n;
        Solve(n);
    }
    return 0;
}
```

[C. Rudolf and the Another Competition](https://codeforces.com/contest/1846/problem/C)

```c++
#include <bits/stdc++.h>
using namespace std;
int main()
{
	ios::sync_with_stdio(false);
	cin.tie(NULL);
	int t;
	for (cin >> t; t--; )
	{
		vector<pair<int, long long>> vec;
		int n, m, h;
		cin >> n >> m >> h;
		pair<int, long long> key;
		for (int i = 0; i < n; i++)
		{
			vector<int> a(m);
			for (int j = 0; j < m; j++) cin >> a[j];
			sort(a.begin(), a.end());
			long long sum = 0, tmp = 0; int cnt = 0;
			for (int j = 0; j < m; j++)
			{
				if (tmp + a[j] > h) break;
				cnt++;
				tmp += a[j];
				sum += tmp;
			}
			pair<int, long long> p = {-cnt, sum};
			vec.push_back(p);
			if (i == 0) key = p;
		}
		sort(vec.begin(), vec.end());
		for (int i = 0; i < vec.size(); i++)
			if (vec[i] == key)
			{
				cout << i + 1 << endl;
				break;
			}
	}
	return 0;
}
```

[E2. Rudolf and Snowflakes (hard version)](https://codeforces.com/contest/1846/problem/E2)

```c++
#include <bits/stdc++.h>
using namespace std;
int main()
{
	ios::sync_with_stdio(false);
	cin.tie(NULL);

	set<long long> se;
	for (long long k = 2; k <= 1e6; k++)
	{
		long long val = 1 + k + k * k + k * k * k;
		long long pw = k * k * k;
		se.insert(val);
		while (val < 1e18)
		{
			if (pw <= 1e18 / k)
			{
				pw *= k;
				val += pw;
				se.insert(val);
			}
			else break;
		}
	}
	int t;
	for (cin >> t; t--; )
	{
		long long n; cin >> n;
		bool f = false;
		long long l = 0, r = 1e9;
		while (l < r)
		{
			long long mid = l + r >> 1;
			if (1 + mid + mid * mid >= n) r = mid;
			else l = mid + 1;
		}
		if (l >= 2 && 1 + l + l * l == n) f = true;
		if (!f && se.count(n)) f = true;
		cout << (f ? "YES" : "NO") << endl;
	}
	return 0;
}
```

[E. Data Structures Fan](https://codeforces.com/contest/1872/problem/E)

本题需要掌握异或的知识点, 异或可以通过前缀处理的方法实现快速得到区间异或值, 类似于前缀和与前缀差, 原理就是两个相同的数异或得到0, 即一个数被异或两次就等价于没有异或. 然后就是动态存储的问题了, 在本题中也不需要真的去改变`string` 中的`0`和`1`, 而是直接存储`0`的位置的数的异或值即可, 然后动态维护这个值, 一旦有某个区间发生改变, 就异或上这个区间的异或值即可, 由于相同为0, 不同为1的原则, 这个值所代表的意义永远不会改变. 

```c++
#include <bits/stdc++.h>
using namespace std;
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int t;
    for (cin >> t; t--; )
    {
        int n; cin >> n;
        vector<int> ve(n);
        for (int i = 0; i < n; i++) cin >> ve[i];
        vector<int> S(n + 1);
        for (int i = 0; i < n; i++) S[i + 1] = S[i] ^ ve[i];
        string s; cin >> s;
        long long x = 0;
        for (int i = 0; i < n; i++)
            if (s[i] == '0')
                x ^= ve[i];
        int q, op;
        for (cin >> q; q--; )
        {
            cin >> op;
            if (op == 1)
            {
                int l, r; cin >> l >> r;
                l--;
                x ^= S[l] ^ S[r];
            }
            else
            {
                int r; cin >> r;
                if (r == 0) cout << x << ' ';
                else cout << (x ^ S[n]) << ' ';
            }
        }
        cout << endl;
    }
    return 0;
}
```

[F. Selling a Menagerie](https://codeforces.com/contest/1872/problem/F)

关键是把题中所表达的关系转化为有向图, 就会比较好理解. 存储每个点的出度, 先解决链式关系, 留下成环的关系后, 再来解决环即可. 处理环的过程中, 由于必然会有一个点以原本的价值卖出, 所以找到那个最小的点, 其他按照链式关系卖出即可. 

```c++
#include <bits/stdc++.h>
using namespace std;
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int t;
    for (cin >> t; t--; )
    {
        int n; cin >> n;
        vector<int> a(n);
        for (int i = 0; i < n; i++) cin >> a[i], a[i]--;
        vector<int> c(n);
        for (int i = 0; i < n; i++) cin >> c[i];
        vector<int> ind(n, 0);
        for (int i = 0; i < n; i++) ind[a[i]]++;
        queue<int> Q;
        for (int i = 0; i < n; i++)
            if (ind[i] == 0) 
                Q.push(i);
        vector<int> p;
        while (!Q.empty())
        {
            int v = Q.front();
            Q.pop();
            p.push_back(v);
            ind[a[v]]--;
            if (ind[a[v]] == 0) Q.push(a[v]);
        }
        vector<bool> vis(n, false);
        for (int i = 0; i < n; i++)
        {
            if (ind[i] == 1 && vis[i] == 0)
            {
                vector<int> P;
                for (int k = i; !vis[k]; k = a[k])
                {
                    vis[k] = true;
                    P.push_back(k);
                }
                int cnt = P.size();
                int x = 0;
                for (int k = 1; k < cnt; k++)
                    if (c[P[k]] < c[P[x]]) x = k;
                for (int k = 1; k <= cnt; k++)
                    p.push_back(P[(x + k) % cnt]);
            }
        }
        for (int i = 0; i < n; i++)
            cout << p[i] + 1 << (i == n - 1 ? "\n" : " ");
    }
    return 0;
}
```

[G. Replace With Product](https://codeforces.com/contest/1872/problem/G)

```c++
#include <bits/stdc++.h>
using namespace std;
#define LL long long
void solve()
{
    int n; cin >> n;
    vector<int> a(n);
    for (int i = 0; i < n; i++) cin >> a[i];
    LL tot = 1;
    for (int i = 0; i < n; i++)
    {
        if (INT64_MAX / a[i] <= tot)
            tot = INT64_MAX;
        else tot *= a[i];
    }
    if (tot == INT64_MAX) 
    {
        int l = 0, r = n - 1;
        while (a[l] == 1) l++;
        while (a[r] == 1) r--;
        cout << l + 1 << ' ' << r + 1 << endl;
    }
    else
    {
        array<LL, 3> best = {0, 0, 0};
        vector<LL> sum(n + 1), mul(n + 1);
        sum[0] = 0, mul[0] = 1;
        vector<int> pos;
        for (int i = 0; i < n; i++)
        {
            sum[i + 1] = sum[i] + a[i];
            mul[i + 1] = mul[i] * a[i];
            if (a[i] > 1) pos.push_back(i);
        }
        for (int l : pos)
            for (int r : pos)
                if (l < r)
                    best = max(best, {mul[r + 1] / mul[l] - sum[r + 1] + sum[l], l, r});
        cout << best[1] + 1 << ' ' << best[2] + 1 << endl;
    }
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int t;
    for (cin >> t; t--; )
    {
        solve();
    }
    return 0;
}
```



####  lanqiao

[P8748 蓝桥杯 2021 省 B 时间显示 - 洛谷](https://www.luogu.com.cn/problem/P8748)

```c++
#include <bits/stdc++.h>
using namespace std;
typedef long long LL;

LL n;
int main()
{
    cin >> n;
    int a, b, c, d;
    n /= 1000;
    a = n / 60 / 60 % 24;
    b = n / 60 % 60;
    c = n % 60;
    printf("%0.2d:%0.2d:%0.2d", a, b, c);
    return 0;
}
```

[P8684 蓝桥杯 2019 省 B 灵能传输 - 洛谷](https://www.luogu.com.cn/problem/P8684)

转换为前缀和，对前缀和进行操作使得每个项之间的差的绝对值的最大值最小，显然对其排序，使得前缀和序列成为单调序列时，各项之间差的绝对值的最大值最小，但是由于`s0` 和 `sn` 项是无法移动的，因为可以操作的只能是 $[2, n - 1]$ ，所以要记录排序之后`s0` 和 `s1` 的位置，然后 `s0` 先向左遍历至最小值，再遍历至最右端即最大值处，最后再遍历至 `sn`， 还需要注意的是，为了避免遍历时重复遍历某一个数，在有重复的部分要隔两个进行遍历，即先后的遍历分别错位。

```c++
#include <bits/stdc++.h>
using namespace std;

typedef long long LL;
const int N = 300010;
int n;
LL sum[N], a[N], s0, sn;
bool st[N];
int main()
{
    int t; cin >> t; 
    while (t--)
    {
        cin >> n;
        sum[0] = 0;
        for (int i = 1; i <= n; i++)
        {
            cin >> sum[i];
            sum[i] += sum[i - 1];
        }
        s0 = sum[0]; sn = sum[n];
        if (s0 > sn) swap(s0, sn);
        sort(sum, sum + n + 1);
        for (int i = 0; i <= n; i++)
            if (s0 == sum[i])
            {
                s0 = i;
                break;
            }
        for (int i = n; i >= 0; i--)
            if (sn == sum[i])
            {
                sn = i; 
                break;
            }
        memset(st, 0, sizeof st);
        int l = 0, r = n;
        for (int i = s0; i >= 0; i -= 2)
        {
            a[l++] = sum[i];
            st[i] = true;
        }
        for (int i = sn; i <= n; i += 2)
        {
            a[r--] = sum[i];
            st[i] = true;
        }
        for (int i = 0; i <= n; i++)
            if (!st[i]) a[l++] = sum[i];
        LL res = 0;
        for (int i = 1; i <= n; i++)
            res = max(res, abs(a[i] - a[i - 1]));
        cout << res << endl;
    }
    return 0;
}
```

[P8720 蓝桥杯 2020 省 B2 平面切分 - 洛谷](https://www.luogu.com.cn/problem/P8720)

分两种情况讨论：1. 若新加入的直线不与平面中任何一条直线重合，设该直线与平面中已经存在的直线的不同的交点数为`s`，那么部分数加`s+1`；2. 否则，部分数不变。注意可以使用`set`来维护交点的不同

```c++
#include <bits/stdc++.h>
using namespace std;

typedef pair<double, double> pdd;
const int N = 1e3 + 5;
int n, ans;
double a[N], b[N];
bool vis[N];
int main()
{
    cin >> n;
    for (int i = 1; i <= n; i++)
    {
        cin >> a[i] >> b[i];
        set<pdd> se;
        se.clear();
        for (int j = 1; j < i; j++)
        {
            if (vis[j]) continue;
            if (a[i] == a[j] && b[i] == b[j])
            {
                vis[i] = 1; break;
            }
            if (a[i] == a[j]) continue;
            se.insert(pdd((b[i] - b[j])/(a[j] - a[i]), (a[j] * b[i] - a[i] * b[j])/(a[j] - a[i])));

        }
        if (vis[i] == 0) ans += se.size() + 1;
    }
    cout << ans + 1 << endl;
    return 0;
}
```

[P8715 蓝桥杯 2020 省 AB2 子串分值 - 洛谷](https://www.luogu.com.cn/problem/P8715)

本题一开始的思路是遍历窗口大小, 从[2, n], 维护每个时刻内窗口内部仅出现一次的字母的数量, 然后将值全部加起来, 但是这样的话, 总的时间复杂度会到达 $O()$ , 在此题的数据量下会导致TLE, 所以采用的是另一种巧妙的方法, 由于题目中要求的是每个子区间内仅出现一次的字符的个数, 所以转换思维, 遍历该字符串, 记录遍历到的每个字母它上一次出现的位置和下一次出现的位置, 那在这段区间内该字母就只出现一次, 符合题目的要求, 所以给答案加上 `(i - pre[i]) * (-i + nex[i])` , 这是仅包含一个该字母的子区间个数, 也是这些区间内该仅出现一次的字母的出现次数, 两者是等值的.

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 100010;
string s;
int pre[N], nex[N], idx[200];
int main()
{
	cin >> s;
	int n = s.size();
	s = ' ' + s;
	for (int i = 1; i <= n; i++)
	{
		pre[i] = idx[s[i]];
		idx[s[i]] = i; 
	}
	for (int i = 97; i <= 122; i++)
	{
		idx[i] = n + 1;
	}
	for (int i = n; i >= 1; i--)
	{
		nex[i] = idx[s[i]];
		idx[s[i]] = i;
	}
	long long ans = 0;
	for (int i = 1; i <= n; i++)
		ans += 1LL * (i - pre[i]) * (-i + nex[i]);
	cout << ans;
	return 0;
}
```

[P8716 蓝桥杯 2020 省 AB2 回文日期 - 洛谷](https://www.luogu.com.cn/problem/P8716)

巧妙处理字符与数字的手法, 包括计算和转换

```c++
#include <bits/stdc++.h>
using namespace std;

string s;
int month[13] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
int f1, f2;
bool check(int x)
{
	if ((x % 4 == 0 && x % 100 != 0) || (x % 400 == 0))
		return true;
	return false;
}
int main()
{
	cin >> s;
	int a = atoi(s.substr(0, 4).c_str());
	int b = atoi(s.substr(4, 2).c_str());
	int c=  atoi(s.substr(6, 2).c_str());
	int y = a, m = (((a % 10) * 10) + a / 10 % 100), d = (((a % 1000) / 100 * 10) + (a / 1000));
	if (m <= 12 && m > 0)
	{
		string A = to_string(y);
		if ((m == 2 && d <= (month[2] + check(y))) || (d <= month[m]))
		{
			if (b <= m && c < d)
			printf("%d%.02d%.02d\n", y, m, d), f1 = 1;
			if (b <= m && c < d && A[0] == A[2] && A[1] == A[3] && A[0] != A[1])
			printf("%d%.02d%.02d\n", y, m, d), f2 = 1;
		}
	}

	while (++a < 9999 || !(f1 && f2))
	{
		int y = a, m = (((a % 10) * 10) + a / 10 % 10), d = (((a % 1000) / 100 * 10) + (a / 1000));
		string A = to_string(a);
		if (m == 2)
		{
			if (d <= (28 + check(a)))
			{
				if (f1 == 0)
					printf("%d%.02d%.02d\n", y, m, d), f1 = 1;
				if (f2 == 0 && A[0] == A[2] && A[1] == A[3] && A[0] != A[1])
					printf("%d%.02d%.02d\n", y, m, d), f2 = 1;
			}
		}
		else if (m <= 12 && m > 0)
		{
			if (d <= month[m])
			{
				if (f1 == 0)
					printf("%d%.02d%.02d\n", y, m, d), f1 = 1;
				if (f2 == 0 && A[0] == A[2] && A[1] == A[3] && A[0] != A[1])
					printf("%d%.02d%.02d\n", y, m, d), f2 = 1;
			}
		}
	}
	return 0;
}
```

[积木画](https://www.lanqiao.cn/problems/2110/learning/?page=1&first_category_id=1&sort=students_count&name=积木画)

涉及取模最好开 `long long` , 可以避免一些加法的超限, 而涉及减法的取模, 一定要在最后加上 `mod` , 防止负数出现

```c++
#include <iostream>
using namespace std;
const int N = 1e7 + 10;
const int mod = 1e9 + 7;
long long dp[N][3];
int n;
int main()
{
    cin >> n;
    dp[0][0] = 1;
    for (int i = 1; i <= n; i++)
    {
        dp[i][0] = (dp[i - 1][0] + dp[i - 1][1] + dp[i - 1][2] + (i >= 2 ? dp[i - 2][0] : 0)) % mod;
        dp[i][1] = (dp[i - 2][0] + dp[i - 1][2]) % mod;
        dp[i][2] = (dp[i - 2][0] + dp[i - 1][1]) % mod;
    }
    cout << dp[n][0] << endl;
    return 0;
}
```

[扫雷 - lanqiao.cn](https://www.lanqiao.cn/problems/2113/learning/?page=1&first_category_id=1&sort=students_count&name=扫雷)

```c++
#include <iostream>
#include <algorithm>
using namespace std;
const int N = 5e5 + 10;
int n, m;
int ans;
struct bomb
{
    int x, y, r;
    bool f;
    bool operator < (const bomb &xx) const
    {
        return x < xx.x;
    }
}a[N];
struct rocket
{
    int x, y, r;
}b[N];
void dfs(int x, int y, int r)
{
    int l1 = 1, r1 = n;
    while (l1 < r1)
    {
        int mid = l1 + r1 + 1 >> 1;
        if (a[mid].x <= x + r) l1 = mid;
        else r1 = mid - 1;
    }
    int l2 = 1, r2 = n;
    while (l2 < r2)
    {
        int mid = l2 + r2 >> 1;
        if (a[mid].x >= x - r) r2 = mid;
        else l2 = mid + 1;
    }
    for (int i = l2; i <= l1; i++)
    {
        if (a[i].f == 0 && (a[i].x - x) * (a[i].x - x) + (a[i].y - y) * (a[i].y - y) <= r * r)
        {
            ans++;
            a[i].f = 1;
            dfs(a[i].x, a[i].y, a[i].r);
        }
    }
}
int main()
{
    cin >> n >> m;
    for (int i = 1; i <= n; i++)
        cin >> a[i].x >> a[i].y >> a[i].r;
    for (int i = 1; i <= m; i++)
        cin >> b[i].x >> b[i].y >> b[i].r;
    sort(a + 1, a + 1 + n);
    for (int i = 1; i <= m && ans <= n; i++)
    {
        dfs(b[i].x, b[i].y, b[i].r);
    }
    cout << ans << endl;
    return 0;
}
```

[李白打酒加强版 - lanqiao.cn](https://www.lanqiao.cn/problems/2114/learning/?page=1&first_category_id=1&sort=students_count&name=李白打酒)

记忆化搜索和剪枝优化

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
const int mod = 1e9 + 7;
int dp[101][101][101];
int n, m;
int dfs(int d, int vn, int vm)
{
    if (vn < 0 || vm < 0 || d < 0) return 0;
    if (d > m) return 0;
    if (vn == 0 && d == 1 && vm == 1) return 1;
    if (dp[d][vn][vm] != -1) return dp[d][vn][vm];
    return dp[d][vn][vm] = (dfs(d * 2, vn - 1, vm) + dfs(d - 1, vn, vm - 1)) % mod;
}
int main()
{
    memset(dp, -1, sizeof dp);
    cin >> n >> m;
    cout << dfs(2, n, m) << endl;
    return 0;
}
```

#### 省赛训练

[1197:共现的数 (csgrandeur.cn)](https://cpc.csgrandeur.cn/csgoj/problemset/problem?pid=1197)

题目大意: 给定两个数, 统计有多少个数能在给定的数字集合中, 与这两个数都成为共现数.

思路: 用 `bitset` 的 `0` 和 `1` 巧妙判断, 分别存储和 `x` , `y` 形成共现的数, 存在 `a1` 和 `a2` 里, 然后进行逻辑与即可, 注意最后答案还要减去 `x` 和 `y` 自身. 借此题要掌握 `bitset` 用法

```c++
#include <bits/stdc++.h>
using namespace std;
bitset<20010> q[55];
bitset<20010> a1, a2;
int main()
{
    int n;
    while (cin >> n)
    {
        for (int i = 1; i <= n; i++) q[i].reset();
        for (int i = 1; i <= n; i++)
        {
            int m; cin >> m;
            while (m--)
            {
                int x; cin >> x; q[i][x] = 1;
            }
        }
        int Q; cin >> Q;
        while (Q--)
        {
            a1.reset(); a2.reset();
            int x, y; cin >> x >> y;
            for (int i = 1; i <= n; i++)
            {
                if (q[i][x]) a1 |= q[i];
                if (q[i][y]) a2 |= q[i];
            }
            a1 &= a2;
            int ans = a1.count();
            if (a1[x]) ans--;
            if (a1[y]) ans--;
            cout << ans << endl;
        }
    }
    return 0;
}
```





#### python

```python
#合并列表
def merge(L1,  L2):
    if len(L1) == 0:
        return L2
    elif len(L2) == 0:
        return L1

    if L1[0] > L2[0]:
        return [L1[0]] + merge(L1[1:len(L1)],  L2)
    else:
        return [L2[0]] + merge(L1,  L2[1:len(L2)])


if __name__ == "__main__":
    X = input("请输入列表X：").split(", ")
    Y = input("请输入列表Y：").split(", ")
    S = merge(X,  Y)
    for i in range(len(S)):
        S[i] = int(S[i])
    print(S)

#汉诺塔
def Hanoi(n,  A,  C,  B):
    global count
    if n < 1:
        print('invalid input')
    elif n == 1:
        count = count + 1
        print("%d:\t%s ---> %s" % (count,  A,  C))
    else:
        Hanoi(n - 1,  A,  B,  C)
        Hanoi(1,  A,  C,  B)
        Hanoi(n - 1,  B,  C,  A)


if __name__ == "__main__":
    print("请输入A柱子上的圆盘个数:")
    n = int(input())
    count = 0
    Hanoi(n,  "A",  "C",  "B")

#斐波那契数列
def fab(n):
    if n == 1 or n == 2:
        return 1
    else:
        return fab(n - 1) + fab(n - 2)


if __name__ == "__main__":
    global result
    n_str = input('请输入需要计算fabonacci数列的第几个元素:')
    n = int(n_str)
    result = fab(n)
    print(result)

#欧几里得算法
def assignment(a, dec):
    x = a; y = dec
    while y:
        temp = x
        r = x % y
        x = y
        y = r
    if x != 1:
        print("{}和{}的最大公约数为{}。".format(a,  dec,  x))
    else:
        print("{}与{}互质。".format(a,  dec))


if __name__ == "__main__":
    M = int(input())
    N = int(input())
    x = assignment(M,  N)

#冒泡排序
def bubbleSort(a):
    for i in range(len(array),  1,  -1):
        for j in range(i - 1):
            if array[j] > array[j + 1]:
                array[j],  array[j + 1] = array[j + 1],  array[j]
        print(array)
    return array


if __name__ == '__main__':
    arraystr = input().split(', ')
    array = [int(i) for i in arraystr]
    print("排序之后的结果为：{}".format(bubbleSort(array)))

# 选择排序
arraystr = input().split(', ')
array = [int(i) for i in arraystr]


def selectsort(array):
    # ********* Begin *********
    for i in range(len(array) - 1):
        min_index = i
        for j in range(i + 1,  len(array)):
            if array[j] < array[min_index]:
                min_index = j
        if min_index != i:
            array[i],  array[min_index] = array[min_index],  array[i]
        print(array)
    # ********* End *********
    return array


print("排序之后的结果为：{}".format(selectsort(array)))

#数值数据表示（一） 基础习题1
from random import *

def dec2bin_Int(dec):
    binum = ''
    x = bin(dec)
    binum = x[2:]
    binum = binum[::-1]
    return binum[::-1]


def dec2bin_Point(dec,  length):
    binum = ''
    x = dec
    while x:
        x *= 2
        binum += ('1' if x >= 1. else '0')
        x -= int(x)
    binum = binum[:length]
    return '0.'+binum


def bin2oh(binum,  oh):
    result = ''
    if oh == 'o':
        x = oct(int(binum,  2))
        result = x[2:]
        return result
    elif oh == 'h':
        x = hex(int(binum,  2))
        result = x[2:]
        result = result.upper()
        return result


if __name__ == '__main__':
    seed(0)
    tests = [randint(1,  n) for n in [10,  20,  50,  100,  200,  500,  1000,  2000,  5000,  10000]]
    bins = []
    for num in tests:
        binum = dec2bin_Int(num)
        print(binum)
        bins.append(binum)

    print('*'*30)

    seed(99)
    decimals = []
    for i in range(10):
        decimals.append(round(random(),  3))
    print(decimals)
    for dec in decimals:
        print(dec2bin_Point(dec,  8))

    print('*' * 30)
    print(tests)
    for binum in bins:
        print(bin2oh(binum,  'o'))
    print('*' * 30)
    for binum in bins:
        print(bin2oh(binum,  'h'))

#基础习题(2)
from random import *

def makechange(num):
    changes = {}
    t = [50,  20,  10,  5,  2,  1,  0.5,  0.2,  0.1,  0.05,  0.02,  0.01]
    numint = int(num)
    numdec = round(num - numint,  2)
    for i,  money in enumerate(t):
        if numint != 0:
            res = numint // money
        else:
            res = numdec // money
        if i < 6 and res != 0:
            changes[t[i]] = numint // money
            numint = numint % money
        elif i > 5 and res != 0:
            changes[t[i]] = int(numdec // money)
            numdec = round(numdec % money,  2)
    return changes


if __name__ == '__main__':
    seed(0)
    for i in range(10):
        num = round(random() * 100,  2)
        print(sorted(makechange(num).items(),  key=lambda item: item[0],  reverse=True))

#置换加密
import math

def encryptMessage(key,  message):
    if key <= 0:
        return message
    else:
        return "".join([message[i::key] for i in range(key)])

def decryptMessage(key,  message):
    numOfColumns = math.ceil(len(message) / key)
    numOfRows = key
    numOfShadeBoxes = (numOfColumns * numOfRows) - len(message)
    plaintext = [''] * numOfColumns

    col = 0
    row = 0
    for symbol in message:
        plaintext[col] += symbol
        col += 1

        if (col == numOfColumns) or (col == numOfColumns-1 and row >= numOfRows - numOfShadeBoxes):
            col = 0
            row += 1
    return ''.join(plaintext)


if __name__ == '__main__':
    messages = ["Behind every successful man there's a lot of unsuccessful years.", 
                'Common sense is not so common.', 
                'There are no secrets to success.It is the result of preparation,  hard work,  and learning from failure.', 
                'All things are difficult before they are easy.']
    for message in messages:
        for key in range(8,  10):
            encrytext = encryptMessage(key,  message)
            print(encrytext)
            print(decryptMessage(key,  encrytext))


#找词
import jieba

def countWords(excludes,  merges):
    txt = open('西游记.txt', 'r', encoding='utf-8').read()
    words = jieba.lcut(txt)
    counts = {}
    # 取出⻓度为⼀的词和符号以及excludes中的词
    for word in words:
        if len(word) == 1 or word in excludes:
            continue
        else:
            counts[word] = counts.get(word, 0) + 1
    # 合并名称相同的⼈名
    for merge in merges:
        for name in merge[1]:
            counts[merge[0]] += counts.get(name, 0)
            del counts[name]
    word_list = list(counts.items())
    word_list.sort(key=lambda x: x[1], reverse=True)
    return word_list

excludes =  {'怎么','两个','那怪','甚么','这个','不曾','不是','三个','出来','只是','真个','有些','闻言','这里','进去','那个','乃是','袈裟','这般',
'铁棒','果然','就是','不要','小妖','如今','弟子','宝贝','妇人','认得','观看','上前','起来','哥哥','行李','一个个','国王','金光','叫做','一座','晓得',
'不好','十分','取经','师徒','他们','一把','听见','兵器','人家','性命','女婿','金星','神仙','扯住','云头','王子','问道','你们','所以','童子','变化',
'看看','怎生','取出','员外','里面','故此','西方','也罢','西天','女儿','公主','妖魔','欢喜','吩咐','一条','本事','不尽','金箍棒','慌得','口里','老儿',
'大仙','果子','看见','驸马','贫僧','人参果','进来','转身','还有','罢了','拜佛','手段','大唐','多少','几个','忍不住','老魔道','高叫','抬头','赶上','洞口',
'降妖','回来','洞里','模样','一场','天地','为证','一般','礼拜','儿子','女子','之下','出去','言语','叩头','走路','东土','叫声','唬得','老者','玉帝','那些',
'方才','有个','不住','神通','地下','不题','空中','还是','一口','只有','下界','哪吒','二郎','放心','清风','老师','造化','天上','报道','仔细','烦恼','明日',
'近前','一则','却是','毕竟','下回分解','四众','知道','坐在','做个','未曾','看时','怪物','老爷','喝道','土地','老魔','厉声','说话','脱身','失迎','人参','帝君',
'老王','宫殿','二怪','三怪','东胜','宝殿','南天门','之物','宝塔','烟霞','抽身','之类','慌忙','长生','筵宴','高山','不怕','真言','一发','茶饭','供养','那洞',
'用手','五色','十个','躬身','外面','去处','好歹','老和尚','古人云','借宿','方可','起身','看处','一张','山头','黄金','四位','走上','好道','等候','怎敢','勾当',
'急急','来时','莫想','简帖','可是','五行','大闹天宫','祥光','二位','浑家','医治','暗笑','舍利子','这话','天师','径转','父王','几时','道人','举起','即便','方丈',
'一阵','无奈','何如','教他','相识','法力','不济','当时','李天王','牌位','香案','蟠桃','保护','毫毛','一杯','禅师','万寿山','猴儿','元子','一家','施主','正在',
'逃生','众怪','大鹏','钻风','毒药','丝绳','无人','万物','五千四百岁','部洲','之意','玉皇','奉旨','大字','身上','处处','听得','头上','说出','二则','不远','山坡',
'望见','紧闭','开门','接待','菩提','一见','明白','暗喜','纵身','万望','般若','报怨','沙门','担子','半空中','门楼','丈夫','闻得','推倒','关门','二哥','剥皮',
'摇身一变','今朝','丈母','伏侍','难禁','还要','神通广大','亏了','息怒','几日','不管','打得','一棍','径回','老妖','凡间','筋斗','无边','只闻','兄长','正说',
'蓬莱','门上','这厮','三年','这场','莫忙','迎着','黑熊','早到','仙丹','一粒','这样','大神','好生','开口','吹口','前后','今番','放下','左手','高老','高才',
'不多时','果树','偷吃','妈妈','安在','梆铃','圆满','老妪','暴纱亭','武艺','蜘蛛精','蓝道','混沌','正当','至此','下降','牛贺洲','青松','石猴','山上','石崖',
'应声','欠身','一行','猿猴','走兽','时节','仙山','凤凰','满心欢喜','这一去','富贵','果是','四时','急忙','天明','打扮','樵夫','念念','君子','他家','汉子',
'假若','彩云','想必','老实','既然','天色','安歇','高老庄','怠慢','那般','之情','我们','那里','两个','怎么','那怪','甚么','这个','不曾','不是','兄弟','原来',
'正是','不得','如何','不敢','今日','天王','大王','如来','道士','一声'}
merges =  [  ('孙悟空',('孙行者','齐天大圣','大圣','孙长老','孙大圣','悟空','行者','老孙')),
        ('猪八戒',('猪悟能','八戒','呆子')),
        ('沙和尚',('沙僧','师弟')),
        ('唐僧',('唐三藏','唐长老','金蝉子','长老'))]
word_list = countWords(excludes,  merges)
for i in range(30):
    word,  count = word_list[i]
    print(i+1,  word,  count) # chr(12288)为中⽂空格·

```

​	

#### 练习

[**Mountain Walking**](http://poj.org/problem?id=2110)

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
int n; 
int p[105][105];
int step[5] = {0, 1, 0, -1, 0};
bool vis[105][105];
int ll, rl;
bool check(int x, int y)
{
    if (x == n && y == n) return true;
    for (int k = 1; k <= 4; k++)
    {
        int xx = x + step[k], yy = y + step[k - 1];
        if (xx >= 1 && xx <= n && yy >= 1 && yy <= n && p[xx][yy] <= rl && p[xx][yy] >= ll && vis[xx][yy] == 0)
        {
            vis[xx][yy] = 1;
            if(check(xx, yy))
            {
                return true;
            }
        }
    }
    return false;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    cin >> n;
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= n; j++)
            cin >> p[i][j];
    int l = abs(p[n][n] - p[1][1]), r = 110;
    int minn = min(p[n][n], p[1][1]), maxn = max(p[n][n], p[1][1]);
    while (l < r)
    {
        int mid = l + r >> 1;
        if (mid < maxn - minn)
        {
            l = mid + 1;
            continue;
        }
        int ret = (maxn - mid >= 0) ? (maxn - mid) : 0;
        for (int k = ret; k <= minn; k++)
        {
            memset(vis, 0, sizeof vis);
            vis[1][1] = 1;
            ll = k, rl = k + mid;
            if (check(1, 1))
            {
                r = mid;
                break;
            }
            if (k == minn) l = mid + 1;
        }
    }
    cout << l << endl;
    return 0;
}
```

