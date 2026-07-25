# Sliding Window

## Variable 

### Use Case

You are looking for the longest/smallest subarray/substring that satisfies a certain constraint.

### Templates

```cpp
int variable_sliding_window_max(std::vector<int>& array) {
    int left = 0;
    int current = 0;
    int result = 0;

    for (int right = 0; right < array.size(); right++) {
        // 1. unconditonally extend add the new element to the window.
        <update state for array[right]>;

        // 2. while the invariant is violated, restore the sliding window.
        while (<window is broken condition>) {
            <update state for array[left]>;   // undo the leaving element's contribution to the sliding window
            left++;
        }

        // 3. record the window length now that the invariant now holds (i.e., window is valid).
        result = std::max(result, right - left + 1);
    }

    return result;
}
```

```cpp
#include <limits>

int variable_sliding_window_min(std::vector<int>& array) {
    int left = 0;
    <data to track the window> current;
    int result = std::numeric_limits<int>::max();

    for (int right = 0; right < array.size(); right++) {
        // 1. unconditonally extend add the new element to the window.
        <update `current` for `array[right]`>;

        // 2. while the invariant holds, shrink the sliding window.
        while (<window is valid condition>) {
            result = std::min(result, right - left + 1);
            <update `current` for `array[left]`>;
            left++;
        }
    }

    return result != std::numeric_limits<int>::max() ? result : -1;
}
```

### Complexity Analysis

Let \\(n\\) be the length of the array. Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(1)\\)

## Fixed 

### Use Case

You are looking for a subarray/substring of some length `k` that satisfies a certain constraint.

### Template

```cpp
<result type> fixed_sliding_window(std::vector<int>& array, int k) {
    <data to track the window> current;
    <result type> result = <initial value>;

    // 1. seed the first window of size `k`.
    for (int i = 0; i < k; i++) {
        <update `current` for array[i]>;
    }

    <update result from initial window>;

    // 2. slide the window: add `right`, remove `left`, update `result`.
    for (int right = k; right < array.size(); right++) {
        <update `current` for `array[right]`>;
        <undo `current` for `array[right - k]`>;
        <update `result`>;
    }

    return result;
}
```

### Complexity Analysis

Let \\(n\\) be the length of the array and \\(k\\) the window size. Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(1)\\), excluding the \\(O(k)\\) needed to seed the first window if `current` tracks per-element state

> [!NOTE]
> The constraint must be preserved as the sliding window shrinks. If shrinking the window can break the constraint, consider using the _prefix state_ technique instead.

> [!NOTE]
> The formula for the length of any window is `right - left + 1` .
