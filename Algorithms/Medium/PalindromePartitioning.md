![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 131. [Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning)

### Solution :

Method 1 (Backtracking + Two Pointer) :
```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        self.result = []
        self.backtracking(0, [], "", s)

        return self.result

    def backtracking(self, index: int, substrings: list[str], substring: str, s: str):
        if index >= len(s):
            if self.is_palindrome(substring):
                temp = substrings.copy()
                temp.append(substring)
                self.result.append(temp)
            return

        self.backtracking(index+1, substrings, substring+s[index], s)
        if self.is_palindrome(substring):
            substrings.append(substring)
            self.backtracking(index+1, substrings, s[index], s)
            substrings.pop()

    def is_palindrome(self, s: str) -> bool:
        n = len(s)
        if n == 0:
            return False

        left = 0
        right = n - 1
        while left < right:
            if s[left] != s[right]:
                return False

            left += 1
            right -= 1

        return True
```
