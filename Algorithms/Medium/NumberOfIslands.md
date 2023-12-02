![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 200. [Number Of Islands](https://leetcode.com/problems/number-of-islands)

### Solution :

Method 1 (DFS) :
```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        m = len(grid)
        n = len(grid[0])
        result = 0
        for index_m in range(m):
            for index_n in range(n):
                if grid[index_m][index_n] != "1":
                    continue

                result += 1
                grid[index_m][index_n] = result
                stack = [(index_m, index_n)]
                while stack:
                    index_m_current, index_n_current = stack.pop()
                    # Option 1
                    if index_m_current > 0 and grid[index_m_current-1][index_n_current] == "1":
                        grid[index_m_current-1][index_n_current] = result
                        stack.append((index_m_current-1, index_n_current))

                    if index_n_current > 0 and grid[index_m_current][index_n_current-1] == "1":
                        grid[index_m_current][index_n_current-1] = result
                        stack.append((index_m_current, index_n_current-1))

                    if index_m_current < m-1 and grid[index_m_current+1][index_n_current] == "1":
                        grid[index_m_current+1][index_n_current] = result
                        stack.append((index_m_current+1, index_n_current))

                    if index_n_current < n-1 and grid[index_m_current][index_n_current+1] == "1":
                        grid[index_m_current][index_n_current+1] = result
                        stack.append((index_m_current, index_n_current+1))
                    """
                    # Option 2

                    for offset_m, offset_n in [(-1, 0), (0, -1), (1, 0), (0, 1)]:
                        index_m_next = index_m_current + offset_m
                        index_n_next = index_n_current + offset_n
                        if 0 <= index_m_next < m and 0 <= index_n_next < n and grid[index_m_next][index_n_next] == "1":
                            grid[index_m_next][index_n_next] = result
                            stack.append((index_m_next, index_n_next))
                    """

        return result
```

Method 2 (BFS) :
```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        m = len(grid)
        n = len(grid[0])
        result = 0
        for index_m in range(m):
            for index_n in range(n):
                if grid[index_m][index_n] != "1":
                    continue

                result += 1
                grid[index_m][index_n] = result
                queue = deque([(index_m, index_n)])
                while queue:
                    index_m_current, index_n_current = queue.popleft()
                    for offset_m, offset_n in [(-1, 0), (0, -1), (1, 0), (0, 1)]:
                        index_m_next = index_m_current + offset_m
                        index_n_next = index_n_current + offset_n
                        if 0 <= index_m_next < m and 0 <= index_n_next < n and grid[index_m_next][index_n_next] == "1":
                            grid[index_m_next][index_n_next] = result
                            queue.append((index_m_next, index_n_next))

        return result
```
