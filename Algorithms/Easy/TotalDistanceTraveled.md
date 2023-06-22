![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2739. [Total Distance Traveled](https://leetcode.com/problems/total-distance-traveled)

### Solution :

Method 1 (In weekly contest 350) :
```python
class Solution:
    def distanceTraveled(self, mainTank: int, additionalTank: int) -> int:
        counter = 0
        result = 0
        while mainTank > 0:
            mainTank -= 1
            counter += 1
            if counter == 5 and additionalTank > 0:
                counter = 0
                mainTank += 1
                additionalTank -= 1
            result += 10
        return result
```
