![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2419. [Longest Subarray With Maximum Bitwise AND](https://leetcode.com/problems/longest-subarray-with-maximum-bitwise-and)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn longest_subarray(nums: Vec<i32>) -> i32 {
        let value_maximum: i32 = *nums.iter().max().unwrap();
        let mut cumulative_amount: i32 = 0;
        let mut result: i32 = 0;
        for num in nums {
            if num == value_maximum {
                cumulative_amount += 1;
            } else {
                cumulative_amount = 0;
            }

            result = i32::max(result, cumulative_amount);
        }

        return result
    }
}
```
