# Topological Sorting

## Use Case

Problems involving prerequisites.

## Kahn's Algorithm

### Complexity Analysis

- Time Complexity: \(O(V + E)\)
- Space Complexity: 

### Template

```rust
use std::collections::{HashMap, VecDeque};

fn kahns_algorithm(n: usize, edges: &[(usize, usize)]) -> Vec<usize> {
    let mut indegrees = vec![0; n];
    let mut graph: HashMap<usize, Vec<usize>> = HashMap::new();
    for &(u, v) in edges {
        graph.entry(u).or_default().push(v);
        indegrees[v] += 1;
    }

    let mut queue: VecDeque<usize> = (0..n).filter(|&v| indegrees[v] == 0).collect();
    let mut result = Vec::new();

    while let Some(vertex) = queue.pop_front() {
        result.push(vertex);
        for &neighbour in graph.get(&vertex).unwrap_or(&Vec::new()) {
            indegrees[neighbour] -= 1;
            if indegrees[neighbour] == 0 {
                queue.push_back(neighbour);
            }
        }
    }

    if result.len() == n { result } else { Vec::new() } // if result.len() != n, there's a cycle
}
```

## DFS-Based Algorithm 

```rust
use std::collections::HashMap;

fn dfs_topological_sort(n: usize, edges: &[(usize, usize)]) -> Vec<usize> {
    let mut graph: HashMap<usize, Vec<usize>> = HashMap::new();
    for &(u, v) in edges {
        graph.entry(u).or_default().push(v);
    }

    const UNVISITED: u8 = 0;
    const IN_PROGRESS: u8 = 1;
    const VISITED: u8 = 2;

    let mut state = vec![UNVISITED; n];
    let mut result = Vec::new();
    let mut has_cycle = false;

    fn dfs(
        vertex: usize,
        graph: &HashMap<usize, Vec<usize>>,
        state: &mut [u8],
        result: &mut Vec<usize>,
        has_cycle: &mut bool,
    ) {
        state[vertex] = IN_PROGRESS;
        for &neighbour in graph.get(&vertex).unwrap_or(&Vec::new()) {
            if state[neighbour] == IN_PROGRESS {
                *has_cycle = true;
                return;
            }
            if state[neighbour] == UNVISITED {
                dfs(neighbour, graph, state, result, has_cycle);
                if *has_cycle {
                    return;
                }
            }
        }
        state[vertex] = VISITED;
        result.push(vertex);
    }

    for vertex in 0..n {
        if state[vertex] == UNVISITED {
            dfs(vertex, &graph, &mut state, &mut result, &mut has_cycle);
            if has_cycle {
                return Vec::new();
            }
        }
    }

    result.reverse();
    result
}
```

