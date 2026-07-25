# Sweep Line

## Use Case

Problem involves intervals of events (i.e., each event happens over a continuous number line of time or position) represented as a 2D array where each element represents an event `[left, right, value]`.

## Examples

### [LeetCode 1094. Car Pooling](https://leetcode.com/problems/car-pooling/description/)

```cpp
class Solution {
public:
    bool carPooling(std::vector<std::vector<int>>& trips, int capacity) {
        int last_end = 0;
        for (const auto& trip : trips) {
            last_end = std::max(last_end, trip[2]);
        }

        std::vector<int> diff_array(last_end + 1, 0);
        for (const auto& trip : trips) {
            int passengers = trip[0], start = trip[1], end = trip[2];
            diff_array[start] += passengers;
            diff_array[end] -= passengers;
        }

        int passenger_count = 0;
        for (int change : diff_array) {
            passenger_count += change;
            if (passenger_count > capacity) {
                return false;
            }
        }

        return true;
    }
};
```

### [LeetCode 2021. Brightest Position on Street](https://leetcode.com/problems/brightest-position-on-street/description/)

```cpp
class Solution {
public:
    int brightestPosition(std::vector<std::vector<int>>& lights) {
        std::vector<std::pair<int, int>> diff_array;
        for (const auto& light : lights) {
            int position = light[0], radius = light[1];
            diff_array.push_back({position - radius, 1});
            diff_array.push_back({position + radius + 1, -1});
        }

        std::sort(diff_array.begin(), diff_array.end());

        int result = 0;
        int curr_brightness = 0;
        int max_brightness = 0;
        for (const auto& [position, change] : diff_array) {
            curr_brightness += change;
            if (curr_brightness > max_brightness) {
                max_brightness = curr_brightness;
                result = position;
            }
        }

        return result;
    }
};
```