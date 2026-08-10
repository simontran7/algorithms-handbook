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

## Complexity Analysis

Let \\(S\\) be number of possible states explored and \\(C\\) the cost of processing a single state. Then:
- Time Complexity: worst-case \\(O(S \cdot C)\\)
- Space Complexity: worst-case \\(O(d)\\) for the recursion stack, where \\(d\\) is the maximum depth of the recursion (i.e., the length of a complete `path`), excluding the space to store `path` itself or the accumulated results

> [!NOTE]
> Common values of \\(S\\) in the backtracking algorithm worst-case time complexity formula:
> - Combinations of \\(k\\) from \\(n\\): \\(\binom{n}{k}\\)
> - Permutations of from \\(n\\): \\(\frac{n!}{(n - k)!}\\)
> - Generic tree with branching factor \\(b\\) and depth \\(d\\): \\(b^d\\)

> [!NOTE]
> Backtracking can be visualized as a tree, where each node represents the current state of the path during a recursive function call. The `backtrack()` calls explore different branches of this tree, building potential solutions along the way. The leaves of the tree correspond to base cases, often representing complete solutions, though not necessarily in every problem.

> [!NOTE]
> Pass `path` by **reference** (`std::vector<int>&`), never by value, as copying it at every call would add an \\(O(n)\\) cost per node.