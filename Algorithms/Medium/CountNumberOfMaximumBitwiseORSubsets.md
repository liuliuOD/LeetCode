![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2044. [Count Number Of Maximum Bitwise-OR Subsets](https://leetcode.com/problems/count-number-of-maximum-bitwise-or-subsets)

### Solution :

Method 1 (Bitmask, Time Complexity: $O(N*2^N)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn count_max_or_subsets(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let maximum_or_num: i32 = nums.iter().fold(0, |acc, num| acc | *num);
        let mut result: i32 = 0;
        for bitmask in 0..2i32.pow(n as u32) {
            let mut current_or_num: i32 = 0;
            for index in 0..n {
                if 1<<index & bitmask == 0 {
                    continue;
                }

                current_or_num |= nums[index];
            }

            if current_or_num == maximum_or_num {
                result += 1;
            }
        }

        return result
    }
}
```
