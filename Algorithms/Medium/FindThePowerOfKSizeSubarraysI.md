![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3254. [Find The Power Of K-Size Subarrays I](https://leetcode.com/problems/find-the-power-of-k-size-subarrays-i)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N*K)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`, K: the value of `k`)):
```rust
impl Solution {
    pub fn results_array(nums: Vec<i32>, k: i32) -> Vec<i32> {
        let k: usize = k as usize;
        let n: usize = nums.len();
        let mut result: Vec<i32> = Vec::new();
        for index_start in 0..=n-k {
            let mut is_valid: bool = true;
            let mut maximum: i32 = nums[index_start];
            for offset in 1..k {
                maximum = i32::max(maximum, nums[index_start+offset]);
                if nums[index_start+offset-1] > nums[index_start+offset] || (nums[index_start+offset]-nums[index_start+offset-1]) != 1 {
                    is_valid = false;
                    break;
                }
            }

            if is_valid {
                result.push(maximum);
            } else {
                result.push(-1);
            }
        }

        return result
    }
}
```
