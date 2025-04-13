![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1922. [Count Good Numbers](https://leetcode.com/problems/count-good-numbers)

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded", 69/166, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the value of `n`)) :
```rust
impl Solution {
    const MOD: i64 = 1_000_000_007;

    pub fn count_good_numbers(n: i64) -> i32 {
        let mut result: i64 = 5;
        let mut current_n: i64 = 1;
        while current_n < n {
            result = (result * match current_n%2 == 1 {
                true => 4,
                _ => 5,
            }) % Self::MOD;

            current_n += 1;
        }

        return result as i32
    }
}
```
