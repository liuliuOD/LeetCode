![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2338. [Count The Number Of Ideal Arrays](https://leetcode.com/problems/count-the-number-of-ideal-arrays)

### Solution :

Method 1 (AI by Grok3, Time Complexity: $O(M*Log(M)+Log(N))$, Space Complexity: $O(M^2)$ (M: the value of `max_value`, N: the value of `n`)) :
```rust
impl Solution {
    pub fn ideal_arrays(n: i32, max_value: i32) -> i32 {
        const MOD: i64 = 1_000_000_007;
        let n = n as usize;
        let max_value = max_value as usize;

        // Step 1: Compute divisors for each number
        let mut divisors = vec![vec![]; max_value + 1];
        for i in 1..=max_value {
            for j in (i..=max_value).step_by(i) {
                divisors[j].push(i);
            }
        }

        // Step 2: DP to count sequences up to length 14
        let mut dp = vec![0_i64; max_value + 1];
        // Base case: sequences of length 1
        for k in 1..=max_value {
            dp[k] = 1;
        }

        // For each length up to 14 (max possible chain length)
        let max_len = 14.min(n);
        let mut ways = vec![0_i64; max_len + 1];
        ways[1] = max_value as i64; // Number of sequences of length 1

        for len in 2..=max_len {
            let mut new_dp = vec![0_i64; max_value + 1];
            for k in 1..=max_value {
                for &j in &divisors[k] {
                    if j == k {
                        continue; // Avoid counting the same number twice in the chain
                    }
                    new_dp[k] = (new_dp[k] + dp[j]) % MOD;
                }
            }
            dp = new_dp;
            ways[len] = dp[1..=max_value].iter().sum::<i64>() % MOD;
        }

        // Step 3: Use combinatorics to extend to length n
        let mut result = 0_i64;
        for len in 1..=max_len {
            if ways[len] == 0 {
                continue;
            }
            // Compute combinations: (n - 1) choose (len - 1)
            let mut comb = 1_i64;
            for i in 1..len {
                comb = (comb * (n as i64 - i as i64)) % MOD;
                comb = (comb * mod_inverse(i as i64, MOD)) % MOD;
            }
            result = (result + ways[len] * comb) % MOD;
        }

        return result as i32
    }
}

// Helper function to compute modular inverse using Fermat's little theorem
fn mod_inverse(a: i64, m: i64) -> i64 {
    mod_pow(a, m - 2, m)
}

// Helper function to compute modular exponentiation
fn mod_pow(mut base: i64, mut exp: i64, modulus: i64) -> i64 {
    let mut result = 1;
    base %= modulus;
    while exp > 0 {
        if exp & 1 == 1 {
            result = (result * base) % modulus;
        }
        base = (base * base) % modulus;
        exp >>= 1;
    }

    return result
}
```
