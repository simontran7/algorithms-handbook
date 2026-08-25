# Complexity Analysis

## Bachmann-Landau Notation

### Definition (big O)

Let $f(n)$ and $g(n)$ be functions mapping positive integers to positive real numbers. We say that $f(n)$ is $O(g(n))$ if there is a real constant $c \gt 0$ and an integer constant $n_0 \ge 1$ such that:

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

| Growth type  | Function           |
| ------------ | ------------------ |
| Constant     | $1$            |
| Logarithmic  | $\log n$       |
| Linear       | $n$            |
| Linearithmic | $n \log n$     |
| Quadratic    | $n^2$          |
| Cubic        | $n^3$          |
| Exponential  | $2^n$          |
| Factorial    | $n!$           |

## Worst-case Time Complexity

### Calculating the Worst Case

1. Identify the input parameters that influence running time and assign variables (commonly $n$, $m$, $k$, etc.).
2. Break the algorithm into significant parts
3. Assign a cost to each part based on the following methods
4. Combine the costs of sequential parts using the law of addition, and nested parts using the law of multiplication
5. Simplify using the simplification rules

### Primitive Operations

The following primitive operations are worst-case $O(1)$:
- Assigning a value to a variable
- Accessing an element by index or field
- Performing an arithmetic, comparison, or bitwise operation
- Calling or returning from a function

### Iterative Loops Algorithms

1. Identify the **loop variant** of the outermost loop or recursion: the quantity that changes by a predictable amount each iteration/level and has known start and end values. For `for` loops, this is the loop variable itself; for `while` loops, find or invent it (e.g., the gap `right - left` in a two-pointer loop, the search space size in binary search); for recursion, it is the recursion level.
2. For every possible value of the loop variant, determine the cost of one iteration/level as a function of that variant.
3. Sum those costs and express the result as a summation matching the LHS of one of the following formulas, applying properties as needed to massage it into the right form
4. Substitute the RHS of the matching formula to get a closed form, then apply Bachmann-Landau rules to simplify to asymptotic complexity

> [!NOTE]
> For step 2, for fixed-limit formulas, if the upper limit does not match the standard formula (e.g. $\sum_{i=0}^{n-1}$ instead of $\sum_{i=1}^{n}$), substitute the upper limit into the formula in place of $n$. However, if the lower limit doesn't match the fixed-limit formula, there are two approaches. If the lower limit is larger than that of the fixed formula, then your sum is missing terms compared to the formula's sum, so you compute the full sum and subtract the prefix you don't want (e.g., $\sum_{i=3}^{n} i = \sum_{i=1}^{n} i - \sum_{i=1}^{2} i = \frac{n(n+1)}{2} - 3$). If the lower limit is smaller than that of the fixed formula, then your sum has extra terms compared to the formula's sum, so you compute the formula's sum and add the extras manually (e.g., $\sum_{i=0}^{n} i = 0 + \sum_{i=1}^{n} i = \frac{n(n+1)}{2}$).

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

#### Formula (summation of a $1$)

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

#### Formula ($i^k$ series)

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

#### Formula ($\log_{2}$ series)

$$
\sum_{i = 1}^{n} \log_2 i = O\left(\sum_{i = 1}^{n} \log_2 n\right) = O(n\log_2 n)
$$

### Recursive Algorithms (Recursion Tree Method)

To determine the worst-case time complexity of a recursive algorithm, we are concerned with determining the total number of function calls multiplied by the work done per function call.

We can determine the total number of functions calls by drawing out the **recursion tree**. The recursion tree is an tree that is used to denote the execution flow of the recursive algorithm in question:
- Each node represents a recursive call
- the branching factor $b$ is determined by the number of recursive calls in the recursive case (of the recurrence relation)

1. Draw out the recursion tree

2. Determine the branching factor $b$.

3. Figure out the work done per node at level $k$ $W(k)$ which is a function of the subproblem size at that level $k$
    - If dividing by $b$ each time: $W(k) = \frac{n}{b^k}$
    - If decrementing by 1 each time: $W(k) = n - k$
    - If work per node doesn't depend on the subproblem size: $O(1)$

4. Figure out the number of levels $d$

5. Plug into the formula

$$
\sum_{k=0}^{d} W(k) \cdot b^k
$$

## Amortized Time Complexity (Aggregate Method)

1. Identify the resource whose movement drives the inner loop's cost (e.g., a pointer, a counter, a stack's size).
2. Verify the resource is **monotonic** (i.e., resource never gets refilled, or each step refills at most a constant amount) and **globally bounded** (i.e., cannot exceed some value $B$ over the entire run).
3. Conclude that the inner loop body executes at most $B$ times *in total across all outer iterations*.

## Worst-case Space Complexity

- Integers: $O(1)$
- Array based collection or pointer based collection: $O(n)$, where $n$ is the number of elements
- Collection of collection: $O(\text{outer collection size} \times \text{inner collection size})$
- Adjacency List: $O(V + E)$, where $V$ is the number of vertices, and $E$ is the number of edges
- Call Stack: $O(d \cdot F)$, where $d$ is maximum recursion depth, and $F$ is the memory consumed per stack frame

<img width="500" src="https://github.com/user-attachments/assets/00f45c72-e91a-48ee-a4fc-13b9c7e52613" />

### Optimizing Space Complexity

- Whenever the problem space is predetermined (e.g. we know there are vertices from `0` to `n - 1`), you might be able to use a static array of booleans instead of a hashset or a hashmap.

> [!NOTE]
> In interviews, the algorithm's input *and* output is typically excluded from the total space complexity cost, and only the auxiliary space is considered.
