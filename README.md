# algorithms handbook

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

## exercises

### Arrays and Strings

- [x] [485. Max Consecutive Ones](https://leetcode.com/problems/max-consecutive-ones/description/)
- [ ] [1295. Find Numbers with Even Number of Digits](https://leetcode.com/problems/find-numbers-with-even-number-of-digits/description/)
- [ ] [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/description/)
- [ ] [1089. Duplicate Zeros](https://leetcode.com/problems/duplicate-zeros/description/)
- [ ] [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/description/)
- [ ] [27. Remove Element](https://leetcode.com/problems/remove-element/description/)
- [ ] [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)
- [ ] [1346. Check If N and Its Double Exist](https://leetcode.com/problems/check-if-n-and-its-double-exist/description/)
- [ ] [941. Valid Mountain Array](https://leetcode.com/problems/valid-mountain-array/description/)
- [ ] [1299. Replace Elements with Greatest Element on Right Side](https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/description/)
- [ ] [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)
- [ ] [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/description/)
- [ ] [905. Sort Array By Parity](https://leetcode.com/problems/sort-array-by-parity/description/)


- [ ] [27. Remove Element](https://leetcode.com/problems/remove-element/description/)
- [ ] [1051. Height Checker](https://leetcode.com/problems/height-checker/description/)
- [ ] [487. Max Consecutive Ones II](https://leetcode.com/problems/max-consecutive-ones-ii/description/)
- [ ] [414. Third Maximum Number](https://leetcode.com/problems/third-maximum-number/description/)
- [ ] [448. Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/description/)
- [ ] [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/description/)
- [ ] [724. Find Pivot Index](https://leetcode.com/problems/find-pivot-index/description/)
- [ ] [747. Largest Number At Least Twice of Others](https://leetcode.com/problems/largest-number-at-least-twice-of-others/description/)
- [ ] [66. Plus One](https://leetcode.com/problems/plus-one/description/)
- [ ] [498. Diagonal Traverse](https://leetcode.com/problems/diagonal-traverse/description/)
- [ ] [54. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/description/)
- [ ] [118. Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/description/)
- [ ] [67. Add Binary](https://leetcode.com/problems/add-binary/description/)
- [ ] [28. Implement strStr()](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/description/)
- [ ] [14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/description/)
- [ ] [344. Reverse String](https://leetcode.com/problems/reverse-string/description/)
- [ ] [167. Two Sum II - [ ] Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)
- [ ] [27. Remove Element](https://leetcode.com/problems/remove-element/description/)
- [ ] [485. Max Consecutive Ones](https://leetcode.com/problems/max-consecutive-ones/description/)
- [ ] [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/description/)
- [ ] [189. Rotate Array](https://leetcode.com/problems/rotate-array/description/)
- [ ] [119. Pascal's Triangle II](https://leetcode.com/problems/pascals-triangle-ii/description/)
- [ ] [151. Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/description/)
- [ ] [557. Reverse Words in a String III](https://leetcode.com/problems/reverse-words-in-a-string-iii/description/)
- [ ] [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)
- [ ] [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/description/)

### Sorting

- [ ] [75. Sort Colors](https://leetcode.com/problems/sort-colors/description/)
- [ ] [1051. Height Checker](https://leetcode.com/problems/height-checker/description/)
- [ ] [147. Insertion Sort List](https://leetcode.com/problems/insertion-sort-list/description/)
- [ ] [912. Sort an Array](https://leetcode.com/problems/sort-an-array/description/)
- [ ] [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)
- [ ] [75. Sort Colors](https://leetcode.com/problems/sort-colors/description/)
- [ ] [1200. Minimum Absolute Difference](https://leetcode.com/problems/minimum-absolute-difference/description/)
- [ ] [1998. Query Kth Smallest Trimmed Number](https://leetcode.com/problems/query-kth-smallest-trimmed-number/description/)
- [ ] [164. Maximum Gap](https://leetcode.com/problems/maximum-gap/description/)
- [ ] [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/description/)

### Queue and Stack

- [ ] [622. Design Circular Queue](https://leetcode.com/problems/design-circular-queue/description/)
- [ ] [346. Moving Average from Data Stream](https://leetcode.com/problems/moving-average-from-data-stream/description/)
- [ ] [286. Walls and Gates](https://leetcode.com/problems/walls-and-gates/description/)
- [ ] [200. Number of Islands](https://leetcode.com/problems/number-of-islands/description/)
- [ ] [752. Open the Lock](https://leetcode.com/problems/open-the-lock/description/)
- [ ] [279. Perfect Squares](https://leetcode.com/problems/perfect-squares/description/)
- [ ] [155. Min Stack](https://leetcode.com/problems/min-stack/description/)
- [ ] [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/description/)
- [ ] [739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/description/)
- [ ] [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/description/)
- [ ] [200. Number of Islands](https://leetcode.com/problems/number-of-islands/description/)
- [ ] [133. Clone Graph](https://leetcode.com/problems/clone-graph/description/)
- [ ] [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)
- [ ] [232. Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/description/)
- [ ] [225. Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/description/)
- [ ] [394. Decode String](https://leetcode.com/problems/decode-string/description/)
- [ ] [733. Flood Fill](https://leetcode.com/problems/flood-fill/description/)
- [ ] [542. 01 Matrix](https://leetcode.com/problems/01-matrix/description/)
- [ ] [841. Keys and Rooms](https://leetcode.com/problems/keys-and-rooms/description/)

### Hash Table

- [ ] [705. Design HashSet](https://leetcode.com/problems/design-hashset/description/)
- [ ] [706. Design HashMap](https://leetcode.com/problems/design-hashmap/description/)
- [ ] [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/description/)
- [ ] [136. Single Number](https://leetcode.com/problems/single-number/description/)
- [ ] [349. Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/description/)
- [ ] [202. Happy Number](https://leetcode.com/problems/happy-number/description/)
- [ ] [1. Two Sum](https://leetcode.com/problems/two-sum/description/)
- [ ] [205. Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings/description/)
- [ ] [599. Minimum Index Sum of Two Lists](https://leetcode.com/problems/minimum-index-sum-of-two-lists/description/)
- [ ] [387. First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/description/)
- [ ] [350. Intersection of Two Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii/description/)
- [ ] [219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii/description/)
- [ ] [359. Logger Rate Limiter](https://leetcode.com/problems/logger-rate-limiter/description/)
- [ ] [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/description/)
- [ ] [249. Group Shifted Strings](https://leetcode.com/problems/group-shifted-strings/description/)
- [ ] [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku/description/)
- [ ] [652. Find Duplicate Subtrees](https://leetcode.com/problems/find-duplicate-subtrees/description/)
- [ ] [771. Jewels and Stones](https://leetcode.com/problems/jewels-and-stones/description/)
- [ ] [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)
- [ ] [170. Two Sum III - [ ] Data structure design](https://leetcode.com/problems/two-sum-iii-data-structure-design/description/)
- [ ] [454. 4Sum II](https://leetcode.com/problems/4sum-ii/description/)
- [ ] [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/description/)
- [ ] [288. Unique Word Abbreviation](https://leetcode.com/problems/unique-word-abbreviation/description/)
- [ ] [380. Insert Delete GetRandom O(1)](https://leetcode.com/problems/insert-delete-getrandom-o1/description/)

### Linked List

- [ ] [707. Design Linked List](https://leetcode.com/problems/design-linked-list/description/)
- [ ] [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/description/)
- [ ] [142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/description/)
- [ ] [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/description/)
- [ ] [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)
- [ ] [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/description/)
- [ ] [203. Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/description/)
- [ ] [328. Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/description/)
- [ ] [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/description/)
- [ ] [707. Design Linked List](https://leetcode.com/problems/design-linked-list/description/)
- [ ] [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/description/)
- [ ] [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/description/)
- [ ] [430. Flatten a Multilevel Doubly Linked List](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/description/)
- [ ] [708. Insert into a Cyclic Sorted List](https://leetcode.com/problems/insert-into-a-sorted-circular-linked-list/description/)
- [ ] [138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/description/)
- [ ] [61. Rotate List](https://leetcode.com/problems/rotate-list/description/)

### Recursion I

- [ ] [344. Reverse String](https://leetcode.com/problems/reverse-string/description/)
- [ ] [24. Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/description/)
- [ ] [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/description/)
- [ ] [700. Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/description/)
- [ ] [119. Pascal's Triangle II](https://leetcode.com/problems/pascals-triangle-ii/description/)
- [ ] [509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/description/)
- [ ] [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/description/)
- [ ] [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)
- [ ] [50. Pow(x, n)](https://leetcode.com/problems/powx-n/description/)
- [ ] [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/description/)
- [ ] [779. K-th Symbol in Grammar](https://leetcode.com/problems/k-th-symbol-in-grammar/description/)
- [ ] [95. Unique Binary Search Trees II](https://leetcode.com/problems/unique-binary-search-trees-ii/description/)

### Recursion II

- [ ] [912. Sort an Array](https://leetcode.com/problems/sort-an-array/description/)
- [ ] [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/description/)
- [ ] [240. Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/description/)
- [ ] [52. N-Queens II](https://leetcode.com/problems/n-queens-ii/description/)
- [ ] [489. Robot Room Cleaner](https://leetcode.com/problems/robot-room-cleaner/description/)
- [ ] [37. Sudoku Solver](https://leetcode.com/problems/sudoku-solver/description/)
- [ ] [77. Combinations](https://leetcode.com/problems/combinations/description/)
- [ ] [100. Same Tree](https://leetcode.com/problems/same-tree/description/)
- [ ] [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/description/)
- [ ] [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)
- [ ] [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)
- [ ] [426. Convert Binary Search Tree to Sorted Doubly Linked List](https://leetcode.com/problems/convert-binary-search-tree-to-sorted-doubly-linked-list/description/)
- [ ] [84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/description/)
- [ ] [46. Permutations](https://leetcode.com/problems/permutations/description/)
- [ ] [17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)
- [ ] [218. The Skyline Problem](https://leetcode.com/problems/the-skyline-problem/description/)

### Binary Search

- [ ] [704. Binary Search](https://leetcode.com/problems/binary-search/description/)
- [ ] [69. Sqrt(x)](https://leetcode.com/problems/sqrtx/description/)
- [ ] [374. Guess Number Higher or Lower](https://leetcode.com/problems/guess-number-higher-or-lower/description/)
- [ ] [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)
- [ ] [278. First Bad Version](https://leetcode.com/problems/first-bad-version/description/)
- [ ] [162. Find Peak Element](https://leetcode.com/problems/find-peak-element/description/)
- [ ] [153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)
- [ ] [34. Search for a Range](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)
- [ ] [658. Find K Closest Elements](https://leetcode.com/problems/find-k-closest-elements/description/)
- [ ] [162. Find Peak Element](https://leetcode.com/problems/find-peak-element/description/)
- [ ] [270. Closest Binary Search Tree Value](https://leetcode.com/problems/closest-binary-search-tree-value/description/)
- [ ] [702. Search in a Sorted Array of Unknown Size](https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size/description/)
- [ ] [50. Pow(x, n)](https://leetcode.com/problems/powx-n/description/)
- [ ] [367. Valid Perfect Square](https://leetcode.com/problems/valid-perfect-square/description/)
- [ ] [744. Find Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target/description/)
- [ ] [153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)
- [ ] [154. Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/description/)
- [ ] [349. Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/description/)
- [ ] [350. Intersection of Two Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii/description/)
- [ ] [167. Two Sum II - [ ] Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)
- [ ] [287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/description/)
- [ ] [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/description/)
- [ ] [719. Find K-th Smallest Pair Distance](https://leetcode.com/problems/find-k-th-smallest-pair-distance/description/)
- [ ] [410. Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/description/)

### Binary Tree

- [x] [144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/description/)
- [x] [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)
- [x] [145. Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/description/)
- [x] [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)
- [x] [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)
- [x] [101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/description/)
- [ ] [112. Path Sum](https://leetcode.com/problems/path-sum/description/)
- [ ] [250. Count Univalue Subtrees](https://leetcode.com/problems/count-univalue-subtrees/description/)
- [ ] [106. Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/)
- [ ] [105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)
- [ ] [116. Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/description/)
- [ ] [117. Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/description/)
- [ ] [236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/)
- [ ] [297. Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/)

### N-ary Tree

- [ ] [589. N-ary Tree Preorder Traversal](https://leetcode.com/problems/n-ary-tree-preorder-traversal/description/)
- [ ] [590. N-ary Tree Postorder Traversal](https://leetcode.com/problems/n-ary-tree-postorder-traversal/description/)
- [ ] [429. N-ary Tree Level Order Traversal](https://leetcode.com/problems/n-ary-tree-level-order-traversal/description/)
- [ ] [559. Maximum Depth of N-ary Tree](https://leetcode.com/problems/maximum-depth-of-n-ary-tree/description/)
- [ ] [431. Encode N-ary Tree to Binary Tree](https://leetcode.com/problems/encode-n-ary-tree-to-binary-tree/description/)
- [ ] [428. Serialize and Deserialize N-ary Tree](https://leetcode.com/problems/serialize-and-deserialize-n-ary-tree/description/)

### Binary Search Tree

- [ ] [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/description/)
- [ ] [285. Inorder Successor in BST](https://leetcode.com/problems/inorder-successor-in-bst/description/)
- [ ] [173. Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator/description/)
- [ ] [700. Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/description/)
- [ ] [701. Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/description/)
- [ ] [450. Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/description/)
- [ ] [703. Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/description/)
- [ ] [235. Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/)
- [ ] [220. Contains Duplicate III](https://leetcode.com/problems/contains-duplicate-iii/description/)
- [ ] [110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/description/)
- [ ] [108. Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/description/)

### Heap

- [ ] [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)
- [ ] [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/description/)
- [ ] [703. Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/description/)
- [ ] [1046. Last Stone Weight](https://leetcode.com/problems/last-stone-weight/description/)
- [ ] [1337. The K Weakest Rows in a Matrix](https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix/description/)
- [ ] [378. Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/description/)
- [ ] [253. Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/description/)
- [ ] [973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/description/)
- [ ] [1167. Minimum Cost to Connect Sticks](https://leetcode.com/problems/minimum-cost-to-connect-sticks/description/)
- [ ] [1642. Furthest Building You Can Reach](https://leetcode.com/problems/furthest-building-you-can-reach/description/)
- [ ] [295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/description/)

### Trie

- [ ] [208. Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/description/)
- [ ] [677. Map Sum Pairs](https://leetcode.com/problems/map-sum-pairs/description/)
- [ ] [648. Replace Words](https://leetcode.com/problems/replace-words/description/)
- [ ] [642. Design Search Autocomplete System](https://leetcode.com/problems/design-search-autocomplete-system/description/)
- [ ] [211. Add and Search Word - [ ] Data structure design](https://leetcode.com/problems/add-and-search-word-data-structure-design/description/)
- [ ] [421. Maximum XOR of Two Numbers in an Array](https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/description/)
- [ ] [212. Word Search II](https://leetcode.com/problems/word-search-ii/description/)
- [ ] [425. Word Squares](https://leetcode.com/problems/word-squares/description/)
- [ ] [336. Palindrome Pairs](https://leetcode.com/problems/palindrome-pairs/description/)

### Graph

- [ ] [547. Number of Provinces](https://leetcode.com/problems/number-of-provinces/description/)
- [ ] [261. Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree/description/)
- [ ] [323. Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/description/)
- [ ] [1101. The Earliest Moment When Everyone Become Friends](https://leetcode.com/problems/the-earliest-moment-when-everyone-become-friends/description/)
- [ ] [1202. Smallest String With Swaps](https://leetcode.com/problems/smallest-string-with-swaps/description/)
- [ ] [399. Evaluate Division](https://leetcode.com/problems/evaluate-division/description/)
- [ ] [1168. Optimize Water Distribution in a Village](https://leetcode.com/problems/optimize-water-distribution-in-a-village/description/)
- [ ] [1971. Find if Path Exists in Graph](https://leetcode.com/problems/find-if-path-exists-in-graph/description/)
- [ ] [797. All Paths From Source to Target](https://leetcode.com/problems/all-paths-from-source-to-target/description/)
- [ ] [133. Clone Graph](https://leetcode.com/problems/clone-graph/description/)
- [ ] [332. Reconstruct Itinerary](https://leetcode.com/problems/reconstruct-itinerary/description/)
- [ ] [1059. All Paths from Source Lead to Destination](https://leetcode.com/problems/all-paths-from-source-lead-to-destination/description/)
- [ ] [1971. Find if Path Exists in Graph](https://leetcode.com/problems/find-if-path-exists-in-graph/description/)
- [ ] [797. All Paths From Source to Target](https://leetcode.com/problems/all-paths-from-source-to-target/description/)
- [ ] [116. Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/description/)
- [ ] [1091. Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/description/)
- [ ] [429. N-ary Tree Level Order Traversal](https://leetcode.com/problems/n-ary-tree-level-order-traversal/description/)
- [ ] [994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/description/)
- [ ] [1584. Min Cost to Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points/description/)
- [ ] [1584. Min Cost to Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points/description/)
- [ ] [743. Network Delay Time](https://leetcode.com/problems/network-delay-time/description/)
- [ ] [787. Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/description/)
- [ ] [1631. Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort/description/)
- [ ] [210. Course Schedule II](https://leetcode.com/problems/course-schedule-ii/description/)
- [ ] [269. Alien Dictionary](https://leetcode.com/problems/alien-dictionary/description/)
- [ ] [310. Minimum Height Trees](https://leetcode.com/problems/minimum-height-trees/description/)
- [ ] [1136. Parallel Courses](https://leetcode.com/problems/parallel-courses/description/)

### Dynamic Programming

- [ ] [198. House Robber](https://leetcode.com/problems/house-robber/description/)
- [ ] [746. Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/description/)
- [ ] [1137. N-th Tribonacci Number](https://leetcode.com/problems/n-th-tribonacci-number/description/)
- [ ] [740. Delete and Earn](https://leetcode.com/problems/delete-and-earn/description/)
- [ ] [1770. Maximum Score from Performing Multiplication Operations](https://leetcode.com/problems/maximum-score-from-performing-multiplication-operations/description/)
- [ ] [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/description/)
- [ ] [221. Maximal Square](https://leetcode.com/problems/maximal-square/description/)
- [ ] [1335. Minimum Difficulty of a Job Schedule](https://leetcode.com/problems/minimum-difficulty-of-a-job-schedule/description/)
- [ ] [322. Coin Change](https://leetcode.com/problems/coin-change/description/)
- [ ] [139. Word Break](https://leetcode.com/problems/word-break/description/)
- [ ] [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/description/)
- [ ] [188. Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/description/)
- [ ] [309. Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/description/)
- [ ] [746. Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/description/)
- [ ] [276. Paint Fence](https://leetcode.com/problems/paint-fence/description/)
- [ ] [518. Coin Change 2](https://leetcode.com/problems/coin-change-2/description/)
- [ ] [91. Decode Ways](https://leetcode.com/problems/decode-ways/description/)
- [ ] [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)
- [ ] [918. Maximum Sum Circular Subarray](https://leetcode.com/problems/maximum-sum-circular-subarray/description/)
- [ ] [62. Unique Paths](https://leetcode.com/problems/unique-paths/description/)
- [ ] [63. Unique Paths II](https://leetcode.com/problems/unique-paths-ii/description/)
- [ ] [64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/description/)
- [ ] [931. Minimum Falling Path Sum](https://leetcode.com/problems/minimum-falling-path-sum/description/)
- [ ] [714. Best Time to Buy and Sell Stock with Transaction Fee](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/description/)
- [ ] [256. Paint House](https://leetcode.com/problems/paint-house/description/)
- [ ] [265. Paint House II](https://leetcode.com/problems/paint-house-ii/description/)
- [ ] [1473. Paint House III](https://leetcode.com/problems/paint-house-iii/description/)
- [ ] [1220. Count Vowels Permutation](https://leetcode.com/problems/count-vowels-permutation/description/)
- [ ] [718. Maximum Length of Repeated Subarray](https://leetcode.com/problems/maximum-length-of-repeated-subarray/description/)
- [ ] [1155. Number of Dice Rolls With Target Sum](https://leetcode.com/problems/number-of-dice-rolls-with-target-sum/description/)
- [ ] [790. Domino and Tromino Tiling](https://leetcode.com/problems/domino-and-tromino-tiling/description/)
- [ ] [983. Minimum Cost For Tickets](https://leetcode.com/problems/minimum-cost-for-tickets/description/)
- [ ] [97. Interleaving String](https://leetcode.com/problems/interleaving-string/description/)

### Bit Manipulation

- [ ] [504. Base 7](https://leetcode.com/problems/base-7/description/)
- [ ] [405. Convert a Number to Hexadecimal](https://leetcode.com/problems/convert-a-number-to-hexadecimal/description/)
- [ ] [191. Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/description/)
- [ ] [190. Reverse Bits](https://leetcode.com/problems/reverse-bits/description/)
- [ ] [371. Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/description/)
- [ ] [89. Gray Code](https://leetcode.com/problems/gray-code/description/)
- [ ] [201. Bitwise AND of Numbers Range](https://leetcode.com/problems/bitwise-and-of-numbers-range/description/)
- [ ] [338. Counting Bits](https://leetcode.com/problems/counting-bits/description/)
- [ ] [136. Single Number](https://leetcode.com/problems/single-number/description/)
- [ ] [137. Single Number II](https://leetcode.com/problems/single-number-ii/description/)
- [ ] [260. Single Number III](https://leetcode.com/problems/single-number-iii/description/)
- [ ] [1349. Maximum Students Taking Exam](https://leetcode.com/problems/maximum-students-taking-exam/description/)

