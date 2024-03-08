![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 239. [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum)

### Solution :

Method 1 (Monotonic Queue) :
```rust
use std::collections::VecDeque;
impl Solution {
    pub fn max_sliding_window(nums: Vec<i32>, k: i32) -> Vec<i32> {
        let k: usize = k as usize;
        let mut result: Vec<i32> = vec![];
        let mut dequeue: VecDeque<usize> = VecDeque::new();
        for index in 0..nums.len() {
            // need to check if index >= k, otherwise index-k would overflow
            while dequeue.len() > 0 && index >= k && dequeue[0] <= index-k {
                dequeue.pop_front();
            }
            while dequeue.len() > 0 && nums[dequeue[dequeue.len()-1]] < nums[index] {
                dequeue.pop_back();
            }

            dequeue.push_back(index);

            if index < k-1 {
                continue;
            }

            result.push(nums[dequeue[0]]);
        }

        return result
    }
}
```

### Solution :

Method 1 (Sliding Window, ERROR: "Time Limit Exceeded", 49/51) :
```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        result = []
        window = defaultdict(int)
        maximum = 0
        for index in range(len(nums)):
            num = nums[index]
            window[num] += 1
            maximum = max(maximum, num)
            if index < k-1:
                continue

            if index >= k:
                num_left = nums[index-k]
                window[num_left] -= 1
                if num_left == maximum and window[num_left] == 0:
                    maximum = max(nums[index-k+1:index+1])

            result.append(maximum)

        return result
```

Method 2 (Monotonic Queue) :
```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        result = []
        queue = deque()
        for index in range(len(nums)):
            # remove values at right-side of the dequeue, smaller than current `num`
            while queue and nums[queue[-1]] < nums[index]:
                queue.pop()

            # remove items that out-side of sliding window
            while queue and queue[0] <= index-k:
                queue.popleft()

            queue.append(index)

            if index < k-1:
                continue

            result.append(nums[queue[0]])

        return result
```
