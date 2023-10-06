![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 343. [Integer Break](https://leetcode.com/problems/integer-break)

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def integerBreak(self, n: int) -> int:
        if n <= 3:
            return n - 1

        memoization = {}
        return self.dfs(n, memoization)

    def dfs(self, n: int, memoization: Dict[int, int]) -> int:
        if n in memoization:
            return memoization[n]

        maximum = 1
        for num in range(1, n+1):
            maximum = max(maximum, num * self.dfs(n-num, memoization))

        memoization[n] = maximum

        return maximum
```

Method 2 (Dynamic Programming) :
```python
class Solution:
    def integerBreak(self, n: int) -> int:
        if n <= 3:
            return n - 1

        # Option 1
        dp = defaultdict(int)
        dp[1], dp[2], dp[3] = 1, 2, 3
        for num in range(4, n+1):
            for offset in range(2, num):
                dp[num] = max(dp[num], offset*dp[num-offset])
        """
        # Option 2

        dp = {1: 1, 2: 2, 3: 3}
        for num in range(4, n+1):
            for offset in range(2, num):
                dp[num] = max(dp.get(num, 0), offset*dp[num-offset])
        """

        return dp[n]
```
