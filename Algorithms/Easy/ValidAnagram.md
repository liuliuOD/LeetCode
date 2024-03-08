![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 242. [Valid Anagram](https://leetcode.com/problems/valid-anagram)

### Solution :

Method 1 :
```rust
const BASE: usize = b'a' as usize;

impl Solution {
    pub fn is_anagram(s: String, t: String) -> bool {
        if s.len() != t.len() {
            return false
        }

        let mut mapping: [i32; 26] = [0; 26];
        for index in s.bytes() {
            mapping[index as usize - BASE] += 1;
        }
        for index in t.bytes() {
            mapping[index as usize - BASE] -= 1;
        }

        return mapping.iter().all(|&value| value == 0)
    }
}
```

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        counter = Counter(s)
        target = Counter(t)
        for key, amount in target.items():
            if key not in counter or counter[key] != amount:
                return False

        return True
```
