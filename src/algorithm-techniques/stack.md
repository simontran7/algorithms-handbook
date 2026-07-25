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

## API

```cpp
#include <stack>

// Create an empty stack
std::stack<int> stack;

// Get the element at the top
stack.top();

// Get the number of elements in the stack
stack.size();

// Check if the stack is empty
stack.empty();

// Push an element onto the top
stack.push(element);

// Pop the element at the top (returns void!)
stack.pop();
```

> [!NOTE]
> We often use the stack to store the result and convert it to a string. In C++, `std::string` itself supports `push_back` / `pop_back` / `back`, so it can serve as **both the stack and the result**.
