# [NeetCode 150](https://neetcode.io/roadmap)

## Arrays and Hashing Problems

### [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/description/)

#### Solution

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        seen = set()

        for num in nums:
            if num in seen:
                return True
            seen.add(num)

        return False
```

#### Complexity Analysis

Let \\(n\\) be the element count of `nums`. Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(n)\\)

### [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/description/)

#### Solution

```python
from collections import defaultdict

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        s_chars = defaultdict(int)
        t_chars = defaultdict(int)

        for i in range(len(s)):
            s_chars[s[i]] += 1
            t_chars[t[i]] += 1

        return s_chars == t_chars
```

#### Complexity Analysis

Let \\(n\\) be the element count of `s` and `t` (they should be equal). Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(1)\\)

### [1. Two Sum](https://leetcode.com/problems/two-sum/description/)

#### Solution

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        seen = dict()

        for i, n in enumerate(nums):
            complement = target - n
            if complement in seen:
                return [seen[complement], i]
            seen[n] = i

        return []
```

#### Complexity Analysis

Let \\(n\\) be the element count of `nums`. Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(n)\\)

### [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/description/)

#### Solution

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        result = defaultdict(list)

        for s in strs:
            char_count = [0] * 26
            for c in s:
                char_count[ord(c) - ord('a')] += 1
            result[tuple(char_count)].append(s)

        return list(result.values())
```

#### Complexity Analysis

Let \\(n\\) be the element count of `strs`, and \\(k\\) the element count of the longest possible string in `strs`. Then:
- Time Complexity: worst-case \\(O(nk)\\)
- Space Complexity: worst-case \\(O(nk)\\)

### [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/description/)

#### Solution

```python
from collections import Counter
import random

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        def partition(left, right, pivot_idx):
            # save the frequency of the pivot
            pivot_freq = frequency[unique[pivot_idx]]

            # move the pivot to the end of the list
            unique[pivot_idx], unique[right] = unique[right], unique[pivot_idx]
            store_idx = left

            # partition the list
            for i in range(left, right):
                if frequency[unique[i]] < pivot_freq:
                    unique[store_idx], unique[i] = unique[i], unique[store_idx]
                    store_idx += 1

            # place the pivot at the insertion index `store_idx`
            unique[right], unique[store_idx] = unique[store_idx], unique[right]

            return store_idx

        def quickselect(left, right, k_smallest_idx):
            if left == right:
                return

            # pick an random pivot from [left, right)
            pivot_idx = random.randint(left, right)

            # partition the list such that:
            #   - any elements to the left of the pivot has a lower frequency
            #   - any elements to the right of the pivot has an equal or higher frequency
            pivot_idx = partition(left, right, pivot_idx)

            if pivot_idx == k_smallest_idx:
                return
            elif k_smallest_idx < pivot_idx:
                quickselect(left, pivot_idx - 1, k_smallest_idx)
            else:
                quickselect(pivot_idx + 1, right, k_smallest_idx)

        # build an unordered map where the key is an element, and the value is its frequency
        frequency = Counter(nums)
        unique = list(frequency.keys())

        # run quickselect on the list
        n = len(unique)
        quickselect(0, n - 1, n - k)

        # return a slice of the list starting at the kth most frequent element
        return unique[n - k:]
```

#### Complexity Analysis

Let \\(n\\) be the element count of `nums`. Then:
- Time Complexity: average-case \\(O(n)\\), worst-case \\(O(n^2)\\)
- Space Complexity: worst-case \\(O(nk)\\)

### [271. Encode and Decode Strings](https://leetcode.com/problems/encode-and-decode-strings/description/)

#### Solution

```python
class Codec:
    def encode(self, strs: List[str]) -> str:
        """Encodes a list of strings to a single string.
        """
        result = []

        for s in strs:
            result.append(str(len(s)) + '#' + s)

        return ''.join(result)


    def decode(self, s: str) -> List[str]:
        """Decodes a single string to a list of strings.
        """
        result = []
        i = 0

        while i < len(s):
            delim_idx = s.find('#', i)
            str_len = int(s[i:delim_idx])
            str_start = delim_idx + 1
            result.append(s[str_start:str_start + str_len])
            i = str_start + str_len

        return result


# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.decode(codec.encode(strs))
```

#### Complexity Analysis

Let \\(m\\) be the total characters across all original strings, and \\(n\\) be the element count of `strs`. Then:
- Time Complexity: worst-case \\(O(m)\\)
- Space Complexity: worst-case \\(O(m + n)\\)

### [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)

#### Solution

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n = len(nums)
        result = [1] * n

        prefix = 1
        for i in range(n):
            result[i] *= prefix
            prefix *= nums[i]

        postfix = 1
        for i in range(n - 1, -1, -1):
            result[i] *= postfix
            postfix *= nums[i]

        return result
```

#### Complexity Analysis

Let \\(n\\) be the element count of `nums`. Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(1)\\) (excluding the output list)

### [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku/description/)

#### Solution

```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        rows = defaultdict(set)
        cols = defaultdict(set)
        boxes = defaultdict(set)

        for row in range(9):
            for col in range(9):
                if board[row][col] == '.':
                    continue
                if board[row][col] in rows[row] or board[row][col] in cols[col] or board[row][col] in boxes[(row // 3, col // 3)]:
                    return False

                rows[row].add(board[row][col])
                cols[col].add(board[row][col])
                boxes[(row // 3, col // 3)].add(board[row][col])

        return True
```

#### Complexity Analysis

Let \\(n\\) be the element count of `board`. Then:
- Time Complexity: worst-case \\(O(n^2)\\)
- Space Complexity: worst-case \\(O(n^2)\\)

### [121. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/description/)

#### Solution

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        unique_nums = set(nums)
        result = 0

        for num in unique_nums:
            if num - 1 in unique_nums:
                continue

            curr_len = 1
            while num + curr_len in unique_nums:
                curr_len += 1

            result = max(result, curr_len)

        return result
```

#### Complexity Analysis

Let \\(n\\) be the element count of `nums`. Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(n)\\)

## Two Pointers Problems

### [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/description/)

#### Solution

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        left = 0
        right = len(s) - 1

        while left < right:
            while left < right and not s[left].isalnum():
                left += 1
            while left < right and not s[right].isalnum():
                right -= 1

            if s[left].lower() != s[right].lower():
                return False

            left += 1
            right -= 1

        return True
```

#### Complexity Analysis

Let \\(n\\) be the element count of `s`. Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(1)\\)

### [167. Two Sum II - Input Array is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

#### Solution

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        left = 0
        right = len(numbers) - 1

        while left < right:
            curr_sum = numbers[left] + numbers[right]
            if curr_sum < target:
                left += 1
            elif curr_sum > target:
                right -= 1
            else:
                return [left + 1, right + 1]

        return [-1, -1]
```

#### Complexity Analysis

Let \\(n\\) be the element count of `numbers`. Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(1)\\)

### [15. 3Sum](https://leetcode.com/problems/3sum/description/)

#### Solution

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()

        result = []

        for i in range(len(nums)):
            if nums[i] > 0:
                break
            if i != 0 and nums[i] == nums[i - 1]:
                continue

            left = i + 1
            right = len(nums) - 1
            while left < right:
                triplet_sum = nums[i] + nums[left] + nums[right]
                if triplet_sum < 0:
                    left += 1
                elif triplet_sum > 0:
                    right -= 1
                else:
                    result.append([nums[i], nums[left], nums[right]])
                    left += 1
                    right -= 1
                    while left < right and nums[left] == nums[left - 1]:
                        left += 1

        return result
```

#### Complexity Analysis

Let \\(n\\) be the element count of `nums`. Then:
- Time Complexity: worst-case \\(O(n^2)\\)
- Space Complexity: worst-case \\(O(n)\\)

### [11. Container with Most Water](https://leetcode.com/problems/container-with-most-water/)

#### Solution

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        result = 0
        left = 0
        right = len(height) - 1

        while left < right:
            area = min(height[left], height[right]) * (right - left)
            result = max(result, area)
            if height[left] <= height[right]:
                left += 1
            else:
                right -= 1

        return result
```

#### Complexity Analysis

Let \\(n\\) be the element count of `height`. Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(1)\\)

### [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/description/)

#### Solution

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        left = 0
        right = len(height) - 1
        left_pile_max = 0
        right_pile_max = 0
        result = 0

        while left < right:
            if height[left] < height[right]:
                left_pile_max = max(left_pile_max, height[left])
                result += left_pile_max - height[left]
                left += 1
            else:
                right_pile_max = max(right_pile_max, height[right])
                result += right_pile_max - height[right]
                right -= 1

        return result
```

#### Complexity Analysis

Let \\(n\\) be the element count of `height`. Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(1)\\)

## Stack Problems

### [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/description/)

#### Solution

```python
class Solution:
    def isValid(self, s: str) -> bool:
        bracket_pairs = {
            ')': '(',
            '}': '{',
            ']': '[',
        }
        stack = []

        for c in s:
            if c in bracket_pairs:
                if len(stack) == 0 or stack[-1] != bracket_pairs[c]:
                    return False
                stack.pop()
            else:
                stack.append(c)

        return len(stack) == 0
```

#### Complexity Analysis

Let \\(n\\) be the element count of `s`. Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(n)\\)

### [155. Min Stack](https://leetcode.com/problems/min-stack/description/)

#### Solution

```python
class MinStack:

    def __init__(self):
        self.data = []

    def push(self, val: int) -> None:
        if len(self.data) == 0:
            self.data.append((val, val))
        else:
            self.data.append((val, min(val, self.data[-1][1])))

    def pop(self) -> None:
        self.data.pop()

    def top(self) -> int:
        return self.data[-1][0]

    def getMin(self) -> int:
        return self.data[-1][1]

# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```

#### Complexity Analysis

Let \\(n\\) be the number of operations:
- Time Complexity:
    - `push(...)`: worst-case \\(O(1)\\)
    - `pop(...)`: worst-case \\(O(1)\\)
    - `top(...)`: worst-case \\(O(1)\\)
    - `getMin(...)`: worst-case \\(O(1)\\)
- Space Complexity: worst-case \\(O(n)\\)

### [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

#### Solution

```python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []

        for token in tokens:
            match token:
                case "+":
                    y = stack.pop()
                    x = stack.pop()
                    stack.append(x + y)
                case "-":
                    y = stack.pop()
                    x = stack.pop()
                    stack.append(x - y)
                case "*":
                    y = stack.pop()
                    x = stack.pop()
                    stack.append(x * y)
                case "/":
                    y = stack.pop()
                    x = stack.pop()
                    stack.append(math.trunc(x / y))
                case _:
                    stack.append(int(token))

        return stack.pop()
```

#### Complexity Analysis

Let \\(n\\) be the element count of `tokens`. Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(n)\\)

### [739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)

#### Solution

```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        n = len(temperatures)
        result = [0] * n
        mono_stack = []

        for i in range(n):
            while mono_stack and temperatures[mono_stack[-1]] < temperatures[i]:
                top = mono_stack.pop()
                result[top] = i - top
            mono_stack.append(i)

        return result
```

#### Complexity Analysis

Let \\(n\\) be the element count of `temperatures`. Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(n)\\)

### [853. Car Fleet](https://leetcode.com/problems/car-fleet/description/)

#### Solution

```python
class Solution:
    def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        cars = sorted(zip(position, speed), reverse=True)
        prev_time = 0
        result = 0

        for position, speed in cars:
            time = (target - position) / speed
            if time > prev_time:
                result += 1
                prev_time = time

        return result
```

#### Complexity Analysis

Let \\(n\\) be the element count of `cars`. Then:
- Time Complexity: worst-case \\(O(n \log n)\\)
- Space Complexity: worst-case \\(O(n)\\)

### [84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/description/)

#### Solution

```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        stack = []
        result = 0

        for i in range(len(heights)):
            while stack and heights[stack[-1]] >= heights[i]:
                current_height = heights[stack.pop()]
                left_pile_bound = stack[-1] + 1 if stack else 0
                right_pile_bound = i - 1
                current_width = right_pile_bound - left_pile_bound + 1
                result = max(result, current_height * current_width)
            stack.append(i)

        while stack:
            current_height = heights[stack.pop()]
            left_pile_bound = stack[-1] + 1 if stack else 0
            right_pile_bound = len(heights) - 1
            current_width = right_pile_bound - left_pile_bound + 1
            result = max(result, current_height * current_width)

        return result
```

#### Complexity Analysis

Let \\(n\\) be the element count of `heights`. Then:
- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(n)\\)

## Binary Search Problems

### [704. Binary Search](https://leetcode.com/problems/binary-search/)

#### Solution

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        low = 0
        high = len(nums) - 1

        while low <= high:
            mid = (low + high) // 2
            if nums[mid] < target:
                low = mid + 1
            elif nums[mid] > target:
                high = mid - 1
            else:
                return mid

        return -1
```

#### Complexity Analysis

Let \\(n\\) be the element count of `nums`. Then:
- Time Complexity: worst-case \\(O(\log n)\\)
- Space Complexity: worst-case \\(O(1)\\)

### [74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)

#### Solution

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        ROWS = len(matrix)
        COLS = len(matrix[0])
        low = 0
        high = ROWS * COLS - 1

        while low <= high:
            mid = (low + high) // 2
            row = mid // COLS
            col = mid % COLS
            if matrix[row][col] < target:
                low = mid + 1
            elif matrix[row][col] > target:
                high = mid - 1
            else:
                return True

        return False
```

#### Complexity Analysis

Let \\(m\\) be the element count of `matrix`, and \\(n\\) be the element count of `matrix[i]` for \\(i \in 1, 2, \dots, m\\). Then:
- Time Complexity: worst-case \\(O(\log (m \times n))\\)
- Space Complexity: worst-case \\(O(1)\\)

### [875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/description/)

#### Solution

```python
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        def is_valid(k):
            hours = 0
            for pile in piles:
                hours += math.ceil(pile / k)
            return hours <= h

        low = 1
        high = max(piles)

        while low <= high:
            mid = (low + high) // 2
            if is_valid(mid):
                high = mid - 1
            else:
                low = mid + 1

        return low
```

#### Complexity Analysis

Let \\(m\\) be the largest possible \\(k\\), and \\(n\\) be the element count of `piles`. Then:
- Time complexity: worst-case \\(O(n \log m)\\)
- Space complexity: worst-case \\(O(1)\\)

### [153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)

#### Solution

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        low = 0
        high = len(nums) - 1

        while low < high:
            mid = (low + high) // 2
            if nums[mid] > nums[high]:
                low = mid + 1
            else:
                high = mid

        return nums[low]
```

#### Complexity Analysis

Let \\(n\\) be the count of `nums`. Then:
- Time Complexity: worst-case \\(O(\log n)\\)
- Space Complexity: worst-case \\(O(1)\\)

### [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)

#### Solution

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        low = 0
        high = len(nums) - 1

        while low <= high:
            mid = (low + high) // 2

            if nums[mid] == target:
                return mid

            if nums[low] <= nums[mid]:
                if nums[low] <= target and target < nums[mid]:
                    high = mid - 1
                else:
                    low = mid + 1
            else:
                if nums[mid] < target and target <= nums[high]:
                    low = mid + 1
                else:
                    high = mid - 1

        return -1
```

#### Complexity Analysis

Let \\(n\\) be the count of `nums`. Then:
- Time Complexity: worst-case \\(O(\log n)\\)
- Space Complexity: worst-case \\(O(1)\\)

### [981. Time Based Key-Value Store](https://leetcode.com/problems/time-based-key-value-store/description/)

#### Solution

```python
from collections import defaultdict

class TimeMap:

    def __init__(self):
        self.data = defaultdict(list)

    def set(self, key: str, value: str, timestamp: int) -> None:
        self.data[key].append((value, timestamp))

    def get(self, key: str, timestamp: int) -> str:
        values = self.data[key]
        low = 0
        high = len(values)

        while low < high:
            mid = (low + high) // 2
            if values[mid][1] <= timestamp:
                low = mid + 1
            else:
                high = mid

        return values[low - 1][0] if low > 0 else ""


# Your TimeMap object will be instantiated and called as such:
# obj = TimeMap()
# obj.set(key,value,timestamp)
# param_2 = obj.get(key,timestamp)
```

#### Complexity Analysis

Let \\(m\\) be the number of `set` function calls, \\(n\\) the number of `get` function calls, and `l` be the average element count of key and value strings. Then:
- Time Complexity:
    - `set(...)`: worst-case \\(O(m \cdot l)\\)
    - `get(...)`: worst-case \\(O(n \cdot (l \cdot \log m))\\)
- Space Complexity: worst-case \\(O(m \cdot l)\\)

### [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/description/)

#### Solution

The goal is to find the correct *partition* of both arrays since with a correct partition, the median is simply the the largest element on the left when the total is *odd*, or the average of the largest on the left and smallest on the right when the total number of elements is *even*.

A partition is correct when *everything on the left is smaller than everything on the right* across *both* arrays.

For instance, given `nums1 = [1, 3, 5]` and `nums2 = [2, 4, 6]`, acorrect partition is:

```
nums1:  1  3  |  5
nums2:  2     |  4  6
```

The idea is to binary search over the *position of the dividing line* in the smaller list, since once that's fixed, the position of the dividing line in the larger array is determined automatically (i.e., both left piles together must contain exactly half of all elements, leaving no freedom in where the second dividing line goes).

We then adjust accordingly the dividing line in the smaller array based on the values of the *boundaries* (i.e., the largest value on each left pile, `nums1_left_pile_max` and `nums2_left_pile_max`, and the smallest value on each right pile, `nums1_right_pile_min` and `nums2_right_pile_min`) given that each list is already sorted:
- If `nums1_left_pile_max <= nums2_right_pile_min` (since `nums1_left_pile_max <= nums1_right_pile_min` is always true) and `nums2_left_pile_max <= nums1_right_pile_min` (since `nums2_left_pile_max <= nums2_right_pile_min` is always true): it is a correct partition.
- If `nums1_left_pile_max > nums2_right_pile_min`: the left pile of `nums1`  has a value that's too large, so we decrement the `nums1_left_pile_count` by 1.
- Otherwise: the left pile of `nums2`'s left pile has a value that's too large, so we decrement the `nums1_left_pile_count` by 1.

```python
import math

class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        # set `nums1` to be the smaller list.
        # goal is to binary search on the smallest list
        if len(nums1) > len(nums2):
            nums1, nums2 = nums2, nums1

        low = 0 # represents no elements can go in `nums1`'s left pile
        high = len(nums1) # represents all elements can go in `nums1`' left pile

        while low <= high:
            nums1_left_pile_count = (low + high) // 2
            # If the total is odd, you want the left pile to have one more element than the right (that way the median is simply the largest element on the left)
            nums2_left_pile_count = (len(nums1) + len(nums2) + 1) // 2 - nums1_left_pile_count

            nums1_left_pile_max = nums1[nums1_left_pile_count - 1] if nums1_left_pile_count > 0 else -math.inf
            nums1_right_pile_min = nums1[nums1_left_pile_count] if nums1_left_pile_count < len(nums1) else math.inf
            nums2_left_pile_max = nums2[nums2_left_pile_count - 1] if nums2_left_pile_count > 0 else -math.inf
            nums2_right_pile_min = nums2[nums2_left_pile_count] if nums2_left_pile_count < len(nums2) else math.inf

            if nums1_left_pile_max <= nums2_right_pile_min and nums2_left_pile_max <= nums1_right_pile_min:
                return (max(nums1_left_pile_max, nums2_left_pile_max) + min(nums1_right_pile_min, nums2_right_pile_min)) / 2 if (len(nums1) + len(nums2)) % 2 == 0 else max(nums1_left_pile_max, nums2_left_pile_max)
            elif nums1_left_pile_max > nums2_right_pile_min:
                high = nums1_left_pile_count - 1
            else:
                low = nums1_left_pile_count + 1
```

#### Complexity Analysis

Let \\(m\\) be the size of `nums1` and \\(n\\) be the size of  `nums2`. Then:

- Time Complexity: worst-case \\(O(\log(min(m, n)))\\)
- Space Complexity: worst-case \\(O(1)\\)

## Sliding Window Problems

### [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)

#### Solution

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        left = 0
        result = 0

        for right in range(len(prices)):
            if prices[right] < prices[left]:
                left = right
            result = max(result, prices[right] - prices[left])

        return result
```

#### Complexity Analysis

Let \\(n\\) be the size of `prices`. Then:

- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(1)\\)

### [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

#### Solution

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        left = 0
        last_seen = dict()
        result = 0

        for right in range(len(s)):
            if s[right] in last_seen and last_seen[s[right]] >= left:
                left = last_seen[s[right]] + 1
            last_seen[s[right]] = right
            result = max(result, right - left + 1)

        return result
```

#### Complexity Analysis

Let \\(n\\) be the count of `s` and \\(m\\) be the number of distinct characters in the input's alphabet. Then:

- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(min(n, m))\\)

### [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)

#### Solution

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        freq = dict()
        max_freq = 0
        left = 0
        result = 0

        for right in range(len(s)):
            freq[s[right]] = freq.get(s[right], 0) + 1
            max_freq = max(max_freq, freq[s[right]])

            chars_to_replace = (right - left + 1) - max_freq
            if chars_to_replace > k:
                freq[s[left]] -= 1
                left += 1

            result = max(result, right - left + 1)

        return result
```

#### Complexity Analysis

Let \\(n\\) be the count of `s`, and  \\(m\\) be the number of distinct characters in the input's alphabet. Then:

- Time Complexity: worst-case \\(O(n)\\)
- Space Complexity: worst-case \\(O(m)\\)

### [567. Permutation in String](https://leetcode.com/problems/permutation-in-string/description/)

#### Solution

```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        ALPHABET_COUNT = 26

        if len(s1) > len(s2):
            return False

        s1_char_freq = [0] * ALPHABET_COUNT
        s2_char_freq = [0] * ALPHABET_COUNT

        for i in range(len(s1)):
            s1_char_freq[ord(s1[i]) - ord('a')] += 1
            s2_char_freq[ord(s2[i]) - ord('a')] += 1

        freq_matches = 0
        for i in range(ALPHABET_COUNT):
            if s1_char_freq[i] == s2_char_freq[i]:
                freq_matches += 1

        for right in range(len(s1), len(s2)):
            if freq_matches == ALPHABET_COUNT:
                return True

            r = ord(s2[right]) - ord('a')
            s2_char_freq[r] += 1
            if s2_char_freq[r] == s1_char_freq[r]:
                freq_matches += 1
            elif s2_char_freq[r] == s1_char_freq[r] + 1:
                freq_matches -= 1

            l = ord(s2[right - len(s1)]) - ord('a')
            s2_char_freq[l] -= 1
            if s2_char_freq[l] == s1_char_freq[l]:
                freq_matches += 1
            elif s2_char_freq[l] == s1_char_freq[l] - 1:
                freq_matches -= 1

        return freq_matches == ALPHABET_COUNT
```

#### Complexity Analysis

Let \\(l_1\\) be the length of `s1`, and  \\(l_2\\) be the length of `s2`. Then:

- Time Complexity: worst-case \\(O(l_2)\\)
- Space Complexity: worst-case \\(O(1)\\)

### [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/description/)

#### Solution

```python
from collections import Counter

class Solution:
    def minWindow(self, s: str, t: str) -> str:
        left = 0
        required = Counter(t)
        current = dict()
        satisfied = 0    
        result = ""

        for right in range(len(s)):
            current[s[right]] = current.get(s[right], 0) + 1
            if s[right] in required and current[s[right]] == required[s[right]]:
                satisfied += 1

            while satisfied == len(required):
                window = s[left:right + 1]
                if not result or len(window) < len(result):
                    result = window

                current[s[left]] -= 1
                if s[left] in required and current[s[left]] < required[s[left]]:
                    satisfied -= 1
                    
                left += 1

        return result
```

#### Complexity Analysis

Let \\(s\\) and \\(t\\) be the length of the strings `s` and `t` respectively. Then:

- Time Complexity: \\(O(s + t)\\)
- Space Complexity: \\(O(s + t)\\)