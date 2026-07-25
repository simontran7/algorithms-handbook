# Divide and Conquer

## Use Case

The problem has a natural partition where it can be split into independent subproblems of the same type, solved separately, then combined.

## Template

```rust
fn divide_and_conquer(s: S) -> T {
    // Divide
    let subproblems = divide(s);

    // Conquer
    let subresults: Vec<T> = subproblems.into_iter().map(divide_and_conquer).collect();

    // Combine
    combine(subresults)
}
```

