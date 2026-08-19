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

```cpp
```

### Complexity Analysis

...

## Red-Black Tree

### Implementation

```cpp
```

### Standard Library API 

#### Ordered Map

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
*ordered_map.begin(); // .first is the key, .second is the value

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

#### Ordered Set

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
> For duplicate elements, use a `std::multiset`. `std::multiset` also doubles as a "sorted sliding window", where `*ms.begin()` and `*ms.rbegin()` give the window's min and max simultaneously. However, a footgun is `multiset.erase(<value>)`, which removes *all* copies of `value`. To remove just one, erase by iterator: `multiset.erase(multiset.find(<value>))`. 

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Lookup | worst-case $O(\log n)$ |
| Insertion | worst-case $O(\log n)$ |
| Deletion | worst-case $O(\log n)$ |

## Prefix Tree (Trie)

### Implementation

```cpp
template<typename T>
class TrieMap {
public:
    TrieMap() : root(new TrieNode()) {}

    TrieMap(const std::vector<std::pair<std::string, T>>& words) : root(new TrieNode()) {
        for (const auto& [word, value] : words) {
            add(word, value);
        }
    }

    std::optional<T> get(const std::string& word) const {
        TrieNode* cursor = root;
        for (char c : word) {
            if (!cursor->children.count(c)) {
                return std::nullopt;
            }
            cursor = cursor->children[c];
        }
        return cursor->data;
    }

    void add(const std::string& word, const T& value) {
        TrieNode* cursor = root;
        for (char c : word) {
            if (!cursor->children.count(c)) {
                cursor->children[c] = new TrieNode();
            }
            cursor = cursor->children[c];
        }
        cursor->data = value;
    }

    bool remove(const std::string& word) {
        return remove_rec(root, word, 0);
    }

    ~TrieMap() {
        delete_node(root);
    }

private:
    struct TrieNode {
        std::optional<T> data;
        std::unordered_map<char, TrieNode*> children;
        TrieNode() : data(std::nullopt) {}
    };

    TrieNode* root;

    bool remove_rec(TrieNode* node, const std::string& word, int index) {
        if (index == word.size()) {
            if (!node->data.has_value()) {
                return false;
            }
            node->data = std::nullopt;
            return node->children.empty();
        }

        char c = word[index];
        if (!node->children.count(c)) {
            return false;
        }

        bool should_delete_child = remove_rec(node->children[c], word, index + 1);
        if (should_delete_child) {
            delete node->children[c];
            node->children.erase(c);
            return node->children.empty() && !node->data.has_value();
        }
        return false;
    }

    void delete_node(TrieNode* node) {
        if (!node) {
            return;
        }
        for (auto& [_, child] : node->children) {
            delete_node(child);
        }
        delete node;
    }
};
```

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Lookup | worst-case $O(m)$, where $m$ is the length of the key |
| Add | worst-case $O(m)$, where $m$ is the length of the key |
| Remove | worst-case $O(m)$, where $m$ is the length of the key |

