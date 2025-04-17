![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2176. [Count Equal And Divisible Pairs In An Array](https://leetcode.com/problems/count-equal-and-divisible-pairs-in-an-array)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn count_pairs(nums: Vec<i32>, k: i32) -> i32 {
        let n: usize = nums.len();
        let mut result: i32 = 0;
        for index in 0..n {
            let num: i32 = nums[index];
            for index_right in index+1..n {
                let right: i32 = nums[index_right];
                if num != right {
                    continue;
                }

                let multiple: usize = index * index_right;
                if multiple%(k as usize) != 0 {
                    continue;
                }

                result += 1;
            }
        }

        return result
    }
}
```
