# Stack

## Abstract Data Type

| **Operation** | **Description**                               |
| ------------- | --------------------------------------------- |
| `top()`      | Returns the element at the top of the stack |
| `push(e)`  | Inserts element `e` at the top of the stack  |
| `pop()`   | Removes the element at the stack of the stack |

## Python Standard Library

```python
# Create an empty stack
stack = list()

# Get the element at the top
stack[-1]

# Get the number of elements in the stack
len(stack)

# Check if the stack is empty
not stack

# Push an element onto the top
stack.append(<element>)

# Pop the element at the top
stack.pop()
```

> [!NOTE]
> We often use the stack to store the result and convert it to a string. In Python, strings are immutable, so accumulate the result in the stack, and join it at the end with `"".join(stack)`.
