
# Dijkstra Algorithm
## code
```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

#define MAX_VERTICES 1000
#define MAX_EDGES 10000

struct edge {
    int u, v, w;
};

struct graph {
    int num_vertices, num_edges;
    struct edge edges[MAX_EDGES];
};

void dijkstra(struct graph* g, int source, int dist[]) {
    int visited[MAX_VERTICES] = { 0 };

    for (int i = 0; i < g->num_vertices; i++) {
        dist[i] = INT_MAX;
    }
    dist[source] = 0;

    for (int i = 0; i < g->num_vertices; i++) {
        int min_dist = INT_MAX;
        int min_vertex = -1;

        for (int j = 0; j < g->num_vertices; j++) {
            if (!visited[j] && dist[j] < min_dist) {
                min_dist = dist[j];
                min_vertex = j;
            }
        }

        if (min_vertex == -1) {
            break;
        }

        visited[min_vertex] = 1;

        for (int j = 0; j < g->num_edges; j++) {
            struct edge e = g->edges[j];
            if (e.u == min_vertex) {
                int new_dist = dist[min_vertex] + e.w;
                if (new_dist < dist[e.v]) {
                    dist[e.v] = new_dist;
                }
            }
        }
    }
}

int main() {
    struct graph g;
    int source;
    int dist[MAX_VERTICES];

    printf("Enter the number of vertices: ");
    scanf("%d", &g.num_vertices);

    printf("Enter the number of edges: ");
    scanf("%d", &g.num_edges);

    for (int i = 0; i < g.num_edges; i++) {
        printf("Enter the start, end, and weight of edge %d: ", i + 1);
        scanf("%d %d %d", &g.edges[i].u, &g.edges[i].v, &g.edges[i].w);
    }

    printf("Enter the source vertex: ");
    scanf("%d", &source);

    dijkstra(&g, source, dist);

    for (int i = 0; i < g.num_vertices; i++) {
        printf("Shortest path from %d to %d is %d\n", source, i, dist[i]);
    }

    return 0;
}

```

## test
test1:
输入：
```
Enter the number of vertices: 5
Enter the number of edges: 7
Enter the start, end, and weight of edge 1: 0 1 4
Enter the start, end, and weight of edge 2: 0 2 1
Enter the start, end, and weight of edge 3: 1 3 1
Enter the start, end, and weight of edge 4: 1 4 5
Enter the start, end, and weight of edge 5: 2 1 2
Enter the start, end, and weight of edge 6: 2 3 4
Enter the start, end, and weight of edge 7: 3 4 1
Enter the source vertex: 0
```
输出：
```
Shortest path from 0 to 0 is 0
Shortest path from 0 to 1 is 3
Shortest path from 0 to 2 is 1
Shortest path from 0 to 3 is 4
Shortest path from 0 to 4 is 5
```
test2:
输入：
```
Enter the number of vertices: 4
Enter the number of edges: 4
Enter the start, end, and weight of edge 1: 0 1 1
Enter the start, end, and weight of edge 2: 1 2 2
Enter the start, end, and weight of edge 3: 2 3 3
Enter the start, end, and weight of edge 4: 3 0 -100
Enter the source vertex: 0
```
输出：
```
Shortest path from 0 to 0 is 0
Shortest path from 0 to 1 is 1
Shortest path from 0 to 2 is 3
Shortest path from 0 to 3 is -97
```
test3:
输入：
```
Enter the number of vertices: 4
Enter the number of edges: 5
Enter the start, end, and weight of edge 1: 0 1 1
Enter the start, end, and weight of edge 2: 1 2 2
Enter the start, end, and weight of edge 3: 2 3 3
Enter the start, end, and weight of edge 4: 3 0 4
Enter the start, end, and weight of edge 5: 1 1 1
Enter the source vertex: 0
```
输出：
```
Shortest path from 0 to 0 is 0
Shortest path from 0 to 1 is 1
Shortest path from 0 to 2 is 3
Shortest path from 0 to 3 is 6

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NjQwODAwNDJdfQ==
-->