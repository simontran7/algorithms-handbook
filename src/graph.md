# Graph

> [!NOTE]
> In leetcode, unlike linked lists and binary trees, which we are given `head` or `root` respectively, there are various graph inputs:
> 1. Matrix: A 2D list, where each element will represent a vertex, but are _not_ numbered `0` to `n`, its neighbours are the adjacent squares, and the edges are determined by the problem description.
> 2. Edge list: A list of edges `edges`. It's useful to turn it into an adjacency list.
>
> ```python
> from collections import defaultdict
>
> def build_adjacency_list_graph(edges):
>    graph = defaultdict(list)
>    for u, v in edges:
>        graph[u].append(v)
>        graph[v].append(u) # comment out this line if the input is a directed graph
>
>    return graph
> ```
>
> 3. Integer Adjacency List: A 2D list of integers `graph`, where `n` nodes are numbered from `0` to `n - 1`, and `graph[i]` represents the neighbours of node `i`.
> 4. Integer Adjacency Matrix: A 2D list of integers, where `n` nodes are numbered from `0` to `n - 1`, thereby forming an `n x n` square matrix, and where when `graph[i][j] == 1`, there exist an edge between node `i` and node `j`, and when `graph[i][j] == 0`, there is no edge between node `i` and node `j`. It's also useful to pre-process it into an adjacency list.
>
> ```python
> from collections import defaultdict
>
> def build_adjacency_list_graph(adjacency_matrix):
>     graph = defaultdict(list)
>     n = len(adjacency_matrix)
>
>     for i in range(n):
>         for j in range(i + 1, n):
>             if adjacency_matrix[i][j]:
>                 graph[i].append(j)
>                 graph[j].append(i) # comment out this line if the input is a directed graph
>
>    return graph
> ```
> Although, even if the input is none of the above, it may still be an implicit graph problem, often where vertices aren't explicitly given, but can be generated on the fly through valid transitions or transformations. These problems typically involve:
> - A starting state and a goal/end state
> - A defined set of valid transitions or mutations
> - Optional constraints like invalid/intermediate states
