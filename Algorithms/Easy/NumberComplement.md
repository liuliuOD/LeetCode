![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 476. [Number Complement](https://leetcode.com/problems/number-complement)

### Solution :

Method 1 (Bitwise, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the bits in `num`)) :
```Rust
impl Solution {
    pub fn find_complement(num: i32) -> i32 {
        let mut temp: i32 = num;
        let mut bits: u8 = 0;
        while temp > 0 {
            bits += 1;
            temp >>= 1;
        }

        return num ^ ((1 << bits) - 1)
    }
}
```
