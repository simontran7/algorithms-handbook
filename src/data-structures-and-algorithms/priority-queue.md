# Priority Queue

## Interface

```rust
trait PriorityQueue<T> {
    fn new() -> Self;
    fn top(&self) -> T;
    fn add(&mut self, item: T);
    fn remove(&mut self) -> T;
}
```

## Use Case

- Repeatedly find the maximum or minimum element
- Get the "top" \(k\) elements
- Find a running/streaming median

## Binary Heap

A binary heap is a complete binary tree (every level fully filled except possibly the last, filled left to right) satisfying the **heap property**: every parent is \(\ge\) its children (max-heap) or \(\le\) its children (min-heap). Because the tree is always complete, it can be stored implicitly in an array with no pointers: for a node at index \(i\), its children sit at \(2i + 1\) and \(2i + 2\), and its parent at \(\lfloor (i - 1) / 2 \rfloor\).

### Lookup

The maximum (or minimum) is always at the root, so peeking at the top is just reading index \(0\) of the array.

### Insertion

Append the new element at the end of the array (the next open leaf), then **sift up**: repeatedly compare it against its parent and swap if it violates the heap property, stopping once it doesn't or it reaches the root.

### Deletion

Swap the root with the last element in the array and shrink the array by one, then **sift down** the new root: repeatedly swap it with its larger (max-heap) or smaller (min-heap) child until the heap property is restored or it reaches a leaf.

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Initialize | worst-case \(O(n)\) |
| Lookup min/max | worst-case \(O(1)\) |
| Add    | worst-case \(O(\log n)\) |
| Remove | worst-case \(O(\log n)\) |
