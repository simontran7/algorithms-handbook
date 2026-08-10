# Sorting

## Comparison-Based Algorithms

### Bubble Sort

#### Complexity Analysis

- Time Complexity: worst-case \\(O(N^2)\\)
- Space Complexity: worst-case \\(O(1)\\)

#### Code

```
func bubble_sort<T: PartialOrder>(array: &mut [T]) {
    let n = array.count();
    for i in 0..n {
        let mut swapped = false;
        for j in 0..n - 1 - i {
            if array[j] > array[j + 1] {
                array.swap(j, j + 1);
                swapped = true;
            }
        }       
        if not swapped {
            break; 
        }
    }
}
```

### Selection Sort

### Insertion Sort

### Heap Sort

### Merge Sort

### Quick Sort

## Non-comparison-Based Algorithms

### Counting Sort

### Radix Sort

### Bucket Sort