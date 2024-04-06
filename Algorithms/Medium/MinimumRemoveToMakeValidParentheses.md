![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1249. [Minimum Remove To Make Valid Parentheses](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minRemoveToMakeValid(self, s: str) -> str:
        result = ""
        depth = 0
        for char in s:
            if char == '(':
                depth += 1
            elif char == ')':
                depth -= 1

            if depth < 0:
                depth = 0
                continue

            result += char

        if depth == 0:
            return result

        temp = result
        result = ""
        for char in reversed(temp):
            if depth > 0 and char == '(':
                depth -= 1
                continue

            result += char

        return result[::-1]
```
