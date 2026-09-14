# Prefix State

## Stored in Arrays (Prefix Sum)

### Use Case

Query the sum of any range \\([i, j]\\) in \\(O(1)\\)

### Template

```python
def prefix_sum(array):
    """
    Returns an array where the sum of elements in array[i..=j]: prefix[j + 1] - prefix[i]
    """
    prefix = [0] * (len(array) + 1)

    for i, num in enumerate(array):
        prefix[i + 1] = prefix[i] + num

    return prefix
```

```python
def 2d_prefix_sum(matrix):
    """
    Returns a 2D array where the sum from (r1, c1) to (r2, c2) inclusive: prefix[r2 + 1][c2 + 1] - prefix[r1][c2 + 1] - prefix[r2 + 1][c1] + prefix[r1][c1]
    """
    rows = len(matrix)
    cols = len(matrix[0])
    prefix = [[0] * (cols + 1) for _ in range(rows + 1)]

    for i in range(rows):
        for j in range(cols):
            prefix[i + 1][j + 1] = (
                prefix[i][j + 1] + prefix[i + 1][j] - prefix[i][j] + matrix[i][j]
            )

    return prefix
```
  
## Stored in HashMaps

### Use Case

Count or find longest/shortest subarrays, submatrics, or tree paths that satisfies some condition, where that condition can be reduced to comparing a combining function of two prefix states for some invertible combine operation.

### Template

```python
def longest_subarray_with_state(array, target_state):
    """
    Returns the length of the longest subarray in `array` whose state equals `target_state`.
    """
    state_first_index = {0: -1}  # state -> FIRST index it appeared at (greedy: keep earliest)
    current_state = 0
    result = 0

    for i, num in enumerate(array):
        current_state = current_state + num  # or `current_state ^ num`, etc.

        needed_state = current_state - target_state  # or `current_state ^ target_state`
        if needed_state in state_first_index:
            result = max(result, i - state_first_index[needed_state])

        # Only store the FIRST time we see a state — a later index would only
        # ever produce a shorter subarray, so overwriting is never beneficial.
        if current_state not in state_first_index:
            state_first_index[current_state] = i

    return result
```

```python
def shortest_subarray_with_state(array, target_state):
    """
    Returns the length of the shortest subarray in `array` whose state equals `target_state`.
    """
    state_last_index = {0: -1}  # state -> MOST RECENT index it appeared at
    current_state = 0
    result = float("inf")

    for i, num in enumerate(array):
        current_state = current_state + num

        needed_state = current_state - target_state
        if needed_state in state_last_index:
            result = min(result, i - state_last_index[needed_state])

        # Always overwrite — the most recent occurrence gives the shortest
        # possible subarray for any future match.
        state_last_index[current_state] = i

    return result if result != float("inf") else 0
```

```python
def count_subarrays_with_state(array, target_state):
    """
    Returns the number of subarrays in `array` whose state equals `target_state`.
    """
    state_freq = {0: 1}  # state -> how many prefixes have had this state
    current_state = 0
    result = 0

    for num in array:
        current_state = current_state + num

        needed_state = current_state - target_state
        result += state_freq.get(needed_state, 0)

        # Every prefix state seen contributes independently, so accumulate
        # frequency rather than overwrite.
        state_freq[current_state] = state_freq.get(current_state, 0) + 1

    return result
```
