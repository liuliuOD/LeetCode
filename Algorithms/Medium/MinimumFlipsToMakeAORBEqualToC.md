![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1318. [Minimum Flips To Make A OR B Equal To C](https://leetcode.com/problems/minimum-flips-to-make-a-or-b-equal-to-c)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn min_flips(mut a: i32, mut b: i32, mut c: i32) -> i32 {
        let mut result = 0;
        while a > 0 || b > 0 || c > 0 {
            let bit_a = a & 1;
            let bit_b = b & 1;
            let bit_c = c & 1;
            a >>= 1;
            b >>= 1;
            c >>= 1;

            if bit_c == 1 && bit_a == 0 && bit_b == 0 {
                result += 1;
            } else if bit_c == 0 {
                result += bit_a + bit_b;
            }
        }
        return result
    }
}
```

### Solution :

Method 1 :
```python
class Solution:
    def minFlips(self, a: int, b: int, c: int) -> int:
        result = 0
        while a or b or c:
            bit_a = a & 1
            bit_b = b & 1
            bit_c = c & 1
            if bit_c == 1 and bit_a == 0 and bit_b == 0:
                result += 1
            elif bit_c == 0:
                result += bit_a + bit_b

            a >>= 1
            b >>= 1
            c >>= 1
        return result
```
