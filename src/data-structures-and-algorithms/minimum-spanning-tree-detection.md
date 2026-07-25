# Minimum Spanning Tree Algorithms

## Signal

Determine the minimum/maximum cost to connect all vertices given weighted edges and no required path.

## Template

### Kruskal's Algorithm

```rust
fn kruskal(n: usize, mut edges: Vec<(i32, usize, usize)>) -> i32 {
    let mut ds = DisjointSet::new(n);
    let mut mst_cost = 0;
    let mut edges_used = 0;

    edges.sort();

    for (weight, u, v) in edges {
        if ds.union(u, v) {
            mst_cost += weight;
            edges_used += 1;
            if edges_used == n - 1 {
                break;
            }
        }
    }

    mst_cost
}
```

### Prim's Algorithm

```rust
use std::cmp::Reverse;
use std::collections::{BinaryHeap, HashSet};

fn prim(n: usize, graph: &[Vec<(i32, usize)>]) -> i32 {
    let mut visited = HashSet::new();
    let mut pq = BinaryHeap::new();
    pq.push(Reverse((0, 0))); // (weight, vertex)
    let mut mst_cost = 0;

    while let Some(Reverse((weight, vertex))) = pq.pop() {
        if visited.len() >= n {
            break;
        }
        if visited.contains(&vertex) {
            continue;
        }
        mst_cost += weight;
        visited.insert(vertex);
        for &(neighbour_weight, neighbour) in &graph[vertex] {
            if !visited.contains(&neighbour) {
                pq.push(Reverse((neighbour_weight, neighbour)));
            }
        }
    }

    mst_cost
}
```

## Complexity Analysis

### Kruskal's Algorithm

$$
O(E \log E) + O(E \alpha(V)) = O(E \log E)
$$

- \(V\): number of vertices
- \(E\): number of edges

### Prim's Algorithm

$$
O(V + E) \cdot O(\log V) = O(E \cdot \log V)
$$

- \(V\): number of vertices
- \(E\): number of edges

> [!NOTE]
> Common values of \(E\) in the classic graph algorithms worst-case time complexity formulas:
> - Complete graph: \(E = \binom{n}{2} = \frac{N(N - 1)}{2}\)
> - Tree: \(E = V − 1\)
> - Dense graph: \(E = O(V^2)\)
> - Sparse graph: \(E =O(V)\)
