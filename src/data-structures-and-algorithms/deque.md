# Deque

## Interface

```
trait Deque<T> {
    fn new() -> Self;
    fn front(&self) -> T;
    fn back(&self) -> T;
    fn push_front(&mut self, item: T);
    fn push_back(&mut self, item: T);
    fn pop_front(&mut self) -> T;
    fn pop_back(&mut self) -> T;
}
```

## Use Case

Need to add or remove elements from both ends efficiently (e.g., sliding window front/back, palindrome checks, bounded history).

## Standard Library API

```python
```
