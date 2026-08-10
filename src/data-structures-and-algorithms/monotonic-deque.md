# Monotonic Deque

## Use Case

Maximum or minimum values in a sliding window or some ranges.

## Template

```cpp
#include <deque>

std::vector<int> monotonic_non_increasing_deque(const std::vector<int>& array, int k) {
    std::deque<int> mono_deque;
    std::vector<int> result;

    for (int i = 0; i < array.size(); ++i) {
        while (!mono_deque.empty() && array[mono_deque.back()] < array[i]) {
            mono_deque.pop_back();
        }

        mono_deque.push_back(i);

        if (mono_deque.front() <= i - k) {
            mono_deque.pop_front();
        }

        if (i >= k - 1) {
            result.push_back(array[mono_deque.front()]);
        }
    }

    return result;
}
```
