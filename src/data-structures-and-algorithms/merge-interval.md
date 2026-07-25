# Merge Interval

## Signal

Interval problems

## Template

```rust
fn merge(mut intervals: Vec<[i32; 2]>) -> Vec<[i32; 2]> {
    if intervals.is_empty() {
        return Vec::new();
    }

    intervals.sort();

    let mut result = vec![intervals[0]];

    for interval in intervals {
        let [start, end] = interval;
        let prev_end = result.last().unwrap()[1];
        if start <= prev_end {
            result.last_mut().unwrap()[1] = prev_end.max(end);
        } else {
            result.push(interval);
        }
    }

    result
}
```

