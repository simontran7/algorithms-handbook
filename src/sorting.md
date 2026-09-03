# Sorting

## Problem

Given a sequence of \(n\) elements \(A = \langle a_1, a_2, \ldots, a_n \rangle\), rearrange the elements into nondecreasing order, so that

\[
a_1 \leq a_2 \leq \cdots \leq a_n.
\]

## Bubble Sort

### Template

```python
def bubble_sort(array):
    n = len(array)

    for i in range(n):
        swapped = False

        for j in range(n - 1 - i):
            if array[j] > array[j + 1]:
                array[j], array[j + 1] = array[j + 1], array[j]
                swapped = True

        if not swapped:
            break
```

### Complexity Analysis

Let \(N\) be the number of elements in the input sequence. Then:
- Time: worst-case \(O(N^2)\)
- Auxiliary Space: worst-case \(O(1)\)

## Selection Sort

## Insertion Sort

## Heap Sort

## Merge Sort

## Quick Sort

## Counting Sort

## Radix Sort

## Bucket Sort
