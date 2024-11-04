![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3163. [String Compression III](https://leetcode.com/problems/string-compression-iii)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `word`)) :
```rust
impl Solution {
    pub fn compressed_string(word: String) -> String {
        let mut word_char: Vec<char> = word.chars().collect();
        word_char.push('?');
        let n: usize = word_char.len();
        let mut char_previous: char = word_char[0];
        let mut times: usize = 1;
        let mut result: String = String::new();
        for index in 1..n {
            let char_current: char = word_char[index];
            if times == 9 || char_previous != char_current {
                result += &(times.to_string() + &char_previous.to_string());
                times = 0;
                char_previous = char_current;
            }

            times += 1;
        }

        return result
    }
}
```
