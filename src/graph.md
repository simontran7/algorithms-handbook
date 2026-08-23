# Graph

## Terminology

## Interface

```
```

## Facts

- Complete graph has \binom{V}{2} = \frac{V(V-1)}{2} edges
- A tree has $V-1$ edges
- A dense graph has $O(V^2)$ edges, while a sparse graph has $E = O(V)$ edges

## Adjacency List

```python
from collections import defaultdict

def from(edges):
    graph = defaultdict(list)
    for u, v in edges:
        graph[u].append(v)
        graph[v].append(u) # comment out this line if the input is a directed graph

    return graph
```

```python
from collections import defaultdict

def from(adjacency_matrix):
    graph = defaultdict(list)
    n = len(adjacency_matrix)

    for i in range(n):
        for j in range(i + 1, n):
            if adjacency_matrix[i][j]:
                graph[i].append(j)
                graph[j].append(i) # comment out this line if the input is a directed graph

    return graph
```

## Adjacency Matrix
