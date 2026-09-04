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

Index into the `array` at the desired index \\(i\\) if it is within bounds \\([0, N)\\).

```
func get(this, i: UInt) -> Result[E, ListError] {
    if i >= this.count {
        return Error(ListError::IndexOutOfBounds);
    } 
    Ok(this.data[i])
}
```

### Insertion

1. Reject the insertion if the desired index \\(i\\) is less than \\(0\\).
2. Resize the current array if the number of elements in the current array is equal to the capacity \\(N\\) of the array by allocating a new array of capacity \\(N * 1.5\\) (i.e., **geometric resizing**), then copying all elements from the current array to the new array.
3. If inserting at index \\(N - 1\\), skip to step 4. Otherwise, shift all elements from \\([i + 1, N)\\) to the right to make way for the new element.
4. Write the new element at index \\(i\\).

```
func add(this, i: UInt, e: E) -> Result[(), ListError] {
    if i > this.count {
        return Error(ListError::IndexOutOfBounds);
    }
    if this.count == this.data.capacity() {
        let new_capacity = if this.count == 0 { 1 } else { (this.count.to_float() * 1.5).ceil() as UInt };
        try this.resize(new_capacity);
    }
    for j in (i..this.count).rev() {
        this.data[j + 1] = this.data[j];
    }
    this.data[i] = e; // alternatively, since `j` is also at `i`, `array[j] = <new value>`
    this.count += 1;
    Ok(())
}

func resize(this, new_capacity: UInt) -> Result[(), ListError] {
    let new_array = Array::with_capacity(new_capacity);
    for i in 0..this.count {
        new_array[i] = this.data[i];
    }
    this.data = new_array;
    Ok(())
}
```

<img width="500" src="https://github.com/user-attachments/assets/a4eb2879-823c-4e4a-9926-c9ecd66a94c4" />  

<img width="500" src="https://github.com/user-attachments/assets/a69fdb6d-fc2c-4b7c-83a0-42ca4ac60d6e" />

<img width="500" src="https://github.com/user-attachments/assets/b27f4f89-28c7-4fc3-b23b-fc05736dc3fb" />

### Deletion

```
func remove(this, i: UInt) -> Result[E, ListError] {
    if i >= this.count { 
        return Error(ListError::IndexOutOfBounds); // also prevents `this.count - 1` underflow when `this.count` is 0
    }
    let old_element = this.data[i];
    for j in i..this.count - 1 { 
        this.data[j] = this.data[j + 1];
    }
    this.data[this.count - 1] = 0; 
    this.count -= 1;
    Ok(old_element)
}
```

### `ArrayList`

```
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
| Add at the last position | worst-case \\(O(n)\\), but amortized \\(O(1)\\)  |
| Add at the first position | worst-case \\(O(n)\\) |
| Add in the middle position | worst-case \\(O(n)\\) |
| Lookup by index | worst-case \\(O(1)\\) |
| Remove at the last position | worst-case \\(O(1)\\) |
| Remove at the first position | worst-case \\(O(n)\\) |
| Remove in the middle position | worst-case \\(O(n)\\) |

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
