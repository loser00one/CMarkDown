# Floyd Algorithm
## code
```c
#include <stdio.h>
#include <stdlib.h>

#define INF 1000000000

int main() {
    int n, i, j, k;
    printf("Enter the number of vertices: ");
    scanf("%d", &n);
    int** dist = (int**)malloc(n * sizeof(int*));
    for (i = 0; i < n; i++) {
        dist[i] = (int*)malloc(n * sizeof(int));
    }
    printf("Enter the adjacency matrix:\n");
    for (i = 0; i < n; i++) {
        for (j = 0; j < n; j++) {
            scanf("%d", &dist[i][j]);
            if (dist[i][j] == -1) {
                dist[i][j] = INF;
            }
        }
    }
    for (k = 0; k < n; k++) {
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                if (dist[i][k] + dist[k][j] < dist[i][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }
    printf("Shortest path matrix:\n");
    for (i = 0; i < n; i++) {
        for (j = 0; j < n; j++) {
            if (dist[i][j] == INF) {
                printf("INF ");
            }
            else {
                printf("%d ", dist[i][j]);
            }
        }
        printf("\n");
    }

    for (i = 0; i < n; i++) {
        free(dist[i]);
    }
    free(dist);

    return 0;
}
```

## test

test1
输入：
```
3
0 1 -1
1 0 2
-1 2 0
```
输出:
```
0 1 3
1 0 2
3 2 0
```
test2
输入：
```
5
0 1 2 3 4
1 0 1 2 3
2 1 0 1 2
3 2 1 0 1
-1 -1 -1 -1 0
```
输出：
```
0 1 2 3 4 
1 0 1 2 3 
2 1 0 1 2 
3 2 1 0 1 
INF INF INF INF 0
```

test3
输入:
```
4
0 2 3 1
-1 0 2 3
-1 -1 0 1
-1 -1 -1 0
```
输出：

```
0 2 3 1 
INF 0 2 3 
INF INF 0 1 
INF INF INF 0
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDMwNDUyMDcyXX0=
-->