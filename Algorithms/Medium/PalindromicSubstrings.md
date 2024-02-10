![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 647. [Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings)

### Solution :

Method 1 (Sliding Window, Time Complexity: $O(N^3)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        n = len(s)
        result = 0
        window = 1
        while window <= n:
            for index in range(n-window+1):
                if self.isPalindrom(s[index:index+window]):
                    result += 1

            window += 1

        return result

    def isPalindrom(self, s: str) -> bool:
        n = len(s)
        index = 0
        while index < n // 2:
            if s[index] != s[n-index-1]:
                return False

            index += 1

        return True
```
