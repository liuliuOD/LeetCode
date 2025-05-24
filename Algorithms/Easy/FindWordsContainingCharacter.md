![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2942. [Find Words Containing Character](https://leetcode.com/problems/find-words-containing-character)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$ (M: the average number of characters in `words`, N: the number of elements in `words`)) :
```rust
impl Solution {
    pub fn find_words_containing(words: Vec<String>, x: char) -> Vec<i32> {
        let n: usize = words.len();
        let mut result: Vec<i32> = Vec::new();
        for index in 0..n {
            let word: &str = &words[index];
            if !word.contains(x) {
                continue;
            }

            result.push(index as i32);
        }

        return result
    }
}
```
