# Stack

## Abstract Data Type

| **Operation** | **Description**                               |
| ------------- | --------------------------------------------- |
| `top()`      | Returns the element at the top of the stack |
| `push(e)`  | Inserts element `e` at the top of the stack  |
| `pop()`   | Removes the element at the stack of the stack |

## C++ STL API

```cpp
#include <stack>

// Creates an empty stack
std::stack<T> stack;

// Returns the element at the top of the stack
stack.top();

// Returns the number of elements in the stack
stack.size();

// Returns whether the stack is empty
stack.empty();

// Inserts an element at the top of the stack
stack.push(<element>);

// Removes the element at the top of the stack
stack.pop();
```