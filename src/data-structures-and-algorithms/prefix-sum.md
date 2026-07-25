# Prefix Sum

## Use Case

You need a subroutine which involves range-sum queries of a subarray in \(O(1)\).

## Template

```rust
fn prefix_sum(array: &[i32]) -> Vec<i32> {
    let mut result = vec![0];

    for &num in array {
        result.push(result.last().unwrap() + num);
    }

    result // sum from [i..j]: `prefix[j + 1] - prefix[i]`
}
```