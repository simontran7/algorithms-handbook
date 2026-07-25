# Searching

## Problem

Given a collection and a target value, determine whether the target exists in the collection, and if so, where.

## Binary Search

### Exact Match On an Array

#### Use Case

For some input array, `array`, and a desired element `target`, `array` must be sorted, and you want to find the index of `target` if it is in `array`, or otherwise return `-1`.

#### Template

```rust
fn binary_search(array: &[i32], target: i32) -> i32 {
    let mut low: i32 = 0;
    let mut high: i32 = array.len() as i32 - 1;
    while low <= high {
        let mid = low + (high - low) / 2;

        if <found condition> {
            return mid;
        }

        if <go right condition> {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    -1
}
```

### Boundary Convergence On an Array

#### Signal

You want the first index where a condition flips in a sorted array (e.g. find minimum in rotated sorted array, or more commonly, you want to find a neighbouring value of a target value)

#### Template

```rust
// Returns the index of the leftmost value >= `target`
fn lower_bound(array: &[i32], target: i32) -> usize {
    let mut low = 0;
    let mut high = array.len();

    while low < high {
        let mid = low + (high - low) / 2;
        if array[mid] < target {
            low = mid + 1;
        } else {
            high = mid;
        }
    }

    low
}
```

```rust
// Returns the index of the leftmost value > `target`
fn upper_bound(array: &[i32], target: i32) -> usize {
    let mut low = 0;
    let mut high = array.len();

    while low < high {
        let mid = low + (high - low) / 2;
        if array[mid] <= target {
            low = mid + 1;
        } else {
            high = mid;
        }
    }

    low
}
```

> [!NOTE]
> If you want the neighbouring value to a target, then the template requires little to no changes, and then use it as follows accordingly. Otherwise, you likely need to tweak the if condition, and set `high = array.len() - 1` (in the pure `lower_bound()` and `upper_bound()`, we kept `high = array.len()` because an insertion point that goes beyond the last element of the array is valid).

```rust
// Returns the rightmost value < `target`
fn find_lt(array: &[i32], target: i32) -> i32 {
    let i = lower_bound(array, target);
    if i > 0 {
        return array[i - 1];
    }
    panic!("no value found")
}

// Returns the rightmost value <= `target`
fn find_le(array: &[i32], target: i32) -> i32 {
    let i = upper_bound(array, target);
    if i > 0 {
        return array[i - 1];
    }
    panic!("no value found")
}

// Returns the leftmost value > `target`
fn find_gt(array: &[i32], target: i32) -> i32 {
    let i = upper_bound(array, target);
    if i != array.len() {
        return array[i];
    }
    panic!("no value found")
}

// Returns the leftmost value >= `target`
fn find_ge(array: &[i32], target: i32) -> i32 {
    let i = lower_bound(array, target);
    if i != array.len() {
        return array[i];
    }
    panic!("no value found")
}
```

> [!NOTE]
> `binary_search()` doesn't work if `array` contains duplicates, but `lower_bound()` and `upper_bound()` allows duplicates in `array`.

> [!NOTE]
> If the input array is sorted in descending order, simply invert the inequality in the if condition.

### Boundary Convergence On a Solution Space

#### Signal

You're trying to find a **maximum** or **minimum** value, and:

- You can verify (usually with a greedy algorithm) in \(O(n)\) time (or faster) whether a given candidate `x` is a valid solution
- The solution space has to be structured so that all valid answers are grouped together on one side. That is:
    - If `x` is a valid solution:
        - For a maximum, all values \( \le x\) are also valid.
        - For a minimum, all values \(\ge x\) are also valid.
    - If `x` is not a valid solution:
        - For a maximum, all values \(\gt x\) are also invalid.
        - For a minimum, all values \(\lt x\) are also invalid.

#### Template

```rust
fn binary_search_minimum(array: &[i32]) -> i32 {
    fn is_valid(x: i32) -> bool {
        // Some O(n) algorithm (usually also a greedy algorithm)
        <boolean>
    }

    let mut low: i32 = <minimum possible answer>;
    let mut high: i32 = <maximum possible answer>;

    while low <= high {
        let mid = low + (high - low) / 2;
        if is_valid(mid) {
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }

    low
}
```

```rust
fn binary_search_maximum(array: &[i32]) -> i32 {
    fn is_valid(x: i32) -> bool {
        // Some O(n) algorithm (usually also a greedy algorithm)
        <boolean>
    }

    let mut low: i32 = <minimum possible answer>;
    let mut high: i32 = <maximum possible answer>;

    while low <= high {
        let mid = low + (high - low) / 2;
        if is_valid(mid) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }

    high
}
```

## Complexity Analysis

Let \(n\) be the size of your initial search space. Then:
- Time Complexity: worst-case \(O(\log n)\)
- Space Complexity: worst-case \(O(1)\)
