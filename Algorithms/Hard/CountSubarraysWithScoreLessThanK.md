![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2302. [Count Subarrays With Score Less Than K](https://leetcode.com/problems/count-subarrays-with-score-less-than-k)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn count_subarrays(nums: Vec<i32>, k: i64) -> i64 {
        let n: usize = nums.len();
        let mut left: usize = 0;
        let mut right: usize = 0;
        let mut sum: i64 = 0;
        let mut result: i64 = 0;
        while right < n {
            sum += nums[right] as i64;
            while left <= right && sum*(right-left+1) as i64 >= k {
                sum -= nums[left] as i64;
                left += 1;
            }

            result += (right-left+1) as i64;
            right += 1;
        }

        return result
    }
}
```
