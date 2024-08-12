![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1568. [Minimum Number Of Days To Disconnect Island](https://leetcode.com/problems/minimum-number-of-days-to-disconnect-island)

### Solution :

Method 1 (BFS) :
```python
class Solution:
    def minDays(self, grid: List[List[int]]) -> int:
        amount_islands = self.count_islands(grid)

        if amount_islands != 1:
            return 0

        num_visited_land = 2
        m, n = len(grid), len(grid[0])
        for index_m in range(m):
            for index_n in range(n):
                if grid[index_m][index_n] == 0:
                    continue

                grid[index_m][index_n] = 0
                if self.count_islands(grid, num_visited_land) != 1:
                    return 1

                num_visited_land += 1
                grid[index_m][index_n] = num_visited_land

        return 2

    def count_islands(self, grid: list[list[int]], num_land: int = 1):
        m, n = len(grid), len(grid[0])
        amount_islands = 0
        for index_m in range(m):
            for index_n in range(n):
                if grid[index_m][index_n] != num_land:
                    continue

                amount_islands += self.traverse(index_m, index_n, grid, num_land)

        return amount_islands

    def traverse(self, index_m: int, index_n: int, grid: list[list[int]], num_land: int = 1) -> int:
        grid[index_m][index_n] = num_land + 1

        m, n = len(grid), len(grid[0])
        queue = deque([(index_m, index_n)])
        while queue:
            index_m, index_n = queue.popleft()
            amount_adjacent_water = 0
            for offset_m, offset_n in [(0, 1), (0, -1), (1, 0), (-1, 0)]:
                index_m_next, index_n_next = index_m + offset_m, index_n + offset_n
                if index_m_next < 0 or index_m_next >= m or index_n_next < 0 or index_n_next >= n or grid[index_m_next][index_n_next] != num_land:
                    continue

                queue.append((index_m_next, index_n_next))
                grid[index_m_next][index_n_next] = num_land + 1

        return 1
```
