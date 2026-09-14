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
        # process `array[left]` and/or `array[right]`

        if <condition>:
            left += 1
        else:
            right -= 1

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

## Merge

### Use Case

You have two separate lists (often sorted) and want to combine, compare, or synchronize them

### Template

```python
def two_pointer_merge(list1, list2):
    i = 0
    j = 0

    while i < len(list1) and j < len(list2):
        # compare values of `list1[i]` and `list2[i]`

        # increment either `i` and/or `j`

    # process leftover elements `list1[i:]` and `list2[j:]`
```
