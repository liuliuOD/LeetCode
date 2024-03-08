![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 561. [Array Partition](https://leetcode.com/problems/array-partition)

### Solution :

Method 1 (Built-In Sort) :
```rust
impl Solution {
    pub fn array_pair_sum(mut nums: Vec<i32>) -> i32 {
        nums.sort();

        /* Option 1 */
        let mut result: i32 = 0;
        let mut index: usize = 0;
        while index < nums.len() {
            result += nums[index];
            index += 2;
        }

        return result
        /* Option 2

        return nums.into_iter().step_by(2).reduce(|a, b| a + b).unwrap()
        */
        /* Option 3

        return nums.iter().step_by(2).fold(0, |a, b| a + b)
        */
    }
}
```

Method 2 (Binary Heap) :
```rust
use std::cmp::Reverse;
use std::collections::BinaryHeap;
impl Solution {
    pub fn array_pair_sum(nums: Vec<i32>) -> i32 {
        let mut heap: BinaryHeap<Reverse<i32>> = BinaryHeap::from(nums.iter().map(|&value| Reverse(value)).collect::<Vec<Reverse<i32>>>());
        let mut result: i32 = 0;
        while !heap.is_empty() {
            result += heap.pop().unwrap().0;
            heap.pop();
        }

        return result
    }
}
```

### Solution :

Method 1 (Built-In Sort, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def arrayPairSum(self, nums: List[int]) -> int:
        nums.sort()
        result = 0
        index = 0
        while index < len(nums):
            result += nums[index]
            index += 2

        return result
```

Method 2 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def arrayPairSum(self, nums: List[int]) -> int:
        heapq.heapify(nums)
        result = 0
        while len(nums) > 1:
            result += heapq.heappop(nums)
            heapq.heappop(nums)

        return result
```

Method 3 (Counting Sort like) :
```python
class Solution:
    def arrayPairSum(self, nums: List[int]) -> int:
        sorted_nums = self.countingSort(nums)
        result = 0
        index = 0
        while index < len(nums):
            result += sorted_nums[index]
            index += 2

        return result

    def countingSort(self, nums: List[int]) -> List[int]:
        prefix_sum = defaultdict(int)
        for num in nums:
            prefix_sum[num] += 1

        keys = sorted(prefix_sum.keys())
        for index in range(1, len(keys)):
            prefix_sum[keys[index]] += prefix_sum[keys[index-1]]

        n = len(nums)
        sorted_nums = [0] * n
        for index in reversed(range(n)):
            prefix_sum[nums[index]] -= 1
            sorted_nums[prefix_sum[nums[index]]] = nums[index]

        return sorted_nums
```
