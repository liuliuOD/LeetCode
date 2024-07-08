![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1823. [Find The Winner Of The Circular Game](https://leetcode.com/problems/find-the-winner-of-the-circular-game)

### Solution :

Method 1 (Simulation + Hash Set, Time Complexity: $O(N*K)$, Space Complexity: $O(N)$ (N: value of `n`, K: value of `k`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn find_the_winner(n: i32, k: i32) -> i32 {
        let mut hash_set: HashSet<i32> = HashSet::from_iter((1..=n).into_iter());
        let mut current: i32 = 0;
        let mut k_current: i32 = 0;
        while (hash_set.len() as i32) > 1 {
            current = current%n + 1;
            if !hash_set.contains(&current) {
                continue;
            }
            k_current += 1;

            if k_current == k {
                hash_set.remove(&current);
                k_current = 0;
            }
        }

        return *hash_set.iter().next().unwrap()
    }
}
```
