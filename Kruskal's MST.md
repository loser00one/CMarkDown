# Kruskal's MST
## code
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX_EDGES 1000
#define MAX_VERTICES 1000

struct Edge {
    int u, v, weight;
};

int parent[MAX_VERTICES];
int rank[MAX_VERTICES];
struct Edge edges[MAX_EDGES];

int cmp(const void* a, const void* b) {
    struct Edge* e1 = (struct Edge*)a;
    struct Edge* e2 = (struct Edge*)b;
    return e1->weight - e2->weight;
}

int find(int u) {
    if (parent[u] != u) {
        parent[u] = find(parent[u]);
    }
    return parent[u];
}

void merge(int u, int v) {
    u = find(u);
    v = find(v);
    if (rank[u] > rank[v]) {
        parent[v] = u;
    }
    else if (rank[v] > rank[u]) {
        parent[u] = v;
    }
    else {
        parent[v] = u;
        rank[u]++;
    }
}

int kruskal(int n, int m) {
    int i, count = 0, cost = 0;
    for (i = 1; i <= n; i++) {
        parent[i] = i;
        rank[i] = 0;
    }
    qsort(edges, m, sizeof(struct Edge), cmp);
    for (i = 0; i < m; i++) {
        int u = edges[i].u;
        int v = edges[i].v;
        int weight = edges[i].weight;
        if (find(u) != find(v)) {
            merge(u, v);
            cost += weight;
            count++;
            if (count == n - 1) {
                break;
            }
        }
    }
    return cost;
}

int main() {
    int n, m, i;
    printf("Enter the number of vertices and edges:\n");
    scanf("%d %d", &n, &m);
    printf("Enter the edges and their weights:\n");
    for (i = 0; i < m; i++) {
        scanf("%d %d %d", &edges[i].u, &edges[i].v, &edges[i].weight);
    }
    printf("Minimum cost of spanning tree: %d\n", kruskal(n, m));

    return 0;
}

```

## test
test1:
输入：
```
4 5
1 2 2
1 3 3
1 4 1
2 3 4
3 4 5
```
输出：
```
6
```
test2:
输入：
```
6 10
1 2 6
1 3 1
1 4 5
2 3 5
2 5 3
3 4 5
3 5 6
3 6 4
4 6 2
5 6 6

```
输出：
```
15
```
test3:
输入：
```
3 3
1 2 1
2 3 2
1 3 3
```
输出：
```
3
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzU0MTY0NzU4XX0=
-->