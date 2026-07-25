# Tree and Graph Traversals

## Problem

## Depth-First Search (DFS)

### Tree DFS

> [!NOTE]
> These templates assume a binary tree is stored as an arena: a `SlotMap<TreeKey, TreeNode<T>>` holding every node, where `TreeKey` is an opaque handle (like a checked index) rather than a pointer. 
> ```rust
> use slotmap::{new_key_type, SlotMap};
>
> new_key_type! { struct TreeKey; }
>
> struct BinaryTreeNode<T> {
>     val: T,
>     left: Option<TreeKey>,
>     right: Option<TreeKey>,
> }
> ```

```rust
fn recursive_preorder_dfs(nodes: &SlotMap<TreeKey, BinaryTreeNode<T>>, root: Option<TreeKey>) -> i32 {
    let Some(key) = root else { return <base case result> };
    let node = &nodes[key];

    // Additional base cases

    // ... involving the current node and the current result

    recursive_preorder_dfs(nodes, node.left);
    recursive_preorder_dfs(nodes, node.right);

    <current result and the two recursive calls above>
}
```

```rust
fn iterative_preorder_dfs(nodes: &SlotMap<TreeKey, TreeNode<T>>, root: Option<TreeKey>) -> i32 {
    let Some(root) = root else { return <base case result> };

    let mut stack = vec![root];

    let mut result = <initial value>;

    while let Some(key) = stack.pop() {
        let node = &nodes[key];

        // Additional base cases

        // ... involving the popped node and the result

        if let Some(right) = node.right {
            stack.push(right);
        }
        if let Some(left) = node.left {
            stack.push(left);
        }
    }

    result
}
```

> [!NOTE]
> In the iterative depth-first search, the flow is usually pre-order `pop node → process node → push right → push left` , while in the recursive depth-first search, pre-order `process node → recurse left → recurse right` is the most common, followed by post-order `recurse left → recurse right → process node` , then in-order `recurse left → process node → recurse right` .

> [!NOTE]
> In depth-first search, a **state** is all the data you need to remember at one point in the search. Each state is typically compromised of one or more variables, which we call a **state variable**. In a recursive implementation, the state consist of function arguments stored in a call stack frame, while in an iterative implementation, the state consist of variables stored in tuple that will be pushed and popped from an explicit stack you create outside the while loop.

> [!NOTE]
> In a recursive depth-first search, `result` is typically implicit since it's usually sufficient to implicitly be returned, but an explicit `result` is sometimes a good choice, where you create it within the scope of the provided function, then create and call an inner depth-first search function to perform the actual work. In an iterative depth-first search, you typically create an explicit `result` variable outside the while loop.

### Graph DFS

#### On an Adjacency List Graph

```rust
use std::collections::{HashMap, HashSet};

fn adjacency_list_recursive_dfs(graph: &HashMap<i32, Vec<i32>>) -> i32 {
    fn dfs(vertex: i32, graph: &HashMap<i32, Vec<i32>>, visited: &mut HashSet<i32>) -> i32 {
        visited.insert(vertex);
        let mut result = <initial value>;
        for &neighbour in &graph[&vertex] {
            if !visited.contains(&neighbour) {
                result += dfs(neighbour, graph, visited);
            }
        }
        result
    }

    let mut result = <initial value>;
    let mut visited = HashSet::new();
    for &vertex in graph.keys() {
        if !visited.contains(&vertex) {
            dfs(vertex, graph, &mut visited);

            // Some logic involving the result per connected component
        }
    }

    result
}
```

```rust
fn adjacency_list_iterative_dfs(graph: &HashMap<i32, Vec<i32>>) -> i32 {
    fn dfs(vertex: i32, graph: &HashMap<i32, Vec<i32>>, visited: &mut HashSet<i32>) -> i32 {
        let mut result = <initial value>;
        let mut stack = vec![vertex];
        while let Some(vertex) = stack.pop() {
            visited.insert(vertex);
            for &neighbour in &graph[&vertex] {
                if !visited.contains(&neighbour) {
                    result += <calculation>;
                    stack.push(neighbour);
                }
            }
        }
        result
    }

    let mut result = <initial value>;
    let mut visited = HashSet::new();
    for &vertex in graph.keys() {
        if !visited.contains(&vertex) {
            dfs(vertex, graph, &mut visited);

            // Some logic involving the result per connected component
        }
    }

    result
}
```

#### On a Matrix Graph

```rust
use std::collections::HashSet;

fn matrix_recursive_dfs(matrix: &[Vec<i32>]) -> i32 {
    let rows = matrix.len() as i32;
    let columns = matrix[0].len() as i32;
    // NOTE: each element is of the form (change in row, change in col)
    let directions = [(1, 0), (-1, 0), (0, -1), (0, 1)];

    fn valid_cell(row: i32, col: i32, rows: i32, columns: i32) -> bool {
        0 <= row && row < rows && 0 <= col && col < columns && <another condition for a cell to be valid>
    }

    fn dfs(
        row: i32,
        col: i32,
        visited: &mut HashSet<(i32, i32)>,
        rows: i32,
        columns: i32,
        directions: &[(i32, i32)],
    ) -> i32 {
        visited.insert((row, col));
        let mut result = <initial value>;
        for &(dr, dc) in directions {
            let neighbour_row = row + dr;
            let neighbour_col = col + dc;
            if valid_cell(neighbour_row, neighbour_col, rows, columns)
                && !visited.contains(&(neighbour_row, neighbour_col))
            {
                result += dfs(neighbour_row, neighbour_col, visited, rows, columns, directions);
            }
        }
        result
    }

    let mut visited = HashSet::new();
    let mut result = <initial value>;
    for row in 0..rows {
        for col in 0..columns {
            if !visited.contains(&(row, col)) {
                dfs(row, col, &mut visited, rows, columns, &directions);

                // Some logic involving the result per connected component
            }
        }
    }

    result
}
```

```rust
fn matrix_iterative_dfs(matrix: &[Vec<i32>]) -> i32 {
    let rows = matrix.len() as i32;
    let columns = matrix[0].len() as i32;
    // NOTE: each element is of the form (change in row, change in col)
    let directions = [(1, 0), (-1, 0), (0, -1), (0, 1)];

    fn valid_cell(row: i32, col: i32, rows: i32, columns: i32) -> bool {
        0 <= row && row < rows && 0 <= col && col < columns && <another condition for a cell to be valid>
    }

    fn dfs(row: i32, col: i32, visited: &mut HashSet<(i32, i32)>, rows: i32, columns: i32, directions: &[(i32, i32)]) -> i32 {
        let mut stack = vec![(row, col)];
        let mut result = <initial value>;
        while let Some((row, col)) = stack.pop() {
            visited.insert((row, col));
            for &(dr, dc) in directions {
                let neighbour_row = row + dr;
                let neighbour_col = col + dc;
                if valid_cell(neighbour_row, neighbour_col, rows, columns)
                    && !visited.contains(&(neighbour_row, neighbour_col))
                {
                    result += <some calculation>;
                    stack.push((neighbour_row, neighbour_col));
                }
            }
        }
        result
    }

    let mut visited = HashSet::new();
    let mut result = <initial value>;
    for row in 0..rows {
        for col in 0..columns {
            if !visited.contains(&(row, col)) {
                dfs(row, col, &mut visited, rows, columns, &directions);

                // Some logic involving the result per connected component
            }
        }
    }

    result
}
```

## Breadth-First Search (BFS)

### Tree BFS

```rust
use std::collections::VecDeque;

fn bfs(nodes: &SlotMap<TreeKey, TreeNode<T>>, root: Option<TreeKey>) -> i32 {
    let Some(root) = root else { return 0 };

    let mut queue = VecDeque::from([root]);
    let mut result = 0;

    while !queue.is_empty() {
        let level_width = queue.len();

        // Some logic involving the current level

        for _ in 0..level_width {
            let key = queue.pop_front().unwrap();
            let node = &nodes[key];

            // Some logic involving the current node

            if let Some(left) = node.left {
                queue.push_back(left);
            }
            if let Some(right) = node.right {
                queue.push_back(right);
            }
        }
    }

    result
}
```

### Graph BFS

#### On an Adjacency List Graph

```rust
use std::collections::{HashMap, HashSet, VecDeque};

fn adjacency_list_bfs(graph: &HashMap<i32, Vec<i32>>) -> i32 {
    let mut queue = VecDeque::from([(<source vertex>, <additional state variable>, <initial distance>)]);
    let mut visited = HashSet::from([<source vertex>]);

    while let Some((vertex, <additional state>, dist)) = queue.pop_front() {
        if vertex == <destination vertex> {
            return dist;
        }

        for &neighbour in &graph[&vertex] {
            if !visited.contains(&neighbour) {
                visited.insert(neighbour);
                queue.push_back((neighbour, <additional state variable>, dist + 1));
            }

            // Some logic involving the neighbour
        }
    }

    -1
}
```

#### On a Matrix Graph

```rust
use std::collections::{HashSet, VecDeque};

fn matrix_iterative_bfs(matrix: &[Vec<i32>]) -> i32 {
    let rows = matrix.len() as i32;
    let columns = matrix[0].len() as i32;
    // NOTE: each element is of the form (change in row, change in col)
    let directions = [(0, 1), (1, 0), (1, 1), (-1, -1), (-1, 1), (1, -1), (-1, 0), (0, -1)];

    fn valid_cell(row: i32, col: i32, rows: i32, columns: i32) -> bool {
        0 <= row && row < rows && 0 <= col && col < columns && <another condition for a cell to be valid>
    }

    let mut queue = VecDeque::from([(<source vertex>, <additional state>, <initial distance>)]);
    let mut visited = HashSet::from([(<source vertex>, <initial distance>)]);

    while let Some((row, col, dist)) = queue.pop_front() {
        if (row, col) == (<destination row>, <destination col>) {
            return dist;
        }

        for &(dr, dc) in &directions {
            let neighbour_row = row + dr;
            let neighbour_col = col + dc;
            let neighbour_dist = dist + 1;
            if !visited.contains(&(neighbour_row, neighbour_col)) && valid_cell(neighbour_row, neighbour_col, rows, columns) {
                visited.insert((neighbour_row, neighbour_col));
                queue.push_back((neighbour_row, neighbour_col, <additional state>, neighbour_dist));
            }

            // Some logic involving the neighbour's row and col
        }
    }

    -1
}
```

> [!NOTE]
>  `visited` is typically a HashSet, but you might achieve better runtime performance by using a boolean array when the node range is predetermined (which is typical since graph problems usually number nodes from `0` to `n - 1` )

> [!NOTE]
> When using BFS to find shortest paths:
> - If the you need to find the distance (number of moves/steps), initialize source vertices with `distance = 0`
> - If the you need to find the path length (number of cells in the path), initialize source vertices with `path_length = 1`

> [!NOTE]
> For a multi-source BFS, create a for loop that visits all source nodes and appends them to the queue for the BFS.

## Complexity Analysis

### Tree Algorithms

$$
O(n \cdot C_{node})
$$

- \(n\): number of nodes in the tree
- \(C_{node}\): cost of processing a single node

### Graph Traversal Algorithms

$$
O(S \cdot C_{state} + T \cdot C_{transition})
$$

- \(S\): number of reachable states (product of the ranges of each state variable)
- \(C_{state}\): cost of processing a single state
- \(T\): number of transitions (the transitions per state times S)
- \(C_{transition}\): cost of processing a single transition
