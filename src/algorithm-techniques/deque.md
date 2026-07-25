# Deque

## Interface

```
trait Deque<T> {
    fn new() -> Self;
    fn front(&self) -> T;
    fn back(&self) -> T;
    fn push_front(&mut self, item: T);
    fn push_back(&mut self, item: T);
    fn pop_front(&mut self) -> T;
    fn pop_back(&mut self) -> T;
}
```

## Use Case

Need to add or remove elements from both ends efficiently (e.g., sliding window front/back, palindrome checks, bounded history).

## Doubly Linked List

A deque is a doubly linked list where both the head and tail are directly reachable, so operations at either end are symmetric. Each node holds a `next` and `prev` pointer, letting the structure be extended or shrunk from whichever end is convenient without touching the rest of the list.

### Lookup

Peeking at either end is a direct read of the head or tail reference, no traversal needed.

### Insertion

Pushing to either end creates a new node and relinks it as the new head or tail, updating that end's `next`/`prev` pointer.

### Deletion

Popping from either end reads off the head or tail node, then repoints the head/tail reference to its neighbour.

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Lookup front/back | worst-case \(O(1)\) |
| Add to front/back | worst-case \(O(1)\) |
| Remove from front/back | worst-case \(O(1)\) |
