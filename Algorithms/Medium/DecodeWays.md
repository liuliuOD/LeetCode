![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 91. [Decode Ways](https://leetcode.com/problems/decode-ways)

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def numDecodings(self, s: str) -> int:
        memoization = defaultdict(int)
        return self.dfs(-1, memoization, s)

    def dfs(self, index: int, memoization: Dict[int, int], s: str) -> int:
        if index in memoization:
            return memoization[index]

        if index >= len(s)-1:
            return 1

        if s[index+1] == '0':
            return 0

        result = self.dfs(index+1, memoization, s)
        #  index+1 = latest or s[index+1 ~ index+2] > 26
        if index < len(s)-2 and int(s[index+1:index+3]) <= 26:
            result += self.dfs(index+2, memoization, s)

        memoization[index] = result
        return result
```

Method 2 (DFS + Memoization) :
```python
class Solution:
    def numDecodings(self, s: str) -> int:
        memoization = defaultdict(int)

        return self.dfs(0, memoization, s)

    def dfs(self, index: int, memoization: Dict[int, int], s: str) -> int:
        if index >= len(s):
            return 1

        if index in memoization:
            return memoization[index]

        result = 0
        if s[index] != '0':
            result = self.dfs(index+1, memoization, s)
        if index+1 < len(s) and (s[index] == '1' or (s[index] =='2' and s[index+1] in ['0', '1', '2', '3', '4', '5', '6',])):
            result += self.dfs(index+2, memoization, s)

        memoization[index] = result
        return result
```

Method 3 (Dynamic Programming) :
```python
class Solution:
    def numDecodings(self, s: str) -> int:
        n = len(s)
        dp = [0] * (n+1)
        dp[0] = 1
        for index_dp in range(1, n+1):
            index_s = index_dp - 1
            if s[index_s] != '0':
                dp[index_dp] += dp[index_dp-1]

            if index_s > 0 and s[index_s-1] != '0' and int(s[index_s-1:index_s+1]) <= 26:
                dp[index_dp] += dp[index_dp-2]

        return dp[n]
```
