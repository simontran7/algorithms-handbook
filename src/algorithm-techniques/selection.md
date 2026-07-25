# Selection

## Problem

Given an unsorted array and an integer $k$, find the $k^\text{th}$ smallest element (the element that would be at index $k$ if the array were sorted).

## QuickSelect (Hoare's Selection Algorithm)

### Use Case

- Find the $k^\text{th}$ smallest/largest element in a static array, one-shot
- Top-$k$ variants where the array may be reordered (e.g., K Closest Points to Origin)

> [!NOTE]
> For streaming input or small $k$, prefer a size-$k$ priority queue, and for repeated queries on a changing set, prefer an augmented BST.

### Template

```cpp
#include <random>

int quickselect(std::vector<int>& array, int k) {
    std::mt19937 gen(std::random_device{}());

    auto partition = [&](int left, int right, int pivot_idx) -> int {
        int pivot_val = array[pivot_idx];
        std::swap(array[pivot_idx], array[right]);
        int write_idx = left;
        for (int i = left; i < right; ++i) {
            if (array[i] < pivot_val) {
                std::swap(array[write_idx], array[i]);
                write_idx++;
            }
        }
        std::swap(array[right], array[write_idx]);
        return write_idx;
    };

    int low = 0;
    int high = array.size() - 1;

    while (low <= high) {
        int pivot_idx = std::uniform_int_distribution<>(low, high)(gen);
        pivot_idx = partition(low, high, pivot_idx);

        if (pivot_idx < k) {
            low = pivot_idx + 1;
        } else if (pivot_idx > k) {
            high = pivot_idx - 1;
        } else {
            return array[k];
        }
    }

    return -1;  // unreachable for valid k
}
```

### Complexity Analysis

Let \(n\) be the length of the array. Then:
- Time Complexity: average-case \(O(n)\), worst-case \(O(n^2)\)
- Space Complexity: worst-case \(O(1)\)

> [!NOTE]
> The average case follows from each partition recursing into only one side: \(n + \frac{n}{2} + \frac{n}{4} + \cdots = O(n)\). The \(O(n^2)\) worst case requires the random pivot to be nearly the smallest/largest at every step, which randomization makes vanishingly unlikely. The space is \(O(1)\) because this template is iterative (a recursive implementation would use \(O(\log n)\) average stack depth).

> [!NOTE]
> The standard library ships quickselect as **`std::nth_element(array.begin(), array.begin() + k, array.end())`**, where afterwards `array[k]` is the \(k^\text{th}\) smallest, with everything before it \(\le\) and everything after \(\ge\). 