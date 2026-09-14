# Introduction to Complexity Analysis

## Best, Worst, and Average Case

Runtime is usually analyzed based on three different scenarios:
- **Best-Case:** \\(T_{best}(n) = \min\left\lbrace t(x) \;\middle|\; x \text{ is an input of size } n \right\rbrace\\)
- **Worst-Case:** \\(T_{worst}(n) = \max\left\lbrace t(x) \;\middle|\; x \text{ is an input of size } n \right\rbrace\\)
- **Average-Case:** \\(T_{average}(n) = \sum_{x} t(x) \cdot \Pr[x]\\)

> [!NOTE]
> Best case is is rarely studied since we're interested in the runtime for _all_ inputs!

## Asymptotic Notation

The asymptotic notation tells you how tightly/loosely you're bounding that scenario's growth.

### Definition (big O)

\\(O(f(n))\\) is the set of functions that grow *at most* as fast as \\(c \dot f(n)\\), for some constant \\(c\\). 

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

