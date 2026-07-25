# Disjoint Set (Union-Find)

## Interface

```rust
trait DisjointSet {
    fn new(n: usize) -> Self;
    fn union(&mut self, x: usize, y: usize) -> bool;
    fn find(&mut self, x: usize) -> usize;
}
```

## Use Case

- Detect and track connected components (static graphs or as edges are added dynamically)
- Detect cycles in undirected graphs
- Enforce grouping constraints (union nodes that must belong together, then validate)

## Forest (with Path Compression & Union by Rank)

A disjoint set is a collection of trees (a forest), one per group, where every node points to its parent, and each tree's root points to itself. Which group an element belongs to is identified by walking up to that tree's root, its **representative**.

### Find

Walk up parent pointers from a node until reaching a node that points to itself (the root/representative). **Path compression** repoints every node visited along the way directly to that root, so future lookups for those nodes are faster.

### Union

Find the representative of each of the two elements. If they're already the same, the elements are already in the same group. Otherwise, merge the two trees by pointing one root at the other. **Union by rank** decides which root to attach to which by tracking each tree's approximate height (its rank), always attaching the shorter tree under the taller one's root. That keeps the forest from growing tall, keeping `find` fast.

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Initialize | worst-case \(O(n)\) |
| Find    | worst-case \(O(\log n)\), but amortized \(O(\alpha(n))\) |
| Union    | worst-case \(O(\log n)\), but amortized \(O(\alpha(n))\) |

> [!NOTE]
> \(\alpha(n)\) is the inverse Ackermann function, which grows so slowly that it's less than \(5\) for any \(n\) that could ever fit in memory. So in practice, both operations are effectively \(O(1)\).
