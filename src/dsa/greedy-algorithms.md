# Greedy Algorithms

## Signal

Typically finding the minimum or the maximum of a property of the input array.

## Steps

1. Determine if you should greedily pick the minimum or the maximum at each step.
2. Sort the input array (often you may need to sort based on the frequency of each element).
3. Iterate over the sorted array and increment the result, making use of a priority queue as needed.

## Complexity Analysis

Let \\(n\\) be the length of the input array. Then, typically:
- Time Complexity: worst-case \\(O(n \log n)\\), dominated by the sort in step 2 (or \\(O(n \log n)\\) from priority queue pushes/pops in step 3, if one is used)
- Space Complexity: worst-case \\(O(n)\\), or \\(O(1)\\) if the sort is in-place and no auxiliary priority queue is needed

> [!NOTE]
> These bounds depend entirely on the specific greedy strategy chosen; an algorithm that skips sorting or the priority queue can do better (e.g., \\(O(n)\\)).

