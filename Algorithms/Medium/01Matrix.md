![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 542. [01 Matrix](https://leetcode.com/problems/01-matrix)

### Solution :

Method 1 (BFS, ERROR: "Time Limit Exceeded", 49/50) :
```python
class Solution:
    def updateMatrix(self, mat: List[List[int]]) -> List[List[int]]:
        m = len(mat)
        n = len(mat[0])
        result = [[-1]*n for _ in range(m)]
        queue = deque()
        for index_m in range(m):
            for index_n in range(n):
                queue.append((index_m, index_n, index_m, index_n, 0))

        visited = set()
        while queue:
            index_m, index_n, index_m_moved, index_n_moved, distance = queue.popleft()

            key_visited = f'{index_m}-{index_n}-{index_m_moved}-{index_n_moved}'
            if key_visited in visited:
                continue
            visited.add(key_visited)

            if result[index_m][index_n] >= 0:
                continue

            if mat[index_m_moved][index_n_moved] == 0:
                result[index_m][index_n] = distance
                continue

            for offset_m, offset_n in [(1, 0), (0, 1), (-1, 0), (0, -1)]:
                index_m_next, index_n_next = index_m_moved+offset_m, index_n_moved+offset_n
                if index_m_next < 0 or index_m_next >= m or index_n_next < 0 or index_n_next >= n:
                    continue

                queue.append((index_m, index_n, index_m_next, index_n_next, distance+1))

        return result
```

Method 2 (BFS) :
```python
class Solution:
    def updateMatrix(self, mat: List[List[int]]) -> List[List[int]]:
        m = len(mat)
        n = len(mat[0])
        result = [[-1]*n for _ in range(m)]
        queue = deque()
        for index_m in range(m):
            for index_n in range(n):
                if mat[index_m][index_n] == 0:
                    queue.append((index_m, index_n))

        distance = 0
        visited = set()
        while queue:
            for _ in range(len(queue)):
                index_m, index_n = queue.popleft()

                visited.add((index_m, index_n))

                result[index_m][index_n] = distance

                for offset_m, offset_n in [(1, 0), (0, 1), (-1, 0), (0, -1)]:
                    index_m_next, index_n_next = index_m+offset_m, index_n+offset_n
                    if index_m_next < 0 or index_m_next >= m or index_n_next < 0 or index_n_next >= n or (index_m_next, index_n_next) in visited or mat[index_m_next][index_n_next] == 0:
                        continue

                    queue.append((index_m_next, index_n_next))
                    visited.add((index_m_next, index_n_next))

            distance += 1
        return result
```

Method 3 (BFS) :
```python
class Solution:
    def updateMatrix(self, mat: List[List[int]]) -> List[List[int]]:
        m = len(mat)
        n = len(mat[0])
        result = [[-1]*n for _ in range(m)]
        queue = deque()
        for index_m in range(m):
            for index_n in range(n):
                if mat[index_m][index_n] == 0:
                    queue.append((index_m, index_n, 0))

        visited = set()
        while queue:
            index_m, index_n, distance = queue.popleft()

            visited.add((index_m, index_n))

            result[index_m][index_n] = distance

            for offset_m, offset_n in [(1, 0), (0, 1), (-1, 0), (0, -1)]:
                index_m_next, index_n_next = index_m+offset_m, index_n+offset_n
                if index_m_next < 0 or index_m_next >= m or index_n_next < 0 or index_n_next >= n or (index_m_next, index_n_next) in visited or mat[index_m_next][index_n_next] == 0:
                    continue

                queue.append((index_m_next, index_n_next, distance+1))
                visited.add((index_m_next, index_n_next))

        return result
```
