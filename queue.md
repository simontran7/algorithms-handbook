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

## Circular Dynamic Array

### Lookup

### Insertion

### Deletion

### Complexity Analysis

...

## Python Standard Library

### Queue

```python
from collections import deque

# Create an empty queue
queue = deque()

# Get the number of elements
len(queue)

# Check if queue is empty
not queue

# Get the element at the front
queue[0]

# Enqueue an element at the back
queue.append(element)

# Dequeue the element at the front
queue.popleft()
```

### Deque

```python
from collections import deque

# Initializes an empty deque
dq = deque()

# Returns the number of elements in the deque
len(dq)

# Returns whether the deque has any elements
len(dq) == 0

# Returns the element at the front of the deque
dq[0]

# Returns the element at the back of the deque
dq[-1]

# Inserts an element at the front of the deque
dq.appendleft(element)

# Inserts an element at the back of the deque
dq.append(element)

# Removes the element at the front of the deque
dq.popleft()

# Removes the element at the back of the deque
dq.pop()
```
