# C++

## Division Operations

| Operation | Python | C++ |
|---|---|---|
| Integer division | `//` (floors) | `/` (truncates toward zero) |
| Floating-point division | `/` | `/` |
| Remainder | N/A | `%` |
| Modulo | `%` | N/A |
| Division flooring an integer | `//` | `div_floor(<num>, <denom>)` (see below) |
| Division ceiling an integer | `-(a // -b)` | `div_ceil(<num>, <denom>)` (see below) |
| Division Flooring a float | `math.floor(<num> / <denom>)` | `floor(<num> / <denom>)` |
| Division Ceiling a float | `math.ceil(<num> / <denom>)` | `ceil(<num> / <denom>)` |

```cpp
template <typename T>
auto div_ceil(T a, T b) -> T {
    auto q = a / b;
    auto r = a % b;
    bool remainder_exists = (r != 0);
    bool same_sign = (r < 0) == (b < 0);
    if (remainder_exists && same_sign) {
        q = q + 1;
    }
    return q;
}
```

```cpp
template <typename T>
auto div_floor(T a, T b) -> T {
    auto q = a / b;
    auto r = a % b;
    bool remainder_exists = (r != 0);
    bool different_sign = (r < 0) != (b < 0);
    if (remainder_exists && different_sign) {
        q = q - 1;
    }
    return q;
}
```
