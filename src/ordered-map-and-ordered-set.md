# Ordered Map and Ordered Set

## Abstract Data Type

### Ordered Map

```
trait OrderedMap[K: Order, V] {
    func get(&self, key: K) -> V;
    func add(&mut self, key: K, value: V);
    func remove(&mut self, key: K) -> V;
    func min(&self) -> (K, V);
    func max(&self) -> (K, V);
    func range(&self, start: K, end: K) -> impl Iterator<Item = (K, V)>;
}
```

### Ordered Set

```
trait OrderedSet[E: Order] {
    func add(&mut self, element: E);
    func contains(&self, element: E) -> Bool;
    func remove(&mut self, element: E);
    func min(&self) -> E;
    func max(&self) -> E;
    func range(&self, start: E, end: E) -> impl Iterator<Item = E>;
}
```

## Use Case

- Iterating over keys in sorted order without sorting them yourself
- Finding the minimum or maximum key
- Range queries

## Binary Search Tree

- At level $d$, there are at most $2^d$ nodes.
- A binary tree with $n$ levels has $2^n - 1$ nodes
- A binary tree with height $h$ has 2^{h + 1} - 1$ nodes
- Height of a complete binary tree is $\floor{\log_{2} n}$
- A binary tree with $n$ nodes has $n$ - 1 edges
- A full binary tree has $\text{internal nodes} + 1$ leaves
- A full binary tree has $2 \times \text{internal nodes} + 1$ nodes, or equivalently, $2 \times \text{internal leaves} + 1$

### Lookup

[Exercise](https://leetcode.com/problems/search-in-a-binary-search-tree/description/)

### Insertion

[Exercise](https://leetcode.com/problems/insert-into-a-binary-search-tree/description/)

### Deletion

[Exercise](https://leetcode.com/problems/delete-node-in-a-bst/description/)

### Implementation

```python
```

### Complexity Analysis

...

## Red-Black Tree

> [!NOTE]
> The height of a balanced binary search tree's is $O(\log n)$

### Implementation

```python
```

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Lookup | worst-case $O(\log n)$ |
| Insertion | worst-case $O(\log n)$ |
| Deletion | worst-case $O(\log n)$ |

## Prefix Tree (Trie)

### Implementation

```python
class TrieNode:
    def __init__(self):
        self.data = None
        self.children = {}


class TrieMap:
    def __init__(self):
        self.root = TrieNode()

    @classmethod
    def from_pairs(cls, pairs):
        trie = cls()
        for word, value in pairs:
            trie.add(word, value)
        return trie

    def get(self, word):
        cursor = self.root
        for c in word:
            if c not in cursor.children:
                return None
            cursor = cursor.children[c]
        return cursor.data

    def add(self, word, value):
        cursor = self.root
        for c in word:
            if c not in cursor.children:
                cursor.children[c] = TrieNode()
            cursor = cursor.children[c]
        cursor.data = value

    def remove(self, word):
        return self._remove_rec(self.root, word, 0)

    def _remove_rec(self, node, word, index):
        if index == len(word):
            if node.data is None:
                return False

            node.data = None
            return not node.children

        c = word[index]
        if c not in node.children:
            return False

        should_delete_child = self._remove_rec(
            node.children[c], word, index + 1
        )

        if should_delete_child:
            del node.children[c]
            return not node.children and node.data is None

        return False
```

### Complexity Analysis

Let $m$ be the length of the key. Then:

| Operation | Time Complexity |
| --- | --- |
| Lookup | worst-case $O(m)$ |
| Insertion | worst-case $O(m)$ |
| Deletion | worst-case $O(m)$ |

