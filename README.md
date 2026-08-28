# algorithms handbook

## Exercises

### Binary Tree

- [144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/description/)
- [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)
- [145. Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/description/)
- [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)
- [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)
- [101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/description/)
- [112. Path Sum](https://leetcode.com/problems/path-sum/description/)
- [250. Count Univalue Subtrees](https://leetcode.com/problems/count-univalue-subtrees/description/)
- [106. Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/)
- [105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)
- [116. Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/description/)
- [117. Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/description/)
- [236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/)
- [297. Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/)

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
