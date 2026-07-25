# Shortest Path Algorithms

## Problem

Given a weighted graph and a source vertex, find the minimum total edge weight to reach a destination vertex (or every other vertex).

## Dijkstra's Algorithm

### Use Case

Finding the single source shortest path on graphs with non-negative edge weights.

### Template

```cpp
std::vector<long long> dijkstras(const std::vector<std::vector<int>>& edges, int n, int source) {
    std::unordered_map<int, std::vector<std::pair<int, int>>> graph;
    for (const auto& edge : edges) {
        int u = edge[0], v = edge[1], w = edge[2];
        graph[u].push_back({v, w});
    }

    std::vector<long long> distances(n, LLONG_MAX);
    distances[source] = 0;

    std::priority_queue<std::pair<long long, int>,
                        std::vector<std::pair<long long, int>>,
                        std::greater<>> pq;
    pq.push({0, source});

    while (!pq.empty()) {
        auto [distance, node] = pq.top();
        pq.pop();

        if (distance > distances[node]) {
            continue;
        }

        for (const auto& [neighbour, weight] : graph[node]) {
            long long new_distance = distance + weight;
            if (new_distance < distances[neighbour]) {
                distances[neighbour] = new_distance;
                pq.push({new_distance, neighbour});
            }
        }
    }

    return distances;
}
```

### Complexity Analysis

Let \\(V\\) be the number of vertices and \\(E\\) be the number of edges. Then:
- Time Complexity: worst-case \\(O((V + E) \log V)\\)
- Space Complexity: worst-case \\(O(V + E)\\)

> [!NOTE]
> With lazy deletion, the heap can hold up to \\(E\\) entries (one per edge relaxation), so each push/pop costs \\(O(\log E)\\). but since \\(E \le V^2\\), we have \\(\log E \le 2 \log V\\), so this simplifies to \\(O(\log V)\\). The space bound covers the adjacency list \\(O(V + E)\\), the distances array \\(O(V)\\), and the heap \\(O(E)\\).