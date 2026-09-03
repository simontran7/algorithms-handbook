# Disjoint Set (Union-Find)

## Abstract Data Type

```
trait DisjointSet {
    func new(n: usize) -> Self;
    func union(&mut self, x: UInt, y: UInt) -> Bool;
    func find(&mut self, x: UInt) -> UInt;
}
```

## Use Case

- Detect and track connected components 
- Detect cycles in undirected graphs
- Enforce grouping constraints 

## Forest (with Path Compression & Union by Rank)

### Implementation

```python
class DisjointSet:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n

    def find(self, x):
        while self.parent[x] != x:
            self.parent[x] = self.parent[self.parent[x]]
            x = self.parent[x]
        return x

    def union(self, x, y):
        x_rep = self.find(x)
        y_rep = self.find(y)

        if x_rep == y_rep:
            return False

        if self.rank[x_rep] < self.rank[y_rep]:
            self.parent[x_rep] = y_rep
        elif self.rank[x_rep] > self.rank[y_rep]:
            self.parent[y_rep] = x_rep
        else:
            self.parent[y_rep] = x_rep
            self.rank[x_rep] += 1

        return True
```

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Initialize | worst-case \\(O(n)\\) |
| Find | worst-case \\(O(\log n)\\), but amortized \\(O(\alpha(n))\\) |
| Union | worst-case \\(O(\log n)\\), but amortized \\(O(\alpha(n))\\) |

