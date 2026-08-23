# Graph

## Terminology

## Interface

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
