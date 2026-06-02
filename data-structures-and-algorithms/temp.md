## Divide and Conquer

### Use Case

The problem has a natural partition where it can be split into independent subproblems of the same type, solved separately, then combined.

### Usage

```python
def divide_and_conquer(S):
    # Divide
    subproblems = divide(S)

    # Conquer
    subresults = [divide_and_conquer(subproblem) for subproblem in subproblems]

    # Combine
    return combine(subresults)
```

### Canonical Problems

- [148. Sort List](https://leetcode.com/problems/sort-list/description/)
- [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/description/)
- [493. Reverse Pairs](https://leetcode.com/problems/reverse-pairs/description/)
- [315. Count of Smaller Numbers After Self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/description/)
- [327. Count of Range Sum](https://leetcode.com/problems/count-of-range-sum/description/)

### Bellman-Ford Algorithm (TO LEARN)

### Floyd-Warshall algorithm (TO LEARN)

## Fenwick Tree (Binary Index Tree) (TO LEARN)

## Segment Tree (TO LEARN)

## Suffix Tree (TO LEARN)

## String Matching Algorithms (TO LEARN)

### Rolling hash

### Rabin Karp

### KMP



