![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2729. [Check If The Number Is Fascinating](https://leetcode.com/problems/check-if-the-number-is-fascinating)

### Solution :

Method 1 (In biweekly contest 106) :
```python
class Solution:
    def isFascinating(self, n: int) -> bool:
        result = set()
        length = 0
        length += self.findNum(n, result)
        length += self.findNum(n*2, result)
        length += self.findNum(n*3, result)
        amount = 0
        for item in result:
            if item == 0:
                return False
            amount += 1
        return amount == 9 and length == 9

    def findNum(self, n: int, result: Set[int]) -> int:
        length = len(str(n))
        while n > 0:
            temp = n % 10
            n = n // 10
            result.add(temp)
        return length
```
