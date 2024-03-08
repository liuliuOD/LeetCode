![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1732. [Find The Highest Altitude](https://leetcode.com/problems/find-the-highest-altitude)

### Solution :

Method 1 :
```python
class Solution:
    def largestAltitude(self, gain: List[int]) -> int:
        result = 0
        temp = 0
        for altitude in gain:
            temp += altitude
            result = max(result, temp)
        return result
```
