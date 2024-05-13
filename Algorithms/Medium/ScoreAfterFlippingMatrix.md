![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 861. [Score After Flipping Matrix](https://leetcode.com/problems/score-after-flipping-matrix)

### Solution :

Method 1 (Greedy, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def matrixScore(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        for index_m in range(m):
            if grid[index_m][0] == 0:
                for index_n in range(n):
                    grid[index_m][index_n] = (grid[index_m][index_n]+1) % 2

        for index_n in range(n):
            sum_m = sum(grid[index_m][index_n] for index_m in range(m))
            if sum_m <= m//2:
                for index_m in range(m):
                    grid[index_m][index_n] = (grid[index_m][index_n]+1) % 2

        result = 0
        for row in grid:
            score = 0
            for bit in row:
                score = (score<<1) | bit
            result += score

        return result
```
