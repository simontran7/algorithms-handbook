# Bit Manipulation

## OR Operator

### Behaviour

If _any_ bit is `1`, then the result will be `1`. Otherwise, the result is `0`.

### Syntax

```rust
a | b
```

## AND Operator

### Behaviour

If _all_ bits are `1`, then the result will be `1`. Otherwise, the result is `0`.

### Syntax

```rust
a & b
```

## XOR Operator

### Behaviour

If the count of `1` is odd, then the result will be `1`. Otherwise, the result is `0`.

### Syntax

```rust
a ^ b
```

## Left Shift Operator and Right Shift Operator

### Behaviour

- Left Shift: Moves all bits in `n` over by `k` places to the left, and fills `0`s from the right. Corresponds to multiplying by `2`.
- Right Shift: Moves all bits in `n` over by `k` places to the right, and fills `0`s from the left. Corresponds to floor division by `2`.

### Syntax

```rust
n << k
```

```rust
n >> k
```

> [!NOTE]
> Bitwise operators have low precedence, and therefore happens later in evaluation order, so make sure to use parentheses to clearly define your intended grouping.

## Bit Mask

### Signal

- Isolate bit(s) in a bit field.
- A memory efficient set data structure used backtracking or dynamic programming problems.

### Steps

1. Select the bitwise operator based on your use case.
2. Construct a bit mask.

```rust
// set
let mask = 1 << k;

// k lower bits
let mask = (1 << k) - 1;

// range of bits
let mask = (1 << 5) | (1 << 3);
```

3. Retrieve the bits via `n <operator> mask`.

