# MultiplyPrim's MST
## code
```c
#include <stdio.h>
#include <limits.h>

#define V 5

int minKey(int key[], int mstSet[])
{
    int min = INT_MAX, min_index;

    for (int v = 0; v < V; v++)
        if (mstSet[v] == 0 && key[v] < min)
            min = key[v], min_index = v;

    return min_index;
}

void printMST(int parent[], int graph[V][V])
{
    printf("Edge   Weight\n");
    for (int i = 1; i < V; i++)
        printf("%d - %d    %d \n", parent[i], i, graph[i][parent[i]]);
}

void primMST(int graph[V][V])
{
    int parent[V];
    int key[V];
    int mstSet[V];

    for (int i = 0; i < V; i++)
        key[i] = INT_MAX, mstSet[i] = 0;

    key[0] = 0;
    parent[0] = -1;

    for (int count = 0; count < V - 1; count++)
    {
        int u = minKey(key, mstSet);

        mstSet[u] = 1;

        for (int v = 0; v < V; v++)

            if (graph[u][v] && mstSet[v] == 0 && graph[u][v] < key[v])
                parent[v] = u, key[v] = graph[u][v];
    }

    printMST(parent, graph);
}

int main()
{
    int graph[V][V];
    printf("Enter the graph as an adjacency matrix:\n");
    for (int i = 0; i < V; i++)
        for (int j = 0; j < V; j++)
            scanf("%d", &graph[i][j]);
    primMST(graph);
    return 0;
}
```

## test
test1:
输入：
```
0 2 0 6 0
2 0 3 8 5
0 3 0 0 7
6 8 0 0 9
0 5 7 9 0
```
输出：
```
Edge   Weight
0 - 1    2 
1 - 2    3 
0 - 3    6 
1 - 4    5 
```
test2:
输入：
```
0 4 0 0 0 0 8 0
4 0 8 0 0 0 11 0
0 8 0 7 0 4 0 2
0 0 7 0 9 14 0 0
0 0 0 9 0 10 0 0
0 0 4 14 10 0 2 0
8 11 0 0 0 2 0 7
0 0 2 0 0 0 7 0
```
输出：
```
Edge   Weight
0 - 1    0
3 - 2    0
1 - 3    0
3 - 4    2
```
test3:
输入：
```
0 2 0 6 0
2 0 3 0 0
0 3 0 1 0
6 0 1 0 4
0 0 0 4 0
```
输出：
```
Edge   Weight
0 - 1    2 
1 - 2    3 
2 - 3    1 
3 - 4    4 
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMTU5MjYzNTRdfQ==
-->