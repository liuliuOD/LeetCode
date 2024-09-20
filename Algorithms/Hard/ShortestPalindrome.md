![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 214. [Shortest Palindrome](https://leetcode.com/problems/shortest-palindrome)

### Solution :

Method 1 (Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```rust
impl Solution {
    pub fn shortest_palindrome(s: String) -> String {
        let n: usize = s.len();
        let s_reversed: String = s.chars().rev().collect();
        for index in 0..n {
            if s[0..n-index] == s_reversed[index..n] {
                return s_reversed[0..index].to_string() + &s
            }
        }

        return String::new()
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```python
class Solution:
    def shortestPalindrome(self, s: str) -> str:
        n = len(s)
        s_reversed = s[::-1]
        for index in range(n):
            if s[:n-index] == s_reversed[index:]:
                return s_reversed[:index] + s

        return ""
```
