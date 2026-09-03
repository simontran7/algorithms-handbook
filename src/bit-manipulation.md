# Bit Manipulation

## AND Operator

### Behaviour

The AND of 2 bits is 1 if both bits are 1, and 0 otherwise.

### Syntax

```python
a & b
```

### Truth Table

| a | b | output |
|---|---|--------|
| 0 | 0 | 0      |
| 0 | 1 | 0      |
| 1 | 0 | 0      |
| 1 | 1 | 1      |

## OR Operator

### Behaviour

The OR of 2 bits is 1 if either (or both) bits is 1

### Syntax

```python
a | b
```

### Truth table

| a | b | output |
|---|---|--------|
| 0 | 0 | 0      |
| 0 | 1 | 1      |
| 1 | 0 | 1      |
| 1 | 1 | 1      |

## NOT Operator

### Behaviour

The NOT of a bit is 1 if the bit is 0, or 1 otherwise.

### Syntax

```python
~a
```

### Truth Table

| a | output |
|---|--------|
| 0 | 1      |
| 1 | 0      |

## XOR Operator

### Behaviour

The XOR of 2 bits is 1 if *exactly* one of the bits is 1, or 0 otherwise.

### Syntax

```python
a ^ b
```

### Truth Table

| a | b | output |
|---|---|--------|
| 0 | 0 | 0      |
| 0 | 1 | 1      |
| 1 | 0 | 1      |
| 1 | 1 | 0      |

> [!NOTE]
> When these operators are applied to numbers (multiple bits), the operator is applied to the corresponding bits in each number!

## Left Shift Operator and Right Shift Operator

### Behaviour

- Left Shift: Moves all bits in `n` over by `k` places to the left, and fills `0`s from the right (**logical left shift**)
- Right Shift: 
    - Unsigned Integers: moves all bits in `n` over by `k` places to the right, and fills `0`s from the left. (**logical right shift**)
    - Signed Integers: sign extends (**arithmetic right shift**)

### Syntax

```python
n << k
```

```python
n >> k
```

> [!NOTE]
> `x << n` can be thought as multiplying by \(2^n\) while `x >> n` can be thought as floor dividing by \(2^n\)

> [!WARNING]
> Bitwise operators have low precedence, and therefore happens later in evaluation order, so make sure to use parentheses to clearly define your intended grouping.

## Bit Mask

### Use Case

- Isolate bit(s) in an integer.
- A hand-rolled static set typically used in backtracking or dynamic programming algorithms.

### Steps

1. Select the bitwise operator based on your use case.
2. Construct a bit mask.

```python
# set
mask = 1 << k

# k lower bits
mask = (1 << k) - 1

# range of bits
mask = (1 << 5) | (1 << 3)
```

3. Retrieve the bits via `n & mask`.

## Patterns

### Find the most significant bit 

Idea: the most significant bit of some integer `x` can be thought as `log2(x)`, and `log2(x)` can be thought as how many times do i need to divide `x` by 2 (accomplished via `>> 1`) to get to 0.

```python
x = abs(<...>)
bit_index = -1  # so we can get 0-based index
while x != 0:
    bit_index += 1
    x >>= 1
```

> [!WARNING]
> We *need* to take the *absolute* value of `x` first because, as mentioned above, right-shifting a negative `x` sign-extends indefinitely and will never reach `0` (leading to an infinite loop).

> [!NOTE]
> Equivalent builtin is `x.bit_length() - 1`.
