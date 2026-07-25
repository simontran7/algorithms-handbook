# Dynamic Programming

## Signal

Problems suitable for dynamic programming typically involve making decisions where each choice influences subsequent decisions. Then, the goal is to:

- Optimization problems
- Combinatorial problems
- Feasability problems

## Template

### Step 1: Define a function `dp()`

Define a function `dp()` and determine its return value based on the problem description.

### Step 2: Define the Subproblems

Decide on the relevant state variables (i.e. what parameters it should have). A good way to think about state variables is to imagine if the problem was a real-life scenario, and ask determine what information would you need to describe it in full.

**Common state variables:**

- A primary index \(i\) along an input string, input array, or an implicit range of numbers. This state variable represents the slice in the range \([0, i]\), thereby flowing backwards, or it may represent a slice in the range \([i, N)\), thereby flowing forwards.
- A secondary index \(j\) along an input string or an input array, or an implicit range of numbers. This state variable is often used in conjunction with a primary state variable \(i\) to represent the slice in the range \([i, j]\). It may also simply represent another index into the second input.
- An integer variable to track the remaining amount of moves when there is an imposed problem constraint \(k\).
- A boolean variable to track a status.

> [!NOTE]
> Constants given by the problem should _never_ be state variables!

> [!NOTE]
> The **dimensionality** of a dynamic programming problem is determined by the number of state variables required by a dynamic programming algorithm. We say a problem is a \(1D\) dynamic programming problem when a dynamic programming algorithm only requires one state variable, and when the dynamic programming algorithm requires only two state variables, we call that problem a \(2D\) dynamic programming problem.

### Step 3: Determine the Recurrence Relation

1. Determine the recurrence rule which will involve calls to `dp()`, and typically the `min()` or `max()` function for optimization problems.
2. Determine the base case(s) derived from the problem description.

> [!NOTE]
> A state variable may either flow _forward_ or _backward_:
> - If a state variable flows forward, the recurrence depends on larger values of that variable, and the base case(s) appear at the maximal values.
> - If a state variable flows backward, the recurrence depends on smaller values of that variable, and the base case(s) appear at the minimal values.
>
> In multi-dimensional problems, each variable can have its own flow direction.

### Step 4: Determine the Arguments to the Initial `dp()` Call

The initial `dp()` call will return the result to the overall problem.

The arguments depend on the direction of flow of the state variables:

- If a state variable flows forward, the initial argument will be the minimum value.
- If a state variable flows backwards, the initial argument will be the maximum value.

### Step 5: Produce the Top-Down Solution (Memoization)

```rust
use std::collections::HashMap;

fn dp(<state variables>, memo: &mut HashMap<(<state variable types>), T>) -> T {
    if <state variable> == <value> {
        return <base case value>;
    }

    if let Some(&cached) = memo.get(&(<state variables>)) {
        return cached;
    }

    let result = <recurrence>; // may be more involved

    memo.insert((<state variables>), result);

    result
}

// dp(<initial arguments for the state variables>, &mut HashMap::new())
```

### Step 6: Produce the Bottom-Up Solution (Tabulation)

1. Initialize an array `dp` that is sized according to the subproblem variables largest values. In particular, whenever you have a base case of the form `if i >= n: return <base case value>`, and somewhere else in your algorithm you have `dp(i + x)`, then your array must have `n + x` rows.
2. For every base case `if <state variable> == <value>: return <base case value>`, explicitly set them in the lookup table `dp` i.e., `dp[<state variable>][...] = <base case value>` or implicitly through the initial values of the lookup table.
3. Write for-loop(s) that will iterate over your state variables, such that the outermost for loop iterates the first state variable in the order of the `dp()` parameters, and such that the `range()` should begin from the first _non-base-case_ state variables problems, and end at the final result state variables. For boolean state variables, the range should be from \([0, 2)\). However, for certain matrix problems (e.g., Unique Paths, Minimum Path Sum) where the calculation for a cell `(row, col)` depends only on the results from cells that are above it `(row - 1, col)`, to its left `(row, col - 1)`, or both `(row - 1, col - 1)`, you can iterate through all the rows and columns from top-to-bottom, left-to-right. Within the loop, you use `continue` to skip the base case cells because their values have already been correctly initialized.
4. Under the inner-most for loop, copy-paste _only_ the recurrence logic from your memoization function.
5. Change every `dp(<state variable 1>, <state variable 2>, <...>)` function calls and `result` to array accesses `dp[<state variable 1>][<state variable 2][<...>]`. For boolean state variables, represent `True` as `1` and `False` as `0`.

> [!NOTE]
> We can reduce the space complexity of a bottom-up dynamic programming algorithm whenever the recurrence is static (i.e., it doesn't change between inputs and it only cares about a static number of previous states). Simply replace the lookup table with variables to keep track of those previous states, one rolling variable per dp index you look back at. Additionally, add an aggregation `result` variable (initialized to the first valid base case value) if the answer is the maximum over all states rather than just the final state `dp[n - 1]`. This happens when the recurrence can produce values smaller than a previous state, meaning the peak may not be at the end.

## Complexity Analysis

$$
O(P \cdot C)
$$

- \(P\): number of subproblems (product of the ranges of each subproblem variable)
- \(C\): cost of processing a single subproblem

