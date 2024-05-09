![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3075. [Maximize Happiness Of Selected Children](https://leetcode.com/problems/maximize-happiness-of-selected-children)

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maximumHappinessSum(self, happiness: List[int], k: int) -> int:
        happiness.sort()
        turn = 0
        result = 0
        while turn < k:
            result += max(0, happiness.pop() - turn)
            turn += 1

        return result
```
