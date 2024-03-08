![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1143. [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence)

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(M*N), Space Complexity: $O(M*N)$) :
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        memoization = defaultdict(int)
        return self.dfs(0, 0, memoization, text1, text2)

    def dfs(self, index1: int, index2: int, memoization: Dict, text1: str, text2: str) -> int:
        n1 = len(text1)
        n2 = len(text2)
        if index1 >= n1 or index2 >= n2:
            return 0

        key = (index1, index2)
        if key in memoization:
            return memoization[key]

        if text1[index1] == text2[index2]:
            result = 1 + self.dfs(index1+1, index2+1, memoization, text1, text2)
        else:
            result = max(self.dfs(index1+1, index2, memoization, text1, text2), self.dfs(index1, index2+1, memoization, text1, text2))

        memoization[key] = result
        return memoization[key]
```

Method 2 (DFS + Memoization, Time Complexity: $O(M*N), Space Complexity: $O(M*N)$) :
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        memoization = defaultdict(int)
        return self.dfs(len(text1)-1, len(text2)-1, memoization, text1, text2)

    def dfs(self, index1: int, index2: int, memoization: Dict, text1: str, text2: str) -> int:
        if index1 < 0 or index2 < 0:
            return 0

        key = (index1, index2)
        if key in memoization:
            return memoization[key]

        if text1[index1] == text2[index2]:
            result = 1 + self.dfs(index1-1, index2-1, memoization, text1, text2)
        else:
            result = max(self.dfs(index1-1, index2, memoization, text1, text2), self.dfs(index1, index2-1, memoization, text1, text2))

        memoization[key] = result
        return memoization[key]
```

Method 3 (Dynamic Programming, Time Complexity: $O(M*N), Space Complexity: $O(M*N)$) :
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m = len(text1) + 1
        n = len(text2) + 1
        dp = [[0] * n for _ in range(m)]
        for index_m in range(1, m):
            for index_n in range(1, n):
                if text1[index_m-1] == text2[index_n-1]:
                    dp[index_m][index_n] = 1 + dp[index_m-1][index_n-1]
                else:
                    dp[index_m][index_n] = max(dp[index_m-1][index_n], dp[index_m][index_n-1])

        return dp[-1][-1]
```
