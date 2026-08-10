# Prefix State

## Use Case

- Find the longest/shortest subarray that satisfies some condition
- Count the number of subarrays that satisfies some condition, and the state of any subarray `array[i..j]` can be computed from two prefix states `state[0..j]` and `state[0..(i - 1)]`.

## Template

```cpp
#include <limits>
#include <unordered_map>

int prefix_state(std::vector<int>& array, int target_state) {
    std::unordered_map<int, int> state_index_map = {{0, -1}}; // we'll want to store the state as the key, and the first index of its appearance if looking for the longest subarray, the last index of its appearance if looking for the longest subarray, or its frequency as the value.
    int current_state = 0;
    int result = 0; // initialize to `std::numeric_limits<int>::max()` if looking for shortest subarray

    for (int i = 0; i < array.size(); i++) {
        current_state = <update the running prefix state with the new element>;

        int needed_state = current_state - target_state; // or `current_state ^ target_state`
        if (state_index_map.count(needed_state)) {
            int subarray_len = i - state_index_map[needed_state];
            result = std::max(result, subarray_len); // for shortest, use `std::min()` instead
        } else {
            state_index_map[current_state] = i; // for shortest, remove the else branch and do this instead `state_index_map[current_state] = i`
        }
    }

    return result; // for shortest subarray, do this instead `return result != std::numeric_limits<int>::max() ? result : 0`
}
```
