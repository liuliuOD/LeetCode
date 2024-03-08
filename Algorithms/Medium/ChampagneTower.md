![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 799. [Champagne Tower](https://leetcode.com/problems/champagne-tower)

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def champagneTower(self, poured: int, query_row: int, query_glass: int) -> float:
        memoization = {}
        full = self.dfs(poured, query_row, query_glass, memoization)
        return 1 if full > 1 else full

    def dfs(self, poured: int, query_row: int, query_glass: int, memoization):
        key = (query_row, query_glass)
        if key in memoization:
            return memoization[key]

        if poured <= 0 or query_row < 0 or query_glass < 0:
            return 0

        if query_row == 0 and query_glass == 0:
            return poured

        memoization[key] = max(0, (self.dfs(poured, query_row-1, query_glass-1, memoization)-1)/2) + max(0, (self.dfs(poured, query_row-1, query_glass, memoization)-1)/2)

        return memoization[key]
```

Method 2 (Dynamic Programming) :
```python
class Solution:
    def champagneTower(self, poured: int, query_row: int, query_glass: int) -> float:
        dp = [poured]
        for amount_level in range(2, query_row+2):
            dp_next = [0] * amount_level
            for index in range(amount_level):
                dp_next[index] = 0
                if index > 0:
                    dp_next[index] += max(0, (dp[index-1]-1) / 2)
                if index < amount_level-1:
                    dp_next[index] += max(0, (dp[index]-1) / 2)
            dp = dp_next

        return 1 if dp[query_glass] >= 1 else dp[query_glass]
```
