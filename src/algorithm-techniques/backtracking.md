## Backtracking (Complete Search)

## Use Case

Enumerating all possible solutions

## Template

```cpp
bool is_valid(/* candidate */) {
    // Some logic to check if candidate is valid or not
}

int backtrack(std::vector<int>& path /*, other state variables */) {
    if (/* base case */) {
        // update global result (i.e., append the path to the global result
        // or increment the global result)
        return /* ... */;
    }

    int local_result = /* initial value */;
    for (/* candidate in input */) {
        if (!is_valid(candidate)) {
            continue;
        }
        // modify `path`
        local_result += backtrack(path /*, other state variables */);
        // undo the modification to `path`
    }

    return local_result;
}
```

> [!NOTE]
> Backtracking can be visualized as a tree, where each node represents the current state of the path during a recursive function call. The `backtrack()` calls explore different branches of this tree, building potential solutions along the way. The leaves of the tree correspond to base cases, often representing complete solutions, though not necessarily in every problem.

> [!NOTE]
> Pass `path` by **reference** (`std::vector<int>&`), never by value, as copying it at every call would add an $O(n)$ cost per node.