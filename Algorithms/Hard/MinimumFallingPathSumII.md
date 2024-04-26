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

Method 2 (Dynamic Programming + Space Optimization, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minFallingPathSum(self, grid: List[List[int]]) -> int:
        n = len(grid)
        if n == 1:
            return grid[0][0]

        dp = [0] * n
        index_min_1, index_min_2 = 0, 0
        for row in grid:
            temp = [inf] * n
            temp_index_min_1, temp_index_min_2 = None, None
            for index, column in enumerate(row):
                temp[index] = column
                if index == index_min_1:
                    temp[index] += dp[index_min_2]
                elif index == index_min_2:
                    temp[index] += dp[index_min_1]
                else:
                    temp[index] += min(dp[index_min_1], dp[index_min_2])

                if temp_index_min_1 is None or temp[index] < temp[temp_index_min_1]:
                    temp_index_min_1, temp_index_min_2 = index, temp_index_min_1
                elif temp_index_min_2 is None or temp[index] < temp[temp_index_min_2]:
                    temp_index_min_2 = index

            dp = temp
            index_min_1, index_min_2 = temp_index_min_1, temp_index_min_2

        return min(dp)
```
