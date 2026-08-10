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

An ordered map/set is a superset of the [Map and Set](/notes/algorithm-techniques/map-and-set) ADT: it supports everything a regular map/set does, as well as operations that depend on keys being sorted:

- Iterating over keys in sorted order without sorting them yourself
- Finding the minimum or maximum key
- Range queries: all keys/entries between a lower and upper bound

## Binary Search Tree

...

## Red-Black Tree

...

## B-Tree

A **B-tree** generalizes a binary search tree by letting each node hold *multiple* sorted keys (up to some maximum determined by the tree's **order**) and correspondingly more children, one more than it has keys. This wide branching factor keeps the tree very shallow, which matters most when each node access is expensive (e.g., a disk read in a database or filesystem index): a shallow tree means far fewer accesses to reach any key.

### Lookup

Within a node, search its sorted keys for a match or for the two keys the target falls between; if no match, descend into the child between them and repeat, until a match is found or a leaf is reached without one.

### Insertion

Descend to the correct leaf as in a lookup and insert the key into that leaf's sorted key list. If the leaf now holds more keys than the maximum, split it in two around its median key and push that median up into the parent; if the parent overflows too, the split propagates upward, and if it reaches the root, the tree grows one level taller.

### Deletion

Locate the key. If it's in a leaf, remove it directly, then rebalance if the leaf now holds too few keys, either by borrowing a key from an adjacent sibling or merging with one. If it's in an internal node, swap it with its in-order predecessor or successor (which lives in a leaf), then remove it from there instead.

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Lookup | worst-case \\(O(\log n)\\) |
| Insertion | worst-case \\(O(\log n)\\) |
| Deletion | worst-case \\(O(\log n)\\) |

> [!NOTE]
> A B-tree's \\(O(\log n)\\) has a much larger logarithm base (the branching factor) than a binary tree's, so in practice its height, and therefore the number of node accesses per operation, is far smaller. This is precisely why B-trees are the standard choice for on-disk structures like database indexes, where minimizing the number of expensive disk reads matters more than the constant-factor cost of scanning within a node.

## Trie (Prefix Tree)

A **trie (prefix tree)** stores string keys not as a whole, but character by character down a tree: each node holds a map from character to child node, and a path from the root spells out a prefix. A node is marked as the end of a complete key so lookups can distinguish a stored word from a prefix that just happens to lead through it. This structure is especially suited to string matching problems: autocomplete, spell checking, and prefix search all reduce to walking the trie a few characters at a time instead of scanning every stored string.

### Lookup

Walk down from the root one character at a time, following the child edge matching each character of the target key. If any character has no matching child, the key isn't present. If the walk completes, check whether the final node is marked as a complete key (for an exact match) or just return true (for a prefix check).

### Insertion

Walk down from the root one character at a time, creating a new child node whenever the next character doesn't already have one. Once the last character is placed, mark that final node as the end of a key.

### Deletion

Walk down to the node for the target key as in a lookup, then unmark it as the end of a key. If that node (and any of its ancestors, walking back up) is left with no children and isn't the end of some other key, it's now dead weight and can be pruned from the tree.

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Lookup | worst-case \\(O(m)\\), where \\(m\\) is the length of the key |
| Add | worst-case \\(O(m)\\), where \\(m\\) is the length of the key |
| Remove | worst-case \\(O(m)\\), where \\(m\\) is the length of the key |

## API

### Ordered Map

```cpp
#include <map>

// Create an empty ordered map
std::map<int, int> ordered_map;

// Get the value for a key (inserts default if absent!)
ordered_map[key];

// Get the value for a key without inserting
ordered_map.at(key);

// Check if a key exists
ordered_map.count(key);

// Add / update a key-value pair
ordered_map[key] = value;

// Remove a key
ordered_map.erase(key);

// Get the number of entries
ordered_map.size();

// Check if the ordered map is empty
ordered_map.empty();

// Get the minimum key-value pair
*ordered_map.begin();       // .first is the key, .second is the value

// Get the maximum key-value pair
*ordered_map.rbegin();

// Get an iterator to the first entry with key >= `target`
ordered_map.lower_bound(target);

// Get an iterator to the first entry with key > `target`
ordered_map.upper_bound(target);

// Range query: iterate over all entries with start <= key < end
for (auto it = ordered_map.lower_bound(start); it != ordered_map.lower_bound(end); ++it) {
    // key, value = it->first, it->second
}

// Iterate over all entries in sorted key order
for (const auto& [key, value] : ordered_map) {
    // ...
}
```

### Ordered Set

```cpp
#include <set>

// Create an empty ordered set
std::set<int> ordered_set;

// Add an element
ordered_set.insert(element);

// Check if an element exists
ordered_set.count(element);

// Remove an element
ordered_set.erase(element);

// Get the number of elements
ordered_set.size();

// Check if the ordered set is empty
ordered_set.empty();

// Get the minimum element
*ordered_set.begin();

// Get the maximum element
*ordered_set.rbegin();

// Get an iterator to the first element >= `target`
ordered_set.lower_bound(target);

// Get an iterator to the first element > `target`
ordered_set.upper_bound(target);

// Range query: iterate over all elements with start <= element < end
for (auto it = ordered_set.lower_bound(start); it != ordered_set.lower_bound(end); ++it) {
    // *it is the element
}

// Iterate over all elements in sorted order
for (int element : ordered_set) {
    // ...
}
```

> [!NOTE]
> `lower_bound`/`upper_bound` return **iterators**, which may be `end()` if no such element exists — always check before dereferencing: `auto it = ordered_set.lower_bound(target); if (it != ordered_set.end()) { ... }`. To find the rightmost element `< target`, use `lower_bound` and step back: `if (it != ordered_set.begin()) { int value = *prev(it); }`.

> [!NOTE]
> For duplicate elements, use a `std::multiset` (bag ADT). `std::multiset` also doubles as a "sorted sliding window", where `*ms.begin()` and `*ms.rbegin()` give the window's min and max simultaneously. However, a footgun is `multiset.erase(value)`, which removes *all* copies of `value`. to remove just one, erase by iterator: `multiset.erase(multiset.find(value))`. 

### `TrieSet`

```cpp
class TrieNode {
public:
    int data;
    std::unordered_map<char, TrieNode*> children;

    TrieNode() : data(0) {}
};

TrieNode* from(const std::vector<std::string>& words) {
    TrieNode* root = new TrieNode();

    for (const std::string& word : words) {
        TrieNode* current = root;
        for (char c : word) {
            if (!current->children.count(c)) {
                current->children[c] = new TrieNode();
            }
            current = current->children[c];
        }
        // Some logic (you have a full word at `current`).
    }

    return root;
}
```s