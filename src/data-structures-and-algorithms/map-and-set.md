# Map and Set

## Map

### Interface

```
trait Map<K, V> {
    fn new() -> Self;
    fn get(&self, key: K) -> V;
    fn add(&mut self, key: K, value: V);
    fn remove(&mut self, key: K) -> V;
}
```

### Use Case

- Track elements seen so far for uniqueness (with any extra info stored as the value)
- Frequency counting
- Basic mapping

### Hash Table

A hash table stores entries in an array of **buckets**. To find where a key lives, a **hash function** converts the key into an integer, which is then reduced (usually via modulo) to an index into the bucket array. Since different keys can hash to the same bucket (a **collision**), each bucket typically holds a small list of entries rather than a single one (**chaining**). As more entries are added, the ratio of entries to buckets (the **load factor**) grows; once it crosses a threshold, the table **resizes** (allocates a bigger bucket array and re-hashes every existing entry into it) to keep buckets small and lookups fast.

#### Lookup

Hash the key to find its bucket, then scan that bucket's (usually short) list for an entry with a matching key.

#### Insertion

Hash the key to find its bucket, check whether an entry with that key already exists (update it if so), otherwise append a new entry to the bucket. If this insertion pushes the load factor over the resize threshold, trigger a resize first.

#### Deletion

Hash the key to find its bucket, then scan it for a matching entry and remove it.

#### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Lookup | worst-case \(O(n)\), but average \(O(1)\) |
| Add | worst-case \(O(n)\), but amortized \(O(1)\) |
| Remove | worst-case \(O(n)\), but average \(O(1)\) |

> [!NOTE]
> The worst case (\(O(n)\)) happens when every key collides into the same bucket (e.g., a bad hash function), degrading the bucket into a plain list that must be scanned linearly. The average case assumes a good hash function spreads keys roughly evenly across buckets, keeping each bucket's list short and close to constant size.

## Set

### Interface

```
trait Set<T> {
    fn new() -> Self;
    fn add(&mut self, item: T);
    fn contains(&self, item: T) -> bool;
    fn remove(&mut self, item: T);
}
```

### Use Case

- Track elements seen so far for uniqueness
- Store a chunk (or all) of the input for fast lookups

### Hash Table

A set is implemented the same way as a map, just without a value attached to each key: each bucket holds the raw elements themselves instead of key-value pairs. Everything about hashing, collisions, and resizing works identically; see [Map](#map) above.

#### Lookup

Hash the element to find its bucket, then scan that bucket for a match.

#### Insertion

Hash the element to find its bucket, add it if it isn't already present, triggering a resize first if needed.

#### Deletion

Hash the element to find its bucket, then scan it for a match and remove it.

#### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Lookup | worst-case \(O(n)\), but average \(O(1)\) |
| Add | worst-case \(O(n)\), but amortized \(O(1)\) |
| Remove | worst-case \(O(n)\), but average \(O(1)\) |
