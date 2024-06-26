![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1438. [Longest Continuous Subarray With Absolute Diff Less Than Or Equal To Limit](https://leetcode.com/problems/longest-continuous-subarray-with-absolute-diff-less-than-or-equal-to-limit)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```rust
use std::collections::BinaryHeap;

impl Solution {
    pub fn longest_subarray(nums: Vec<i32>, limit: i32) -> i32 {
        let mut result: i32 = 0;
        let mut heap_min: BinaryHeap<(i32, usize)> = BinaryHeap::new();
        let mut heap_max: BinaryHeap<(i32, usize)> = BinaryHeap::new();
        let mut left: usize = 0;
        let mut right: usize = nums.len() - 1;
        for right in 0..nums.len() {
            heap_min.push((-nums[right], right));
            heap_max.push((nums[right], right));

            while (*heap_max.peek().unwrap()).0 + (*heap_min.peek().unwrap()).0 > limit {
                left = usize::min((*heap_max.peek().unwrap()).1, (*heap_min.peek().unwrap()).1) + 1;
                while (*heap_max.peek().unwrap()).1 < left {
                    heap_max.pop();
                }
                while (*heap_min.peek().unwrap()).1 < left {
                    heap_min.pop();
                }
            }

            result = i32::max(result, (right - left + 1) as i32);
        }

        return result
    }
}
```

### Solution :

Method 1 (Sliding Window + Binary Search, ERROR: "Time Limit Exceeded", 56/61, Time Complexity: $O(N^2*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def longestSubarray(self, nums: List[int], limit: int) -> int:
        n = len(nums)
        left = 1
        right = n
        while left <= right:
            middle = left + (right - left)//2
            result = False
            ordered = []
            for index in range(n):
                bisect.insort_left(ordered, nums[index])
                if index >= middle:
                    index_remove = bisect.bisect_left(ordered, nums[index-middle])
                    ordered.pop(index_remove)

                if index >= middle-1 and ordered[-1]-ordered[0] <= limit:
                    result = True
                    break

            if result:
                left = middle + 1
            else:
                right = middle - 1

        return right
```

Method 2 (Sliding Window + Binary Heap, Time Complexity: $O(N*(Log(N))^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def longestSubarray(self, nums: List[int], limit: int) -> int:
        n = len(nums)
        left = 1
        right = n
        while left <= right:
            middle = left + (right - left)//2
            heap_max = []
            heap_min = []
            result = False
            for index in range(n):
                heapq.heappush(heap_max, (-nums[index], index))
                heapq.heappush(heap_min, (nums[index], index))
                if index >= middle:
                    while heap_max[0][1] <= index-middle:
                        heapq.heappop(heap_max)
                    while heap_min[0][1] <= index-middle:
                        heapq.heappop(heap_min)

                if index >= middle-1 and -heap_max[0][0]-heap_min[0][0] <= limit:
                    result = True
                    break

            if result:
                left = middle + 1
            else:
                right = middle - 1

        return right
```

Method 3 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def longestSubarray(self, nums: List[int], limit: int) -> int:
        n = len(nums)
        heap_max = []
        heap_min = []
        result = 0
        left = 0
        for right in range(n):
            heapq.heappush(heap_max, (-nums[right], right))
            heapq.heappush(heap_min, (nums[right], right))

            while -heap_max[0][0]-heap_min[0][0] > limit:
                left = min(heap_max[0][1], heap_min[0][1]) + 1
                while heap_max[0][1] < left:
                    heapq.heappop(heap_max)
                while heap_min[0][1] < left:
                    heapq.heappop(heap_min)

            result = max(result, right - left + 1)

        return result
```
