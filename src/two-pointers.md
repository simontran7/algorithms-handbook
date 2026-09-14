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

        if <condition to move only `left`>:
            left += 1
        elif <condition to move only `right`>:
            right -= 1
        else:
            # both pointers satisfy/violate the condition together
            left += 1
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
        # compare `list1[i]` and `list2[j]`

        if <condition to advance only `i`>:
            i += 1
        elif <condition to advance only `j`>:
            j += 1
        else:
            # both elements satisfy the condition together (e.g. equal, or matched pair)
            i += 1
            j += 1

    # drain whichever list wasn't exhausted )only one of these runs)
    while i < len(list1):
        # process `list1[i]`
        i += 1

    while j < len(list2):
        # process `list2[j]`
        j += 1
```
