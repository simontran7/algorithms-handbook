# Two Pointers

## Opposite Ends

### Use Case

The list input is sorted, and you are looking for a pair (or pairs) that meet a specific condition.

### Template

```python
def opposite_ends_two_pointers(array):
    left = 0
    right = len(array) - 1
    result = 0

    while left < right:
        # Some logic involving array[left] and/or array[right]

        if <condition>:
            left += 1
        else:
            right -= 1

    return result
```

## Merge

### Use Case

The input list is sorted, and you want to perform an in-place modification by filtering or deduplicating elements.

### Template

```python
def merge_two_pointers(array1, array2):
    i = 0
    j = 0
    result = 0

    while i < len(array1) and j < len(array2):
        # Some logic involving array1[i] and array2[j]
        if <condition>:
            i += 1
        else:
            j += 1

    while i < len(array1):
        # Some logic involving array1[i]
        i += 1

    while j < len(array2):
        # Some logic involving array2[j]
        j += 1

    return result
```

## Read/Write

### Use Case

The problem asks you to modify an array in-place and return its new count.

### Template

```python
def read_write_two_pointers(array):
    write = 0

    for read in range(len(array)):
        if <condition to keep array[read]>:
            array[write] = array[read]  # optionally transform
            write += 1

    return write  # new length
```
