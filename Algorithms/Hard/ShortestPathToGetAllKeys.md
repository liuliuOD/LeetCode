![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 864. [Shortest Path To Get All Keys](https://leetcode.com/problems/shortest-path-to-get-all-keys)

### Solution :

Method 1 (BFS) :
```python
class Solution:
    def shortestPathAllKeys(self, grid: List[str]) -> int:
        m = len(grid)
        n = len(grid[0])
        total_keys_amount = 0
        queue = deque([])
        for index_m in range(m):
            for index_n in range(n):
                value = grid[index_m][index_n]
                if value == '@':
                    queue.append((index_m, index_n, tuple(), 0))
                elif value.islower():
                    total_keys_amount += 1

        visited = set()
        while queue:
            x, y, current_keys, current_moves = queue.popleft()
            next_moves = current_moves + 1

            if (x, y, current_keys) in visited:
                continue
            visited.add((x, y, current_keys))

            for offset_x, offset_y in [(0, -1), (0, 1), (-1, 0), (1, 0)]:
                next_x, next_y = x+offset_x, y+offset_y
                # block the following statuses: 1. next step is out of the grid, 2. next step has already been visited with current keys, 3. next step is a wall (#), 4. next step is a lock (uppercase) and the key hasn't been obtained yet
                if next_x < 0 or next_x >= m or next_y < 0 or next_y >= n or (next_x, next_y, current_keys) in visited or grid[next_x][next_y] == '#' or (grid[next_x][next_y].isupper() and grid[next_x][next_y].lower() not in current_keys):
                    continue

                next_keys = set(current_keys)
                if grid[next_x][next_y].islower():
                    next_keys.add(grid[next_x][next_y])
                    if len(next_keys) == total_keys_amount:
                        return next_moves
                
                queue.append((next_x, next_y, tuple(next_keys), next_moves))

        return -1
```
