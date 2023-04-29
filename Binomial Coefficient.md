# Binomial Coeffcient
## code
```c
#include<stdio.h>
#include<stdlib.h>

long long binomial(long long n, long long k);


long long main() {
	long long n, k;
	printf("Please enter the quantity of items n: ");
	scanf("%lld", &n);
	printf("Please enter the number of selections k: ");
	scanf("%lld", &k);  
    printf("result=%lld ",binomial(n, k));
}

long long binomial(long long n, long long k)
{
    long long** dp = (long long**)malloc(sizeof(long long*) * n + 1);
    for (long long i = 0; i < n + 1; i++)
        dp[i] = (long long*)malloc(sizeof(long long) * k + 1);
    for (long long i = 0; i <= n; i++) {
        for (long long j = 0; j <= min(i, k); j++) {
            if (j == 0 || j == i) {
                dp[i][j] = 1;
            }
            else {
                dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j];
            }
        }
    }
    return dp[n][k];
}
```

## test
test1:
输入：
```
7 2
```
输出：
```
21
```
test2:
输入：
```
6 3
```
输出：
```
20
```
test3:
输入：
```
8 3
```
输出：
```
56
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcxNTk0NDYwMF19
-->