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

23/1/7

22/1/14

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



