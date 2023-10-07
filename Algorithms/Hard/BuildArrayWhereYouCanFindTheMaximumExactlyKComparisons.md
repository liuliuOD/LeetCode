![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1420. [Build Array Where You Can Find The Maximum Exactly K Comparisons](https://leetcode.com/problems/build-array-where-you-can-find-the-maximum-exactly-k-comparisons)

### Solution :

Method 1 (DFS + Memoization) :
```python
MOD = 1_000_000_007
class Solution:
    def numOfArrays(self, n: int, m: int, k: int) -> int:
        memoization = defaultdict(int)
        return self.dfs(0, 0, 0, memoization, n, m, k)

    def dfs(self, index_n: int, index_m: int, index_k: int, memoization: Dict[str, int], n: int, m: int, k: int) -> int:
        key = self.key(index_n, index_m, index_k)
        if key in memoization:
            return memoization[key]

        if index_n == n:
            # 0 or 1
            return index_k == k

        result = index_m * self.dfs(index_n+1, index_m, index_k, memoization, n, m, k) % MOD
        if index_k+1 <= k:
            for index_m_next in range(index_m+1, m+1):
                # Option 1
                result += self.dfs(index_n+1, index_m_next, index_k+1, memoization, n, m, k)
                result %= MOD
                """
                # Option 2

                result = (result + self.dfs(index_n+1, index_m_next, index_k+1, memoization, n, m, k)) % MOD
                """

        memoization[key] = result
        return result

    def key(self, index_n: int, index_m: int, index_k: int) -> str:
        # n: amount of list item, m: range of list item value, k: result of execution by using function in the problem description
        return f'{index_n}-{index_m}-{index_k}'
```

Method 2 ([Dynamic Programming](https://leetcode.com/problems/build-array-where-you-can-find-the-maximum-exactly-k-comparisons/?envType=daily-question&envId=2023-10-07), Time Complexity: $O(M^2*N*K)$) :
```python
MOD = 1_000_000_007

class Solution:
    def numOfArrays(self, n: int, m: int, k: int) -> int:
        dp = defaultdict(int)
        for value_maximum in range(1, m + 1):
            dp[self.key(1, value_maximum, 1)] = 1

        for amount in range(1, n + 1):
            for value_maximum in range(1, m + 1):
                for index_k in range(1, k + 1):
                    key_current = self.key(amount, value_maximum, index_k)
                    dp[key_current] = (dp[key_current] + value_maximum*dp[self.key(amount-1, value_maximum, index_k)]) % MOD

                    for value_lower in range(1, value_maximum):
                        dp[key_current] = (dp[key_current] + dp[self.key(amount-1, value_lower, index_k-1)]) % MOD

        result = 0
        for value in range(1, m+1):
            result = (result + dp[self.key(n, value, k)]) % MOD

        return result

    def key(self, index_n: int, index_m: int, index_k: int) -> str:
        return f'{index_n}-{index_m}-{index_k}'
```
