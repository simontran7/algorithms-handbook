# Assembly

Instructions are written as follows:

```
<instruction> <destination> <source>
```

> [!NOTE]
> AT&T (a.k.a. GNU Assembler) assembly's syntax — which is emitted by GCC, LLVM — has a few differences:
> - Instructions are formated as `<instruction> <source> <destination>`.
> - Immediate values and registers are prefixed with sigils (`$` and `%`, respectively)
> - Instructions are *suffixed* with a letter to indicate the byte size they operate on:
>    - `<...>b`: applies to a 1 byte value
>    - `<...>w`: applies to a 2 byte value
>    - `<...>l`: applies to a 4 byte value
>    - `<...>q`: applies to an 8 byte value


- `rax`, `rbx`, `rcx` and `rdx`: general purpose registers used to hold on to intermediate values loaded from memory or used during a calculation of some kind.
- `rsp`: the stack pointer, which holds the memory location of the top of the stack.
- `rbp`: the base pointer, which holds the memory location of the base of the current stack frame
- `rip`: the instruction pointer, which holds the memory location of the next instruction to execute
- `rflags`: holds a series of flags, used by comparison instructions for example.

Registers are *prefixed* with a letter to indicate their byte size:
    - 
    - `e<...>`: stores 4 bytes
    - `r<...>`: stores 8 bytes


