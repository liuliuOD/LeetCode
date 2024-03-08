![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
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

Method 2 (Dynamic Programming, Time Complexity: $O(M*N^2)$, Space Complexity: $O(M*N^2)$) :
```python
class Solution:
    def cherryPickup(self, grid: List[List[int]]) -> int:
        m = len(grid)
        n = len(grid[0])
        dp = [[[-1]*n for _ in range(n)] for _ in range(m)]
        dp[0][0][-1] = grid[0][0] + grid[0][-1]
        for index_m in range(m-1):
            for index_1 in range(n):
                for index_2 in range(n):
                    if dp[index_m][index_1][index_2] == -1:
                        continue

                    current = 0
                    for offset_1 in range(-1, 2):
                        index_1_next = index_1 + offset_1
                        if index_1_next < 0 or index_1_next >= n:
                            continue

                        for offset_2 in range(-1, 2):
                            index_2_next = index_2 + offset_2
                            if index_2_next < 0 or index_2_next >= n:
                                continue

                            current = dp[index_m][index_1][index_2] + grid[index_m+1][index_1_next]
                            if index_1_next != index_2_next:
                                current += grid[index_m+1][index_2_next]

                            dp[index_m+1][index_1_next][index_2_next] = max(dp[index_m+1][index_1_next][index_2_next], current)

        return max([max(row) for row in dp[-1]])
```

Method 3 (Dynamic Programming + Optimization, Time Complexity: $O(M*N^2)$, Space Complexity: $O(N^2)$) :
```python
class Solution:
    def cherryPickup(self, grid: List[List[int]]) -> int:
        m = len(grid)
        n = len(grid[0])
        dp = [[-1]*n for _ in range(n)]
        dp[0][-1] = grid[0][0] + grid[0][-1]
        for index_m in range(m-1):
            temp = [[-1]*n for _ in range(n)]
            for index_1 in range(n):
                for index_2 in range(n):
                    if dp[index_1][index_2] == -1:
                        continue

                    current = 0
                    for offset_1 in range(-1, 2):
                        index_1_next = index_1 + offset_1
                        if index_1_next < 0 or index_1_next >= n:
                            continue

                        for offset_2 in range(-1, 2):
                            index_2_next = index_2 + offset_2
                            if index_2_next < 0 or index_2_next >= n:
                                continue

                            current = dp[index_1][index_2] + grid[index_m+1][index_1_next]
                            if index_1_next != index_2_next:
                                current += grid[index_m+1][index_2_next]

                            temp[index_1_next][index_2_next] = max(temp[index_1_next][index_2_next], current)

            dp = temp

        return max([max(row) for row in dp])
```
