# List

## Interface

```
trait List<T> {
    fn new() -> Self;
    fn add_front(&mut self, item: T);
    fn add_last(&mut self, item: T);
    fn get_front(&self) -> T;
    fn get_last(&self) -> T;
    fn get(&self, index: usize) -> T;
    fn set(&mut self, index: usize, item: T);
    fn remove_front(&mut self) -> T;
    fn remove_last(&mut self) -> T;
    fn remove(&mut self, item: usize) -> T;
}
```

## Use Case

- Order matters, and you need to iterate over items sequentially
- The problem is naturally described as a sequence of items

## Dynamic Array

### Implementation

```cpp
```

### Standard Library API

```cpp
// new
std::vector<T> v;

// add front
v.insert(v.begin(), item);

// add last
v.push_back(item);

// get front
v.front();

// get last
v.back();

// get element at `index`
v[index]; // no runtime bounds checks
v.at(index) // runtime bounds checks

// set element at `index`
v[index] = item;

// remove front 
v.erase(v.begin());

// remove last
v.pop_back();

// remove at `index`
v.erase(v.begin() + index);
```

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Add at the end | worst-case \\(O(n)\\), but amortized \\(O(1)\\)  |
| Add at the front | worst-case \\(O(n)\\) |
| Add in the middle | worst-case \\(O(n)\\) |
| Lookup by index | worst-case \\(O(1)\\) |
| Remove at the end | worst-case \\(O(1)\\) |
| Remove at the front | worst-case \\(O(n)\\) |
| Remove in the middle | worst-case \\(O(n)\\) |

## Singly Linked List

### Implementation

```cpp
```

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Add at the head | worst-case \\(O(1)\\) |
| Add at the tail | worst-case \\(O(n)\\), or \\(O(1)\\) with a maintained tail pointer |
| Add in the middle | worst-case \\(O(n)\\) |
| Lookup by index | worst-case \\(O(n)\\) |
| Remove at the head | worst-case \\(O(1)\\) |
| Remove at the tail | worst-case \\(O(n)\\) |
| Remove in the middle | worst-case \\(O(n)\\) |

## Doubly Linked List

### Implementation

```cpp
```

### Standard Library API

```cpp
// new
std::list<T> l;

// add front
l.push_front(item);

// add last
l.push_back(item);

// get front
l.front();

// get last
l.back();

// get element at `index` 
*std::next(l.begin(), index);

// set element at `index`
*std::next(l.begin(), index) = item;

// remove front
l.pop_front();

// remove last
l.pop_back();

// remove at `index`
l.erase(std::next(l.begin(), index));
```

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Add at the head | worst-case \\(O(1)\\) |
| Add at the tail | worst-case \\(O(1)\\) (with a maintained tail pointer) |
| Add in the middle | worst-case \\(O(n)\\) to find the position, \\(O(1)\\) to link |
| Lookup by index | worst-case \\(O(n)\\) |
| Remove at the head | worst-case \\(O(1)\\) |
| Remove at the tail | worst-case \\(O(1)\\) (with a maintained tail pointer) |
| Remove in the middle | worst-case \\(O(n)\\) to find the node, \\(O(1)\\) to unlink |

> [!NOTE]
> Both variants benefit from a **sentinel node** (or dummy node): an extra node holding no real data, placed immediately before the head (and, for a doubly linked list, another one immediately after the tail). Its only purpose is to always be a valid neighbour, so insertions and removals at a boundary no longer need a special case; the same relinking logic that works in the middle of the list works there too. The real head becomes `sentinel.next` (and the real tail `sentinel.prev`, for a doubly linked list).
