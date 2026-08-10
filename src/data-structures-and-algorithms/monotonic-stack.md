# Monotonic Stack

## Use Case

- Looking for the next/previous greater/smaller element
- Spans, ranges, or boundaries

#### Template

```cpp
std::vector<int> monotonic_decreasing_stack(const std::vector<int>& array) {
    std::vector<int> mono_stack;
    auto result = /* initial value */;

    for (int i = 0; i < array.size(); ++i) {
        while (!mono_stack.empty() && array[mono_stack.back()] < array[i]) {
            mono_stack.pop_back();
            // Utilize the popped index in result
            // e.g. result[mono_stack.back()] = /* something involving i */;
            // e.g. result += mono_stack.back();
            // (read back() before pop_back() if you need the popped value)
        }

        mono_stack.push_back(i);
    }

    return result;
}
```
