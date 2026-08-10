# Prefix Sum

## Use Case

You need a subroutine which involves range-sum queries of a subarray in \\(O(1)\\).

## Template

```cpp
std::vector<int> prefix_sum(std::vector<int>& array) {
    std::vector<int> result = {0};

    for (int num : array) {
        result.push_back(result.back() + num);
    }

    return result; // sum from [i..j]: `prefix[j + 1] - prefix[i]`
}
```
