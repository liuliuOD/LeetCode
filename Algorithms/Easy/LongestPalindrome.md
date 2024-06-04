![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 409. [Longest Palindrome](https://leetcode.com/problems/longest-palindrome)

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
