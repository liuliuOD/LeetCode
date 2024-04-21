![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 3120. [Count The Number Of Special Characters I](https://leetcode.com/problems/count-the-number-of-special-characters-i)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
use std::collections::HashSet;

const BASE_LOWER: u8 = 'a' as u8;
const BASE_UPPER: u8 = 'A' as u8;
impl Solution {
    pub fn number_of_special_chars(word: String) -> i32 {
        let mut result: i32 = 0;
        let candidates: HashSet<u8> = HashSet::from_iter(word.bytes().collect::<Vec<u8>>());
        for &ascii in candidates.iter() {
            let ascii_upper: u8 = BASE_UPPER + ascii - BASE_LOWER;
            if BASE_LOWER <= ascii && ascii < (BASE_LOWER+26) && candidates.contains(&ascii_upper) {
                result += 1;
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (In weekly contest 394, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def numberOfSpecialChars(self, word: str) -> int:
        result = 0
        mapping = defaultdict(int)
        for char in word:
            offset_lower = ord(char) - ord('a')
            offset_upper = ord(char) - ord('A')
            key = ""
            if char.isupper():
                key = chr(ord('A')+offset_upper)
                key_opposite = chr(ord('a')+offset_upper)
            else:
                key = chr(ord('a')+offset_lower)
                key_opposite = chr(ord('A')+offset_lower)

            mapping[key] += 1
            if mapping[key] == 1 and mapping[key_opposite] >= 1:
                result += 1

        return result
```

Method 2 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def numberOfSpecialChars(self, word: str) -> int:
        candidates = set(word)
        result = 0
        for char in candidates:
            if 'a' <= char <= 'z' and (chr(ord('A')+ord(char)-ord('a'))) in candidates:
                result += 1

        return result
```

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func numberOfSpecialChars(word string) int {
    var exists map[rune]bool = make(map[rune]bool)
    for _, char := range word {
        exists[char] = true
    }

    var result int
    for char, _ := range exists {
        if 'a' <= char && char <= 'z' {
            _, ok := exists['A' + char - 'a']
            if ok {
                result += 1
            }
        }
    }
    return result
}
```
