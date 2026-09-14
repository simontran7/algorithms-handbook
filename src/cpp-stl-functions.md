# C++ STL Functions

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

## Accumulate

```cpp
#include <numeric>
#include <vector>
#include <iostream>
#include <functional>

int main() {
    std::vector<int> values = {1, 2, 3, 4};

    int sum = std::accumulate(values.begin(), values.end(), 0);
    int product = std::accumulate(values.begin(), values.end(), 1, std::multiplies<int>());

    std::cout << "sum: " << sum << "\n";      // 10
    std::cout << "product: " << product << "\n";  // 24
}
```

## GCD and LCM

```cpp
#include <numeric>
#include <iostream>

int main() {
    std::cout << "gcd: " << std::gcd(12, 18) << "\n";  // 6
    std::cout << "lcm: " << std::lcm(4, 6) << "\n";    // 12
}
```

## Next Permutation

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> values = {1, 2, 3};

    do {
        for (int v : values) std::cout << v << " ";
        std::cout << "\n";
    } while (std::next_permutation(values.begin(), values.end()));
    // 1 2 3
    // 1 3 2
    // 2 1 3
    // 2 3 1
    // 3 1 2
    // 3 2 1
}
```

## Nth Element

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> values = {5, 2, 9, 1, 7};

    std::nth_element(values.begin(), values.begin() + 2, values.end());

    std::cout << "3rd smallest: " << values[2] << "\n";  // 5
}
```

## Iota

```cpp
#include <numeric>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> indices(5);

    std::iota(indices.begin(), indices.end(), 0);

    for (int i : indices) {
        std::cout << i << " "; 
    } // 0 1 2 3 4
}
```
