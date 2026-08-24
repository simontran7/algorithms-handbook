# Searching

## Problem

Given a collection of candidates and a criterion, find an element that satisfies the criterion (or determine that none does).

## Binary Search

### Exact Match On an Array

#### Use Case

For some input array, `array`, and a desired element `target`, `array` must be sorted, and you want to find the index of `target` if it is in `array`, or otherwise return `-1`.

#### Template

```python
def binary_search(array, target):
    low = 0
    high = len(array) - 1

    while low <= high:
        mid = low + (high - low) // 2

        if <found condition>:
            return mid

        if <go right condition>:
            low = mid + 1
        else:
            high = mid - 1

    return -1
```

#### Complexity Analysis

Let $n$ be the length of the array. Then:
- Time Complexity: worst-case $O(\log n)$
- Space Complexity: worst-case $O(1)$

### Boundary Convergence On an Array

#### Use Case

You want the first index where a condition flips in a sorted array (e.g. find minimum in rotated sorted array, or more commonly, you want to find a neighbouring value of a target value)

#### Template

```python
def lower_bound(array, target):
    """Returns the index of the leftmost value >= `target`"""
    low = 0
    high = len(array)

    while low < high:
        mid = low + (high - low) // 2
        if array[mid] < target:
            low = mid + 1
        else:
            high = mid

    return low
```

```python
def upper_bound(array, target):
    """Returns the index of the leftmost value > `target`"""
    low = 0
    high = len(array)

    while low < high:
        mid = low + (high - low) // 2
        if array[mid] <= target:
            low = mid + 1
        else:
            high = mid

    return low
```

#### Complexity Analysis

Let $n$ be the length of the array. Then, for `lower_bound()`, `upper_bound()`, and the `find_*()` helpers built on them:
- Time Complexity: worst-case $O(\log n)$
- Space Complexity: worst-case $O(1)$

> [!NOTE]
> If you want the neighbouring value to a target, then the template requires little to no changes, and then use it as follows accordingly. Otherwise, you likely need to tweak the if condition, and set `high = array.size() - 1` (in the pure `lower_bound()` and `upper_bound()`, we kept `high = array.size()` because an insertion point that goes beyond the last element of the array is valid).

```python
def find_lt(array, target):
    """Returns the rightmost value < `target`"""
    i = lower_bound(array, target)
    if i > 0:
        return array[i - 1]
    raise ValueError("no value < target")

def find_le(array, target):
    """Returns the rightmost value <= `target`"""
    i = upper_bound(array, target)
    if i > 0:
        return array[i - 1]
    raise ValueError("no value <= target")

def find_gt(array, target):
    """Returns the leftmost value > `target`"""
    i = upper_bound(array, target)
    if i != len(array):
        return array[i]
    raise ValueError("no value > target")

def find_ge(array, target):
    """Returns the leftmost value >= `target`"""
    i = lower_bound(array, target)
    if i != len(array):
        return array[i]
    raise ValueError("no value >= target")
```

> [!NOTE]
> `binary_search()` doesn't work if `array` contains duplicates, but `lower_bound()` and `upper_bound()` allows duplicates in `array`.

> [!NOTE]
> If the input array is sorted in descending order, simply invert the inequality in the if condition.

### Boundary Convergence On a Solution Space

#### Use Case

You're trying to find a **maximum** or **minimum** value, and:

- You can verify (usually with a greedy algorithm) in $O(n)$ time (or faster) whether a given candidate `x` is a valid solution
- The solution space has to be structured so that all valid answers are grouped together on one side. That is:
    - If `x` is a valid solution:
        - For a maximum, all values $\le x$ are also valid.
        - For a minimum, all values $\ge x$ are also valid.
    - If `x` is not a valid solution:
        - For a maximum, all values $\gt x$ are also invalid.
        - For a minimum, all values $\lt x$ are also invalid.

#### Template

```python
def binary_search_minimum(array):
    def is_valid(x):
        # Some O(n) algorithm (usually also a greedy algorithm)
        return <boolean>

    low = <minimum possible answer>
    high = <maximum possible answer>

    while low <= high:
        mid = low + (high - low) // 2
        if is_valid(mid):
            high = mid - 1
        else:
            low = mid + 1

    return low
```

```python
def binary_search_maximum(array):
    def is_valid(x):
        # Some O(n) algorithm (usually also a greedy algorithm)
        return <boolean>

    low = <minimum possible answer>
    high = <maximum possible answer>

    while low <= high:
        mid = low + (high - low) // 2
        if is_valid(mid):
            low = mid + 1
        else:
            high = mid - 1

    return high
```

#### Complexity Analysis

Let $k$ be the size of the solution space (`high - low`) and $f(n)$ be the time complexity of `is_valid()`. Then:
- Time Complexity: worst-case $O(f(n) \log k)$
- Space Complexity: worst-case $O(1)$, and whatever `is_valid()` itself uses
