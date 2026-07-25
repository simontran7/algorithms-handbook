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