![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 931. [Minimum Falling Path Sum](https://leetcode.com/problems/minimum-falling-path-sum)

### Solution :

Method 1 (DFS, Time Complexity: $O(N^2)$, Space Complexity: $O(N^2)$) :
```python
class Solution:
    def minFallingPathSum(self, matrix: List[List[int]]) -> int:
        memoization = defaultdict(lambda: inf)
        result = inf
        for y in range(len(matrix[0])):
            result = min(result, self.dfs(0, y, memoization, matrix))

        return result

    def dfs(self, x: int, y: int, memoization: Dict[Tuple[int, int], int], matrix: List[List[int]]) -> int:
        m = len(matrix)
        n = len(matrix[0])
        if x >= m or y < 0 or y >= n:
            return inf

        current = matrix[x][y]
        if x == m-1:
            return current

        key = (x, y)
        if key in memoization:
            return memoization[key]

        result = current + min(self.dfs(x+1, y-1, memoization, matrix), self.dfs(x+1, y, memoization, matrix), self.dfs(x+1, y+1, memoization, matrix))
        memoization[key] = result
        return result
```
