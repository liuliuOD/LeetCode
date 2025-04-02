![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2873. [Maximum Value Of An Ordered Triplet I](https://leetcode.com/problems/maximum-value-of-an-ordered-triplet-i)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^3)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn maximum_triplet_value(nums: Vec<i32>) -> i64 {
        let n: usize = nums.len();
        let mut result: i64 = 0;
        for index_i in 0..n {
            for index_j in index_i+1..n {
                for index_k in index_j+1..n {
                    result = i64::max(result, (nums[index_i] as i64 - nums[index_j] as i64)*nums[index_k] as i64);
                }
            }
        }

        return result
    }
}
```
