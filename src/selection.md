# Selection

## Problem

Given an unsorted array and an integer \\(k\\), find the \\(k^\text{th}\\) smallest element (i.e., the element that would be at index \\(k\\) if the array were sorted).

## QuickSelect (Hoare's Selection Algorithm)

> [!NOTE]
> For streaming input or small \\(k\\), prefer a priority queue of size \\(k\\), and for repeated queries on a changing set, prefer an augmented BST.

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

Let \\(n\\) be the length of the array. Then:
- Time Complexity: worst-case \\(O(n^2)\\), but average-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(1)\\)

