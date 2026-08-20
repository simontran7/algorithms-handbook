# Record Reordering

## Alignment Requirement

Every type has an **alignment requirement**, a number of bytes \\(N\\) that determines the memory addresses where objects of that type can be placed. If a type \\(T\\) has an alignment requirement of \\(N\\), objects of type \\(T\\) must be placed at memory addresses that are multiples of (N).

A primitive type has a **natural alignment requirement**, which is equal to its byte size.

The following is a table describing the alignment requirements the Rust compiler defaults to:

| Type                              |                                            Typical         alignment | Natural               |
| --------------------------------- | -------------------------------------------------------------------: | --------------------- |
| `bool`                            |                                                                    1 | Yes                   |
| `u8` / `i8`                       |                                                                    1 | Yes                   |
| `u16` / `i16`                     |                                                                    2 | Yes                   |
| `u32` / `i32`                     |                                                                    4 | Yes                   |
| `u64` / `i64`                     |                                                                    8 | Yes                   |
| `u128` / `i128`                   |                         **16 on many targets, but target-dependent** | Yes                   |
| `usize` / `isize`                 |                                             8 on 64-bit, 4 on 32-bit | Yes                   |
| `f32`                             |                                                                    4 | Yes                   |
| `f64`                             |                                                                    8 | Yes                   |
| `char`                            |                                                                    4 | Yes                   |
| `()`                              |                                                                    1 | Yes                   |
| Struct                            |                                      maximum alignment of its fields | Depends               |
| Enum                              | implementation-defined (generally at least enough for its variants)  | Depends               |
| Array `[T; N]`                    |                                                     alignment of `T` | Yes                   |
| Slice `[T]`                       |                                                     alignment of `T` | Yes*                  |
| Reference `&T` / `&mut T`         |                                                    pointer alignment | Yes*                  |
| Raw pointer `*const T` / `*mut T` |                                                    pointer alignment | Yes*                  |

## The Issue

For record types, the compiler may insert **padding** —  unused byte(s) holding no data — to satisfy alignment requirements.

There are two kinds of padding:
- **Internal padding**: unused bytes added after a field so the subsequent field is aligned.
- **Trailing padding**: unused bytes added after last field, so in an array of structs, the subsequent's record object is aligned.  

However, padding increases a record's size, which increases memory consumption.

## The Solution

To reduce the size of a record, the idea is to re-order the fields:
1. Put fields with the larger alignment requirements first, then progressively smaller ones.
2. Group together fields of the same alignment