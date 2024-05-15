![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2812. [Find The Safest Path In A Grid](https://leetcode.com/problems/find-the-safest-path-in-a-grid)

### Solution :

Method 1 (BFS + Binary Search, Time Complexity: $O(N^2*Log(N))$ (N: length of `grid`), Space Complexity: $O(N^2)$) :
```python
class Solution:
    def maximumSafenessFactor(self, grid: List[List[int]]) -> int:
        grid = self.bfs(grid)

        return self.binary_search(grid)

    # Option 1
    def bfs(self, grid: list[list[int]]) -> list[list[int]]:
        n = len(grid)
        queue = deque()
        for index_m in range(n):
            for index_n in range(n):
                current = -1
                if grid[index_m][index_n] == 1:
                    current = 0
                    queue.append((index_m, index_n, 0))

                grid[index_m][index_n] = current

        while queue:
            index_m, index_n, distance = queue.popleft()

            for offset_m, offset_n in [(0, 1), (0, -1), (1, 0), (-1, 0)]:
                index_m_next = index_m + offset_m
                index_n_next = index_n + offset_n
                if 0 <= index_m_next < n and 0 <= index_n_next < n and grid[index_m_next][index_n_next] == -1:
                    grid[index_m_next][index_n_next] = distance + 1
                    queue.append((index_m_next, index_n_next, distance+1))

        return grid
    """
    # Option 2

    def bfs(self, grid: list[list[int]]) -> list[list[int]]:
        n = len(grid)
        queue = deque()
        for index_m in range(n):
            for index_n in range(n):
                current = -1
                if grid[index_m][index_n] == 1:
                    current = 0
                    queue.append((index_m, index_n))

                grid[index_m][index_n] = current

        while queue:
            index_m, index_n = queue.popleft()
            distance = grid[index_m][index_n]
            for offset_m, offset_n in [(0, 1), (0, -1), (1, 0), (-1, 0)]:
                index_m_next = index_m + offset_m
                index_n_next = index_n + offset_n
                if 0 <= index_m_next < n and 0 <= index_n_next < n and grid[index_m_next][index_n_next] == -1:
                    grid[index_m_next][index_n_next] = distance + 1
                    queue.append((index_m_next, index_n_next))

        return grid
    """

    def binary_search(self, grid: list[list[int]]) -> list[list[int]]:
        left = 0
        right = len(grid) - 1
        while left <= right:
            middle = left + (right - left)//2
            if self.bfs_safe(grid, middle):
                left = middle + 1
            else:
                right = middle - 1

        return right

    def bfs_safe(self, grid: list[list[int]], threshold: int) -> bool:
        n = len(grid)
        visited: list[list[bool]] = [[False]*n for _ in range(n)]
        queue = deque([(0, 0)])
        while queue:
            index_m, index_n = queue.popleft()
            if grid[index_m][index_n] < threshold:
                continue
            if visited[index_m][index_n]:
                continue
            visited[index_m][index_n] = True

            if index_m == index_n == n-1:
                return True

            for offset_m, offset_n in [(0, 1), (0, -1), (1, 0), (-1, 0)]:
                index_m_next = index_m + offset_m
                index_n_next = index_n + offset_n
                if 0 <= index_m_next < n and 0 <= index_n_next < n and grid[index_m_next][index_n_next] >= threshold:
                    queue.append((index_m_next, index_n_next))

        return False
```

Method 2 (BFS + Dijkstra, Time Complexity: $O(N^2*Log(N))$ (N: length of `grid`), Space Complexity: $O(N^2)$) :
```python
class Solution:
    def maximumSafenessFactor(self, grid: List[List[int]]) -> int:
        grid = self.bfs(grid)

        return self.dijkstra(grid)

    def bfs(self, grid: list[list[int]]) -> list[list[int]]:
        n = len(grid)
        queue = deque()
        for index_m in range(n):
            for index_n in range(n):
                current = -1
                if grid[index_m][index_n] == 1:
                    current = 0
                    queue.append((index_m, index_n))

                grid[index_m][index_n] = current

        while queue:
            index_m, index_n = queue.popleft()
            distance = grid[index_m][index_n]
            for offset_m, offset_n in [(0, 1), (0, -1), (1, 0), (-1, 0)]:
                index_m_next = index_m + offset_m
                index_n_next = index_n + offset_n
                if 0 <= index_m_next < n and 0 <= index_n_next < n and grid[index_m_next][index_n_next] == -1:
                    grid[index_m_next][index_n_next] = distance + 1
                    queue.append((index_m_next, index_n_next))

        return grid

    def dijkstra(self, grid: list[list[int]]) -> int:
        n = len(grid)
        heap = [(-grid[0][0], 0, 0)]
        grid[0][0] = -1
        while heap:
            distance, index_m, index_n = heapq.heappop(heap)
            if index_m == index_n == n-1:
                return -distance

            for offset_m, offset_n in [(0, 1), (0, -1), (1, 0), (-1, 0)]:
                index_m_next = index_m + offset_m
                index_n_next = index_n + offset_n
                if 0 <= index_m_next < n and 0 <= index_n_next < n and grid[index_m_next][index_n_next] != -1:
                    # Option 1
                    heapq.heappush(heap, (max(distance, -grid[index_m_next][index_n_next]), index_m_next, index_n_next))
                    """
                    # Option 2

                    heapq.heappush(heap, (-min(-distance, grid[index_m_next][index_n_next]), index_m_next, index_n_next))
                    grid[index_m_next][index_n_next] = -1
                    """

        return 0
```
