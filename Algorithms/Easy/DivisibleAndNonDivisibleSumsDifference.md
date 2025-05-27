![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2894. [Divisible And Non-divisible Sums Difference](https://leetcode.com/problems/divisible-and-non-divisible-sums-difference)

### Solution :

Method 1 (Greedy, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the value of `n`)) :
```rust
impl Solution {
    pub fn difference_of_sums(n: i32, m: i32) -> i32 {
        let mut result: i32 = 0;
        for num in 1..=n {
            match num%m {
                0 => result -= num,
                _ => result += num,
            };
        }

        return result
    }
}
```
