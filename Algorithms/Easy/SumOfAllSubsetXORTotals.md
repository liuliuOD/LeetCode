![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1863. [Sum Of All Subset XOR Totals](https://leetcode.com/problems/sum-of-all-subset-xor-totals)

### Solution :

Method 1 (Bit Mask, Time Complexity: $O(2^N)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn subset_xor_sum(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut result: i32 = 0;
        for mask in 1..=i32::pow(2, n as u32) {
            let mut xor: i32 = 0;
            for index in 0..n {
                if (mask >> index) & 1 == 0 {
                    continue;
                }

                xor ^= nums[index];
            }

            result += xor;
        }

        return result
    }
}
```
