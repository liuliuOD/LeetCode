![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 279. [Perfect Squares](https://leetcode.com/problems/perfect-squares)

### Solution :

Method 1 (DFS + Memoization, ERROR: "Time Limit Exceeded", 581/588) :
```python
class Solution:
    def numSquares(self, n: int) -> int:
        squares = self.getSquares(n)
        memoization = defaultdict(lambda: inf)
        return self.dfs(0, memoization, squares, n)

    def getSquares(self, n: int) -> List[int]:
        result = []
        for num in reversed(range(1, int(math.sqrt(n))+1)):
            result.append(num ** 2)

        return result

    def dfs(self, index: int, memoization, squares, n) -> int:
        if n < 0 or index >= len(squares):
            return inf

        if n == 0:
            return 0

        key = (index, n)
        if key in memoization:
            return memoization[key]

        result = min(1+self.dfs(index, memoization, squares, n-squares[index]), 1+self.dfs(index+1, memoization, squares, n-squares[index]), self.dfs(index+1, memoization, squares, n))

        memoization[key] = result
        return result
```

Method 2 (Dynamic Programming, Time Complexity: $O(M*N)$ (M: amount of squares, N: value of `n`), Space Complexity: $O(N)$) :
```python
class Solution:
    def numSquares(self, n: int) -> int:
        squares = self.getSquares(n)
        dp = [inf for _ in range(n+1)]
        dp[0] = 0
        for target in range(1, n+1):
            for square in squares:
                if target - square < 0:
                    continue

                dp[target] = min(dp[target], 1 + dp[target-square])

        return dp[n]

    def getSquares(self, n: int) -> List[int]:
        squares = []
        for num in range(1, int(math.sqrt(n))+1):
            squares.append(num ** 2)

        return squares
```
