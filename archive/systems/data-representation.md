# Data Representation

## Number Systems

### Decimal System

The **Decimal System** is a number system that uses base 10, characterized by two fundamental properties:
- Each digit position can hold one of 10 unique values (0 through 9), where values greater than 9 require carrying to an additional digit position to the left.
- Each digit's position determines its contribution to the overall value through positional notation. Digits are labeled from right to left as $d_0, d_1, d_2, \dots, d_{N - 1}$ where each successive position represents ten times the value of the position to its right.

More formally, any $N$-digit number can be expressed using **positional notation** as:

$$
(d_{N-1} \cdot 10^{N-1}) + (d_{N-2} \cdot 10^{N-2}) + \dots + (d_2 \cdot 10^2) + (d_1 \cdot 10^1) + (d_0 \cdot 10^0)
$$

### Binary System

**Binary** is a number system that uses base 2, where:

- Each digit position (called a **bit**) can hold one of two unique values: 0 or 1. Values greater than 1 require carrying to an additional bit position to the left.
- Each bit's position determines its contribution through powers of 2: $2^{N-1}, \dots, 2^1, 2^0$.
- We call the bit with the highest positional value the **most significant bit**, and the bit with the lowest positional value the **leas significant bit**.

#### Bit groupings

- **Byte**: 8 bits (the smallest addressable unit of memory)
- **Nibble**: 4 bits 
- **Word**: determined by the CPU's register (the natural unit of data that a processor operates on)

> [!NOTE]
> By the multiplication principle, for a base $b$, and $n$ digits, you can represent $b^n$ unique values.

### Hexadecimal System

**Hexadecimal** uses base 16, where:
- Each digit position can hold one of 16 unique values, such that:
  - 0 to 9 are represented as is.
  - 10 to 15 are represented as `A` to `F`.
- Each digit's position determines its contribution through powers of 16: $16^{N-1}, \dots, 16^1, 16^0$.

> [!NOTE]
> Binary numbers are typically prefixed with `0b`, while hexadecimal numbers with `0x`.

## Converting Between Number Systems

### Decimal to any base $b$

#### Method 1: build the number $n$ from the left (Find the most significant bit first)

1. Find largest exponent such that $b^{exponent} \le n$
2. Write at position $b^{exponent}$ the quotient $q = n \div b^{exponent}$
3. Update $n = n - (q \cdot b^{exponent})$
4. Repeat steps 1 to 3 until the $n \le 0$

#### Method 2: Build the number $n$ from the right (Find the least significant bit first)

1. Repeatedly divide the decimal number by the target base
2. Record the remainder at each step
3. Continue until the quotient becomes 0
4. Read the remainders from bottom to top to get the result

### Any base $b$ to decimal 

For a number with digits $d_{N - 1}, d_{N - 2}, \dots, d_1, d_0$ in base $b$, convert the number by multiplying each digit by its place value $b^i$:

$$
(d_{N-1} \cdot b^{N-1}) + (d_{N-2} \cdot b^{N-2}) + \dots + (d_1 \cdot b^1) + (d_0 \cdot b^0)
$$

> [!NOTE]
> When converting bits encoded using two’s complement, first check the most significant bit. If it is 1, treat its place value as negative, then proceed with the conversion as usual.

### Binary to Hexadecimal

1. Group binary digits into sets of 4 bits from right to left
2. Pad the leftmost group with leading zeros if necessary
3. Convert each 4-bit group to its hexadecimal equivalent using the table below

### Hexadecimal to Binary

1. Convert each hexadecimal digit to its 4-bit binary equivalent using the table below
2. Concatenate all binary groups

| Hex | Binary | Decimal |
| --- | ------ | ------- |
| 0   | 0000   | 0       |
| 1   | 0001   | 1       |
| 2   | 0010   | 2       |
| 3   | 0011   | 3       |
| 4   | 0100   | 4       |
| 5   | 0101   | 5       |
| 6   | 0110   | 6       |
| 7   | 0111   | 7       |
| 8   | 1000   | 8       |
| 9   | 1001   | 9       |
| A   | 1010   | 10      |
| B   | 1011   | 11      |
| C   | 1100   | 12      |
| D   | 1101   | 13      |
| E   | 1110   | 14      |
| F   | 1111   | 15      |

## Computer Data Units

### Memory and Storage Capacities

| Unit            | Value                                                    |
| --------------- | -------------------------------------------------------- |
| 1 KiB (Kibibyte) | $2^{10}$ bytes (1,024 bytes)                         |
| 1 MiB (Mebibyte) | $2^{20}$ bytes (1,048,576 bytes)                     |
| 1 GiB (Gibibyte) | $2^{30}$ bytes (1,073,741,824 bytes)                 |
| 1 TiB (Tebibyte) | $2^{40}$ bytes (1,099,511,627,776 bytes)             |
| 1 PiB (Pebibyte) | $2^{50}$ bytes (1,125,899,906,842,624 bytes)         |
| 1 EiB (Exbibyte) | $2^{60}$ bytes (1,152,921,504,606,846,976 bytes)     |

### Data Transfer Units

| Unit           | Value                  |
| -------------- | ---------------------- |
| 1 Kilobit (Kb) | 1,000 bits             |
| 1 Megabit (Mb) | 1,000,000 bits         |
| 1 Gigabit (Gb) | 1,000,000,000 bits     |
| 1 Terabit (Tb) | 1,000,000,000,000 bits |

## Character Representation

### ASCII

The **American Standard Code for Information Interchange (ASCII)** is a character encoding standard which uses 7 bits per character.

#### Types of ASCII Characters

- Non-printable characters
  - Control characters, from `0x00` to `0x1F`
  - Delete character, `0x7F`
- Printable characters, from `0x20` to `0x7E`

#### ASCII Table

| Dec | Char |
|-----|------|
| 0   | `NUL`  |
| 1   | `SOH`  |
| 2   | `STX`  |
| 3   | `ETX`  |
| 4   | `EOT`  |
| 5   | `ENQ`  |
| 6   | `ACK`  |
| 7   | `BEL`  |
| 8   | `BS`   |
| 9   | `HT`   |
| 10  | `LF`   |
| 11  | `VT`   |
| 12  | `FF`   |
| 13  | `CR`   |
| 14  | `SO`   |
| 15  | `SI`   |
| 16  | `DLE`  |
| 17  | `DC1`  |
| 18  | `DC2`  |
| 19  | `DC3`  |
| 20  | `DC4`  |
| 21  | `NAK`  |
| 22  | `SYN`  |
| 23  | `ETB`  |
| 24  | `CAN`  |
| 25  | `EM`   |
| 26  | `SUB`  |
| 27  | `ESC`  |
| 28  | `FS`   |
| 29  | `GS`   |
| 30  | `RS`   |
| 31  | `US`   |
| 32  | `` ` `` |
| 33  | `!`    |
| 34  | `"`    |
| 35  | `#`    |
| 36  | `$`    |
| 37  | `%`    |
| 38  | `&`    |
| 39  | `'`    |
| 40  | `(`    |
| 41  | `)`    |
| 42  | `*`    |
| 43  | `+`    |
| 44  | `,`    |
| 45  | `-`    |
| 46  | `.`    |
| 47  | `/`    |
| 48  | `0`    |
| 49  | `1`    |
| 50  | `2`    |
| 51  | `3`    |
| 52  | `4`    |
| 53  | `5`    |
| 54  | `6`    |
| 55  | `7`    |
| 56  | `8`    |
| 57  | `9`    |
| 58  | `:`    |
| 59  | `;`    |
| 60  | `<`    |
| 61  | `=`    |
| 62  | `>`    |
| 63  | `?`    |
| 64  | `@`    |
| 65  | `A`    |
| 66  | `B`    |
| 67  | `C`    |
| 68  | `D`    |
| 69  | `E`    |
| 70  | `F`    |
| 71  | `G`    |
| 72  | `H`    |
| 73  | `I`    |
| 74  | `J`    |
| 75  | `K`    |
| 76  | `L`    |
| 77  | `M`    |
| 78  | `N`    |
| 79  | `O`    |
| 80  | `P`    |
| 81  | `Q`    |
| 82  | `R`    |
| 83  | `S`    |
| 84  | `T`    |
| 85  | `U`    |
| 86  | `V`    |
| 87  | `W`    |
| 88  | `X`    |
| 89  | `Y`    |
| 90  | `Z`    |
| 91  | `[`    |
| 92  | `\`    |
| 93  | `]`    |
| 94  | `` ` `` |
| 95  | `_`    |
| 96  | `` ` `` |
| 97  | `a`    |
| 98  | `b`    |
| 99  | `c`    |
| 100 | `d`    |
| 101 | `e`    |
| 102 | `f`    |
| 103 | `g`    |
| 104 | `h`    |
| 105 | `i`    |
| 106 | `j`    |
| 107 | `k`    |
| 108 | `l`    |
| 109 | `m`    |
| 110 | `n`    |
| 111 | `o`    |
| 112 | `p`    |
| 113 | `q`    |
| 114 | `r`    |
| 115 | `s`    |
| 116 | `t`    |
| 117 | `u`    |
| 118 | `v`    |
| 119 | `w`    |
| 120 | `x`    |
| 121 | `y`    |
| 122 | `z`    |
| 123 | `{`    |
| 124 | `` ` `` |
| 125 | `}`    |
| 126 | `~`    |
| 127 | `DEL`  |

### Unicode

**Unicode** is a character set standard that assigns a unique hexadecimal identifier, called a **code point**, to every character across all writing systems. These code points follow the format `U+<....>`. It is also a superset of ASCII.

#### Code Point Categories

- **Surrogate code points**: Code points in the range `U+D800` to `U+DFFF`, which are reserved for use in UTF-16 encoding
- **Scalar values**: All other Unicode code points (excluding surrogate code points)

#### Character Encoding Standards

Unicode defines three primary character encoding standards for converting code points into bytes for storage and transmission. These standards use **code units** as their basic storage elements to represent characters.

- UTF-8
  - **Code unit size**: 8 bits (1 byte)
  - **Character representation**: 1 to 4 code units per character
  - **Encoding type**: Variable-length encoding
- UTF-16
  - **Code unit size**: 16 bits (2 bytes)
  - **Character representation**: 1 code unit, or 2 code units for surrogate code points, and we call these 2 code units a **surrogate pair**
- UTF-32
  - **Code unit size**: 32 bits (4 bytes)
  - **Character representation**: Exactly 1 code unit per character

> [!NOTE]
> Code points can be encoded in another encoding scheme. However, when there is equivalent Unicode code point in the other encoding scheme, the character will appear as a $\unicode{xFFFD}$.

> [!NOTE]
> Since UTF-16 and UTF-32 stores multi-byte code points, characters whose Unicode code points fall in the ASCII range ($U+0000$ to $U+007F$) gets zero-padded. This leads to both big-endian and little-endian valid orderings.
> For instance, "Hello", corresponding to $U+0048 U+0065 U+006C U+006C U+006F$, which can be represented as `00 48 00 65 00 6C 00 6C 00 6F` (big-endian) or `48 00 65 00 6C 00 6C 00 6F 00` (little-endian).
> To help decoders detect the byte order, Unicode introduced the **Byte Order Mark** $U+FEFF$ which encodes as `FE FF` in big-endian and reads as `FF FE` in little-endian. Modern systems that do use UTF-16 typically just assume little-endian and skip the BOM entirely, which is its own subtle gotcha.

### Grapheme clusters

A **grapheme cluster** represents what users typically think of as a "character", that is, the smallest unit of written language that has semantic meaning.

For instance, the grapheme clusters in the Hindi word $"क्षत्रिय"$ are $["क्ष", "त्रि", "य"]$, where each cluster can comprise multiple Unicode code points:
- The first grapheme $"य"$ corresponds to a Unicode single code point, yet
- The third grapheme $"क्ष"$ is a conjunct consonant formed from three code points: $"क"$ ($U+0915$), $"्"$ ($U+094D$), and $"ष"$ ($U+0937$), which combine to create one visual unit.
- The second grapheme $"त्रि"$ is even more complex, consisting of four code points: $"त"$ ($U+0924$), $"्"$ ($U+094D$), $"र"$ ($U+0930$), and the vowel sign $"ि"$ ($U+093F$), where the vowel mark appears visually before the consonant cluster despite following it in the Unicode sequence.

> [!NOTE]
> The example above highlights why simply counting Unicode code points does not always correspond to what users perceive as individual characters!

## Integers

### Unsigned Integers

An $N$ **unsigned integer** is an integer that can take up values in the range of $[0, 2^N - 1]$.

They use all available bits to represent positive values (including zero)

### Signed Integers

An $N$-bit **signed integer** is an integer that can take up values from $-2^{N-1}$ to $2^{N-1} - 1$.

They reserve one bit (typically the most significant bit) to indicate the sign. This unfortunately reduces the range of representable positive values but enabling representation of negative numbers.

Signed integers are encoded using the **two's complement** encoding system (designed in 1945 by the famous John von Neumann in First Draft of a Report on the EDVAC machine). 

- To encode a positive number using two's complement: we don't change anything. The binary representation of a signed positive integer is the exact same as the binary representation of an unsigned integer.
- To encode a negative number using two's complement:
  1. Start with the binary representation of the positive number and toggle all the bits
  2. Add 1 to the result from step 1

Under two's complement,the most significant bit is reserved to store the sign:
- $\text{MSB} = 0$: positive number (or zero)
- $\text{MSB} = 1$: negative number

To understand why this works, think of these steps as a way of finding the additive inverse $-b$ such that $b + (-b) = 1000\dots0$. We target $1000\dots0$ ($n + 1$ bits wide) rather than $0000\dots0$ because in a $n$ fixed-width register, the leading $1$ is discarded as overflow, making them equivalent. It also sidesteps the problem with one's complement, where $b + \tilde{b} = 1111\dots1$ introduces a "negative zero" ($1111\dots1$) alongside the usual $0000\dots0$.

Step 1 exploits the fact that toggling all the bits of $b$ produces a number $\tilde{b}$ such that every bit position sums to $1$, giving $b + \tilde{b} = 1111\dots1$. Step 2 then adds $1$ to both sides of the equation: the right-hand side carries all the way through, flipping $1111\dots1$ into $1000\dots0$ (with the leading $1$ overflowing out of the register), and the left-hand side tells us the additive inverse is $\tilde{b} + 1$.

> [!NOTE]
> Signed and unsigned integers differ only in interpretation. The same bit pattern can represent different values depending on the type (e.g., the bits `11111101` is $253$ when interpreted as an unsigned integer, and $-3$ as signed integer).

<img src="./images/unsigned-and-signed-integer-representation.png" width="700">

### Integer Overflow and Underflow

**Integer overflow** occurs when an arithmetic operation produces a result too large to fit in the available bits. 

For instance, the following shows integer overflow for a 32-bit unsigned integer.

```c
let a: u32 = u32::MAX;
let b: u32 = 1;
let c: u32 = a.wrapping_add(b);

println!("c = {}", c); // 0
```

**Integer underflow** occurs when an arithmetic operation produces a result too small to fit in the available bits. 

For instance, the following shows integer underflow for a 32-bit unsigned integer:

```rust
let a: u32 = 0;
let b: u32 = 1;
let c: u32 = a.wrapping_sub(b);

println!("c = {}", c); // 4294967295
```

For unsigned integers, when an unsigned integer overflows, the result typically wraps around to the smallest representable value for that bit width, and when an unsigned integer underflows, the result typically wraps around to the largest representable value for that bit width. When a signed integer overflows or underflows, it is considered undefined behavior.

To check for integer overflow in Rust:

```rust
// Returns Option<i32> (`None` on overflow)
match <value>.checked_add(<other>) {
    Some(result) => { 
      // use result 
    }
    None => { 
      // handle overflow
    }
}

<value>.wrapping_add(<other>) // wraps around on overflow
<value>.saturating_add(<other>)  // clamps to min for underflow and clamps to max for overflow
``` 

### Integer Casts

Casting from an integer to a thinner integer involves **truncation**: the most significant bit(s) are discarded until the most significant bit of the smaller integer! 

This may or may not alter the casted value. 

For example, here `after` is a new number:

```rust
let before: u32 = 128000;
let after: u16 = before as u16;
println!("before: {before:b}"); // 0000 0000 0000 0001 1111 0100 0000 0000
println!("after: {after:b}"); //                     1111 0100 0000 0000
```

In this example, `after` is the same as `before` even after truncation!

```rust
let before: u32 = -3;
let after: u16 = before as u16;
println!("before: {before:b}"); // 1111 1111 1111 1111 1111 1111 1111 1101
println!("after: {after:b}"); //                       1111 1111 1111 1101
```

On the other hand, casting from an integer to a wider integer causes no issues because we're simply adding unessential bits!
  - For unsigned values: prepend the signed bit until it is as wide as the new larger data type

  ```rust
  let before: i16 = 4;           
  let after: i32 = before as i32; 
  println!("before: {before:b}"); //                    0000 0000 0000 0100b
  println!("after: {after:b}"); //  0000 0000 0000 0000 0000 0000 0000 0100b
  ```

  - For signed values: repeat the sign of the value for new digits (a.k.a **sign extension**)

  ```rust
  let before: i16 = -4;          
  let after: i32 = before as i32; 
  println!("before: {before:b}"); //                    1111 1111 1111 1100b
  println!("after: {after:b}");  // 1111 1111 1111 1111 1111 1111 1111 1100b
  ```

When casting integers of the same width but different signs (e.g., signed 32 bit integer to unsigned 32 bit integer), the underlying bits does not change! The variable that holds the casted integer only changes its type.

Because of this, it's especially important to know that casting a signed integer to an unsigned integer does not turn it take the absolute value of its signed representation (explicitly use the `abs` function)!

For example: casting a signed integer $x$ with a value $-12345$ to an unsigned integer means its new value is now $4294954951$.

```rust
let x: i32 = -12345;
let y: u32 = x as u32;
let z: u32 = 12345;
println!("x: {x:b}"); // 11111111111111111100111111000111
println!("y: {y:b}"); // 11111111111111111100111111000111 
println!("z: {z:b}"); // z: 11000000111001
```

## Floating-Point Representation

### IEEE 754 Structure

For some number $x$:

$$
x = (-1)^\text{sign} \times (\text{integer}.\text{fraction})_2 \times 2^\text{actual exponent}
$$

- Single precision (32 bits):
```
| 1 bit | 8 bits         |           23 bits                   |
  sign    biased exponent            fraction
```
- Double precision (64 bits):
```
| 1 bit |     11 bits      |             52 bits                |
  sign    biased exponent               fraction
```
- Quadruple precision (128 bits):
```
| 1 bit |     15 bits      |             112 bits                |
  sign    biased exponent               fraction
```

> [!NOTE]
> It may not be possible to store a given $x$ exactly with such a scheme whenever the actual exponent is outside of the possible range, or if the fraction field can't fit in the allocated number of bits (i.e., say for single precision, bits 24 and bits 25, where bit 0 is the implicit integer, are ones)

### Fields

- **Signed field**: Represents the positivity, either 0 (for positive) or 1 (for negative).
- **Biased exponent field**: Determines the power of 2 by which to scale the fraction. The exponent is biased, meaning we add a constant to the actual exponent. The general formula is $2^{\text{bits allocated for biased exponent} - 1} - 1$.
    - Single precision bias: $2^{8 - 1} - 1 = (127)_{10}$
    - Double precision bias: $2^{11 - 1} - 1_{10} = (1023)_{10}$
    - Quadruple precision bias: $2^{15 - 1} - 1 = (16383)_{10}$
    - Range of the actual exponents: $[1 - \text{bias}, \text{bias}]$
- **Fraction field**: Represents the digits after the decimal point.

### Normal Numbers

$$
x = (-1)^\text{sign} \times (1.\text{fraction})_2 \times 2^\text{actual exponent}
$$

```
| sign = any | exponent != 00000000 or exponent != 11111111 | fraction = any
```

### Special Numbers

#### $+\infty$ and $-\infty$

```
| sign = any | exponent = 11111111 | fraction = 000...0 |
```

#### NaN

Key properties:
- Any operation with $\text{NaN}$ produces $\text{NaN}$
- $\text{NaN}$ is never equal to anything, including itself

Types of $\text{NaN}$:
- Quiet $\text{NaN}$: silently propagates $\text{NaN}$ through calculations
- Signalling $\text{NaN}$: triggers an exception or error when encountered in operations

**Quiet $\text{NaN}$**

```
| sign = any | exponent = 11111111 | fraction = 1<no restriction> |
```

**Signalling $\text{NaN}$**

```
| sign = any | exponent = 11111111 | fraction = 0<no restriction> |
```

#### 0

```
| sign = any | exponent = 00000000 | fraction = 000000...0 |
```

#### Denormalized (Subnormal) Numbers

$$
x = (-1)^\text{sign} \times (0.\text{fraction})_2 \times 2^\text{smallest possible actual exponent}
$$

```
| sign = any | exponent = 00000000 | fraction != 000...0 |
```

> [!WARNING]
> $+\infty$ and $-\infty$, $+0$ and $-0$ are not interchangeable!

### Converting Decimal to IEEE 754

To convert $12.375_{10}$ to single precision IEEE 754:

#### Step 1: Convert to binary

$$
12.375_{10} = 1100.011_2
$$

#### Step 2: Determine the sign

Since it's a positive number, the sign bit is 0.

#### Step 3: Normalize the fraction

$$
1100.011_2 = 1.100011_2 \times 2^3
$$

The normalized fraction, padded to 23 bits, is: $10001100000000000000000_2$

#### Step 4: Calculate the biased exponent

$$
\text{biased exponent} = \text{actual exponent} + \text{bias} =  3 + 127 = 130 = 10000010_2
$$

#### Step 5: Combine all fields

```
| Sign | Exponent | Mantissa                |
|  0   | 10000010 | 10001100000000000000000 |
```

Final result: $01000001010001100000000000000000_2$

## Byte Order

Bytes are stored contiguously. As such, we may ask: "how do we organize those bytes in a back-to-back fashion"?

**Byte order**, also known as **endianness** of a system defines how _multi $N$-byte_ chunks ($N \gt 1$) are assigned to memory addresses.
- **Big endian Byte Order**: The most significant byte in the $N$-byte chunk is stored at the lowest memory address.
- **Little endian Byte Order**: The least significant byte in the $N$-byte chunk is stored at the lowest memory address.

For example: for the bytes `0x 01 23 45 67`

```
  Big endian representation
byte:     67    45    23    01
address: 0x100 0x101 0x102 0x103
```

```
          Little endian
byte:     01    23    45    67
address: 0x100 0x101 0x102 0x103
```

> [!NOTE]
> A raw blob has no recoverable endianness on its own. 

> [!NOTE]
> On x86-64 systems (and most systems today), the byte ordering is *little* endian.
