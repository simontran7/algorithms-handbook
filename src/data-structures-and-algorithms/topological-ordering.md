# Topological Ordering

## Problem

Given a directed acyclic graph, produce a linear ordering of its vertices such that for every edge \\((u, v)\\), \\(u\\) appears before \\(v\\).

## Use Case

Problems involving prerequisites.

## Template

```cpp
std::vector<int> kahns_algorithm(int n, const std::vector<std::vector<int>>& edges) {
    std::vector<int> indegrees(n, 0);
    std::unordered_map<int, std::vector<int>> graph;
    for (const auto& edge : edges) {
        int u = edge[0], v = edge[1];
        graph[u].push_back(v);
        indegrees[v]++;
    }

    std::queue<int> queue;
    for (int vertex = 0; vertex < n; ++vertex) {
        if (indegrees[vertex] == 0) {
            queue.push(vertex);
        }
    }

    std::vector<int> result;

    while (!queue.empty()) {
        int vertex = queue.front();
        queue.pop();
        result.push_back(vertex);
        for (int neighbour : graph[vertex]) {
            indegrees[neighbour]--;
            if (indegrees[neighbour] == 0) {
                queue.push(neighbour);
            }
        }
    }

    // if result.size() != n, there's a cycle
    return result.size() == n ? result : std::vector<int>{};
}
```

## Complexity Analysis

Let \\(V\\) be the number of vertices and \\(E\\) be the number of edges. Then:
- Time Complexity: worst-case \\(O(V + E)\\)
- Space Complexity: worst-case \\(O(V + E)\\)
