![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2426. [Minimize XOR](https://leetcode.com/problems/minimize-xor)

### Solution :

Method 1 (Bit Manipulation, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the bits in `num1`)) :
```rust
impl Solution {
    pub fn minimize_xor(num1: i32, num2: i32) -> i32 {
        let mut amount_bits: u32 = num2.count_ones();
        let mut result: i32 = 0;
        for index_bit in (0..32).rev() {
            if amount_bits == 0 {
                break;
            }

            if (1<<index_bit) & num1 > 0 {
                result |= 1 << index_bit;
                amount_bits -= 1;
            }
        }

        let mut index_bit: usize = 0;
        while amount_bits > 0 && index_bit < 32 {
            if (1<<index_bit) & num1 == 0 {
                result |= 1 << index_bit;
                amount_bits -= 1;
            }

            index_bit += 1;
        }

        return result
    }
}
```
