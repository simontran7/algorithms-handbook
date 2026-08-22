# Shortest Path Algorithms

## Problem

Given a weighted graph and a source vertex, find the minimum total edge weight to reach a destination vertex (or every other vertex).

## Dijkstra's Algorithm

### Use Case

Finding the single source shortest path on graphs with non-negative edge weights.

### Template

```python
import heapq
from collections import defaultdict

def dijkstras(edges, n, source):
    graph = defaultdict(list)
    for u, v, w in edges:
        graph[u].append((v, w))

    distances = [float("inf")] * n
    distances[source] = 0

    pq = [(0, source)]

    while pq:
        distance, node = heapq.heappop(pq)

        if distance > distances[node]:
            continue

        for neighbour, weight in graph[node]:
            new_distance = distance + weight
            if new_distance < distances[neighbour]:
                distances[neighbour] = new_distance
                heapq.heappush(pq, (new_distance, neighbour))

    return distances
```

### Complexity Analysis

Let $V$ be the number of vertices and $E$ be the number of edges. Then:
- Time Complexity: worst-case $O((V + E) \log V)$
- Space Complexity: worst-case $O(V + E)$
