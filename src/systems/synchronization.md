# Synchronization

Multiple threads can read shared data simultaneously as long as no one is writing. However, whenever any of those threads write, it introduces a class of concurrency bugs called **data races**. 

A data race occurs when:
- Two or more threads concurrently accessing the same memory location
- At least one access is a write
- The accesses are not synchronized

There's a  broader concurrency class of concurrency bugs called **race conditions**. This type of bug arises when the program's correctness depends on the timing or ordering of events (like thread scheduling), and different orderings produce different results. 

To prevent data races and race conditions, we must introduce **synchronization primitives**.

## Mutex Lock

...

## Readers-writer Lock

A **readers-writer lock** ([`std::sync::RwLock`](https://doc.rust-lang.org/std/sync/struct.RwLock.html)) is a synchronization primitive for multi-threaded shared mutable state that allows multiple readers *or* a single writer at a time. It is best used for scenarios where reads are frequent and writes are infrequent. 

Its two core methods are:
- `read()`: Acquires a read lock, and returns `RwLockReadGuard<T>`, or blocks if a write lock is held.
- `write()`: Acquires a write lock, and returns `RwLockWriteGuard<T>`, or blocks if read or write locks are held.

## Condition Variable

...

## Semaphore

...


