# Prefix State

## Use Case

- Find the longest/shortest subarray that satisfies some condition
- Count the number of subarrays that satisfies some condition, and the state of any subarray `array[i..j]` can be computed from two prefix states `state[0..j]` and `state[0..(i - 1)]`.

## Template

```python
def prefix_state(array, target_state):
    state_index_map = {0: -1}  # we'll want to store the state as the key, and the first index of its appearance if looking for the longest subarray, the last index of its appearance if looking for the longest subarray, or its frequency as the value.
    current_state = 0
    result = 0  # initialize to `float("inf")` if looking for shortest subarray

    for i in range(len(array)):
        current_state = <update the running prefix state with the new element>

        needed_state = current_state - target_state  # or `current_state ^ target_state`
        if needed_state in state_index_map:
            subarray_len = i - state_index_map[needed_state]
            result = max(result, subarray_len)  # for shortest, use `min()` instead
        else:
            state_index_map[current_state] = i  # for shortest, remove the else branch and do this instead `state_index_map[current_state] = i`

    return result  # for shortest subarray, do this instead `return result if result != float("inf") else 0`
```
