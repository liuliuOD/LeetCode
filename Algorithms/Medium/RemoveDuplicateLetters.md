![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Remove Duplicate Letters](https://leetcode.com/problems/remove-duplicate-letters)

### Solution :

Method 1 (Monotonic Stack) :
```rust
use std::collections::{ HashMap, HashSet };
impl Solution {
    pub fn remove_duplicate_letters(s: String) -> String {
        let mut letter_choosen = HashSet::new();
        let mut letter_last_indexes = HashMap::new();
        for (index, ch) in s.chars().into_iter().enumerate() {
            letter_last_indexes.insert(ch, index);
        }

        let mut result = vec![];
        for (index, ch) in s.chars().into_iter().enumerate() {
            if letter_choosen.contains(&ch) {
                continue;
            }

            while !result.is_empty() {
                let last = result.pop().unwrap();
                let index_stack_last = letter_last_indexes.get(&last).unwrap();
                if (last as u8) < (ch as u8) || *index_stack_last <= index {
                    result.push(last);
                    break;
                }

                letter_choosen.remove(&last);
            }

            result.push(ch);
            letter_choosen.insert(ch);
        }

        result.iter().collect()
    }
}
```
