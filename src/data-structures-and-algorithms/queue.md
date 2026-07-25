# Queue

## Interface

```rust
trait Queue<T> {
    fn new() -> Self;
    fn front(&self) -> T;
    fn enqueue(&mut self, item: T);
    fn dequeue(&mut self) -> T;
}
```

## Use Case

Processing elements in a FIFO order.

