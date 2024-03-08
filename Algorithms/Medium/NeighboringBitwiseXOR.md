![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2683. [Neighboring Bitwise XOR](https://leetcode.com/problems/neighboring-bitwise-xor)

### Solution :

[Method 1 (Math Proof) :](https://leetcode.com/problems/neighboring-bitwise-xor/solutions/3521882/c-java-python-explanation-with-formal-proof-one-liner-time-o-n/?orderBy=hot)
```rust
impl Solution {
    pub fn does_valid_array_exist(derived: Vec<i32>) -> bool {
        let mut xor = 0;
        for num in derived.iter() {
            xor ^= num;
        }
        xor == 0
    }
}
```
