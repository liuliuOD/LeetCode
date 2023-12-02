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

Method 3 (Union Find, Time Complexity: $O(M*N^2)$, Space Complexity: $O(M*N)$) :
```python
class UnionFind:
    def __init__(self, n: int):
        self.parents = list(range(n))

    def find(self, target: int) -> int:
        while self.parents[target] != target:
            target = self.parents[target]

        return target

    def union(self, a: int, b: int) -> bool:
        parent_a, parent_b = self.find(a), self.find(b)
        if parent_a == parent_b:
            return False

        self.parents[parent_a] = parent_b
        return True

class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        m = len(grid)
        n = len(grid[0])
        union_find = UnionFind(m*n)
        result = 0
        for index_m in range(m):
            for index_n in range(n):
                if grid[index_m][index_n] == "0":
                    continue

                result += 1
                node_current = n*index_m + index_n
                for offset in [(0, 1), (1, 0), (0, -1), (-1, 0)]:
                    index_m_next, index_n_next = index_m+offset[0], index_n+offset[1]
                    if index_m_next < 0 or index_m_next >= m or index_n_next < 0 or index_n_next >= n or grid[index_m_next][index_n_next] == "0":
                        continue

                    node_neighbor = n*index_m_next + index_n_next
                    if union_find.union(node_current, node_neighbor):
                        result -= 1

        return result
```

Method 4 ([Union Find + Path Compression](https://leetcode.com/problems/number-of-islands/?envType=list&envId=rzn6xok2), Time Complexity: $O(M*N*Log(M*N))$, Space Complexity: $O(M*N)$) :
```python
class UnionFind:
    def __init__(self, n: int):
        self.parents = list(range(n))

    def find(self, target: int) -> int:
        # Path Compression
        if self.parents[target] != target:
            self.parents[target] = self.find(self.parents[target])

        return self.parents[target]

    def union(self, a: int, b: int) -> bool:
        parent_a, parent_b = self.find(a), self.find(b)
        if parent_a == parent_b:
            return False

        self.parents[parent_a] = parent_b
        return True

class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        m = len(grid)
        n = len(grid[0])
        union_find = UnionFind(m*n)
        result = 0
        for index_m in range(m):
            for index_n in range(n):
                if grid[index_m][index_n] == "0":
                    continue

                result += 1
                node_current = n*index_m + index_n
                for offset in [(0, 1), (1, 0), (0, -1), (-1, 0)]:
                    index_m_next, index_n_next = index_m+offset[0], index_n+offset[1]
                    if index_m_next < 0 or index_m_next >= m or index_n_next < 0 or index_n_next >= n or grid[index_m_next][index_n_next] == "0":
                        continue

                    node_neighbor = n*index_m_next + index_n_next
                    if union_find.union(node_current, node_neighbor):
                        result -= 1

        return result
```
