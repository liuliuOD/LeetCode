![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2501. [Longest Square Streak In An Array](https://leetcode.com/problems/longest-square-streak-in-an-array)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn longest_square_streak(mut nums: Vec<i32>) -> i32 {
        let mut visited: HashSet<i64> = HashSet::from_iter(nums.iter().map(|num| *num as i64));
        nums.sort();
        let maximum: i64 = *nums.last().unwrap() as i64;
        let mut result: i32 = -1;
        for num in nums {
            let mut current: i64 = num as i64;
            let mut current_length: i32 = 1;
            while current < maximum && visited.contains(&(i64::pow(current, 2))) {
                current_length += 1;
                current = i64::pow(current, 2);
                result = i32::max(result, current_length);
            }
        }

        return result
    }
}
```
