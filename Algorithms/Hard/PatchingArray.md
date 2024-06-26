![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 330. [Patching Array](https://leetcode.com/problems/patching-array)

### Solution :

[Method 1](https://leetcode.com/problems/patching-array/solutions/78488/solution-explanation) :
```rust
impl Solution {
    pub fn min_patches(nums: Vec<i32>, target: i32) -> i32 {
        let n: usize = nums.len();
        let mut index: usize = 0;
        let mut result: i32 = 0;
        let mut miss: i64 = 1;
        while miss <= target as i64 {
            if index < n && nums[index] as i64 <= miss {
                miss += nums[index] as i64;
                index += 1;
            } else {
                miss += miss;
                result += 1;
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$ (N: value of `n`), Space Complexity: $O(1)$) :
```python
class Solution:
    def minPatches(self, nums: List[int], target: int) -> int:
        n = len(nums)
        result = 0
        index = 0
        miss = 1
        while miss <= target:
            if index < n and nums[index] <= miss:
                miss += nums[index]
                index += 1
            else:
                miss += miss
                result += 1

        return result
```

Method 2 (Prefix Sum, Time Complexity: $O(N)$ (N: value of `n`), Space Complexity: $O(1)$) :
```python
class Solution:
    def minPatches(self, nums: List[int], n: int) -> int:
        index = 0
        prefix_sum = 0
        result = 0
        while prefix_sum < n:
            if index < len(nums) and nums[index] <= prefix_sum+1:
                prefix_sum += nums[index]
                index += 1
            else:
                prefix_sum = prefix_sum*2 + 1
                result += 1

        return result
```
