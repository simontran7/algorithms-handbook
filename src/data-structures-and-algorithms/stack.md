# Stack

## Interface

```rust
trait Stack<T> {
    fn new() -> Self;
    fn top(&self) -> T;
    fn push(&mut self, item: T);
    fn pop(&mut self) -> T;
}
```

## Use Case

Elements in the input interacting with each other, with a LIFO order.


