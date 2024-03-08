![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2697. [Lexicographically Smallest Palindrome](https://leetcode.com/problems/lexicographically-smallest-palindrome)

### Solution :

Method 1 (In weekly contest 346) :
```python
class Solution:
    def makeSmallestPalindrome(self, s: str) -> str:
        n = len(s)
        len_half = n // 2
        result = [''] * n
        
        for move in range(0, len_half):
            if s[0+move] > s[n-move-1]:
                result[0+move] = result[n-move-1] = s[n-move-1]
            else:
                result[n-move-1] = result[0+move] = s[0+move]
        
        if n % 2 == 1:
            result[len_half] = s[len_half]

        return ''.join(result)
```
