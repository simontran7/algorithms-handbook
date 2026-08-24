# Stack

## Abstract Data Type

```
trait Stack[E] {
    func top(&self) -> E;
    func push(&mut self, element: E);
    func pop(&mut self) -> E;
}
```

## Standard Library API

```python
# Create an empty stack
stack = []

# Get the element at the top
stack[-1]

# Get the number of elements in the stack
len(stack)

# Check if the stack is empty
not stack

# Push an element onto the top
stack.append(element)

# Pop the element at the top
stack.pop()
```

> [!NOTE]
> We often use the stack to store the result and convert it to a string. In Python, strings are immutable, so accumulate the result in the stack, and join it at the end with `"".join(stack)`.
