![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3335. [Total Characters In String After Transformations I](https://leetcode.com/problems/total-characters-in-string-after-transformations-i)

### Solution :

Method 1 (DFS, Time Complexity: $O(N*2^T)$, Space Complexity: $O(N*T)$ (N: the number of the elements in `s`, T: the value of `t`)) :
```rust
impl Solution {
    const TOTAL: u8 = 25;
    const BASE: u8 = b'a';
    const MODULO: i32 = 1_000_000_007;

    pub fn length_after_transformations(s: String, t: i32) -> i32 {
        let mut result: i32 = 0;
        for &ascii in s.as_bytes() {
            let offset: u8 = ascii - Self::BASE;
            result += Self::calculate_replaced_length(offset, t);
        }

        return result
    }

    fn calculate_replaced_length(offset: u8, t: i32) -> i32 {
        let used_t: i32 = (Self::TOTAL - offset) as i32;
        if used_t >= t {
            return 1
        }

        return Self::calculate_replaced_length(0, t-used_t) + Self::calculate_replaced_length(1, t-used_t)
    }
}
```

Method 2 (DFS + Memoization, Time Complexity: $O(N*T)$, Space Complexity: $O(T)$ (N: the number of the elements in `s`, T: the value of `t`)) :
```rust
use std::collections::HashMap;

impl Solution {
    const TOTAL: u8 = 25;
    const BASE: u8 = b'a';
    const MODULO: i64 = 1_000_000_007;

    pub fn length_after_transformations(s: String, t: i32) -> i32 {
        let mut memoization: HashMap<(u8, i32), i64> = HashMap::new();
        let mut result: i64 = 0;
        for &ascii in s.as_bytes() {
            let offset: u8 = ascii - Self::BASE;
            result = (result + Self::calculate_replaced_length(offset, t, &mut memoization)) % Self::MODULO;
        }

        return result as i32
    }

    fn calculate_replaced_length(offset: u8, t: i32, memoization: &mut HashMap<(u8, i32), i64>) -> i64 {
        let key: (u8, i32) = (offset, t);
        if memoization.contains_key(&key) {
            return *memoization.get(&key).unwrap()
        }

        let used_t: i32 = (Self::TOTAL - offset) as i32;
        if used_t >= t {
            return 1
        }

        let result: i64 = (Self::calculate_replaced_length(0, t-used_t-1, memoization) + Self::calculate_replaced_length(1, t-used_t-1, memoization)) % Self::MODULO;
        memoization.entry(key).or_insert(result);

        return result
    }
}
```
