# Table of Contents

- [Complexity Analysis](./src/complexity-analysis.md)
- [Recursion](./src/recursion.md)
- Data Structures
    - [List](./src/list.md)
    - [Stack](./src/stack.md)
    - [Queue](./src/queue.md)
    - [Deque](./src/deque.md)
    - [Priority Queue](./src/priority-queue.md)
    - [Ordered Map and Ordered Set](./src/ordered-map-and-ordered-set.md)
    - [Map and Set](./src/map-and-set.md)
    - [Disjoint Set](./src/disjoint-set.md)
    - [Graph](./src/graph.md)

- Algorithms
    - [Sorting](./src/sorting.md)
    - [Searching](./src/searching.md)
    - [Tree & Graph Traversals](./src/tree-and-graph-traversals.md)
    - [Topological Ordering](./src/topological-ordering.md)
    - [Minimum Spanning Tree](./src/minimum-spanning-tree.md)
    - [Shortest Path](./src/shortest-path.md)
    - [Selection](./src/selection.md)

- Algorithmic Paradigms
    - [Backtracking](./src/backtracking.md)
    - [Divide and Conquer](./src/divide-and-conquer.md)
    - [Dynamic Programming](./src/dynamic-programming.md)
    - [Greedy Algorithms](./src/greedy-algorithms.md)
    - [Sweep Line](./src/sweep-line.md)

- Algorithmic Techniques
    - [Two Pointers](./src/two-pointers.md)
    - [Sliding Window](./src/sliding-window.md)
    - [In Place Reversal](./src/in-place-reversal.md)
    - [Fast and Slow Pointers](./src/fast-and-slow-pointers.md)
    - [Prefix Sum](./src/prefix-sum.md)
    - [Prefix State](./src/prefix-state.md)
    - [Merge Intervals](./src/merge-intervals.md)
    - [Monotonic Stack](./src/monotonic-stack.md)
    - [Monotonic Deque](./src/monotonic-deque.md)
    - [Bit Manipulation](./src/bit-manipulation.md)
    - [Modular Arithmetic](./src/modular-arithmetic.md)

**Division and Modulo**

| Operation | Python | C |
|---|---|---|
| Integer division | `//` (floors) | `/` (truncates toward zero) |
| Floating-point division | `/` | `/` |
| Remainder | N/A | `%` |
| Modulo | `%` | N/A |

**Division Flooring and Division Ceiling**

| Operation | Python | C |
|---|---|---|
| Division flooring an integer | `//` | `div_floor()` (custom, no builtin) |
| Division ceiling an integer | `-(a // -b)` | `div_ceil()` (custom, no builtin) |
| Flooring a float | `math.floor(/)` | `floor()` |
| Ceiling a float | `math.ceil(/)` | `ceil()` |

```c
long div_floor(long a, long b) {
    long q = a / b;
    if ((a % b != 0) && ((a < 0) != (b < 0))) q--;
    return q;
}

long div_ceil(long a, long b) {
    long q = a / b;
    if ((a % b != 0) && ((a < 0) == (b < 0))) q++;
    return q;
}
```
