# Fast and Slow Pointers

> [!NOTE]
> These templates assume a linked list is stored as an arena: a `SlotMap<NodeKey, ListNode<T>>` holding every node, where `NodeKey` is an opaque handle (like a checked index) rather than a pointer. This sidesteps `Option<Box<...>>`/`Rc<RefCell<...>>` entirely, and lets two handles be compared for equality directly (`fast == slow`), instead of needing `std::ptr::eq()`.
> ```rust
> use slotmap::{new_key_type, SlotMap};
>
> new_key_type! { struct NodeKey; }
>
> struct ListNode<T> {
>     val: T,
>     next: Option<NodeKey>,
> }
> ```

## Dynamic

### Signal

Detect cycles in a linked list.

### Template

```rust
fn fast_and_slow_pointers(nodes: &SlotMap<NodeKey, ListNode<T>>, head: Option<NodeKey>) -> i32 {
    let mut slow = head;
    let mut fast = head;
    let result = <initial value>;

    while let Some(f) = fast {
        let Some(f_next) = nodes[f].next else { break };
        fast = nodes[f_next].next;
        slow = slow.and_then(|s| nodes[s].next);
        // Optionally to detect cycle: `if fast == slow { break; }`
    }

    // `slow` is at midpoint

    result
}
```

## Fixed

### Signal

Find the \(k^\text{th}\) node from the end of a linked list.

### Template

```rust
fn fixed_gap(nodes: &SlotMap<NodeKey, ListNode<T>>, head: Option<NodeKey>, k: usize) -> Option<NodeKey> {
    let mut slow = head;
    let mut fast = head;

    // Advance fast by `k` steps
    // so that when `fast` is `None`,
    // `slow` will be `k` step(s) away from `None`
    // i.e., the `k`th last node
    for _ in 0..k {
        fast = fast.and_then(|f| nodes[f].next);
    }

    while fast.is_some() {
        fast = fast.and_then(|f| nodes[f].next);
        slow = slow.and_then(|s| nodes[s].next);
    }

    // ... involving `slow` is the `k`th last node
    slow
}
```
