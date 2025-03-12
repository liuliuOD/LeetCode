![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2529. [Maximum Count Of Positive Integer And Negative Integer](https://leetcode.com/problems/maximum-count-of-positive-integer-and-negative-integer)

### Solution :

Method 1 (Brute Force + Optimization, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn maximum_count(nums: Vec<i32>) -> i32 {
        let n: i32 = nums.len() as i32;
        let mut amount_negative: i32 = 0;
        let mut amount_positive: i32 = 0;
        for (index, num) in nums.into_iter().enumerate() {
            if num < 0 {
                amount_negative += 1;
            } else if num > 0 {
                amount_positive = n - index as i32;
                break;
            }
        }

        return i32::max(amount_negative, amount_positive)
    }
}
```
