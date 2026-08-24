# Selection

## Problem

Given an unsorted array and an integer $k$, find the $k^\text{th}$ smallest element (the element that would be at index $k$ if the array were sorted).

## QuickSelect (Hoare's Selection Algorithm)

> [!NOTE]
> For streaming input or small $k$, prefer a size-$k$ priority queue, and for repeated queries on a changing set, prefer an augmented BST.

### Template

```python
import random

def quickselect(array, k):
    def partition(left, right, pivot_idx):
        pivot_val = array[pivot_idx]
        array[pivot_idx], array[right] = array[right], array[pivot_idx]
        write_idx = left
        for i in range(left, right):
            if array[i] < pivot_val:
                array[write_idx], array[i] = array[i], array[write_idx]
                write_idx += 1
        array[right], array[write_idx] = array[write_idx], array[right]
        return write_idx

    low = 0
    high = len(array) - 1

    while low <= high:
        pivot_idx = random.randint(low, high)
        pivot_idx = partition(low, high, pivot_idx)

        if pivot_idx < k:
            low = pivot_idx + 1
        elif pivot_idx > k:
            high = pivot_idx - 1
        else:
            return array[k]

    return -1  # unreachable for valid k
```

### Complexity Analysis

Let $n$ be the length of the array. Then:
- Time Complexity: average-case $O(n)$, worst-case $O(n^2)$
- Space Complexity: worst-case $O(1)$

> [!NOTE]
> The average case follows from each partition recursing into only one side: $n + \frac{n}{2} + \frac{n}{4} + \cdots = O(n)$. The $O(n^2)$ worst case requires the random pivot to be nearly the smallest/largest at every step, which randomization makes vanishingly unlikely. The space is $O(1)$ because this template is iterative (a recursive implementation would use $O(\log n)$ average stack depth).

> [!NOTE]
> Python's standard library has no built-in quickselect. `heapq.nsmallest(k + 1, array)[-1]` gives the $k^\text{th}$ smallest in $O(n \log k)$ instead of $O(n)$ average; for true $O(n)$ average, use the template above, or `numpy.partition(array, k)[k]` if NumPy is available.
