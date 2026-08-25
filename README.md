# Table of Contents

- [Complexity Analysis](./src/complexity-analysis.md)
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
    - [Recursion](./src/recursion.md)
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

| Operation | Python | C++ |
|---|---|---|
| Integer division | `//` (floors) | `/` (truncates toward zero) |
| Floating-point division | `/` | `/` |
| Remainder | N/A | `%` |
| Modulo | `%` | N/A |

**Division Flooring and Division Ceiling**

| Operation | Python | C++ |
|---|---|---|
| Division flooring an integer | `//` | `div_floor(<num>, <denom>)` (see below) |
| Division ceiling an integer | `-(a // -b)` | `div_ceil(<num>, <denom>)` (see below) |
| Flooring a float | `math.floor(<num> / <denom>)` | `floor(<num> / <denom>)` |
| Ceiling a float | `math.ceil(<num> / <denom>)` | `ceil(<num> / <denom>)` |

```cpp
template <typename T>
T div_ceil(T a, T b) {
    T q = a / b;
    T r = a % b;

    bool remainder_exists = (r != 0);
    bool same_sign = (r < 0) == (b < 0);
    if (remainder_exists && same_sign) {
        q = q + 1;
    }

    return q;
}
```

```cpp
template <typename T>
T div_floor(T a, T b) {
    T q = a / b;
    T r = a % b;

    bool remainder_exists = (r != 0);
    bool different_sign = (r < 0) != (b < 0);
    if (remainder_exists && different_sign) {
        q = q - 1;
    }

    return q;
}
```
