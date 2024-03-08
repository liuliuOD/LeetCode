![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2745. [Construct The Longest New String](https://leetcode.com/problems/construct-the-longest-new-string)

### Solution :

Method 1 (In biweekly contest 107) :
```python
class Solution:
    def longestString(self, x: int, y: int, z: int) -> int:
        result = 0
        if x > y:
            result = y * 2 + 1 + z
        elif x < y:
            result = x * 2 + 1 + z
        elif x == y:
            result = x * 2 + z
        return result * 2
```
