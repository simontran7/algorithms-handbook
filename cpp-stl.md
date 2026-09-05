# C++ STL

## Minimum and Maximum Element

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> values = {5, 2, 9, 1, 7};

    auto [min_it, max_it] = std::minmax_element(values.begin(), values.end());

    std::cout << "min: " << *min_it << "\n";  // 1
    std::cout << "max: " << *max_it << "\n";  // 9
}
```

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
    if (remainder_exists and same_sign) {
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
    if (remainder_exists and different_sign) {
        q = q - 1;
    }
    return q;
}
```
