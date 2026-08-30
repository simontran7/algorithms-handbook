# algorithms handbook

## Resources

- [UC Berkeley CS61B Course](https://sp26.datastructur.es/)
- [LeetCode's Interview Crash Course — Data Structures and Algorithms](https://leetcode.com/explore/featured/card/leetcodes-interview-crash-course-data-structures-and-algorithms/)
- Leetcode Explore Cards
    - [arrays 101](https://leetcode.com/explore/learn/card/fun-with-arrays/)
    - [array and string](https://leetcode.com/explore/learn/card/array-and-string/)
    - [sorting](https://leetcode.com/explore/learn/card/sorting/)
    - [linked list](https://leetcode.com/explore/learn/card/linked-list/)
    - [recursion I](https://leetcode.com/explore/learn/card/recursion-i/)
    - [hash table](https://leetcode.com/explore/learn/card/hash-table/)
    - [queue & stack](https://leetcode.com/explore/learn/card/queue-stack/)
    - [heap](https://leetcode.com/explore/learn/card/heap/)
    - [binary search](https://leetcode.com/explore/learn/card/binary-search/)
    - [binary tree](https://leetcode.com/explore/learn/card/data-structure-tree/)
    - [binary search tree](https://leetcode.com/explore/learn/card/introduction-to-data-structure-binary-search-tree/)
    - [n-ary tree](https://leetcode.com/explore/learn/card/n-ary-tree/)
    - [trie](https://leetcode.com/explore/learn/card/trie/)
    - [recursion II](https://leetcode.com/explore/learn/card/recursion-ii/)
    - [graph](https://leetcode.com/explore/learn/card/graph/)
    - [dynamic programming](https://leetcode.com/explore/learn/card/dynamic-programming/)
    - [bit manipulation](https://leetcode.com/explore/learn/card/bit-manipulation/)


## Table of Contents

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

**Division Operations**

| Operation | Python | C++ |
|---|---|---|
| Integer division | `//` (floors) | `/` (truncates toward zero) |
| Floating-point division | `/` | `/` |
| Remainder | N/A | `%` |
| Modulo | `%` | N/A |
| Division flooring an integer | `//` | `div_floor(<num>, <denom>)` (see below) |
| Division ceiling an integer | `-(a // -b)` | `div_ceil(<num>, <denom>)` (see below) |
| Division Flooring a float | `math.floor(<num> / <denom>)` | `floor(<num> / <denom>)` |
| Division Ceiling a float | `math.ceil(<num> / <denom>)` | `ceil(<num> / <denom>)` |

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
