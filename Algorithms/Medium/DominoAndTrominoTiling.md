![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 790. [Domino And Tromino Tiling](https://leetcode.com/problems/domino-and-tromino-tiling)

### Solution :

Method 1 (AI by Grok3, Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the value of `n`)) :
```rust
impl Solution {
    pub fn num_tilings(n: i32) -> i32 {
        const MOD: i64 = 1_000_000_007;
        let n = n as usize;

        if n == 0 {
            return 1
        }

        let mut dp = vec![0_i64; (n + 3).max(3)];
        dp[0] = 1; // Empty board
        dp[1] = 1; // One vertical domino
        dp[2] = 2; // Two dominoes (vertical or horizontal)

        for i in 3..=n {
            dp[i] = (2 * dp[i-1] + dp[i-3]) % MOD;
        }

        return dp[n] as i32
    }
}
```
