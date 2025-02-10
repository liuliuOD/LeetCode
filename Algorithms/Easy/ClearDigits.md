![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3174. [Clear Digits](https://leetcode.com/problems/clear-digits)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```rust
impl Solution {
    pub fn clear_digits(s: String) -> String {
        let mut result: String = "".to_string();
        for character in s.chars() {
            if character.is_ascii_digit() {
                result.pop();
                continue;
            }

            result.push_str(character.encode_utf8(&mut [0]));
        }

        return result
    }
}
```
