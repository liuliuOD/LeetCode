![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2486. [Append Characters To String To Make Subsequence](https://leetcode.com/problems/append-characters-to-string-to-make-subsequence)

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
