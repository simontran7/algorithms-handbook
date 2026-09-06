# Introduction to Complexity Analysis

## Best, Worst, and Average Case

There are three running time cases:

- Best-Case: \\(T_best(n) = min{t(x) | x is an input of size n }\\)
- Worst-Case: \\(T_worst(n)\\)
- Average-Case: \\(T_avg(n)\\)

> [!NOTE]
> Best case is is rarely studied since we're interested in the running time on _all_ inputs!

## Asymptotic Notation

The asymptotic notation tells you how tightly/loosely you're bounding that scenario's growth.

### Definition (big O (Micron))

\\(\mathcal{O}(f(n))\\) is the set of functions that grow *at most* as fast as \\(c \dot f(n)\\), for some constant \\(c\\). 
,
If \\(g \in O(f)\\), then we say \\(g\\) is asymptotically **upper bounded** by \\(f\\).

### Definition (big Omega)

\\(\Omega(f(n))\\) is the set of functions that grow *at least* as fast as \\(c \dot f(n)\\), for some constant \\(c\\). 

If \\(g \in \omega(f)\\), then we say \\(g\\) is asymptotically **lower bounded** by \\(f\\).

### Definition (big Theta)

\\(\Theta(f(n)))\\) is the set of functions that grow *as fast* as \\(f(n)\\). 

If \\(g \in O(f)\\) and \\(g \in \omega(f)\\), then \\(g \in \Theta(f)\\), and we say \\(g\\) is asymptotically **tight bounded** by \\(f\\).

> [!WARNING]
> The case and the asymptotic notation are independent choices!

### Simplification Rules

1. Drop constant factors (since we only care about the rate of growth)

\\[
O(c \cdot f(n)) \rightarrow O(f(n))
\\]

3. Drop lower-order terms (since we only care about large inputs)

\\[
O(f(n) + g(n)) \rightarrow O(max(f, g))
\\]

### Laws

#### Law of Addition

\\[
O(f(n)) + O(g(n)) \rightarrow O(f(n) + g(n))
\\]

#### Law of Multiplication

\\[
O(f(n)) \cdot O(g(n)) \rightarrow O(f(n) \cdot g(n))
\\]

### Common Orders of Growth

| Growth type  | Function           |
| ------------ | ------------------ |
| Constant     | \\(1\\)            |
| Logarithmic  | \\(\log n\\)       |
| Linear       | \\(n\\)            |
| Linearithmic | \\(n \log n\\)     |
| Quadratic    | \\(n^2\\)          |
| Cubic        | \\(n^3\\)          |
| Exponential  | \\(2^n\\)          |
| Factorial    | \\(n!\\)           |

> [!NOTE]
> Asymptotic notation does not tell the whole story about how fast a program runs in real life! In real-world applications, constant factor matters, hardware matters, and implementation matters!

