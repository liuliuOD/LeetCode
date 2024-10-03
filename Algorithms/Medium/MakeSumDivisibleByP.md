![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1590. [Make Sum Divisible By P](https://leetcode.com/problems/make-sum-divisible-by-p)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(P)$ (N: the number of the elements in `nums`, P: the value of `p`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn min_subarray(nums: Vec<i32>, p: i32) -> i32 {
        let n: usize = nums.len();
        let mut remaining_total: i32 = 0;
        for &num in nums.iter() {
            remaining_total = (remaining_total + num) % p;
        }

        if remaining_total == 0 {
            return 0
        }

        let mut remaining_mapping: HashMap<i32, i32> = HashMap::from([(0, -1)]);
        let mut remaining_cumulative: i32 = 0;
        let mut result: i32 = n as i32;
        for index in 0..n {
            remaining_cumulative = (remaining_cumulative + nums[index]) % p;

            let remaining_opposite: i32 = (p + remaining_cumulative - remaining_total) % p;
            if remaining_mapping.contains_key(&remaining_opposite) {
                result = i32::min(result, index as i32 - remaining_mapping[&remaining_opposite]);
            }

            remaining_mapping.entry(remaining_cumulative).and_modify(|value| *value = index as i32).or_insert(index as i32);
        }

        if result == n as i32 {
            return -1
        }
        return result
    }
}
```
