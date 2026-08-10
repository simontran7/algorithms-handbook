# Modular Arithmetic

## Use Case

Problems that involve `x mod m`, (`m` is typically \\(10^9 + 7\\)), where:

- Building `x` is expensive (repeated work)
- `x` becomes too large

## Templates

```cpp
std::vector<int> mod_subdigits(const std::string& word, int m) {
    long long remainder = 0;
    std::vector<int> result;

    for (char digit_char : word) {
        int digit = digit_char - '0';
        remainder = (remainder * 10 + digit) % m;

        if (remainder == 0) {
            result.push_back(1);  // divisible
        } else {
            result.push_back(0);
        }
    }

    return result;
}

long long mod_power(long long base, long long exp, long long mod) {
    long long result = 1;
    base = base % mod;

    while (exp > 0) {
        if (exp % 2 == 1) {  // odd exponent
            result = (result * base) % mod;
        }
        exp = exp >> 1;  // divide by 2
        base = (base * base) % mod;
    }

    return result;
}

long long mod_product(const std::vector<int>& nums, long long mod) {
    long long result = 1;

    for (int num : nums) {
        result = (result * num) % mod;
    }

    return result;
}

long long mod_sum(const std::vector<int>& nums, long long mod) {
    long long result = 0;

    for (int num : nums) {
        result = (result + num) % mod;
    }

    return result;
}
```

> [!NOTE]
> With \\(m = 10^9 + 7\\), the product of two reduced values can reach \\(\approx 10^{18}\\), which silently (in C++) overflows `int` but fits in `long long`, so always use `long long` for any intermediate that multiplies two mod-reduced values. Also, C++'s `%` on negative operands yields a negative result (truncation), so after subtractions normalize with: `((x % m) + m) % m`.