# List

## Interface

```rust
trait List<T> {
    fn new() -> Self;
    fn add_front(&mut self, item: T);
    fn add_last(&mut self, item: T);
    fn get_front(&self) -> T;
    fn get_last(&self) -> T;
    fn get(&self, index: usize) -> T;
    fn set(&mut self, index: usize, item: T);
    fn remove_front(&mut self) -> T;
    fn remove_last(&mut self) -> T;
    fn remove(&mut self, item: usize) -> T;
}
```

## Use Case

- Order matters, and you need to iterate over items sequentially
- The problem is naturally described as a sequence of items

## Dynamic Array

A dynamic array stores items contiguously in memory, which is what gives it \(O(1)\) random access by index (the address of item \(i\) is just `base + i * item_size`). Since the underlying memory block has a fixed capacity, growing past it means allocating a new, larger block (typically double the size) and copying every existing item over.

### Lookup

Reading index \(i\) is a direct memory access, no traversal needed.

### Insertion

Adding at the end writes into the next open slot; if the array is already at capacity, it first grows (allocate a new block, copy everything over) before writing. Adding at the front or in the middle requires shifting every item after the insertion point one slot to the right first.

### Deletion

Removing from the end just shrinks the logical length by one. Removing from the front or middle requires shifting every item after the removed index one slot to the left to close the gap.

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Add at the end | worst-case \(O(n)\), but amortized \(O(1)\)  |
| Add at the front | worst-case \(O(n)\) |
| Add in the middle | worst-case \(O(n)\) |
| Lookup by index | worst-case \(O(1)\) |
| Remove at the end | worst-case \(O(1)\) |
| Remove at the front | worst-case \(O(n)\) |
| Remove in the middle | worst-case \(O(n)\) |

## Singly Linked List

A singly linked list stores items as separately allocated nodes scattered across memory, each holding a value and a pointer to the next node. There's no random access: reaching item \(i\) means walking the pointer chain from the head, one node at a time.

A singly linked list is always accessed through a **head pointer**, a reference to the first node. It's the only fixed entry point, since there's no way to reach any other node except by walking from it. Some implementations also maintain a **tail pointer**, a reference to the last node, kept up to date on every insertion or deletion. A tail pointer turns adding at the end into an \(O(1)\) operation (append, then repoint the tail), but it doesn't help removal at the end: after removing the tail node, the new tail is its predecessor, and reaching that predecessor still means walking the whole list from the head, since a singly linked list has no way to go backwards.

### Lookup

Start at the head and follow `next` pointers one node at a time until reaching the target index.

### Insertion

Adding at the head just points the new node's `next` at the current head and repoints the head to the new node, no shifting. Adding elsewhere requires walking to the node just before the insertion point first, then relinking two pointers.

### Deletion

Removing the head just repoints the head to `head.next`. Removing elsewhere requires walking to the *predecessor* of the target node (since there's no `prev` pointer to jump back with) to relink around it.

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Add at the head | worst-case \(O(1)\) |
| Add at the tail | worst-case \(O(n)\), or \(O(1)\) with a maintained tail pointer |
| Add in the middle | worst-case \(O(n)\) |
| Lookup by index | worst-case \(O(n)\) |
| Remove at the head | worst-case \(O(1)\) |
| Remove at the tail | worst-case \(O(n)\) |
| Remove in the middle | worst-case \(O(n)\) |

## Doubly Linked List

A doubly linked list is a singly linked list where each node also holds a `prev` pointer back to its predecessor. That second pointer is what lets a node be removed in \(O(1)\) once you're holding a reference to it (no need to walk from the head to find its predecessor), and lets the list be traversed backwards.

Like a singly linked list, a doubly linked list is accessed through a maintained **head pointer** and, typically, a **tail pointer**. But because every node also has a `prev` pointer, the tail pointer alone is enough to support \(O(1)\) removal at the end too: the new tail is just `tail.prev`, no walk required. This is the key difference from a singly linked list, where a tail pointer only speeds up insertion, not removal.

### Lookup

Same as a singly linked list: walk pointers one node at a time from the head (or from the tail, if closer, since traversal now works both directions).

### Insertion

Adding at the head or tail relinks two pointers on one end using a maintained head/tail reference. Adding in the middle still requires walking to the insertion point, but relinking is \(O(1)\) once there, since both the predecessor's and successor's `prev`/`next` pointers are directly reachable.

### Deletion

Given a reference to a node, removal is \(O(1)\): read its `prev` and `next` directly, and relink them to each other. Deleting by index still requires walking to that node first.

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Add at the head | worst-case \(O(1)\) |
| Add at the tail | worst-case \(O(1)\) (with a maintained tail pointer) |
| Add in the middle | worst-case \(O(n)\) to find the position, \(O(1)\) to link |
| Lookup by index | worst-case \(O(n)\) |
| Remove at the head | worst-case \(O(1)\) |
| Remove at the tail | worst-case \(O(1)\) (with a maintained tail pointer) |
| Remove in the middle | worst-case \(O(n)\) to find the node, \(O(1)\) to unlink |

> [!NOTE]
> Both variants benefit from a **sentinel node** (or dummy node): an extra node holding no real data, placed immediately before the head (and, for a doubly linked list, another one immediately after the tail). Its only purpose is to always be a valid neighbour, so insertions and removals at a boundary no longer need a special case; the same relinking logic that works in the middle of the list works there too. The real head becomes `sentinel.next` (and the real tail `sentinel.prev`, for a doubly linked list).
