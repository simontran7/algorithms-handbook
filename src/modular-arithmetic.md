# Modular Arithmetic

## Use Case

Problems that involve `x mod m`, (`m` is typically \\(10^9 + 7\\)), where:

- Building `x` is expensive (repeated work)
- `x` becomes too large

## Theorem

\\[
\boxed{
\begin{aligned}
a \equiv b \pmod{m}
&\iff m \mid (a-b)\\\\
&\iff a-b=km,\quad k\in\mathbb{Z}.
\end{aligned}
}
\\]

\\[
\text{In other words, }a\text{ and }b\text{ have the same remainder when divided by }m.
\\]

### Properties 

We get the following properties from the above:

- \\(\boxed{(a+b)\bmod m = \big((a\bmod m)+(b\bmod m)\big)\bmod m}\\)

- \\(\boxed{(a-b)\bmod m = \big((a\bmod m)-(b\bmod m)\big)\bmod m}\\)

- \\(\boxed{(a \cdot b)\bmod m = \big((a\bmod m)(b\bmod m)\big)\bmod m}\\)

- \\(\boxed{(a^k) \bmod m = \big((a \bmod m)^k\big) \bmod m}\\)

## Templates

### Modular Sum

```python
def mod_sum(nums, mod):
    result = 0

    for x in nums:
        result = (result + x) % mod

    return result
```

### Modular Substraction

```python
def mod_sub(nums, mod):
    result = nums[0] % mod

    for x in nums[1:]:
        result = (result - x) % mod

    return result
```

### Modular Product

```python
def mod_product(nums, mod):
    result = 1

    for x in nums:
        result = (result * x) % mod

    return result
```

### Fast Modular Exponentiation

```python
def mod_exponentiation(base, exp, mod):
    result = 1
    base = base % mod

    while exp > 0:
        if exp % 2 == 1:  # odd exponent
            result = (result * base) % mod
        exp = exp >> 1  # divide by 2
        base = (base * base) % mod

    return result
```

### Modular Number Construction

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
```

### Prefix Remainder

```python
def prefix_remainders(nums, mod):
    remainder = 0
    result = []

    for x in nums:
        remainder = (remainder + x) % mod
        result.append(remainder)

    return result
```

> [!NOTE]
> Python's `%` always returns a result with the same sign as the modulus
