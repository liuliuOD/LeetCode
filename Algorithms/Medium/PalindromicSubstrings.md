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
                if self.isPalindrome(s[index:index+window]):
                    result += 1

            window += 1

        return result

    def isPalindrome(self, s: str) -> bool:
        # Option 1
        n = len(s)
        index = 0
        while index < n // 2:
            if s[index] != s[n-index-1]:
                return False

            index += 1

        return True
        """
        # Option 2

        return s == s[::-1]
        """
```

Method 2 (Two Pointer, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        n = len(s)
        result = 0
        for index in range(n):
            result += self.countPalindrome(index, index, s) + self.countPalindrome(index, index+1, s)

        return result

    def countPalindrome(self, left: int, right: int, s: str) -> int:
        n = len(s)
        result = 0
        while left >= 0 and right < n and s[left] == s[right]:
            result += 1
            left -= 1
            right += 1

        return result
```
