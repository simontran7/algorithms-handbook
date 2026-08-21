# Ordered Map and Ordered Set

## Interface

### Ordered Map

```
trait OrderedMap<K: Ord, V> {
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
trait OrderedSet<T: Ord> {
    func add(&mut self, item: T);
    func contains(&self, item: T) -> Bool;
    func remove(&mut self, item: T);
    func min(&self) -> T;
    func max(&self) -> T;
    func range(&self, start: T, end: T) -> impl Iterator<Item = T>;
}
```

## Use Case

- Iterating over keys in sorted order without sorting them yourself
- Finding the minimum or maximum key
- Range queries

## Binary Search Tree

### Implementation

```python
```

### Complexity Analysis

...

## Red-Black Tree

### Implementation

```python
```

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Lookup | worst-case \\(O(\log n)\\) |
| Insertion | worst-case \\(O(\log n)\\) |
| Deletion | worst-case \\(O(\log n)\\) |

## Prefix Tree (Trie)

### Implementation

```python
class TrieNode:
    def __init__(self):
        self.data = None
        self.children = {}

class TrieMap:
    def __init__(self, words=None):
        self.root = TrieNode()
        for word, value in (words or []):
            self.add(word, value)

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

        should_delete_child = self._remove_rec(node.children[c], word, index + 1)
        if should_delete_child:
            del node.children[c]
            return not node.children and node.data is None
        return False
```

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Lookup | worst-case $O(m)$, where $m$ is the length of the key |
| Add | worst-case $O(m)$, where $m$ is the length of the key |
| Remove | worst-case $O(m)$, where $m$ is the length of the key |

