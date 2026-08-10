# Merge Intervals

## Use Case

Interval problems

## Template

```cpp
std::vector<std::vector<int>> merge(std::vector<std::vector<int>>& intervals) {
    if (intervals.empty()) {
        return {};
    }

    std::sort(intervals.begin(), intervals.end());

    std::vector<std::vector<int>> result = {intervals[0]};

    for (const auto& interval : intervals) {
        int start = interval[0], end = interval[1];
        int prev_end = result.back()[1];
        if (start <= prev_end) {
            result.back()[1] = std::max(prev_end, end);
        } else {
            result.push_back(interval);
        }
    }

    return result;
}
```

## Complexity Analysis

Let \\(n\\) be the number of intervals. Then:
- Time Complexity: worst-case \\(O(n \log n)\\)
- Space Complexity: worst-case \\(O(n)\\)

> [!NOTE]
> The space is for `result` (or the sort itself, if it isn't in-place).