![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1545. [Find Kth Bit In Nth Binary String](https://leetcode.com/problems/find-kth-bit-in-nth-binary-string)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(2^N)$, Space Complexity: $O(2^N)$ (N: the value of `n`)) :
```rust
impl Solution {
    pub fn find_kth_bit(n: i32, k: i32) -> char {
        let mut s: String = "0".to_string();
        for _ in 2..=n {
            let mut s_reverse: String = "".to_string();
            for character in s.chars().rev() {
                if character == '0' {
                    s_reverse.push('1');
                } else {
                    s_reverse.push('0');
                }
            }
            s += &("1".to_string() + &s_reverse);
        }

        return s.chars().nth(k as usize -1).unwrap()
    }
}
```
