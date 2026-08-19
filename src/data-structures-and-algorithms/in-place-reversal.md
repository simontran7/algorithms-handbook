# In-Place Reversal

## Use Case

Reverse in-place the pointers in a linked list.

## Template

```cpp
ListNode* reverse_list(ListNode* head) {
    ListNode* i = nullptr;
    ListNode* j = head;

    while (j) {
        ListNode* temp = j->next;
        j->next = i;

        i = j;
        j = temp;
    }
    
    return i;
}
```
