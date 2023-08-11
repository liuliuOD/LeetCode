![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 518. [Coin Change II](https://leetcode.com/problems/coin-change-ii)

### Solution :

Method 1 (ERROR: "Time Limit Exceeded", 14/28) :
```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        return self.dfs(amount, 0, coins)

    def dfs(self, amount: int, index_current: int, coins: List[int]) -> int:
        if amount == 0:
            return 1

        if amount < 0:
            return 0

        result = 0
        for index_coin in range(index_current, len(coins)):
            result += self.dfs(amount-coins[index_coin], index_coin, coins)

        return result
```

Method 2 (DFS + Memoization) :
```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        memoization: Dict[int, Dict[int, int]] = defaultdict(dict) # index_current -> amount
        self.dfs(amount, memoization, 0, coins)

        return memoization[0][amount] if amount in memoization[0] else 1

    def dfs(self, amount: int, memoization: Dict[int, int], index_current: int, coins: List[int]) -> int:
        if amount == 0:
            return 1
        elif amount < 0 or index_current >= len(coins):
            return 0

        if index_current in memoization and amount in memoization[index_current]:
            return memoization[index_current][amount]

        result = 0
        for index_coin in range(index_current, len(coins)):
            result += self.dfs(amount-coins[index_coin], memoization, index_coin, coins)

        memoization[index_current][amount] = result
        return memoization[index_current][amount]
```

Method 3 (Dynamic Programming, 2D) :
```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        n = len(coins)
        dp = [[0]*(amount+1) for _ in range(n+1)]
        dp[0][0] = 1

        for index_coin in range(n):
            for current_amount in range(amount+1):
                index_dp = index_coin + 1
                dp[index_dp][current_amount] = dp[index_dp-1][current_amount]
                if coins[index_coin] <= current_amount:
                    dp[index_dp][current_amount] += dp[index_dp][current_amount-coins[index_coin]]

        return dp[n][amount]
```

Method 4 (Dynamic Programming, 1D) :
```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        dp = [0] * (amount+1)
        dp[0] = 1

        for index_coin in range(len(coins)):
            for current_amount in range(amount+1):
                if coins[index_coin] <= current_amount:
                    dp[current_amount] += dp[current_amount-coins[index_coin]]

        return dp[amount]
```
