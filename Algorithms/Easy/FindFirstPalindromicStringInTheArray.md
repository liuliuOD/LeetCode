![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2108. [Find First Palindromic String In The Array](https://leetcode.com/problems/find-first-palindromic-string-in-the-array)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(M*N)$ (M: length of each word, N: length of `words`), Space Complexity: $O(1)$) :
```python
class Solution:
    def firstPalindrome(self, words: List[str]) -> str:
        for word in words:
            if self.isPalindrome(word):
                return word

        return ''

    def isPalindrome(self, s: str) -> bool:
        n = len(s)
        head = 0
        tail = n - 1
        while head < n//2:
            if s[head] != s[tail]:
                return False

            head += 1
            tail -= 1

        return True
```

Method 2 (Brute Force, Time Complexity: $O(M*N)$ (M: length of each word, N: length of `words`), Space Complexity: $O(1)$) :
```python
class Solution:
    def firstPalindrome(self, words: List[str]) -> str:
        for word in words:
            if word == word[::-1]:
                return word

        return ''
```
