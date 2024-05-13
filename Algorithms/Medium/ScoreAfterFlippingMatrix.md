![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 861. [Score After Flipping Matrix](https://leetcode.com/problems/score-after-flipping-matrix)

### Solution :

Method 1 (Greedy + Modify Input, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$) :
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

Method 2 (Greedy + Without Modify Input, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def matrixScore(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        result = m * (1<<(n-1))
        for index_n in range(1, n):
            count_one = 0
            for index_m in range(m):
                current = grid[index_m][index_n]
                if (current == 0 and grid[index_m][0] == 0) or (current == 1 and grid[index_m][0] == 1):
                    count_one += 1

            if count_one <= m//2:
                count_one = m - count_one

            result += count_one * (1<<(n-index_n-1))

        return result
```
