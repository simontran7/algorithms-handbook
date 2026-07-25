# Selection

## Problem

## QuickSelect (Hoare's Selection Algorithm) 

### Signal

### Template

```rust
use rand::Rng;

fn quickselect(array: &mut [i32], k: usize) -> i32 {
    fn partition(array: &mut [i32], left: usize, right: usize, pivot_idx: usize) -> usize {
        let pivot_val = array[pivot_idx];
        array.swap(pivot_idx, right);
        let mut write_idx = left;
        for i in left..right {
            if array[i] < pivot_val {
                array.swap(write_idx, i);
                write_idx += 1;
            }
        }
        array.swap(right, write_idx);
        write_idx
    }

    let mut low = 0;
    let mut high = array.len() - 1;

    loop {
        let pivot_idx = rand::thread_rng().gen_range(low..=high);
        let pivot_idx = partition(array, low, high, pivot_idx);

        if pivot_idx < k {
            low = pivot_idx + 1;
        } else if pivot_idx > k {
            high = pivot_idx - 1;
        } else {
            return array[k];
        }
    }
}
```

