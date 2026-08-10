# Map and Set

## Interface

### Map

```
trait Map<K, V> {
    func get(&self, key: K) -> V;
    func add(&mut self, key: K, value: V);
    func remove(&mut self, key: K) -> V;
}
```

### Set

```
trait Set<T> {
    func add(&mut self, item: T);
    func contains(&self, item: T) -> Bool;
    func remove(&mut self, item: T);
}
```

### Use Case

#### Map

- Track elements seen so far for uniqueness (with any extra info stored as the value)
- Frequency counting
- Basic mapping

#### Set

- Track elements seen so far for uniqueness
- Store a chunk (or all) of the input for fast lookups

## Hash Table

A **hash table** stores entries in an array of **buckets**. To find where a key lives, a **hash function** converts the key into an integer, which is then reduced (usually via modulo) to an index into the bucket array. Since different keys can hash to the same bucket (a **collision**), each bucket typically holds a small list of entries rather than a single one (**chaining**). As more entries are added, the ratio of entries to buckets (the **load factor**) grows; once it crosses a threshold, the table **resizes** (allocates a bigger bucket array and re-hashes every existing entry into it) to keep buckets small and lookups fast.

### Lookup

Hash the key to find its bucket, then scan that bucket's (usually short) list for an entry with a matching key.

### Insertion

Hash the key to find its bucket, check whether an entry with that key already exists (update it if so), otherwise append a new entry to the bucket. If this insertion pushes the load factor over the resize threshold, trigger a resize first.

### Deletion

Hash the key to find its bucket, then scan it for a matching entry and remove it.

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Lookup | worst-case \\(O(n)\\), average \\(O(1)\\) |
| Add | worst-case \\(O(n)\\), amortized \\(O(1)\\) |
| Remove | worst-case \\(O(n)\\), average \\(O(1)\\) |

## API

### Map

```cpp
#include <unordered_map>

// Create an empty map
std::unordered_map<K, V> m;

// Create a map with initial values
std::unordered_map<K, V> m = {
    {<key 1>, <value 1>},
    {<key 2>, <value 2>}
};

// Get number of entries
m.size();

// Check if the map is empty
m.empty();

// Add new entry or update current entry
m[<key>] = <value>;

// Remove an entry
m.erase(<key>);

// Remove all entries
m.clear();

// Get value
// Note: throws std::out_of_range if the key isn't found, unlike operator[] which default-constructs and inserts it
m.at(<key>);

// Check if key exists (C++20)
m.contains(<key>);

// Iterate all entries
for (const auto& [key, value] : my_map) {
    // ...
}
```

### Set

```cpp
#include <unordered_set>

// Create an empty set
std::unordered_set<T> s;

// Check if a set contains an element 
s.contains(<element>);

// Get the number of elements
s.size();

// Check if the set is empty
s.empty();

// Add an element
s.insert(<element>);

// Remove an element
s.erase(<element>);

// Remove all elements
s.clear();
```
