![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1289. [Minimum Falling Path Sum II](https://leetcode.com/problems/minimum-falling-path-sum-ii)

### Solution :

Method 1 (Dynamic Programming + Space Optimization, Time Complexity: $O(N^3)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minFallingPathSum(self, grid: List[List[int]]) -> int:
        n = len(grid)
        dp = [0] * n
        for row in grid:
            temp = [inf] * n
            for index, column in enumerate(row):
                temp[index] = column
                if len(row) > 1:
                    temp[index] += min(dp[:index] + dp[index+1:])
            dp = temp

        return min(dp)
```
