![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1552. [Magnetic Force Between Two Balls](https://leetcode.com/problems/magnetic-force-between-two-balls)

### Solution :

Method 1 (Binary Search, Time Complexity: $O(N*Log(N))$ (N: length of `position`), Space Complexity: $O(N)$) :
```python
class Solution:
    def maxDistance(self, position: List[int], m: int) -> int:
        position.sort()
        left, right = 0, max(position) - min(position)
        while left <= right:
            distance = left + (right - left)//2

            position_previous = -inf
            m_temp = m
            for position_current in position:
                if position_current - position_previous >= distance:
                    m_temp -= 1
                    position_previous = position_current

                if m_temp == 0:
                    break

            if m_temp == 0:
                left = distance + 1
            else:
                right = distance - 1

        return right
```
