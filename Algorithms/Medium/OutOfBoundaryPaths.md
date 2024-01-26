![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 576. [Out Of Boundary Paths](https://leetcode.com/problems/out-of-boundary-paths)

### Solution :

Method 1 (BFS, ERROR: "Memory Limit Exceeded", 76/94)
```python
MODULO: int = 1_000_000_007

class Solution:
    def findPaths(self, m: int, n: int, max_move: int, start_row: int, start_column: int) -> int:
        if max_move == 0:
            return 0

        queue = deque([(start_row, start_column, max_move)])
        result = 0
        while queue:
            index_m, index_n, remaining_move = queue.popleft()

            for offset_m, offset_n in [(-1, 0), (0, -1), (0, 1), (1, 0)]:
                index_m_next = index_m + offset_m
                index_n_next = index_n + offset_n
                if index_m_next < 0 or index_m_next >= m or index_n_next < 0 or index_n_next >= n:
                    result = (result + 1) % MODULO
                    continue
                if remaining_move <= 1:
                    continue

                queue.append((index_m_next, index_n_next, remaining_move-1))

        return result
```

Method 2 (DFS + Memoization, Time Complexity: $O(M*N*K)$ (K: value of `maxMove`), Space Complexity: $O(M*N*K)$) :
```python
MODULO: int = 1_000_000_007
class Solution:
    def findPaths(self, m: int, n: int, maxMove: int, startRow: int, startColumn: int) -> int:
        memoization = defaultdict(int)
        return self.dfs(maxMove, startRow, startColumn, memoization, m, n)

    def dfs(self, remainingMove: int, indexM: int, indexN: int, memoization: Dict, m: int, n: int) -> int:
        if remainingMove < 0:
            return 0

        if indexM >= m or indexM < 0 or indexN >= n or indexN < 0:
            return 1

        key = (indexM, indexN, remainingMove)
        if key in memoization:
            return memoization[key]

        result = 0
        for offsetM, offsetN in [(-1, 0), (0, -1), (0, 1), (1, 0)]:
            result += self.dfs(remainingMove-1, indexM+offsetM, indexN+offsetN, memoization, m, n)

        memoization[key] = result % MODULO
        return memoization[key]
```

Method 3 (Dynamic Programming, Time Complexity: $O(M*N*K)$ (K: value of `maxMove`), Space Complexity: $O(M*N)$) :
```python
MODULO: int = 1_000_000_007

class Solution:
    def findPaths(self, m: int, n: int, max_move: int, start_row: int, start_column: int) -> int:
        dp = [[0]*n for _ in range(m)]
        dp[start_row][start_column] = 1
        result = 0
        for move in range(1, max_move+1):
            temp = [[0]*n for _ in range(m)]
            for index_m in range(m):
                for index_n in range(n):
                    times = 0
                    if index_m == 0:
                        times += 1
                    if index_m == m-1:
                        times += 1
                    if index_n == 0:
                        times += 1
                    if index_n == n-1:
                        times += 1
                    result = (result + dp[index_m][index_n]*times) % MODULO

                    if index_m > 0:
                        temp[index_m][index_n] = (temp[index_m][index_n] + dp[index_m-1][index_n]) % MODULO
                    if index_m < m-1:
                        temp[index_m][index_n] = (temp[index_m][index_n] + dp[index_m+1][index_n]) % MODULO
                    if index_n > 0:
                        temp[index_m][index_n] = (temp[index_m][index_n] + dp[index_m][index_n-1]) % MODULO
                    if index_n < n-1:
                        temp[index_m][index_n] = (temp[index_m][index_n] + dp[index_m][index_n+1]) % MODULO

            dp = temp

        return result
```
