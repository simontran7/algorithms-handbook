# Queue

## Abstract Data Type

```
trait Queue[E] {
    func front(&self) -> E;
    func enqueue(&mut self, element: E);
    func dequeue(&mut self) -> E;
}
```

## Standard Library API

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

