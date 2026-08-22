# Tree and Graph Traversals

## Complexity Analysis

### Tree Traversals

Let $n$ be the number of nodes in the tree and $C_{node}$ be the cost of processing a single node. Then:

$$
O(n \cdot C_{node})
$$

### Graph Traversals

Let $S$ be the number of reachable states (product of the ranges of each state variable), $C_{state}$ the cost of processing a single state, $T$ the number of transitions (the transitions per state times $S$), and $C_{transition}$ the cost of processing a single transition. Then:

$$
O(S \cdot C_{state} + T \cdot C_{transition})
$$

## Tree Traversals

### Depth-First Search

#### Use Case

Most binary tree problems that don't involve processing nodes by their levels.

#### Template

```python
def recursive_preorder_dfs(root):
    if not root:
        return <base case result>

    # Additional base cases

    # ... involving the current node and the current result

    recursive_preorder_dfs(root.left)
    recursive_preorder_dfs(root.right)

    return <current result and the two recursive calls above>
```

```python
def iterative_preorder_dfs(root):
    if not root:
        return <base case result>

    stack = [root]

    result = <initial value>

    while stack:
        node = stack.pop()

	    # Additional base cases

        # ... involving the popped node and the result

	    if node.right:
            stack.append(node.right)
        if node.left:
            stack.append(node.left)

    return result
```

#### Complexity Analysis

Let $n$ be the number of nodes in the tree. Then, Space Complexity is worst-case $O(n)$.

> [!NOTE]
> The $O(n)$ space comes from the call stack (recursive) or the explicit `stack` (iterative), which in the worst case (a completely skewed tree) holds all $n$ nodes; for a balanced tree, this drops to $O(\log n)$ (the tree's height).

> [!NOTE]
> In the iterative depth-first search, the flow is usually pre-order `pop node → process node → push right → push left` , while in the recursive depth-first search, pre-order `process node → recurse left → recurse right` is the most common, followed by post-order `recurse left → recurse right → process node` , then in-order `recurse left → process node → recurse right` .

> [!NOTE]
> In depth-first search, a **state** is all the data you need to remember at one point in the search. Each state is typically compromised of one or more variables, which we call a **state variable**. In a recursive implementation, the state consist of function arguments stored in a call stack frame, while in an iterative implementation, the state consist of variables stored in tuple that will be pushed and popped from an explicit stack you create outside the while loop.

> [!NOTE]
> In a recursive depth-first search, `result` is typically implicit since it's usually sufficient to implicitly be returned, but an explicit `result` is sometimes a good choice, where you create it within the scope of the provided function, then create and call an inner depth-first search function to perform the actual work. In an iterative depth-first search, you typically create an explicit `result` variable outside the while loop.

> [!NOTE]
> BST problems typically use DFS traversal. Common techniques include:
> - Checking if the current node's value is within bounds (e.g., `low <= node.val <= high`)
> - Leveraging the BST property to prune subtrees: if `node.val < low` , skip the left subtree; if `node.val > high` , skip the right subtree (where `low` or `high` can also just be a target value)
> - Using inorder traversal to collect values in sorted order for problems requiring sorted data without explicit sorting.

### Breadth-First Search

#### Use Case

Binary tree problems that involve processing nodes by their levels.

#### Template

```python
from collections import deque

def bfs(root):
    if not root:
        return

    queue = deque([root])
    result = 0

    while queue:
        level_width = len(queue)

        # Some logic involving the current level

        for _ in range(level_width):
            node = queue.popleft()

            # Some logic involving the current node

            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)

    return result
```

#### Complexity Analysis

Let $n$ be the number of nodes in the tree. Then, Space Complexity is worst-case $O(n)$, for `queue` holding an entire level (up to $n / 2$ nodes for the widest level of a complete binary tree).

## Graph Traversals

### Depth-First Search

#### Use Case

Most graph problems.

#### Templates

```python
def adjacency_list_recursive_dfs(graph):
    def dfs(vertex):
        visited.add(vertex)
        result = <initial value>
        for neighbour in graph[vertex]:
            if neighbour not in visited:
                result += dfs(neighbour)
        return result

    result = <initial value>
    visited = set()
    for vertex in graph:
        if vertex not in visited:
            dfs(vertex)

            # Some logic involving the result per connected component
```

```python
def adjacency_list_iterative_dfs(graph):
    def dfs(vertex):
	    result = <initial value>
        stack = [vertex]
        while stack:
            vertex = stack.pop()
            visited.add(vertex)
            for neighbour in graph[vertex]:
                if neighbour not in visited:
                    result += <calculation>
                    stack.append(neighbour)
		return result

    result = <initial value>
    visited = set()
    for vertex in graph.keys():
        if vertex not in visited:
            dfs(vertex)

            # Some logic involving the result per connected component
```

```python
def matrix_recursive_dfs(matrix):
    ROWS = len(matrix)
    COLUMNS = len(matrix[0])
    # NOTE: each element is of the form (change in row, change in col)
    DIRECTIONS = [(1, 0), (-1, 0), (0, -1), (0, 1)]

    def valid_cell(row, col):
        return 0 <= row < ROWS and 0 <= col < COLUMNS and <another condition for a cell to be valid>

    def dfs(row, col):
        visited.add((row, col))
        result = <initial value>
        for dr, dc in DIRECTIONS:
            neighbour_row = row + dr
            neighbour_col = col + dc
            if valid_cell(neighbour_row, neighbour_col) and (neighbour_row, neighbour_col) not in visited:
                result += dfs(neighbour_row, neighbour_col)
        return result

    visited = set()
    result = <initial value>
    for row in range(ROWS):
        for col in range(COLUMNS):
            if (row, col) not in visited:
                dfs(row, col)

                # Some logic involving the result per connected component

    return result
```

```python
def matrix_iterative_dfs(matrix):
    ROWS = len(matrix)
    COLUMNS = len(matrix[0])
    # NOTE: each element is of the form (change in row, change in col)
    DIRECTIONS = [(1, 0), (-1, 0), (0, -1), (0, 1)]

    def valid_cell(row, col):
        return 0 <= row < ROWS and 0 <= col < COLUMNS and <another condition for a cell to be valid>

    def dfs(row, col):
        stack = [(row, col)]
        result = <initial value>
        while stack:
            row, col = stack.pop()
            visited.add((row, col))
            for dr, dc in DIRECTIONS:
                neighbour_row = row + dr
                neighbour_col = col + dc
                if valid_cell(neighbour_row, neighbour_col) and (neighbour_row, neighbour_col) not in visited:
                    result += <some calculation>
                    stack.append((neighbour_row, neighbour_col))
        return result

    visited = set()
    result = <initial value>
    for row in range(ROWS):
        for col in range(COLUMNS):
            if (row, col) not in visited:
                dfs(row, col)

                # Some logic involving the result per connected component

    return result
```

#### Complexity Analysis

For the adjacency-list templates, let $V$ be the number of vertices and $E$ be the number of edges. For the matrix templates, let $R$ and $C$ be the number of rows and columns. Then:

| Template | Space Complexity |
| --- | --- |
| Adjacency list | worst-case $O(V + E)$ |
| Matrix | worst-case $O(R \cdot C)$ |

> [!NOTE]
> The space bound covers `visited` and the recursion/explicit stack, both of which can hold every vertex/cell in the worst case (e.g., a graph with no cycles to terminate recursion early, or a grid with no invalid cells).

### Breadth-First Search 

#### Use Case

Determine the distance in a graph.

#### Template

```python
from collections import deque

def adjacency_list_bfs(graph):
    queue = deque([(<source vertex>,<additional state variable>, <initial distance>)])
    visited = set([<source vertex>])

    while queue:
        vertex, <additional state>, dist = queue.popleft()

        if vertex == <destination vertex>:
            return dist

        for neighbour in graph[vertex]:
            if neighbour not in visited:
                visited.add(neighbour)
                queue.append((neighbour, <additional state variable>, dist + 1))

            # Some logic involving the neighbour
```

```python
def matrix_iterative_bfs(matrix):
    ROWS = len(matrix)
    COLUMNS = len(matrix[0])
    # NOTE: each element is of the form (change in row, change in col)
    DIRECTIONS = [(0, 1), (1, 0), (1, 1), (-1, -1), (-1, 1), (1, -1), (-1, 0), (0, -1)]

    def valid_cell(row, col):
        return 0 <= row < ROWS and 0 <= col < COLUMNS and <another condition for a cell to be valid>

    queue = deque([(<source vertex>,<additional state>, <initial distance>)])
    visited = set([(<source vertex>, <initial distance>)])

    while queue:
        row, col, dist = queue.popleft()

        if (row, col) == (<destination row>, <destination col>):
            return dist

        for dr, dc in DIRECTIONS:
            neighbour_row = row + dr
            neighbour_col = col + dc
            neighbour_dist = dist + 1
            if (neighbour_row, neighbour_col) not in visited and valid_cell(neighbour_row, neighbour_col):
                visited.add((neighbour_row, neighbour_col))
                queue.append((neighbour_row, neighbour_col, <additional state>, neighbour_dist))

            # Some logic involving the neighbour's row and col
```

#### Complexity Analysis

For the adjacency-list template, let $V$ be the number of vertices and $E$ be the number of edges. For the matrix template, let $R$ and $C$ be the number of rows and columns. Then:

| Template | Space Complexity |
| --- | --- |
| Adjacency list | worst-case $O(V + E)$ |
| Matrix | worst-case $O(R \cdot C)$ |

> [!NOTE]
> Common values of $E$ in the classic graph algorithms worst-case time complexity formulas:
> - Complete graph: $E = \binom{n}{2} = \frac{N(N - 1)}{2}$
> - Tree: $E = V − 1$
> - Dense graph: $E = O(V^2)$
> - Sparse graph: $E =O(V)$

> [!NOTE]
> Unlike linked lists and binary trees, which we are given `head` or `root` respectively, there are various graph inputs:
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

> [!NOTE]
>  `visited` is typically a HashSet, but you might achieve better runtime performance by using a boolean array when the node range is predetermined (which is typical since graph problems usually number nodes from `0` to `n - 1` )

> [!NOTE]
> Whenever the problem mentions prohibited vertices, then that's an indicator to add them straight away to the `visited` container.

> [!NOTE]
> When using BFS to find shortest paths:
> - If the problem asks for distance (number of moves/steps), initialize source vertices with `distance = 0`
> - If the problem asks for path length (number of cells in the path), initialize source vertices with `path_length = 1`

> [!NOTE]
> For a multi-source BFS, create a for loop that visits all source nodes and appends them to the queue for the BFS.

> [!NOTE]
> For graph problems, it's useful to rephrase the problem in terms of its inverse. For instance, take [LeetCode #1557](https://leetcode.com/problems/minimum-number-of-vertices-to-reach-all-nodes/). The original problem description asks us to find the smallest set of vertices from which all nodes in the graph are reachable. Instead, we can rephrase the problem description in terms of its inverse: find the smallest set of nodes that _cannot_ be reached from other nodes, since if a node can be reached from another node, then we would rather just include the pointer rather than the pointee in our set. Another example is [LeetCode #542](https://leetcode.com/problems/01-matrix/description/). The brute force solution would be to perform BFS for each cell with a 1, but instead, we can perform a multi-source BFS by performing starting from all cells with a 0 (if we have a cell `x` with value 1 and its nearest cell y has value 0, then it doesn't make a difference if we traverse from `x -> y` or `y -> x`; both give the same distance).