# Bit Manipulation

## OR Operator

### Behaviour

If *any* bit is `1`, then the result will be `1`. Otherwise, the result is `0`.

### Syntax

```cpp
a | b
```

## AND Operator

### Behaviour

If *all* bits are `1`, then the result will be `1`. Otherwise, the result is `0`.

### Syntax

```cpp
a & b
```

## XOR Operator

### Behaviour

If the count of `1` is odd, then the result will be `1`. Otherwise, the result is `0`.

### Syntax

```cpp
a ^ b
```

## Left Shift Operator and Right Shift Operator

### Behaviour

- Left Shift: Moves all bits in `n` over by `k` places to the left, and fills `0`s from the right. Corresponds to multiplying by `2`.
- Right Shift: Moves all bits in `n` over by `k` places to the right, and fills `0`s from the left. Corresponds to floor division by `2`.

### Syntax

```cpp
n << k
```

```cpp
n >> k
```

### Complexity Analysis

Every bitwise operator (`|`, `&`, `^`, `<<`, `>>`) works on a fixed-width machine word, so each is:
- Time Complexity: worst-case \\(O(1)\\)
- Space Complexity: worst-case \\(O(1)\\)

> [!NOTE]
> Bitwise operators have low precedence, and therefore happens later in evaluation order, so make sure to use parentheses to clearly define your intended grouping.

## Bit Mask

### Use Case

- Isolate bit(s) in a bit field.
- A memory efficient set data structure used backtracking or dynamic programming problems.

### Steps

1. Select the bitwise operator based on your use case.
2. Construct a bit mask.

```cpp
// set
int mask = 1 << k;

// k lower bits
int mask = (1 << k) - 1;

// range of bits
int mask = (1 << 5) | (1 << 3);
```

3. Retrieve the bits via `n <operator> mask`.

### Complexity Analysis

Constructing and applying a bit mask is a fixed number of \\(O(1)\\) bitwise operations, so:
- Time Complexity: worst-case \\(O(1)\\)
- Space Complexity: worst-case \\(O(1)\\)

> [!NOTE]
> When a bit mask is used to represent a **set** of up to \\(k\\) items (e.g., in backtracking or DP over subsets), it replaces an \\(O(k)\\)-space hash set with a single integer, and set operations (add/remove/check membership) drop from whatever the set data structure offers to \\(O(1)\\). But enumerating *all* subsets of \\(k\\) items is still \\(O(2^k)\\), since there are that many masks.

> [!NOTE]
> In C++, shifting by the type's width or more is **undefined behavior** (e.g., `1 << 32` on an `int`), as is left-shifting into the sign bit — use `1LL << k` when the mask may exceed 31 bits, or an `unsigned` type. Right shift on signed negative values is implementation-defined pre-C++20 (arithmetic shift in practice). 

> [!NOTE]
> Useful built-ins: 
> - `__builtin_popcount(n)`: count set bits
> - `__builtin_ctz(n)`: count trailing zeros