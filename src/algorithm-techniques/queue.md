# Queue

## Interface

```
trait Queue<T> {
    func new() -> Self;
    func front(&self) -> T;
    func enqueue(&mut self, item: T);
    func dequeue(&mut self) -> T;
}
```

## Use Case

Processing elements in a FIFO order.

## API

```cpp
#include <queue>

// Create an empty queue
std::queue<int> queue;

// Get the number of elements
queue.size();

// Check if queue is empty
queue.empty();

// Get the element at the front
queue.front();

// Enqueue an element at the back
queue.push(element);

// Dequeue the element at the front (returns void!)
queue.pop();
``` 

