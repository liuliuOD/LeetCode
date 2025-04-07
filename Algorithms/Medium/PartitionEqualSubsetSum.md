![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 416. [Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum)

### Solution :

Method 1 (Brute Force, ERROR: "Memory Limit Exceeded", 37/144, Time Complexity: $O(2^N)$, Space Complexity: $O(2^N)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn can_partition(nums: Vec<i32>) -> bool {
        let mut summarize: i64 = nums.iter().map(|num| *num as i64).sum();
        if summarize % 2 == 1 {
            return false
        }

        let mut candidates: Vec<i64> = Vec::new();
        for num in nums {
            if num as i64 == summarize/2 {
                return true
            }

            for index in 0..candidates.len() {
                let candidate: i64 = candidates[index];
                if candidate+num as i64 == summarize/2 {
                    return true
                }

                candidates.push(candidate + num as i64);
            }

            candidates.push(num as i64);
        }

        return false
    }
}
```
