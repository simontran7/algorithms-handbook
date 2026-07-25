# Shortest Path Algorithms

## Dijkstra's Algorithm

### Signal

Finding the single source shortest path on graphs with non-negative edge weights.

### Template

```rust
use std::cmp::Reverse;
use std::collections::{BinaryHeap, HashMap};

fn dijkstras(edges: &[(usize, usize, i64)], source: usize, n: usize) -> Vec<i64> {
    let mut graph: HashMap<usize, Vec<(usize, i64)>> = HashMap::new();
    for &(u, v, w) in edges {
        graph.entry(u).or_default().push((v, w));
    }

    let mut distances = vec![i64::MAX; n];
    distances[source] = 0;

    let mut pq = BinaryHeap::new();
    pq.push(Reverse((0, source)));

    while let Some(Reverse((distance, node))) = pq.pop() {
        if distance > distances[node] {
            continue;
        }

        for &(neighbour, weight) in graph.get(&node).unwrap_or(&Vec::new()) {
            let new_distance = distance + weight;
            if new_distance < distances[neighbour] {
                distances[neighbour] = new_distance;
                pq.push(Reverse((new_distance, neighbour)));
            }
        }
    }

    distances
}
```

## Bellman-Ford Algorithm (TO LEARN)

## Floyd-Warshall Algorithm (TO LEARN)

