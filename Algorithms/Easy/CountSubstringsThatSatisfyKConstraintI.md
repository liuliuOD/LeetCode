![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3258. [Count Substrings That Satisfy K-Constraint I](https://leetcode.com/problems/count-substrings-that-satisfy-k-constraint-i)

### Solution :

Method 1 (Prefix Sum, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```Rust
impl Solution {
    pub fn count_k_constraint_substrings(s: String, k: i32) -> i32 {
        let s_bytes: Vec<u8> = s.into_bytes();
        let mut prefix_sum: Vec<(i32, i32)> = Vec::new();
        prefix_sum.push((0, 0));
        for &byte in s_bytes.iter() {
            let mut amount_zero: i32 = 0;
            let mut amount_one: i32 = 0;
            if prefix_sum.len() > 1 {
                amount_zero += prefix_sum.last().unwrap().0;
                amount_one += prefix_sum.last().unwrap().1;
            }

            if byte == b'0' {
                amount_zero += 1;
            } else {
                amount_one += 1;
            }

            prefix_sum.push((amount_zero, amount_one));
        }

        let n: usize = prefix_sum.len();
        let mut result: i32 = 0;
        for index_end in 1..n {
            for index_start in 0..index_end {
                if (prefix_sum[index_end].0-prefix_sum[index_start].0) <= k || (prefix_sum[index_end].1-prefix_sum[index_start].1) <= k {
                    result += 1;
                }
            }
        }

        return result
    }
}
```

Method 2 (Sliding Window, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$ (N: the length of `s`)) :
```rust
impl Solution {
    pub fn count_k_constraint_substrings(s: String, k: i32) -> i32 {
        let s_bytes: Vec<u8> = s.into_bytes();
        let n: usize = s_bytes.len();
        let mut result: i32 = 0;
        for window in 1..=n {
            let mut amount_zero: i32 = 0;
            let mut amount_one: i32 = 0;
            for index in 0..n {
                if s_bytes[index] == b'0' {
                    amount_zero += 1;
                } else {
                    amount_one += 1;
                }

                if index < window-1 {
                    continue;
                }

                if index >= window {
                    if s_bytes[index-window] == b'0' {
                        amount_zero -= 1;
                    } else {
                        amount_one -= 1;
                    }
                }

                if amount_zero <= k || amount_one <= k {
                    result += 1;
                }
            }
        }

        return result
    }
}
```
