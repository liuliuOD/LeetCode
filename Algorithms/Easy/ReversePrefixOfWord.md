![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2000. [Reverse Prefix Of Word](https://leetcode.com/problems/reverse-prefix-of-word)

### Solution :

Method 1 (Built-In method, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn reverse_prefix(word: String, ch: char) -> String {
        for (index, ch_current) in word.chars().enumerate() {
            if ch_current != ch {
                continue;
            }

            return word[..index+1].chars().rev().collect::<String>() + &word[index+1..]
        }

        return word
    }
}
```

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def reversePrefix(self, word: str, ch: str) -> str:
        word = list(word)
        for index, char in enumerate(word):
            if char != ch:
                continue

            index_left = 0
            while index_left < index:
                word[index_left], word[index] = word[index], word[index_left]
                index_left += 1
                index -= 1
            break

        return ''.join(word)
```

Method 2 (Built-In method, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def reversePrefix(self, word: str, ch: str) -> str:
        for index, char in enumerate(word):
            if char != ch:
                continue

            return word[:index+1][::-1] + word[index+1:]

        return word
```
