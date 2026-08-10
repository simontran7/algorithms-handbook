# Minimum Spanning Tree

## Problem

Given a connected, undirected, weighted graph, find a subset of edges that connects all vertices with no cycles and minimum total edge weight.

## Use Case

Determine the minimum/maximum cost to connect all vertices given weighted edges and no required path.

## Kruskal's Algorithm

### Template

```cpp
int kruskal(int n, std::vector<std::vector<int>>& edges) {
    DisjointSet ds(n);
    int mst_cost = 0;
    int edges_used = 0;

    // edges as {weight, u, v} so sorting orders by weight
    std::sort(edges.begin(), edges.end());

    for (const auto& edge : edges) {
        int weight = edge[0], u = edge[1], v = edge[2];
        if (ds.unite(u, v)) {
            mst_cost += weight;
            edges_used++;
            if (edges_used == n - 1) {
                break;
            }
        }
    }

    return mst_cost;
}
```

### Complexity Analysis

Let \\(V\\) be number of vertices, and \\(E\\) be the number of edges. Then:
- Time Complexity: worst-case \\(O(E \log E) + O(E \alpha(V)) = O(E \log E)\\)
- Space Complexity: worst-case \\(O(V)\\)

## Prim's Algorithm

### Template

```cpp
int prim(int n, const std::vector<std::vector<std::pair<int, int>>>& graph) {
    std::vector<bool> visited(n, false);
    int visited_count = 0;

    std::priority_queue<std::pair<int, int>,
                        std::vector<std::pair<int, int>>,
                        std::greater<>> pq;  // {weight, vertex}
    pq.push({0, 0});

    int mst_cost = 0;

    while (!pq.empty() && visited_count < n) {
        auto [weight, vertex] = pq.top();
        pq.pop();
        if (visited[vertex]) {
            continue;
        }
        mst_cost += weight;
        visited[vertex] = true;
        visited_count++;
        for (const auto& [neighbour_weight, neighbour] : graph[vertex]) {
            if (!visited[neighbour]) {
                pq.push({neighbour_weight, neighbour});
            }
        }
    }

    return mst_cost;
}
```

### Complexity Analysis

Let \\(V\\) be number of vertices, and \\(E\\) be the number of edges. Then:
- Time Complexity: worst-case \\(O(V + E) \cdot O(\log V) = O(E \log V)\\)
- Space Complexity: worst-case \\(O(V + E)\\)