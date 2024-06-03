![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2486. [Append Characters To String To Make Subsequence](https://leetcode.com/problems/append-characters-to-string-to-make-subsequence)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(M or N)$ (M: length of `s`, N: length of `t`), Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn append_characters(s: String, t: String) -> i32 {
        let s: Vec<u8> = s.into_bytes();
        let t: Vec<u8> = t.into_bytes();
        let n_s: usize = s.len();
        let n_t: usize = t.len();
        let mut index_s: usize = 0;
        let mut index_t: usize = 0;
        while index_s < n_s && index_t < n_t {
            if s[index_s] == t[index_t] {
                index_t += 1;
            }

            index_s += 1;
        }

        return (n_t - index_t) as i32
    }
}
```

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(M or N)$ (M: length of `s`, N: length of `t`), Space Complexity: $O(1)$) :
```python
class Solution:
    def appendCharacters(self, s: str, t: str) -> int:
        n_s, n_t = len(s), len(t)
        index_s, index_t = 0, 0
        while index_s < n_s and index_t < n_t:
            if s[index_s] == t[index_t]:
                index_t += 1

            index_s += 1

        return n_t - index_t
```
