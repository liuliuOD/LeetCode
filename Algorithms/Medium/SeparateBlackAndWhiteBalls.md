![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2938. [Separate Black And White Balls](https://leetcode.com/problems/separate-black-and-white-balls)

### Solution :

Method 1 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```rust
impl Solution {
    pub fn minimum_steps(s: String) -> i64 {
        let n: usize = s.len();
        let s_bytes: Vec<u8> = s.into_bytes();
        let mut prefix_sum: i64 = 0;
        let mut result: i64 = 0;
        for index in 0..n {
            match s_bytes[index] {
                b'0' => {
                    result += prefix_sum;
                },
                b'1' => {
                    prefix_sum += 1;
                },
                _ => {},
            }
        }

        return result
    }
}
```
