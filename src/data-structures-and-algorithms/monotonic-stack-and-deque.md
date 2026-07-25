# Monotonic Stack and Monotonic Deque

## Monotonic Stack

### Signal

- Looking for the next/previous greater/smaller element
- Spans, ranges, or boundaries

### Template

```rust
fn monotonic_decreasing_stack(array: &[i32]) -> i32 {
    let mut mono_stack: Vec<usize> = Vec::new();
    let mut result = <initial value>;

    for i in 0..array.len() {
        while let Some(&top) = mono_stack.last() {
            if array[top] < array[i] {
                mono_stack.pop();
                // Utilize the popped index in result
                // e.g. result[mono_stack.pop().unwrap()] = <something involving i>
                // e.g. result += mono_stack.pop().unwrap()
            } else {
                break;
            }
        }

        mono_stack.push(i);
    }

    result
}
```

## Monotonic Deque

### Signal

Maximum or minimum values in a sliding window or some ranges.

### Template

```rust
use std::collections::VecDeque;

fn monotonic_non_increasing_deque(array: &[i32], k: usize) -> Vec<i32> {
    let mut mono_deque: VecDeque<usize> = VecDeque::new();
    let mut result = Vec::new();

    for i in 0..array.len() {
        while let Some(&back) = mono_deque.back() {
            if array[back] < array[i] {
                mono_deque.pop_back();
            } else {
                break;
            }
        }

        mono_deque.push_back(i);

        if *mono_deque.front().unwrap() as i32 <= i as i32 - k as i32 {
            mono_deque.pop_front();
        }

        if i >= k - 1 {
            result.push(array[*mono_deque.front().unwrap()]);
        }
    }

    result
}
```

> [!NOTE]
> A monotonic increasing/decreasing stack or queue implies that the elements are always increasing/decreasing, while a monotonic non-decreasing/non-increasing one may include repeated elements.
