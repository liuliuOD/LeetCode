![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 7. [Reverse Integer](https://leetcode.com/problems/reverse-integer)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the digits amount of `x`)) :
```rust
impl Solution {
    pub fn reverse(x: i32) -> i32 {
        let is_positive: bool = x >= 0;
        let mut x_reverse: i64 = 0;
        let mut temp: i64 = (x as i64).abs();
        while temp > 0 {
            x_reverse = 10*x_reverse + temp%10;
            temp /= 10;
        }

        if (x_reverse as i32) as i64 != x_reverse {
            return 0
        }
        return match is_positive {
            true => x_reverse as i32,
            _ => -(x_reverse as i32),
        }
    }
}
```
