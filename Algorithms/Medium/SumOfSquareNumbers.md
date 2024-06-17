![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 633. [Sum Of Square Numbers](https://leetcode.com/problems/sum-of-square-numbers)

### Solution :

Method 1 (Pre-Calculate + Binary Search + Hash Map + Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(MAX(N, 5*10^4))$) :
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

Method 2 (Two Pointer, Time Complexity: $O(\sqrt{N})$, Space Complexity: $O(1)$) :
```python
class Solution:
    def judgeSquareSum(self, c: int) -> bool:
        left, right = 0, int(c**0.5) + 1
        while left <= right:
            temp = left**2 + right**2
            if temp == c:
                return True
            elif temp < c:
                left += 1
            elif temp > c:
                right -= 1

        return False
```
