![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 367. [Valid Perfect Square](https://leetcode.com/problems/valid-perfect-square)

### Solution :

Method 1 (Binary Search) :
```python
class Solution:
    def isPerfectSquare(self, num: int) -> bool:
        left = 1
        right = num
        while left <= right:
            middle = left + (right - left) // 2
            temp = middle**2
            if temp == num:
                return True
            elif temp < num:
                left = middle + 1
            elif temp > num:
                right = middle - 1
        return False
```
