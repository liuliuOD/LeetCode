![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2328. [Number Of Increasing Paths In A Grid](https://leetcode.com/problems/number-of-increasing-paths-in-a-grid)

### Solution :

Method 1 (Dynamic Programming) :
```python
MOD = 10**9 + 7
class Solution:
    def countPaths(self, grid: List[List[int]]) -> int:
        self.grid = grid
        self.dp = [[-1]*len(grid[0]) for _ in range(len(grid))]

        result = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                result = (result + self.dynamicProgramming(i, j)) % MOD
        
        return result
    
    def dynamicProgramming(self, x: int, y: int) -> int:
        if self.dp[x][y] > 0:
            return self.dp[x][y]

        current = self.grid[x][y]
        result = 1
        if x+1 < len(self.grid) and current < self.grid[x+1][y]:
            result = (result + self.dynamicProgramming(x+1, y)) % MOD
        if x-1 >= 0 and current < self.grid[x-1][y]:
            result = (result + self.dynamicProgramming(x-1, y)) % MOD
        if y+1 < len(self.grid[0]) and current < self.grid[x][y+1]:
            result = (result + self.dynamicProgramming(x, y+1)) % MOD
        if y-1 >= 0 and current < self.grid[x][y-1]:
            result = (result + self.dynamicProgramming(x, y-1)) % MOD

        self.dp[x][y] = result
        return result
```

Method 2 (Dynamic Programming) :
```python
MOD = 10**9 + 7
class Solution:
    def countPaths(self, grid: List[List[int]]) -> int:
        self.grid = grid
        self.dp = [[-1]*len(grid[0]) for _ in range(len(grid))]

        result = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                result = (result + self.dynamicProgramming(i, j)) % MOD
        
        return result
    
    def dynamicProgramming(self, x: int, y: int) -> int:
        if self.dp[x][y] > 0:
            return self.dp[x][y]

        current = self.grid[x][y]
        result = 1
        for target_x, target_y in [(x+1, y), (x-1, y), (x, y+1), (x, y-1)]:
            if target_x >= 0 and target_x < len(self.grid) and target_y >= 0 and target_y < len(self.grid[0]) and current < self.grid[target_x][target_y]:
                result = (result + self.dynamicProgramming(target_x, target_y)) % MOD

        self.dp[x][y] = result
        return result
```
