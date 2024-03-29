![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 191. [Number Of 1 Bits](https://leetcode.com/problems/number-of-1-bits)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn hammingWeight (mut n: u32) -> i32 {
        let mut result: i32 = 0;
        while n > 0 {
            /* Option 1 */
            result += match n % 2 {
                1 => 1,
                _ => 0,
            };
            /* Option 2

            result += (n&1) as i32;
            */

            n >>= 1;
        }

        return result
    }
}
```

Method 2 (Built-In method) :
```rust
impl Solution {
    pub fn hammingWeight (n: u32) -> i32 {
        return n.count_ones() as _
    }
}
```

Method 3 (Bitwise) :
```rust
impl Solution {
    pub fn hammingWeight (n: u32) -> i32 {
        return (0..32).fold(0, |result, bit| {
            return if (1 & (n>>bit)) == 1 {
                result + 1
            } else {
                result
            }
        }) as _
    }
}
```

### Solution :

Method 1 :
```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        result = 0
        while n:
            result += n % 2 == 1
            n //= 2

        return result
```

Method 2 (Bitwise) :
```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        result = 0
        while n:
            result += (n&1)
            n >>= 1

        return result
```
