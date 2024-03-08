![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 62. [Unique Paths](https://leetcode.com/problems/unique-paths)

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        memoization = defaultdict(int)
        return self.dfs(0, 0, memoization, m, n)

    def dfs(self, index_m: int, index_n: int, memoization: Dict[str, int], m: int, n: int) -> int:
        key = self.getKey(index_m, index_n)

        if key in memoization:
            return memoization[key]

        if index_m == 0 or index_n == 0:
            memoization[key] = 1

        if index_m == m-1 and index_n == n-1:
            return 1

        if index_m >= m or 0 > index_m or index_n >= n or 0 > index_n:
            return 0

        memoization[key] = self.dfs(index_m+1, index_n, memoization, m, n) + self.dfs(index_m, index_n+1, memoization, m, n)
        return memoization[key]

    def getKey(self, index_m: int, index_n: int) -> str:
        return f'{index_m}-{index_n}'
```

Method 2 (Dynamic Programming, 2D) :
```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[0]*n for _ in range(m)]
        dp[0] = [1] * n
        for index_m in range(1, m):
            dp[index_m][0] = 1
            for index_n in range(1, n):
                dp[index_m][index_n] = dp[index_m-1][index_n] + dp[index_m][index_n-1]

        return dp[-1][-1]
```

Method 3 (Dynamic Programming, 1D) :
```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [1] * n
        for _ in range(1, m):
            for index_n in range(1, n):
                dp[index_n] = dp[index_n] + dp[index_n-1]
        return dp[-1]
```

### Solution :

Method 1 (Dynamic Programming, 1D) :
```php
class Solution {

    /**
     * @param Integer $m
     * @param Integer $n
     * @return Integer
     */
    function uniquePaths($m, $n) {
        $dp = array_fill(0, $n, 1);
        for ($_ = 1; $_ < $m; $_++) {
            for ($indexN = 1; $indexN < $n; $indexN++) {
                $dp[$indexN] += $dp[$indexN-1];
            }
        }

        return $dp[$n-1];
    }
}
```
