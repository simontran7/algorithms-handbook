# Fast and Slow Pointers

## Dynamic

### Use Case

Detect cycles in a linked list.

### Template

```python
def dynamic_fast_and_slow_pointers(head):
    slow = head
    fast = head
    result = <initial value>

    while fast and fast.next:
        fast = fast.next.next
        slow = slow.next
        # Optionally to detect cycle:
        # if fast == slow: break

    # `slow` is at midpoint

    return result
```

## Fixed

### Use Case

Find the \\(k^\text{th}\\) node from the end of a linked list.

### Template

```python
def fixed_gap_fast_and_slow_pointers(head, k):
    slow = head
    fast = head

    # Advance fast by `k` steps
    # so that when `fast` is None,
    # `slow` will be `k` step(s) away from None,
    # i.e., the `k`th last node
    for _ in range(k):
        fast = fast.next

    while fast:
        fast = fast.next
        slow = slow.next

    # ... involving `slow` as the `k`th last node
```

> [!NOTE]
> In order to reduce edge cases, and when your algorithm might modify the head, create a **sentinel head node**. This is because modifications at the head typically require a predecessor, yet the head has none, so the sentinel acts as that predecessor, reducing edge-case checks.
> ```python
> sentinel = ListNode(0, head)
> current = sentinel   # prev starts at index -1
> # uniform logic
> return sentinel.next  # the actual head
> ```
