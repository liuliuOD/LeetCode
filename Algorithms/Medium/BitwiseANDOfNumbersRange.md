![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 201. [Bitwise AND Of Numbers Range](https://leetcode.com/problems/bitwise-and-of-numbers-range)

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded") :
```python
class Solution:
    def rangeBitwiseAnd(self, left: int, right: int) -> int:
        result = right
        for current in range(left, right):
            result &= current

        return result
```

Method 2 (ERROR: "Time Limit Exceeded", 8260/8269) :
```python
class Solution:
    def rangeBitwiseAnd(self, left: int, right: int) -> int:
        power_left = 0
        while 2 ** power_left <= left:
            power_left += 1

        result = left
        for current in range(left+1, min(right, 2**power_left)+1):
            result &= current

        return result
```

Method 3 :
```python
class Solution:
    def rangeBitwiseAnd(self, left: int, right: int) -> int:
        offset = 0
        while left != right:
            left >>= 1
            right >>= 1
            offset += 1

        return left << offset
```
