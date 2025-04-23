![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1399. [Count Largest Group](https://leetcode.com/problems/count-largest-group)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the value of `n`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn count_largest_group(n: i32) -> i32 {
        let mut counter: HashMap<i32, i32> = HashMap::new();
        for mut num in 1..=n {
            let mut sum_digits: i32 = 0;
            while num > 0 {
                sum_digits += num % 10;
                num /= 10;
            }

            counter.entry(sum_digits).and_modify(|amount| *amount += 1).or_insert(1);
        }

        let largest_size: i32 = *counter.values().max().unwrap();
        return counter.values().filter(|size| **size == largest_size).count() as i32
    }
}
```
