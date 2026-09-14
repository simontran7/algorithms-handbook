# Queue

## Abstract Data Type

### Standard Queue

| **Operation** | **Description**                               |
| ------------- | --------------------------------------------- |
| `peek()`      | Returns the element at the front of the queue |
| `enqueue(e)`  | Inserts element `e` at the back of the queue  |
| `dequeue()`   | Removes the element at the front of the queue |

### Double-Ended Queue

| **Operation**    | **Description**                               |
| ---------------- | --------------------------------------------- |
| `front()`        | Returns the element at the front of the deque |
| `back()`         | Returns the element at the back of the deque  |
| `push_front(e)`  | Inserts element `e` at the front of the deque |
| `push_back(e)`   | Inserts element `e` at the back of the deque  |
| `remove_front()` | Removes the element at the front of the deque |
| `remove_back()`  | Removes the element at the back of the deque  |

## C++ STL API

### Standard Queue

```cpp
#include <queue>

// Creates an empty queue
std::queue<T> queue;

// Returns the number of elements in the queue
queue.size();

// Returns whether the queue is empty
queue.empty();

// Returns the element at the front of the queue
queue.front();

// Inserts an element at the back of the queue
queue.push(<element>);

// Removes the element at the front of the queue
// Note: unlike Python's `popleft()`, this does not return the removed element -
// call `front()` first if you need the value
queue.pop();
```

### Double-Ended Queue

```cpp
#include <deque>

// Initializes an empty deque
std::deque<T> dq;

// Returns the number of elements in the deque
dq.size();

// Returns whether the deque has any elements
dq.empty();

// Returns the element at the front of the deque
dq.front();

// Returns the element at the back of the deque
dq.back();

// Inserts an element at the front of the deque
dq.push_front(<element>);

// Inserts an element at the back of the deque
dq.push_back(<element>);

// Removes the element at the front of the deque
dq.pop_front();

// Removes the element at the back of the deque
dq.pop_back();
```

## Circular Dynamic Array

### Lookup

### Insertion

### Deletion

### Complexity Analysis

...
