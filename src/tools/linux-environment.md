# Linux Environment

## Bash Scripting

TO WRITE

## Regular Expressions (PCRE)

### Character Classes

- `[<pattern>]`: matches any single character inside the enclosing square brackets.
- `[<start>-<end>]`: range
- `[^<pattern>]`: negates the list

> [!NOTE]
> Special characters (e.g., `.`, `+`, `*`) lose their meaning when placed in a character class

> [!NOTE]
> Both `-` and `^` are context-sensitive. The `-` only acts as a range operator when it appears between two characters (e.g., `[a-z]`). If it's placed at the very beginning or very end of the brackets (e.g., `[-az]` or `[az-]`), or if it's escaped with a backslash (e.g., `[a\-z]`), regex treats it as a literal hyphen character, not a range. The `^` only negates the entire class when it appears as the first character inside the brackets (e.g., `[^abc]`). If `^` appears anywhere else inside the brackets (e.g., `[a^bc]`), it is treated as a literal caret character and is simply included as one of the characters to match.

#### Shorthand Character Classes

The **lowercase** version matches something, and the **uppercase** version matches the exact opposite (its complement):

| Notation | Description |
|----------|-------------|
| `\d` | Any digit (same as `[0-9]`) |
| `\D` | Any *non*-digit |
| `\w` | Any alphanumeric (letters, digits) or `_` |
| `\W` | Neither alphanumeric nor `_` |
| `\s` | Any whitespace (space, tab, newline) |
| `\S` | Not whitespace |

### Alternation

`<pattern>|<pattern>`: matches the pattern to its left *or* the pattern to its right

> [!NOTE]
> Alternation applies to whole subpatterns, so group when needed (e.g., `foo|barbaz` matches `foo` or `barbaz`, while `(foo|bar)baz` matches `foobaz` or `barbaz`)

### Wildcards

| Notation | Description                            |
|----------|----------------------------------------|
| `.`      | Matches to any character               |
| `?`      | Optional previous (i.e., 0 or 1 of previous) |
| `*`      | 0 or more of previous                  |
| `+`      | 1 or more of previous                  |
| `{n}`    | Exactly `n` of previous                |
| `{n,}`   | `n` or more of previous                |
| `{n, m}` | Between `n` and `m` times of previous  |

> [!NOTE]
> To match it literally, escape it (i.e., `\<wildcard>`).

> [!NOTE]
> By default, quantifiers are **greedy** (i.e., they match as much as possible). Append `?` to make them **lazy** (i.e., match as little as possible): `*?`, `+?`, `??`, `{n, m}?`.


### Anchors

- `^`: anchors the match to the start of the string (or start of the line in multiline mode)
- `$`: anchors the match to the end of the string (or end of the line in multiline mode)
- `\b`: word boundary (i.e., matches the position between a `\w` and a `\W` character (or the start/end of the string))
- `\B`: non-word boundary (i.e., matches any position that `\b` does not)

> [!NOTE]
> Using `^<pattern>$` forces the entire string to match the pattern, instead of letting the regex match a substring somewhere in the middle.


### Groups and Backreferences

- `(<pattern>)`: capturing group (i.e., records what was matched); referenced by position with `\1`, `\2`, … (within the pattern) or `$1`, `$2`, … (in a replacement string)
- `(?:<pattern>)`: non-capturing group (i.e., groups without recording); preferred when you don't need a backreference, as it keeps group numbering cleaner
- `(?<name><pattern>)`: named capturing group; referenced with `\k<name>` within the pattern

> [!NOTE]
> `(\w+) \1` matches a repeated word like `hello hello`, because `\1` must match whatever `(\w+)` captured.


### Lookarounds

**Lookarounds** are zero-width assertions, which means they check for a pattern at the current position without consuming any characters.

- `(?=<pattern>)`: positive lookahead (i.e., matches if `pattern` follows)
- `(?!<pattern>)`: negative lookahead (i.e., matches if `pattern` does not follow)
- `(?<=<pattern>)`: positive lookbehind (i.e., matches if `pattern` precedes)
- `(?<!<pattern>)`: negative lookbehind (i.e., matches if `pattern` does not precede)

> [!NOTE]
> `\d+(?= dollars)` matches the number in `100 dollars` but not in `100 euros`, and the match is just `100`, not `100 dollars`, since the lookahead doesn't consume characters.

> [!NOTE]
> Lookbehind patterns in PCRE must be *fixed-width* (you can't use `*` or `+` inside them). Lookaheads have no such restriction.

## Text Processing

- Search and replace across several files

```shell
rg --files-with-matches '<old text>' | xargs sed -i 's/<old text>/<new text>/g'
```

- Search and replace a single file

```shell
sed -i 's/<old text>/<new text>/g' <file to search>
```

