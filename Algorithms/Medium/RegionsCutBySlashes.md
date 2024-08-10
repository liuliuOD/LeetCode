![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 959. [Regions Cut By Slashes](https://leetcode.com/problems/regions-cut-by-slashes)

### Solution :

Method 1 (BFS, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$) :
```python
MULTIPLIER = 3

class Solution:
    def regionsBySlashes(self, grid: List[str]) -> int:
        m, n = len(grid), len(grid[0])
        graph = [[0]*n*MULTIPLIER for _ in range(m*MULTIPLIER)]
        for index_m in range(m):
            for index_n in range(n):
                value = grid[index_m][index_n]
                match value:
                    # Option 1
                    case "/":
                        graph[index_m*MULTIPLIER][index_n*MULTIPLIER+2] = 1
                        graph[index_m*MULTIPLIER+1][index_n*MULTIPLIER+1] = 1
                        graph[index_m*MULTIPLIER+2][index_n*MULTIPLIER] = 1
                    case "\\":
                        graph[index_m*MULTIPLIER][index_n*MULTIPLIER] = 1
                        graph[index_m*MULTIPLIER+1][index_n*MULTIPLIER+1] = 1
                        graph[index_m*MULTIPLIER+2][index_n*MULTIPLIER+2] = 1
                    """
                    # Option 2

                    case "/":
                        for offset in range(MULTIPLIER):
                            graph[index_m*MULTIPLIER+offset][index_n*MULTIPLIER+MULTIPLIER-offset-1] = 1
                    case "\\":
                        for offset in range(MULTIPLIER):
                            graph[index_m*MULTIPLIER+offset][index_n*MULTIPLIER+offset] = 1
                    """

        result = 0
        for index_m in range(len(graph)):
            for index_n in range(len(graph[0])):
                if graph[index_m][index_n] == 1:
                    continue

                result += 1
                self.filled(index_m, index_n, graph)

        return result

    def filled(self, index_m: int, index_n: int, graph: list[list[int]]) -> None:
        m, n = len(graph), len(graph[0])
        queue = deque([(index_m, index_n)])
        while queue:
            index_m_current, index_n_current = queue.popleft()
            if graph[index_m_current][index_n_current] == 1:
                continue
            graph[index_m_current][index_n_current] = 1

            for offset_m, offset_n in [(0, 1), (0, -1), (1, 0), (-1, 0)]:
                index_m_next = index_m_current + offset_m
                index_n_next = index_n_current + offset_n
                if index_m_next < 0 or m <= index_m_next or index_n_next < 0 or n <= index_n_next or graph[index_m_next][index_n_next] == 1:
                    continue

                queue.append((index_m_next, index_n_next))
```
