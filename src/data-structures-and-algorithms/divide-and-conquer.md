# Divide and Conquer

## Use Case

The problem has a natural partition where it can be split into independent subproblems of the same type, solved separately, then combined.

## Template

```cpp
/* result type */ divide_and_conquer(const /* problem type */& s) {
    // Divide
    std::vector</* problem type */> subproblems = divide(s);

    // Conquer
    std::vector</* result type */> subresults;
    for (const auto& subproblem : subproblems) {
        subresults.push_back(divide_and_conquer(subproblem));
    }

    // Combine
    return combine(subresults);
}
```

## Complexity Analysis

A divide-and-conquer algorithm that splits a problem of size \\(n\\) into \\(a\\) subproblems of size \\(n / b\\), doing \\(O(n^d)\\) work outside the recursive calls to divide and combine, has the recurrence \\(T(n) = a \cdot T(n / b) + O(n^d)\\). By the **Master Theorem**:
- If \\(d < \log_b a\\): \\(T(n) = O(n^{\log_b a})\\) (the leaves dominate)
- If \\(d = \log_b a\\): \\(T(n) = O(n^d \log n)\\) (work is balanced across levels)
- If \\(d > \log_b a\\): \\(T(n) = O(n^d)\\) (the root's divide/combine step dominates)

Space Complexity is typically \\(O(\log_b n)\\) for the recursion stack (the depth of the recursion tree), plus whatever `divide()`/`combine()` allocate at each level.