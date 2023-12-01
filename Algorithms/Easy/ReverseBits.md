![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 190. [Reverse Bits](https://leetcode.com/problems/reverse-bits)

### Solution :

Method 1 (Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn reverse_bits(mut x: u32) -> u32 {
        let mut result: u32 = 0;
        for _ in 0..32 {
            result <<= 1;
            result |= (x & 1);
            x >>= 1;
        }

        return result
    }
}
```

### Solution :

Method 1 :
```python
class Solution:
    def reverseBits(self, n: int) -> int:
        result = ""
        while n:
            result += str(n%2)
            n //= 2

        if len(result) < 32:
            result += "0" * (32 - len(result))

        return int(result, 2)
```

Method 2 :
```python
class Solution:
    def reverseBits(self, n: int) -> int:
        result = 0
        for _ in range(32):
            result <<= 1
            result |= (n & 1)
            n >>= 1

        return result
```
