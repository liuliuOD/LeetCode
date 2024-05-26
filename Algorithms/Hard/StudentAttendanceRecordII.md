![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 552. [Student Attendance Record II](https://leetcode.com/problems/student-attendance-record-ii)

### Solution :

Method 1 (DFS + Memoization, ERROR: "Memory Limit Exceeded", 28/59, Time Complexity: $O(N)$, Space Complexity; $O(N)$) :
```python
MODULO = 1_000_000_007

class Solution:
    def checkRecord(self, n: int) -> int:
        if n == 0:
            return 1

        return self.dfs(n, 0, 0, {}) % MODULO

    def dfs(self, n: int, a: int, l: int, memoization: dict[tuple[int, int, int], int]) -> int:
        if n == 0:
            return 1

        key = (n, a, l)
        if key in memoization:
            return memoization[key]

        result = self.dfs(n-1, a, 0, memoization)
        if l < 2:
            result += self.dfs(n-1, a, l+1, memoization)
        if a < 1:
            result += self.dfs(n-1, a+1, 0, memoization)

        memoization[key] = result
        return result
```

Method 2 (DFS + Built-In LRU-Cache, ERROR: "Time Limit Exceeded", 47/59, Time Complexity: $O(N)$, Space Complexity; $O(N)$) :
```python
MODULO = 1_000_000_007

class Solution:
    def checkRecord(self, n: int) -> int:
        if n == 0:
            return 1

        return self.dfs(n, 0, 0) % MODULO

    @lru_cache
    def dfs(self, n: int, a: int, l: int) -> int:
        if n == 0:
            return 1

        result = self.dfs(n-1, a, 0)
        if l < 2:
            result += self.dfs(n-1, a, l+1)
        if a < 1:
            result += self.dfs(n-1, a+1, 0)

        return result
```

Method 3 (DFS + Built-In Cache, ERROR: "Memory Limit Exceeded", 39/59, Time Complexity: $O(N)$, Space Complexity; $O(N)$) :
```python
MODULO = 1_000_000_007

class Solution:
    def checkRecord(self, n: int) -> int:
        if n == 0:
            return 1

        return self.dfs(n, 0, 0)

    @cache
    def dfs(self, n: int, a: int, l: int) -> int:
        if n == 0:
            return 1

        result = self.dfs(n-1, a, 0)
        if l < 2:
            result += self.dfs(n-1, a, l+1)
        if a < 1:
            result += self.dfs(n-1, a+1, 0)

        return result % MODULO
```

Method 4 (DFS + Memoization, Time Complexity: $O(N)$, Space Complexity; $O(N)$) :
```python
MODULO = 1_000_000_007

class Solution:
    def checkRecord(self, n: int) -> int:
        if n == 0:
            return 1

        return self.dfs(n, 0, 0, {})

    def dfs(self, n: int, a: int, l: int, memoization: dict[tuple[int, int, int], int]) -> int:
        if n == 0:
            return 1

        key = (n, a, l)
        if key in memoization:
            return memoization[key]

        result = self.dfs(n-1, a, 0, memoization)
        if l < 2:
            result += self.dfs(n-1, a, l+1, memoization)
        if a < 1:
            result += self.dfs(n-1, a+1, 0, memoization)

        memoization[key] = result % MODULO
        return memoization[key]
```

Method 5 (DFS + Memoization, Time Complexity: $O(N)$, Space Complexity; $O(N)$) :
```python
MODULO = 1_000_000_007

class Solution:
    def checkRecord(self, n: int) -> int:
        if n == 0:
            return 1

        def dfs(n: int, a: int, l: int) -> int:
            if n == 0:
                return 1

            if memoization[n][a][l] > -1:
                return memoization[n][a][l]

            result = dfs(n-1, a, 0)
            if l < 2:
                result += dfs(n-1, a, l+1)
            if a < 1:
                result += dfs(n-1, a+1, 0)

            memoization[n][a][l] = result % MODULO
            return memoization[n][a][l]

        memoization: list[list[list[int]]] = [[[-1]*3 for _ in range(2)] for _ in range(n+1)]
        return dfs(n, 0, 0)
```
