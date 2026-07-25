# Modular Arithmetic

## Use Case

Problems that involve `x mod m`, (`m` is typically \(10^9 + 7\)), where:
- Building `x` is expensive (repeated work)
- `x` becomes too large

## Template

```rust
fn mod_subdigits(word: &str, m: i64) -> Vec<i32> {
    let mut remainder: i64 = 0;
    let mut result = Vec::new();

    for digit_char in word.chars() {
        let digit = digit_char.to_digit(10).unwrap() as i64;
        remainder = (remainder * 10 + digit) % m;

        if remainder == 0 {
            result.push(1); // divisible
        } else {
            result.push(0);
        }
    }

    result
}

fn mod_power(base: i64, exp: i64, modulus: i64) -> i64 {
    let mut result = 1;
    let mut base = base % modulus;
    let mut exp = exp;

    while exp > 0 {
        if exp % 2 == 1 {
            // odd exponent
            result = (result * base) % modulus;
        }
        exp >>= 1; // divide by 2
        base = (base * base) % modulus;
    }

    result
}

fn mod_product(nums: &[i64], modulus: i64) -> i64 {
    let mut result = 1;

    for &num in nums {
        result = (result * num) % modulus;
    }

    result
}

fn mod_sum(nums: &[i64], modulus: i64) -> i64 {
    let mut result = 0;

    for &num in nums {
        result = (result + num) % modulus;
    }

    result
}
```

