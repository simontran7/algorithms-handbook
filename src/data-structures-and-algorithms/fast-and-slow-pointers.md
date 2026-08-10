# Fast and Slow Pointers

## Dynamic

### Use Case

Detect cycles in a linked list.

### Template

```cpp
ListNode* dynamic_fast_and_slow_pointers(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    auto result = /* initial value */;

    while (fast && fast->next) {
        fast = fast->next->next;
        slow = slow->next;
        // Optionally to detect cycle:
        // if (fast == slow) break;
    }

    // `slow` is at midpoint

    return result;
}
```

## Fixed

### Use Case

Find the \\(k^\text{th}\\) node from the end of a linked list.

### Template

```cpp
ListNode* fixed_gap_fast_and_slow_pointers(ListNode* head, int k) {
    ListNode* slow = head;
    ListNode* fast = head;

    // Advance fast by `k` steps
    // so that when `fast` is nullptr,
    // `slow` will be `k` step(s) away from nullptr,
    // i.e., the `k`th last node
    for (int i = 0; i < k; ++i) {
        fast = fast->next;
    }

    while (fast) {
        fast = fast->next;
        slow = slow->next;
    }

    // ... involving `slow` as the `k`th last node
}
```

> [!NOTE]
> In order to reduce edge cases, and when your algorithm might modify the head, create a **sentinel head node**. This is because modifications at the head typically require a predecessor, yet the head has none, so the sentinel acts as that predecessor, reducing edge-case checks.
> ```cpp
> ListNode sentinel(0, head);      // stack-allocated: no new/delete needed
> ListNode* current = &sentinel;   // prev starts at index -1
> // uniform logic
> return sentinel.next;            // the actual head
> ```
