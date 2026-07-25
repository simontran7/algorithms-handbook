# Sliding Window

## Variable 

### Signal

You are looking for the longest/smallest subarray/substring that satisfies a certain constraint.

### Template

```rust
fn variable_sliding_window_max(array: &[T]) -> i32 {
    let mut left = 0;
    let mut current = 0;
    let mut result = 0;

    for right in 0..array.len() {
        // 1. unconditonally extend add the new element to the window.
        <update state for array[right]>

        // 2. while the invariant is violated, restore the sliding window.
        while <window is broken condition> {
            <update state for array[left]> // undo the leaving element's contribution to the sliding window
            left += 1;
        }

        // 3. record the window length now that the invariant now holds (i.e., window is valid).
        result = result.max(right - left + 1);
    }

    result
}
```

```rust
fn variable_sliding_window_min(array: &[T]) -> i32 {
    let mut left = 0;
    let mut current = <data to track the window>;
    let mut result = i32::MAX;

    for right in 0..array.len() {
        // 1. unconditonally extend add the new element to the window.
        <update `current` for `array[right]`>

        // 2. while the invariant holds, shrink the sliding window.
        while <window is valid condition> {
            result = result.min((right - left + 1) as i32);
            <update `current` for `array[left]`>
            left += 1;
        }
    }

    if result != i32::MAX { result } else { -1 }
}
```

## Fixed 

### Signal

You are looking for a subarray/substring of some length `k` that satisfies a certain constraint.

### Template

```rust
fn fixed_sliding_window(array: &[T], k: usize) -> i32 {
    let mut current = <data to track the window>;
    let mut result = <initial value>;

    // 1. seed the first window of size `k`.
    for i in 0..k {
        <update `current` for array[i]>
    }

    <update result from initial window>

    // 2. slide the window: add `right`, remove `left`, update `result`.
    for right in k..array.len() {
        <update `current` for `array[right]`>
        <undo `current` for `array[right - k]`>
        <update `result`>
    }

    result
}
```

> [!NOTE]
> The constraint must be preserved as the sliding window shrinks. If shrinking the window can break the constraint, consider using the _prefix state_ technique instead.

> [!NOTE]
> The formula for the length of any window is `right - left + 1` .
