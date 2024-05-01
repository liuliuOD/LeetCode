![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
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

### Solution :

Method 1 (Built-In method, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func reversePrefix(word string, ch byte) string {
    for index, _ := range word {
        if word[index] != ch {
            continue
        }

        /* Option 1 */
        var prefix string
        for index_reverse := index; index_reverse >= 0; index_reverse-- {
            prefix += string(word[index_reverse])
        }

        return prefix + word[index+1:]
        /* Option 2

        var prefix []byte
        for index_reverse := index; index_reverse >= 0; index_reverse-- {
            prefix = append(prefix, word[index_reverse])
        }

        return string(prefix) + word[index+1:]
        */
    }

    return word
}
```

Method 2 (Built-In method, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func reversePrefix(word string, ch byte) string {
    var result []byte = []byte(word)
    for index, _ := range word {
        if word[index] != ch {
            continue
        }

        for index_left := 0; index_left < index; index_left++ {
            result[index_left], result[index] = result[index], result[index_left]
            index--
        }

        break
    }

    return string(result)
}
```
