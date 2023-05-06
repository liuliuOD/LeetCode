## [Longest Nice Substring](https://leetcode.com/problems/longest-nice-substring)

### Solution :

Method 1 (Divide & Conquer) :
```rust
use std::cmp::Ordering;
use std::collections::HashSet;
impl Solution {
    pub fn longest_nice_substring(s: String) -> String {
        let mut hs = HashSet::new();
        for ch in s.chars().into_iter() {
            hs.insert(ch.to_string());
        }

        for (index, ch) in s.chars().into_iter().enumerate() {
            match ch.is_uppercase() {
                true => {
                    if hs.contains(&ch.to_lowercase().to_string()) {
                        continue;
                    }
                },
                false => {
                    if hs.contains(&ch.to_uppercase().to_string()) {
                        continue;
                    }
                },
            }
            let mut string_left = Self::longest_nice_substring(s[..index].to_string());
            let mut string_right = Self::longest_nice_substring(s[index+1..s.len()].to_string());

            match string_left.len().cmp(&string_right.len()) {
                Ordering::Greater | Ordering::Equal => {
                    return string_left
                },
                _ => {
                    return string_right
                },
            }
        }
        return s
    }
}
```
