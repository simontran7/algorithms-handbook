# Priority Queue

## Interface

```
trait PriorityQueue<T> {
    func top(&self) -> T;
    func add(&mut self, item: T);
    func remove(&mut self) -> T;
}
```

## Use Case

- Repeatedly find the maximum or minimum element
- Get the "top" \\(k\\) elements

```cpp
#include <queue>

std::vector<int> top_k(const std::vector<int>& array, int k) {
    // use a min heap to keep the largest `k` elements,
    // or a max heap to keep the smallest `k`
    std::priority_queue<std::pair<int, int>,
                        std::vector<std::pair<int, int>>,
                        std::greater<>> pq;

    for (int num : array) {
        // some logic to add an element according to problem's criteria
        pq.push({/* criteria as key */, num});
        if (pq.size() > k) {
            pq.pop();
        }
    }

    std::vector<int> result;
    while (!pq.empty()) {
        result.push_back(pq.top().second);
        pq.pop();
    }

    return result;
}
```

- Find a running/streaming median

```cpp
#include <queue>

class MedianFinder {
private:
    std::priority_queue<int, std::vector<int>, std::greater<>> min_pq;
    std::priority_queue<int> max_pq;

public:
    MedianFinder() {}

    /**
     * second/third lines maintain the invariant that all the elements in the
     * min pq are >= all the elements in the max pq
     * the `if` maintains the invariant that the max pq will store 1 more
     * element than the min pq if there are an odd number of elements
     */
    void addNum(int num) {
        max_pq.push(num);
        min_pq.push(max_pq.top());
        max_pq.pop();
        if (min_pq.size() > max_pq.size()) {
            max_pq.push(min_pq.top());
            min_pq.pop();
        }
    }

    /**
     * - If there are even numbers, then max_pq.size() == min_pq.size()
     *   (i.e., the median will be the average of the top elements)
     * - If there are odd numbers, then max_pq.size() == min_pq.size() + 1
     *   (i.e., it will have the median)
     */
    double findMedian() {
        if (max_pq.size() == min_pq.size()) {
            return (max_pq.top() + min_pq.top()) / 2.0;
        }
        return max_pq.top();
    }
};
```

## Binary Heap

A binary heap is a complete binary tree (every level fully filled except possibly the last, filled left to right) satisfying the **heap property**: every parent is \(\ge\) its children (max-heap) or \(\le\) its children (min-heap). Because the tree is always complete, it can be stored implicitly in an array with no pointers: for a node at index \(i\), its children sit at \(2i + 1\) and \(2i + 2\), and its parent at \(\lfloor (i - 1) / 2 \rfloor\).

### Lookup

The maximum (or minimum) is always at the root, so peeking at the top is just reading index \(0\) of the array.

### Insertion

Append the new element at the end of the array (the next open leaf), then **sift up**: repeatedly compare it against its parent and swap if it violates the heap property, stopping once it doesn't or it reaches the root.

### Deletion

Swap the root with the last element in the array and shrink the array by one, then **sift down** the new root: repeatedly swap it with its larger (max-heap) or smaller (min-heap) child until the heap property is restored or it reaches a leaf.

### Complexity Analysis

| Operation | Time Complexity |
| --- | --- |
| Initialize | worst-case \(O(n)\) |
| Lookup min/max | worst-case \(O(1)\) |
| Add    | worst-case \(O(\log n)\) |
| Remove | worst-case \(O(\log n)\) |

## API

### Min Priority Queue

```cpp
#include <queue>

// Create an empty min priority queue
std::priority_queue<int, std::vector<int>, std::greater<>> min_pq;

// Heapify an existing array in O(n) by constructing from iterators
std::priority_queue<int, std::vector<int>, std::greater<>> min_pq(array.begin(), array.end());

// Peek at the top element
min_pq.top();

// Get the number of elements
min_pq.size();

// Check if the priority queue is empty
min_pq.empty();

// Add an element
min_pq.push(element);

// Remove the top element (returns void!)
min_pq.pop();
```

### Max Priority Queue

```cpp
#include <queue>

// Create an empty max priority queue (max heap is the DEFAULT in C++)
std::priority_queue<int> max_pq;

// Heapify an existing array in O(n) by constructing from iterators
std::priority_queue<int> max_pq(array.begin(), array.end());

// Peek at the top element
max_pq.top();

// Get the number of elements
max_pq.size();

// Check if the priority queue is empty
max_pq.empty();

// Add an element
max_pq.push(element);

// Remove the top element (returns void!)
max_pq.pop();
```

> [!NOTE]
> To simulate an **indexed priority queue**, store pairs: `std::pair<int, int>{key, element}`, where pairs are compared lexicographically (key first, then element as tie-breaker).