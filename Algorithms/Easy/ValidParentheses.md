![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Valid Parentheses](https://leetcode.com/problems/valid-parentheses)

### Solution :
```rust
impl Solution {
    pub fn is_valid(s: String) -> bool {
        let mut stack = Vec::new();
        for symbol in s.chars() {
            match symbol {
                '(' => stack.push(')'),
                '{' => stack.push('}'),
                '[' => stack.push(']'),
                right => if Some(right) != stack.pop() {
                    return false
                },
            }
        }
        stack.is_empty()
    }
}
```
