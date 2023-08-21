![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 459. [Repeated Substring Pattern](https://leetcode.com/problems/repeated-substring-pattern)

### Solution :

Method 1 ([Rotated](https://leetcode.com/problems/repeated-substring-pattern/editorial)) :
```rust
impl Solution {
    pub fn repeated_substring_pattern(s: String) -> bool {
        let n: usize = s.len();
        let temp: String = s.clone()[1..].to_string() + &s.clone()[..n-1];

        return temp.contains(&s)
    }
}
```

### Solution :

Method 1 (Brute Force + Divide) :
```python
class Solution:
    def repeatedSubstringPattern(self, s: str) -> bool:
        n = len(s)
        divide = 1
        while n > divide:
            if n % divide == 0 and s[:divide]*(n//divide) == s:
                return True

            divide += 1

        return False
```

Method 2 ([Rotated](https://leetcode.com/problems/repeated-substring-pattern/editorial)) :
```python
class Solution:
    def repeatedSubstringPattern(self, s: str) -> bool:
        # created a new string by merging `s + s`` and dropping head and tail, valid if `s` is substring of the new string
        return s in s[1:] + s[:-1]
```
