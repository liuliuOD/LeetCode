![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 633. [Sum Of Square Numbers](https://leetcode.com/problems/sum-of-square-numbers)

### Solution :

Method 1 (Pre-Calculate + Binary Search + Hash Map + Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
MAPPING: set[int] = set()
CANDIDATES: list[int] = []
for i in range(50000):
    CANDIDATES.append(i**2)
    MAPPING.add(i**2)

class Solution:
    def judgeSquareSum(self, c: int) -> bool:
        index = bisect.bisect_left(CANDIDATES, c)
        for i in range(index+1):
            if c - CANDIDATES[i] in MAPPING:
                return True

        return False
```
