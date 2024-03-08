![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1091. [Shortest Path In Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix)

### Solution :

Method 1 (BFS) :
```python
THRESHOLD = 10001
class Solution:
    def shortestPathBinaryMatrix(self, grid: List[List[int]]) -> int:
        self.n = len(grid)
        self.grid = grid
        self.path = [[THRESHOLD] * self.n for _ in range(self.n)]
        if grid[0][0] == 1:
            return -1

        queue = collections.deque([(0, 0, 1)])
        while queue:
            x, y, current_value = queue.popleft()
            if x == y == self.n - 1:
                return current_value

            for offset_x, offset_y in [[0, 1], [1, 1], [1, 0], [1, -1], [0, -1], [-1, -1], [-1, 0], [-1, 1]]:
                target_x = x + offset_x
                target_y = y + offset_y
                if target_x < 0 or target_x >= self.n or target_y < 0 or target_y >= self.n or self.path[target_x][target_y] <= current_value or self.grid[target_x][target_y] is not 0:
                    continue
                self.grid[target_x][target_y] = -1

                queue.append((target_x, target_y, current_value + 1))

        return -1
```

Method 2 (DFS) :
```python
```
