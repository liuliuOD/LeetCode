![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 409. [Longest Palindrome](https://leetcode.com/problems/longest-palindrome)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn longest_palindrome(s: String) -> i32 {
        let mut table: HashSet<u8> = HashSet::new();
        let mut result: i32 = 0;
        for ascii in s.bytes() {
            match table.contains(&ascii) {
                true => {
                    result += 2;
                    table.remove(&ascii);
                },
                false => {
                    table.insert(ascii);
                }
            };
        }

        if table.len() > 0 {
            result += 1;
        }

        return result
    }
}
```

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def longestPalindrome(self, s: str) -> int:
        frequency = defaultdict(int)
        result = 0
        for char in s:
            frequency[char] += 1
            if frequency[char] % 2 == 0:
                result += 2
                del frequency[char]

        if frequency:
            result += 1

        return result
```

Method 2 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def longestPalindrome(self, s: str) -> int:
        frequency = set()
        result = 0
        for char in s:
            if char in frequency:
                result += 2
                frequency.remove(char)
            else:
                frequency.add(char)

        if frequency:
            result += 1

        return result
```

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```golang
func longestPalindrome(s string) int {
    var result int
    var table = make(map[rune]bool)
    for _, char := range s {
        _, ok := table[char]
        if ok {
            result += 2
            delete(table, char)
        } else {
            table[char] = true
        }
    }

    if len(table) > 0 {
        result++
    }

    return result
}
```
