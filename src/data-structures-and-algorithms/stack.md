# Stack

## Interface

```
trait Stack<T> {
    func new() -> Self;
    func top(&self) -> T;
    func push(&mut self, item: T);
    func pop(&mut self) -> T;
}
```

## Use Case

Elements in the input interacting with each other, with a LIFO order.

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
> We often use the stack to store the result and convert it to a string. In Python, strings are immutable, so build the result as a list of characters and join it at the end with `"".join(stack)`.
