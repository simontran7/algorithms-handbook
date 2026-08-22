# Prefix Sum

## Use Case

You need a subroutine which involves range-sum queries of a subarray in $O(1)$.

## Template

```python
def prefix_sum(array):
    result = [0]

    for num in array:
        result.append(result[-1] + num)

    return result  # sum from [i..j]: `prefix[j + 1] - prefix[i]`
```
