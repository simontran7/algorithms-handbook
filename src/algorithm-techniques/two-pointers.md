# Two Pointers

## Opposite Ends

### Use Case

The list input is sorted, and you are looking for a pair (or pairs) that meet a specific condition.

### Template

```cpp
int opposite_ends_two_pointers(std::vector<int>& array) {
    int left = 0;
    int right = array.size() - 1;
    int result = 0;

    while (left < right) {
        // Some logic involving `array[left]` and/or `array[right]`

        if (<condition>) {
            left++;
        } else {
            right--;
        }
    }

    return result;
}
```

## Merge

### Use Case

The input list is sorted, and you want to perform an in-place modification by filtering or deduplicating elements.

### Template

```cpp
int merge_two_pointers(std::vector<int>& array1, std::vector<int>& array2) {
    int i = 0;
    int j = 0;
    int result = 0;

    while (i < array1.size() && j < array2.size()) {
        // Some logic involving `array1[i]` and `array2[j]`
        if (<condition>) {
            i++;
        } else {
            j++;
        }
    }

    while (i < array1.size()) {
        // Some logic involving `array1[i]`
        i++;
    }

    while (j < array2.size()) {
        // Some logic involving `array2[j]`
        j++;
    }

    return result;
}
```

## Read/Write

### Use Case

The problem asks you to modify an array in-place and return its new count.

### Template

```cpp
int read_write_two_pointers(std::vector<int>& array) {
    int write = 0;

    for (int read = 0; read < array.size(); read++) {
        if (<condition to keep array[read]>) {
            array[write] = array[read]; // optionally transform
            write++;
        }
    }

    return write; // new length
}
```