# Disjoint Set (Union-Find)

## Interface

```
trait DisjointSet {
    func new(n: usize) -> Self;
    func union(&mut self, x: usize, y: usize) -> bool;
    func find(&mut self, x: usize) -> usize;
}
```

## Use Case

- Detect and track connected components (static graphs or as edges are added dynamically)
- Detect cycles in undirected graphs
- Enforce grouping constraints (union nodes that must belong together, then validate)

## Forest (with Path Compression & Union by Rank)

### Implementation

```cpp
class DisjointSet {
private:
    std::vector<int> parent;
    std::vector<int> rank_;

public:
    DisjointSet(int n) : parent(n), rank_(n, 0) {
        std::iota(parent.begin(), parent.end(), 0);
    }

    int find(int x) {
        while (parent[x] != x) {
            parent[x] = parent[parent[x]];
            x = parent[x];
        }
        return x;
    }

    bool unite(int x, int y) {
        int x_rep = find(x);
        int y_rep = find(y);

        if (x_rep == y_rep) {
            return false;
        }

        if (rank_[x_rep] < rank_[y_rep]) {
            parent[x_rep] = y_rep;
        } else if (rank_[x_rep] > rank_[y_rep]) {
            parent[y_rep] = x_rep;
        } else {
            parent[y_rep] = x_rep;
            rank_[x_rep]++;
        }

        return true;
    }
};
```

> [!NOTE]
> Sometimes, you may need to augment the Disjoint Set to a relational Disjoint Set by storing extra data along parent pointers to propagate edge weights or relations.

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Initialize | worst-case \\(O(n)\\) |
| Find | worst-case \\(O(\log n)\\), but amortized \\(O(\alpha(n))\\) |
| Union | worst-case \\(O(\log n)\\), but amortized \\(O(\alpha(n))\\) |

