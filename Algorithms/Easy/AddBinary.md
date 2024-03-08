![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Add Binary](https://leetcode.com/problems/add-binary)

### Solution :

Method 1 :
```rust
use std::iter::FromIterator;
impl Solution {
    pub fn add_binary(a: String, b: String) -> String {
        let mut max_length:i16 = 0;
        if a.len() > b.len() {
            max_length = a.len() as _;
        } else {
            max_length = b.len() as _;
        }

        let mut chars_a = a.chars().rev();
        let mut chars_b = b.chars().rev();
        let mut offset = '0';
        let mut result = vec![];
        while max_length > 0 {
            match (chars_a.next().unwrap_or('0'), chars_b.next().unwrap_or('0')) {
                ('0', '0') => {
                    result.push(offset);
                    offset = '0';
                },
                ('0', '1') | ('1', '0') => if offset == '0' {
                    result.push('1');
                    offset = '0';
                } else {
                    result.push('0');
                    offset = '1';
                },
                ('1', '1') => if offset == '0' {
                    result.push('0');
                    offset = '1';
                } else {
                    result.push('1');
                    offset = '1';
                },
                _ => (),
            };

            max_length -= 1;
        }

        if offset == '1' {
            result.push('1');
        }

        result.reverse();
        String::from_iter(result)
    }
}
```

Method 2 :
```rust
```

Method 3 :
```rust
```
