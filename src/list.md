# List

## Abstract Data Type

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

### Lookup

A lookup at element \\(i\\) in `array` is done by indexing i.e., `array[i]`.

### Insertion

#### Inserting at the Front

<img width="500" src="https://github.com/user-attachments/assets/a4eb2879-823c-4e4a-9926-c9ecd66a94c4" />


#### Inserting in the Middle 

<img width="500" src="https://github.com/user-attachments/assets/a69fdb6d-fc2c-4b7c-83a0-42ca4ac60d6e" />

#### Inserting at the Back

<img width="500" src="https://github.com/user-attachments/assets/b27f4f89-28c7-4fc3-b23b-fc05736dc3fb" />

### Deletion

### `ArrayList`

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

### `SinglyLinkedList`

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

### `DoublyLinkedList`

```python
```

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Add at the head | worst-case \\(O(1)\\) |
| Add at the tail | worst-case \\(O(1)\\) (with a maintained tail pointer) |
| Add in the middle | worst-case \\(O(n)\\) to find the position, \\(O(1)\\) to link |
| Lookup | worst-case \\(O(n)\\) |
| Remove at the head | worst-case \\(O(1)\\) |
| Remove at the tail | worst-case \\(O(1)\\) (with a maintained tail pointer) |
| Remove in the middle | worst-case \\(O(n)\\) to find the node, \\(O(1)\\) to unlink |

> [!NOTE]
> Both variants benefit from a **sentinel node**: an extra node holding no real data, placed immediately before the head (and, for a doubly linked list, another one immediately after the tail). Its only purpose is to always be a valid neighbour, so insertions and removals at a boundary no longer need a special case i.e., the same relinking logic for the middle of the list will work in general. The real head becomes `sentinel.next` (and the real tail `sentinel.prev`, for a doubly linked list).
