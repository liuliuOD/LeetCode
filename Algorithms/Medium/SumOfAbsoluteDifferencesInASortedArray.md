![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1685. [Sum Of Absolute Differences In A Sorted Array](https://leetcode.com/problems/sum-of-absolute-differences-in-a-sorted-array)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn get_sum_absolute_differences(nums: Vec<i32>) -> Vec<i32> {
        let n: usize = nums.len();
        let sum_total: i32 = nums.iter().sum();
        let mut sum_previous: i32 = 0;
        let mut result: Vec<i32> = vec![];
        for index in 0..n {
            let part_left: i32 = nums[index]*(index as i32) - sum_previous;
            let part_right: i32 = sum_total - sum_previous - nums[index]*((n-index) as i32);
            result.push(part_left+part_right);

            sum_previous += nums[index];
        }

        return result
    }
}
```

### Solution :

Method 1 (Prefix Sum + Binary Search, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def getSumAbsoluteDifferences(self, nums: List[int]) -> List[int]:
        n = len(nums)
        prefix_sum = [nums[0]]
        for index in range(1, n):
            prefix_sum.append(prefix_sum[index-1]+nums[index])

        result = []
        for num in nums:
            index_left = bisect.bisect_left(nums, num)
            index_right = bisect.bisect_right(nums, num)
            part_left = num*index_left - (prefix_sum[index_left-1] if index_left > 0 else 0)
            part_right = prefix_sum[n-1] - prefix_sum[index_right-1] - num*(n-index_right)
            result.append(part_left + part_right)

        return result
```

Method 2 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def getSumAbsoluteDifferences(self, nums: List[int]) -> List[int]:
        n = len(nums)
        prefix_sum = [nums[0]]
        for index in range(1, n):
            prefix_sum.append(prefix_sum[index-1]+nums[index])

        result = []
        for index, num in enumerate(nums):
            part_left = num*index - prefix_sum[index] + nums[index]
            part_right = prefix_sum[n-1] - prefix_sum[index] - num*(n-index-1)
            result.append(part_left + part_right)

        return result
```

Method 3 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def getSumAbsoluteDifferences(self, nums: List[int]) -> List[int]:
        n = len(nums)
        sum_total = sum(nums)
        sum_previous = 0
        result = []
        for index, num in enumerate(nums):
            part_left = num*index - sum_previous
            part_right = sum_total - sum_previous - num*(n-index)
            result.append(part_left+part_right)

            sum_previous += num

        return result
```
