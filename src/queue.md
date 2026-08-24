# Queue

## Abstract Data Type

```
trait Queue<T> {
    func new() -> Self;
    func front(&self) -> T;
    func enqueue(&mut self, item: T);
    func dequeue(&mut self) -> T;
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

