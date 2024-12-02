![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1455. [Check If A Word Occurs As A Prefix Of Any Word In A Sentence](https://leetcode.com/problems/check-if-a-word-occurs-as-a-prefix-of-any-word-in-a-sentence)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(M*N)$, Space Complexity: $O(N)$ (M: the length of `sentence`, N: the length of `search_word`)) :
```Rust
impl Solution {
    pub fn is_prefix_of_word(sentence: String, search_word: String) -> i32 {
        let mut result: i32 = 1;
        for word in sentence.split(' ') {
            if word.starts_with(&search_word) {
                return result
            }

            result += 1;
        }

        return -1
    }
}
```
