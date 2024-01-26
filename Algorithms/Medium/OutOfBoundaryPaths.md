![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 576. [Out Of Boundary Paths](https://leetcode.com/problems/out-of-boundary-paths)

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(M*N*K)$ (K: value of `maxMove`), Space Complexity: $O(M*N*K)$) :
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
