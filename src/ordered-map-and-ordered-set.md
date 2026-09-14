# Ordered Map and Ordered Set

## Abstract Data Type

### Ordered Map

| Operation          | Description                                                                           |
| ------------------ | ------------------------------------------------------------------------------------- |
| `get(key)`         | Returns the value corresponding to a given key in the ordered map.                 |
| `add(key, value)`  | Inserts a new key-value pair into the ordered map.                                    |
| `remove(key)`      | Removes the key-value pair with the given key from the ordered map.                |
| `min()`            | Returns the minimum key-value pair in the ordered map.                                |
| `max()`            | Returns the maximum key-value pair from the ordered map.                              |
| `successor(key)`   | Returns the smallest key-value pair with a key greater than `key` in the ordered map. |
| `predecessor(key)` | Returns the largest key-value pair with a key less than `key` in the ordered map.     |

### Ordered Set

| Operation          | Description                                                                           |
| ------------------ | ------------------------------------------------------------------------------------- |
| `contains(<element>)`    | Returns whether `element` exists in the ordered set.                           |
| `add(<element>)`  | Inserts an element into the ordered set.                                    |
| `remove(<element>)`      | Removes `element` from the ordered set.                |
| `min()`            | Returns the minimum element in the ordered set.                                |
| `max()`            | Returns the maximum element in the ordered set.                              |
| `successor(<element>)`   | Returns the smallest element greater than `element` in the ordered set. |
| `predecessor(<element>)` | Returns the largest element less than `element` in the ordered set.     |

## Use Case

- Iterating over keys in sorted order without sorting them yourself
- Range queries

## Red-Black Tree

### Tree Properties

- In a binary tree, a level \\(d\\) has at most \\(2^d\\) nodes.
- A binary tree with \\(n\\) levels has \\(2^n - 1\\) nodes.
- A binary tree with height \\(h\\) has \\(2^{h + 1} - 1\\) nodes.
- A binary tree with \\(n\\) nodes has \\(n\\) - 1 edges.
- A complete binary tree has at most \\(\lceil{\frac{n}{2}}\rceil\\) leaves.
- The height \\(h\\) of a complete binary tree is \\(\lfloor{\log_{2} n}\rfloor\\).
- The height \\(h\\) of a balanced binary search tree is \\(\log n\\).
- A full binary tree has \\(\text{internal nodes} + 1\\) leaves.
- A full binary tree has \\(2 \times \text{internal nodes} + 1\\) nodes, or equivalently, \\(2 \cdot \text{internal leaves} + 1\\)

### Lookup

### Insertion

### Deletion

### Complexity Analysis

| Operation | Time Complexity   |
| --------- | ----------------- |
| Lookup    | worst-case \\(O(\log n)\\) |
| Insertion | worst-case \\(O(\log n)\\) |
| Deletion  | worst-case \\(O(\log n)\\) |

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

| Operation | Time Complexity |
| --- | --- |
| Lookup | worst-case \\(O(m)\\) |
| Insertion | worst-case \\(O(m)\\) |
| Deletion | worst-case \\(O(m)\\) |

