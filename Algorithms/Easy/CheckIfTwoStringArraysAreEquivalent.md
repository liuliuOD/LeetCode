![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1662. [Check If Two String Arrays Are Equivalent](https://leetcode.com/problems/check-if-two-string-arrays-are-equivalent)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn array_strings_are_equal(word1: Vec<String>, word2: Vec<String>) -> bool {
        return word1.concat() == word2.concat()
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn array_strings_are_equal(word1: Vec<String>, word2: Vec<String>) -> bool {
        return word1.into_iter().collect::<String>() == word2.into_iter().collect::<String>()
    }
}
```

### Solution :

Method 1 :
```python
class Solution:
    def arrayStringsAreEqual(self, word_1: List[str], word_2: List[str]) -> bool:
        return ''.join(word_1) == ''.join(word_2)
```

Method 2 :
```python
class Solution:
    def arrayStringsAreEqual(self, word_1: List[str], word_2: List[str]) -> bool:
        string_1 = ''.join(word_1)

        for word in word_2:
            if string_1[:len(word)] != word:
                return False

            string_1 = string_1[len(word):]

        return len(string_1) == 0
```

Method 3 :
```python
class Solution:
    def arrayStringsAreEqual(self, word_1: List[str], word_2: List[str]) -> bool:
        len_1 = len(word_1)
        len_2 = len(word_2)
        pointer_1 = [0, 0]
        pointer_2 = [0, 0]
        while pointer_1[0] < len_1 and pointer_2[0] < len_2:
            if word_1[pointer_1[0]][pointer_1[1]] != word_2[pointer_2[0]][pointer_2[1]]:
                return False

            pointer_1[1] += 1
            pointer_2[1] += 1
            if pointer_1[1] >= len(word_1[pointer_1[0]]):
                pointer_1 = [pointer_1[0]+1, 0]
            if pointer_2[1] >= len(word_2[pointer_2[0]]):
                pointer_2 = [pointer_2[0]+1, 0]

        return pointer_1[0] == len_1 and pointer_2[0] == len_2
```
