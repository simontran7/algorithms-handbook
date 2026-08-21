# Modular Arithmetic

## Use Case

Problems that involve `x mod m`, (`m` is typically \\(10^9 + 7\\)), where:

- Building `x` is expensive (repeated work)
- `x` becomes too large

## Templates

```python
def mod_subdigits(word, m):
    remainder = 0
    result = []

    for digit_char in word:
        digit = int(digit_char)
        remainder = (remainder * 10 + digit) % m

        if remainder == 0:
            result.append(1)  # divisible
        else:
            result.append(0)

    return result

def mod_power(base, exp, mod):
    result = 1
    base = base % mod

    while exp > 0:
        if exp % 2 == 1:  # odd exponent
            result = (result * base) % mod
        exp = exp >> 1  # divide by 2
        base = (base * base) % mod

    return result

def mod_product(nums, mod):
    result = 1

    for num in nums:
        result = (result * num) % mod

    return result

def mod_sum(nums, mod):
    result = 0

    for num in nums:
        result = (result + num) % mod

    return result
```

> [!NOTE]
> Unlike C++, Python integers are arbitrary-precision, so there's no `long long`-style overflow to worry about. Also, Python's `%` always returns a result with the same sign as the modulus (non-negative for a positive `m`), so unlike C++'s truncating `%`, no extra normalization is needed after subtractions.