# Backtracking (Complete Search)

## Use Case

Enumerating all possible solutions

## Template

```rust
fn is_valid(candidate: &T) -> bool {
    // check if candidate is valid or not
}

fn backtrack(path: &mut Vec<T>, <other state variables>) -> i32 {
    if <base case> {
        // update global result (i.e., append the path to the global result or increment the global result)
        return 0;
    }

    let mut local_result = <initial value>;
    for candidate in <input> {
        if !is_valid(&candidate) {
            continue;
        }
        // modify `path`
        local_result += backtrack(path, <other state variables>);
        // undo the modification to `path`
    }

    local_result
}
```

> [!NOTE]
> Backtracking can be visualized as a tree, where each node represents the current state of the path during a recursive function call. The `backtrack()` calls explore different branches of this tree, building potential solutions along the way. The leaves of the tree correspond to base cases, often representing complete solutions, though not necessarily in every problem.

## Complexity Analysis

$$
O(S \cdot C)
$$

- \(S\): number of possible states explored
- \(C\): cost of processing a single state

> [!NOTE]
> Common values of \(S\) in the backtracking algorithm worst-case time complexity formula:
> - Combinations of \(k\) from \(n\): \(\binom{n}{k}\)
> - Permutations of from \(n\): \(\frac{n!}{(n - k)!}\)
> - Generic tree with branching factor \(b\) and depth \(d\): \(b^d\)

