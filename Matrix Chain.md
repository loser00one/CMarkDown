# Matrix Chain
## code
```c
#include <stdio.h>
#include <limits.h>

#define MAX 0x7fffffff
#define N 100

int n;
int p[N];
int s[N][N], dp[N][N]; // S 存储切割位置，dp 存储最优值

void MatricChain()
{
    for (int i = 0; i < n + 1; i++)
    {
        for (int j = 0; j < n + 1; j++)
        {
            dp[i][j] = MAX;
            s[i][j] = 0;
        }
    }

    for (int i = 0; i <= n; i++)
    {
        scanf("%d", &p[i]);
        dp[i][i] = 0; // 只有一个矩阵时不能相乘
    }

    for (int L = 2; L <= n; L++) // 相乘矩阵的个数
    {
        for (int i = 1; i <= n; i++)
        {
            int j = i + L - 1;
            if (j > n)
                break;
            for (int k = i; k < j; k++) // 遍历切割位置
            {
                int min_ = dp[i][j];
                int temp = dp[i][k] + dp[k + 1][j] + p[i - 1] * p[k] * p[j];
                if (temp < min_)
                {
                    dp[i][j] = temp;
                    min_ = temp;
                    s[i][j] = k;
                }
                // dp[i][j] = min(dp[i][j], dp[i][k] + dp[k + 1][j] + p[i - 1] * p[k] * p[j]);
            }
        }
    }
}

void Traceback(int i, int j)
{
    if (i == j)
        return;
    int k = s[i][j];
    Traceback(i, k);
    Traceback(k + 1, j);
    printf("A[%d:%d]*A[%d:%d]\n", i, k, k + 1, j);
}

int main()
{
    scanf("%d", &n);

    MatricChain();

    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
            printf("%10d ", dp[i][j]);
        printf("\n");
    }

    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
            printf("%5d ", s[i][j]);
        printf("\n");
    }

    printf("连乘的最少次数是 %d 次。\n", dp[1][n]);
    Traceback(1, n);
    return 0;
}

```

## test
test1:
输入：
```
6
2 7 5 4 2 3 8
```
输出：
```
         0         70        110        126        138        186
2147483647          0        140        110        152        270
2147483647 2147483647          0         40         70        168
2147483647 2147483647 2147483647          0         24        112
2147483647 2147483647 2147483647 2147483647          0         48
2147483647 2147483647 2147483647 2147483647 2147483647          0
    0     1     2     3     4     5
    0     0     2     2     4     4
    0     0     0     3     4     4
    0     0     0     0     4     4
    0     0     0     0     0     5
    0     0     0     0     0     0
连乘的最少次数是 186 次。
A[1:1]*A[2:2]
A[1:2]*A[3:3]
A[1:3]*A[4:4]
A[1:4]*A[5:5]
A[1:5]*A[6:6]

```
test2:
输入：
```
5
30 35 15 5 10 20
```
输出：
```
         0      15750       7875       9375      11875
2147483647          0       2625       4375       7125
2147483647 2147483647          0        750       2500
2147483647 2147483647 2147483647          0       1000
2147483647 2147483647 2147483647 2147483647          0
    0     1     1     3     3
    0     0     2     3     3
    0     0     0     3     3
    0     0     0     0     4
    0     0     0     0     0
连乘的最少次数是 11875 次。
A[2:2]*A[3:3]
A[1:1]*A[2:3]
A[4:4]*A[5:5]
A[1:3]*A[4:5]
```
test3:
输入：
```
```
输出：
```
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkxMDU5NTM3M119
-->