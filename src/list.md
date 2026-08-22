# List

## Interface

```
trait List[E] {
    func new() -> Self;
    func get_first(&self) -> E;
    func get_last(&self) -> E;
    func get(&self, index: usize) -> E;
    func add_first(&mut self, element: E);
    func add_last(&mut self, element: E);
    func add(&mut self, index: usize, element: E);
    func set(&mut self, index: usize, element: E);
    func remove_first(&mut self) -> E;
    func remove_last(&mut self) -> E;
    func remove(&mut self, index: usize) -> E;
}
```

## Use Case

You need an ordered sequence of elements where each element has an index.

## Dynamic Array

### Implementation

```python
```

### Standard Library API

```python
# new
l = []

# add first
l.insert(0, item)

# add last
l.append(item)

# get first
l[0]

# get last
l[-1]

# get element at `index`
l[<index>]

# set `element` at `index`
l[<index>] = <element>

# remove first
l.pop(0)

# remove last
l.pop()

# remove at `index`
l.pop(<index>)
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

```python
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

```python
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
> Both variants benefit from a **sentinel node**: an extra node holding no real data, placed immediately before the head (and, for a doubly linked list, another one immediately after the tail). Its only purpose is to always be a valid neighbour, so insertions and removals at a boundary no longer need a special case i.e., the same relinking logic for the middle of the list will work in general. The real head becomes `sentinel.next` (and the real tail `sentinel.prev`, for a doubly linked list).
