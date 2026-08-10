# In-Place Reversal

## Use Case

Reverse in-place the pointers in a linked list.

## Usage

```cpp
ListNode* reverse_list(ListNode* head) {
    ListNode* previous = nullptr;
    ListNode* current = head;

    while (current) {
        ListNode* temp = current->next;
        current->next = previous;

        previous = current;
        current = temp;
    }
    
    return previous;
}
```

## Complexity Analysis

Let \\(n\\) be the number of nodes in the linked list. Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(1)\\)