![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3392. [Count Subarrays Of Length Three With A Condition](https://leetcode.com/problems/count-subarrays-of-length-three-with-a-condition)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn count_subarrays(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut result: i32 = 0;
        for index in 0..n-2 {
            let sum: i32 = nums[index] + nums[index+2];
            if nums[index+1]%2 == 0 && sum == nums[index+1]/2 {
                result += 1;
            }
        }

        return result
    }
}
```
