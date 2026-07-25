# Two Pointers 

## Opposite Ends

### Signal

The list input is sorted, and you are looking for a pair (or pairs) that meet a specific condition.

### Template

```rust
fn opposite_ends_two_pointers(array: &[T]) -> i32 {
    let mut left = 0;
    let mut right = array.len() - 1;
    let mut result = 0;

    while left < right {
        // Some logic involving `array[left]` and/or `array[right]`

        if <condition> {
            left += 1;
        } else {
            right -= 1;
        }
    }

    result
}
```

## Merge

### Signal

The input list is sorted, and you want to perform an in-place modification by filtering or deduplicating elements.

### Template

```rust
fn merge_two_pointers(array1: &[T], array2: &[T]) -> i32 {
    let mut i = 0;
    let mut j = 0;
    let mut result = 0;

    while i < array1.len() && j < array2.len() {
        // Some logic involving `array1[i]` and `array2[j]`
        if <condition> {
            i += 1;
        } else {
            j += 1;
        }
    }

    while i < array1.len() {
        // Some logic involving `array1[i]`
        i += 1;
    }

    while j < array2.len() {
        // Some logic involving `array2[j]`
        j += 1;
    }

    result
}
```

## Read/Write

### Signal

The problem asks you to modify an array in-place and return its new count.

### Template

```rust
fn read_write_two_pointers(array: &mut [T]) -> usize {
    let mut write = 0;

    for read in 0..array.len() {
        if <condition to keep array[read]> {
            array[write] = array[read]; // optionally transform
            write += 1;
        }
    }

    write // new length
}
```
