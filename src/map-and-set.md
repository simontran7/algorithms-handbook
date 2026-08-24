# Map and Set

## Abstract Data Type

### Map

```
trait Map[K, V] {
    func get(&self, key: K) -> V;
    func add(&mut self, key: K, value: V);
    func remove(&mut self, key: K) -> V;
}
```

### Set

```
trait Set[T] {
    func add(&mut self, item: T);
    func contains(&self, item: T) -> Bool;
    func remove(&mut self, item: T);
}
```

## Use Case

### Map

- Track elements seen so far for uniqueness (with any extra info stored as the value)
- Frequency counting
- Basic mapping

### Set

- Track elements seen so far for uniqueness
- Store a chunk (or all) of the input for fast lookups

## Hash Table

### Implementation

```python
```

### Standard Library API

#### Map

```python
# Create an empty map
m = dict()

# Create a map with initial values
m = {
    <key 1>: <value 1>,
    <key 2>: <value 2>
}

# Get number of entries
len(m)

# Check if the map is empty
not m

# Add new entry or update current entry
m[<key>] = <value>

# Remove an entry
del m[<key>]

# Remove all entries
m.clear()

# Get value
# Note: raises KeyError if the key isn't found, unlike `m.get(<key>)` which returns None
m[<key>]

# Get the value with a default value if key isn't found
# Note: I like this over `defaultdict(<default value type>)` for counting since it can avoid accidentally creating phantom keys
m.get(<key>, <default value>)

# Note: pretty much a must for adjacency list creation
from collections import defaultdict
m = defaultdict(<default value's type>)

# Check if key exists
<key> in m

# Iterate all entries
for key, value in m.items():
    # ...
```

#### Set

```python
# Create an empty set
s = set()

# Check if a set contains an element
<element> in s

# Get the number of elements
len(s)

# Check if the set is empty
not s

# Add an element
s.add(<element>)

# Remove an element
s.remove(<element>)

# Remove all elements
s.clear()
```

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Lookup | worst-case $O(n)$, average $O(1)$ |
| Add | worst-case $O(n)$, amortized $O(1)$ |
| Remove | worst-case $O(n)$, average $O(1)$ |

