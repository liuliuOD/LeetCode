![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2779. [Maximum Beauty Of An Array After Applying Operation](https://leetcode.com/problems/maximum-beauty-of-an-array-after-applying-operation)

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded", 611/621) :
```rust
impl Solution {
    pub fn maximum_beauty(mut nums: Vec<i32>, k: i32) -> i32 {
        let n: usize = nums.len();
        nums.sort();
        let mut result: i32 = 1;
        for index_start in 0..n {
            for index in index_start+1..n {
                if (nums[index]-nums[index_start]) > k*2 {
                    break;
                }

                result = i32::max(result, (index-index_start+1) as i32);
            }
        }

        return result
    }
}
```

Method 2 (Two Pointer, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn maximum_beauty(mut nums: Vec<i32>, k: i32) -> i32 {
        let n: usize = nums.len();
        nums.sort();
        let mut result: i32 = 1;
        let mut left: usize = 0;
        let mut right: usize = 0;
        while left < n && right < n {
            if nums[right]-nums[left] > 2*k {
                left += 1;
                continue;
            }

            result = i32::max(result, (right-left+1) as i32);
            right += 1;
        }

        return result
    }
}
```

### Solution :

Method 1 (Two Pointer) :
```python
class Solution:
    def maximumBeauty(self, nums: List[int], k: int) -> int:
        n = len(nums)
        pointer_left = 0
        pointer_right = 0
        result = 0
        nums.sort()
        while pointer_left < n and pointer_right < n:
            if nums[pointer_right]-nums[pointer_left] > k*2:
                pointer_left += 1
                continue

            result = max(result, pointer_right-pointer_left+1)
            pointer_right += 1
        return result
```
