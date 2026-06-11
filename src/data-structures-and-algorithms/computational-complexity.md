# Computational Complexity

## Bachmann-Landau Notation

### Definition (big O)

Let \\(f(n)\\) and \\(g(n)\\) be functions mapping positive integers to positive real numbers. We say that \\(f(n)\\) is \\(O(g(n))\\) if there is a real constant \\(c \gt 0\\) and an integer constant \\(n_0 \ge 1\\) such that:
$$
f(n) \leq c \cdot g(n), \text{ for } n \geq n_0
$$

### Simplification Rules

1. Drop constant factors

$$
O(c \cdot f(n)) \rightarrow O(f(n))
$$

3. Drop lower-order terms

$$
O(f(n) + g(n)) \rightarrow O(max(f, g))
$$

### Laws

#### Law of Addition

$$
O(f(n)) + O(g(n)) \rightarrow O(f(n) + g(n))
$$

#### Law of Multiplication

$$
O(f(n)) \cdot O(g(n)) \rightarrow O(f(n) \cdot g(n))
$$

### Common Orders of Growth

| Growth type  | Function       |
| ------------ | ------------   |
| Constant     | \\(1\\)            |
| Logarithmic  | \\(\log n\\)       |
| Linear       | \\(n\\)            |
| Linearithmic | \\(n \log n\\)     |
| Quadratic    | \\(n^2\\)          |
| Cubic        | \\(n^3\\)          |
| Exponential  | \\(2^n\\)          |
| Factorial    | \\(n!\\)           |

## Worst-case Time Complexity

### Calculating the Worst Case

1. Identify the input parameters that influence running time and assign variables (commonly \\(n\\), \\(m\\), \\(k\\), etc.).
2. Break the algorithm into significant parts
3. Assign a cost to each part based on the following methods
4. Combine the costs of sequential parts using the law of addition, and nested parts using the law of multiplication
5. Simplify using the simplification rules

> [!NOTE]
> Lowercase variables (\\(n\\), \\(m\\), \\(k\\)) are generic placeholders. Uppercase variables (\\(V\\), \\(E\\), \\(S\\), \\(C\\), etc.) are named placeholders with a specific meaning in context.

### Primitive Operations

The following primitive operations are worst-case \\(O(1)\\):
- Assigning a value to a variable
- Accessing an element by index or field
- Performing an arithmetic or comparison operation
- Calling or returning from a function

### Iterative Loops Algorithms

1. Identify the **loop variant** of the outermost loop or recursion: the quantity that changes by a predictable amount each iteration/level and has known start and end values. For `for` loops, this is the loop variable itself; for `while` loops, find or invent it (e.g., the gap `right - left` in a two-pointer loop, the search space size in binary search); for recursion, it is the recursion level.
2. For every possible value of the loop variant, determine the cost of one iteration/level as a function of that variant.
3. Sum those costs and express the result as a summation matching the LHS of one of the following formulas, applying properties as needed to massage it into the right form
4. Substitute the RHS of the matching formula to get a closed form, then apply Bachmann-Landau rules to simplify to asymptotic complexity

> [!NOTE]
> Use **amortized analysis** when an operation is sometimes cheap and sometimes expensive. To check, look for a resource that each expensive iteration uses up (e.g., a pointer moving forward, an element popped off a stack) and verify both criteria:
> 1. Capped: over the entire run, there is a hard limit \(B\) on how much can ever be spent.
> 2. Stays spent: the resource never gets refilled, or each step refills at most a constant amount (e.g., one push per loop iteration).
>
> If both hold, the expensive code runs at most \(B\) times total, no matter how those runs are spread out across iterations. So,  count its cost once, globally, instead of multiplying it by the outer loop.

> [!NOTE]
> For step 2, for fixed-limit formulas, if the upper limit does not match the standard formula (e.g. \\(\sum_{i=0}^{n-1}\\) instead of \\(\sum_{i=1}^{n}\\)), substitute the upper limit into the formula in place of \\(n\\). However, if the lower limit doesn't match the fixed-limit formula, there are two approaches. If the lower limit is larger than that of the fixed formula, then your sum is missing terms compared to the formula's sum, so you compute the full sum and subtract the prefix you don't want (e.g., \\(\sum_{i=3}^{n} i = \sum_{i=1}^{n} i - \sum_{i=1}^{2} i = \frac{n(n+1)}{2} - 3\\)). If the lower limit is smaller than that of the fixed formula, then your sum has extra terms compared to the formula's sum, so you compute the formula's sum and add the extras manually (e.g., \\(\sum_{i=0}^{n} i = 0 + \sum_{i=1}^{n} i = \frac{n(n+1)}{2}\\)).

#### Property (big O and summation)

$$
\sum_{i \in I} O(f(i)) = O\left(\sum_{i \in I} f(i)\right)
$$

#### Property (summation of a constant)

$$
\sum_{i = m}^{n} ca_i = c \sum_{i = m}^{n} a_i
$$

#### Property (addition and subtraction of summations)

$$
\sum_{i = m}^{n} (a_i \pm b_i) = \sum_{i = m}^{n} a_i \pm \sum_{i = m}^{n} b_i
$$

#### Formula (summation of a \\(1\\))

$$
\sum_{i = m}^{n} 1 = n - m + 1
$$

#### Formula (arithmetic series)

$$
\sum_{i = 1}^{n} i = \frac{n(n + 1)}{2}
$$

#### Formula (sum of squares)

$$
\sum_{i = 1}^{n} i^2 = \frac{n(n + 1)(2n + 1)}{6}
$$

#### Formula (cubic series)

$$
\sum_{i = 1}^{n} i^3 = \left(\frac{n(n + 1)}{2}\right)^2
$$

#### Formula (\\(i^k\\) series)

$$
\sum_{i = 1}^{n} i^k \approx \frac{1}{k + 1}n^{k + 1}
$$

#### Formula (geometric series)

$$
\sum_{k = 0}^{n}r^k = \frac{r^{n + 1} - 1}{r - 1}, \text{ where } r > 0 \text{ and } r \neq 1
$$

#### Formula (harmonic series)

$$
\sum_{i = 1}^{n} \frac{1}{i} \approx \ln n + \gamma, \text{ where } \gamma \approx 0.5772 \dots
$$

#### Formula (\\(\log_{2}\\) series)

$$
\sum_{i = 1}^{n} \log_2 i = O\left(\sum_{i = 1}^{n} \log_2 n\right) = O(n\log_2 n)
$$

### Binary Tree Algorithms

$$
O(n \cdot C_{node})
$$

- \\(n\\): number of nodes in the binary tree
- \\(C_{node}\\): cost of processing a single node

### Graph Traversal Algorithms

$$
O(S \cdot C_{state} + T \cdot C_{transition})
$$

- \\(S\\): number of reachable states (product of the ranges of each state variable)
- \\(C_{state}\\): cost of processing a single state
- \\(T\\): number of transitions (the transitions per state times S)
- \\(C_{transition}\\): cost of processing a single transition

### Recursive Algorithms

#### Master Theorem Method

$$
T(n) = aT(\frac{n}{b}) + f(n)
$$

#### Recursion Tree Method

1. Draw out the recursion tree

2. Figure out the branching factor (i.e., determine \\(b\\)) by counting the number of recursive calls the function makes.

3. Figure out the work done per node at level \\(k\\) (i.e., determine \\(W(k)\\)) which is usually a function of the subproblem size at that level \\(k\\)
    - If dividing by \\(b\\) each time: \\(W(k) = \frac{n}{b^k}\\)
    - If decrementing by 1 each time: \\(W(k) = n - k\\)
    - If work per node doesn't depend on the subproblem size: \\(O(1)\\)

4. Figure out the number of levels (i.e., determine \\(L\\)) by asking "how many times do I apply the shrinking operation before hitting the base case?"

5. Plug into the formula

$$
\sum_{k=0}^{L} W(k) \cdot b^k
$$

> [!NOTE]
> If \\(W(k) = O(1)\\) at every level and \\(b \geq 2\\), we can use the shorter formula \\(O(b^{L+1})\\) instead.

### Binary Search Algorithms

$$
O(\log⁡ n)
$$

- \\(n\\): size of your initial search space

### Topological Sorting Algorithms

#### Kahn's Algorithm

$$
O(V + E)
$$

- \\(V\\): number of vertices
- \\(E\\): number of edges

### MST Detection Algorithms

#### Kruskal's Algorithm

$$
O(E \log E) + O(E \alpha(V)) = O(E \log E)
$$

- \\(V\\): number of vertices
- \\(E\\): number of edges

#### Prim's Algorithm

$$
O(V + E) \cdot O(\log V) = O(E \cdot \log V)
$$

- \\(V\\): number of vertices
- \\(E\\): number of edges

> [!NOTE]
> Common values of \\(E\\) in the classic graph algorithms worst-case time complexity formulas:
> - Complete graph: \\(E = \binom{n}{2} = \frac{N(N - 1)}{2}\\)
> - Tree: \\(E = V − 1\\)
> - Dense graph: \\(E = O(V^2)\\)
> - Sparse graph: \\(E =O(V)\\)

### Backtracking Algorithms

$$
O(S \cdot C)
$$

- \\(S\\): number of possible states explored
- \\(C\\): cost of processing a single state

> [!NOTE]
> Common values of \\(S\\) in the backtracking algorithm worst-case time complexity formula:
> - Combinations of \\(k\\) from \\(n\\): \\(\binom{n}{k}\\)
> - Permutations of from \\(n\\): \\(\frac{n!}{(n - k)!}\\)
> - Generic tree with branching factor \\(b\\) and depth \\(d\\): \\(b^d\\)

### Dynamic Programming Algorithms

$$
O(P \cdot C)
$$

- \\(P\\): number of subproblems (product of the ranges of each subproblem variable)
- \\(C\\): cost of processing a single subproblem

### Dynamic Array Operations

| Operation | Time Complexity |
| --- | --- |
| Add at the end | worst-case \\(O(n)\\), but amortized \\(O(1)\\)  |
| Add at the front | worst-case \\(O(n)\\) |
| Add in the middle | worst-case \\(O(n)\\) |
| Lookup by index | worst-case \\(O(1)\\) |
| Remove at the end | worst-case \\(O(1)\\) |
| Remove at the front | worst-case \\(O(n)\\) |
| Remove in the middle | worst-case \\(O(n)\\) |

### Hash Table Operations

| Operation | Time Complexity |
| --- | --- |
| Lookup | worst-case \\(O(n)\\), but average \\(O(1)\\) |
| Add | worst-case \\(O(n)\\), but amortized \\(O(1)\\) |
| Remove | worst-case \\(O(n)\\), but average \\(O(1)\\) |

### Binary Heap Operations

| Operation | Time Complexity |
| --- | --- |
| Initialize | worst-case \\(O(n)\\) |
| Lookup min/max | worst-case \\(O(1)\\) |
| Add    | worst-case \\(O(\log n)\\) |
| Remove | worst-case \\(O(\log n)\\) |

### Prefix Tree Operations

| Operation | Time Complexity |
| --- | --- |
| Lookup | worst-case \\(O(m)\\) |
| Add | worst-case \\(O(m)\\) |

### Forest (with path compression + union by rank) Operations

| Operation | Time Complexity |
| --- | --- |
| Initialize | worst-case \\(O(n)\\) |
| Lookup    | worst-case \\(O(\log n)\\), but amortized \\(O(\alpha(n))\\) |
| Merge    | worst-case \\(O(\log n)\\), but amortized \\(O(\alpha(n))\\) |

## Amortized Time Complexity (Aggregate Method)

1. Identify the quantity whose movement drives the inner loop's cost (e.g., a pointer, a counter, a stack's size).
2. Verify the quantity is **monotonic** (only moves one direction) and **globally bounded** (cannot exceed some value \\(B\\) over the entire run).
3. Conclude the inner loop body executes at most \\(B\\) times *in total across all outer iterations*, so total cost is \\(O(\text{outer loop cost}) + O(B \cdot \text{inner body cost})\\).

## Worst-case Space Complexity

- Variable: \\(O(1)\\)
- Array based collection or pointer based collection: \\(O(n)\\), where \\(n\\) is the number of elements
- Collection of collection: \\(O(\text{outer collection size} \times \text{inner collection size})\\)
- Adjacency List: \\(O(V + E)\\), where \\(V\\) is the number of vertices, and \\(E\\) is the number of edges
- Call Stack: \\(O(D \cdot F)\\), where \\(D\\) is maximum recursion depth, and \\(F\\) is the memory call per stack frame

> [!NOTE]
> The algorithm's input *and* output is typically excluded from the total space complexity cost. Space complexity is only concerned with auxiliary memory.
