![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1463. [Cherry Pickup II](https://leetcode.com/problems/minimum-window-substring)

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(M*N^2)$, Space Complexity: $O(M*N^2)$) :
```python
class Solution:
    def cherryPickup(self, grid: List[List[int]]) -> int:
        m = len(grid)
        n = len(grid[0])
        memoization = defaultdict(int)
        return self.dfs(0, n-1, 0, memoization, grid)

    def dfs(self, index_1: int, index_2: int, index_row: int, memoization, grid) -> int:
        m = len(grid)
        if index_row >= m:
            return 0

        key = (index_1, index_2, index_row)
        if key in memoization:
            return memoization[key]

        result = 0
        n = len(grid[0])
        for index_1_next in range(max(0, index_1-1), min(n, index_1+2)):
            for index_2_next in range(max(0, index_2-1), min(n, index_2+2)):
                current = grid[index_row][index_1]
                if index_1 != index_2:
                    current += grid[index_row][index_2]

                result = max(result, current + self.dfs(index_1_next, index_2_next, index_row+1, memoization, grid))

        memoization[key] = result
        return result
```
