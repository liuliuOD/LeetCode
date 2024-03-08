![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2909. [Minimum Sum Of Mountain Triplets II](https://leetcode.com/problems/minimum-sum-of-mountain-triplets-ii)

### Solution :

Method 1 (In weekly contest 368, Prefix Sum + Suffix Sum) :
```python
class Solution:
    def minimumSum(self, nums: List[int]) -> int:
        n = len(nums)

        # Prefix Sum
        minimum_left = [None] * n
        for index in range(n):
            if index > 0 and (nums[index-1] < nums[index] or (minimum_left[index-1] and minimum_left[index-1] < nums[index])):
                minimum_left[index] = min(nums[index-1], minimum_left[index-1] if minimum_left[index-1] else inf)

        # Suffix Sum
        minimum_right = [None] * n
        for index in reversed(range(n)):
            if index+1 < n and (nums[index+1] < nums[index] or (minimum_right[index+1] and minimum_right[index+1] < nums[index])):
                minimum_right[index] = min(nums[index+1], minimum_right[index+1] if minimum_right[index+1] else inf)

        result = inf
        for index in range(1, n-1):
            if minimum_left[index] is None or minimum_right[index] is None:
                continue

            result = min(result, minimum_left[index]+minimum_right[index]+nums[index])

        return -1 if result == inf else result
```

Method 2 (Prefix Sum + Suffix Sum) :
```python
class Solution:
    def minimumSum(self, nums: List[int]) -> int:
        n = len(nums)
        minimum_left = [inf] * n
        # Option 1
        for index in range(n):
            if index-1 >= 0 and (nums[index-1] < nums[index] or minimum_left[index-1] < nums[index]):
        """
        # Option 2

        for index in range(1, n):
            if nums[index] > nums[index-1] or nums[index] > minimum_left[index-1]:
        """
                minimum_left[index] = min(nums[index-1], minimum_left[index-1])

        minimum_right = [inf] * n
        # Option 1
        for index in reversed(range(n)):
            if index+1 < n and (nums[index+1] < nums[index] or minimum_right[index+1] < nums[index]):
        """
        # Option 2

        for index in reversed(range(n-1)):
            if nums[index] > nums[index+1] or nums[index] > minimum_right[index+1]:
        """
                minimum_right[index] = min(nums[index+1], minimum_right[index+1])

        result = inf
        for index in range(1, n-1):
            result = min(result, minimum_left[index]+minimum_right[index]+nums[index])

        return -1 if result == inf else result
```

### Solution :

Method 1 (Prefix Sum + Suffix Sum) :
```rust
impl Solution {
    pub fn minimum_sum(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut prefix_sum: Vec<i32> = vec![i32::MAX; n];
        for index in 1..n {
            if prefix_sum[index-1] < nums[index] || nums[index-1] < nums[index] {
                prefix_sum[index] = prefix_sum[index-1].min(nums[index-1]);
            }
        }

        let mut suffix_sum: Vec<i32> = vec![i32::MAX; n];
        for index in (0..n-1).rev() {
            if suffix_sum[index+1] < nums[index] || nums[index+1] < nums[index] {
                suffix_sum[index] = suffix_sum[index+1].min(nums[index+1]);
            }
        }

        let mut result: i32 = i32::MAX;
        for index in 1..n-1 {
            if prefix_sum[index] == i32::MAX || suffix_sum[index] == i32::MAX {
                continue;
            }

            result = result.min(prefix_sum[index]+nums[index]+suffix_sum[index]);
        }

        return match result {
            i32::MAX => -1,
            _ => result,
        }
    }
}
```
