![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2185. [Counting Words With A Given Prefix](https://leetcode.com/problems/counting-words-with-a-given-prefix)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `words`)) :
```rust
impl Solution {
    pub fn prefix_count(words: Vec<String>, pref: String) -> i32 {
        let mut result: i32 = 0;
        for word in words {
            if word.starts_with(&pref) {
                result += 1;
            }
        }

        return result
    }
}
```
