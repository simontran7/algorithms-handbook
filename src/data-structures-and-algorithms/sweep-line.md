# Sweep Line

## Use Case

Problem involves intervals of events (i.e., each event happens over a continuous number line of time or position) represented as a 2D array where each element represents an event `[left, right, value]`.

## Examples

### [LeetCode 1094. Car Pooling](https://leetcode.com/problems/car-pooling/description/)

```rust
fn car_pooling(trips: Vec<Vec<i32>>, capacity: i32) -> bool {
    let last_end = trips.iter().map(|t| t[2]).max().unwrap();
    let mut diff_array = vec![0; (last_end + 1) as usize];
    for trip in &trips {
        let (passengers, start, end) = (trip[0], trip[1] as usize, trip[2] as usize);
        diff_array[start] += passengers;
        diff_array[end] -= passengers;
    }

    let mut passenger_count = 0;
    for change in diff_array {
        passenger_count += change;
        if passenger_count > capacity {
            return false;
        }
    }

    true
}
```

### [LeetCode 2021. Brightest Position on Street](https://leetcode.com/problems/brightest-position-on-street/description/)

```rust
fn brightest_position(lights: Vec<Vec<i32>>) -> i32 {
    let mut diff_array = Vec::new();
    for light in &lights {
        let (position, radius) = (light[0], light[1]);
        diff_array.push((position - radius, 1));
        diff_array.push((position + radius + 1, -1));
    }

    diff_array.sort();
    let mut result = 0;
    let mut curr_brightness = 0;
    let mut max_brightness = 0;
    for (position, change) in diff_array {
        curr_brightness += change;
        if curr_brightness > max_brightness {
            max_brightness = curr_brightness;
            result = position;
        }
    }

    result
}
```

