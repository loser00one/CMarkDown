
# Fibonacci Numbers
## code
```c
#include <stdio.h>

int main() {
    int n, i, fib1 = 0, fib2 = 1, fib3;

    printf("Enter the number of terms for Fibonacci series: ");
    scanf("%d", &n);

    printf("The Fibonacci series of first %d terms is:\n", n);
    printf("%d ", fib1);
    for (i = 1; i < n; i++) {
        printf("%d ", fib2);
        fib3 = fib1 + fib2;
        fib1 = fib2;
        fib2 = fib3;
    }

    return 0;
}

```

## test
test1:
输入：
```
5
```
输出：
```
0 1 1 2 3
```
test2:
输入：
```
8
```
输出：
```
0 1 1 2 3 5 8 13
```
test3:
输入：
```
0
```
输出：
```
0
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMwNTY4MTE4Nl19
-->