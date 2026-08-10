# In-Place Reversal

## Use Case

Reverse in-place the pointers in a linked list.

## Template

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
