![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 678. [Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string)

### Solution :

Method 1 (Two Direction, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def checkValidString(self, s: str) -> bool:
        depth_a = 0
        for char in s:
            if char in ['*', '(']:
                depth_a += 1
            elif char == ')':
                depth_a -= 1

            if depth_a < 0:
                return False

        depth_b = 0
        for char in s[::-1]:
            if char == '(':
                depth_b += 1
            elif char in ['*', ')']:
                depth_b -= 1

            if depth_b > 0:
                return False

        return True
```
